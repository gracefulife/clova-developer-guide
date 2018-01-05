# SpeechRecognizer

The SpeechRecognizer namespace provides interfaces for processing recognition of user voice request. To have a voice request processed:

1. Send CIC the [`SpeechRecognizer.Recognize`](#Recognize) event when the user makes a voice request.
2. Continue to send the speech input to CIC in every 200ms.
3. Repeat step 2 until the user finishes speaking or the [`SpeechRecognizer.StopCapture`](#StopCapture) directive from CIC is received.

The SpeechRecognizer namespace provides the following events and directives.

| Message name         | Message type  | Message description                                   |
|------------------|-----------|---------------------------------------------|
| [`ExpectSpeech`](#ExpectSpeech)                 | Directive | Instructs a client to receive speech input from a user.         |
| [`KeepRecording`](#KeepRecording)               | Directive | Instructs a client to continue taking in and recording user's voice request.            |
| [`Recognize`](#Recognize)                       | Event     | A message to request CIC to recognize what the user has requested. |
| [`ShowRecognizedText`](#ShowRecognizedText)     | Directive | Returns in real time the recognition result of a user's voice request.      |
| [`StopCapture`](#StopCapture)                   | Directive | Instructs a client to stop taking in the user's voice request.      |

## ExpectSpeech directive {#ExpectSpeech}

Instructs a client to activate its microphone and receive speech input from a user. CIC sends this directive to engage a multi-turn conversation to request additional information, because the information provided in the original user request was inadequate. To send the user's voice request to CIC, use the [`SpeechRecognizer.Recognize`](#Recognize) event.

### Payload fields

| Field name       | Type    | Description                     | Provided |
|---------------|:---------:|-----------------------------|:---------:|
| `expectContentType`        | string  | When the client takes in additional vocal input from the user, this field decides in which type the data should be sent. Available values are: <ul><li><code>"audio/l16"</code>: Denotes audio data in PCM format that had not been processed specifically for speech recognition such as eliminating echo or noise.</li><li><code>"application/x-clova-feat"</code>: Denotes audio data in PCM format that had been processed specifically for speech recognition such as eliminating echo or noise.</li></ul>  | Conditional |
| `expectSpeechId`        | string  | The ID for CIC to identify user's additional vocal input. Use this value in the `speechId` field when delivering the user's voice request to CIC with the [`SpeechRecognizer.Recognize`](#Recognize) event.    | Always |
| `explicit`              | boolean | Indicates whether user's vocal input is required or not. This field is usually set as `true` and is used to obtain additional information from the user.<ul><li><code>true</code>: User's vocal input is required.</li><li><code>false</code>: User's vocal input is not required.</li></ul>Suppose a user requests, “Order me a pizza”. To acquire necessary information such as quantity, CIC will ask the user, “How many boxes of pizza do you want to order?”. With this question, CIC may send the `SpeechRecognizer.ExpectSpeech` directive with the `explicit` field is set to `true`.  If the quantity is not specified by the user, the order cannot be processed successfully. Therefore, if the `explicit` field is `true`, the client must acquire the user’s vocal input. | Always |
| `timeoutInMilliseconds` | number  | The time to standby until user speaks to Clova. The value is an Integer and the unit is millisecond. | Always |

### Remarks

* When this directive is received, send the user's voice recording to CIC with the same dialog ID (`dialogRequestId`) used in the user's previous request message.
* If the `explicit` field is `false`, taking the user's vocal input depends on the client policy or the conditions the client has.

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

## KeepRecording directive {#KeepRecording}

Instructs a client to continue to receive vocal input from the user. The `SpeechRecognizer.KeepRecording` directive is an interim response indicating that CIC is in a process of recognizing user's vocal input taken by the client. The client has an option to implement timeout for CIC's response and apply the timeout in UX.

### Payload fields

None

### Message example

{% raw %}

```json
{
  "directive": {
    "header": {
      "namespace": "SpeechRecognizer",
      "name": "KeepRecording",
      "dialogRequestId": "bc834682-6d22-4bbb-8352-4a49df2ed3d7",
      "messageId": "b120c3e0-e6b9-4a3d-96de-71539e5f6214"
    },
    "payload": {}
  }
}
```

{% endraw %}

### See also

* [`SpeechRecognizer.Recognize`](#Recognize)
* [`SpeechRecognizer.ExpectSpeechTimedOut`](#ExpectSpeechTimedOut)

## Recognize event {#Recognize}

A message for sending user's voice request and requesting CIC to recognize what the user wants. Clova's natural language analysis system and dialog understanding system interpret user's request and process the request accordingly. Most [directives](/CIC/References/CIC_API.md#Directive) from CIC are sent after CIC has confirmed the user requests sent through the `SpeechRecognizer.Recognize` events.

CIC can process the following audio formats:
* 16-bit Linear PCM
* 16 kHz sample rate
* Mono
* Little endian

### Context fields

Send the following [context information](/CIC/References/Context_Objects.md) with this event.

* [`Alerts.AlertsState`](/CIC/References/Context_Objects.md#AlertsState)
* [`AudioPlayer.PlaybackState`](/CIC/References/Context_Objects.md#PlaybackState)
* [`Device.DeviceState`](/CIC/References/Context_Objects.md#DeviceState)
* [`Device.Display`](/CIC/References/Context_Objects.md#Display)
* [`Clova.Location`](/CIC/References/Context_Objects.md#Location)
* [`Clova.SavedPlace`](/CIC/References/Context_Objects.md#SavedPlace)
* [`Speaker.VolumeState`](/CIC/References/Context_Objects.md#VolumeState)

### Payload fields

| Field name       | Type    | Description                     | Required |
|---------------|:---------:|-----------------------------|:---------:|
| `speechId`   | string   | If receiving additional vocal input due to the [`SpeechRecognizer.ExpectSpeech`](#ExpectSpeech) directive, use the value of the `expectSpeechId` field specified in the `SpeechRecognizer.ExpectSpeech` directive.  | Optional |
| `explicit`         | boolean  | If receiving additional vocal input due to the [`SpeechRecognizer.ExpectSpeech`](#ExpectSpeech) directive, use the value of `explicit` field specified in `SpeechRecognizer.ExpectSpeech` directive.  | Optional |
| `format`           | string   | Audio data format of the user's request. The value is always `AUDIO_L16_RATE_16000_CHANNELS_1`.                             | Optional |
| `lang`             | string   | The language CIC shall recognize user's request in: <ul><li><code>"ko"</code>: Korean</li><li><code>"en"</code>: English</li></ul> | Required |
| `profile`          | string   | A field reserved for future use. The value is always `CLOSE_TALK`.                                     | Optional |

### Message example

{% raw %}
```json
// General user request
{
  "context": [
    {{Alerts.AlertsState}},
    {{AudioPlayer.PlayerState}},
    {{Device.DeviceState}},
    {{Device.Display}},
    {{Clova.Location}},
    {{Clova.SavedPlace}},
    {{Speaker.VolumeState}}
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

// Additional vocal input for the SpeechRecognizer.ExpectSpeech directive
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

After sending the `SpeechRecognizer.Recognize` event, continue to send the user's voice record until the user finishes speaking or the [StopCapture](#StopCapture) directive is received. Send the user's voice record as a part of a multipart message of the original HTTP request, as shown in the following example.

```
[ Message Header ]
Content-Disposition: form-data; name="audio"
Content-Type: application/octet-stream

[ PCM Audio Attachment ]
```

### See also

* [`SpeechRecognizer.ExpectSpeech`](#ExpectSpeech)
* [`SpeechRecognizer.StopCapture`](#StopCapture)
* [`Alert.AlertsState`](/CIC/References/Context_Objects.md#AlertsState)
* [`AudioPlayer.PlaybackState`](/CIC/References/Context_Objects.md#PlaybackState)
* [`Clova.Location`](/CIC/References/Context_Objects.md#Location)
* [`Clova.SavedPlace`](/CIC/References/Context_Objects.md#SavedPlace)
* [`Device.DeviceState`](/CIC/References/Context_Objects.md#DeviceState)
* [`Device.Display`](/CIC/References/Context_Objects.md#Display)
* [`Speaker.VolumeState`](/CIC/References/Context_Objects.md#VolumeState)

## ShowRecognizedText directive {#ShowRecognizedText}

Returns recognition result to a client in real time. Clova's speech recognition system analyzes and returns the user's voice request in real time while taking the user's voice request through the [`SpeechRecognizer.Recognize`](#Recognize) event. During the recognition process, CIC returns partial recognition result to the client with the `SpeechRecognizer.ShowRecognizedText` directive. A client has an option to display the recognition progress in real time.

### Payload fields

| Field name       | Type    | Description                     | Provided |
|---------------|:---------:|-----------------------------|:---------:|
| `text`  | string | Contains real time recognition result of the user's request. | Always |

### Remarks

* This directive is sent through a [downchannel](/CIC/Guides/Interact_with_CIC.md#CreateConnection), which means that this directive is not a response to an event.
* CIC does not provide partial result to a client by default. Only under special conditions will the `SpeechRecognizer.ShowRecognizedText` directive be sent.

### Message example

{% raw %}

```json
// Partial recognition result 1
{
  "directive": {
    "header": {
      "namespace": "SpeechRecognizer",
      "name": "ShowRecognizedText",
      "dialogRequestId": "277b40c3-b046-4f61-a551-783b1547e7b7",
      "messageId": "ceb4c638-d817-4a65-977d-03726d72cb91"
    },
    "payload": {
      "text": "Let me"
    }
  }
}

// Partial recognition result 2
{
  "directive": {
    "header": {
      "namespace": "SpeechRecognizer",
      "name": "ShowRecognizedText",
      "dialogRequestId": "277b40c3-b046-4f61-a551-783b1547e7b7",
      "messageId": "fab4c638-d8df7-4adf-977d-adf72cb91"
    },
    "payload": {
      "text": "Let me know"
    }
  }
}

// Partial recognition result 3
{
  "directive": {
    "header": {
      "namespace": "SpeechRecognizer",
      "name": "ShowRecognizedText",
      "dialogRequestId": "277b40c3-b046-4f61-a551-783b1547e7b7",
      "messageId": "efac233-8df7d-14df-d37d-72f72cb91"
    },
    "payload": {
      "text": "Let me know today's weather"
    }
  }
}

```
{% endraw %}

### See also

* [`SpeechRecognizer.Recognize`](#Recognize)
* [`SpeechRecognizer.StopCapture`](#StopCapture)

## StopCapture directive {#StopCapture}

Returns the last recognition result and instructs a client to stop recording user's voice when CIC decides no more voice recording (PCM) is required. When you receive this directive, stop recording user's voice request immediately. However, a client can choose to continue to receive user's request even after CIC sends this directive, but the voice request taken after receiving this directive will not be processed by Clova.

### Payload fields

| Field name       | Type    | Description                     | Provided |
|---------------|:---------:|-----------------------------|:---------:|
| `recognizedText` | string | Contains recognition results of the user's speech input. This field is not included in the `SpeechRecognizer.StopCapture` directive by default. It will be included only under special conditions. | Conditional |

### Remarks

This directive is sent through a [downchannel](/CIC/Guides/Interact_with_CIC.md#CreateConnection), not as a response to an event.

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
