## Clova.FreetalkState {#FreetalkState}
FreetalkState는 Clova의 대화 모드(Freetalk mode) 서비스가 클라이언트 측에서 어떤 상태인지 나타내는 메시지 포맷입니다.

### Message structure
{% raw %}
```json
{
  "header": {
      "namespace": "Clova",
      "name": "FreetalkState"
  },
  "payload": {
      "foreground": {{boolean}},
      "reprompt": {{boolean}}
  }
}
```
{% endraw %}

### Payload field

| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|---------|
| `foreground`    | boolean | 대화 모드(Freetalk mode)의 활성화 여부 <ul><li><code>true</code>: 활성화됨.</li><li><code>false</code>: 비활성화됨.</li></ul>  | 필수 |
| `reprompt`      | boolean | 사용자 응답 재요청 여부. 일정 시간 동안 사용자 입력이 없어 한번 더 사용자에게 입력을 요청했는지 확인하는 상태 값입니다. <ul><li><code>true</code> : 사용자에게 응답을 재요청한 상황이며, 대화 모드(Freetalk mode)가 종료됩니다.</li><li><code>false</code> : 사용자에게 응답을 재요청하지 않은 상황이며, 응답 대기 상태입니다.</li></ul> | 필수 |

### Remarks
대화 모드(Freetalk mode)는 현재 영어 버전만 제공하고 있습니다. 따라서, `foreground` 필드 값이 true라면 SpeechRecognizer의 Recognize 이벤트 메시지의 lang 필드 값은 "en"여야 합니다.

### Message example
{% raw %}
```json
{
  "header": {
      "namespace": "Clova",
      "name": "FreetalkState"
  },
  "payload": {
      "foreground": flase,
      "reprompt": true
  }
}
```
{% endraw %}

### See also
* [`SpeechRecognizer.Recognize`](/CIC/References/CICInterface/SpeechRecognizer.md#Recognize)
