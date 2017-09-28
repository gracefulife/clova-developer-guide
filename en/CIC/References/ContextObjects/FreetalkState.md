## Clova.FreetalkState {#FreetalkState}
FreetalkState is a message format that shows the state of the Clova Freetalk service at a client side.

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

| Field name       | Type    | Field description                     | Required |
|---------------|---------|-----------------------------|---------|
| `foreground`    | boolean | Whether the Freetalk mode is activated or not <ul><li><code>true</code>: Activated.</li><li><code>false</code>: Inactivated.</li></ul>  | Yes |
| `reprompt`      | boolean | Whether the user was reprompted for a response or not. This value verifies whether the user was reprompted for a response or not when the user did not give input for a specified time. <ul><li><code>true</code>: The user was reprompted for a response; the Freetalk mode will be finished.</li><li><code>false</code>: The user was not reprompted for a response; still waiting for a response.</li></ul> | Yes |

### Remarks
The Freetalk mode is available only in English at the moment. If the `foreground` field is set to true, set the lang field in the Recognize event message of the SpeechRecognizer API to "en".

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