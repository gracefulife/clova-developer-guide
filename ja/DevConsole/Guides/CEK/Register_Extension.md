# Extensionを登録する

[Custom Extension](/CEK/Guides/Build_Custom_Extension.md)または[Clova Home Extension](/CEK/Guides/Build_Clova_Home_Extension.md)を開発しているか、または開発済みの場合、そのExtensionをClova Developer Centerに登録する必要があります。CEKのメニューページで、ページの下にある**新規のExtensionを作成**ボタンをクリックすると、新規のExtensionを登録できます。

![](/DevConsole/Resources/Images/DevConsole-First_Look_of_Extension_List.png)

Extensionの登録は、通常、次の順で行われます。

<ol>
  <li><a href="#AgreeTermsOfUse">利用規約および個人情報の取得に同意する</a></li>
  <li><a href="#InputExtensionInfo">Extensionの基本情報を入力する</a></li>
  <li><a href="#SetServerConnection">サーバーとの連携を設定する</a>
    <ul>
      <li><a href="#SetAccountLinking">アカウントリンクを設定する</a></li>
    </ul>
  </li>
</ol>

## 利用規約および個人情報の取得に同意する {#AgreeTermsOfUse}

Extensionを登録するには、先にCEKのAPIサービスの利用規約と個人情報の取得に同意する必要があります。利用規約および個人情報の取得に関する内容は、最初の一度のみ表示され、同意した後は表示されません。

![](/DevConsole/Resources/Images/DevConsole-Agree_Terms_of_Use_and_Collecting_Personal_Info.png)

## Extensionの基本情報を入力する {#InputExtensionInfo}

Extensionを登録する最初のステップは、登録するExtensionの基本情報を入力することです。
Extensionの基本情報は、Clova Developer CenterでExtensionを作成するための最小限必要な情報です。Extensionの基本情報を入力すると、CEKメニューで、作成したExtensionに自由にアクセスし、また修正できるようになります。

次の順でExtensionを登録します。

![](/DevConsole/Resources/Images/DevConsole-Create_New_Extension.png)

<ol>
  <li><strong>{{ book.DevConsole.cek_type }}</strong>項目で、登録するExtensionのタイプを選択します。Extensionのタイプを選択すると、該当する入力フィールドが表示されます。</li>
  <li><strong>{{ book.DevConsole.cek_lang }}</strong>項目で、Extensionで使用する言語を選択します。現在、<strong>{{ book.DevConsole.ja_JP }}</strong>のみサポートされています。</li>
  <li>ExtensionのID、名前、呼び出し名を次の項目に入力します。
    <ol>
      <li><strong>{{ book.DevConsole.cek_id }}</strong>：Extensionの一意のIDです。リバースドメインネームの形式で入力します。(例：com.yourdomain.Extension.pizzabot)</li>
      <li><strong>{{ book.DevConsole.cek_name }}</strong>：Extensionの名前です。今後スキルストアで表示されます。</li>
      <li><strong>{{ book.DevConsole.cek_invocation_name }}</strong>：ユーザーがExtensionを呼び出す際に呼ぶ名前です。保有しているサービス、会社および組織の名前を使用できますが、ユーザーにとって呼びやすい、シンプルで独特な言葉を指定することをお勧めします。一般的に使われている言葉、他社の名前やサービスに該当する言葉は使用できません。<strong>{{ book.DevConsole.cek_invocation_name }}</strong>は、Extensionを審査する際にチェックされます。</li>
      <li><strong>{{ book.DevConsole.cek_provider }}</strong>：Extensionを作成した主体(会社や個人)の名前、またはニックネームを入力します。後ほどスキルストアで表示され、Extensionを審査する際にチェックされます。</li>
    </ol>
  </li>
  <li>Extensionが<a href="/CIC/References/CICInterface/AudioPlayer.html">AudioPlayer</a>ディレクティブを使用する場合、<strong>{{ book.DevConsole.cek_audioplayer }}</strong>項目で<strong>{{ book.DevConsole.cek_yes }}</strong>を選択します。Extensionがオーディオストリーミングサービスを提供する際に使用されます。</li>
  <li><strong>{{ book.DevConsole.cek_email }}</strong>項目に、連絡可能なメールアドレスを入力します。</li>
  <li><strong>{{ book.DevConsole.cek_tester }}</strong>項目に、Extensionのテストに使用する{{ book.OrientedService }}アカウントを入力します。必須ではなく、後ほど<a href="/DevConsole/Guides/CEK/Test_Extension.html">のExtensionをテスト</a>する際に入力することもできます。</li>
  <li>Extensionの基本情報をすべて入力して、<strong>{{ book.DevConsole.cek_create }}</strong>ボタンをクリックします。</li>
