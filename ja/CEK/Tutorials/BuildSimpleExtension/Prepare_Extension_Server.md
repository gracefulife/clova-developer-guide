Extensionサーバーは、Clovaと通信してユーザーのインテントを処理するREST APIサーバーです。Extensionをサービスするためには必ず必要です。

Extensionサーバーを構築するには、HTTPを使用してメッセージをやり取りするコードを作成する必要があります。
ここでは、できるだけ短時間でExtensionを作成してみるために、直接サーバーを構築せず、すでに作成されたExtensionをを使用します。

Clovaがサービスする「サイコロ遊び」というExtensionは、そのソースコードが公開されています。
ソースコードをダウンロードして実行するには、次の項目が必要です。

| 項目     | 説明                               | 必須/選択 |
|---------|-----------------------------------|:-------:|
| <a href="https://git-scm.com/" target="_blank">git</a>    | ソースコードをダウンロードするために必要です。          | 選択     |
| <a href="https://nodejs.org/" target="_blank">node.js</a> | Extensionサーバーを実行するために必要です。          | 必須     |
| <a href="https://chrome.google.com/webstore/detail/postman/fhbjgbiflinjbdggehcddcbncdddomop" target="_blank">Google Chrome拡張機能「Postman - REST Client」</a> | Extensionサーバーが動作しているか確認するために必要です。 | 選択     |

必要なソフトウェアをインストールして、次のようにサイコロ遊びExtensionのソースコードをダウンロードし、実行します。`tutorial1`ブランチを使用します。

```bash
git clone {{ book.GitHubBaseURLforExtensionExample }}/clova-extension-sample-dice.git
cd clova-extension-sample-dice
git checkout tutorial1
npm install
node app.js
```

こうやって実行したExtensionサーバーが正しく動作しているか確認するには、Postmanを使用してリクエストを送信します。詳細については、<a href="{{ GitHubBaseURLforExtensionExample }}/clova-extension-sample-dice" target="_blank">サイコロ遊びExtensionのgithubページ</a>で確認できます。

上記どおりに正しく実行されることを確認したら、外部からアクセスできるサーバーに移して実行します。
