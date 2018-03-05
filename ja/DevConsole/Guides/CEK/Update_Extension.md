# Extensionをアップデートする

Extensionが審査を通過し、配布が承認されると、そのextensionは**{{ book.DevConsole.cek_status_prd }}**状態になります。Clova developer consoleはその際、次のようにextensionの2つのバージョンを作成します。

* **{{ book.DevConsole.cek_version_service }}**バージョン：現在、**{{ book.DevConsole.cek_status_prd }}**状態のextensionの元の情報を持つバージョンです。Extension情報の照会のみできます。
* **{{ book.DevConsole.cek_version_test }}**バージョン：配布されたextensionの元の情報をコピーして作成されたバージョンです。Extensionをアップデートする際に使用されます。

![](/DevConsole/Resources/Images/DevConsole-Extension_List_After_Submission.png)

**{{ book.DevConsole.cek_version_service }}**バージョンのextensionは、現在サービス中の内容を反映しているため、修正することができません。Extensionをアップデートするには、コピーされた**{{ book.DevConsole.cek_version_test }}**バージョンを使用します。Extensionに次の項目に該当するアップデート事項がある場合、**{{ book.DevConsole.cek_version_test }}**バージョンのextensionに反映後、再び審査をリクエストします。
* [基本情報](/DevConsole/Guides/CEK/Register_Extension.md#InputExtensionInfo)
* [サーバーとの連携情報](/DevConsole/Guides/CEK/Register_Extension.md#SetServerConnection)
* [Iinteraction model](/DevConsole/Guides/CEK/Register_Interaction_Model.md)
* [配布情報](/DevConsole/Guides/CEK/Deploy_Extension.md)

審査を通過すると、**{{ book.DevConsole.cek_version_service }}**バージョンから、アップデートが反映された**{{ book.DevConsole.cek_version_test }}**バージョンに置き換えられます。それからまた、**{{ book.DevConsole.cek_version_service }}**バージョンのextensionをコピーし、**{{ book.DevConsole.cek_version_test }}**バージョンのextensionを生成します。

以下の図は、Clova developer consoleでextensionがアップデートされる仕組みを示します。

![](/DevConsole/Resources/Images/DevConsole-Branch_Chart_For_Extension_Update.png)
