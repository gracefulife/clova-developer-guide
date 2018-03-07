# Testing an extension
You can test the registered extension or interaction model prior to deployment. Follow the steps below to test the extension and the interaction model:

* (Custom extension only) [Building an interaction model](#BuildInteractionModel)
* (Custom extension only) [Testing an interaction model](#TestInteractionModel)
* [Testing an extension using Clova app](#TestOnClovaApp)

## Building an interaction model {#BuildInteractionModel}

In order to deploy the custom extension, the [interaction model must be registered](/DevConsole/Guides/CEK/Register_Interaction_Model.md). The defined interaction must go through the build process to [test](#TestInteractionModel) or use the newly written or updated details. Build the interaction model by completing the following steps:

<ol>
  <li>On the list of registered extensions, click on the <strong>{{ book.DevConsole.cek_edit }}</strong> menu of the extension to build the interaction model.</li>
  <img src="/DevConsole/Resources/Images/DevConsole-Interaction_Model_Menu.png" />
  <li>On the <strong>{{ book.DevConsole.cek_interaction_model }}: {{ book.DevConsole.cek_builder_header_title_dashboard }}</strong> screen, click the <strong>{{ book.DevConsole.cek_builder_menu_build }}</strong> button on the top left section to build the interaction model. It may take around 3-5 minutes depending on the size of the interaction model.</li>
  <img src="/DevConsole/Resources/Images/DevConsole-Build_Interaction_Model.png" />
</ol>

<div class="note">
  <p><strong>Note!</strong></p>
  <p>If you move to a different menu within the <strong>{{ book.DevConsole.cek_interaction_model }}: {{ book.DevConsole.cek_builder_header_title_dashboard }}</strong> screen, the build will not be cancelled. You can move between menus or edit details after starting the build.</p>
</div>

## Testing an interaction model {#TestInteractionModel}

Once the [interaction model build](#BuildInteractionModel) is complete, you can test the interaction model. Follow the steps below to test the utterances:

<ol>
  <li>Click the <strong>{{ book.DevConsole.cek_test }}</strong> menu below the menu bar on the left. When you click the menu, the <strong>{{ book.DevConsole.cek_interaction_model }}: {{ book.DevConsole.cek_test }}</strong> screen will be displayed.</li>
  <img src="/DevConsole/Resources/Images/DevConsole-Test_Menu.png" />
  <li>On the <strong>{{ book.DevConsole.cek_builder_test_expression_title }}</strong> field, enter the utterance to test and click the <strong>{{ book.DevConsole.cek_builder_test_request_test }}</strong> button.</li>
  <img src="/DevConsole/Resources/Images/DevConsole-Test_Utterance_Example.png" />
</ol>

Once the test is complete, you can check the results. Based on the results below, you must check the following items:

* Use the **{{ book.DevConsole.cek_builder_test_service_response }}** item to check whether the [registered custom extension](/DevConsole/Guides/CEK/Register_Extension.md) is responding properly.
* Use the **{{ book.DevConsole.cek_builder_test_intent_result }}** and **{{ book.DevConsole.cek_builder_test_slot_result }}** item to check whether intents and slots are recognized as intended.
* Use the **{{ book.DevConsole.cek_builder_test_request_json }}** item to check whether there are any problems with the [request messages](/CEK/References/CEK_API.md#CustomExtRequestMessage) which the CEK sends to the custom extension. In addition, you can perform the test again after editing the details of the corresponding JSON by clicking the **{{ book.DevConsole.cek_builder_test_test_again }}** button.
* Use the **{{ book.DevConsole.cek_builder_test_response_json }}** item to check whether the registered custom extension sends [response messages](/CEK/References/CEK_API.md#CustomExtResponseMessage) as intended.

![](/DevConsole/Resources/Images/DevConsole-Test_Result.png)

## Testing an extension using the Clova app {#TestOnClovaApp}

You can test the extensions on the actual client, the Clova app. For this, you must enter the <strong>{{ book.OrientedService }} account</strong> of the developer or the tester in the **{{ book.DevConsole.cek_tester }}** field of the page for registering the basic extension information. Click **{{ book.DevConsole.cek_save }}** after adding the account to test the extension under development on the Clova app where the entered account is verified. To cancel the test from the Clova app, simply delete the entered account information.

![](/DevConsole/Resources/Images/DevConsole-Add_Tester_ID.png)

<div class="note">
  <p><strong>Note!</strong></p>
  <p>Wait a short while after registering the tester ID to test the extension. If you are unable to test the extension even after about an hour, make an inquiry through the forum or the partnerships team.</p>
</div>

