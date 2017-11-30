## Speaker.VolumeState {#VolumeState}
`Speaker.VolumeState` is a message format used to report the client's speaker volume information at the time when the user has spoken, such as how high/low its volume is or whether the speaker is in mute to CIC.

### Message structure
{% raw %}
```json
{
  "header": {
      "namespace": "Speaker",
      "name": "VolumeState"
  },
  "payload": {
      "volume": {{number}},
      "muted": {{boolean}}
  }
}
```
{% endraw %}

### Payload field

| Field name       | Type    | Field description                     | Required |
|---------------|---------|-----------------------------|---------|
| `muted`         | boolean | Whether the speaker is in mute                    | Yes     |
| `volume`        | number  | Current speaker volume (0-10)     | Yes     |

### Message example
{% raw %}
```json
{
  "header": {
      "namespace": "Speaker",
      "name": "VolumeState"
  },
  "payload": {
      "volume": 8,
      "muted": false
  }
}
```
{% endraw %}

### See also
* [`SpeechRecognizer.Recognize`](/CIC/References/CICInterface/SpeechRecognizer.md#Recognize)