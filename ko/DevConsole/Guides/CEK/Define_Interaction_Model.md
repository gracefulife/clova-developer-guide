# Interaction 모델 정의하기

CEK가 extension으로 사용자의 요청 정보를 보낼 때 사용자의 발화를 어떻게 분석하고 이를 어떤 형식으로 보낼지 interaction 모델을 미리 정의해야 합니다. Interaction 모델은 [custom extension](/CEK/Guides/Build_Custom_Extension.md)이 받게 될 요청을 정형화한 스키마입니다.

Clova developer console에서 [extension을 등록](/DevConsole/Guides/CEK/Register_Extension.md)한 후 Interaction 모델을 정의할 수 있습니다. Extension 등록 메뉴에서 **인터렉션 모델**을 선택합니다.

![](/DevConsole/Resources/Images/DevConsole-Interaction_Model_Menu.png)

**인터렉션 모델** 메뉴를 선택하면 다음과 같은 **인터랙션 모델: 대시보드** 화면이 표시됩니다.

![](/DevConsole/Resources/Images/DevConsole-Interaction_Model_Dashboard.png)

이제 다음과 같은 순서로 interaction 모델을 정의하면 됩니다.

1. (사전 요구 지식) [Interaction 모델 이해하기](#UnderstandInteractionModel)
2. [Built-in slot 타입 추가하기](#AddBuiltinSlotType)
3. [Custom slot 타입 추가하기](#AddCustomSlotType)
4. [Built-in intent 추가하기](#AddBuiltinIntent)
5. [Custom intent 추가하기](#AddCustomIntent)

<div class="note">
  <p><strong>Note!</strong></p>
  <p>참고로 custom intent를 추가하고 필요한 slot 타입을 추가할 수도 있지만 Clova developer console이 제공하는 UI 특성상 slot 타입을 추가한 후 intent를 추가하는 순서로 진행하는 것이 좋습니다.</p>
</div>

## Interaction 모델 이해하기 {#UnderstandInteractionModel}

Clova에서 interaction 모델이란, 음성으로부터 인식된 사용자의 요청을 extension에 전달하기 위해 정형화된 포맷(JSON)으로 바꿔주는 규칙을 명세한 것입니다. 예를 들어, custom extension이 피자 배달 서비스를 제공한다고 가정할 때 "페퍼로니 피자 2판 주문해줘"와 같은 요청이 사용자로부터 입력된다고 가정할 수 있습니다. Interaction 모델은 이런 사용자의 요청을 아래와 같이 서비스 제공에 필요한 포맷(JSON)으로 변경하는 규칙을 정의해 놓은 것이라고 보면됩니다.

![](/DevConsole/Resources/Images/DevConsole-Interaction_Model_Analysis_Diagram.png)

Interaction 모델을 Clova developer console에서 정의하기 전에 우선 interaction 모델을 이해하고 설계하는 과정이 필요합니다. 이런 과정없이 무작정 Clova developer console에서 interaction 모델을 등록하게 되면 작업 효율이 떨어지거나 사용자 요청이 의도된 대로 입력되지 않을 수 있습니다. 사용자의 실제 의도를 잘 파악하는 interaction 모델을 만들려면 interaction 모델을 만들기 전에 다음과 같은 내용을 이해하고 interaction 모델 설계에 반영해야 합니다.

* [Intent](#Intent)
* [Slot](#Slot)
* [발화 예시](#UtteranceExample)

### Intent {#Intent}

Intent는 extension이 처리할 사용자의 요청을 구별한 범주이며, custom intent와 built-in intent로 나뉩니다. 이 중 Built-in intent는 Clova 플랫폼이 일부 공통적인 사용자 요청 범주를 정하고 이를 공유하여 사용하기 위해 선언한 명세입니다. 일반적으로 빈번히 발생할 수 있는 intent로 다음과 같은 요청을 미리 정의해 두고 있습니다. Extension에서 어떤 built-in intent를 사용할지 선택할 수 있으며, extension에서 선택한 built-in intent를 처리할 수 있게 만들어야 합니다.

| Built-in intent 이름       | 의도               | 대응하는 사용자 발화 예시                                      |
|---------------------------|-------------------|----------------------------------------------------------|
| Clova.GuideIntent         | 도움말 요청          | "너 뭐 할 줄 아니?", "할 줄 아는 거 말해봐", "너 할 줄 아는게 뭐냐?" |
| Clova.CancelIntent        | 실행 취소 요청        | "취소", "취소해줘"                                          |
| Clova.YesIntent           | 긍정 응답(예, Yes)   | "응", "그래", "알겠어", "알겠습니다", "오케이"                   |
| Clova.NoIntent            | 부정 응답(아니오, No) | "아니", "아니요", "싫어"                                     |

Custom intent는 서비스 제공자(extension 개발자)가 서비스에 맞게 사용자 요청을 여러 범주로 나누고 사용자의 발화에서 어떤 정보([Slot](#Slot))를 파악해야 하는지 또 해당 요청 범주에는 어떤 다양한 [발화 예시](#UtteranceExample)가 있는지 정의한 명세입니다. 피자 배달 서비스를 계속 예로 들어 설명하면, 해당 서비스는 다음과 같은 요청 범주가 있을 수 있습니다.

* 메뉴 조회 요청
* 주문 요청
* 배달 조회 요청

이를 토대로 피자 배달 서비스(extension)의 interaction 모델을 정의한다는 것은 메뉴 조회 intent, 주문 intent, 배달 조회 intent와 같은 intent 목록을 선언하고 각 intent에서 어떤 정보(slot)를 취할지 어떤 발화 예시가 있는지 열거하는 것이라고 보면됩니다. 따라서, **interaction 모델을 정의할 때 가장 먼저해야 할 일은 extension이 어떤 범주의 요청을 처리해줄 것인지 정의하고 열거하는 것**입니다. 이는 extension을 개발할 때 비즈니스 로직, 즉 프로그램의 분기를 나누는 기준이 되기도 합니다.

![](/DevConsole/Resources/Images/DevConsole-Design_Interaction_Model.png)

**사용자 요청의 범주를 나눴다면 각 범주에 이름을 정의해야 합니다.** 이는 곧 intent의 이름이 됩니다. 피자 배달 서비스의 "주문 intent"와 같은 것은 추상적인 개념과 같은 것이고 이를 extension이 알 수 있는 구체적인 이름 즉 식별될 수 있는 문자열로 선언해야 합니다. 예를 들면, "주문 intent"는 "OrderPizza"와 같은 이름으로 선언할 수 있습니다.

이제 "OrderPizza" intent가 사용자의 발화로부터 **어떤 정보([Slot](#Slot))를 취해야 하는지 정의**해야 하며, 어떤 식의 사용자 발화를 처리할 수 있는지 **다양한 [발화 예시](#UtteranceExample)를 열거**해야 합니다.

### Slot {#Slot}

Slot은 사용자의 발화로부터 획득하는 정보이며, [custom intent](#Intent)를 정의할 때 해당 intent가 필요한 slot이 무엇인지 정의해야 합니다. 소프트웨어 개발에 비유해 설명하자면 extension이 특정 범주의 사용자 요청을 처리하는 함수 또는 핸들러가 intent이고 이때 이 함수나 핸들러에 필요한 파라미터가 slot입니다. 위에서 언급했던 "페퍼로니 피자 2판 주문해줘"라는 사용자 발화를 보면 "OrderPizza" intent를 처리하려면 "페퍼로니 피자"와 같은 피자 종류에 대한 정보와 "2판"과 같은 수량 정보가 필요하다는 것을 알 수 있습니다. Intent를 정의할 때 어떤 정보(slot)가 필요한지 미리 파악해둬야 합니다.

Slot을 선언할 때 slot이 어떤 유형의 정보인지 구분해야 하며 이를 slot 타입이라고 합니다. slot 타입은 built-in slot 타입과 custom slot 타입으로 나뉩니다. Built-in slot 타입은 Clova에서 미리 정의해둔 정보 유형으로서 모든 서비스(extension)에서 범용적으로 사용될 수 있는 정보 표현을 정의한 것입니다. Built-in slot 타입은 주로 시간, 장소, 수량 등과 같은 정보를 인식해야 할 때 사용됩니다. 위 발화를 예로 들면 "2판"에 해당하는 정보를 인식하기 위해 built-in slot 타입을 사용할 수 있습니다. Clova는 다음과 같은 built-in slot 타입을 제공하고 있습니다.

| Built-in slot 타입 이름 | 설명                                            |
| ----------------------|------------------------------------------------|
| CLOVA.DATETIME      | 날짜 및 시간 표현에 해당하는 정보입니다. (예: "10분 30초", "오전 9시", "1시간 전", "12시", "정오", "2017년 8월 4일", "저번 달 마지막 날") |
| CLOVA.DURATION      | 기간 표현에 해당하는 정보입니다. (예: "하루", "밤새", "한 달", "다음주", "주말") |
| CLOVA.NUMBER        | 숫자 표현에 해당하는 정보입니다. 수량 명사를 포함합니다. (예: "한번", "7명", "하나", "30살", "8정도", "16칸") |
| CLOVA.RELATIVETIME  | 상대적인 시간 표현에 해당하는 정보입니다. (예: "앞으로", "이따가", "잠시후", "방금", "아까") |
| CLOVA.UNIT          | 단위 표현에 해당하는 정보입니다. (예: "113평", "100메가", "25마일") |
| CLOVA.ORDER         | 순서 표현에 해당하는 정보입니다. (예: "넥스트", "앞", "이전", "마지막", "다음", "이번", "지난", "마지막") |
| CLOVA.KO_ADDRESS_[행정 구역 단위] | 국내의 행정 구역 단위에 따라 불리는 지명 표현을 의미하는 정보입니다. Clova가 제공하는 행정 구역 단위는 Clova developer console을 통해서 확인하면 됩니다. |
| CLOVA.WORLD_COUNTRY | 세계의 국가명 표현에 해당하는 정보입니다. (예: "가나", "일본", "대한민국", "프랑스") |
| CLOVA.WORLD_CITY    | 세계의 도시명 표현에 해당하는 정보입니다. (예: "뉴욕", "파리", "런던") |
| CLOVA.CURRENCY      | 화폐 표현에 해당하는 정보입니다. (예: "위안", "엔", "달러", "러시아 돈", "영국 통화") |
| CLOVA.OFFICIALDATE  | 공휴일 및 국경일, 기념일 표현에 해당하는 정보입니다. (예: "입춘", "신정", "석가탄신일", "광복절") |

Custom slot 타입은 제공하는 서비스(extension)의 도메인에 특화된 정보 유형을 정의한 것으로 custom slot 타입을 만들 때 주로 고유 명사 또는 명사를 지정합니다. 위 발화를 예를 들면 "OrderPizza" intent는 피자의 종류에 해당하는 정보(slot)를 사용자 발화에서 파악해야 하며 피자 종류를 나타내는 표현은 피자와 관련된 서비스에서만 사용될 가능성이 큽니다. 따라서 "PIZZA_TYPE"과 같은 custom slot 타입을 정의하고 "PIZZA_TYPE"에는 피자 배달 서비스에서 주문 가능한 "페퍼로니 피자", "콤비네이션 피자", "치즈 피자"와 같은 항목들이 표현될 수 있음을 선언할 수 있습니다.

다만, 이런 항목들은 문장에서 같은 의미를 지니지만 비슷하거나 다양하게 표현될 수 있습니다. "바베큐 피자"는 "BBQ 피자"와 같은 동의어를 가질 수 있으며, "쉬림프 골드 크러스트 피자"와 같이 이름이 긴 경우 "쉬림프 골크 피자"처럼 사용자들이 흔히 짧게 부르는 표현이 존재할 수 있습니다. 따라서 custom slot 타입을 정의할 때 개념적으로 구분된 항목을 선언해야 할뿐만 아니라 각 항목의 대표어와 동의어/유의어를 정의해줘야 합니다. 이는 사용자 발화를 인식하는 과정에서 다양하게 표현된 동의어/유의어를 대표어로 전환해주며, extension이 intent를 처리할 때 같은 개념에 해당하는 정보를 일관된 값으로 받을 수 있도록 해줍니다.

위와 같이 slot 타입을 정의하고 나면 각 intent에서 사용할 slot의 이름을 정의하고 해당 slot이 어떤 slot 타입을 가지는지 선언해야 합니다. 예를 들면, "OrderPizza" intent는 피자 종류 정보를 위해 "pizzaType", 피자 수량 정보를 위해 "pizzaAmount"라는 slot을 선언하고 각 slot에 미리 정의해둔 "PIZZA_TYPE" custome slot 타입과 이미 제공되고 있는 CLOVA.NUMBER built-in slot 타입을 지정할 수 있습니다.

### 발화 예시 {#UtteranceExample}
Intent를 정의할 때 다양한 사용자 발화 예시를 열거할 수 있습니다. 발화 예시는 비슷한 의도를 지닌 다양한 사용자의 표현을 Clova가 인식하는데 필요한 기반 데이터가 되며 위에서 언급한 slot이 사용자 발화 중 어느 위치에 있는지 파악할 때 사용됩니다. 참고로 보통 서술어(동사)에 의해 intent가 결정됩니다. 그리고 발화 예시를 작성할 때는 intent의 의미에 딱맞는 표현을 반복적으로 사용하기 보다는 비슷한 의미를 가진 다양한 사용자 표현을 나열하는 것이 좋습니다. 이는 사용자 의도를 잘 인식하는 interaction 모델을 만들 수 있는 가장 좋은 방법입니다.

다음은 피자 배달 서비스의 주문과 관련된 intent(OrderPizza)에 입력될 수 있는 발화 예시 목록이며, 잘 작성된 예와 그렇지 않은 예를 보여줍니다.

<table>
  <thead>
    <tr>
      <th width="50%">좋은 예</th>
      <th width="50%">나쁜 예</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>
        <pre>페퍼로니 피자 1판 주문해줘.
BBQ 피자 2판 배달시켜줄래?
콤비네이션 세 개 시켜줘.
쉬림프 골크 피자 하나 부탁해.
...</pre>
      </td>
      <td>
        <pre>페퍼로니 피자 1판 주문해줘.
콤비네이션 피자 1판 주문해줘.
불고기 피자 1판 주문해줘.
치즈 피자 1판 주문해줘.
...</pre>
      </td>
    </tr>
  </tbody>
</table>

위와 같이 "OrderPizza" intent에 관련된 발화를 텍스트로 열거한 후 각 slot에 해당하는 영역을 표시하게 됩니다. CLOVA.NUMBER built-in slot 타입과 "PIZZA_TYPE"이라는 slot 타입으로부터 과 이는 추후 Clova developer console에서 Intent를 등록할 때 처리하게 됩니다.

{% raw %}

```
<pizzaType>페퍼로니</pizzaType> <pizzaAmount>2판</pizzaAmount> 주문해줘.
<pizzaType>BBQ 피자</pizzaType> <pizzaAmount>2판</pizzaAmount> 배달시켜줄래?
<pizzaType>콤비네이션 피자</pizzaType> <pizzaAmount>2개</pizzaAmount> 시켜줘.
<pizzaType>쉬림프 골크</pizzaType> <pizzaAmount>하나</pizzaAmount> 부탁해.
...
```
{% endraw %}


추후 custom extension은 다음과 같은 메시지를 수신하게 됩니다.

{% raw %}

```json
// Custom intent: 페퍼로니 피자 2판 주문해줘.
{
  "version": "0.1.0",
  "session": {
    "new": false,
    "sessionAttributes": {},
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
      "name": "OrderPizza",
      "slots": {
        "pizzaAmount": {
          "name": "pizzaAmount",
          "value": "2"
        },
        "pizzaType": {
          "name": "pizzaType",
          "value": "페퍼로니"
        }
      }
    }
  }
}

// Built-in intent: 취소해줘
{
  "version": "0.1.0",
  "session": {
    "new": false,
    "sessionAttributes": {},
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
      "name": "Clova.CancelIntent",
      "slots": {}
    }
  }
}
```

{% endraw %}

## Built-in slot 타입 추가하기 {#AddBuiltinSlotType}

서비스를 제공할 extension이 어떤 [built-in slot 타입](#Slot)을 사용할지 결정했다면 해당 extension의 interaction 모델에 built-in slot 타입을 추가해야 합니다. 예를 들어 피자 배달 extension을 만든다면, 피자 수량에 대한 정보 표현이 사용자 발화에 사용될 수 있습니다. 따라서 이와 관련된 built-in slot 타입을 extension에서 사용해야 한다면 다음과 같은 단계로 built-in slot 타입을 extension에 추가할 수 있습니다.

<ol>
  <li><strong>Slot 타입</strong> 패널의 우측 상단이나 <strong>인터랙션 모델 빌더 메뉴</strong> 아래에서 <strong>사용중인 Slot 타입</strong> 메뉴 영역 우측 상단에 있는 <img src="/DevConsole/Resources/Images/DevConsole-Plus_Button.png" /> 버튼을 클릭합니다. 버튼을 클릭하면 <strong>인터렉션 모델: Slot 타입 추가하기</strong> 화면이 표시됩니다.</li>
  <li>필요한 built-in slot 타입의 체크 박스를 체크합니다.</li>
  <img src="/DevConsole/Resources/Images/DevConsole-Add_Built-in_Slot.png" />
  <li>필요한 built-in slot 타입을 체크한 후 페이지 맨 아래에 있는 <strong>만들기</strong> 버튼을 클릭합니다.</li>
</ol>

위 과정을 수행하고 나면 **인터랙션 모델: 대시보드** 화면의 **Slot 타입 패널**에 다음과 같이 built-in slot 타입이 추가된 것을 확인할 수 있습니다.

![](/DevConsole/Resources/Images/DevConsole-Added_Built-in_Slot.png)

## Custom slot 타입 추가하기 {#AddCustomSlotType}

이제 extension에서 사용할 [custom slot 타입](#Slot)을 정의해야 합니다. [Built-in slot 타입 추가하기](#AddBuiltinSlotType) 절에 이어 피자 배달 서비스 extension 계속 예로 들면, 사용자의 발화 중 피자 종류에 해당하는 부분을 custom slot 타입으로 정의해야 할 것 입니다. 다음과 같은 대표어와 동의어를 가지는 "PIZZA_TYPE"이라는 custom slot 타입을 추가한다고 가정하겠습니다.

| 대표어           | 동의어                                        |
|----------------|----------------------------------------------|
| 페퍼로니          | 페퍼로니 피자                                  |
| 바베큐           | 바베큐 피자, BBQ 피자                           |
| 치즈             | 치즈 피자                                     |
| 야채             | 야채 피자, 베지 피자, 베지테리언 피자               |
| 쉬림프 골드 크러스트 | 쉬림프 골드 크러스트 피자, 쉬림프 골크 피자, 쉬림프 골크 |

다음 절차에 따라 custom slot 타입을 추가합니다.

<ol>
  <li><strong>Slot 타입</strong> 패널의 우측 상단이나 <strong>인터랙션 모델 빌더 메뉴</strong> 아래에서 <strong>사용중인 Slot 타입</strong> 메뉴 영역 우측 상단에 있는 <img src="/DevConsole/Resources/Images/DevConsole-Plus_Button.png" /> 버튼을 클릭합니다. 버튼을 클릭하면 <strong>인터렉션 모델: Slot 타입 추가하기</strong> 화면이 표시됩니다.</li>
  <li><strong>새로운 slot 타입 만들기</strong>의 입력 필드에 추가할 custom slot 타입의 이름을 입력하고 <strong>만들기</strong> 버튼을 클릭합니다. Custom slot 타입이 생성되면 해당 custom slot 타입에 대한 상세 정보를 볼 수 있는 화면이 나타납니다.</li>
  <img src="/DevConsole/Resources/Images/DevConsole-Add_Custom_Slot_1.png" />
  <li><strong>Slot 타입 사전</strong>에 <img src="/DevConsole/Resources/Images/DevConsole-Plus_Button.png" /> 버튼을 클릭하여 대표어를 추가합니다.</li>
  <img src="/DevConsole/Resources/Images/DevConsole-Add_Custom_Slot_2.png" />
  <li>추가한 대표어에 동의어나 유사 표현을 추가합니다.</li>
  <img src="/DevConsole/Resources/Images/DevConsole-Add_Custom_Slot_3.png" />
  <li>마지막으로 우측 상단에 있는 <strong>저장</strong> 버튼을 클릭합니다.</li>
</ol>

오른쪽의 <strong>대시 보드</strong> 메뉴를 통해 **인터렉션 모델: 대시보드**로 이동하면 custom slot 타입이 추가된 것을 확인할 수 있습니다.

![](/DevConsole/Resources/Images/DevConsole-Added_Custom_Slot.png)

정의하려는 custom slot 타입에 대량의 정보를 입력해야 하는 경우 TSV(Tab-separated values, .tsv) 형식의 파일을 업로드할 수도 있습니다. TSV 파일의 각 행의 첫 번째 값은 대표어가 되며, 그 다음부터 탭 문자로 구분된 값은 대표어에 대한 동의어나 유사 표현이 됩니다. 다음은 "PIZZA_TYPE" custom slot 타입의 정의를 TSV 형식으로 표현한 예입니다.

```
페퍼로니    페퍼로니 피자
바베큐      바베큐 피자      BBQ 피자
치즈       치즈 피자
야채       야채 피자        베지 피자       베지테리언 피자
쉬림프 골드 크러스트         쉬림프 골드 크러스트 피자       쉬림프 골크 피자       쉬림프 골크
```

다음에 표시된 **업로드**, **다운로드** 버튼을 클릭하면 미리 TSV 파일에 정의한 custom slot 타입의 정의를 업로드하거나 현재 작성된 custom slot의 정의를 TSV 파일로 다운로드할 수 있습니다.

![](/DevConsole/Resources/Images/DevConsole-Custom_Slot_Upload_and_Download_Button.png)

## Built-in intent 추가하기 {#AddBuiltinIntent}

[Built-in intent](#Intent)는 Clova 플랫폼이 일부 공통적인 사용자 요청 범주를 정하고 이를 공유하여 사용하기 위해 선언한 intent입니다. 예를 들면, 일반적으로 빈번히 발생할 수 있는 사용자의 긍정/부정 요청, 중지나 취소와 같은 요청을 intent로 미리 정의해 둔 것입니다. Extension에서 사용할 built-in intent를 선택적으로 추가할 수 있습니다.

<div class="note">
  <p><strong>Note!</strong></p>
  <p>현재 모든 extension은 Clova가 제공하는 built-in intent를 모두 처리할 수 있어야 합니다. 추후 extension별로 필요한 built-in intent를 선택적으로 사용할 수 있게 변경할 예정입니다. 따라서, 이 절에 대한 내용은 조만간 업데이트될 예정입니다.</p>
</div>

## Custom intent 추가하기 {#AddCustomIntent}
Extension에서 사용할 [built-in slot 타입](#AddBuiltinSlotType)과 [custom slot 타입](#AddCustomSlotType)을 추가했다면 이제 custom intent를 추가하면 됩니다. 이전 설명에 이어서 피자를 주문하는 사용자의 요청을 가정하고 다음 절차에 따라 "OrderPizza"라는 이름의 intent를 추가합니다.

<ol>
  <li><strong>Intents</strong> 패널의 우측 상단이나 <strong>인터랙션 모델 빌더 메뉴</strong> 아래에서 <strong>사용중인 Intent</strong> 영역 우측 상단에 있는 <img src="/DevConsole/Resources/Images/DevConsole-Plus_Button.png" /> 버튼을 클릭합니다. 버튼을 클릭하면 <strong>인터렉션 모델: Intent 추가하기</strong> 화면이 표시됩니다.</li>
  <li><strong>새로운 커스텀 Intent 만들기</strong>의 입력 필드에 추가할 custom intent의 이름을 입력하고 <strong>만들기</strong> 버튼을 클릭합니다. Custom intent가 생성되면 해당 custom intent에 대한 상세 정보를 볼 수 있는 화면이 나타납니다.</li>
  <img src="/DevConsole/Resources/Images/DevConsole-Add_Custom_Intent_1.png" />
  <li><strong>Intent Slot 리스트</strong>의 입력 필드에 추가할 slot의 이름을 입력하고 오른쪽에 있는 <img src="/DevConsole/Resources/Images/DevConsole-Plus_Button.png" /> 버튼을 클릭하여 Slot을 추가합니다.</li>
  <img src="/DevConsole/Resources/Images/DevConsole-Add_Custom_Intent_2.png" />
  <li>Slot을 추가한 후 해당 slot이 어떤 slot 타입인지 지정합니다.</li>
  <img src="/DevConsole/Resources/Images/DevConsole-Add_Custom_Intent_3.png" />
  <li>이제 <strong>사용자 표현 리스트</strong>에 사용자 발화 예시를 입력하고 오른쪽에 있는 <img src="/DevConsole/Resources/Images/DevConsole-Plus_Button.png" /> 버튼을 클릭하여 사용자 발화 예시를 추가합니다.</li>
  <img src="/DevConsole/Resources/Images/DevConsole-Add_Custom_Intent_4.png" />
  <li>추가한 발화 예시에서 slot으로 처리할 부분을 드래그하여 slot을 지정해줍니다.</li>
  <img src="/DevConsole/Resources/Images/DevConsole-Add_Custom_Intent_5.png" />
  <li>5번과 6번 단계를 반복하여 intent에 발화 예시를 필요한 만큼 추가합니다.</li>
  <li>마지막으로 우측 상단에 있는 <strong>저장</strong> 버튼을 클릭합니다.</li>
</ol>

참고로 발화 예시는 사용자 언어를 분석하는 기반 데이터가 되기 때문에 intent에 대한 발화 예시가 많고 표현이 다양할수록 사용자의 의도를 더 잘 분석할 확률이 커집니다. 따라서 발화 예시는 하나의 intent에 최소 30개 이상의 발화 예시를 입력하는 것이 좋습니다.

Custom slot 타입을 추가할 때와 마찬가지로 정의하려는 TSV(Tab-separated values, .tsv) 형식의 파일을 업로드할 수도 있습니다. TSV 파일은 두 부분으로 나뉘며 각각 intent의 slot을 정의하는 부분과 발화 예시를 나열하는 부분으로 나뉩니다. Intent의 slot을 정의하는 부분이 파일의 앞 부분에 오며 `[INTENT SLOT]`이 입력된 줄 바로 다음에 slot이 나열됩니다. 탭 문자로 구분된 첫 번째 열은 intent에서 사용되는 slot의 이름이며, 두 번째 열은 slot type입니다.

Intent의 발화 예시를 열거하는 내용은 파일의 뒷 부분에 오며 `[INTENT EXPRESSION]`이 입력된 줄 바로 다음에 발화 예시가 나열됩니다. 발화 예시에서 slot을 구분하기 위해 slot 이름으로 된 태그로 관련 표현 부분을 감싸야 합니다. 다음은 intent를 정의한 TSV 파일 예입니다.

```
[INTENT SLOT]
pizzaType	PIZZA_TYPE
pizzaAmount	CLOVA.NUMBER

[INTENT EXPRESSION]
<pizzaType>페퍼로니</pizzaType> <pizzaAmount>2판</pizzaAmount> 주문해줘.
<pizzaType>BBQ 피자</pizzaType> <pizzaAmount>2판</pizzaAmount> 배달시켜줄래?
<pizzaType>콤비네이션 피자</pizzaType> <pizzaAmount>2개</pizzaAmount> 시켜줘.
<pizzaType>쉬림프 골크</pizzaType> <pizzaAmount>하나</pizzaAmount> 부탁해.
...
```

다음에 표시된 **업로드**, **다운로드** 버튼을 클릭하면 미리 TSV 파일에 정의한 custom slot의 정의를 업로드하거나 현재 작성된 custom slot의 정의를 TSV 파일로 다운로드할 수 있습니다.

![](/DevConsole/Resources/Images/DevConsole-Utterance_Example_Upload_and_Download_Button.png)

<div class="danger">
  <p><strong>Caution!</strong></p>
  <p>같은 interaction 모델 내에서는 intent와 상관 없이 slot 타입에 같은 이름을 선언하여 사용할 것을 권고합니다. 예를 들면 "OrderPizza" intent에서 피자 종류("PIZZA_TYPE")에 관련된 slot 이름이 "pizzaType"이었다면 다른 intent에서도 같은 slot 타입을 선언해서 사용할 때 같은 이름인 "pizzaType"을 사용해야 합니다. 다만, "서울에서 부산 가는데 걸리는 시간 알려줘"와 같이 "서울"과 "부산"이 같은 slot 타입이라도 사용 목적이 구분되어야 하는 상황에서는 slot의 이름을 구분하여 작성합니다.</p>
</div>

여기까지 하나의 intent를 interaction 모델에 추가하는 방법을 설명했습니다. 앞에서 설명했던 방법을 반복하여 extension에 intent를 필요한 만큼 추가하면 다음과 같이 interaction 모델을 완성할 수 있습니다.

![](/DevConsole/Resources/Images/DevConsole-Added_Interaction_Model.png)
