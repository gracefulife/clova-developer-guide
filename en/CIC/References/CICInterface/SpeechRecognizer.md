# SpeechRecognizer

Processes recognition of user speech. To process speech input, perform the following steps.

1. Send CIC a [`SpeechRecognizer.Recognize`](#Recognize) event message while speech input is coming in from a user.
2. Continue to send the speech input to CIC by capturing it with the interval of 200ms.
3. Repeat the step 2 until the user finishes speech input or a [`SpeechRecognizer.StopCapture`](#StopCapture) directive message is returned from CIC.

SpeechRecognizer provides the following event and directive messages.

| Message name         | Message type  | Message description                                   |
|------------------|-----------|---------------------------------------------|
| [`ExpectSpeech`](#ExpectSpeech)                 | Directive | Instructs your client to receive speech input from a user.         |
| [`ExpectSpeechTimedOut`](#ExpectSpeechTimedOut) | Event     | Reports to CIC that the specified waiting time for speech input has timed out.           |
| [`KeepRecording`](#KeepRecording)               | Directive | Instructs your client to continually receive speech input.            |
| [`Recognize`](#Recognize)                       | Event     | Requests CIC to recognize speech input coming in from a user. |
| [`ShowRecognizedText`](#ShowRecognizedText)     | Directive | Returns recognition results of user speech in real time.      |
| [`StopCapture`](#StopCapture)                   | Directive | Instructs your client to stop recognizing user's speech.      |

## ExpectSpeech directive {#ExpectSpeech}

Instructs your client to activate its microphone and receive speech input from a user. CIC returns this directive message to execute multi-turn conversation requesting additional information when the original user request does not provide enough information. Or, CIC returns this message to engage conversation with a user, for example, in the Freetalk mode. To send the speech input to CIC, use a [`SpeechRecognizer.Recognize`](#Recognize) event message.

### Payload field

| Field name       | Type    | Field description                     | Required |
|---------------|---------|-----------------------------|---------|
| `expectContentType`        | string  | When the client receives additional speech input of the user, the value decides in which type the data should be sent. Available values are: <ul><li><code>"audio/l16"</code> : A speech data in PCM format which did not go through postprocess distinctively for speech recognition such as eliminating echo or noise.</li><li><code>"application/x-clova-feat"</code> : A speech data in PCM format which went through postprocess distinctively for speech recognition such as eliminating echo or noise.</li></ul>  | No  |
| `expectSpeechId`        | string  | An ID for CIC to identify additional user's speech input This value has to be entered on `speechId` field when passing the user's speech input as a [`SpeechRecognizer.Recognize`](#Recognize) event message to CIC in the future.    | Yes |
| `explicit`              | boolean | Whether user’s speech input was done or not. `explicit` is usually set as `true` and it is applied to grasp additional information from the user.<ul><li><code>true</code> : Yes</li><li><code>false</code> : No</li></ul>For instance, if the user makes a request saying “order a pizza”, CIC will reply “how many boxes of pizza do you want to order?” to acquire required information such as an amount. By replying, CIC can return a `SpeechRecognizer.ExpectSpeech` directive message with `explicit` field is set as `true`.  If the amount information is not given from the user, the pizza order cannot be processed successfully. Thus, in case `explicit` field is `true`, CIC must acquire the user’s voice input. | Yes  |
| `timeoutInMilliseconds` | number  | It is the time to standby until receiving user’s voice input. The value is in integer form and the unit is millisecond. | Yes    |

### Remarks
* When this directive message is returned, send user's input to CIC, using the same dialog ID (`dialogRequestId`) as the previous request message.
* If `explicit` field is `false`, the user’s voice input may not be received according to policies or conditions the client has.
* If you do not receive any speech input from the user for specified `timeoutInMilliseconds` time,  send CIC a [`SpeechRecognizer.ExpectSpeechTimedOut`](#ExpectSpeechTimedOut) event message.

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

## KeepRecording directive {#KeepRecording}

Instructs your client to continually receive speech input from a user. A `SpeechRecognizer.KeepRecording` directive message is an intermediate response indicating that it is recognizing user's speech input entered on the client. Upon receiving the directive message, the client can implement timeout as a response to CIC or apply it to UX.

### Payload field

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
`SpeechRecognizer.Recognize` event message sends user's speech input to CIC and requests to recognize what the user wants. Clova's natural language analysis and dialog understanding system interpret the results and process user requests accordingly. Most of [directive messages](/CIC/References/CIC_API.md#Directive) are returned from CIC after CIC confirms user requests which are sent in `SpeechRecognizer.Recognize` event messages.

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
| Field name       | Type    | Field description                     | Required |
|---------------|---------|-----------------------------|---------|
| `speechId`   | string   | If receiving additional speech input because of [`SpeechRecognizer.ExpectSpeech`](#ExpectSpeech) directive message, enter the value of `expectSpeechId` field included in `SpeechRecognizer.ExpectSpeech` directive message.  | No  |
| `explicit`         | boolean  | If receiving additional speech input because of [`SpeechRecognizer.ExpectSpeech`](#ExpectSpeech) directive message, enter the value of `explicit` field included in `SpeechRecognizer.ExpectSpeech` directive message.  | No  |
| `format`           | string   | Speech audio data format. The value is always `AUDIO_L16_RATE_16000_CHANNELS_1`.                             | No    |
| `lang`             | string   | Determines in which language user's speech input will be recognized. <ul><li><code>"ko"</code>: Korean</li><li><code>"en"</code>: English</li></ul> | Yes    |
| `profile`          | string   | A field reserved for future use. The value is always `CLOSE_TALK`.                                     | No    |

### Remarks
In general, user's speech is recognizable in Korean. However, when in the Freetalk mode, it may have to be recognized in English (`"en"`).

### Message example
{% raw %}
```json
// Input general user's voice
{
  "context": [
    {{Alerts.AlertsState}},
    {{AudioPlayer.PlayerState}},
    {{Device.DeviceState}},
    {{Device.Display}},
    {{Clova.FreetalkState}},
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

// Input additional user's voice according to a SpeechRecognizer.ExpectSpeech directive message
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
After sending a `SpeechRecognizer.Recognize` event message, continue to send the audio data as follows until the user finishes speech input or a [StopCapture](#StopCapture) directive message is returned. You must keep streaming it in a same message part, not separate message parts.
```
[ Message Header ]
Content-Disposition: form-data; name="audio"
Content-Type: application/octet-stream

[ PCM Audio Attachment ]
```

### See also
* [`SpeechRecognizer.ExpectSpeech`](#ExpectSpeech)
* [`SpeechRecognizer.StopCapture`](#StopCapture)
* [Alert.AlertsState](/CIC/References/Context_Objects.md#AlertsState)
* [AudioPlayer.PlaybackState](/CIC/References/Context_Objects.md#PlaybackState)
* [Clova.FreetalkState](/CIC/References/Context_Objects.md#FreetalkState)
* [Clova.Location](/CIC/References/Context_Objects.md#Location)
* [Clova.SavedPlace](/CIC/References/Context_Objects.md#SavedPlace)
* [Device.DeviceState](/CIC/References/Context_Objects.md#DeviceState)
* [Device.Display](/CIC/References/Context_Objects.md#Display)
* [Speaker.VolumeState](/CIC/References/Context_Objects.md#VolumeState)

## ShowRecognizedText directive {#ShowRecognizedText}

While receiving speech input from users in [`SpeechRecognizer.Recognize`](#Recognize) event messages, Clova's speech recognition system analyzes it and provides analysis results. During the process, CIC returns intermediate recognition results to your client in `SpeechRecognizer.ShowRecognizedText` directive messages. You can make your client display the progress of recognition processing in real time.

### Payload field

| Field name       | Type    | Field description                     | Required |
|---------------|---------|-----------------------------|---------|
| `text`  | string | Contains recognition results of user speech in real time. | Yes    |

### Remarks

This directive message is sent through a [downchannel](/CIC/Guides/Interact_with_CIC.md#CreateConnection), which means that the message is not a response to an event message.
* CIC does not provide intermediate result to your client by default. `SpeechRecognizer.ShowRecognizedText` directive message will be returned only under special conditions.

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
After receiving a [`SpeechRecognizer.Recognize`](#Recognize) event message, CIC returns a `SpeechRecognizer.StopCapture` directive message to your client when it decides that it does not need to receive recorded PCM data any longer. You must stop recording user's speech immediately upon receiving this message. Although you can continue to receive user's speech even after CIC returns this message, the speech audio data will not be processed. Also, the `SpeechRecognizer.StopCapture` directive message will contain the last recognition result of the user's speech input in the `payload` field.

### Payload field
| Field name       | Type    | Field description                     | Required |
|---------------|---------|-----------------------------|---------|
| `recognizedText` | string | Contains recognition results of the user's speech input. This field is not included in the `SpeechRecognizer.StopCapture` directive message by default. It will be included only under special conditions. | No |

### Remarks
This directive message is sent through [downchannel](/CIC/Guides/Interact_with_CIC.md#CreateConnection), not as a response to an event message.

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
