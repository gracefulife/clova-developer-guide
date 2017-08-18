## Clova.SavedPlace {#SavedPlace}
A message format that sends client's pre-saved location information.

### Message format
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
        "refreshedAt": {{string}}
        "name": {{string}}
      }
    ]
  }
}
```
{% endraw %}

### Payload field

| Field name  | Type  | Field description  | Required |
|---------------|---------|-----------------------------|---------|
| `places[]`  | object array | An object array containing pre-saved location information  | Yes |
| `places[].latitude`  | string  | Latitude  | Yes |
| `places[].longitude`  | string  | Longitude  | Yes |
| `places[].name`  | string  | The name of the location saved. Available values are: <ul><li><strong>"회사"</strong></li><li><strong>"집"</strong></li></ul>  | Yes |
| `places[].refreshedAt` | string  | The time when the location was saved (UTC, [ISO 8601](https://en.wikipedia.org/wiki/ISO_8601) format)  | Yes |


### Message example
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
        "name": "집"
      },
      {
        "latitude": "36.3542315",
        "longitude": "125.1345242",
        "refreshedAt": "2017-03-12T10:21:33.089723+08:28",
        "name": "회사"
      }
    ]
  }
}
```
{% endraw %}

### See also
* [`SpeechRecognizer.Recognize`](/CIC/References/APIs/SpeechRecognizer.md#recognize-event)