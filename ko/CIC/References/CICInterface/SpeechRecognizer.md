# SpeechRecognizer

SpeechRecognizer는 사용자의 음성 인식을 위해 사용되는 네임스페이스입니다. 사용자의 음성 입력은 다음과 같이 수행되어야 합니다.

1. 클라이언트는 사용자의 음성이 입력될 때 CIC로 [`SpeechRecognizer.Recognize`](#Recognize) 이벤트 메시지를 전송합니다.
2. 클라이언트는 입력되는 사용자의 음성을 200ms 단위로 계속 CIC에 전송해야 합니다.
3. 클라이언트는 사용자의 음성 입력이 끝나거나 CIC로부터 [`SpeechRecognizer.StopCapture`](#StopCapture) 지시 메시지를 받기 전까지 2번 단계를 계속 수행해야 합니다.

SpeechRecognizer가 제공하는 이벤트 메시지와 지시 메시지는 다음과 같습니다.

| 메시지 이름         | 메시지 타입  | 메시지 설명                                   |
|------------------|-----------|---------------------------------------------|
| [`ExpectSpeech`](#ExpectSpeech)                 | Directive | 클라이언트에게 사용자의 음성 입력을 받도록 지시합니다.      |
| [`ExpectSpeechTimedOut`](#ExpectSpeechTimedOut) | Event     | 음성 입력 대기 시간이 초과했음을 CIC에 보고합니다.           |
| [`Recognize`](#Recognize)                       | Event     | 입력되는 사용자의 음성을 전달하여 음성 인식을 CIC에 요청합니다. |
| [`ShowRecognizedText`](#ShowRecognizedText)     | Directive | 클라이언트에게 인식된 사용자 음성을 실시간으로 전달합니다.   |
| [`StopCapture`](#StopCapture)                   | Directive | 클라이언트에게 사용자의 음성 인식을 중지하도록 지시합니다.      |

## ExpectSpeech directive {#ExpectSpeech}

클라이언트에게 마이크를 활성화하여 사용자의 음성 입력을 받도록 지시합니다. 해당 지시 메시지는 CIC가 먼저 사용자의 요청에서 불충분한 정보를 추가로 요구하는 multi-turn 대화를 수행하거나 대화 모드(Freetalk mode)와 같이 대화를 계속 진행하기 위해 전달됩니다. 입력된 사용자 음성은 [`SpeechRecognizer.Recognize`](#Recognize) 이벤트 메시지를 통해 CIC로 전달합니다.

### Payload field

| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|---------|
| `expectContentType`        | string  | 클라이언트가 추가로 사용자의 음성을 입력 받으면 해당 음성 데이터를 어떤 형식으로 보내야 할지 지정한 값입니다. 다음과 같은 값을 가질 수 있습니다. <ul><li><code>"audio/l16"</code>: 음성 인식을 위해 에코/잡음 제거 및 음성 인식에 특징적인 후처리를 수행하지 않은 PCM 포맷의 음성 데이터</li><li><code>"application/x-clova-feat"</code>: 음성 인식을 위해 에코/잡음 제거 및 음성 인식에 특징적인 후처리를 수행한 PCM 포맷의 음성 데이터</li></ul>  | 선택  |
| `expectSpeechId`        | string  | 사용자의 음성 입력을 추가로 받을 때 CIC가 이를 식별하기 위한 ID. 추후 이 값은 사용자의 추가 음성 입력을 [`SpeechRecognizer.Recognize`](#Recognize) 이벤트 메시지로 CIC에게 보낼 때 `speechId` 필드에 입력되어야 합니다.    | 필수 |
| `explicit`              | boolean | 사용자 음성 입력의 필수 여부.`explicit`는 주로 `true`로 설정되며, 사용자로부터 필수 정보를 추가로 알아내야 할 때 사용됩니다.<ul><li><code>true</code>: 필수</li><li><code>false</code>: 선택</li></ul>예를 들면, 사용자가 "피자 주문해줘."와 같은 요청을 했고 CIC는 수량과 같은 필수 정보를 얻기 위해 "몇 판 주문할까요?"라는 음성과 함께 `explicit` 필드가 `true`로 설정된 `SpeechRecognizer.ExpectSpeech` 지시 메시지를 보낼 수 있습니다.  이 경우 사용자로부터 수량 정보를 입력받지 않는다면 주문을 제대로 수행할 수 없게 됩니다. 따라서, `explicit` 필드가 `true`인 경우 반드시 사용자 음성 입력을 받아야 합니다. | 필수  |
| `timeoutInMilliseconds` | number  | 사용자의 음성 입력을 받기 위해 대기하는 시간으로 정수 형태 값이며, 단위는 밀리초(millisecond) 입니다. | 필수    |

### Remarks
* 이 지시 메시지를 받으면 클라이언트는 사용자의 입력을 CIC로 전달할 때 이전 요청 메시지와 같은 대화 ID(`dialogRequestId`)를 사용해서 전송해야 합니다.
* `explicit` 필드가 `false`인 경우는 클라이언트가 가지고 있는 정책이나 조건에 따라 사용자의 음성 입력을 받지 않을 수도 있습니다.
* `timeoutInMilliseconds` 시간 동안 사용자의 음성 데이터 입력이 없으면  [`SpeechRecognizer.ExpectSpeechTimedOut`](#ExpectSpeechTimedOut) 이벤트 메시지를 CIC로 전달해야 합니다.

### Message example

{% raw %}

```json
{
  "directive": {
    "header": {
      "namespace": "SpeechRecognizer",
      "name": "ExpectSpeech",
      "dialogRequestId": "bc834682-6d22-4bbb-8352-4a49df2ed3d7",
      "messageId": "b120c3e0-e6b9-4a3d-96de-71539e5f6214"
    },
    "payload": {
      "timeoutInMilliseconds": 7000,
      "explicit": false,
      "expectSpeechId": "561aeecf-2096-40fa-ba17-6612e28b339f"
    }
  }
}
```

{% endraw %}

### See also

* [`SpeechRecognizer.Recognize`](#Recognize)
* [`SpeechRecognizer.ExpectSpeechTimedOut`](#ExpectSpeechTimedOut)

## ExpectSpeechTimedOut event {#ExpectSpeechTimedOut}

[`SpeechRecognizer.ExpectSpeech`](#ExpectSpeech) 지시 메시지로 전달된 대기 시간 동안 사용자의 음성 입력이 없으면 해당 이벤트 메시지를 CIC로 전달합니다.

### Context field

해당 이벤트 메시지는 다음과 같은 [맥락 정보(Context)](/CIC/References/Context_Objects.md)를 함께 전송해야 합니다.

* [`Clova.FreetalkState`](/CIC/References/Context_Objects.md#FreetalkState)

### Payload field

없음

### Remarks

* 이 이벤트 메시지는 대화 모드(Freetalk mode)에서만 동작합니다.

### Message example

{% raw %}

```json
{
  "context": [
    {{Clova.FreetalkState}}
  ],
  "event": {
    "header": {
      "namespace": "SpeechRecognizer",
      "name": "ExpectSpeechTimedOut",
      "messageId": "56dcd20e-7fdc-4294-b6d9-a4b960d72df8"
    },
    "payload": {}
  }
}
```

{% endraw %}

### See also
* [`Clova.FreetalkState`](/CIC/References/Context_Objects.md#FreetalkState)
* [`SpeechRecognizer.ExpectSpeech`](#ExpectSpeech)

## Recognize event {#Recognize}
`SpeechRecognizer.Recognize` 이벤트 메시지는 사용자 음성 입력을 CIC로 전송하여 사용자가 무엇을 원하는지 인식하도록 요청합니다. Clova 내부의 자연어 분석 시스템과 대화 이해 시스템이 해당 결과를 해석하여 사용자의 요청을 처리합니다. CIC로부터 전달되는 대부분의 [지시 메시지](/CIC/References/CIC_API.md#Directive)는 `SpeechRecognizer.Recognize` 이벤트 메시지를 통해 사용자의 요청을 확인한 후 전달됩니다.

다음과 같은 기준의 음성 입력을 처리할 수 있습니다.
* 16-bit Linear PCM
* 16 kHz sample rate
* Mono
* Little endian

### Context field
Recognize 이벤트 메시지는 다음과 같은 [맥락 정보(Context)](/CIC/References/Context_Objects.md)를 함께 전송해야 합니다.
* [`Speaker.VolumeState`](/CIC/References/Context_Objects.md#VolumeState)
* [`Clova.FreetalkState`](/CIC/References/Context_Objects.md#FreetalkState)

### Payload field
| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|---------|
| `speechId`   | string   | [`SpeechRecognizer.ExpectSpeech`](#ExpectSpeech) 지시 메시지로 인해 사용자 음성 입력을 추가로 받는 경우 `SpeechRecognizer.ExpectSpeech` 지시 메시지에 포함된 `expectSpeechId` 필드의 값을 그대로 입력합니다.  | 선택  |
| `explicit`         | boolean  | [`SpeechRecognizer.ExpectSpeech`](#ExpectSpeech) 지시 메시지로 인해 사용자 음성 입력을 추가로 받는 경우 `SpeechRecognizer.ExpectSpeech` 지시 메시지에 포함된 `explicit` 필드의 값을 그대로 입력합니다.  | 선택  |
| `format`           | string   | 음성 데이터 포맷. `AUDIO_L16_RATE_16000_CHANNELS_1`으로 고정 입력합니다.                             | 선택    |
| `lang`             | string   | 사용자 음성 입력이 어떤 언어로 인식되도록 할지 결정합니다. <ul><li><code>"ko"</code>: 한국어</li><li><code>"en"</code>: 영어</li></ul> | 필수    |
| `profile`          | string   | 추후 사용을 위해 예약해 놓은 필드. `CLOSE_TALK`으로 고정 입력합니다.                                     | 선택    |

### Remarks
일반적으로 사용자 음성을 한국어로 인식하지만 대화 모드(Freetalk mode)의 경우 사용자 음성을 영어(`"en"`)로 인식해야 할 수 있습니다.

### Message example
{% raw %}
```json
// 일반적인 사용자 음성 입력
{
  "context": [
    {{Speaker.VolumeState}},
    {{Clova.FreetalkState}}
  ],
  "event": {
    "header": {
      "namespace": "SpeechRecognizer",
      "name": "Recognize",
      "dialogRequestId": "277b40c3-b046-4f61-a551-783b1547e7b7",
      "messageId": "4e4080d6-c440-498a-bb73-ae86c6312806"
    },
    "payload": {
      "lang": "ko",
      "profile": "CLOSE_TALK",
      "format": "AUDIO_L16_RATE_16000_CHANNELS_1"
    }
  }
}

// SpeechRecognizer.ExpectSpeech 지시 메시지에 따른 추가적인 사용자 음성 입력
{
        "header": {
            "dialogRequestId": "4951cbfe-0064-41e2-ac3a-b0e4e1b0a570",
            "messageId": "6ab89102-668b-42eb-89d0-639253db10ba",
            "namespace": "SpeechRecognizer",
            "name": "Recognize"
        },
        "payload": {
            "profile": "CLOSE_TALK",
            "format": "AUDIO_L16_RATE_16000_CHANNELS_1",
            "speechId": "561aeecf-2096-40fa-ba17-6612e28b339f",
            "explicit": false
        }
}

```
{% endraw %}

### Audio Data
`SpeechRecognizer.Recognize` 이벤트 메시지를 전송한 이후 다음과 같은 음성 데이터를 사용자가 음성 입력을 마치거나 [StopCapture](#StopCapture) 지시 메시지를 받기 전까지 계속 전달합니다. 단, 이 경우 별도의 메시지 파트로 메세지를 전송하는게 아니라 같은 메시지 파트 내에서 계속 스트리밍 해야 함을 의미합니다.
```
[ Message Header ]
Content-Disposition: form-data; name="audio"
Content-Type: application/octet-stream

[ PCM Audio Attachment ]
```

### See also
* [`Speaker.VolumeState`](/CIC/References/Context_Objects.md#VolumeState)
* [`Clova.FreetalkState`](/CIC/References/Context_Objects.md#FreetalkState)
* [`SpeechRecognizer.ExpectSpeech`](#ExpectSpeech)
* [`SpeechRecognizer.StopCapture`](#StopCapture)

## ShowRecognizedText directive {#ShowRecognizedText}

Clova 음성 인식 시스템은 [`SpeechRecognizer.Recognize`](#Recognize) 이벤트 메시지로 전달받고 있는 사용자의 음성 입력을 분석하여 인식 결과를 제공합니다. CIC는 `SpeechRecognizer.ShowRecognizedText` 지시 메시지로 사용자 음성 인식의 중간 처리 결과를 클라이언트로 전달합니다. 클라이언트는 이를 바탕으로 처리 과정을 사용자에게 실시간으로 보여 줄 수 있습니다.

### Payload field

| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|---------|
| `text`  | string | 입력된 사용자 음성이 어떤 어떻게 인식이 되고 있는지 그 결과를 실시간으로 담고 있습니다. | 필수    |

### Remarks

* 해당 지시 메시지는 이벤트 메시지에 대한 응답이 아닌 [downchannel](/CIC/Guides/Interact_with_CIC.md#CreateConnection)을 통해 전달됩니다.
* 기본적으로 CIC는 음성 인식 중간 결과를 클라이언트에게 전달하지 않으며, 일부 특수한 조건에 `SpeechRecognizer.ShowRecognizedText` 지시 메시지를 전달합니다.

### Message example

{% raw %}

```json
// 중간 인식 결과 1
{
  "directive": {
    "header": {
      "namespace": "SpeechRecognizer",
      "name": "ShowRecognizedText",
      "dialogRequestId": "277b40c3-b046-4f61-a551-783b1547e7b7",
      "messageId": "ceb4c638-d817-4a65-977d-03726d72cb91"
    },
    "payload": {
      "text": "오늘"
    }
  }
}

// 중간 인식 결과 2
{
  "directive": {
    "header": {
      "namespace": "SpeechRecognizer",
      "name": "ShowRecognizedText",
      "dialogRequestId": "277b40c3-b046-4f61-a551-783b1547e7b7",
      "messageId": "fab4c638-d8df7-4adf-977d-adf72cb91"
    },
    "payload": {
      "text": "오늘 날씨"
    }
  }
}

// 중간 인식 결과 3
{
  "directive": {
    "header": {
      "namespace": "SpeechRecognizer",
      "name": "ShowRecognizedText",
      "dialogRequestId": "277b40c3-b046-4f61-a551-783b1547e7b7",
      "messageId": "efac233-8df7d-14df-d37d-72f72cb91"
    },
    "payload": {
      "text": "오늘 날씨 알려줘"
    }
  }
}

```
{% endraw %}

### See also

* [`SpeechRecognizer.Recognize`](#Recognize)
* [`SpeechRecognizer.StopCapture`](#StopCapture)

## StopCapture directive {#StopCapture}
CIC가 [`SpeechRecognizer.Recognize`](#Recognize) 이벤트 메시지를 받은 후 더 이상 녹음 데이터(PCM)를 수신할 필요가 없다고 판단한 경우 `SpeechRecognizer.StopCapture` 지시 메시지를 클라이언트에 전달합니다. 클라이언트는 이 메시지를 수신한 즉시 사용자 음성 녹음을 중지해야 합니다. CIC가 이 메시지를 보낸 후에도 사용자 음성 정보를 수신할 수 있지만 해당 음성 정보는 처리되지 않습니다. 또한, `SpeechRecognizer.StopCapture` 지시 메시지는 사용자의 음성 입력이 마지막까지 인식된 결과를 `payload` 필드에 포함하고 있습니다.

### Payload field
| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|---------|
| `recognizedText` | string | 입력된 사용자 음성이 어떻게 인식이 되었는지 그 결과를 담고 있습니다. 기본적으로 이 필드는 `SpeechRecognizer.StopCapture` 지시 메시지에 포함되지 않으며, 일부 특수한 조건에 이 필드가 포함됩니다. | 선택 |

### Remarks
이 지시 메시지는 이벤트 메시지에 대한 응답이 아닌 [downchannel](/CIC/Guides/Interact_with_CIC.md#CreateConnection)을 통해 전달됩니다.

### Message example
{% raw %}
```json
{
  "directive": {
    "header": {
      "namespace": "SpeechRecognizer",
      "name": "StopCapture",
      "dialogRequestId": "277b40c3-b046-4f61-a551-783b1547e7b7",
      "messageId": "4e4080d6-c440-498a-bb73-ae86c6312806"
    },
    "payload": {
    }
  }
}
```
{% endraw %}

### See also
* [`SpeechRecognizer.Recognize`](#Recognize)
* [`SpeechRecognizer.ShowRecognizedText`](#ShowRecognizedText)
