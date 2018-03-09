対話モデルが正しく動作することを確認したら、審査をリクエストする前に、実際のデバイスでテストして、音声の認識と応答が想定した通りに動作するか確認する必要があります。

### テスターIDを登録する
特定のアカウントでのみ、このExtensionを実行できるように、テスターIDを登録します。

1. <a href="{{ book.DeveloperConsoleURL }}" target="_blank">Clova Developer Center</a>に接続します。
2. サンプルサイコロの**{{ book.DevConsole.cek_skill_info }}**項目の**{{ book.DevConsole.cek_edit }}**ボタンをクリックします。
3. 表示された画面の**{{ book.DevConsole.cek_tester }}**項目に、あなたの{{ book.OrientedService }}アカウントIDを入力します。
4. **{{ book.DevConsole.cek_save }}**ボタンをクリックします。

<div class="note">
  <p><strong>メモ</strong></p>
  <p>テスターIDを登録してしばらく待つと、Extensionをテストできるようになります。もし1時間以上経ってもExtensionをテストできない場合には、フォーラムまたは提携担当者までお問い合わせください。</p>
</div>

<div class="danger">
<p><strong>注意</strong></p>
  <p>実際のデバイスでテストするには、<strong>{{ book.DevConsole.cek_skill_info }}</strong>に外部からアクセスできる実際のExtensionサーバーのURLを必ず登録する必要があります。</p></li>
</div>

### Clovaアプリで実行する
ClovaアプリでサンプルサイコロExtensionを実行します。

1. テストするデバイスにClovaアプリをインストールします。
2. テスターIDとして入力した{{ book.OrientedService }}アカウントでログインします。
3. テスト用のExtensionの呼び出し名で、音声指示を出します。例えば、「クローバー、サンプルサイコロにサイコロを振らせて」と指示します。
4. Clovaアプリが「サイコロを1つ振ります」と応答するか確認します。

Extensionが実際のデバイスでも正しく動作したら、サービスの準備は完了です。Clova Developer Centerで審査をリクエストして、Extensionを配布することができます。
