## Clova.Location {#Location}
A message format that sends client's current location information. You can obtain location information from GPS, base stations or network devices and send it to CIC.

### Message structure
{% raw %}
```json
{
  "header": {
    "namespace": "Clova",
    "name": "Location"
  },
  "payload": {
    "latitude": {{string}},
    "longitude": {{string}},
    "refreshedAt": {{string}}
  }
}
```
{% endraw %}

### Payload field

| Field name       | Type    | Field description                     | Required |
|---------------|---------|-----------------------------|---------|
| `latitude`      | string  | Latitude                                                                                     | Yes |
| `longitude`     | string  | Longitude                                                                                     | Yes |
| `refreshedAt`   | string  | The time when the location was last checked (UTC, [ISO 8601](https://en.wikipedia.org/wiki/ISO_8601) format) | Yes |

### Message example
{% raw %}
```json
{
  "header": {
    "namespace": "Clova",
    "name": "Location"
  },
  "payload": {
    "latitude": "37.3594915",
    "longitude": "127.1032242",
    "refreshedAt": "2017-04-06T13:34:15.074361+08:28"
  }
}
```
{% endraw %}

### See also
* [`SpeechRecognizer.Recognize`](/CIC/References/CICInterface/SpeechRecognizer.md#recognize-event)