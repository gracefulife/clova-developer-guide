# Extension 배포하기
[Custom extension](/CEK/Guides/Build_Custom_Extension.md) 또는 Clova Home extension을 [Clova developer console에 등록](/DevConsole/Guides/CEK/Register_Extension.md)했다면 등록한 extension을 Clova 서비스에 배포할 수 있습니다. 배포하면 일반 사용자들이 **확장 기능 관리**라는 메뉴에서 배포된 extension을 사용할 수 있게 됩니다.

Extension을 배포할 때 일반적으로 다음 항목을 순차적으로 수행해야 합니다.

* (Custom extension 전용) [Interaction 모델 빌드하기](#BuildInteractionModel)
* (Custom extension 전용) [Interaction 모델 테스트하기](#TestInteractionModel)
* [배포 정보 입력](#InputDeploymentInfo)
* [개인 정보 및 규정 준수 정보 입력](#InputComplianceInfo)
* [Extension 승인 요청하기](#RequestExtensionSubmission)

## Interaction 모델 빌드하기 {#BuildInteractionModel}

Custom extension을 배포하는 경우 [interaction 모델이 정의](/DevConsole/Guides/CEK/Define_Interaction_Model.md)되어 있어야 합니다. 정의된 interaction 모델은 빌드 과정을 거쳐야 새로 작성했거나 또는 업데이트한 내용을 [테스트](#TestInteractionModel)하거나 사용할 수 있습니다. 다음과 같이 정의된 interaction 모델을 빌드할 수 있습니다.

<ol>
  <li>등록한 extension 목록에서 interaction 모델을 빌드하려는 extension 항목의 <strong>수정하기</strong> 메뉴를 클릭합니다.</li>
  <img src="/DevConsole/Resources/Images/DevConsole-Extension_list_after_Creation.png" />
  <li>위쪽 탭 메뉴 중 <strong>인터렉션 모델</strong> 메뉴를 선택합니다.</li>
  <img src="/DevConsole/Resources/Images/DevConsole-Build_Interaction_Model_1.png" />
  <li><strong>인터렉션 모델: 대시보드</strong> 화면에서 오른쪽에 있는 <strong>빌드</strong> 버튼을 클릭하면 인터렉션 모델 빌드를 시작합니다. 인터렉션 모델의 크기 등에 따라 3~5분 정도 소요될 수 있습니다.</li>
  <img src="/DevConsole/Resources/Images/DevConsole-Build_Interaction_Model_2.png" />
</ol>

참고로 빌드 중에 **인터렉션 모델: 대시보드** 내에서 다른 메뉴로 이동하더라도 빌드가 취소되지 않습니다. 빌드를 시작한 이후에 얼마든지 메뉴 이동 및 내용 편집이 가능합니다.

## Interaction 모델 테스트하기 {#TestInteractionModel}

[Interaction 모델 빌드](#BuildInteractionModel)가 완료되면, interaction 모델을 테스트할 수 있습니다. 다음과 같이 발화문을 테스트해볼 수 있습니다.

<ol>
  <li><strong>인터랙션 모델 빌더 메뉴</strong> 아래에서 <strong>테스트</strong> 메뉴를 클릭합니다. 메뉴를 클릭하면 <strong>인터렉션 모델: 테스트</strong> 화면이 표시됩니다.</li>
  <img src="/DevConsole/Resources/Images/DevConsole-Test_Menu.png" />
  <li><strong>사용자 표현 문장입력</strong> 필드에 테스트할 발화문을 입력하고 <strong>테스트 요청</strong> 버튼을 클릭합니다.</li>
  <img src="/DevConsole/Resources/Images/DevConsole-Test_Utterance_Example.png" />
</ol>

테스트를 완료하면 다음과 같은 결과를 확인할 수 있습니다. 아래 결과를 토대로 다음과 같은 항목을 확인해야 합니다.

* **서비스 응답** 항목을 보고 [등록한 custom extension](/DevConsole/Guides/CEK/Register_Extension.md)이 제대로 응답하는지 확인합니다.
* **분석된 Intent** 항목과 **분석된 Intent Slot** 항목을 보고 의도한대로 intent와 slot이 인식되는지 확인합니다.
* **서비스 요청 JSON** 항목을 보고 CEK가 custom extension으로 보내는 [요청 메시지](/CEK/References/CEK_API.md#CustomExtRequestMessage)에 이상이 없는지 확인합니다. 뿐만 아니라 해당 JSON의 내용을 수정한 후 **테스트 재요청** 버튼을 클릭하면 테스트를 다시 수행할 수 있습니다.
* **서비스 응답 JSON** 항목을 보고 등록한 custom extension이 의도한대로 [응답 메시지](/CEK/References/CEK_API.md#CustomExtResponseMessage)를 보내는지 확인합니다.

![](/DevConsole/Resources/Images/DevConsole-Test_Result.png)

## 배포 정보 입력 {#InputDeploymentInfo}

Clova developer console에서 [extension을 등록](/DevConsole/Guides/CEK/Register_Extension.md)과 [Interaction 모델을 정의](/DevConsole/Guides/CEK/Define_Interaction_Model.md)한 후 배포 정보를 입력할 수 있습니다. Extension 등록 메뉴에서 **배포 정보**을 선택합니다.

![](/DevConsole/Resources/Images/DevConsole-Deployment_Info_Menu.png)

다음와 같이 배포 정보를 입력합니다.

![](/DevConsole/Resources/Images/DevConsole-Input_Deployment_Info.png)

* Extension을 사용자에게 설명하기 위한 정보로서 Clova 앱의 **확장 기능 관리** 메뉴에서 사용자에게 제공됩니다. 다음과 같은 정보들이 입력됩니다.
  - **카테고리**: Extension의 종류로서 사용자가 extension 종류별로 목록을 확인하거나 검색할 때 이용됩니다.
  - **익스텐션 요약 설명**: Extension 상세 페이지에 표시할 요약 설명입니다.
  - **익스텐션 상세 설명**: Extension 상세 페이지에서 사용자가 좀 더 자세한 설명을 원할 경우 제공할 상세 설명입니다.
  - **대표 표현 문장**: 사용자가 extension을 어떻게 사용할 수 있는지 보여주는 예시문입니다. 첫 번째 예시문은 extension 목록을 보여줄 때 표시됩니다.
  - **검색 키워드**: 사용자가 extension을 검색할 때 특정 키워드가 포함되면 검색 결과에 표시되도록 해주는 검색어입니다.
  - **작은 아이콘**: Extension 아이콘을 나타낼 이미지 파일입니다.(108px X 108px)
  - **큰 아이콘**: Extension 아이콘의 큰 이미지로서 추후 사용 예정입니다.(512px X 512px)
* 테스트용 지시어: [Extension 승인](#RequestExtensionSubmission) 프로세스에서 승인 담당자가 extension을 검증하는데 필요한 참고 정보로서 일반 사용자에게는 노출되지 않습니다. Extension이 제공하는 기능(intent) 목록, 테스트 계정([계정 연결](/CEK/Guides/LinkUserAccount.md)이 필요하다면) 그리고 열거한 기능을 테스트할 수 있는 발화문 예시와 해당 동작이 제대로 동작했는지 판단할 수 있는 [세부 목표](/Design/DesignGuidelineForExtension.md#SettingGoal) 등을 입력합니다.
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

* 구매 절차 여부: Extension을 사용할 때 사용자가 결제하거나 지불해야 하는 부분이 있을 경우 **네**를 선택합니다.
* 개인 정보 수집 여부: Extension이 사용자의 개인 정보를 수집할 경우 **네**를 선택합니다.
* 미성년자 사용 여부: 미성년자가 extension을 사용해도 되면 **네**를 선택합니다.
* 개인 정보 정책 URL: Extension이 개인 정보를 수집하는 경우 이와 관련된 정책 정보 페이지를 입력합니다. 이는 extension 설명 페이지의 맨 아래에 표시됩니다.
* 면책 조항: Extension과 관련한 면책 조항을 보여주는 페이지를 입력합니다. 이는 개인 정보 정책 URL과 같이 extension 설명 페이지의 맨 아래에 표시됩니다.

**개인 정보 관리 URL**과 **면책 조항**에 입력된 내용은 extension 상세 설명 페이지에서 다음과 같이 표시됩니다.

![](/DevConsole/Resources/Images/DevConsole-Store_UI_Example-Extension_Policy.png)

## Extension 승인 요청하기 {#RequestExtensionSubmission}

Extension의 [배포 정보](#InputDeploymentInfo)와 [개인 정보 관리 및 규정 준수 정보](#InputComplianceInfo)까지 입력이 완료되었다면 최종적으로 등록한 extension에 대해 심사를 요청할 수 있습니다. Clova의 운영자는 등록한 extension의 정보와 실제 실행 여부 및 적합성 등을 검수하게 됩니다.

* Extension이 정상 동작하고 검수 시 특별한 문제 사항이 없다면 extension은 심사를 통과하게 될 것이며, 심사 통과 후 즉시 혹은 원하는 시간에 배포할 수 있게 됩니다.
* 만약, 심사 과정에서 실행 오류가 있거나 사용자 시나리오 상의 심각한 문제 발견되면 운영자에 의해 재심사 받도록 extension 수정을 요청할 수 있습니다.

![](/DevConsole/Resources/Images/DevConsole-Extension_Submission_Process.png)

심사 과정은 개별 심사로 진행되며 심사는 심사를 위한 별도 환경에서 진행됩니다. 만약, [사용자 계정 연결](/CEK/Guides/LinkUserAccount.md)이 필요한 서비스인 경우에는 [배포 정보를 입력](#InputDeploymentInfo)할 때 테스트를 위한 계정 정보를 **테스트용 지시어** 항목에 입력해야 합니다.

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