</ol>

Extensionの基本情報をすべて入力すると、作成されたExtensionの情報を修正する画面に切り替わります。ページの下にある**{{ book.DevConsole.cek_save }}**ボタンをクリックして、入力中の内容を自由に保存できます。また、CEKのメニューで、登録されたExtensionのリストを確認することもできます。

![](/DevConsole/Resources/Images/DevConsole-Extension_List_After_Creation.png)

## サーバーとの連携を設定する {#SetServerConnection}

ExtensionはCEKとHTTPSで通信します。その際、CEKはExtensionにHTTPリクエストを送り、ExtensionはCEKにHTTPレスポンスを返します。CEKがExtensionにHTTPリクエストを送るためには、Clova Developer Centerでサーバーとの連携を設定する必要があります。[Extensionの基本情報を入力](#InputExtensionInfo)すると、作成されたExtensionに対し、サーバーとの連携を設定できます。

Extensionのサーバーを登録するには、先にExtensionのサーバーと通信できるか確認する必要があります。次の例のように、簡単なcurlコマンドで通信状況を確認できます。

{% raw %}
```bash
$ curl "https://yourdomain.com/pizzabot" -X POST
```
{% endraw %}

次の順でサーバーとの連携を設定します。

![](/DevConsole/Resources/Images/DevConsole-Extension_Server_Settings.png)

<ol>
  <li>Extensionの情報入力UIで、上にある<strong>{{ book.DevConsole.cek_configuration }}</strong>タブをクリックします。</li>
  <li>ExtensionサーバーのURL(エンドポイント)を<strong>{{ book.DevConsole.cek_service_endpoint_url }}</strong>項目に入力します。
    <div class="note">
    <p><strong>メモ</strong></p>
    <p>テスト段階ではHTTPも使用できますが、正式なサービスのためにはHTTPSを使用する必要があります。Extensionのサーバーは、HTTPで80ポート、HTTPSで443ポートに設定してください。</p>
  </div>
  </li>
  <li>Extensionが提供するサービスのアカウントが、Clovaのユーザーアカウントとのリンクを必要とする場合、<strong>{{ book.DevConsole.cek_account_linking }}</strong>項目で<strong>{{ book.DevConsole.cek_yes }}</strong>を選択します。アカウントリンクの詳細については、<a href="#SetAccountLinking">アカウントリンクを設定する</a>を参照してください。</li>
  <li><strong>{{ book.DevConsole.cek_ssl_certificate }}</strong>項目のボタンをクリックします。Extensionを提供するサーバーは、必ず信頼された認証局から発行された証明書を使用しなければなりません。(自己署名証明書は使用できません)</li>
  <li>サーバーとの連携に関する内容を入力して、<strong>{{ book.DevConsole.cek_save }}</strong>ボタンをクリックします。</li>
</ol>

### アカウントリンクを設定する {#SetAccountLinking}

Extensionが提供するサービスのアカウントが、Clovaのユーザーアカウントとのリンクを必要とする場合、[サーバーとの連携を設定する](#SetServerConnection)の内、[アカウントリンク](/CEK/Guides/Link_User_Account.md)に関連情報を入力します。

次の順で、アカウントリンクの設定に[必要な情報](/CEK/Guides/Link_User_Account.md#RegisterAccountLinkingInfo)を入力します。

<ol>
  <img src="/DevConsole/Resources/Images/DevConsole-Extension_Accoun_Linking_Settings_1.png" />
  <li><strong>{{ book.DevConsole.cek_account_linking }}</strong>項目で<strong>{{ book.DevConsole.cek_yes }}</strong>を選択します。</li>
  <li>ユーザーにアカウント認証UIを提供する認証URLを、<strong>{{ book.DevConsole.cek_authorization_url }}</strong>項目に入力します。ユーザーがExtensionをアクティブにすると、このページに移動します。</li>
  <li>ユーザーが自身のアカウントを即座に設定できるようにする場合には、<strong>{{ book.DevConsole.cek_configuration_url }}</strong>項目にアカウント設定ページのURLを入力します。</li>
  <li>ユーザーアカウント認証を行う際、HTTPSリクエストに必要な<strong>{{ book.DevConsole.cek_client_id }}</strong>を入力します。クライアントIDは、<a href="/CEK/Guides/Link_User_Account.html#BuildAuthServer">認証サーバーを構築</a>する際に生成した値です。</li>
  <li><strong>{{ book.DevConsole.cek_privacy_policy_url }}</strong>項目に、Extensionが提供するサービスのプライバシーポリシーが提供されるURLを入力します。このページの内容は、後ほどストアで表示されます。</li>
  <li><strong>{{ book.DevConsole.cek_authorization_url }}</strong>または<strong>{{ book.DevConsole.cek_privacy_policy_url }}</strong>で提供するページが別のドメインから必要なリソースを読み込む場合、<strong>{{ book.DevConsole.cek_domain_list }}</strong>項目に必要なドメインを追加します。</li>
  <li>アカウントリンクの際に発行されるアクセストークンのスコープをあらかじめ定義している場合、<strong>{{ book.DevConsole.cek_scope }}</strong>項目に定義したスコープを追加します。</li>
  <img src="/DevConsole/Resources/Images/DevConsole-Extension_Accoun_Linking_Settings_2.png" />
  <li><strong>{{ book.DevConsole.cek_access_token_uri }}</strong>項目に、サービスのアクセストークンを発行できるURLを入力します。現在、<strong>許可付与タイプは許可コードのみサポート</strong>しています。</li>
  <li><strong>{{ book.DevConsole.cek_refresh_token_uri }}</strong>項目に、サービスのアクセストークンを更新できるURLを入力します。</li>
  <li>サービスのアクセストークンを取得した後、HTTPSリクエストの送信に必要な<strong>{{ book.DevConsole.cek_client_secret }}</strong>を入力します。クライアントシークレットは、<a href="/CEK/Guides/Link_User_Account.html#BuildAuthServer">認証サーバーを構築</a>する際に生成した値です。</li>
  <li><strong>{{ book.DevConsole.cek_client_authentication_scheme }}</strong>は、次のうち認証サーバーのインターフェースの実装に適した値を設定します。
    <ul>
      <li><strong>HTTPベーシック認証(推奨)</strong>：サービスのアクセストークンを取得するために、資格情報をヘッダーに入力される場合</li>
      <li><strong>リクエストボディーの資格情報</strong>：サービスのアクセストークンを取得するため、資格情報をボディーに入力される場合</li>
    </ul>
  </li>
</ol>

<div id="RedirectURI" class="note">
  <p><strong>メモ</strong></p>
  <p>アカウント認証を済ませた後、クライアントがリダイレクトされるURLは<code>{{ book.RedirectURLforAccountLinking }}</code>で、<strong>{{ book.DevConsole.cek_redirect_urls }}</strong>項目で確認できます。</strong></p>
  <img src="/DevConsole/Resources/Images/DevConsole-Redirect_URL_for_Extension_Accoun_Linking.png" />
</div>
