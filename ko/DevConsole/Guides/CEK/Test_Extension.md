# Extension 배포하기
[Custom extension](/CEK/Guides/Build_Custom_Extension.md) 또는 Clova Home extension을 [Clova developer console에 등록](/DevConsole/Guides/CEK/Register_Extension.md)했다면 등록한 extension을 Clova 서비스에 배포할 수 있습니다. 배포하면 일반 사용자들이 **확장 기능 관리**라는 메뉴에서 배포된 extension을 사용할 수 있게 됩니다.

Extension을 배포할 때 일반적으로 다음 항목을 순차적으로 수행해야 합니다.

* (Custom extension 전용) [Interaction 모델 빌드하기](#BuildInteractionModel)
* (Custom extension 전용) [Interaction 모델 테스트하기](#TestInteractionModel)
* [테스트 모드 사용하기](#UsingTestMode)

## Interaction 모델 빌드하기 {#BuildInteractionModel}

Custom extension을 배포하는 경우 [interaction 모델이 등록](/DevConsole/Guides/CEK/Register_Interaction_Model.md)되어 있어야 합니다. 정의된 interaction 모델은 빌드 과정을 거쳐야 새로 작성했거나 또는 업데이트한 내용을 [테스트](#TestInteractionModel)하거나 사용할 수 있습니다. 다음과 같이 정의된 interaction 모델을 빌드할 수 있습니다.

<ol>
  <li>등록한 extension 목록에서 interaction 모델을 빌드하려는 extension 항목의 <strong>수정</strong> 메뉴를 클릭합니다.</li>
  <img src="/DevConsole/Resources/Images/DevConsole-Interaction_Model_Menu.png" />
  <li><strong>Interaction 모델: 대시보드</strong> 화면에서 왼쪽 상단에 있는 <strong>빌드</strong> 버튼을 클릭하면 interaction 모델을 빌드합니다. Interaction 모델의 크기 등에 따라 3~5분 정도 소요될 수 있습니다.</li>
  <img src="/DevConsole/Resources/Images/DevConsole-Build_Interaction_Model.png" />
</ol>

<div class="note">
  <p><strong>Note!</strong></p>
  <p>빌드 중에 <strong>Interaction 모델: 대시보드</strong> 내에서 다른 메뉴로 이동하더라도 빌드가 취소되지 않습니다. 빌드를 시작한 이후에 얼마든지 메뉴 이동 및 내용 편집이 가능합니다.</p>
</div>



## Interaction 모델 테스트하기 {#TestInteractionModel}

[Interaction 모델 빌드](#BuildInteractionModel)가 완료되면, interaction 모델을 테스트할 수 있습니다. 다음과 같이 발화문을 테스트해볼 수 있습니다.

<ol>
  <li>왼쪽 사이드 메뉴바 아래 <strong>테스트</strong> 메뉴를 클릭합니다. 메뉴를 클릭하면 <strong>Interaction 모델: 테스트</strong> 화면이 표시됩니다.</li>
  <img src="/DevConsole/Resources/Images/DevConsole-Test_Menu.png" />
  <li><strong>사용자 표현 문장입력</strong> 필드에 테스트할 발화문을 입력하고 <strong>테스트 요청</strong> 버튼을 클릭합니다.</li>
  <img src="/DevConsole/Resources/Images/DevConsole-Test_Utterance_Example.png" />
</ol>

테스트를 완료하면 다음과 같은 결과를 확인할 수 있습니다. 아래 결과를 토대로 다음과 같은 항목을 확인해야 합니다.

* **서비스 응답** 항목을 보고 [등록한 custom extension](/DevConsole/Guides/CEK/Register_Extension.md)이 제대로 응답하는지 확인합니다.
* **분석된 intent** 항목과 **분석된 slot** 항목을 보고 의도한대로 intent와 slot이 인식되는지 확인합니다.
* **서비스 요청 JSON** 항목을 보고 CEK가 custom extension으로 보내는 [요청 메시지](/CEK/References/CEK_API.md#CustomExtRequestMessage)에 이상이 없는지 확인합니다. 뿐만 아니라 해당 JSON의 내용을 수정한 후 **테스트 재요청** 버튼을 클릭하면 테스트를 다시 수행할 수 있습니다.
* **서비스 응답 JSON** 항목을 보고 등록한 custom extension이 의도한대로 [응답 메시지](/CEK/References/CEK_API.md#CustomExtResponseMessage)를 보내는지 확인합니다.

![](/DevConsole/Resources/Images/DevConsole-Test_Result.png)

## 테스트 모드 사용하기 {#UsingTestMode}

Extension의 실제 테스트를 위해 **테스트 모드**를 제공하고 있습니다. Extension에서 **테스트 모드**를 활성화하면 별도의 설정 없이 개발자 본인의 <strong>{{ book.OrientedService }} 계정이 인증된 Clova 앱</strong>에서 등록한 extension을 바로 테스트해볼 수 있도록 지원할 예정입니다. **테스트 모드**를 활성화하려면 다음과 같이 등록한 extension 목록에서 테스트 모드를 활성화하려는 extension 항목의 <img class="inlineImage" src="/DevConsole/Resources/Images/DevConsole-Check_Button.png" /> 버튼을 클릭합니다.

![](/DevConsole/Resources/Images/DevConsole-Enable_Extension_Test_Mode.png)

<div class="note">
  <p><strong>Note!</strong></p>
  <p>테스트 모드가 활성화한 후 <img class="inlineImage" src="/DevConsole/Resources/Images/DevConsole-Check_Button.png" /> 버튼을 한번 더 클릭하면 언제든지 테스트 모드 사용을 중지할 수 있습니다.</p>
</div>
