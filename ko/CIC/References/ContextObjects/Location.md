## Clova.Location {#Location}
클라이언트의 현재 위치 정보를 CIC에게 보고할 때 사용하는 메시지 포맷입니다. GPS, 기지국, 네트워크 기기 등을 통해 파악된 위치 정보를 CIC로 전송할 수 있습니다.

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

| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|---------|
| `latitude`      | string  | 위도                                                                                     | 필수 |
| `longitude`     | string  | 경도                                                                                     | 필수 |
| `refreshedAt`   | string  | 위치를 마지막으로 확인한 시점(UTC 기준, [ISO 8601](https://en.wikipedia.org/wiki/ISO_8601) 포맷) | 필수 |

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
* [`SpeechRecognizer.Recognize`](/CIC/References/CICInterface/SpeechRecognizer.md#Recognize)
