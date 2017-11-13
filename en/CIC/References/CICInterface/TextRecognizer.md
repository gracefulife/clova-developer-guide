# TextRecognizer

Recognizes text entered by a user.

## Recognize event {#Recognize}
`TextRecognizer.Recognize` event message sends user's text input to CIC and requests to recognize what the user wants. Clova's natural language analysis and dialog understanding system interpret the results and process user requests accordingly. If your client cannot receive speech input from a user or if its microphone is not working properly, you can use this event message instead of [`SpeechRecognizer.Recognize`](/CIC/References/CICInterface/SpeechRecognizer.md#Recognize) to receive text input from a user.

### Context field

There is no required state information

### Payload field
| Field name       | Type    | Field description                     | Required |
|---------------|---------|-----------------------------|---------|
| `text`        | string  | Contains text entered by a user. | Yes     |

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