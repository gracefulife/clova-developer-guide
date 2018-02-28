# Extensionを中止および削除する

審査をリクエストする前のextensionは、[Extensionの基本情報を入力](/DevConsole/Guides/CEK/Register_Extension.md#InputExtensionInfo)するページでそのextensionを削除できます。

![](/DevConsole/Resources/Images/DevConsole-Remove_Extension.png)

ただし、下記の状態にあるextensionは削除できません。

* Extensionが審査を受けている場合
* Extensionがサービス中の場合

Extensionが審査中の場合、審査をキャンセルして、自由にextensionを削除できます。

![](/DevConsole/Resources/Images/DevConsole-Cancel_Submission.png)

もし、extensionが審査を通過し、サービスが開始されている場合には、サービスをいったん中止してからextensionを削除できます。サービスを中止すると、extensionは**{{ book.DevConsole.cek_status_dev }}**状態に戻ります。

<div class="note">
  <p><strong>メモ</strong></p>
  <p>サービスを中止する際には、Clova運営チームの確認が必要です。Extensionを中止するには、<a href="mailto://dl_extension_admin@navercorp.com">dl_extension_admin@navercorp.com</a>まで連絡してください。</p>
</div>
