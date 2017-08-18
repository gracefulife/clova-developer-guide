## Device.DeviceState {#DeviceState}
DeviceState is a message format that sends device states of a client, such as a current local time set in a user's device.

### Message format
{% raw %}
```json
{
  "header": {
    "namespace": "Device",
    "name": "DeviceState"
  },
  "payload": {
    "localTime": {{string}}
  }
}
```
{% endraw %}

### Payload field

| Field name  | Type  | Field description  | Required |
|---------------|---------|-----------------------------|---------|
| `localTime`  | string  | Current local time set in the client device ([ISO 8601](https://en.wikipedia.org/wiki/ISO_8601) format) | Yes |


### Message example
{% raw %}
```json
{
  "header": {
    "namespace": "Device",
    "name": "DeviceState"
  },
  "payload": {
    "localTime": "2017-04-06T13:34:15.074361+08:28"
  }
}
```
{% endraw %}

### See also
* [`SpeechRecognizer.Recognize`](/CIC/References/APIs/SpeechRecognizer.md#recognize-event)