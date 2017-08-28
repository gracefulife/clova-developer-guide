## Having multi-turn dialog {#DoMultiturnDialog}

Sometimes, CEK may return insufficient details about a user request ([`IntentRequest`](/CEK/Guides/Build_Custom_Extension.md#HandleIntentRequest)) for your custom extension to provide a requested service or perform necessary actions. In this case, you can make your custom extension have a multi-turn dialog to get more details.

Assume a user requested, "Order pepperoni pizza", and CEK sent a request message as follows.

{% raw %}
```json
{
  "version": "0.1.0",
  "session": {
    "new": true,
    "sessionAttributes": {},
    "sessionId": "a29cfead-c5ba-474d-8745-6c1a6625f0c5",
    "user": {
      "userId": "V0qe",
      "accessToken": "XHapQasdfsdfFsdfasdflQQ7"
    }
  },
  "context": {
    ...
  },
  "request": {
    "type": "IntentRequest",
    "intent": {
      "name": "OrderPizza",
      "slots": {
        "PizzaType": {
          "name": "PizzaType",
          "value": "페퍼로니"
        }
      }
    }
  }
}
```
{% endraw %}

In addition to a pizza type, the custom extension may require order quantity. If you set `response.shouldEndSession` to `false` in a [response message](/CEK/References/Custom_Extension_Message_Format.md#ResponseMessage), it can attempt to have a multi-turn dialog. Also, you can store the original details in the `sessionAttributes` field in a key-value pair.

If you respond as follows, you can request Clova to keep the previously sent `intent` and `PizzaType` and also request the user to provide quantity.

{% raw %}
```json
{
  "version": "0.1.0",
  "sessionAttributes": {
    "intent": "OrderPizza",
    "PizzaType": "페퍼로니 피자"
  },
  "response": {
    "outputSpeech": {
      "type": "SimpleSpeech",
      "values" : {
          "type": "PlainText",
          "lang": "ko",
          "value": "몇 판 주문할까요?"
      }
    },
    "card": {},
    "directives": [],
    "shouldEndSession": false
  }
}
```
{% endraw %}

When the user provides required quantity, the Clova platform adds the quantity, include the `sessionAttributes` object in the `session.sessionAttributes` field and send a [request message](/CEK/References/Custom_Extension_Message_Format.md#RequestMessage) again. This subsequent message has the same `session.sessionId` as the previous message and your custom extension can now perform next actions.

{% raw %}
```json
{
  "version": "0.1.0",
  "session": {
    "new": false,
    "sessionAttributes": {
        "intent": "OrderPizza",
        "PizzaType": "페퍼로니 피자"
    },
    "sessionId": "a29cfead-c5ba-474d-8745-6c1a6625f0c5",
    "user": {
      "userId": "V0qe",
      "accessToken": "XHapQasdfsdfFsdfasdflQQ7"
    }
  },
  "context": {
    ...
  },
  "request": {
    "type": "IntentRequest",
    "intent": {
      "name": "AddInfo",
      "slots": {
        "PizzaAmount": {
          "name": "PizzaAmount",
          "value": "2"
        }
      }
    }
  }
}
```
{% endraw %}
