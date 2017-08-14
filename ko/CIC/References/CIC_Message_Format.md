# CIC 메시지
클라이언트는 CIC와 데이터를 주고받을 때 이벤트 메시지와 지시 메시지를 사용합니다. 여기에서는 각 메시지가 어떻게 구성되는지 그 포맷에 대해 설명합니다.

* [이벤트 메시지(Event)](#Event)
* [지시 메시지(Directive)](#Directive)
* [오류 메시지](#Error)

## 이벤트 메시지(Event) {#Event}
이벤트 메시지는 클라이언트에서 사용자가 발화한 음성 정보 또는 입력한 텍스트 정보를 CIC에 전달할 때 사용됩니다. 대표적인 이벤트 메시지로 사용자의 음성 입력을 받아 인식을 요청하는 [`SpeechRecognizer.Recognize`](/CIC/References/APIs/SpeechRecognizer.md#Recognize)가 있습니다.

### Message format
{% raw %}
```json
{
  "context": [
    {{AudioPlayer.PlaybackState}}
    {{Device.DeviceState}},
    {{Clova.FreetalkState}},
    {{Clova.Location}},
    {{Clova.SavedPlace}},
    {{Speaker.VolumeState}}
  ],
  "event": {
    "header": {
      "namespace": {{string}},
      "name": {{string}},
      "dialogRequestId": {{string}},
      "messageId": {{string}}
    },
    "payload": {{object}}
  }
}
```
{% endraw %}

### Message field

| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|---------|
| `context`                      | object array | CIC에 전달할 클라이언트의 상태 정보를 담고 있는 배열. 다음과 같은 [맥락 정보](/CIC/References/Context_Objects.md) 객체를 이 배열의 원소로 포함시킬 수 있습니다. 이벤트 메시지에 상황에 따라 필요한 맥락 정보를 포함시키면 됩니다.<ul><li><a href="/CIC/References/Context.html#PlaybackState"><code>AudioPlayer.PlaybackState</code></a> : 최근 재생 정보</li><li><a href="/CIC/References/Context.html#DeviceState"><code>Device.DeviceState</code></a> : 기기 정보</li><li><a href="/CIC/References/Context.html#FreetalkState"><code>Clova.FreetalkState</code></a> : 대화 모드(Freetalk mode) 정보</li><li><a href="/CIC/References/Context.html#Location"><code>Clova.Location</code></a> : 기기 위치 정보</li><li><a href="/CIC/References/Context.html#SavedPlace"><code>Clova.SavedPlace</code></a> : 사전 정의 위치 정보</li><li><a href="/CIC/References/Context.html#VolumeState"><code>Speaker.VolumeState</code></a> : 스피커 정보</li></ul> | 필수 |
| `event`                        | object       | 이벤트 메시지의 헤더와 필요한 데이터(payload)를 가지고 있는 객체                                                                 | 필수 |
| `event.header`                 | object       | 이벤트 메시지의 헤더                                                                                                 | 필수 |
| `event.header.dialogRequestId` | string       | 대화 ID(Dialog ID). CIC 쪽에서 어떤 대화의 응답인지 파악하기 위해 사용됩니다. [`SpeechRecognizer.Regcognize`](/CIC/References/APIs/SpeechRecognizer.md#Recognize) 이벤트 메시지를 전송할 때 반드시 이 필드 값을 입력해야 합니다.| 선택 |
| `event.header.messageId`       | string       | 메시지 ID. 개별 메시지를 구분하기 위해 사용하는 식별자입니다.                                                                 | 필수 |
| `event.header.name`            | string       | 이벤트 메시지의 API 이름                                                                                             | 필수 |
| `event.header.namespace`       | string       | 이벤트 메시지의 API 네임스페이스                                                                                       | 필수 |
| `event.payload`                | object       | 이벤트 메시지와 관련된 정보를 담고 있는 객체. 사용하는 [API](/CIC/References/CIC_API.md)에 따라 payload 객체의 구성과 필드 값이 달라집니다. | 필수 |

### Message example
{% raw %}
```json
{
  "context": [
    {
      "header": {
        "namespace": "Speaker",
        "name": "VolumeState"
      },
      "payload": {
        "volume": 25,
        "muted": false
      }
    }
  ],
  "event": {
    "header": {
      "namespace": "SpeechRecognizer",
      "name": "Recognize",
      "messageId": "277b40c3-b046-4f61-a551-783b1547e7b7",
      "dialogRequestId": "4e4080d6-c440-498a-bb73-ae86c6312806"
    },
    "payload": {
      "profile": "CLOSE_TALK"
    }
  }
}
```
{% endraw %}

### See also
* [맥락 정보(Context)](/CIC/References/Context_Objects.md)
* [CIC API](/CIC/References/CIC_API.md)

## 지시 메시지(Directive) {#Directive}
지시 메시지는 클라이언트가 요청한 이벤트 메시지에 응답을 하거나 특정 조건에 의해 클라이언트로 정보를 전달할 때 사용됩니다. 이 지시 메시지는 주로 사용자의 음성이 인식된 후 그 의도를 클라이언트가 수행하도록 요청하기 위해 전달됩니다. 물론 CIC가 제공하는 [API](/CIC/References/CIC_API.md)를 사용하여 다른 동작을 수행하도록 메시지를 보낼 수도 있습니다.

### Message format
{% raw %}
```json
{
  "directive": {
    "header": {
      "namespace": {{string}},
      "name": {{string}},
      "dialogRequestId": {{string}},
      "messageId": {{string}}
    },
    "payload": {{object}}
  }
}
```
{% endraw %}


### Message field

| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|---------|
| `directive`                        | object | 지시 메시지의 헤더와 필요한 데이터(`payload`)를 가지고 있는 객체                                                                 | 필수     |
| `directive.header`                 | object | 지시 메시지의 헤더                                                                                                 | 필수     |
| `directive.header.dialogRequestId` | string | 대화 ID(Dialog ID). 클라이언트 쪽에서 어떤 대화의 응답인지 파악하기 위해 사용됩니다. 지시 메시지가 [`SpeechRecognizer.Regcognize`](/CIC/References/APIs/SpeechRecognizer.md#Recognize) 이벤트 메시지에 대한 응답이 아닌 경우 이 필드가 지시 메시지에 포함되어 있지 않을 수도 있습니다.  | 선택  |
| `directive.header.messageId`       | string | 메시지 ID. 개별 메시지를 구분하기 위해 사용하는 식별자입니다.                                                                | 필수     |
| `directive.header.name`            | string | 지시 메시지의 API 이름                                                                                             | 필수     |
| `directive.header.namespace`       | string | 지시 메시지의 API 네임스페이스                                                                                       | 필수     |
| `directive.payload`                | object | 지시 메시지와 관련된 정보를 담고 있는 객체. 사용하는 [API](/CIC/References/CIC_API.md)에 따라 `payload` 객체의 구성과 필드 값이 달라집니다. | 필수     |

### Message example
{% raw %}
```json
{
  "directive": {
    "header": {
      "namespace": "SpeechSynthesizer",
      "name": "Speak",
      "messageId": "277b40c3-b046-4f61-a551-783b1547e7b7",
      "dialogRequestId": "4e4080d6-c440-498a-bb73-ae86c6312806"
    },
    "payload": {
      "format": "AUDIO_MPEG",
      "token": "b5fa5144-1e55-4193-8628-c70283083d9b",
      "ttsLang": "ko",
      "ttsText": "내일 날씨는 오전에는 맑다가 오후에는 구름이 많아지겠어요.",
      "url": "cid:9d5d37a3-0e70-41a6-a671-e1a40c7ea4d8",
      "x-clova-pause-before": 0
    }
  }
}
```
{% endraw %}

### See also
* [CIC API](/CIC/References/CIC_API.md)

## 오류 메시지 {#Error}
잘못된 방법이나 형식으로 이벤트 메시지를 전송하거나 서버측 내부 오류 등의 이유로 Clova가 제대로 서비스를 제공할 수 없을 수 있습니다. 이때 CIC는 오류 메시지를 클라이언트로 전송합니다. 클라이언트는 오류 메시지를 보고 그에 상응하는 UX/UI를 제공해야 합니다.

### Message format
{% raw %}
```json
{
  "header": {
    "namespace": "System",
    "name": "Exception",
    "messageId": {{string}}
  },
  "payload": {
    "code": "{{string}}",
    "description": "{{string}}"
  }
}
```
{% endraw %}


### Message field

| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|---------|
| `header`                 | object | 오류 메시지의 헤더                                             | 필수 |
| `header.messageId`       | string | 메시지 ID. 개별 메시지를 구분하기 위해 사용하는 식별자입니다.            | 필수 |
| `header.name`            | string | 오류 메시지의 이름. `"Exception"`으로 고정됩니다.                | 필수 |
| `header.namespace`       | string | 오류 메시지의 네임스페이스. `"System"`으로 고정됩니다.             | 필수 |
| `payload`                | object | 오류와 관련된 정보를 담고 있는 객체                                | 필수 |
| `payload.code`           | string | 오류 코드. 해당 메시지의 HTTP 응답 코드와 같은 값을 가집니다.           | 필수 |
| `payload.description`    | string | 오류 메시지.                                                  | 필수 |

### Error code reference

| 오류 코드 | 설명                             |
|---------|---------------------------------|
| 400     | 사용자 요청이 잘못된 형식으로 전달된 경우 발생하는 오류입니다.                       |
| 401     | 사용자 인증에 실패한 경우 발생하는 오류입니다. access token이 유효한지 확인해야 합니다. |
| 500     | 서버 내부 오류입니다.                                                      |

<div class="note">
  <p><strong>Note!</strong></p>
  <p>오류 코드는 계속 추가될 예정입니다.</p>
</div>

### Message example
{% raw %}
```json
{
  "header": {
    "namespace": "System",
    "name": "Exception",
    "messageId": "369b362b-258c-4104-bdf8-dc276548fe51"
  },
  "payload": {
    "code": 400,
    "description": "Could not decode multipart"
  }
}
```
{% endraw %}

### See also
* [CIC API](/CIC/References/CIC_API.md)
