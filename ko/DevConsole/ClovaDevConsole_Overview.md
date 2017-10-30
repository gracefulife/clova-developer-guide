# Clova developer console 개요

Clova 플랫폼과 연동하는 제품이나 서비스를 개발할 때 필요한 정보나 기능을 제공하는 웹 도구입니다. 클라이언트 개발자는 Clova developer console를 통해 개발하려는 클라이언트(기기 또는 앱)의 정보를 입력하고 해당 클라이언트가 [CIC에 접속](/CIC/CIC_Overview.md)할 수 있도록 보안 정보를 설정합니다. Extension 개발자는 CEK와 extension이 메시지를 주고 받을 수 있도록 [extension 정보를 입력](/DevConsole/Guides/CEK/Register_Extension.md)하고, [Interaction 모델을 등록](/DevConsole/Guides/CEK/Define_Interaction_Model.md)하게 됩니다. 뿐만 아니라 extension 개발자는 [extension 배포](/DevConsole/Guides/CEK/Deploy_Extension.md)를 위해 extension을 테스트하고 extension 심사도 신청해야 합니다.

클라이언트를 개발하거나 extension을 개발할 때 Clova developer console는 다음과 같은 구조로 사용됩니다.

![](/DevConsole/Resources/Images/DevConsole-Concept_Diagram.png)

Clova developer console는 다음과 같은 메뉴를 제공합니다.

* CIC 메뉴(추후 제공 예정)
  * 클라이언트 기기 및 앱 등록 메뉴
  * 클라이언트 인증 정보 관련 메뉴
  * 클라이언트 제품 사양 등록 메뉴
* [CEK 메뉴](/DevConsole/Guides/CEK/Using_CEK_Menu.md)
  * [Clova extension 등록](/DevConsole/Guides/CEK/Register_Extension.md) 메뉴
  * [Interaction 모델 등록](/DevConsole/Guides/CEK/Define_Interaction_Model.md) 메뉴
  * [Extension 테스트 및 배포](/DevConsole/Guides/CEK/Deploy_Extension.md) 메뉴
* Clova 서비스 관련 통계 자료 제공(추후 제공 예정)
