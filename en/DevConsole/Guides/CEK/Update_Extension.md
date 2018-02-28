# Updating the extension

If the extension passes the review and deployment is approved, the extension is changed to a **{{ book.DevConsole.cek_status_prd }}** status. At this time, the Clova developer console makes two versions of the extension as shown below.

* **{{ book.DevConsole.cek_version_service }}** version: Original version containing the origination information of the extension in a **{{ book.DevConsole.cek_status_prd }}** status. You can only view the information on the extension.
* **{{ book.DevConsole.cek_version_test }}** version: Copied version of the original which is used to update the extension.

![](/DevConsole/Resources/Images/DevConsole-Extension_List_After_Submission.png)

The extension information in the **{{ book.DevConsole.cek_version_service }}** version includes the details that are currently in service, and cannot be edited. Therefore, the extension must be updated using the copied **{{ book.DevConsole.cek_version_test }}** version. When there is an update on the items shown below, you can implement it in the **{{ book.DevConsole.cek_version_test }}** version and request for another review.
* [Basic information](/DevConsole/Guides/CEK/Register_Extension.md#InputExtensionInfo)
* [Server connection information](/DevConsole/Guides/CEK/Register_Extension.md#SetServerConnection)
* [Interaction model](/DevConsole/Guides/CEK/Register_Interaction_Model.md)
* [Deployment information](/DevConsole/Guides/CEK/Deploy_Extension.md)

Once the review is passed, the**{{ book.DevConsole.cek_version_service }}** version is replaced with the updated **{{ book.DevConsole.cek_version_test }}** version. Then, the extension information from the **{{ book.DevConsole.cek_version_service }}** version is copied again to create the new **{{ book.DevConsole.cek_version_test }}** version of the extension information.

The image below shows an overview of an extension update in the Clova developer console.

![](/DevConsole/Resources/Images/DevConsole-Branch_Chart_For_Extension_Update.png)

