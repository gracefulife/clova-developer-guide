You must test whether the Sample Dice extension handles the help request built-in intent from the extension via an appropriate method.

There are two test methods shown in the [first tutorial](/CEK/Tutorials/Build_Simple_Extension.md). One method is checking the operation of the interaction model on the Clova developer console and the other is checking the actual operation of the Clova app by registering a tester ID.
This tutorial checks the operation of the interaction model only.

<div class="note">
  <p><strong>Note!</strong></p>
  <p>Built-in intents work by default even if not specified in the interaction model.
  We are planning to allow selective registration of built-in intents for extensions in the future.</p>
</div>

Follow the steps below to check whether the help request of the Sample Dice extension is operating properly:
1. Access the <a href="https://developers.naver.com/console/clova/cek/#/list" target="_blank">Clova developer console</a>.
2. Click the **{{ book.DevConsole.cek_edit}}** button on the **{{ book.DevConsole.cek_interaction_model }}** item of the Sample Dice extension.
3. Click the **{{ book.DevConsole.cek_test }}** menu on the left menu bar.
4. Enter the sentence to request help in **{{ book.DevConsole.cek_builder_test_expression_title }}**. For example, enter "Give me the instructions."
5. Press enter or click the **{{ book.DevConsole.cek_builder_test_request_test }}** button.
6. Check whether "Clova.GuideIntent" appears in the **{{ book.DevConsole.cek_builder_test_intent_result }}** field under the **{{ book.DevConsole.cek_builder_test_result_title }}**.

	<img src="/CEK/Resources/Images/CEK_Tutorial_Builtin_Intent_Test.png" style="max-width:800px;"/>

  <div class="note">
	<p><strong>Note!</strong></p>
  <p>If the externally accessible extension server URL is not registered, an "Undefined response" message is displayed on <strong>{{ book.DevConsole.cek_builder_test_service_response }}</strong>. </p>
	</div>
