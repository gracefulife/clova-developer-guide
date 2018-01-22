# Extension 디자인 가이드라인

새로운 extension을 만들 때 보유하고 있는 기술이나 서비스가 Clova를 통해 사용자에게 어떻게 편리함과 이익을 가져다 줄 수 있는지 생각하는 설계 활동을 해야 합니다. 이 문서는 사용자에게 건전하고 유익한 서비스를 제공하기 위해 extension을 설계할 때 어떤 사항을 지키거나 따라야 하는지 가이드라인을 제공합니다.

웹 서비스의 정보 조회, 쇼핑 및 배달 서비스, 대화형 게임, 방송 또는 실시간 브리핑, IoT 기기 제어 및 그 밖의 음성을 통한 활동이나 서비스를 제공하는 extension 을 만들 수 있습니다. 어떤 종류의 extension을 만들지 결정했다면 Extension을 설계할 때 다음과 같은 사항들을 수행 및 준수해야 합니다. 참고로 여기서 다루는 내용은 extension 설계의 기본 권장 사항이며 간단한 예시와 함께 설명하고 있습니다. 물론, 보유하고 계신 사업적 경험과 서비스의 특성에 따라 extension이 더 많은 가능성을 가지도록 설계/구현할 수도 있습니다.

* [목표 수립](#SettingGoal)
* [사용 시나리오 스크립트 작성](#MakeUseCaseScenarioScript)
* [Interaction 모델 정의](#DefineInteractionModel)
* [유의사항](#Precautions)
* [플랫폼 지원 오디오 압축 포맷](#SupportedAudioCompressionFormat)
* [지속적인 업데이트](#ContinuousUpdate)

## 목표 수립 {#SettingGoal}

Extension을 설계할 때 제일 먼저 할 일은 Extension의 목표를 정하는 것입니다. Extension의 목표는 구체적으로 사용자에게 무엇을 어떻게 전달할 것인지 정하는 것이라고 보면 됩니다. Extension의 목표를 정하는 것은 추후 사용자에게 어떤 기능을 제공하고 이 기능을 사용자가 어떤 시나리오로 사용할지 예상하는 근거가 됩니다. Extension의 목표는 다음과 같은 하나의 근본적이고 추상적인 목표가 있을 수 있습니다.

```
사용자에게 피자 배달 서비스를 제공한다.
```

위와 같이 정한 extension 목표는 좀 더 구체적인 세부 목표들로 다시 기술될 수 있습니다. 세부 목표를 작성할 때는 다음과 같은 항목을 참고하여 정의합니다.

* 세부 목표는 사용자의 입장에서 작성합니다.
* 세부 목표에는 사용자가 extension을 어떻게 호출할 수 있는지에 대한 내용도 포함합니다.
* 세부 목표 달성에 필요한 조건과 성취하게 되는 결과를 조합하여 작성할 것을 권장합니다. 필요 조건에는 다음과 같은 것들이 있을 수 있습니다.
  - 사전 필요 동작이나 상태
  - Extension이 필요로 하는 기능이나 자원(GPS, 카메라, 마이크)
  - 외부 서비스나 플랫폼의 정보 (모바일 기기 연락처 정보, SNS 계정 정보)
* 세부 목표의 집합이 달성하려는 extension 목표의 범위를 모두 포함하고 있는지 확인합니다.
* 하나의 세부 목표는 서비스에서 구분하여 처리하는 하나의 사용자 액션 단위와 같은 수준으로 작성할 것을 권장합니다.

다음은 피자 배달 서비스를 고려하여 만든 세부 목표 예제입니다.

| 세부 목표 ID | 분류                | 목표                                                            |
|------------|--------------------|---------------------------------------------------------------|
| #1         | 서비스 호출           | 사용자가 "피자봇에서~"로 발화를 시작하면 피자 배달 서비스를 사용할 수 있다.    |
| #2         | 사용 제안 또는 추천     | 피자 배달 서비스가 시작되면 사용자는 피자 주문시 예상되는 다음 동작이나 다음 동작에 대한 안내를 제공받을 수 있다. |
| #3         | 브랜드 조회 및 선택     | 사용자는 피자 브랜드를 선택할 수 있다.                                 |
| #4         | 메뉴 조회 및 선택      | 사용자는 피자 메뉴를 조회할 수 있다.                                   |
| #5         | 주문 및 결제          | 사용자가 피자 종류, 수량 및 배달 주소 정보가 있으면 사용자는 피자 주문를 할 수 있다. |
| #6         | 사용 제안 또는 추천     | 사용자는 피자 브랜드를 선택하면 최근 주문한 정보를 통해 피자, 배달 목적지 및 결제 방법을 제안받을 수 있다. |
| #7         | 사용 제안 또는 추천     | 사용자가 다른 메뉴를 요청하면 사용자는 extension이 추천하는 메뉴를 추천 받을 수 있다. |
| #8         | 주문 및 결제          | 사용자는 카메라를 이용하여 결제 시 쿠폰을 적용할 수 있다.                    |
| #9         | 배송 조회             | 사용자가 주문을 완료하면 이후 사용자는 피자 준비 및 배달 상황을 조회할 수 있다.  |
| ...        | ...                 | ...                                                            |

<div class="note">
  <p><strong>Note!</strong></p>
  <p>이렇게 작성된 세부 목표들은 <a href="#MakeUseCaseScenarioScript">사용 시나리오 스크립트를 작성</a>하거나 <a href="#DefineInteractionModel">interaction 모델</a>을 정의하는 기반 정보가 됩니다. 또한, <a href="/DevConsole/Guides/CEK/Deploy_Extension.md#InputDeploymentInfo">extension을 배포</a>할 때 이 정보를 등록해야 하며, 이를 기준으로 extension이 제대로 동작하는지 <a href="/DevConsole/Guides/CEK/Deploy_Extension.md#RequestExtensionSubmission">심사</a>를 받게 됩니다.</p>
</div>

## 사용 시나리오 스크립트 작성 {#MakeUseCaseScenarioScript}

사용 시나리오 스크립트는 사용자와 Clova 사이의 대화를 미리 예상한 것입니다. 세부 목표를 기반으로 다양한 사용 시나리오에 사용자와 Clova의 대화를 미리 예상해 봄으로써 서비스의 편의성, 흐름 등을 점검할 수 있습니다. [목표 수립](#SettingGoal)에서 정한 세부 목표를 기준으로 예상되는 사용 시나리오 스크립트를 작성합니다. 이는 추후 [interaction 모델](#DefineInteractionModel)을 등록할 때 재사용될 수 있습니다.

사용 시나리오 스크립트를 작성할 때는 다음을 고려하여 작성할 것을 권장합니다.

* 문어체 보다는 구어체 형식으로 작성합니다.
* Extension이 정보를 제공할 때 너무 많은 내용 또는 선택지를 주지 않습니다.
* Extension이 사용자에게 다음 동작에 대한 제안이나 서비스 사용 추천을 해야합니다.
* 반복적인 표현은 피할 것을 권장합니다.
* 항상 의도하지 않은 사용자의 요청이나 상황이 발생할 수 있음을 염두에 둬야 합니다.


다음은 사용 시나리오 스크립트를 작성한 예입니다.

| 발화 주체   | 발화 예시                                              | 관련 세부 목표  |
|-----------|------------------------------------------------------|-------------|
| 사용자      | 피자봇에서 피자 시켜줘.                                   | #1           |
| extension | 등록된 피자집은 XX피자와 YY피자가 있어요. 어디로 하시겠어요?      | #2, #3       |
| 사용자      | XX피자로 해줘.                                         | #3           |
| Extension | XX 피자 XX점의 콤비네이션 1판, 콜라 1.5리터 1개를 AA동 111번지로 보내드릴게요. 총 2만 3천원, 배달원에게 직접 결제 가능해요. 주문하시겠어요?   | #2, #6  |
| 사용자      | 다른 메뉴 알려줘.                                        | #7           |
| Extension | 슈퍼슈프림 1판, 콜라 1.5리터 1개를 AA동 111번지로 보내드릴게요. 총 2만6천5백원, 배달원에게 직접 결제 가능해요. 주문하시겠어요? | #2, #7  |
| 사용자      | 그래                                                  | #5           |
| Extension | 주문이 완료되었습니다. 주문 상태가 궁금하시면 제게 다시 물어봐주세요. | #2, #9       |
| 사용자      | 주문한 것 조회해줘                                       | #9           |
| Extension | 지금 열심히 배달 중이에요. 조금만 기다려주세요.                 | #9           |

## Interaction 모델 정의 {#DefineInteractionModel}

Clova에서 interaction 모델이란, 음성으로부터 인식된 사용자의 요청을 extension에 전달하기 위해 정형화된 포맷(JSON)으로 바꿔주는 규칙을 명세한 것입니다. 예를 들어, custom extension이 피자 배달 서비스를 제공한다고 가정할 때 "페퍼로니 피자 2판 주문해줘"와 같은 요청이 사용자로부터 입력될 수 있습니다. Interaction 모델은 이런 사용자의 요청을 아래와 같이 서비스 제공에 필요한 포맷(JSON)으로 변경하는 규칙을 정의해 놓은 것이라고 보면됩니다.

![](/Design/Resources/Images/Extension_Design-Interaction_Model_Analysis_Diagram.png)

Interaction 모델을 Clova developer console에서 정의하기 전에 우선 interaction 모델을 이해하고 설계하는 과정이 필요합니다. 이런 과정없이 무작정 Clova developer console에서 interaction 모델을 등록하게 되면 작업 효율이 떨어지거나 사용자 요청이 의도된 대로 변환되지 않을 수 있습니다. 사용자의 실제 의도를 잘 파악하는 interaction 모델을 만들려면 interaction 모델을 만들기 전에 다음과 같은 내용을 이해하고 interaction 모델 설계에 반영해야 합니다.

* [Intent](#Intent)
* [Slot](#Slot)
* [발화 예시](#UtteranceExample)

### Intent {#Intent}

Intent는 extension이 처리할 사용자의 요청을 구별한 범주이며 주로 사용자 발화문에 사용된 **동사**형 요소에 의해 Intent가 구분됩니다. Intent는 custom intent와 built-in intent로 나뉩니다. 이 중 Built-in intent는 Clova 플랫폼이 일부 공통적인 사용자 요청 범주를 정하고 이를 공유하여 사용하기 위해 선언한 명세입니다. 일반적으로 빈번히 발생할 수 있는 intent로 다음과 같은 요청을 미리 정의해 두고 있습니다.

| Built-in intent 이름       | 의도               | 대응하는 사용자 발화 예시                                      |
|---------------------------|-------------------|----------------------------------------------------------|
| Clova.GuideIntent         | 도움말 요청          | "너 뭐 할 줄 아니?", "할 줄 아는 거 말해봐", "너 할 줄 아는게 뭐냐?" |
| Clova.CancelIntent        | 실행 취소 요청        | "취소", "취소해줘"                                          |
| Clova.YesIntent           | 긍정 응답(예, Yes)   | "응", "그래", "알겠어", "알겠습니다", "오케이"                   |
| Clova.NoIntent            | 부정 응답(아니오, No) | "아니", "아니요", "싫어"                                     |

Custom intent는 built-in intent와 달리 제공하려는 서비스에 특화된 사용자 요청 범주를 정의한 것입니다. Custom intent는 다음과 같은 것을 정의한 명세입니다.
* 서비스에 어떤 범주의 사용자 요청이 있는지?
* 각 사용자 요청 범주에는 어떤 정보([Slot](#Slot))가 필요한지?
* 각 사용자 요청 범주에는 어떤 다양한 [발화 예시](#UtteranceExample)가 있는지?

피자 배달 서비스를 계속 예로 들어 설명하면, 해당 서비스는 다음과 같은 요청 범주가 있을 수 있습니다.

* 메뉴 조회 요청
* 주문 요청
* 배달 조회 요청

이를 토대로 피자 배달 서비스(extension)의 interaction 모델을 정의한다는 것은 메뉴 조회 intent, 주문 intent, 배달 조회 intent와 같은 intent 목록을 선언하고 각 intent에서 어떤 정보(slot)를 취할지 어떤 발화 예시가 있는지 열거하는 것이라고 보면됩니다. 따라서, **interaction 모델을 정의할 때 가장 먼저해야 할 일은 extension이 어떤 범주의 요청을 처리해줄 것인지 정의하고 열거하는 것**입니다. 이는 extension을 개발할 때 비즈니스 로직, 즉 프로그램의 분기를 나누는 기준이 되기도 합니다.

![](/Design/Resources/Images/Extension_Design-Design_Interaction_Model.png)

**사용자 요청의 범주를 나눴다면 각 범주에 이름을 정의해야 합니다.** 이는 곧 intent의 이름이 됩니다. 피자 배달 서비스의 "주문 intent"와 같은 것은 추상적인 개념과 같은 것이고 이를 extension이 알 수 있는 구체적인 이름 즉 식별될 수 있는 문자열로 선언해야 합니다. 예를 들면, "주문 intent"는 "OrderPizza"와 같은 이름으로 선언할 수 있습니다.

이제 "OrderPizza" intent가 사용자의 발화로부터 **어떤 정보([Slot](#Slot))를 취해야 하는지 정의**해야 하며, 어떤 식의 사용자 발화를 처리할 수 있는지 **다양한 [발화 예시](#UtteranceExample)를 열거**해야 합니다.

### Slot {#Slot}

Slot은 사용자의 발화로부터 획득하는 정보이며, 사용자 발화문에 사용된 **명사**형 요소가 Slot이 될 수 있습니다. [custom intent](#Intent)를 정의할 때 해당 intent가 필요한 slot이 무엇인지 정의해야 합니다. 소프트웨어 개발에 비유해 설명하자면 intent는 특정 범주의 사용자 요청을 처리하는 함수 또는 핸들러이고 slot은 이 함수나 핸들러에 필요한 파라미터가 됩니다. 위에서 언급했던 "페퍼로니 피자 2판 주문해줘"라는 사용자 발화를 보면 "OrderPizza" intent를 처리하려면 "페퍼로니 피자"와 같은 피자 종류에 대한 정보와 "2판"과 같은 수량 정보가 필요하다는 것을 알 수 있습니다. Intent를 정의할 때 어떤 정보(slot)가 필요한지 미리 파악해둬야 합니다.

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
Intent를 정의할 때 다양한 사용자 발화 예시를 열거할 수 있습니다. 발화 예시는 비슷한 의도를 지닌 다양한 사용자의 표현을 Clova가 인식하는데 필요한 기반 데이터가 되며 위에서 언급한 slot이 사용자 발화 중 어느 위치에 있는지 파악할 때 사용됩니다. 발화 예시를 잘 입력하면 사용자 의도를 잘 인식하는 interaction 모델을 만들 수 있습니다. 발화 예시를 작성할 때 되도록이면 다음 권고 사항을 따릅니다.

* 같은 의도를 지녔지만 다른 방식으로 표현이 되는 발화 예시를 많이 입력해야 합니다.
* 패턴이 서로 겹치지 않게 표현에 다양한 변형을 주어 발화 예시를 작성합니다.
* 발화 예시 작성 개수는 다음 기준을 따릅니다.
  * Intent에 사용된 slot이 built-in slot 타입이거나 사람이 전부 인지할 수 있는 양의 사전 크기를 가진 custom slot 타입일 경우 해당 slot이 들어가는 발화 문장을 최소 30개 이상 작성해야 합니다.
  * Intent에 사용된 slot이 가수명, 곡명, 영화 제목, 업체명 등 사전의 크기가 매우 큰 slot 타입일 경우 해당 slot이 들어가는 발화 문장을 최소 100개 이상은 작성해야 합니다.
  * 간단한 형태의 표현을 가지는 Intent이면 10개 내외의 발화 예시만 등록해도 됩니다.
* 위 기준으로 발화 예시를 입력한 후 새로운 표현이 생기거나 인식이 잘 안되는 표현을 발견할 때마다 발화 예시를 추가하는 것이 좋습니다.
* Slot 타입의 사전에 등록된 값 중에 slot인지 아닌지 판단하기 모호한 값이 있다면 해당 값을 발화 예시로 사용하여 slot임을 명시하는 것이 좋습니다. 다만, slot 타입에 모호한 값이 들어가도록 정의하지 않는 것을 더 권장합니다.

발화 예시를 많이 입력하되 패턴이 서로 겹치지 않게 표현에 다양한 변형을 주어야 한다는 의미는 다음 그림을 참조하면 이해하기 쉽습니다.

![](/Design/Resources/Images/Extension_Design-Diagram_for_Utterance_Example.png)

예를 들어, 피자 배달 서비스의 주문과 관련된 intent(OrderPizza)에 다음과 같은 발화 예시를 작성했다고 가정합니다.

```
페퍼로니 피자 1판 시켜줘.
페퍼로니 피자 1판 주문해줘.
페퍼로니 피자 1판 보내줘.
페퍼로니 피자 1판 부탁해.
```

위 발화 예시로 Clova가 학습한 경우 `"페퍼로니"`나 `"1판"`이라는 값이 사용자 발화에 포함되면 해당 발화가 `OrderPizza` intent로 인식할 가능성이 매우 높아집니다. 예를 들면, "페퍼로니 피자 1판 얼마야?"와 같이 메뉴 조회를 예상한 발화가 피자를 주문을 요청한 발화로 처리되기 쉽습니다.

따라서, 다음과 같은 형태로 발화 예시를 작성할 것을 권장합니다.

```
페퍼로니 피자 2판 시켜줘.
BBQ 피자 하나만 배달시켜줄래?
콤비네이션 세 개 보내주면 좋겠어.
쉬림프 골크 피자 빨리 부탁해, 배고파.
```

발화를 명사(피자 종류), 명사(수량), 동사(의도)와 같은 패턴으로 구성했으며, 일상적으로 사용하는 조사, 어미, 부사, 감탄사 등도 포함되어 있습니다. 발화 패턴이 더 없다면 이제 패턴을 재사용하고 slot의 값을 바꿔가면서 발화 예시를 권장 기준만큼 추가하면 됩니다. 다음 사항을 따르면서 발화 예시를 추가해야 합니다.
* 발화 예시에 사용된 slot의 값에 변화를 주면서 문장을 추가합니다.
* 조사, 어미, 부사, 감탄사 등의 사용에 변화를 주면서 문장을 추가합니다.
* **특정 값의 조합이 자주 사용되지 않도록 유의하는 것이 좋습니다.** 예를 들면, "페퍼로니 피자 2개 시켜줘"와 "페퍼로니 피자를 1판만 시켜주세요."는 어미/조사와 수량 값에 변화를 줬지만 `"페퍼로니"`와 `"시켜주다"`라는 값 조합이 중복된 예입니다.

```
바베큐 5개만 얼른 시켜.
페퍼로니 1판 먹을래.
야채 피자 부탁해.
맛있는 치츠 피자 넷 주문해주라.
```

"OrderPizza" intent에 관련된 발화를 텍스트로 열거한 후 각 slot에 해당하는 영역을 다음과 같이 표시하게 됩니다.

{% raw %}

```
<pizzaType>페퍼로니 피자</pizzaType> <pizzaAmount>2판</pizzaAmount> 시켜줘.
<pizzaType>BBQ 피자</pizzaType> <pizzaAmount>하나</pizzaAmount>만 배달시켜줄래?
<pizzaType>콤비네이션</pizzaType> <pizzaAmount>세 개</pizzaAmount> 보내주면 좋겠어.
<pizzaType>쉬림프 골크 피자</pizzaType> 빨리 부탁해, 배고파.
<pizzaType>바베큐</pizzaType> <pizzaAmount>5개</pizzaAmount>만 얼른 시켜.
<pizzaType>페퍼로니</pizzaType> <pizzaAmount>1판</pizzaAmount> 먹을래.
<pizzaType>야채 피자</pizzaType> 부탁해.
맛있는 <pizzaType>치즈 피자</pizzaType> <pizzaAmount>넷</pizzaAmount> 주문해.
...
```
{% endraw %}

<div class="note">
  <p><strong>Note!</strong></p>
  <p>추후 <a href="/DevConsole/Guides/CEK/Test_Extension.html#TestInteractionModel">interaction 모델 테스트</a>나 실제 사용자 로그를 통해 완성도를 높여 나갈 수 있습니다. Interaction 모델을 테스트할 때는 발화 예시를 작성한 사람이 아닌 다른 사람이 테스트해보는 것이 좋습니다. 이 방법은 새로운 표현 패턴을 찾는데 도움이 됩니다.</p>
</div>


[Clova developer console](/DevConsole/ClovaDevConsole_Overview.md)을 이용하여 위에서 정의한 [interaction 모델을 등록](/DevConsole/Guides/CEK/Register_Interaction_Model.md)하게 되면 [등록한 custom extension](/DevConsole/Guides/CEK/Register_Extension.md)이 다음과 같은 JSON 메시지를 수신하게 됩니다.

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

## 유의사항 {#Precautions}

Extension을 설계할 때 다음과 같은 사회적인 또는 법적인 문제가 없는지 미리 파악하여 문제가 발생하지 않도록 반드시 주의해야 합니다. Extension을 설계하는 단계뿐만 아니라 extension을 Clova에 등록하거나 배포할 때에도 아래 사항을 한 번 더 검토할 것을 권고합니다.

* 저작권 보호 의무에 대한 위반 사항이 없는지 검토
* 개인 정보 보호 의무에 대한 위반 사항이 없는지 검토
* 서비스 연결이나 데이터 제공이 일회적이지 않고 지속적일 수 있는지 검토
* 아동 또는 일반 사용자에게 해를 줄 수 있는 선정적인 콘텐츠가 없는지 검토

## 플랫폼 지원 오디오 압축 포맷 {#SupportedAudioCompressionFormat}

Extension을 통해 오디오 콘텐츠를 제공하는 경우 반드시 Clova가 지원하는 오디오 압축 포맷으로 음원을 제공해야 합니다.

{% include "/Design/SupportedMediaFormat/Supported_Audio_Format_For_KR.md" %}

<div class="danger">
  <p><strong>Caution!</strong></p>
  <p>Clova가 지원하지 않는 오디오 압축 포맷으로 음원을 제공할 경우 클라이언트가 정상적으로 음원을 재생하지 못 할 수 있습니다.</p>
</div>

## 지속적인 업데이트 {#ContinuousUpdate}

Extension을 개발할 때 사용자가 어떤 발화를 할지 예측하여 시나리오를 만들고 이를 extension에 적용합니다. 이런 활동은 extension을 개발할 때 도움이 되지만 사용자들이 실제 이용하는 방식가 차이가 있을 수 있고 사용자의 모든 사용 패턴을 대변했다고 할 수 없습니다. 즉, 사용자는 예상과 다르게 extension을 사용할 수 있습니다. 따라서, extension을 배포한 이후에도 extension의 기능이나 대화 흐름을 지속적으로 개선하는 활동을 해야 사용자의 만족도를 향상시킬 수 있습니다.

Extension 등록한 후 Clova 플랫폼이 제공하는 통계 데이터나 유입된 사용자 발화 기록(추후 제공 예정) 분석하여 꾸준히 extension을 업데이트해야 합니다.
