# Extensionを配布する
[Custom extension](/CEK/Guides/Build_Custom_Extension.md)またはClova Home extensionを[Clova Developer Centerに登録](/DevConsole/Guides/CEK/Register_Extension.md)すると、登録したextensionをClovaサービスに配布できます。Extensionを配布すると、エンドユーザーが**{{ book.DevConsole.ManageExtensions }}**というメニュー(Extensionストア)で配布されたextensionを使用できるようになります。

Extensionの配布は、通常、次の順で行われます。

* [配布情報を入力する](#InputDeploymentInfo)
* [プライバシーポリシーおよびコンプライアンス情報を入力する](#InputComplianceInfo)
* [審査をリクエストする](#RequestExtensionSubmission)

## 配布情報を入力する {#InputDeploymentInfo}

Clova Developer Centerで[extensionを登録](/DevConsole/Guides/CEK/Register_Extension.md)し、[Interaction modelを登録](/DevConsole/Guides/CEK/Register_Interaction_Model.md)してから、配布情報を入力できます。Extensionの登録メニューで**{{ book.DevConsole.cek_publishing }}**を選択します。

![](/DevConsole/Resources/Images/DevConsole-Deployment_Info_Menu.png)

次のように配布情報を入力します。

![](/DevConsole/Resources/Images/DevConsole-Input_Deployment_Info.png)

Extensionをユーザーに説明するための情報として、Clovaアプリの**{{ book.DevConsole.ManageExtensions }}**メニュー(Extensionストア)でユーザーに提供されます。次の情報を入力する必要があります。

* **{{ book.DevConsole.cek_category }}**：Extensionのカテゴリです。ユーザーがカテゴリごとにextensionのリストを確認したり、検索する際に利用されます。
* **{{ book.DevConsole.cek_test_instructions }}**：[Extensionの承認](#RequestExtensionSubmission)プロセスで承認担当者がextensionを検討する際、必要とされる参考情報です。エンドユーザーには表示されません。案内に従って作成します。
* サービス国および地域：現在、韓国にのみextensionを配布できます。
* **{{ book.DevConsole.cek_full_skill_desc }}**：**{{ book.DevConsole.ExtensionPage }}**でユーザーに提供するextensionの説明です。案内に従って作成します。
* **{{ book.DevConsole.cek_short_skill_desc }}**：**{{ book.DevConsole.ExtensionHome }}**でプロモーションなどの案内を表示する際に使用される説明です。
* **{{ book.DevConsole.cek_example_phrases }}**：ユーザーがextensionをどのように使用できるかを示す例です。**{{ book.DevConsole.ExtensionPage }}**に表示されます。特に、一番目の例は、**{{ book.DevConsole.ExtensionHome }}**でextensionのリストを表示する際に使用されます。
* **{{ book.DevConsole.cek_keywords }}**：ユーザーが特定のキーワードでextensionを検索すると、extensionがその検索結果に含まれます。
* **{{ book.DevConsole.cek_small_icon }}**：小サイズ(108x108ピクセル)のextensionのアイコンファイルです。**{{ book.DevConsole.ManageExtensions }}**と**{{ book.DevConsole.ExtensionPage }}**に表示されます。
* **{{ book.DevConsole.cek_large_icon }}**：大サイズ(512x512ピクセル)のextensionのアイコンファイルです。今後使用される予定です。

このように入力された情報は、Clovaアプリの**{{ book.DevConsole.ManageExtensions }}**メニュー(Extensionストア)で次のように表示されます。

| {{ book.DevConsole.ExtensionHome }} | {{ book.DevConsole.ExtensionPage }}   |
|-------------------|-------------------|
| ![Extension List](/DevConsole/Resources/Images/DevConsole-Store_UI_Example-Extension_Store_Home.png) | ![Extension Details](/DevConsole/Resources/Images/DevConsole-Store_UI_Example-Extension_Page.png) |

<div class="note">
  <p><strong>メモ</strong></p>
  <p><strong>{{ book.DevConsole.ExtensionPage }}</strong>に表示される一部の情報は、<a href="/DevConsole/Guides/CEK/Register_Extension.html#InputExtensionInfo">Extensionの基本情報を登録</a>する際に入力された情報を活用します。</p>
</div>

## プライバシーポリシーおよびコンプライアンス情報を入力する {#InputComplianceInfo}

Extensionの配布に必要な情報を入力する最後の段階です。プライバシーポリシーおよびコンプライアンス関連内容を入力します。Extensionの登録メニューで**{{ book.DevConsole.cek_privacy }}**を選択します。

![](/DevConsole/Resources/Images/DevConsole-Policy_Menu.png)

以下のように情報を入力します。

![](/DevConsole/Resources/Images/DevConsole-Input_Policy.png)

* **{{ book.DevConsole.cek_allow_purchase }}**：Extensionを使用する際、ユーザーが決済をしたり支払いをする場面がある場合、**{{ book.DevConsole.cek_yes }}**を選択します。
* **{{ book.DevConsole.cek_use_personal_info }}**：Extensionがユーザーの個人情報を取得する場合、**{{ book.DevConsole.cek_yes }}**を選択します。
* **{{ book.DevConsole.cek_child_directed }}**：未成年者のextension使用を許可する場合、**{{ book.DevConsole.cek_yes }}**を選択します。
* **{{ book.DevConsole.cek_privacy_policy_url }}**：Extensionが個人情報を取得する場合、それに関するプライバシーポリシーを提供するページを入力します。Extension説明ページの一番下に表示されます。
* **{{ book.DevConsole.cek_terms_of_use }}**：Extensionに関する免責条項を提供するページを入力します。プライバシーポリシーのURLと同じく、extension説明ページの一番下に表示されます。

**{{ book.DevConsole.cek_privacy_policy_url }}**と**{{ book.DevConsole.cek_terms_of_use }}**に入力された内容は、**{{ book.DevConsole.ExtensionPage }}**で次のように表示されます。

![](/DevConsole/Resources/Images/DevConsole-Store_UI_Example-Extension_Policy.png)

## 審査をリクエストする {#RequestExtensionSubmission}

Extensionの[配布情報](#InputDeploymentInfo)と[プライバシーポリシーおよびコンプライアンス情報](#InputComplianceInfo)まで入力すると、登録したextensionの審査をリクエストできます。Clovaの運営者は、登録されたextensionの情報、実際の動作確認と適合性などを審査します。

* Extensionが正常に動作し、検討した結果特に異常がない場合、extensionは審査を通過します。審査を通過すると、直ちに、または好きな時にextensionを配布できます。
* もし審査中に実行エラーが発生したり、ユーザーシナリオの深刻な問題が見つかったりした場合、運営者によって配布のリクエストがリジェクトされ、審査をリクエストする前に戻ります。

![](/DevConsole/Resources/Images/DevConsole-Extension_Submission_Process.png)

Extensionの審査をリクエストするには、登録したextensionのリストで**{{ book.DevConsole.cek_request_submit }}**メニューをクリックします。

![](/DevConsole/Resources/Images/DevConsole-Submit_Extension_1.png)

または[プライバシーポリシーおよびコンプライアンス情報](#InputComplianceInfo)を入力する画面の一番下にある**{{ book.DevConsole.cek_request_submit }}**ボタンをクリックして、リクエストすることもできます。

![](/DevConsole/Resources/Images/DevConsole-Submit_Extension_2.png)

**{{ book.DevConsole.cek_request_submit }}**をクリックすると、次のように審査のリクエストに関する情報を運営者に送信できます。Extensionの最初の審査リクエストの場合、最初の審査リクエストというメッセージと、extensionを説明するメッセージを記載します。Extensionの機能やinteraction modelにアップデートがあったか、またはリジェクトされたextensionを修正して再審査をリクエストする場合、改善事項やリジェクト意見の反映有無を入力します。

![](/DevConsole/Resources/Images/DevConsole-Submission_Request_Message.png)

<div class="note">
  <p><strong>メモ</strong></p>
  <p>審査中には、extensionの情報とinteraction modelを修正できません。</p>
</div>

審査はextensionごとに、審査のための別の環境で行われます。もし、[ユーザーアカウントとのリンク](/CEK/Guides/Link_User_Account.md)が必要なサービスの場合、[配布情報を入力](#InputDeploymentInfo)する際、テストのためのアカウントを**{{ book.DevConsole.cek_test_instructions }}**項目に入力する必要があります。

Extensionを審査する際に確認する評価項目は次のとおりです。

* Extensionのビルドの検証
  * Extensionがサービスに適切な用語を使用しているか確認します。
  * Intent、slotなどのinteraction modelを検証します。
  * Extensionの[詳細な目標](/Design/Design_Guideline_For_Extension.md#SettingGoal)に合ったサービスを提供しているか確認します。
* [使用シナリオ](/Design/Design_Guideline_For_Extension.md#MakeUseCaseScenarioScript)の検証
  * 会話のコンテクストに不自然なところがないか確認します。
  * シナリオで使用される発話データに、禁止用語や差別用語などが含まれていないか確認します。
  * Extensionが[ユーザーアカウントとリンク](/CEK/Guides/Link_User_Account.md)する場合、サービスに特化した部分をさらに検討することがあります。
* 配布情報の検証
  * Extensionの説明、カテゴリ、検索キーワードなどの配布情報が正しく入力されているか確認します。
  * Extensionがプライバシーポリシーなど、入力されたポリシーを遵守しているか確認します。

審査中に**{{ book.DevConsole.cek_cancel_review }}**メニューをクリックすると、いつでも審査のリクエストをキャンセルできます。審査のリクエストをキャンセルすると、前の状態に戻ります。

![](/DevConsole/Resources/Images/DevConsole-Cancel_Submission.png)

審査を通過しなかった場合、extensionの**{{ book.DevConsole.cek_status }}**が **{{ book.DevConsole.cek_status_rejected }}**に変更されます。これは**{{ book.DevConsole.cek_status_dev }}**と同じ状態で、再び審査をリクエストできます。

![](/DevConsole/Resources/Images/DevConsole-Extension_Submission_Rejected.png)

その際、**{{ book.DevConsole.cek_message }}**の**{{ book.DevConsole.cek_view }}**メニューをクリックすると、審査のフィードバックを確認できます。

![](/DevConsole/Resources/Images/DevConsole-Show_Submission_Feedback.png)
