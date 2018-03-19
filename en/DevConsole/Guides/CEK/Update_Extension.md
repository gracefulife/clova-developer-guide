# Updating the extension

When your extension passes the review and deployment is approved, the extension is changed to the **{{ book.DevConsole.cek_status_prd }}** status. Along with the status change, the Clova developer console creates two versions of the extension as shown below.

* **{{ book.DevConsole.cek_version_service }}** version: Original version containing the original information of the extension in the **{{ book.DevConsole.cek_status_prd }}** status. This version of the extension is view-only.
* **{{ book.DevConsole.cek_version_test }}** version: A copied version of the original which is used to update the extension.

![](/DevConsole/Resources/Images/DevConsole-Extension_List_After_Submission.png)

The extension information in the **{{ book.DevConsole.cek_version_service }}** version includes the details that are currently in service, and cannot be edited. Therefore, the extension must be updated using the copied **{{ book.DevConsole.cek_version_test }}** version. When there is an update on the items shown below, you can implement them on the **{{ book.DevConsole.cek_version_test }}** version and request for another review.
* [Basic information](/DevConsole/Guides/CEK/Register_Extension.md#InputExtensionInfo)
* [Server connection information](/DevConsole/Guides/CEK/Register_Extension.md#SetServerConnection)
* [Interaction model](/DevConsole/Guides/CEK/Register_Interaction_Model.md)
* [Deployment information](/DevConsole/Guides/CEK/Deploy_Extension.md)

Once your extension passes the review, the **{{ book.DevConsole.cek_version_service }}** version is replaced with the updated **{{ book.DevConsole.cek_version_test }}** version. The extension information from the **{{ book.DevConsole.cek_version_service }}** version is then copied again to create the new **{{ book.DevConsole.cek_version_test }}** version of the extension information.

The image below shows an overview of an extension update on the Clova developer console.

![](/DevConsole/Resources/Images/DevConsole-Branch_Chart_For_Extension_Update.png)
