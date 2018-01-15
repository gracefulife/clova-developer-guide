# Deploying your extension
If the [custom extension](/CEK/Guides/Build_Custom_Extension.md) and the Clova Home extension are successfully [registered to the Clova developer console](/DevConsole/Guides/CEK/Register_Extension.md), now the registered extension is ready to be deployed to the Clova service. Once it is deployed, regular users can use the extension from a menu named **Manage extension feature**.

Follow the below steps in order to deploy the extension.

* (Exclusively for the custom extension) [Building the interaction model](#BuildInteractionModel)
* (Exclusively for the custom extension) [Testing the interaction model](#TestInteractionModel)
* [Entering deployment information](#InputDeploymentInfo)
* [Entering personal information and compliance to regulation](#InputComplianceInfo)
* [Requesting extension approval](#RequestExtensionSubmission)

## Building interaction model {#BuildInteractionModel}

To deploy the custom extension, the [interaction model has to be defined](/DevConsole/Guides/CEK/Define_Interaction_Model.md). The defined interaction model must go through a build process to [test](#TestInteractionModel) or use a newly written or updated contents. The defined interaction model can be built following the steps.

<ol>
  <li>From the registered extension list, click <strong>Change</strong> from the list of extension you are about to build the interaction model.</li>
  <img src="/DevConsole/Resources/Images/DevConsole-Extension_list_after_Creation.png" />
  <li>Select the <strong>Interaction model</strong> menu from tab menu located at the top.</li>
  <img src="/DevConsole/Resources/Images/DevConsole-Build_Interaction_Model_1.png" />
  <li>From the <strong>Interaction model: Dashboard</strong> page, click <strong>Build</strong> button on the right side to start the interaction model build. Depending on size of the interaction model, it might take 3 to 5 minutes.</li>
  <img src="/DevConsole/Resources/Images/DevConsole-Build_Interaction_Model_2.png" />
</ol>

Note that the build cannot be canceled once it is started even if you navigate to other menu from the **Interaction model: Dashboard** page. Menu modification and other actions can be done after the build.

## Testing the interaction model {#TestInteractionModel}

If the [interaction model build](#BuildInteractionModel) is done, now you can test the interaction model. The speech text can be tested as follow.

<ol>
  <li>Click <strong>Test</strong> located under the <strong>Interaction model builder menu</strong> and the <strong>Interaction model: test</strong> page will appear.</li>
  <img src="/DevConsole/Resources/Images/DevConsole-Test_Menu.png" />
  <li>Enter speech texts on the <strong>User expressions in texts</strong> and click <strong>Request for test</strong>.</li>
  <img src="/DevConsole/Resources/Images/DevConsole-Test_Utterance_Example.png" />
</ol>

After the test is done, you can check results as below. According to the results, the following items have to be verified.

Check **Service response item** item whether the [registered custom extension](/DevConsole/Guides/CEK/Register_Extension.md) is responding properly.
Check **Analyzed intent** item and **Analyzed intent slot** item whether the intents and slots are recognized as intended.
Check **Service request JSON** item whether there is any issue on the [request message](/CEK/References/CEK_API.md#CustomExtRequestMessage) sending from CEK to the custom extension. The test can be re-conducted when clicking the **Re-request for test** button after modifying the JSON.
Check **Service response JSON** item whether the [response message](/CEK/References/CEK_API.md#CustomExtResponseMessage) is sent as intended by the registered custom extension.

![](/DevConsole/Resources/Images/DevConsole-Test_Result.png)

## Entering deployment information {#InputDeploymentInfo}

The deployment information can be entered after [registering the extension](/DevConsole/Guides/CEK/Register_Extension.md) and [defining the interaction model](/DevConsole/Guides/CEK/Define_Interaction_Model.md) from the Clova developer console. Select **Deployment information** from the extension registration menu.

![](/DevConsole/Resources/Images/DevConsole-Deployment_Info_Menu.png)

Enter deployment information as below.

![](/DevConsole/Resources/Images/DevConsole-Input_Deployment_Info.png)

* An information explaining about the extension is provided at the **Managing extension feature** for the users. In the information the following details are included.
  - **Category**: A type of extension used to check list of extension as per types or to search.
  - **Summary of extension**: A brief summary of extension to be displayed on the extension details page.
  - **Details of extension**: A thorough explanation of extension to be displayed on the extension details page in case the users want to understand in details.
  - **Representative expressions in text**: An example text showing how users can use the extension.  The first explanation will be displayed to show an extension list.
  - **Search keywords**: If a specific keyword is included in a users’ search, the search keyword will help to find better search result.
  - **Small icon**: An image file displaying an extension icon (108px X 108px).
  - **Big icon**: A big size image file of an extension icon. It will be displayed in the future (512 px X 512 px).
* Instruction for test: An information for personnel in charge of the [extension approval](#RequestExtensionSubmission) process refers to approve an extension. It is not exposed to regular users. On the information, enter the list of intent provided by the extension and a test account (if required to [connect to the account](/CEK/Guides/LInk_User_Account.md)) and the speech examples to test listed features.
* Service country and district: The deployment of the extension can only be done in Republic of Korea. At the moment, there is no other countries or districts where the extension service can be provided.

The above information will be displayed as below from the Clova app **Managing extension feature** menu.

| List of Extension | Extension in Detail |
|-------------------|-------------------|
| ![Extension List](/DevConsole/Resources/Images/DevConsole-Store_UI_Example_Extension_List.png) | ![Extension Details](/DevConsole/Resources/Images/DevConsole-Store_UI_Example-Extension_Details.png) |

<div class="note">
  <p><strong>Note!</strong></p>
  <p>Some of information being displayed on the ‘Details of extension’ are from the <a href="/DevConsole/Guides/CEK/Register_Extension.html#InputExtensionInfo">Registering basic information of the extension</a>.</p>
</div>

## Entering personal information and compliance to regulation {#InputComplianceInfo}

The last step to take to enter necessary information for the extension deployment. It requires personal information and compliance to regulation. Click **Personal information and compliance to regulation** from the extension registration menu.

![](/DevConsole/Resources/Images/DevConsole-Policy_Menu.png)

Enter required information as shown below.

![](/DevConsole/Resources/Images/DevConsole-Input_Policy.png)

* Purchase process: Select **Yes** if a user has to process a payment.
* Collecting personal information: Select **Yes** if your extension is collecting user information.
* Access of underage: Select **Yes** if underage users can use your extension.
* URL of personal information policy: If your extension is collecting personal information, enter URL of a page indicating the policy related to the collection. The URL will be located at the bottom of the extension details page.
* Exemption clauses: Enter URL of a page indicating the exemption clauses for your extension. The URL will be located at the bottom of the extension details page.

**URL of personal information policy** and **Exemption clauses** are displayed as below on the extension details page.

![](/DevConsole/Resources/Images/DevConsole-Store_UI_Example-Extension_Policy.png)

## Requesting extension approval {#RequestExtensionSubmission}

You will be ready to request for a review for the final extension if [Deployment information](#InputDeploymentInfo) and the [Personal information and compliance to regulation](#InputComplianceInfo) are completed.

A Clova manager will review registered extension details and check execution possibilities and suitability in actual use.

* Once it is verified that the extension is operating normally without issues, it will pass the review. After passing the review the execution can be deployed instantly or at a desired time.
* In cases where errors or critical defects are found in the user scenario during the review, you can request for a modification so that it can be re-reviewed.

![](/DevConsole/Resources/Images/DevConsole-Extension_Submission_Process.png)

The review will be done individually at a particular environment only for the review. In case of a service requiring [user account connection](/CEK/Guides/LInk_User_Account.md), a test account information has to be entered on the **Instruction for test** when [entering the deployment information](#InputDeploymentInfo).

Review items are as below when reviewing your extension.

1. Verify extension build
  * Check if vocabularies are used accurately for the extension service.
  * Check the interaction model such as intents, slots and more.
  * Must refer to a guide on essential elements of development.
2. Verify user scenario
  * Check if there are inappropriate sentences in the contexts.
  * Check if there are any banned words or sensitive words in speech data of the scenario.
  * If the extension is [connected to the user account](/CEK/Guides/LInk_User_Account.md), specific part of the service can be examined.
3. Verify deployment information
  * Check if the deployment information such as explanation, category, and search keyword are correctly entered on the extension.
  * Check if the extension is working properly by following the policies such as Personal information and compliance to regulation.
