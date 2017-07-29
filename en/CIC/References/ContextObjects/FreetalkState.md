## Clova.FreetalkState {#FreetalkState}
FreetalkState is a message format that shows a state of the Clova Freetalk service at a client side.

### Message format
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
| foreground    | boolean | Whether the Freetalk mode is activated or not <ul><li>true: Activated.</li><li>false: Inactivated.</li></ul>  | Yes |
| reprompt      | boolean | Whether reprompted for a user response or not. This state value verifies whether a user was reprompted for a response or not when the user did not give input for a specified time. <ul><li>true: Reprompted for a user response and the Freetalk mode will be finished.</li><li>false: Did not reprompted for a user response and is waiting for a response.</li></ul> | Yes |

### Remarks
The Freetalk mode is available only in English at the moment. If the *foreground* field is set to true, set the lang field of a Recognize event message of SpeechRecognizer API to "en".

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
* [SpeechRecognizer.Recognize](/CIC/References/APIs/SpeechRecognizer.md#Recognize)