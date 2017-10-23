## Custom extension 메시지 {#CustomExtMessage}
Custom extension 메시지는 CEK와 custom extension 사이에서 정보를 주고 받을 때 사용하는 메시지입니다. Custom extension 메시지는 [요청 메시지](#CustomExtRequestMessage)와 [응답 메시지](#CustomExtResponseMessage)로 나뉩니다. 요청 메시지는 다시 [요청 타입](#CustomExtRequestType)에 따라 `LaunchRequest`, `IntentRequest`, `SessionEndedRequest`과 같이 3가지 타입으로 구분됩니다.

### 요청 메시지 {#CustomExtRequestMessage}
CEK는 Clova가 분석한 사용자의 요구 사항을 custom extension으로 전달할 때 요청 메시지를 전달합니다(HTTPS Request). 여기에서는 요청 메시지의 구조, 각 필드의 설명, 그리고 요청 타입과 각 타입에 따라 달라지는 `request` 필드에 대해 설명합니다.

#### Message structure

{% raw %}
```json
{
  "context": {
    "AudioPlayer": {
      "offsetInMilliseconds": {{number}},
      "playerActivity": {{string}},
      "stream": {{AudioStreamInfoObject}},
      "totalInMilliseconds": {{number}},
    },
    "System": {
      "device": {
        "deviceId": {{string}},
        "displayType": {{string}}
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
    "sessionAttributes": {{object}},
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

#### Message field
| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|---------|
| `context`                                  | object  | 클라이언트의 맥락 정보를 가지고 있는 객체                                | 필수 |
| `context.AudioPlayer`                      | object  | 클라이언트가 현재 재생하고 있거나 마지막으로 재생한 미디어 정보를 가지고 있는 객체 | 선택 |
| `context.AudioPlayer.offsetInMilliseconds` | number  | 최근 재생 미디어의 마지막 재생 지점(offset). 단위는 밀리초이며, `playerActivity` 값이 "IDLE"이면 이 필드 값이 비어 있을 수도 있습니다.                                       | 선택 |
| `context.AudioPlayer.playerActivity`       | string  | 플레이어의 상태를 나타내는 값이며 다음과 같은 값을 가집니다.<ul><li><code>"IDLE"</code> : 비활성 상태</li><li><code>"PLAYING"</code> : 재생 중인 상태</li><li><code>"PAUSED"</code> : 일시 정지 상태</li><li><code>"STOPPED"</code> : 중지 상태</li></ul> | 필수 |
| `context.AudioPlayer.stream`               | [AudioStreamInfoObject](/CIC/References/CICInterface/AudioPlayer.md#AudioStreamInfoObject) | 재생 중인 미디어의 상세 정보를 보관한 객체. `playerActivity` 값이 `"IDLE"`이면 이 필드 값이 비어 있을 수도 있습니다.    | 선택 |
| `context.AudioPlayer.totalInMilliseconds`  | number  | 최근 재생 미디어의 전체 길이. 단위는 밀리초이며, `playerActivity` 값이 "IDLE"이면 이 필드 값이 비어 있을 수도 있습니다.                                                                  | 선택 |
| `context.System`                           | object  | 클라이언트 시스템의 맥락 정보를 가지고 있는 객체                          | 필수 |
| `context.System.device`                    | object  | 클라이언트 기기의 정보를 가지고 있는 객체                               | 필수 |
| `context.System.device.deviceId`           | string  | 클라이언트 기기 ID. 모델명과 기기 시리얼 번호가 조합된 정보와 같이 사용자 기기를 식별할 수 있는 정보가 전달됩니다. | 필수 |
| `content.System.device.displayType`        | string  | 클라이언트 기기의 디스플레이 종류이며 다음과 같은 값을 가집니다.<ul><li>빈 문자열(<code>""</code>) : 클라이언트 기기에 디스플레이 장치가 없음</li><li><code>"s100"</code> : 소형 화면(small type, 160px X 107px)</li><li><code>"m100"</code> : 중형 화면(medium type, 427px X 240px)</li><li><code>"l100"</code> : 대형 화면(large type, 640px X 360px)</li><li><code>"xl100"</code> : 초대형 화면(xlarge type, 899px X 506px)</li></ul> <div class="note"><p><strong>Note!</strong></p><p>클라이언트 기기의 화면 해상도에 맞거나 화면 해상도와 같은 비율의 콘텐츠를 제공해야 합니다.</p></div>| 필수 |
| `context.System.user`                      | object  | 클라이언트 기기에 인증된 기본 사용자 정보를 가지고 있는 객체                 | 필수 |
| `context.System.user.userId`               | string  | 기기 기본 사용자의 Clova ID                                    | 필수 |
| `context.System.user.accessToken`          | string  | 특정 서비스의 사용자 계정의 access token. 기기 기본 사용자와 연결된 사용자 계정의 access token이 전달됩니다. CEK는 외부 서비스의 인증 서버로부터 획득한 사용자 계정의 access token을 전달합니다. 자세한 설명은 [사용자 계정 연결하기](/CEK/Guides/LinkUserAccount.md)를 참조합니다. | 필수 |
| `request`                                 | object  | 분석된 사용자의 발화 정보를 가지고 있는 객체. [요청 타입](#CustomExtRequestType)에 따라 구성되는 필드가 달라집니다. | 필수 |
| `session`                                  | object  | 세션 정보를 가지고 있는 객체. 여기서 세션은 사용자의 요청을 구분하는 논리적 단위입니다.     | 필수 |
| `session.new`                              | boolean | 요청 메시지가 새로운 세션에 대한 것인지 아니면 기존 세션에 대한 것인지 구분합니다. <ul><li>true: 새로운 세션</li><li>false: 기존 세션</li></ul>  | 필수 |
| `session.sessionAttributes`                       | object  | 사용자와의 multi-turn 대화를 위해 필요한 정보를 저장해둔 객체. Custom extension은 [응답 메시지](#CustomExtResponseMessage)의 `response.sessionAttributes` 필드를 이용해 중간 정보를 CEK에 전달하게 되며, 사용자의 추가 요청을 수신할 때 다시 해당 정보를 요청 메시지의 `session.sessionAttributes` 필드로 받게 됩니다. 객체는 키(key)-값(value)의 쌍으로 구성되며, custom extension을 구현할 때 임의로 정의할 수 있습니다. 저장된 값이 없으면 빈 객체가 전달됩니다.   | 필수 |
| `session.sessionId`                        | string  | 세션 ID                                                    | 필수 |
| `session.user`                            | object  | 현재 사용자의 정보를 가지고 있는 객체.                             | 필수 |
| `session.user.userId`                      | string  | 현재 사용자의 Clova ID. `context.System.user.userId` 값과 다를 수 있습니다. | 필수 |
| `session.user.accessToken`                 | string  | 특정 서비스의 사용자 계정의 access token. 현재 사용자와 연결된 사용자 계정의 access token이 전달됩니다. CEK는 외부 서비스의 인증 서버로부터 획득한 사용자 계정의 access token을 전달합니다. 자세한 설명은 [사용자 계정 연결하기](/CEK/Guides/LinkUserAccount.md)를 참조합니다.| 선택 |
| `version`                                  | string  | 메시지 포맷의 버전 (CEK 버전)                          | 필수 |

#### Message example
{% raw %}
```json
// 예제 1: LaunchRequest 타입
{
  "version": "0.1.0",
  "session": {
    "new": true,
    "sessionAttributes": {},
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
        "deviceId": "096e6b27-1717-33e9-b0a7-510a48658a9b",
        "displayType": "m100"
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
    "sessionAttributes": {},
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
        "deviceId": "096e6b27-1717-33e9-b0a7-510a48658a9b",
        "displayType": "m100"
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
    "sessionAttributes": {},
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
        "deviceId": "096e6b27-1717-33e9-b0a7-510a48658a9b",
        "displayType": "m100"
      }
    }
  },
  "request": {
    "type": "EndRequest"
  }
}
```
{% endraw %}

#### See also
* [Custom extension 요청 처리하기](/CEK/Guides/Build_Custom_Extension.md#HandleCustomExtensionRequest)
* [AudioStreamInfoObject](/CIC/References/CICInterface/AudioPlayer.md#AudioStreamInfoObject)

### 요청 타입 {#CustomExtRequestType}
요청 메시지는 다음과 같이 3가지 요청 타입으로 나뉘며, 각 요청 타입마다 요청 메시지의 `request` 객체의 필드 구성이 달라집니다.
* [`LaunchRequest`](#CustomExtLaunchRequest)
* [`IntentRequest`](#CustomExtIntentRequest)
* [`SessionEndedRequest`](#CustomExtSessionEndedRequest)

#### LaunchRequest {#CustomExtLaunchRequest}
`LaunchRequest` 타입은 사용자의 특정 extension 사용 시작을 알리는 요청 타입입니다. 예를 들면, 사용자가 "영어 대화 시작하자"라고 말한 것과 같이 특정 모드로 진입하겠다고 선언한 상황입니다. 주로 특정 모드로 진입해야 되는 서비스를 제공하는 extension이 이 타입의 메시지를 받게 됩니다.

`LaunchRequest` 타입 메시지의 `request` 객체 필드 구성은 다음과 같습니다.

{% raw %}
```json
{
  "type": "LaunchRequest"
}
```
{% endraw %}

| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|---------|
| `type`          | string  | 요청 메시지의 타입. `"LaunchRequest"` 값으로 고정됩니다. | 필수 |

다음은 LaunchRequest 타입의 요청 메시지 예제입니다.

#### IntentRequest {#CustomExtIntentRequest}
`IntentRequest` 타입은 분석한 사용자의 요청을 전달하여 그 내용을 수행하도록 하는 요청 타입입니다. Extension 개발자는 서비스를 만들 때 사용자의 요청을 어떻게 받고 처리할지 Clova Developer Console을 이용하여 Interaction 모델을 등록해야 합니다. 이때, 구별되는 사용자의 요청을 Intent라는 정보 형태로 정의합니다. 분석된 사용자의 발화 정보는 Intent로 변환되며, `intent` 필드를 통해 extension에게 전달됩니다.

<div class="note">
  <p><strong>Note!</strong></p>
  <p>현재 Clova Developer Console을 개발하는 중입니다. 따라서, Interaction 모델을 정의하려면 제휴 담당자와 협의하기 바랍니다.</p>
</div>

`IntentRequest` 타입 메시지의 `request` 객체 필드 구성은 다음과 같습니다.

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
| `type`          | string  | 요청 메시지의 타입. `"IntentRequest"` 값으로 고정됩니다.                                                       | 필수 |
| `intent`        | object  | 사용자의 요청을 분석한 정보가 저장된 객체 (intent)                                                                | 필수 |
| `intent.name`   | string  | Intent 이름. Interaction 모델에 정의한 intent를 이 필드로 식별할 수 있다.                                          | 필수 |
| `intent.slots`  | object  | Extension이 intent를 처리할 때 요구되는 정보(slot)가 저장된 객체. 이 필드는 `intent.name` 필드에 따라 구성이 달라질 수 있다. | 필수 |


#### SessionEndedRequest {#CustomExtSessionEndedRequest}
`SessionEndedRequest` 타입은 사용자의 특정 extension 사용이 종료되었음을 알리는 요청입니다. 다음과 같은 상황에서 이 메시지를 받게 됩니다.
* 사용자가 extension 종료를 요청한 경우
* 특정 시간 동안 사용자의 입력이 없을 경우(Timeout)
* 오류가 발생한 경우

<div class="note">
  <p><strong>Note!</strong></p>
  <p><a href="#CustomExtResponseMessage">응답 메시지</a>의 <code>shouldEndSession</code> 필드를 사용하여 extension 쪽에서 먼저 종료를 선언한 경우 이 메시지를 수신하지 않습니다.</p>
</div>


`SessionEndedRequest` 타입 메시지의 `request` 객체 필드 구성은 다음과 같습니다.

{% raw %}
```json
{
  "type": "EndRequest"
}
```
{% endraw %}

| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|---------|
| `type`          | string  | 요청 메시지의 타입. `"EndRequest"` 값으로 고정됩니다. | 필수 |

### 응답 메시지 {#CustomExtResponseMessage}
Extension은 요청 메시지를 처리한 후 응답 메시지를 전달해야 합니다(HTTPS Response). 여기에서는 응답 메시지의 구조와 각 필드에 대해 설명합니다.

#### Message structure
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
          "type": {{string}},
          "values": {{SpeechInfoObject|SpeechInfoObject array}},
          "brief": {{SpeechInfoObject}},
          "verbose": {
            "type" : {{string}},
            "values": {{SpeechInfoObject|SpeechInfoObject array}},
          }
    },
    "shouldEndSession": {{boolean}},
  },
  "sessionAttibutes": {{object}},
  "version": {{string}}
}
```
{% endraw %}

