## SpeechSynthesizer.SpeechState {#SpeechState}
`SpeechSynthesizer.SpeechState`는 클라이언트가 [`SpeechSynthesizer.Speak`](/CIC/References/CICInterface/SpeechSynthesizer.md#Speak) 지시 메시지로 전달된 TTS(text-to-speech)를 재생하고 있는지 여부를 CIC에게 보고할 때 사용하는 메시지 포맷입니다.

### Object structure
{% raw %}
```json
{
  "header": {
      "namespace": "SpeechSynthesizer",
      "name": "SpeechState"
  },
  "payload": {
      "token": {{string}},
      "playerActivity": {{string}}
  }
}
```
{% endraw %}

### Payload fields

| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|:---------:|
| `token`          | string | [`SpeechSynthesizer.Speak`](/CIC/References/CICInterface/SpeechSynthesizer.md#Speak) 지시 메시지를 통해 전달받은 TTS 식별용 token 값  | 필수     |
| `playerActivity` | string | TTS 재생 상태 <ul><li><code>PLAYING</code>: 현재 TTS 재생 상태</li><li><code>STOPPED</code>: 사용자의 음성 입력이나 다른 인터럽트로 TTS 재생이 중간에 중지된 상태</li><li><code>FINISHED</code>: TTS 재생이 완료된 상태</li></ul>     | 필수     |

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
