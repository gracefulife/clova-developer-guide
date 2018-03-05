# Clova developer consoleの概要

Clova developer consoleは、Clovaプラットフォームと連携するデバイスまたはサービスを開発する際に、必要な情報や機能を提供するウェブツールです。クライアントの開発者はClova developer consoleで、開発するクライアント(デバイスまたはアプリ)の情報を入力し、そのクライアントが[CICにアクセス](/CIC/CIC_Overview.md)できるようにセキュリティ情報を設定します。Extensionの開発者は、CEKとextensionがメッセージをやり取りできるように[extensionの情報を入力](/DevConsole/Guides/CEK/Register_Extension.md)し、[interaction modelを登録](/DevConsole/Guides/CEK/Register_Interaction_Model.md)します。また、extensionの開発者は、[extensionを配布](/DevConsole/Guides/CEK/Deploy_Extension.md)するためにextensionをテストし、extensionの審査もリクエストする必要があります。

クライアントまたはextensionを開発する際、Clova developer consoleは以下の仕組みで使用されます。

![](/DevConsole/Resources/Images/DevConsole-Concept_Diagram.png)

Clova developer consoleは、CICメニューとCEKメニューを提供します。それぞれのメニューで、次の作業を行えます。

* [CEKメニュー](/DevConsole/Guides/CEK/Using_CEK_Menu.md)
  * [Extensionを登録する](/DevConsole/Guides/CEK/Register_Extension.md)
  * [Interaction modelを登録する](/DevConsole/Guides/CEK/Register_Interaction_Model.md)
  * [Extensionをテストする](/DevConsole/Guides/CEK/Test_Extension.md)
  * [Extensionを配布する](/DevConsole/Guides/CEK/Deploy_Extension.md)
  * [Extensionをアップデートする](/DevConsole/Guides/CEK/Update_Extension.md)
  * [Extensionを中止および削除する](/DevConsole/Guides/CEK/Remove_Extension.md)

* CICメニュー(今後サービス予定)
  * クライアントデバイスおよびアプリを登録する
  * クライアント認証関連情報を登録する
  * クライアントデバイス仕様を登録する