#### Message field
| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|---------|
| `response`                               | object       | Extension의 응답 정보가 담긴 객체                            | 필수 |
| `response.card`                          | object       | [Content template](/CIC/References/Content_Templates.md) 형태의 데이터이며, 클라이언트 화면에 표시할 콘텐트를 이 필드를 통해 전달할 수 있습니다.           | 필수 |
| `response.directives[]`                  | object array | Extension이 CEK로 전달하는 지시 메시지입니다. `response.directives` 필드에서 사용할 지시 메시지는 추후 API를 제공할 예정입니다. | 필수 |
| `response.directives[].header`           | object       | 지시 메시지의 헤더                                          | 필수 |
| `response.directives[].header.messageId` | string       | 메시지 ID. 개별 메시지를 구분하기 위해 사용하는 식별자입니다(UUID).   | 필수 |
| `response.directives[].header.name`      | string       | 지시 메시지의 API 이름                                      | 필수 |
| `response.directives[].header.namespace` | string       | 지시 메시지의 API 네임스페이스                                | 필수 |
| `response.directives[].payload`          | object       | 지시 메시지와 관련된 정보를 담고 있는 객체. 지시 메시지에 따라 payload 객체의 구성과 필드 값을 달리 작성할 수 있습니다.         | 필수 |
| `response.outputSpeech`                  | object       | 음성으로 합성할 정보를 담고 있는 객체. 합성된 음성 정보는 CIC를 거쳐 클라이언트로 전달됩니다.              | 필수 |
| `response.outputSpeech.brief`            | [SpeechInfoObject](#CustomExtSpeechInfoObject) | 출력할 요약 음성 정보.                    | 선택 |
| `response.outputSpeech.type`             | string       | 출력할 음성 정보의 타입. <ul><li>"SimpleSpeech" : 단문 형태의 음성 정보입니다. 가장 기본적인 타입이며, 이 값을 지정한 경우 <code>response.outputSpeech.values</code> 필드가 <a href="#CustomExtSpeechInfoObject"><code>SpeechInfoObject</code></a> 객체를 가져야 합니다.</li><li><code>"SpeechList"</code> : 복문 형태의 음성 정보입니다. 여러 문장을 출력할 때 사용되며, 이 값을 지정한 경우 <code>response.outputSpeech.values</code> 필드가 <a href="#CustomExtSpeechInfoObject"><code>SpeechInfoObject</code></a> 객체 배열을 가져야 합니다.</li><li><code>"SpeechSet"</code> : 복합 형태의 음성 정보입니다. 스크린이 없는 클라이언트 기기에 요약 음성 정보와 상세 음성 정보를 전달할 때 사용합니다. 이 값을 지정한 경우 <code>response.outputSpeech.values</code> 필드 대신 <code>response.outputSpeech.brief</code>와 <code>response.outputSpeech.verbose</code> 필드를 가져야 합니다.</li></ul> | 필수 |
| `response.outputSpeech.values`           | [SpeechInfoObject](#CustomExtSpeechInfoObject) or [SpeechInfoObject](#CustomExtSpeechInfoObject) array | 클라이언트 기기에서 출력할 음성 정보를 담고 있는 객체 또는 객체 배열 | 선택 |
| `response.outputSpeech.verbose`          | object       | 스크린이 없는 클라이언트 기기에 전달할 때 사용되며, 상세 음성 정보를 가집니다. | 선택 |
| `response.outputSpeech.verbose.type`     | string       | 출력할 음성 정보의 타입. 단문과 복문 형태의 음성 정보만 입력할 수 있습니다. <ul><li><code>"SimpleSpeech"</code> : 단문 형태의 음성 정보입니다. 가장 기본적인 음성 정보를 전달할 때 사용되며, 이 값을 지정한 경우 <code>response.outputSpeech.verbose.values</code> 필드가 <a href="#CustomExtSpeechInfoObject"><code>SpeechInfoObject</code></a> 객체를 가져야 합니다.</li><li><code>"SpeechList"</code> : 복문 형태의 음성 정보입니다. 여러 문장을 출력할 때 사용되며, 이 값을 지정한 경우 <code>response.outputSpeech.verbose.values</code> 필드가 <a href="#CustomExtSpeechInfoObject"><code>SpeechInfoObject</code></a> 객체 배열을 가져야 합니다.</li></ul> | 필수 |
| `response.outputSpeech.verbose.values`           | [SpeechInfoObject](#CustomExtSpeechInfoObject) or [SpeechInfoObject](#CustomExtSpeechInfoObject) array | 클라이언트 기기에서 출력할 상세 음성 정보를 담고 있는 객체 또는 객체 배열 | 필수 |
| `response.shouldEndSession`              | boolean      | 세션 종료 플래그. 클라이언트에게 특정 extension 사용이 종료됨을 알리는 필드입니다. [`SessionEndedRequest`](#CustomExtSessionEndedRequest) 타입의 요청 메시지를 받기 전에 extension이 먼저 사용 종료를 알릴 때 사용합니다.<ul><li>true : 사용 종료</li><li>false : 계속 사용</li></ul> | 필수 |
| `sessionAttributes`                      | object       | 사용자와의 multi-turn 대화를 위해 필요한 정보를 저장할 때 사용하는 객체. Custom extension은 `sessionAttributes` 필드를 이용해 중간 정보를 CEK에 전달하게 되며, 사용자의 추가 요청을 수신할 때 다시 해당 정보를 [요청 메시지](#CustomExtRequestMessage)의 `session.sessionAttributes` 필드로 받게 됩니다. 객체는 키(key)-값(value)의 쌍으로 구성해야 하며, custom extension을 구현할 때 임의로 정의할 수 있습니다. 저장할 값이 없으면 빈 객체를 입력하면 됩니다. | 필수 |
| `version`                                | string       | 메시지 포맷의 버전 (CEK 버전)                        | 필수 |

<div class="note">
  <p><strong>Note!</strong></p>
  <p><code>response.directives</code> 필드를 통해 extension 임의의 지시 메시지를 전달해야 하는 경우 사용하려면 사전 협의가 필요합니다. 제휴 담당자와 협의하기 바랍니다.</p>
</div>

#### SpeechInfoObject {#CustomExtSpeechInfoObject}
SpeechInfoObject 객체는 응답 메시지의 `response.outputSpeech`에서 재사용되는 객체이며, 사용자에게 출력하려는 음성 정보의 가장 작은 단위인 단문 수준의 발화 정보입니다. 이 객체는 다음과 같은 필드를 가집니다.

| 필드 이름        | 자료형         | 설명                                                                | 필수 |
|----------------|--------------|--------------------------------------------------------------------|-----|
| `lang`           | string       | 음성 합성을 할 때 사용할 언어의 코드. 현재 다음과 같은 값을 가집니다.<ul><li><code>"ko"</code>: 한국어</li><li><code>"en"</code>: 영어</li><li><code>""</code> : <code>type</code> 필드의 값이 <code>"URL"</code>이면 이 필드는 빈 문자열(empty string)을 가집니다.</li></ul>         | 필수 |
| `type`           | string       | 재생할 음성의 타입. 이 필드의 값에 따라 `value` 필드 값의 형태가 달라집니다. 현재는 다음과 같은 값을 가집니다.<ul><li><code>"PlainText"</code>: 일반 텍스트</li><li><code>"URL"</code>: 음성 및 음악을 재생할 수 있는 파일의 URI</li></ul>            | 필수 |
| `value`          | string       | 음성 합성할 내용                                                       | 필수 |

#### Message example
{% raw %}
```json
// 예제 1 : 단문 형태(SimpleSpeech) 음성 정보 반환 - 일반 텍스트
{
  "version": "0.1.0",
  "sessionAttributes": {},
  "response": {
    "outputSpeech": {
      "type": "SimpleSpeech",
      "values" : {
          "type": "PlainText",
          "lang": "en",
          "value": "Hi, nice to meet you"
      }
    },
    "card": {},
    "directives": [],
    "shouldEndSession": false
  }
}

// 예제 2 : 복문 형태(SpeechList) 음성 정보 반환 - 일반 텍스트, URL 타입 사용
{
  "version": "0.1.0",
  "sessionAttributes": {},
  "response": {
    "outputSpeech": {
      "type": "SpeechList",
      "values": [
        {
          "type": "PlainText",
          "lang": "ko",
          "value": "노래를 불러볼게요."
        },
        {
          "type": "URL",
          "lang": "" ,
          "value": "https://tts.com/song.mp3"
        }
      ]
    },
    "card": {},
    "directives": [],
    "shouldEndSession": true
  }
}

// 예제 3 : 복합 형태(SpeechSet) 음성 정보 반환 - 요약, 상세 음성 정보
{
  "version": "0.1.0",
  "sessionAttributes": {},
  "response": {
    "outputSpeech": {
      "type": "SpeechSet",
      "brief": {
        "type": "PlainText",
        "lang": "ko",
        "value": "날씨 뉴스 입니다."
      },
      "verbose": {
        "type": "SpeechList",
        "values": [
          {
              "type": "PlainText",
              "lang": "ko",
              "value": "주말까지 전국 장맛비…폭염 누그러져."
          },
          {
              "type": "PlainText",
              "lang": "ko",
              "value": "내일 전국 장맛비…곳곳 국지성 호우 주의."
          }
          ...
        ]
      }
    },
    "card": {},
    "directives": [],
    "shouldEndSession": true
  }
}

// 예제 4 : multi-turn 대화에서 대화 중간 정보 저장 - sessionAttributes 사용
{
  "version": "0.1.0",
  "sessionAttributes": {
    "RequestedIntent": "OrderPizza",
    "PizzaType": "페퍼로니 피자"
  },
  "response": {
    "outputSpeech": {
      "type": "SimpleSpeech",
      "values" : {
          "type": "PlainText",
          "lang": "ko",
          "value": "몇 판 주문할까요?"
      }
    },
    "card": {},
    "directives": [],
    "shouldEndSession": false
  }
}
```
{% endraw %}

#### See also
* [Custom extension 응답 반환하기](/CEK/Guides/Build_Custom_Extension.md#ReturnCustomExtensionResponse)
* [Content template](/CIC/References/Content_Templates.md)
