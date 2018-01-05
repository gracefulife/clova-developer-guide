## Clova.Location {#Location}

`Clova.Location` is a format for reporting client's current location information to CIC. Use GPS or network module of the client device to obtain location information.

### Object structure

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

### Payload fields

| Field       | Type    | Description                     | Required |
|---------------|:---------:|-----------------------------|:---------:|
| `latitude`      | string  | The latitude of the current location.                                                                                   | Required |
| `longitude`     | string  | The longitude of the current location.                                                                                     | Required |
| `refreshedAt`   | string  | The time when the location was last checked, in UTC. Format: [ISO 8601](https://en.wikipedia.org/wiki/ISO_8601) | Required |

### Example

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

* [`SpeechRecognizer.Recognize`](/CIC/References/CICInterface/SpeechRecognizer.md#Recognize)
