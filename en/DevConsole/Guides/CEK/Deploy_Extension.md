# Deploying an extension
If the [custom extension](/CEK/Guides/Build_Custom_Extension.md) or Clova Home extension are registered on the [Clova developer console](/DevConsole/Guides/CEK/Register_Extension.md), it can be deployed to the Clova service. Once deployed, the regular users can find the extension from the **{{ book.DevConsole.ManageExtensions }}** menu in the extension store.

To deploy an extension, you must typically complete the following steps:

* [Entering deployment information](#InputDeploymentInfo)
* [Entering privacy and compliance information](#InputComplianceInfo)
* [Requesting a review](#RequestExtensionSubmission)

## Entering deployment information {#InputDeploymentInfo}

You can enter the deployment information after [registering the extension](/DevConsole/Guides/CEK/Register_Extension.md) and [registering an interaction model](/DevConsole/Guides/CEK/Register_Interaction_Model.md) on the Clova developer console. Once they are registered, select **{{ book.DevConsole.cek_publishing }}** from the Registered Extensions menu.

![](/DevConsole/Resources/Images/DevConsole-Deployment_Info_Menu.png)

Enter the deployment information following the example below.

![](/DevConsole/Resources/Images/DevConsole-Input_Deployment_Info.png)

The information on the extension entered here will be provided to users on the **{{ book.DevConsole.ManageExtensions }}** menu of the Clova app in the extension store. The details of the entered information are as follows:

* **{{ book.DevConsole.cek_category }}**: The type of extension that can be used by users to check or search the extension per type.
* **{{ book.DevConsole.cek_test_instructions }}**: The information used by the review team as a reference for the [Extension approval](#RequestExtensionSubmission) process to verify the extension. It is not shown to regular users. Follow the instruction to fill in the information.
* Supported countries and regions: Currently, the extension can only be deployed in Korea.
* **{{ book.DevConsole.cek_full_skill_desc }}**: The detailed description of the extension to be provided to users on the **{{ book.DevConsole.ExtensionPage }}**. Follow the instruction to fill in the information.
* **{{ book.DevConsole.cek_short_skill_desc }}**: The short description of the extension to be provided to users on **{{ book.DevConsole.ExtensionHome }}**, such as promotional information.
* **{{ book.DevConsole.cek_example_phrases }}**: The sample utterance to show users how to use the extension. This will be displayed on the **{{ book.DevConsole.ExtensionPage }}**. In particular, the first sample utterance will be displayed when showing the extension list on **{{ book.DevConsole.ExtensionHome }}**.
* **{{ book.DevConsole.cek_keywords }}**: The keywords that can be used by users to find the extension on the search result.
* **{{ book.DevConsole.cek_small_icon }}**: The small icon file of the extension (108 x 108 pixels). This will be displayed in the **{{ book.DevConsole.ManageExtensions }}** menu or the **{{ book.DevConsole.ExtensionPage }}**.
* **{{ book.DevConsole.cek_large_icon }}**: The large icon file of the extension (512 x 512 pixels). This will be used as the main icon for the extension in the future.

Once the information is filled out, it is displayed on the **{{ book.DevConsole.ManageExtensions }}** menu of the Clova app in the extension store, as shown below.

| {{ book.DevConsole.ExtensionHome }} | {{ book.DevConsole.ExtensionPage }}   |
|-------------------|-------------------|
| ![Extension List](/DevConsole/Resources/Images/DevConsole-Store_UI_Example-Extension_Store_Home.png) | ![Extension Details](/DevConsole/Resources/Images/DevConsole-Store_UI_Example-Extension_Page.png) |

<div class="note">
  <p><strong>Note!</strong></p>
  <p>Some of the information displayed on the <strong>{{ book.DevConsole.ExtensionPage }}</strong> is based on the information entered when <a href="/DevConsole/Guides/CEK/Register_Extension.html#InputExtensionInfo">registering basic information for the extension</a>.</p>
</div>

## Entering privacy and compliance information {#InputComplianceInfo}

As the last step to enter the information required to deploy the extension, you must enter the details on privacy and compliance. Once they are registered, select **{{ book.DevConsole.cek_privacy }}** from the Registered Extensions menu.

![](/DevConsole/Resources/Images/DevConsole-Policy_Menu.png)

Enter the information following the example below.

![](/DevConsole/Resources/Images/DevConsole-Input_Policy.png)

* **{{ book.DevConsole.cek_allow_purchase }}**: Select **{{ book.DevConsole.cek_yes }}** if the user must make a payment when using the extension.
* **{{ book.DevConsole.cek_use_personal_info }}**: Select **{{ book.DevConsole.cek_yes }}** if the extension collects user's personal information.
* **{{ book.DevConsole.cek_child_directed }}**: Select **{{ book.DevConsole.cek_yes }}** if the extension can be used by minors.
* **{{ book.DevConsole.cek_privacy_policy_url }}**: Enter information on privacy policy, if the extension collects personal information. This will be displayed at the bottom of the extension description page.
* **{{ book.DevConsole.cek_terms_of_use }}**: Enter the URL of the disclaimer for the extension. This will be displayed at the bottom of the extension description page with the URL of privacy policy.

The URLs entered in **{{ book.DevConsole.cek_privacy_policy_url }}** and **{{ book.DevConsole.cek_terms_of_use }}** will be displayed on the **{{ book.DevConsole.ExtensionPage }}** as follows:

![](/DevConsole/Resources/Images/DevConsole-Store_UI_Example-Extension_Policy.png)

## Requesting a review {#RequestExtensionSubmission}

Once you have filled out the [deployment information](#InputDeploymentInfo) and the [privacy and compliance information](#InputComplianceInfo), you can request a review on the last registered extension. Then a Clova administrator reviews the extension, such as its registered information, actual execution, and suitability.

* If the extension is functioning properly and no issues are found during the review, it will pass the review and you will be able to deploy the extension instantly or at a desired time.
* If an execution error is found during the review or a critical issue is found within the user scenario, the request for deployment will be rejected by the administrator. Then the extension will go back to the previous status.

![](/DevConsole/Resources/Images/DevConsole-Extension_Submission_Process.png)

You can request for a review by clicking the **{{ book.DevConsole.cek_request_submit }}** menu on the registered extensions list.

![](/DevConsole/Resources/Images/DevConsole-Submit_Extension_1.png)

Or, click the **{{ book.DevConsole.cek_request_submit }}** button at the bottom of the screen for entering [privacy and compliance information](#InputComplianceInfo).

![](/DevConsole/Resources/Images/DevConsole-Submit_Extension_2.png)

If you click on the **{{ book.DevConsole.cek_request_submit }}** button, you can leave information on the review request for the administrator. If it is your first review request for the extension, you can mention that and describe the extension. If it is your second review request for the extension due to updates on functions or the interaction model, enter the improved details. Or, if it is your second review request due to rejections, enter whether the issues have been corrected.

![](/DevConsole/Resources/Images/DevConsole-Submission_Request_Message.png)

<div class="note">
  <p><strong>Note!</strong></p>
  <p>You cannot edit the extension information and interaction model during the review stage.</p>
</div>

The review will be carried out individually in a separate environment. If the service requires [account linking](/CEK/Guides/Link_User_Account.md), then you must enter the account information for testing under the **{{ book.DevConsole.cek_test_instructions }}** when you [enter the deployment information](#InputDeploymentInfo).

The assessment criteria for the extension review are as follows:

* Extension build verification
  * Check whether appropriate terms for the extension service are used.
  * Verify the interaction model, such as intents and slots.
  * Check whether the service is provided in accordance to the [detailed goals](/Design/Design_Guideline_For_Extension.md#SettingGoal) of the extension.
* [Usage scenario](/Design/Design_Guideline_For_Extension.md#MakeUseCaseScenarioScript) verification
  * Check whether there are unnatural sentences in the dialogue.
  * Check whether there are sensitive or prohibited words in the utterance data used in scenarios.
  * If the extension [links to a user account](/CEK/Guides/Link_User_Account.md), you can examine specific parts of the service.
* Deployment information verification
  * Check whether deployment information, such as the description, category, or search keyword of the extension, is correctly entered for the extension.
  * Check whether the extension is operating properly according to the entered policies, such as the privacy policy.

You can click on the **{{ book.DevConsole.cek_cancel_review }}** menu anytime during the review process to cancel review request. If you cancel the review request, the extension will go back to the previous status.

![](/DevConsole/Resources/Images/DevConsole-Cancel_Submission.png)

If the extension does not pass the review, the **{{ book.DevConsole.cek_status }}** of the extension changes to **{{ book.DevConsole.cek_status_rejected }}**. This status is identical to the **{{ book.DevConsole.cek_status_dev }}** status and you can make a review request again.

![](/DevConsole/Resources/Images/DevConsole-Extension_Submission_Rejected.png)

At this time, you can click the **{{ book.DevConsole.cek_view }}** menu on the **{{ book.DevConsole.cek_message }}** to check feedback on the review.

![](/DevConsole/Resources/Images/DevConsole-Show_Submission_Feedback.png)

