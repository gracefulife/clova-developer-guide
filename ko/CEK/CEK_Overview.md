# CEK 개요
이 문서는 Clova Extension Kit(이하 CEK)에 대해 자세히 설명합니다. 이 문서를 통해 CEK가 무엇이고 어떻게 동작하는지 파악할 수 있으며, CEK와 관련된 가이드나 레퍼런스를 제공합니다.

## CEK란? {#WhatisCEK}
Clova extension(이하 extension)은 사용자에게 외부 서비스(3rd party service)나 집안의 IoT 기기 제어 등 다양한 경험을 제공할 수 있도록 Clova에게 확장적 기능을 제공하는 웹 서비스입니다. CEK는 extension을 개발할 때 필요한 도구와 인터페이스를 제공하는 플랫폼입니다.

CEK는 다음과 같은 기능을 제공합니다.
* Interaction 모델 관리 (Clova Developer Console 제공)
* Clova와 extension 간 인터페이스 제공 ([CEK 메시지 포맷](/CEK/References/CEK_Message_Format.md))

<div class="note">
  <p><strong>Note!</strong></p>
  <p>현재 Clova Developer Console을 개발하고 있는 중입니다. 따라서, Interaction 모델을 정의하려면 제휴 담당자와 협의하기 바랍니다.</p>
</div>

![](/CEK/Resources/Images/CEK_Interaction_Structure.png)

## CEK 동작 구조 {#CEKInteractionStructure}
Extension은 CEK로부터 분석된 사용자의 요청을 전달받으며, extension은 사용자 요청에 대한 처리 결과를 응답으로 돌려줘야 합니다. 이때 미리 정의된 [CEK 메시지 포맷](/CEK/References/CEK_Message_Format.md)에 맞게 메시지를 주고 받게 됩니다.

CEK와 extension 사이에 다양한 커뮤니케이션이 발생합니다. 이때, 커뮤니케이션 방향에 따라 다음과 같은 유형의 메시지가 전달됩니다.







* [이벤트 메시지](/CEK/References/CEK_Message_Format.md#Event): 클라이언트에서 CEK로 전달하는 메시지입니다. 사용자 요청(음성 입력)을 전달하거나 클라이언트의 상태 값이 변경된 것을 알릴 때 이 메시지를 전송합니다.

* [지시 메시지](/CEK/References/CEK_Message_Format.md#Directive): CEK가 클라이언트의 행동을 제어하도록 명세한 메시지입니다. 예를 들면, 앱에 특정 정보를 표시하거나 합성된 음성을 출력하도록 요청하는 메시지입니다. 이런 지시 메시지는 다음과 같은 상황에 전달됩니다.
    * 사용자 요청에 대한 응답 메시지로서 주로 사용자의 음성이 인식된 후 그 의도를 클라이언트가 수행하도록 하기 위해 전달됩니다.
    * 특정 조건에 의해 사용자의 요청 없이 CEK가 클라이언트로 지시 메시지를 먼저 보낼 수도 있습니다.

다음은 CEK와 클라이언트 사이의 메시지 송수신 동작 예를 나타낸 시퀀스 다이어그램입니다.

![](/CEK/Resources/Images/CEK_Interaction_Example_in_Sequence_Diagram.png)

## Extension 종류


* Custom extension
* Clova Home extension
