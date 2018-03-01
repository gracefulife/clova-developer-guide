샘플 주사위 extension이 도움말 요청을 하는 built-in intent를 잘 처리하는지 테스트해야 합니다.

[첫 번째 튜토리얼](/CEK/Tutorials/Build_Simple_Extension.md)에서처럼 두 가지 테스트 방법이 있습니다. 하나는 Clova developer console에서 interaction 모델 동작을 확인하는 것이고, 다른 하나는 테스터 ID를 등록하여 Clova 앱에서 실제 동작을 확인하는 것입니다.
이 튜토리얼에서는 interaction 모델 동작만 확인합니다.

<div class="note">
  <p><strong>Note!</strong></p>
  <p>Built-in intent는 interaction 모델에 명시적으로 등록하지 않아도 기본적으로 동작합니다.
  추후 각 extension에서 built-in intent를 선택하여 등록할 수 있도록 할 예정입니다.</p>
</div>

다음 순서대로 샘플 주사위 extension의 도움말 요청이 잘 동작하는지 확인합니다.
1. <a href="{{ book.DeveloperConsoleURL }}/cek/#/list" target="_blank">Clova developer console</a>에 접속합니다.
2. 샘플 주사위의 **{{ book.DevConsole.cek_interaction_model }}** 항목 내 **{{ book.DevConsole.cek_edit}}** 버튼을 누릅니다.
3. 왼쪽의 메뉴 목록에서 **{{ book.DevConsole.cek_test }}** 메뉴를 누릅니다.
4. **{{ book.DevConsole.cek_builder_test_expression_title }}**에 도움말을 요청하는 문장을 입력합니다. 예를 들어, "사용법 알려줘"라고 입력합니다.
5. 엔터키 또는 **{{ book.DevConsole.cek_builder_test_request_test }}** 버튼을 누릅니다.
6. **{{ book.DevConsole.cek_builder_test_result_title }}**의 **{{ book.DevConsole.cek_builder_test_intent_result }}** 항목에 'Clova.GuideIntent'라고 나타나는지 확인합니다.

	<img src="/CEK/Resources/Images/CEK_Tutorial_Builtin_Intent_Test.png" style="max-width:800px;"/>

  <div class="note">
	<p><strong>Note!</strong></p>
	<p>외부에서 접근할 수 있는 extension 서버 URL을 등록하지 않았다면, <strong>{{ book.DevConsole.cek_builder_test_service_response }}</strong>은 "Response가 없습니다. (undefined)"라고 나타납니다.</p>
	</div>
