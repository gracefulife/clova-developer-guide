샘플 주사위 extension이 등록한 slot을 잘 처리하는지 테스트해야 합니다.

[첫 번째 튜토리얼](/CEK/Tutorials/Build_Simple_Extension.md)에서처럼 두 가지 테스트 방법이 있습니다. 하나는 Clova developer console에서 interaction 모델 동작을 확인하는 것이고, 다른 하나는 테스터 아이디를 등록하여 Clova 앱에서 실제 동작을 확인하는 것입니다.
이 튜토리얼에서는 interaction 모델 동작만 확인합니다.

<a href="https://developers.naver.com/console/clova/cek/#/list" target="_blank">Clova developer console</a>에 접속하여 다음과 같이 샘플 주사위 extension이 주사위 개수를 잘 인식하는지 확인합니다.
1. 샘플 주사위의 **{{ book.DevConsole.cek_interaction_model }}** 항목 내 **{{ book.DevConsole.cek_edit}}** 버튼을 누릅니다.
2. 화면 좌측 상단의 **{{ book.DevConsole.BuildButton }}** 버튼을 눌러 interaction 모델을 빌드합니다.
3. 빌드가 끝난 후, 왼쪽의 메뉴 목록에서 **{{ book.DevConsole.cek_test }}** 메뉴를 선택합니다.
4. **{{ book.DevConsole.cek_builder_test_expression_title }}**에 주사위를 여러 개 던져달라는 문장을 입력합니다. 예를 들어, "주사위 두 개 던져볼래"라고 입력합니다.
5. 엔터키 또는 **{{ book.DevConsole.cek_builder_test_request_test }}** 버튼을 누릅니다.
6. **{{ book.DevConsole.cek_builder_test_result_title }}**의 **{{ book.DevConsole.cek_builder_test_intent_result }}** 항목에 `ThrowDiceIntent`, **{{ book.DevConsole.cek_builder_test_slot_result }}** 항목에 `diceCount`가 나타나고, **{{ book.DevConsole.cek_builder_test_slot_data}}**에 입력한 주사위 개수가 나타나는지 확인합니다.

	<img src="/CEK/Resources/Images/CEK_Tutorial_Builtin_Type_Slot_Test.png" style="max-width:800px;"/>

  <div class="note">
	<p><strong>Note!</strong></p>
	<p>외부에서 접근할 수 있는 extension 서버 URL을 등록하지 않았다면, <strong>{{ book.DevConsole.cek_builder_test_service_response }}</strong>은 "{{ book.DevConsole.cek_builder_test_no_response }}"라고 나타납니다.</p>
	</div>

7. "주사위 열 개 굴려", "네 개 주사위 던져" 등의 문장으로 4-6을 반복합니다.

인식이 잘 되지 않으면 좀 더 다양한 발화 예시를 추가하여 인식 확률을 높일 수 있습니다.
