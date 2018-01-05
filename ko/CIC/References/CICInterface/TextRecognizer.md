# TextRecognizer

TextRecognizer 인터페이스는 사용자가 입력한 텍스트를 인식할 때 사용되는 네임스페이스입니다.

## Recognize event {#Recognize}
`TextRecognizer.Recognize` 이벤트 메시지는 사용자 텍스트 입력을 CIC로 전송하여 사용자가 무엇을 원하는지 인식하도록 요청합니다. Clova 내부의 자연어 분석 시스템과 대화 이해 시스템이 텍스트 입력을 해석하여 사용자의 요청을 처리합니다. 사용자의 음성 입력을 받기 어려운 환경에 있거나 마이크 시스템이 정상 동작하지 않는 경우 [`SpeechRecognizer.Recognize`](/CIC/References/CICInterface/SpeechRecognizer.md#Recognize) 이벤트 메시지 대신 사용하여 사용자의 텍스트 입력을 받을 수 있습니다.

### Context fields

필수 상태 정보 없음

### Payload fields
| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|:---------:|
| `text`        | string  | 사용자가 입력한 텍스트를 설정합니다. | 필수     |

### Message example
{% raw %}
```json
{
  "context":[],
  "event": {
    "header": {
      "namespace": "TextRecognizer",
      "name": "Recognize",
      "dialogRequestId": "bc834682-6d22-4bbb-8352-4a49df2ed3d7",
      "messageId": "b120c3e0-e6b9-4a3d-96de-71539e5f6214"
    },
    "payload": {
      "text": "지금 날씨 어때?"
    }
  }
}
```
{% endraw %}

### See also
* [`SpeechRecognizer.Recognize`](/CIC/References/CICInterface/SpeechRecognizer.md#Recognize)
