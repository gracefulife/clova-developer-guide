<a href="https://developers.naver.com/console/clova/cek/#/list" target="_blank">Clova developer console</a>에서 interaction 모델을 등록합니다.

이 튜토리얼에서 샘플 주사위는 사용자가 개수를 지정하지 않고 주사위를 던져달라는 요청을 하면 기본적으로 주사위 1개를 던집니다. 여기서는 이렇게 주사위 1개를 던지는 명령을 처리하는 단순한 interaction 모델을 사용하기로 합시다. 주사위 개수를 수집하지 않으므로 slot이 없는 intent 하나를 등록하면 됩니다.

### 새로운 custom intent 만들기
여기서는 주사위를 던져달라는 요청에 주사위 1개를 던지도록 간단한 intent를 생성합니다.

1. 샘플 주사위의 **{{ book.DevConsole.cek_interaction_model }}** 항목 내 **{{ book.DevConsole.cek_edit }}** 버튼을 누릅니다.
2. **{{ book.DevConsole.cek_builder_list_title_intent }}** 오른쪽에 있는 <img class="inlineImage" src="/CEK/Resources/Images/DevConsole_Plus_Button.png" /> 버튼을 누릅니다.
3. **{{ book.DevConsole.cek_builder_new_intent }}** 아래 입력창에 'ThrowDiceIntent'라는 이름을 입력합니다.
4. 엔터키 또는 입력창 오른쪽의 **{{ book.DevConsole.cek_builder_new_intent_create }}** 버튼을 누릅니다.

	<img src="/CEK/Resources/Images/CEK_Tutorial_NewIntent.png" style=" max-width:800px;" />

	<div class="danger">
	  <p><strong>Caution!</strong></p>
		<p>Intent 이름의 대소문자에 유의해야 합니다.</p>
	</div>

### 발화 예시 목록에 문장 입력하기
여기서는 사용자가 어떤 말을 할 때 위에 입력한 intent로 처리할지 지정합니다. 발화 예시는 많을수록 좋지만, 이 튜토리얼에서는 하나만 입력합니다.
1. **{{ book.DevConsole.cek_builder_intent_expression_title }}**에서 "주사위 던져줘"라고 입력합니다.
2. 엔터키 또는 <img class="inlineImage" src="/CEK/Resources/Images/DevConsole_Plus_Button.png" /> 버튼을 누릅니다.
3. 모든 발화 예시를 입력하면 **{{ book.DevConsole.cek_save }}** 버튼을 누릅니다.

	<img src="/CEK/Resources/Images/CEK_Tutorial_SpeechExample.png" style=" max-width:800px; margin-top:10px; margin-bottom:10px;" />

### 빌드 및 테스트하기
Interaction 모델이 입력한대로 동작하는지 확인하기 위해 interaction 모델을 빌드하여 테스트 합니다.

1. **Custom Extension** 화면 좌측 상단의 **{{ book.DevConsole.BuildButton }}** 버튼을 누릅니다.

	<div class="note">
	  <p><strong>Note!</strong></p>
		<p>빌드는 3~5분 정도 소요됩니다. 빌드가 시작되면 버튼이 <strong>{{ book.DevConsole.IsBuilding }}</strong>으로 바뀌며, 빌드가 완료된 후 다시 <strong>{{ book.DevConsole.BuildButton }}</strong>로 돌아옵니다.</p>
	</div>

2. 빌드가 완료되면 **{{ book.DevConsole.BuildButton }}** 버튼 아래의 **{{ book.DevConsole.cek_test }}** 메뉴를 누릅니다.

3. **{{ book.DevConsole.cek_builder_test_expression_title }}**에 테스트하고자 하는 문장을 입력합니다. 예를 들어, "주사위 던져줄래"라고 입력합니다.
4. 엔터키 또는 **{{ book.DevConsole.cek_builder_test_request_test }}** 버튼을 누릅니다.
5. **{{ book.DevConsole.cek_builder_test_result_title }}**의 **{{ book.DevConsole.cek_builder_test_intent_result }}** 항목에 'ThrowDiceIntent'라고 나타나는지 확인합니다.

	<img src="/CEK/Resources/Images/CEK_Tutorial_Test.png" style="max-width:800px;"/>

	<div class="note">
	<p><strong>Note!</strong></p>
	<p>2단계에서 외부에서 접근할 수 있는 extension 서버 URL을 등록하지 않았다면, <strong>{{ book.DevConsole.cek_builder_test_service_response }}</strong>은 "{{ book.DevConsole.cek_builder_test_no_response }}"라고 나타납니다.</p>
	</div>
