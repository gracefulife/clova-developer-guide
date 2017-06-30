# CIC 개요
이 문서는 Clova Interface Connect(이하 CIC)에 대해 자세히 설명합니다. 이 문서를 통해 CIC가 무엇이고 어떻게 동작하는지 파악할 수 있으며, CIC와 관련된 가이드나 레퍼런스를 제공합니다.

## CIC란? {#WhatisCIC}
CIC는 인공 지능 비서 서비스를 제공하려는 PC/모바일용 앱, 모바일 또는 가전 기기 등의 클라이언트에게 Clova와 연동할 수 있는 인터페이스를 제공하는 플랫폼입니다. CIC가 제공하는 [API](/CIC/References/CIC_API.md)를 통해 사용자의 요청을 Clova로 전달하며 Clova의 응답을 CIC를 통해 클라이언트에게 제공합니다.

![](/CIC/Resources/Images/CIC_Interaction_Structure.png)

## CIC 동작 구조 {#CICInteractionStructure}
클라이언트는 CIC API를 통해 사용자의 요청을 CIC로 전달하며 응답 결과를 CIC로부터 전달받습니다. CIC에 접속하기 위해 [HTTP/2 프로토콜](https://tools.ietf.org/html/rfc7540)을 사용해야 하며, 음성 인식, 음성 출력, 음악 재생, 개인 일정 관리, 알람/타이머 설정과 같은 기능을 [API](/CIC/References/CIC_API.md)를 통해 제공하고 있습니다.

CIC API를 통해 클라이언트와 CIC 사이에 다양한 커뮤니케이션이 발생합니다. 이때, 커뮤니케이션 방향에 따라 다음과 같은 유형의 메시지가 전달됩니다.

* [이벤트 메시지](/CIC/References/CIC_Message_Format.md#Event): 클라이언트에서 CIC로 전달하는 메시지입니다. 사용자 요청(음성 입력)을 전달하거나 클라이언트의 상태 값이 변경된 것을 알릴 때 이 메시지를 전송합니다.

* [지시 메시지](/CIC/References/CIC_Message_Format.md#Directive): CIC가 클라이언트의 행동을 제어하도록 명세한 메시지입니다. 예를 들면, 앱에 특정 정보를 표시하거나 합성된 음성을 출력하도록 요청하는 메시지입니다. 이런 지시 메시지는 다음과 같은 상황에 전달됩니다.
    * 사용자 요청에 대한 응답 메시지로서 주로 사용자의 음성이 인식된 후 그 의도를 클라이언트가 수행하도록 하기 위해 전달됩니다.
    * 특정 조건에 의해 사용자의 요청 없이 CIC가 클라이언트로 지시 메시지를 먼저 보낼 수도 있습니다.

다음은 CIC와 클라이언트 사이의 메시지 송수신 동작 예를 나타낸 시퀀스 다이어그램입니다.

![](/CIC/Resources/Images/CIC_Interaction_Example_in_Sequence_Diagram.png)
