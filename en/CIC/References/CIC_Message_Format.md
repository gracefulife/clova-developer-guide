# CIC message
You use event and directive messages to exchange data with CIC. This section explains the format of each message.

* [Event message](#Event)
* [Directive message](#Directive)

## Event message {#Event}
Event messages are used when your client sends user's speech input or text input to CIC. One example of an event message is [SpeechRecognizer.Recognize](/CIC/References/APIs/SpeechRecognizer.md#Recognize), which requests CIC to recognize user's speech input.

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
| context                      | object array | An array that contains client states to send to CIC. You can include the following [context](/CIC/References/Context_Objects.md) objects in the array. When necessary, include the following context information in the event message.<ul><li><a href="/CIC/References/Context.html#PlaybackState">AudioPlayer.PlaybackState</a>: Recent playback information</li><li><a href="/CIC/References/Context.html#DeviceState">Device.DeviceState</a>: Device information</li><li><a href="/CIC/References/Context.html#FreetalkState">Clova.FreetalkState</a>: Freetalk mode information</li><li><a href="/CIC/References/Context.html#Location">Clova.Location</a>: Device location information</li><li><a href="/CIC/References/Context.html#SavedPlace">Clova.SavedPlace</a>: Pre-defined location information</li><li><a href="/CIC/References/Context.html#VolumeState">Speaker.VolumeState</a>: Speaker information</li></ul> | Yes |
| event                        | object       | An object that contains header and payload data of an event message                                                                 | Yes |
| event.header                 | object       | A header of an event message                                                                                                 | Yes |
| event.header.dialogRequestId | string       | Dialog ID. It is used on a CIC side to figure out which dialog is associated with which response.                                             | Yes |
| event.header.messageId       | string       | Message ID. It is used to identify individual messages.                                                                 | Yes |
| event.header.name            | string       | The API name of an event message                                                                                             | Yes |
| event.header.namespace       | string       | The API namespace of an event message                                                                                       | Yes |
| event.payload                | object       | An object that contains information of an event message. The configuration of payload objects and field values may vary depending on the [CIC API](/CIC/References/CIC_API.md) in use. | Yes |

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
Directive messages are used when CIC returns a response for an event message requested from a client, or when CIC sends information to a client under certain conditions. Usually, a directive message is returned to instruct a client to perform specific actions after recognizing user's intent from speech input. You can also use the [CIC APIs](/CIC/References/CIC_API.md) to instruct your client to perform other actions.

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
| directive                        | object | An object that contains header and payload data of a directive message                                                                 | Yes     |
| directive.header                 | object | A header of a directive message                                                                                                 | Yes     |
| directive.header.dialogRequestId | string | Dialog ID. It is used on a client side to figure out which dialog is associated with which response.                                        | Yes    |
| directive.header.messageId       | string | Message ID. It is used to identify individual messages.                                                                | Yes     |
| directive.header.name            | string | The API name of a directive message                                                                                             | Yes     |
| directive.header.namespace       | string | The API namespace of a directive message                                                                                       | Yes     |
| directive.payload                | object | An object that contains information of a directive message. The configuration of payload objects and field values may vary depending on the [CIC API](/CIC/References/CIC_API.md) in use. | Yes     |

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
