# Custom extension 만들기

Custom extension이란 Clova가 기본으로 제공하고 있는 기능이나 서비스가 아닌 개발자가 임의로 확장한 기능이나 외부 서비스를 제공해주는 extension입니다. 예를 들면, 웹 검색, 뉴스 클리핑과 같은 서비스 뿐만 사용자 계정의 인증이 필요한 음악, 쇼핑, 금융 서비스와 같은 외부 서비스를 제공하는 extension입니다. Custom extension은 CEK로부터 분석된 사용자의 발화 정보를 전달받게 되며, 이에 상응하는 내용을 처리하고 그 서비스 처리 결과를 반환해야 합니다. Custom extension을 만들기 위해 사전에 준비해야 할 것이 무엇이 있고 CEK와 어떤 메시지를 주고 받으면서 어떻게 동작을 수행해야 하는지 설명합니다.

다음과 같은 순서로 custom extension 개발자가 알아야 할 내용을 전달하고 있습니다.

1. [사전 준비사항](#Preparation)
2. [Custom extension 요청 처리하기](#HandleCustomExtensionRequest)
   * [`LaunchRequest` 요청 처리](#HandleLaunchRequest)
   * [`IntentRequest` 요청 처리](#HandleIntentRequest)
   * [`SessionEndedRequest` 요청 처리](#HandleSessionEndedRequest)
3. [Custom extension 응답 반환하기](#ReturnCustomExtensionResponse)
4. [Multi-turn 대화 수행하기](#DoMultiturnDialog)

{% include "./BuildCustomExtension/Preparation.md" %}

{% include "./BuildCustomExtension/Handle_Custom_Extension_Request.md" %}

{% include "./BuildCustomExtension/Return_Custom_Extension_Response.md" %}

{% include "./BuildCustomExtension/Do_Multiturn_Dialog.md" %}
