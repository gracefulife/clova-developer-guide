## Speaker.VolumeState {#VolumeState}
Message format that contains speaker information at the time when a user has spoken, such as volume size or whether speaker is muted or unmuted.

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

| Field name       | Type    | Field description                     | Required |
|---------------|---------|-----------------------------|---------|
| muted         | boolean | Whether muted or unmuted                    | Yes     |
| volume        | number  | Speaker's current volume size (0-10)     | Yes     |

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