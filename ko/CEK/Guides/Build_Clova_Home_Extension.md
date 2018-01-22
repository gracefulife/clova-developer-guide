# Clova Home extension 만들기

Clova Home extension이란 외부 IoT 서비스를 통해 가정 내 IoT 기기에 원격 제어 기능을 제공하는 extension입니다. Clova Home extension은 CEK에게 사용자가 제어할 수 있는 IoT 기기가 어떤 것이 있는지 정보를 제공해야 합니다. 또한, CEK로부터 전달된 IoT 기기의 제어 요청을 전달받게 되며, 이에 상응하는 내용을 처리하고 그 결과를 반환해야 합니다. 다음은 Clova Home extension이 동작하는 구조를 나타낸 그림입니다.

![](/CEK/Resources/Images/CEK_Clova_Home_Extension_Operation_Structure.png)

Clova Home extension을 만들기 위해 사전에 준비해야 할 것이 무엇이 있고 CEK와 어떤 메시지를 주고 받으면서 어떻게 동작을 수행해야 하는지 설명합니다.

다음과 같은 순서로 Clova Home extension 개발자가 알아야 할 내용을 전달합니다.

1. [사전 준비사항](#Preparation)
2. [Discovery 기능 제공하기](#ProvideDeviceDiscovery)
3. [Clova Home extension 요청 처리하기](#HandleClovaHomeExtensionRequest)
4. [Clova Home extension 응답 반환하기](#ReturnClovaHomeExtensionResponse)

{% include "/CEK/Guides/BuildClovaHomeExtension/Preparation.md" %}

{% include "/CEK/Guides/BuildClovaHomeExtension/Provide_Device_Discovery.md" %}

{% include "/CEK/Guides/BuildClovaHomeExtension/Handle_Clova_Home_Extension_Request.md" %}

{% include "/CEK/Guides/BuildClovaHomeExtension/Return_Clova_Home_Extension_Response.md" %}
