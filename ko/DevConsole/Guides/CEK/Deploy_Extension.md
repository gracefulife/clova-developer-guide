# Extension 배포하기
[Custom extension](/CEK/Guides/Build_Custom_Extension.md) 또는 Clova Home extension을 [Clova developer console에 등록](/DevConsole/Guides/CEK/Register_Extension.md)했다면 등록한 extension을 Clova 서비스에 배포할 수 있습니다. 배포하면 일반 사용자들이 **확장 기능 관리**라는 메뉴에서 배포된 extension을 사용할 수 있게 됩니다.

Extension을 배포할 때 일반적으로 다음 항목을 수행해야 합니다.

* [배포 정보 입력](#InputDeploymentInfo)
* [개인 정보 및 규정 준수 정보 입력](#InputComplianceInfo)
* [심사 신청하기](#RequestExtensionSubmission)

## 배포 정보 입력 {#InputDeploymentInfo}

Clova developer console에서 [extension을 등록](/DevConsole/Guides/CEK/Register_Extension.md)과 [Interaction 모델을 등록](/DevConsole/Guides/CEK/Register_Interaction_Model.md)한 후 배포 정보를 입력할 수 있습니다. Extension 등록 메뉴에서 **배포 정보**을 선택합니다.

![](/DevConsole/Resources/Images/DevConsole-Deployment_Info_Menu.png)

다음와 같이 배포 정보를 입력합니다.

![](/DevConsole/Resources/Images/DevConsole-Input_Deployment_Info.png)

* Extension을 사용자에게 설명하기 위한 정보로서 Clova 앱의 **확장 기능 관리** 메뉴에서 사용자에게 제공됩니다. 다음과 같은 정보들이 입력됩니다.
  - **분류**: Extension의 종류로서 사용자가 extension 종류별로 목록을 확인하거나 검색할 때 이용됩니다.
  - **Extension 요약 설명**: Extension 상세 페이지에 표시할 요약 설명입니다.
  - **Extension 상세 설명**: Extension 상세 페이지에서 사용자가 좀 더 자세한 설명을 원할 경우 제공할 상세 설명입니다.
  - **대표 발화 예시**: 사용자가 extension을 어떻게 사용할 수 있는지 보여주는 예시문입니다. 첫 번째 예시문은 extension 목록을 보여줄 때 표시됩니다.
  - **검색 키워드**: 사용자가 extension을 검색할 때 특정 키워드가 포함되면 검색 결과에 표시되도록 해주는 검색어입니다.
  - **작은 아이콘**: Extension 아이콘을 나타낼 이미지 파일입니다.(108px X 108px)
  - **큰 아이콘**: Extension 아이콘의 큰 이미지로서 추후 사용 예정입니다.(512px X 512px)
* **Extension 심사용 설명**: [Extension 승인](#RequestExtensionSubmission) 프로세스에서 승인 담당자가 extension을 검증하는데 필요한 참고 정보로서 일반 사용자에게는 노출되지 않습니다. Extension이 제공하는 기능(intent) 목록, 테스트 계정([계정 연결](/CEK/Guides/LinkUserAccount.md)이 필요하다면) 그리고 열거한 기능을 테스트할 수 있는 발화문 예시와 해당 동작이 제대로 동작했는지 판단할 수 있는 [세부 목표](/Design/DesignGuidelineForExtension.md#SettingGoal) 등을 입력합니다.
* 서비스 국가 및 지역: 해당 extension이 서비스를 제공할 국가나 지역으로 현재 선택할 수 있는 지역이 없고 한국에만 extension을 배포할 수 있습니다.

이렇게 입력된 정보는 Clova 앱 **확장 기능 관리** 메뉴에서 다음과 같이 표시됩니다.

| Extension 목록 표시 | Extension 상세 표시 |
|-------------------|-------------------|
| ![Extension List](/DevConsole/Resources/Images/DevConsole-Store_UI_Example_Extension_List.png) | ![Extension Details](/DevConsole/Resources/Images/DevConsole-Store_UI_Example-Extension_Details.png) |

<div class="note">
  <p><strong>Note!</strong></p>
  <p>Extension 상세 설명 페이지에 표시되는 일부 정보는 <a href="/DevConsole/Guides/CEK/Register_Extension.html#InputExtensionInfo">Extension 기본 정보를 등록</a>할 때 입력된 정보를 활용합니다.</p>
</div>

## 개인 정보 관리 및 규정 준수 정보 입력 {#InputComplianceInfo}

Extension 배포에 필요한 정보를 입력하는 마지막 단계로서 개인 정보 관리 및 규정 준수에 관련된 내용을 입력해야 합니다. Extension 등록 메뉴에서 **개인 정보 및 규정 준수**를 선택합니다.

![](/DevConsole/Resources/Images/DevConsole-Policy_Menu.png)

다음과 같이 정보를 입력합니다.

![](/DevConsole/Resources/Images/DevConsole-Input_Policy.png)

* **구매/지불 기능 존재 여부**: Extension을 사용할 때 사용자가 결제하거나 지불해야 하는 부분이 있을 경우 **네**를 선택합니다.
* **개인 정보 수집 여부**: Extension이 사용자의 개인 정보를 수집할 경우 **네**를 선택합니다.
* **미성년자 사용 가능 여부**: 미성년자가 extension을 사용해도 되면 **네**를 선택합니다.
* **개인 정보 정책 제공 URL**: Extension이 개인 정보를 수집하는 경우 이와 관련된 정책 정보 페이지를 입력합니다. 이는 extension 설명 페이지의 맨 아래에 표시됩니다.
* **면책 조항 제공 URL**: Extension과 관련한 면책 조항을 보여주는 페이지를 입력합니다. 이는 개인 정보 정책 URL과 같이 extension 설명 페이지의 맨 아래에 표시됩니다.

**개인 정보 정책 제공 URL**과 **면책 조항 제공 URL**에 입력된 내용은 extension 상세 설명 페이지에서 다음과 같이 표시됩니다.

![](/DevConsole/Resources/Images/DevConsole-Store_UI_Example-Extension_Policy.png)

## 심사 신청하기 {#RequestExtensionSubmission}

Extension의 [배포 정보](#InputDeploymentInfo)와 [개인 정보 관리 및 규정 준수 정보](#InputComplianceInfo)까지 입력이 완료되었다면 최종적으로 등록한 extension에 대해 extension 심사를 신청할 수 있습니다. Clova의 운영자는 등록한 extension의 정보와 실제 실행 여부 및 적합성 등을 심사하게 됩니다.

* Extension이 정상 동작하고 검수 시 특별한 문제 사항이 없다면 extension은 심사를 통과하게 될 것이며, 심사를 통과하면 즉시 혹은 원하는 시간에 extension을 배포할 수 있게 됩니다.
* 만약, 심사 과정에서 실행 오류가 있거나 사용자 시나리오 상의 심각한 문제 발견되면 운영자에 의해 배포 요청이 거절되며 신사 신청하기 전 단계로 돌아가게 됩니다.

![](/DevConsole/Resources/Images/DevConsole-Extension_Submission_Process.png)

등록한 extension 목록에서 **심사 신청** 메뉴를 클릭하여 extension 심사를 신청할 수 있습니다.

![](/DevConsole/Resources/Images/DevConsole-Submit_Extension_1.png)

또는 [개인 정보 관리 및 규정 준수 정보](#InputComplianceInfo)를 입력하는 화면 마지막에 있는 **심사 신청** 버튼을 클릭해도 됩니다.

![](/DevConsole/Resources/Images/DevConsole-Submit_Extension_2.png)

<div class="note">
  <p><strong>Note!</strong></p>
  <p>심사 중에는 extension의 정보와 interaction 모델을 수정할 수 없습니다.</p>
</div>

심사는 개별 심사로 진행되며 심사를 위한 별도 환경에서 진행됩니다. 만약, [사용자 계정 연결](/CEK/Guides/LinkUserAccount.md)이 필요한 서비스인 경우에는 [배포 정보를 입력](#InputDeploymentInfo)할 때 테스트를 위한 계정 정보를 **테스트용 지시어** 항목에 입력해야 합니다.

Extension을 심사할 때 살펴보는 기본 평가 항목은 다음과 같습니다.

1. Extension 빌드 검증
  * Extension 서비스에 적합한 용어를 사용하고 있는지 확인합니다.
  * Intent, slot 등 interaction 모델을 검증합니다.
  * Extension [세부 목표](/Design/DesignGuidelineForExtension.md#SettingGoal)에 부합되는 서비스를 제공하고 있는지 확인합니다.
2. [사용 시나리오](/Design/DesignGuidelineForExtension.md#MakeUseCaseScenarioScript) 검증
  * 대화 문맥 상 어색한 부분이 있는지 확인합니다.
  * 시나리오 상 사용되는 발화 데이터에 금칙어, 민감어 등이 있는지 확인합니다.
  * Extension이 [사용자 계정을 연결](/CEK/Guides/LinkUserAccount.md)하는 경우 서비스에 특화된 부분을 더 검토할 수 있습니다.
3. 배포 정보 검증
  * Extension의 설명, 카테고리, 검색 키워드와 같이 입력된 배포 정보가 extension에 맞게 입력되었는지 확인합니다.
  * Extension이 개인 정보 관리 규정 등 입력된 정책에 맞게 동작하는지 확인합니다.

심사 중에 **심사 취소** 메뉴를 클릭하면 언제든지 심사 신청을 취소할 수 있습니다. 심사 신청을 취소하면 이전 상태로 돌아갑니다.

![](/DevConsole/Resources/Images/DevConsole-Cancel_Submission.png)

심사에 통과하지 못하면 extension의 **상태**가 **확인요망**으로 변경됩니다. 이 상태는 **개발 중**인 상태와 같은 상태이며 다시 심사를 신청할 수 있습니다.

![](/DevConsole/Resources/Images/DevConsole-Extension_Submission_Rejected.png)

이때, **메시지**의 **확인** 메뉴를 클릭하면 심사에 대한 피드백을 확인할 수 있습니다.

![](/DevConsole/Resources/Images/DevConsole-Show_Submission_Feedback.png)
