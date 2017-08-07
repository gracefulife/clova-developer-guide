## Device.DeviceState {#DeviceState}
DeviceState는 사용자 기기에 설정된 현지 시간 정보와 같이 클라이언트의 기기 상태 정보를 전송할 때 사용하는 메시지 포맷입니다.

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

| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|---------|
| `localTime`     | string  | 클라이언트 기기에 설정된 현지 시간([ISO 8601](https://en.wikipedia.org/wiki/ISO_8601) 포맷) | 필수 |


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
