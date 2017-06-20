# CEK 메시지 포맷
CEK와 extension이 통신할 때 HTTP/1.1 프로토콜을 사용하며, 기본적인 HTTPS 요청과 HTTPS 응답을 주고 받습니다. CEK와 extension이 서로 통신할 때 HTTP 메시지 본문(body)에는 JSON 포맷의 CEK 메시지가 포함되어 있습니다. 이 CEK 메시지는 extension의 종류에 따라 사용해야 하는 CEK 메시지 포맷이 다릅니다. 여기에서는 HTTP 메시지 포맷과 extension 종류별 CEK 메시지 포맷에 대해 설명합니다.

* [HTTP 메시지](#HTTPMessage)
* [Custom extension 메시지](#CustomExtenstionMessage)
* [Clova Home extension 메시지](#ClovaHomeExtensionMessage)

## HTTP 메시지 {#HTTPMessage}
여기에서는 CEK와 extension 사이에 HTTP 메시지가 어떻게 구성되는지 설명합니다.

### HTTP 헤더 {#HTTPHeader}
CEK가 extension으로 분석된 사용자의 발화 정보를 보낼 때 HTTPS 요청을 사용합니다. 이때 HTTPS 요청 헤더는 다음과 같이 구성됩니다.

{% raw %}
```
POST /APIpath HTTP/1.1
Host : your.extension.endpoint
Content-Type: application/json;charset-UTF-8
Accept :  application/json
Accept-Charset : utf-8
```
{% endraw %}

* HTTP/1.1 버전으로 HTTPS 통신을 수행하며, method로 POST 방식을 사용합니다.
* Host와 요청 대상 path는 extension 개발자가 미리 정의해 둔 URI로 채워집니다.
* 본문의 데이터 형식은 JSON 포맷으로 되어 있으며, UTF-8 인코딩을 사용합니다.


이와 반대로 extension이 CEK로 처리 결과를 보낼 때 HTTPS 응답을 사용합니다. 이때 HTTPS 응답 헤더는 다음과 같이 기본적인 것만 구성하면 됩니다.
{% raw %}
```
HTTP/1.1 200 OK
Content-Type: application/json;charset-UTF-8
```
{% endraw %}
* CEK가 보낸 HTTPS 요청에 대한 응답으로 처리 결과를 전달합니다.
* 본문의 데이터 형식은 JSON 포맷으로 되어 있으며, UTF-8 인코딩을 사용합니다.

### HTTP 본문 {#HTTPBody}
HTTPS 요청 메시지와 응답 메시지의 본문은 JSON 포맷이며, 분석된 사용자의 발화 정보나 entension의 처리 결과가 담긴 정보입니다. 각 메시지의 구성은 어떤 종류의 extension을 사용하느냐에 따라 달라집니다. 메시지의 구성에 대한 자세한 정보는 [Custom extension 메시지](#CustomExtenstionMessage)와 [Clova Home extension 메시지](#ClovaHomeExtensionMessage)를 참조합니다.

## Custom extension 메시지 {#CustomExtenstionMessage}
Custom extension 메시지는 CEK와 Custom extension 사이에서 정보를 주고 받을 때 사용하는 메시지입니다. Custom extension 메시지는 [요청 메시지](#RequestMessage)와 [응답 메시지](#ResponseMessage)로 나뉩니다.

### 요청 메시지 {#RequestMessage}
CEK는 Clova가 분석한 사용자의 요구 사항을 Custom extension으로 전달할 때 요청 메시지를 전달합니다(HTTPS Request). 여기에서는 요청 메시지의 구조, 각 필드의 설명, 그리고 요청 타입과 각 타입에 따라 달라지는 *request* 필드에 대해 설명합니다.

#### Message format
JSON 포맷의 메시지는 이벤트 메시지 정보를 담고 있거나 또는 콘텐츠 정보를 담을 때 사용됩니다. JSON 형식의 데이터를 보낼 때 메시지는 다음 예처럼 헤더와 본문으로 구성됩니다.

{% raw %}
```json
{
  "context": {
    "AudioPlayer": {
      "offsetInMilliseconds": {{number}},
      "playerActivity": {{string}},
      "stream": {{AudioStreamObject}},
      "totalInMilliseconds": {{number}},
    },
    "System": {
      "device": {
        "deviceId": {{string}}
      },
      "user": {
        "userId": {{string}},
        "accessToken": {{string}}
      }
    }
  },
  "request": {{object}},
  "session": {
    "new": {{bolean}},
    "sessionId": {{string}},
    "user": {
      "userId": {{string}},
      "accessToken": {{string}}
    }
  },
  "version": {{string}}
}
```
{% endraw %}

### Message field
| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|---------|
| context                                  | obejct  | 클라이언트의 맥락 정보를 가지고 있는 객체                                | 필수 |
| context.AudioPlayer                      | obejct  | 클라이언트가 현재 재생하고 있거나 마지막으로 재생한 미디어 정보를 가지고 있는 객체 | 선택 |
| context.AudioPlayer.offsetInMilliseconds | number  | 최근 재생 미디어의 마지막 재생 지점(offset). 단위는 밀리초이며, *playerActivity* 값이 "IDLE"이면 이 필드 값이 비어 있을 수도 있습니다.                                       | 선택 |
| context.AudioPlayer.playerActivity       | string  | 플레이어의 상태를 나타내는 값이며 다음과 같은 값을 가집니다.<ul><li>IDLE: 비활성 상태</li><li>PLAYING: 재생 중인 상태</li><li>PAUSED: 일시 정지 상태</li><li>STOPPED: 중지 상태</li></ul> | 필수 |
| context.AudioPlayer.stream               | [AudioStreamObject](/CIC/References/APIs/AudioPlayer.md#AudioStreamObject) | 재생 중인 미디어의 상세 정보를 보관한 객체. *playerActivity* 값이 "IDLE"이면 이 필드 값이 비어 있을 수도 있습니다.    | 선택 |
| context.AudioPlayer.totalInMilliseconds  | number  | 최근 재생 미디어의 전체 길이. 단위는 밀리초이며, *playerActivity* 값이 "IDLE"이면 이 필드 값이 비어 있을 수도 있습니다.                                                                  | 선택 |
| context.System                           | obejct  | 클라이언트 시스템의 맥락 정보를 가지고 있는 객체                          | 필수 |
| context.System.device                    | object  | 클라이언트 기기의 정보를 가지고 있는 객체                               | 필수 |
| context.System.device.deviceId           | string  | 클라이언트 기기 ID. 모델명과 기기 시리얼 번호가 조합된 정보와 같이 사용자 기기를 식별할 수 있는 정보가 전달됩니다. | 필수 |
| context.System.user                      | obejct  | 클라이언트 기기에 인증된 기본 사용자 정보를 가지고 있는 객체                 | 필수 |
| context.System.user.userId               | string  | 기기 기본 사용자의 Clova ID                                    | 필수 |
| context.System.user.accessToken          | string  | 특정 서비스의 사용자 계정의 access token. 기기 기본 사용자와 연결된 사용자 계정의 access token이 전달됩니다. CEK는 외부 서비스의 인증 서버로부터 획득한 사용자 계정의 access token을 전달합니다. 자세한 설명은 [사용자 계정 연결하기](/CEK/Guides/LinkUserAccount.md)를 참조합니다. | 필수 |
| request                                  | object  | 분석된 사용자의 발화 정보를 가지고 있는 객체. [요청 타입](#RequestType)에 따라 구성되는 필드가 달라집니다. | 필수 |
| session                                  | object  | 세션 정보를 가지고 있는 객체. 여기서 세션은 사용자의 요청을 구분하는 논리적 단위입니다.     | 필수 |
| session.new                              | boolean | 요청 메시지가 새로운 세션에 대한 것인지 아니면 기존 세션에 대한 것인지 구분합니다. <ul><li>true: 새로운 세션</li><li>false: 기존 세션</li></ul>  | 필수 |
| session.sessionId                        | string  | 세션 ID                                                    | 필수 |
| session.user                             | object  | 현재 사용자의 정보를 가지고 있는 객체.                             | 필수 |
| session.user.userId                      | string  | 현재 사용자의 Clova ID. *context.System.user.userId* 값과 다를 수 있습니다. | 필수 |
| session.user.accessToken                 | string  | 특정 서비스의 사용자 계정의 access token. 현재 사용자와 연결된 사용자 계정의 access token이 전달됩니다. CEK는 외부 서비스의 인증 서버로부터 획득한 사용자 계정의 access token을 전달합니다. 자세한 설명은 [사용자 계정 연결하기](/CEK/Guides/LinkUserAccount.md)를 참조합니다.| 선택 |
| version                                  | string  | CEK 메시지 버전                                              | 필수 |


### Request type {#RequestType}
요청 메시지는 다음과 같이 3가지 요청 타입으로 나뉘며, 각 요청 타입마다 요청 메시지의 *request* 객체의 필드 구성이 달라집니다.
* [LaunchRequest](#LaunchRequest)
* [IntentRequest](#IntentRequest)
* [SessionEndedRequest](#SessionEndedRequest)

#### LaunchRequest {#LaunchRequest}
*LaunchRequest* 타입은 사용자의 특정 extension 사용 시작을 알리는 요청 타입입니다. 예를 들면, 사용자가 "영어 대화 시작하자"라고 말한 것과 같이 특정 모드로 진입하겠다고 선언한 상황입니다. 주로 특정 모드로 진입해야 되는 서비스를 제공하는 extension이 이 타입의 메시지를 받게 됩니다.

*LaunchRequest* 타입 메시지의 *request* 객체 필드 구성은 다음과 같습니다.

{% raw %}
```json
{
  "type": "LaunchRequest"
}
```
{% endraw %}

| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|---------|
| type          | string  | 요청 메시지의 타입. "LaunchRequest" 값으로 고정됩니다. | 필수 |

다음은 LaunchRequest 타입의 요청 메시지 예제입니다.

#### IntentRequest {#IntentRequest}
*IntentRequest* 타입은 분석한 사용자의 정보를 전달하여 그 내용을 수행하도록 하는 요청 타입입니다. Extension 개발자는 서비스를 만들 때 사용자의 요청을 어떻게 받고 처리할지 Clova Developer Console을 이용하여 Interaction 모델을 등록해야 합니다. 이때, 구별되는 사용자의 요청을 Intent라는 정보 형태로 정의합니다. 분석된 사용자의 발화 정보는 Intent로 변환되며, *intent* 필드를 통해 extension에게 전달됩니다.

<div class="note">
  <p><strong>Note!</strong></p>
  <p>현재 Clova Developer Console을 개발하는 중입니다. 따라서, Interaction 모델을 정의하려면 제휴 담당자와 협의하기 바랍니다.</p>
</div>

*IntentRequest* 타입 메시지의 *request* 객체 필드 구성은 다음과 같습니다.

{% raw %}
```json
{
  "type": "IntentRequest",
  "intent": {
    "name": {{string}},
    "slots": {{object}}
  }
}
```
{% endraw %}

| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|---------|
| type          | string  | 요청 메시지의 타입. "IntentRequest" 값으로 고정됩니다.                                                           | 필수 |
| intent        | object  | 사용자의 요청을 분석한 정보가 저장된 객체 (intent)                                                                | 필수 |
| intent.name   | string  | Intent 이름. Interaction 모델에 정의한 intent를 이 필드로 식별할 수 있다.                                          | 필수 |
| intent.slots  | object  | Extension이 intent를 처리할 때 요구되는 정보(slot)가 저장된 객체. 이 필드는 *intent.name* 필드에 따라 구성이 달라질 수 있다. | 필수 |


#### SessionEndedRequest {#SessionEndedRequest}
*SessionEndedRequest* 타입은 사용자의 특정 extension 사용이 종료되었음을 알리는 요청입니다. 다음과 같은 상황에서 이 메시지를 받게 됩니다.
* 사용자가 종료를 요청한 경우
* 특정 시간 동안 사용자의 입력이 없을 경우(Timeout)
* 오류가 발생한 경우

<div class="note">
  <p><strong>Note!</strong></p>
  <p><a href="ResponseMessage">응답 메시지</a>의 <em>shouldEndSession</em> 필드를 사용하여 extension 쪽에서 먼저 종료를 선언한 경우 이 메시지를 수신하지 않습니다.</p>
</div>


*SessionEndedRequest* 타입 메시지의 *request* 객체 필드 구성은 다음과 같습니다.

{% raw %}
```json
{
  "type": "EndRequest"
}
```
{% endraw %}

| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|---------|
| type          | string  | 요청 메시지의 타입. "EndRequest" 값으로 고정됩니다. | 필수 |

#### Message example
{% raw %}
```json
// 예제 1: LaunchRequest 타입
{
  "version": "0.1.0",
  "session": {
    "new": true,
    "sessionId": "a29cfead-c5ba-474d-8745-6c1a6625f0c5",
    "user": {
      "userId": "V0qe",
      "accessToken": "XHapQasdfsdfFsdfasdflQQ7"
    }
  },
  "context": {
    "System": {
      "user": {
        "userId": "V0qe",
        "accessToken": "XHapQasdfsdfFsdfasdflQQ7"
      },
      "device": {
        "deviceId": "096e6b27-1717-33e9-b0a7-510a48658a9b"
      }
    }
  },
  "request": {
    "type": "LaunchRequest"
  }
}

// 예제 2: IntentRequest 타입
{
  "version": "0.1.0",
  "session": {
    "new": false,
    "sessionId": "a29cfead-c5ba-474d-8745-6c1a6625f0c5",
    "user": {
      "userId": "V0qe",
      "accessToken": "XHapQasdfsdfFsdfasdflQQ7"
    }
  },
  "context": {
    "System": {
      "user": {
        "userId": "V0qe",
        "accessToken": "XHapQasdfsdfFsdfasdflQQ7"
      },
      "device": {
        "deviceId": "096e6b27-1717-33e9-b0a7-510a48658a9b"
      }
    }
  },
  "request": {
    "type": "IntentRequest",
    "intent": {
      "name": "FreeTalk",
      "slots": {
        "q": {
          "name": "q",
          "value": "How are you"
        }
      }
    }
  }
}

// 예제 3: SessionEndedRequest 타입
{
  "version": "0.1.0",
  "session": {
    "new": false,
    "sessionId": "a29cfead-c5ba-474d-8745-6c1a6625f0c5",
    "user": {
      "userId": "V0qe",
      "accessToken": "XHapQasdfsdfFsdfasdflQQ7"
    }
  },
  "context": {
    "System": {
      "user": {
        "userId": "V0qe",
        "accessToken": "XHapQasdfsdfFsdfasdflQQ7"
      },
      "device": {
        "deviceId": "096e6b27-1717-33e9-b0a7-510a48658a9b"
      }
    }
  },
  "request": {
    "type": "EndRequest"
  }
}
```
{% endraw %}

### See also
* [Custom extension 요청 처리하기](/CEK/Guides/Build_Custom_Extension.md#HandleCustomExtensionRequest)
* [이벤트 메시지](/CIC/References/CIC_Message_Format.md#Event)
* [AudioStreamObject](/CIC/References/APIs/AudioPlayer.md#AudioStreamObject)

### 응답 메시지 {#ResponseMessage}
Extension은 요청 메시지를 처리한 후 응답 메시지를 전달해야 합니다(HTTPS Response). 여기에서는 응답 메시지의 구조와 각 필드에 대해 설명합니다.

#### Message format
{% raw %}
```json
{
  "response": {
    "card": {{object}},
    "directives": [
      {
        "header": {
          "messageId": {{string}},
          "name": {{string}},
          "namespace": {{string}}
        },
        "payload": {{object}}
      }
    ],
    "outputSpeech": {
          "lang": {{string}},
          "pause": {{string}},
          "text": {{string}},
          "type": {{string}}
    },
    "shouldEndSession": {{boolean}},
  },
  "sessionAttibutes": {{object}},
  "version": {{string}}
}
```
{% endraw %}

### Message field
| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|---------|
| response                               | object       | Extension의 응답 정보가 담긴 객체                            | 필수 |
| response.card                          | object       | [Content Template](/CIC/References/Content_Templates.md) 형태의 데이터이며, 클라이언트 화면에 표시할 콘텐트를 이 필드를 통해 전달할 수 있습니다.           | 필수 |
| response.directives[]                  | object array | Extension이 CEK로 전달하는 지시 메시지입니다. *response.directives* 필드에서 사용할 지시 메시지는 추후 API를 제공할 예정입니다. | 필수 |
| response.directives[].header           | object       | 지시 메시지의 헤더                                          | 필수 |
| response.directives[].header.messageId | string       | 메시지 ID. 개별 메시지를 구분하기 위해 사용하는 식별자입니다(UUID).   | 필수 |
| response.directives[].header.name      | string       | 지시 메시지의 API 이름                                      | 필수 |
| response.directives[].header.namespace | string       | 지시 메시지의 API 네임스페이스                                | 필수 |
| response.directives[].payload          | object       | 지시 메시지와 관련된 정보를 담고 있는 객체. 지시 메시지에 따라 payload 객체의 구성과 필드 값을 달리 작성할 수 있습니다.         | 필수 |
| response.outputSpeech                  | object       | 사용자에게 발화할 정보를 담고 있는 객체.                         | 필수 |
| response.outputSpeech[].lang           | string       | 음성 합성을 할 때 사용할 언어의 코드. 현재 다음과 같은 값을 가집니다.<ul><li>"ko": 한국어</li><li>"en": 영어</li></ul>         | 필수 |
| response.outputSpeech[].pause          | string       | 발화 지연 시간. 이전 발화 메시지의 음성 출력이 끝나면 지정한 시간만큼 기다렸다가 음성이 출력되도록 설정합니다. 단위는 밀리초(millisecond)입니다. | 필수 |
| response.outputSpeech[].text           | string       | 음성 합성할 내용                                           | 필수 |
| response.outputSpeech[].type           | string       | 현재는 "PlainText"를 고정으로 입력해야 합니다.                  | 필수 |
| response.shouldEndSession              | boolean      | 세션 종료 플래그. 클라이언트에게 특정 extension 사용이 종료됨을 알리는 필드입니다. [SessionEndedRequest](#SessionEndedRequest) 타입의 요청 메시지를 받기 전에 extension이 먼저 사용 종료를 알릴 때 사용합니다.<ul><li>true : 사용 종료</li><li>false : 계속 사용</li></ul> | 필수 |
| sessionAttributes                      | object       | 추후 확장을 위해 예약해 둔 필드                                 | 필수 |
| version                                | string       | CEK 메시지의 버전                                          | 필수 |

<div class="note">
  <p><strong>Note!</strong></p>
  <p><em>response.directives</em> 필드를 통해 extension 임의의 지시 메시지를 전달해야 하는 경우 사용하려면 사전 협의가 필요합니다. 제휴 담당자와 협의하기 바랍니다.</p>
</div>

### Message example
{% raw %}
```json
{
  "version": "0.1.0",
  "sessionAttributes": {},
  "response": {
    "outputSpeech": [
      {
        "type": "PlainText",
        "text": "You are back. I want to know more about you. Do you go to school?",
        "pause": "500",
        "lang": "en"
      }
    ],
    "card": {},
    "directives": [],
    "shouldEndSession": false
  }
}
```
{% endraw %}

### See also
* [Custom extension 응답 반환하기](/CEK/Guides/Build_Custom_Extension.md#ReturnCustomExtensionResponse)
* [Content Template](/CIC/References/Content_Templates.md)

## Clova Home extension 메시지 {#ClovaHomeExtensionMessage}
Clova Home extension 메시지는 IoT 기기를 제어하는 extension이 CEK와 정보를 주고 받을 때 전용으로 사용하는 메시지입니다. Clova Home extension 메시지는 *header* 필드와 *payload* 필드로 구성되어 있으며, 이는 요청 메시지와 응답 메시지 모두 동일합니다. 이 중에서 *payload* 필드는 사용된 [Clova Home API](/CEK/References/Clova_Home_API.md)에 따라 그 구성이 달라질 수 있습니다. 여기에서는 Clova Home extension 메시지의 공통된 포맷에 대해 설명합니다.

<div class="note">
  <p><strong>Note!</strong></p>
  <p>Clova Home extension 메시지는 API에 따라 요청 메시지와 응답 메시지로 구분됩니다. CEK가 extension으로 보내는 요청 메시지는 XxxxRequest와 같은 이름을 가진 API이며, extension이 CEK로 보내는 응답 메시지는 XxxxConfirmation이나 XxxxResponse 형태의 이름을 가집니다. 또한, 오류 상황에도 정상적인 HTTPS 응답(200 OK)을 보내야 하며, 이때 XxxxError와 같은 이름의 API를 사용해서 응답 메시지를 보내야 합니다.</p>
</div>

### Message format
{% raw %}
```json
{
  "header": {
    "messageId": {{string}},
    "namespace": {{string}},
    "name": {{string}},
    "payloadVersion": {{string}}
    },
    "payload": {{object}}
  }
}
```
{% endraw %}


### Message field
| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|---------|
| header                 | object | Clova Home extension 메시지의 헤더                                          | 필수     |
| header.messageId       | string | 메시지 ID. 개별 메시지를 구분하기 위해 Clova에서 생성한 식별자입니다(UUID).               | 필수     |
| header.name            | string | Clova Home extension 메시지의 API 이름                                      | 필수     |
| header.namespace       | string | 이 필드는 "ClovaHome"으로 고정됩니다.                                          | 필수     |
| header.payloadVersion  | string | *header.name*에 명시된 Clova Home API의 버전. 이 버전에 따라 *payload* 필드의 구성이 달라질 수 있습니다.                                   | 필수     |
| payload                | object | *header.name*에 지정된 [Clova Home API](/CEK/References/Clova_Home_API.md)에 따라 payload 객체의 구성과 필드 값이 달라집니다. | 필수     |

### Message example
{% raw %}
```json
예제 1: DiscoverAppliancesRequest API - 요청 메시지
{
  "header": {
    "messageId": "8ddd7f05-7703-4cb4-a6dd-93c209c6647b",
    "name": "DiscoverAppliancesRequest",
    "namespace": "ClovaHome",
    "payloadVersion": "1.0"
  },
  "payload": {
    "accessToken": "92ebcb67fe33"
  }
}

예제 2: DiscoverAppliancesResponse API - 응답 메시지
{
  "header": {
    "messageId": "99f9d8ff-9366-4cab-a90c-b4c7eca0abbe",
    "name": "DiscoverAppliancesResponse",
    "namespace": "ClovaHome",
    "payloadVersion": "1.0"
  },
  "payload": {
    "discoveredAppliances": [
      {
        "applianceId": "device-001",
        "manufacturerName": "device-manufacturer-name",
        "modelName": "스마트 전등",
        "version": "v1.0",
        "friendlyName": "거실 전등",
        "friendlyDescription": "스마트폰으로 제어할 수 있는 전등",
        "isReachable": true,
          "actions": [
            "TurnOn",
            "TurnOff"
        ],
        "applianceTypes": ["LIGHT"],
        "additionalApplianceDetails": {
        }
      },
      {
        "applianceId": "device-002",
        "manufacturerName": "device-manufacturer-name",
        "modelName": "스마트 플러그",
        "version": "v1.0",
        "friendlyName": "부엌 플러그",
        "friendlyDescription": "에너지를 절약하는 플러그",
        "isReachable": true,
        "actions": [
          "TurnOn",
          "TurnOff"
        ],
        "applianceTypes": ["SMARTPLUG"],
        "additionalApplianceDetails": {
        }
      }
    ]
  }
}

예제 3: IncrementTargetTemperatureConfirmation API - 응답 메시지
{
  "header": {
    "messageId": "4ec35000-88ce-4724-b7e4-7f52050558fd",
    "name": "IncrementTargetTemperatureConfirmation",
    "namespace": "ClovaHome",
    "payloadVersion": "1.0"
  },
  "payload": {
    "targetTemperature": {
      "value": 25.0
    },
    "previousState": {
      "targetTemperature": {
        "value": 22.0
      }
    }
  }
}

예제 4: TargetOffLineError API - 오류 응답 메시지
{
  "header": {
    "messageId": "fef949b7-eb94-4bda-a417-2cfb604194c3",
    "namespace": "ClovaHome",
    "name": "TargetOfflineError",
    "payloadVersion": "1.0"
  },
  "payload": {
  }
}
```
{% endraw %}

### See also
* [Clova Home extension 만들기](/CEK/Guides/Build_Clova_Home_Extension.md)
* [API](/CEK/References/CEK_API.md)
