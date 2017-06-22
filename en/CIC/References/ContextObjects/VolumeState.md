## Speaker.VolumeState {#VolumeState}
This message format contains the information of the client speaker at the time user's speech input is initiated, such as the volume size or whether the speaker is muted or not.

### Message format
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

| Field name  | Type  | Field description  | Required |
|---------------|---------|-----------------------------|---------|
| muted  | boolean | Whether the speaker is muted or not  | Yes  |
| volume  | number  | The current volume size of the speaker (0-10)  | Yes  |

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
* [SpeechRecognizer.Recognize](/CIC/References/APIs/SpeechRecognizer.md#recognize-event)