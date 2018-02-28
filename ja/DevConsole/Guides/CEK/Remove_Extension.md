# Extensionを中止および削除する

審査をリクエストする前のExtensionは、[Extensionの基本情報を入力](/DevConsole/Guides/CEK/Register_Extension.md#InputExtensionInfo)するページでそのExtensionを削除できます。

![](/DevConsole/Resources/Images/DevConsole-Remove_Extension.png)

ただし、下記の状態にあるExtensionは削除できません。

* Extensionが審査を受けている場合
* Extensionがサービス中の場合

Extensionが審査中の場合、審査をキャンセルして、自由にExtensionを削除できます。

![](/DevConsole/Resources/Images/DevConsole-Cancel_Submission.png)

もし、Extensionが審査を通過し、サービスが開始されている場合には、サービスをいったん中止してからExtensionを削除できます。サービスを中止すると、Extensionは**{{ book.DevConsole.cek_status_dev }}**状態に戻ります。

<div class="note">
  <p><strong>メモ</strong></p>
  <p>サービスを中止する際には、Clova運営チームの確認が必要です。Extensionを中止するには、<a href="mailto://dl_Extension_admin@navercorp.com">dl_Extension_admin@navercorp.com</a>まで連絡してください。</p>
</div>
