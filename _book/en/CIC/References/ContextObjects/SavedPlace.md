## Clova.SavedPlace {#SavedPlace}

`Clova.SavedPlace` is a format for reporting to CIC the locations saved on the client device.

### Object structure

{% raw %}
```json
{
  "header": {
    "namespace": "Clova",
    "name": "SavedPlace"
  },
  "payload": {
    "places": [
      {
        "latitude": {{string}},
        "longitude": {{string}},
        "refreshedAt": {{string}},
        "name": {{string}}
      }
    ]
  }
}
```
{% endraw %}

### Payload fields

| Field       | Type    | Description                     | Required |
|---------------|:---------:|-----------------------------|:---------:|
| `places[]`             | object array | Contains location information saved on the client.                                         | Required |
| `places[].latitude`    | string       | The latitude of this location.                                                                        | Required |
| `places[].longitude`   | string       | The longitude of this location.                                                                        | Required |
| `places[].name`        | string       | The name of this location. Available values are: <ul><li><code>"Work"</code></li><li><code>"Home"</code></li></ul>       | Required |
| `places[].refreshedAt` | string       | The time when this location was last saved, in UTC. (Format: [ISO 8601](https://en.wikipedia.org/wiki/ISO_8601))  | Required |


### Example

{% raw %}
```json
{
  "header": {
    "namespace": "Clova",
    "name": "SavedPlace"
  },
  "payload": {
    "places": [
      {
        "latitude": "37.3594915",
        "longitude": "127.1032242",
        "refreshedAt": "2017-04-06T13:34:15.074361+08:28",
        "name": "Home"
      },
      {
        "latitude": "36.3542315",
        "longitude": "125.1345242",
        "refreshedAt": "2017-03-12T10:21:33.089723+08:28",
        "name": "Work"
      }
    ]
  }
}
```
{% endraw %}

### See also

* [`SpeechRecognizer.Recognize`](/CIC/References/CICInterface/SpeechRecognizer.md#Recognize)
