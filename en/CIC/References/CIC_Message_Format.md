# CIC message
Your client uses event and directive messages to exchange data with CIC. The following explains the format and configuration of each message.

* [Event message](#Event)
* [Directive message](#Directive)
* [Error message](#Error)

## Event message {#Event}
Event messages are used when your client sends user's speech input or text input to CIC. One example of event messages is [`SpeechRecognizer.Recognize`](/CIC/References/APIs/SpeechRecognizer.md#Recognize), which requests CIC to receive user's speech input and recognize it.

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

| Field name       | Type    | Field description                     | Required |
|---------------|---------|-----------------------------|---------|
| `context`                      | object array | An array containing client states to send to CIC. You can include the following [context](/CIC/References/Context_Objects.md) objects in the array. Include them in event messages as necessary.<ul><li><a href="/CIC/References/Context.html#PlaybackState"><code>AudioPlayer.PlaybackState</code></a>: Recent playback details</li><li><a href="/CIC/References/Context.html#DeviceState"><code>Device.DeviceState</code></a>: Device details</li><li><a href="/CIC/References/Context.html#FreetalkState"><code>Clova.FreetalkState</code></a>: Freetalk mode details</li><li><a href="/CIC/References/Context.html#Location"><code>Clova.Location</code></a>: Device location details</li><li><a href="/CIC/References/Context.html#SavedPlace"><code>Clova.SavedPlace</code></a>: Pre-defined location details</li><li><a href="/CIC/References/Context.html#VolumeState"><code>Speaker.VolumeState</code></a>: Speaker details</li></ul> | Yes |
| `event`                        | object       | An object containing the header and necessary data (payload) of the event message                                                                 | Yes |
| `event.header`                 | object       | The header of the event message                                                                                                 | Yes |
| `event.header.dialogRequestId` | string       | The dialog ID. It is used at a CIC side to figure out which dialog is associated with which response. You must enter a value in this field when sending [`SpeechRecognizer.Regcognize`](/CIC/References/APIs/SpeechRecognizer.md#Recognize) event messages. | No |
| `event.header.messageId`       | string       | The message ID. This is an identifier for distinguishing individual messages.                                                                 | Yes |
| `event.header.name`            | string       | The API name of the event message                                                                                             | Yes |
| `event.header.namespace`       | string       | The API namespace of the event message                                                                                       | Yes |
| `event.payload`                | object       | An object containing details of the event message. Configuration of the payload object and its field values can change depending on which [CIC API](/CIC/References/CIC_API.md) is in use. | Yes |

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
* [Context information](/CIC/References/Context_Objects.md)
* [CIC API](/CIC/References/CIC_API.md)

## Directive message {#Directive}
Directive messages are used when CIC returns responses for event messages (client requests), or when CIC sends information to clients under certain conditions. Directive messages are usually returned to instruct clients to perform specific actions after recognizing user's intent from speech input. Also, directive messages can instruct clients to perform other actions using the [CIC APIs](/CIC/References/CIC_API.md).

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

| Field name       | Type    | Field description                     | Required |
|---------------|---------|-----------------------------|---------|
| `directive`                        | object | An object containing the header and necessary data (`payload`) of the directive message                                                                 | Yes     |
| `directive.header`                 | object | The header of the directive message                                                                                                 | Yes     |
| `directive.header.dialogRequestId` | string | The dialog ID. It is used at a client side to figure out which dialog is associated with which response. A directive message may not includ this field if the directive message is not a response to a [`SpeechRecognizer.Regcognize`](/CIC/References/APIs/SpeechRecognizer.md#Recognize) event message.  | No  |
| `directive.header.messageId`       | string | The message ID. This is an identifier for distinguishing individual messages.                                                                | Yes     |
| `directive.header.name`            | string | The API name of the directive message                                                                                             | Yes     |
| `directive.header.namespace`       | string | The API namespace of the directive message                                                                                       | Yes     |
| `directive.payload`                | object | An object containing details of the directive message. Configuration of the `payload` object and its field values can change depending on which [CIC API](/CIC/References/CIC_API.md) is in use. | Yes     |

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

## Error message {#Error}
If you send event messages using incorrect methods or wrong formats, or if internal server error occurs, Clova may not be able to provide its service properly. In such situations, CIC returns error messages to clients. Implement your client to check error messages and provide UX/UI accordingly.

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

| Field name       | Type    | Field description                     | Required |
|---------------|---------|-----------------------------|---------|
| `header`                 | object | The header of the error message                                             | Yes |
| `header.messageId`       | string | The message ID. This is an identifier for distinguishing individual messages.            | Yes |
| `header.name`            | string | The name of the error message. The value is always `"Exception"`.                | Yes |
| `header.namespace`       | string | The namespace of the error message. The value is always `"System"`.             | Yes |
| `payload`                | object | An object containing details of the error                                | Yes |
| `payload.code`           | string | The error code. It has the same value as the HTTP response code of the message.           | Yes |
| `payload.description`    | string | The error message.                                                  | Yes |

### Error code reference

| Error code | Description                             |
|---------|---------------------------------|
| 400     | The user request was sent in a wrong format.                       |
| 401     | Failed to authenticate the user. Check if the access token is valid. |
| 500     | An internal server error occurred.                                                      |

<div class="note">
  <p><strong>Note!</strong></p>
  <p>Error codes will continue to be added.</p>
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