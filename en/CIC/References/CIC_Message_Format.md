# CIC message format
Your client uses Event and Directive messages to send and receive data to and from CIC. This section explains message formats and how each message is structured.

* [Event message](#Event)
* [Directive message](#Directive)

## Event message {#Event}
An Event message is used when your client sends audio data (user speech) or text data (user input) to CIC. One example of an Event message is [SpeechRecognizer.Recognize](/CIC/References/APIs/SpeechRecognizer.md#Recognize) which asks CIC to recognize user's speech input.

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
| Field name  | Type  | Field description  | Required |
|---------------|---------|-----------------------------|---------|
| context  | object array | The array containing the client states to be sent to CIC. The following [context](/CIC/References/Context_Objects.md) objects can be included as an element of the array. You may include any necessary context information when required by the Event message.<ul><li><a href="/CIC/References/Context.html#PlaybackState">AudioPlayer.PlaybackState</a>: Recent playback information</li><li><a href="/CIC/References/Context.html#DeviceState">Device.DeviceState</a>: Device information</li><li><a href="/CIC/References/Context.html#FreetalkState">Clova.FreetalkState</a>: Freetalk mode information</li><li><a href="/CIC/References/Context.html#Location">Clova.Location</a>: Device location information</li><li><a href="/CIC/References/Context.html#SavedPlace">Clova.SavedPlace</a>: Pre-defined location information</li><li><a href="/CIC/References/Context.html#VolumeState">Speaker.VolumeState</a>: Speaker information</li></ul> | Yes |
| event  | object  | The object containing the header and necessary data (payload) of the Event message  | Yes |
| event.header  | object  | The header of the Event message  | Yes |
| event.header.dialogRequestId | string  | Dialogue ID. CIC uses this ID to figure out which dialogue is associated with the response at a later step. | Yes  |
| event.header.messageId  | string  | Message ID. It is used to identify individual messages. | Yes  |
| event.header.name  | string  | The API name of the Event message  | Yes |
| event.header.namespace  | string  | The API namespace of the Event message  | Yes |
| event.payload  | object  | The object containing information related to the Event message. Payload objects and field values may vary depending on the [CIC API](/CIC/References/CIC_API.md) being used. | Yes |

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
A Directive message is used when CIC should respond to an Event message or when CIC should send information to your client under certain conditions. Generally, a Directive message is sent to instruct your client to perform a specific action after a user's spoken request is recognized. You can also use the [CIC APIs](/CIC/References/CIC_API.md) to instruct your client to do other various actions.

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
| Field name  | Type  | Field description  | Required |
|---------------|---------|-----------------------------|---------|
| directive  | object | The object containing the header and necessary data (payload) of the Directive message  | Yes  |
| directive.header  | object | The header of the Directive message  | Yes  |
| directive.header.dialogRequestId | string | Dialogue ID. Your client uses this ID to figure out which dialogue is associated with the response at a later step.  | Yes  |
| directive.header.messageId  | string | Message ID. It is used to identify individual messages.  | Yes  |
| directive.header.name  | string | The API name of the Directive message  | Yes  |
| directive.header.namespace  | string | The API namespace of the Directive message  | Yes  |
| directive.payload  | object | The object containing information related to the Directive message. Payload objects and field values may vary depending on the [CIC API](/CIC/References/CIC_API.md) being used. | Yes  |

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
