## Speaker.VolumeState {#VolumeState}
`Speaker.VolumeState`는 사용자가 발화한 시점에 클라이언트의 스피커 볼륨 크기나 음소거 여부 정보를 CIC에게 보고할 때 사용하는 메시지 포맷입니다.

### Object structure
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

### Payload fields

| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|:---------:|
| `muted`         | boolean | 음소거 여부                    | 필수     |
| `volume`        | number  | 현재 스피커의 볼륨 크기(0-10)     | 필수     |

### Object example
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
