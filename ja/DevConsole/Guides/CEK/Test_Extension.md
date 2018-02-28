# Extensionをテストする
登録したExtensionとinteraction modelは、配布する前にテストすることができます。次の項目を確認して、Extensionとinteraction modelをテストします。

* (custom Extension専用)[対話モデルをビルドする](#BuildInteractionModel)
* (custom Extension専用)[対話モデルをテストする](#TestInteractionModel)
* [ClovaアプリでExtensionをテストする](#TestOnClovaApp)

## 対話モデルをビルドする {#BuildInteractionModel}

Custom Extensionを配布する場合、先に[interaction modelを登録](/DevConsole/Guides/CEK/Register_Interaction_Model.md)する必要があります。また、定義されたinteraction modelを[テスト](#TestInteractionModel)または使用するには、そのinteraction modelをビルドする必要があります。次のように定義されたinteraction modelをビルドできます。

<ol>
  <li>登録したExtensionのリストから、ビルドするinteraction modelの<strong>{{ book.DevConsole.cek_edit }}</strong>メニューをクリックします。</li>
  <img src="/DevConsole/Resources/Images/DevConsole-Interaction_Model_Menu.png" />
  <li><strong>{{ book.DevConsole.cek_interaction_model }}：{{ book.DevConsole.Dashboard }}</strong>画面で、左上にある<strong>{{ book.DevConsole.BuildButton }}</strong>ボタンをクリックすると、interaction modelのビルドが開始されます。対話モデルのサイズなどによって、3~5分ぐらいかかることがあります。</li>
  <img src="/DevConsole/Resources/Images/DevConsole-Build_Interaction_Model.png" />
</ol>

<div class="note">
  <p><strong>メモ</strong></p>
  <p>ビルド中に<strong>{{ book.DevConsole.cek_interaction_model }}：{{ book.DevConsole.Dashboard }}</strong>内で他のメニューに移動しても、ビルドはキャンセルされません。ビルドが開始されてからも、自由にメニューを移動したり、内容を編集したりできます。</p>
</div>

## 対話モデルをテストする {#TestInteractionModel}

[対話モデルのビルド](#BuildInteractionModel)が完了すると、interaction modelをテストできます。次のように発話をテストできます。

<ol>
  <li>左側のナビゲーションで<strong>{{ book.DevConsole.cek_test }}</strong>メニューをクリックします。メニューをクリックすると、<strong>{{ book.DevConsole.cek_interaction_model }}：{{ book.DevConsole.cek_test }}</strong>画面が表示されます。</li>
  <img src="/DevConsole/Resources/Images/DevConsole-Test_Menu.png" />
  <li><strong>{{ book.DevConsole.cek_builder_test_expression_title }}</strong>フィールドにテストする発話を入力し、<strong>{{ book.DevConsole.cek_builder_test_request_test }}</strong>ボタンをクリックします。</li>
  <img src="/DevConsole/Resources/Images/DevConsole-Test_Utterance_Example.png" />
</ol>

テストが完了すると、次のような結果を確認できます。結果を基に、下記の項目を確認します。

* **{{ book.DevConsole.cek_builder_test_service_response }}**項目から、[登録したcustom Extension](/DevConsole/Guides/CEK/Register_Extension.md)が正しく応答しているか確認します。
* **{{ book.DevConsole.cek_builder_test_intent_result }}**項目と**{{ book.DevConsole.cek_builder_test_slot_result }}**項目から、intentとslotが正しく認識されているか確認します。
* **{{ book.DevConsole.cek_builder_test_request_json }}**項目から、CEKがcustom Extensionに送る[リクエストメッセージ](/CEK/References/CEK_API.md#CustomExtRequestMessage)に異常がないか確認します。JSONファイルを修正してから**{{ book.DevConsole.cek_builder_test_test_again }}**ボタンをクリックすると、再度テストできます。
* **{{ book.DevConsole.cek_builder_test_response_json }}**項目から、登録したcustom Extensionが正しく[レスポンスメッセージ](/CEK/References/CEK_API.md#CustomExtResponseMessage)を返しているか確認します。

![](/DevConsole/Resources/Images/DevConsole-Test_Result.png)

## ClovaアプリでExtensionをテストする {#TestOnClovaApp}

実際のクライアントであるClovaアプリで、Extensionをテストすることができます。そのためには、Extensionの基本情報を登録するページの**{{ book.DevConsole.cek_tester }}**フィールドに、開発者またはExtensionをテストする人の<strong>{{ book.OrientedService }}アカウント</strong>を入力する必要があります。アカウントを追加して**{{ book.DevConsole.cek_save }}**ボタンをクリックすると、そのアカウントで認証されたClovaアプリで、開発中のExtensionをテストできます。Clovaアプリでテストを中止するには、入力したアカウント情報を削除します。

![](/DevConsole/Resources/Images/DevConsole-Add_Tester_ID.png)

<div class="note">
  <p><strong>メモ</strong></p>
  <p>テスターIDを登録してしばらく待つと、Extensionをテストできます。もし1時間以上経ってもExtensionをテストできない場合には、フォーラムまたは提携担当者までお問い合わせください。</p>
</div>
