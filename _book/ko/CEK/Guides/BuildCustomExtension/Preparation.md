## 사전 준비사항 {#Preparation}
Custom extension 개발자는 다음을 미리 준비해야 합니다.

* [Interaction 모델](#InteractionModel)
* (선택) [인증 서버](#AuthServer)

### Interaction 모델 {#InteractionModel}
Custom extension을 만들 때 사용자로부터 어떤 요청을 어떻게 받을지 Interaction 모델을 미리 정의해야 합니다. Interaction 모델은 custom extension이 받게 될 요청을 정형화한 스키마로서 다음과 같은 내용을 Clova Developer Console에 등록해야 합니다.

| 구분         | 설명                            |
|-------------|--------------------------------|
| Intent              | 사용자의 요청을 구별하여 정의한 명세입니다. Custom extension은 *intent*의 집합으로 구성된 Interaction 모델이 있어야 합니다. CEK는 분석된 사용자의 발화 정보를 [IntentRequest](/CEK/References/Custom_Extension_Message_Format.md#IntentRequest) 타입의 요청 메시지로 extension에 전달합니다. 이때, Interaction 모델에 정의된 *intent*를 참조하여 메시지를 구성합니다. |
| slot | Slot은 *intent*에 선언된 요청을 처리할 때 필요한 정보이며, *intent*를 정의할 때 함께 정의해야 합니다. Clova는 사용자 요청을 분석한 후 slot에 해당하는 정보를 추출하게 되며, CEK가 extension으로 *IntentRequest* 메시지를 보낼 때 key, value 쌍의 *slot* 정보를 함께 전달합니다.  |
| 사용자 발화 예시        | 사용자의 요청 발화가 어떤 식으로 입력될 수 있는지 예문을 표현한 목록입니다. *Intent*별로 복수의 사례를 정의할 수 있으며, 예문에는 slot이 표시됩니다. Clova는 사용자 요청을 분석하는 데 이 정보를 사용합니다. |

예를 들어, custom extension이 피자 주문 서비스를 제공한다고 가정할 때 사용자로부터 "페퍼로니 피자 2판 주문해줘"와 같은 요청이 들어온다고 가정할 수 있습니다. 이런 사용자 요청을 Intent로 정의하면 다음과 같이 정의할 수 있습니다.

![](/CEK/Resources/Images/CEK_Interaction_Model_Analysis_Diagram.png)

다음은 JSON 포맷으로 정의한 Interaction 모델입니다.

{% raw %}
```json
{
  "intents": [
    {
      "intent": "OrderPizza",
      "slots": [
        {
          "name": "PizzaAmount",
          "type": "CLOVA.NUMBER"
        },
        {
          "name": "PizzaType",
          "type": "CUSTOM.PIZZA_TYPE"
        }
      ]
    },
    {
      "intent": "OrderSideDish",
      ...
    }
    ...
  ]
}

```
{% endraw %}

사용자 발화 예시는 사용자의 요청이 정의해 둔 *intent*와 *slot*으로 연결(mapping)되는지 나타냅니다. 또한, 이 정보는 같은 의도를 가지지만 표현이 다를 수 있는 사용자의 요청을 처리할 때에도 사용됩니다.

{% raw %}
```
OrerPizza {CUSTOM.PIZZA_TYPE} 주문해줘
OrderItem {CUSTOM.PIZZA_TYPE} 주문해줄래?
OrderItem {CUSTOM.PIZZA_TYPE} {CLOVA.NUMBER}판 주문해줘
...
OrderSIdeDish  {CUSTOM.SIDE_DISH} 주문해줘
```
{% endraw %}

위와 같이 정의된 Interaction 모델에 의해 custom extension은 다음과 같은 메시지를 수신합니다.

{% raw %}
```json
{
  "version": "0.1.0",
  "session": {
    "new": false,
    "sessionId": "a29cfead-c5ba-474d-8745-6c1a6625f0c5",
    "user": {
      "userId": "V0qe",
      "accessToken": "XHapQasdfsdfFsdfasdflQQ7"
    }
  },
  "context": {
    "System": {
      "user": {
        "userId": "V0qe",
        "accessToken": "XHapQasdfsdfFsdfasdflQQ7"
      },
      "device": {
        "deviceId": "096e6b27-1717-33e9-b0a7-510a48658a9b"
      }
    }
  },
  "request": {
    "type": "IntentRequest",
    "intent": {
      "name": "OrderPIzza",
      "slots": {
        "PizzaAmount": {
          "name": "PizzaAmount",
          "value": "2"
        },
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

<div class="note">
  <p><strong>Note!</strong></p>
  <p>현재 Clova Developer Console을 개발하는 중입니다. 따라서, Interaction 모델을 정의하려면 제휴 담당자와 협의하기 바랍니다.</p>
</div>


### 인증 서버 {#AuthServer}
음악, 쇼핑, 금융 서비스 등과 같이 사용자 계정 인증이 필요한 외부 서비스를 제공하는 custom extension의 경우 사용자 계정을 연결해야 합니다. 이를 위해 인증 서버 등을 구축해야 합니다. 자세한 내용은 [사용자 계정 연결하기](/CEK/Guides/LinkUserAccount.md)를 참조합니다.
