You can register an interaction model on the <a href="https://developers.naver.com/console/clova/cek/#/list" target="_blank">Clova developer console</a>.

The information stored in the interaction model are [intent](/Design/Design_Guideline_For_Extension.md#Intent) and [slot](/Design/Design_Guideline_For_Extension.md#Slot). An intent is a command sent to the extension server after analyzing the input sentence and a slot is the information required for the intent.

The Sample Dice extension rolls one die by default if the user requests to roll dice without stating the number of dice. For this tutorial, we will create a simple interaction model to handle the command for throwing a dice. Since the information on the number of dice is not collected, we can register one intent without a slot.

### Creating a new custom intent
Follow the steps below to make a simple intent to roll one die upon user request.

1. Click the **{{ book.DevConsole.cek_edit }}** button on the **{{ book.DevConsole.cek_interaction_model }}** item of the Sample Dice extension.
2. Click the <img class="inlineImage" src="/CEK/Resources/Images/DevConsole_Plus_Button.png" /> button to the right of **{{ book.DevConsole.cek_builder_list_title_intent }}**.
3. Enter the name "ThrowDiceIntent" in the input field below **{{ book.DevConsole.cek_builder_new_intent }}**.
4. Press enter or click the **{{ book.DevConsole.cek_builder_new_intent_create }}** button next to the input field.

	<img src="/CEK/Resources/Images/CEK_Tutorial_NewIntent.png" style=" max-width:800px;" />

	<div class="danger">
	  <p><strong>Caution!</strong></p>
		<p>The intent name is case-sensitive.</p>
	</div>

### Adding a phrase to the sample utterance list
Follow the steps below to configure the user utterances to be processed with the intent created above. We will only add one user utterance for this tutorial, but it is beneficial to have as many sample utterances as possible.
1. Enter "Throw dice" in the **{{ book.DevConsole.cek_builder_intent_expression_title }}** field.
2. Press enter or click the <img class="inlineImage" src="/CEK/Resources/Images/DevConsole_Plus_Button.png" /> button.
3. Once you have finished entering all sample utterances, click **{{ book.DevConsole.cek_save }}**.

	<img src="/CEK/Resources/Images/CEK_Tutorial_SpeechExample.png" style=" max-width:800px; margin-top:10px; margin-bottom:10px;" />

### Building and testing
To check that the interaction model is operating as intended, build and test the interaction model.

1. Click the **{{ book.DevConsole.BuildButton }}** button on the upper-left corner of the **Custom extension** screen.

	<div class="note">
	  <p><strong>Note!</strong></p>
		<p>The build takes around 3-5 minutes to complete. Once the build starts, the button changes to <strong>{{ book.DevConsole.IsBuilding }}</strong>. It returns to a <strong>{{ book.DevConsole.BuildButton }}</strong> button again once the build is complete.</p>
	</div>

2. Once the build is complete, click the **{{ book.DevConsole.cek_test }}** menu below the **{{ book.DevConsole.BuildButton }}** button.

3. Enter the sentence to test in the **{{ book.DevConsole.cek_builder_test_expression_title }}** field. For example, enter "Roll the dice"
4. Press enter or click the **{{ book.DevConsole.cek_builder_test_request_test }}** button.
5. Check whether "ThrowDiceIntent" appears in the **{{ book.DevConsole.cek_builder_test_intent_result }}** field under **{{ book.DevConsole.cek_builder_test_result_title }}**.

	<img src="/CEK/Resources/Images/CEK_Tutorial_Test.png" style="max-width:800px;"/>

	<div class="note">
	<p><strong>Note!</strong></p>
	<p>If you have not registered an extension server URL that can be accessed externally in Step 2, <strong>{{ book.DevConsole.cek_builder_test_service_response }}</strong> will display "{{ book.DevConsole.cek_builder_test_no_response }}".</p>
	</div>
