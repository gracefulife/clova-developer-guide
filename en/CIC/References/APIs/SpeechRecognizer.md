# SpeechRecognizer

This API processes user's speech input for speech recognition. User's speech input should be processed in the following steps.

1. Your client sends a [SpeechRecognizer.Recognize](#Recognize) Event message to CIC when user's speech input is coming in.
2. Your client keeps sending the speech input to CIC by capturing it with the interval of 200ms.
3. Your client should repeat the step 2 until the user finishes speaking or your client receives a [StopCapture](#StopCapture) Directive message from CIC.

This API provides the following Event and Directive messages.

| Message name  | Message type  | Message description  |
|------------------|-----------|---------------------------------------------|
| [ExpectSpeech](#ExpectSpeech)  | Directive | Instructs your client prepare to listen to user's speech input.  |
| [ExpectSpeechTimedOut](#ExpectSpeechTimedOut) | Event  | Reports to CIC that the specified waiting time for speech input has timed out.  |
| [Recognize](#Recognize)  | Event  | Transmits user's speech input to CIC and asks to recognize it. |
| [ShowRecognizedText](#ShowRecognizedText)  | Directive | Delivers the recognition result of the user's speech input in real time using a natural language.  |
| [StopCapture](#StopCapture)  | Directive | Instructs your client to stop capturing the user's speech input.  |

## ExpectSpeech Directive {#ExpectSpeech}

Instructs your client to activate a microphone and listen to the user's speech input. This Directive message is sent when the original user request does not provide enough information and that CIC wants to ask additional information. Or, this message is sent to continue conversation, for example, using the Freetalk mode. User's speech input is transmitted to CIC using a [SpeechRecognizer.Recognize](#Recognize) Event message.

### Payload field

| Field name  | Type  | Field description  | Required |
|---------------|---------|-----------------------------|---------|
| timeoutInMilliseconds | integer | The waiting time to receive user's speech input (in milliseconds). | Yes  |

### Remarks
* Upon receiving this Directive message, your client must use the same dialogue ID (*dialogRequestId*) as the dialogue ID of the previous request message to transmit user's speech input.
* If your does not receive any speech input from the user within the specified timeoutInMilliseconds time, it must send a [SpeechRecognizer.ExpectSpeechTimedOut](#ExpectSpeechTimedOut) Event message to CIC.

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

* [SpeechRecognizer.Recognize](#Recognize)
* [SpeechRecognizer.ExpectSpeechTimedOut](#ExpectSpeechTimedOut)

## ExpectSpeechTimedOut Event {#ExpectSpeechTimedOut}

This Event message is sent to CIC when your client does not receive any speech input from the user within the specified waiting time, which is delivered in a [SpeechRecognizer.ExpectSpeech](#ExpectSpeech) Directive message.

### Context field

Make sure to send the following [context information](/CIC/References/Context_Objects.md) together.

* [Clova.FreetalkState](/CIC/References/Context_Objects.md#FreetalkState)

### Payload field

None

### Remarks

* This Event message works only in the Freetalk mode.

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
* [Clova.FreetalkState](/CIC/References/Context_Objects.md#FreetalkState)
* [SpeechRecognizer.ExpectSpeech](#ExpectSpeech)

## Recognize Event {#Recognize}
A Recognize Event message transmits user's speech input to CIC asking to recognize what the user wants. Clova's natural language analysis and dialog understanding system interpret the result and process the user request. Most of [Directive messages](/CIC/References/CIC_Message_Format.md#Directives) are sent by CIC after user requests are confirmed using Recognize Event messages.

Supported audio input formats are as follows.
* 16-bit Linear PCM
* 16 kHz sample rate
* Mono
* Little endian

### Context field
A Recognize Event message should be sent with the following [context information](/CIC/References/Context_Objects.md).
* [Speaker.VolumeState](/CIC/References/Context_Objects.md#VolumeState)
* [Clova.FreetalkState](/CIC/References/Context_Objects.md#FreetalkState)

### Payload field
| Field name  | Type  | Field description  | Required |
|---------------|---------|-----------------------------|---------|
| format  | string | Audio data format. Use the fixed value, `AUDIO_L16_RATE_16000_CHANNELS_1`.  | No  |
| lang  | string | Determines in which language the user's speech input should be recognized. <ul><li>"ko": Korean</li><li>"en": English</li></ul> | Yes  |
| profile | string | A field reserved future use. Use the fixed value, `CLOSE_TALK`.  | No  |

### Remarks
In general, user's speech input is recognizable in Korean. In the Freetalk mode, however, it may be recognizable only in English ("en").

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
After your client sends a Recognize Event message, it keeps streaming the audio data as follows untill the user finishes speaking or your client receives a [StopCapture](#StopCapture) Directive message. Be noted that the audio data should be streamed over the same message part, not over separate message parts.
```
[ Message Header ]
Content-Disposition: form-data; name="audio"
Content-Type: application/octet-stream

[ PCM Audio Attachment ]
```

### See also
* [Speaker.VolumeState](/CIC/References/Context_Objects.md#VolumeState)
* [Clova.FreetalkState](/CIC/References/Context_Objects.md#FreetalkState)
* [SpeechRecognizer.StopCapture](#StopCapture)

## ShowRecognizedText Directive {#ShowRecognizedText}

Clova's speech recognition system analyzes user's speech input while it is being transmitted over a [SpeechRecognizer.Recognize](#Recognize) Event message and provides the recognition result. CIC delivers intermediate results processed in a natural language to your client over a ShowRecognizedText Directive message. This enables your client to display the ongoing processing for your user in real time.

### Payload field

| Field name  | Type  | Field description  | Required |
|---------------|---------|-----------------------------|---------|
| text  | string | Displays the recognition result of the user's speech input in real time using a natural language. | Yes  |

### Remarks

This Directive message is not a response to an Event message. It is delivered through a [Downchannel](/CIC/Guides/Interact_with_CIC.md#CreateConnection).

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

* [SpeechRecognizer.Recognize](#Recognize)
* [SpeechRecognizer.StopCapture](#StopCapture)

## StopCapture Directive {#StopCapture}
CIC sends a StopCapture Directive message to your client when CIC decides that it does not need to receive recorded PCM data any longer following a [SpeechRecognizer.Recognize](#Recognize) Event message. As soon as receiving this message, your client should stop recording the user's speech input. Your client may keep receiving the user's speech input even after CIC sends this message, but the audio data will not be processed. Also, the StopCapture Directive message will contain payload of the last speech input.

### Payload field
| Field name  | Type  | Field description  | Required |
|---------------|---------|-----------------------------|---------|
| recognizedText | string | Contains the recognition result of the user's speech input. | Yes |

### Remarks
This Directive message is not a response to an Event message. It is delivered through a [Downchannel](/CIC/Guides/Interact_with_CIC.md#CreateConnection).

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
* [SpeechRecognizer.Recognize](#Recognize)
* [SpeechRecognizer.ShowRecognizedText](#ShowRecognizedText)
