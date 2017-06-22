## Clova.FreetalkState {#FreetalkState}
FreetalkState is a message format that indicates the current state of the Clova Freetalk service in your client.

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

| Field name  | Type  | Field description  | Required |
|---------------|---------|-----------------------------|---------|
| foreground  | boolean | Whether the Freetalk mode is activated or not <ul><li>true: Activated.</li><li>false: Inactivated.</li></ul>  | Yes |
| reprompt  | boolean | Whether re-prompted the user to input a response or not. This value verifies whether your client requested input from the user one more time after it did not receive user input for a specified time. <ul><li>true: The user was re-prompted to input a response; the Freetalk mode is finished.</li><li>false: The user was not re-prompted to input a response; still waiting for a response.</li></ul> | Yes |

### Remarks
The Freetalk mode is available only in English at the moment. If the value of *foreground* field is true, the lang field of the Recognize Event message of SpeechRecognizer should be "en".

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
