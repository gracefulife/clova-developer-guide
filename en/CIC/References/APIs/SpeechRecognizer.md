# SpeechRecognizer

Processes user's speech input for speech recognition. Process speech input in the following steps.

1. Send CIC a [`SpeechRecognizer.Recognize`](#Recognize) event message while speech input is coming in from a user.
2. Continue to send the speech input to CIC by capturing it with the interval of 200ms.
3. Repeat the step 2 until the user finishes speaking or a [StopCapture](#StopCapture) directive message is returned from CIC.

The SpeechSynthesizer API provides the following event and directive messages.

| Message name  | Message type  | Message description  |
|------------------|-----------|---------------------------------------------|
| [`ExpectSpeech`](#ExpectSpeech)  | Directive | Instructs your client to be ready to receive speech input from a user.  |
| [`ExpectSpeechTimedOut`](#ExpectSpeechTimedOut) | Event  | Reports to CIC that the specified waiting time for speech input has timed out.  |
| [`Recognize`](#Recognize)  | Event  | Requests CIC to recognize speech input coming in from a user. |
| [`ShowRecognizedText`](#ShowRecognizedText)  | Directive | Returns speech recognition results in real time, in the form of natural language.  |
| [`StopCapture`](#StopCapture)  | Directive | Instructs your client to stop capturing user's speech input.  |

## ExpectSpeech directive {#ExpectSpeech}

Instructs your client to activate its microphone and receive speech input from a user. CIC returns this directive message to request more information when the original user request does not provide enough information. Or, CIC returns this message to engage conversation with the user, for example, in the Freetalk mode. To send the speech input to CIC, use a [`SpeechRecognizer.Recognize`](#Recognize) event message.

### Payload field

| Field name  | Type  | Field description  | Required |
|---------------|---------|-----------------------------|---------|
| `timeoutInMilliseconds` | integer | The time to wait until receiving speech input from a user (in milliseconds). | Yes  |

### Remarks
* When this directive message is returned, send user's input to CIC, using the same dialog ID (`dialogRequestId`) as the previous request message.
* If you do not receive any speech input from the user for specified `timeoutInMilliseconds` time, send CIC a  [`SpeechRecognizer.ExpectSpeechTimedOut`](#ExpectSpeechTimedOut) event message.

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
      "timeoutInMilliseconds": 7000
    }
  }
}
```

{% endraw %}

### See also

* [`SpeechRecognizer.Recognize`](#Recognize)
* [`SpeechRecognizer.ExpectSpeechTimedOut`](#ExpectSpeechTimedOut)

## ExpectSpeechTimedOut event {#ExpectSpeechTimedOut}

Send this event message to CIC if you do not receive any speech input from the user for a specified waiting time, which was returned in a [`SpeechRecognizer.ExpectSpeech`](#ExpectSpeech) directive message.

### Context field

Send the following [context information](/CIC/References/Context_Objects.md) together.

* [`Clova.FreetalkState`](/CIC/References/Context_Objects.md#FreetalkState)

### Payload field

None

### Remarks

* This event message works only in the Freetalk mode.

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
      "dialogRequestId": "bc834682-6d22-4bbb-8352-4a49df2ed3d7",
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
`SpeechRecognizer.Recognize` event message sends user's speech input to CIC and requests to recognize what the user wants. Clova's natural language analysis and dialog understanding system interpret the results and process user requests accordingly. Most of the [directive message](/CIC/References/CIC_Message_Format.md#Directives) are the messages returned from CIC after CIC confirms the user request through a `SpeechRecognizer.Recognize` event message.

Processable audio input formats are as follows.
* 16-bit Linear PCM
* 16 kHz sample rate
* Mono
* Little endian

### Context field
Send the following [context information](/CIC/References/Context_Objects.md) along with a Recognize event message.
* [`Speaker.VolumeState`](/CIC/References/Context_Objects.md#VolumeState)
* [`Clova.FreetalkState`](/CIC/References/Context_Objects.md#FreetalkState)

### Payload field
| Field name  | Type  | Field description  | Required |
|---------------|---------|-----------------------------|---------|
| `format`  | string | Audio data format. The value is always `AUDIO_L16_RATE_16000_CHANNELS_1`.  | No  |
| `lang`  | string | Determines in which language user's speech input will be recognized. <ul><li>"ko": Korean</li><li>"ja": Japanese</li><li>"en": English</li></ul> | Yes  |
| `profile` | string | A field reserved for future use. The value is always `CLOSE_TALK`.  | No  |

### Remarks
In general, user's speech is recognizable in Korean. However, the Freetalk mode may have to be recognized in English ("en").

### Message example
{% raw %}
```json
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
```
{% endraw %}

### Audio Data
After sending a `SpeechRecognizer.Recognize` event message, continue to send the audio data as follows until the user finishes speaking or a [StopCapture](#StopCapture) directive message is returned. You must keep streaming it in a same message part, not separate message parts.
```
[ Message Header ]
Content-Disposition: form-data; name="audio"
Content-Type: application/octet-stream

[ PCM Audio Attachment ]
```

### See also
* [`Speaker.VolumeState`](/CIC/References/Context_Objects.md#VolumeState)
* [`Clova.FreetalkState`](/CIC/References/Context_Objects.md#FreetalkState)
* [`SpeechRecognizer.StopCapture`](#StopCapture)

## ShowRecognizedText directive {#ShowRecognizedText}

While receiving speech input from users through [`SpeechRecognizer.Recognize`](#Recognize) event messages, Clova's speech recognition system analyzes it and provides analysis results. During the process, CIC returns intermediate recognition results to your client in the form of natural language, using `SpeechRecognizer.ShowRecognizedText` directive messages. Therefore, you can make your client display ongoing processing for users in real time.

### Payload field

| Field name  | Type  | Field description  | Required |
|---------------|---------|-----------------------------|---------|
| `text`  | string | Contains speech recognition results in real time, in the form of natural language. | Yes  |

### Remarks

This directive message is sent through a [downchannel](/CIC/Guides/Interact_with_CIC.md#CreateConnection), which means that the message is not a response to an event message.

### Message example

{% raw %}

```json
// Intermediate recognition result 1
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

// Intermediate recognition result 2
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

// Intermediate recognition result 3
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
After receiving [`SpeechRecognizer.Recognize`](#Recognize) event messages, CIC returns a `SpeechRecognizer.StopCapture` directive message to your client when it decides that it does not need to receive recorded PCM data any longer. You must stop recording user's speech immediately upon receiving this message. Although you can continue to receive user's speech even after receiving this message from CIC, the audio data will not be processed. Also, the `SpeechRecognizer.StopCapture` directive message will contain the last recognition result of the user's speech input in the `payload` field.

### Payload field
| Field name  | Type  | Field description  | Required |
|---------------|---------|-----------------------------|---------|
| `recognizedText` | string | Contains recognition results of the user's speech input. | Yes |

### Remarks
This directive message is sent through a [downchannel](/CIC/Guides/Interact_with_CIC.md#CreateConnection), which means that the message is not a response to an event message.

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
      "recognizedText": "오늘 날씨 알려줘"
    }
  }
}
```
{% endraw %}

### See also
* [`SpeechRecognizer.Recognize`](#Recognize)
* [`SpeechRecognizer.ShowRecognizedText`](#ShowRecognizedText)
