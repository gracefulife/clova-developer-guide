## 複数回の対話でやり取りをする {#DoMultiturnDialog}

発話の設計によっては、ユーザーのリクエスト([`IntentRequest`](/CEK/Guides/Build_Custom_Extension.md#HandleIntentRequest))に、Custom Extensionが必要な情報を1つの発話からすべて抽出することができない場合があります。また、UXとしてもユーザーが必要な情報を全て含めて1回で発話するのが難しい場合もあります。その場合、Custom Extensionはユーザーの1度目の発話の中で足りない情報を引き出すために、複数回の対話を行うことができます。

例えば、ユーザーが「ペパロニピザを頼んで」と発話したと仮定します。それを受け、CEKは次のようなリクエストメッセージを送信します。

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
        "pizzaType": {
          "name": "pizzaType",
          "value": "ペパロニ"
        }
      }
    }
  }
}
```
{% endraw %}

ピザの注文を受け付けるには、Custom Extensionがピザの種類だけでなく、注文する数量も必要です。その際、[レスポンスメッセージ](/CEK/References/CEK_API.md#CustomExtResponseMessage)の`response.shouldEndSession`フィールドを`false`に設定すると、もう一度ユーザからの発話を受け付けることができ、対話の中で足りない情報を聴取することができます。また、ユーザーが先に入力した情報を`sessionAttributes`フィールドにキー(key)-値(value)の形で保存することもできます。

以下のようにレスポンスを返すことで、ユーザーが既にリクエストした`intent`フィールドと`pizzaType`の情報を保存するようにClovaにリクエストすることができます。また、ユーザーに数量に関する追加の情報を求めることができます。

{% raw %}
```json
{
  "version": "0.1.0",
  "sessionAttributes": {
    "intent": "OrderPizza",
    "pizzaType": "pepperoni"
  },
  "response": {
    "outputSpeech": {
      "type": "SimpleSpeech",
      "values": {
          "type": "PlainText",
          "lang": "ja",
          "value": "ピザを何枚注文しますか?"
      }
    },
    "card": {},
    "directives": [],
    "shouldEndSession": false
  }
}
```
{% endraw %}

ユーザーから必要な数量を聞くと、Clovaプラットフォームは、次のように解析された数量情報と一緒に、保存していた`sessionAttributes`オブジェクトの情報を[リクエストメッセージ](/CEK/References/CEK_API.md#CustomExtRequestMessage)の`session.sessionAttributes`フィールドに含めて再送信します。その際、追加で送信されたメッセージは前のメッセージと同じ`session.sessionId`値を持ち、Custom Extensionは受信した追加の情報を使用して次の動作をします。

{% raw %}
```json
{
  "version": "0.1.0",
  "session": {
    "new": false,
    "sessionAttributes": {
        "intent": "OrderPizza",
        "pizzaType": "ペパロニ"
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
        "pizzaAmount": {
          "name": "pizzaAmount",
          "value": "2"
        }
      }
    }
  }
}
```
{% endraw %}
