# TextRecognizer

The TextRecognizer namespace provides an interface to request to CIC to recognize the user's text entry.

## Recognize event {#Recognize}

A message for sending user's text entry to CIC and requesting to recognize what the user wants. Clova's natural language analysis system and dialog understanding system interpret the given text and process user requests accordingly.

Use this event instead of the [`SpeechRecognizer.Recognize`](/CIC/References/CICInterface/SpeechRecognizer.md#Recognize) in the following cases:

* The client cannot receive voice requests from a user.
* The client's microphone is not functioning properly.

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
| `explicit`         | boolean  | If receiving additional input due to the [`SpeechRecognizer.ExpectSpeech`](#ExpectSpeech) directive, use the value of `explicit` field specified in `SpeechRecognizer.ExpectSpeech` directive.  | Optional |
| `speechId`   | string   | If receiving additional input due to the [`SpeechRecognizer.ExpectSpeech`](#ExpectSpeech) directive, use the value of the `expectSpeechId` field specified in the `SpeechRecognizer.ExpectSpeech` directive.  | Optional |
| `text`        | string  | The text entered by a user. | Required     |

### Message example

{% raw %}
```json
// General user text input
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
      "namespace": "TextRecognizer",
      "name": "Recognize",
      "dialogRequestId": "bc834682-6d22-4bbb-8352-4a49df2ed3d7",
      "messageId": "b120c3e0-e6b9-4a3d-96de-71539e5f6214"
    },
    "payload": {
      "text": "How is the weather now?"
    }
  }
}

// Additional text input for the SpeechRecognizer.ExpectSpeech directive
{
  "header": {
      "dialogRequestId": "d3f81fec-4cb9-4ce9-a046-1ea9a71018df",
      "messageId": "8526a048-4141-4c30-98a4-c61e223afece",
      "namespace": "TextRecognizer",
      "name": "Recognize"
  },
  "payload": {
      "text": "How about tomorrow?",
      "speechId": "1a4cd9ac-8fd8-4929-9c30-3a592dd2c298",
      "explicit": false
  }
}
```
{% endraw %}

### See also

* [`SpeechRecognizer.Recognize`](/CIC/References/CICInterface/SpeechRecognizer.md#Recognize)
* [`Alerts.AlertsState`](/CIC/References/Context_Objects.md#AlertsState)
* [`AudioPlayer.PlaybackState`](/CIC/References/Context_Objects.md#PlaybackState)
* [`Device.DeviceState`](/CIC/References/Context_Objects.md#DeviceState)
* [`Device.Display`](/CIC/References/Context_Objects.md#Display)
* [`Clova.Location`](/CIC/References/Context_Objects.md#Location)
* [`Clova.SavedPlace`](/CIC/References/Context_Objects.md#SavedPlace)
* [`Speaker.VolumeState`](/CIC/References/Context_Objects.md#VolumeState)
