## CICに接続する {#ConnectToCIC}
クライアントがCICに接続するには、次の作業が必要です。
* [Clovaアクセストークンを作成する](#CreateClovaAccessToken)
* [接続を作成する](#CreateConnection)
* [認証する](#Authorization)
* [接続を管理する](#ManageConnection)

### Clovaアクセストークンを作成する {#CreateClovaAccessToken}
ユーザーがClovaを使用するには、{{ book.TargetServiceForClientAuth }}アカウントをクライアントデバイスまたはアプリで認証する必要があります。クライアントは、{{ book.TargetServiceForClientAuth }}アカウント認証情報まで処理されたClovaアクセストークンをClova認可サーバーから取得後、CICに接続してリクエストを送ることができるようになります。その際、[Clova認証API](/CIC/References/Clova_Auth_API.md)を使用します。

以下の図は、クライアントがClovaアクセストークンを取得するための流れを示しています。ちなみに、クライアントは2つのタイプがあり、タイプによってClovaアクセストークンを取得する方法が少し異なります。
* **GUIを提供しないクライアント**：画面を持たないスピーカーや家電製品に埋め込まれた形で、Clovaサービスを提供するクライアントです。このタイプのクライアントは、ユーザーがアカウントを認証する際、デバイスから認証情報を入力することが容易ではありません。そのため、コンパニオンアプリを提供するか、Clovaアプリと連携する必要があります。
* **GUIを提供するクライアント**：画面を持つデバイスに埋め込まれた形でClovaサービスを提供するクライアント、またはClovaアプリのように、ソフトウェアの形でClovaサービスを提供するクライアントです。

![](/CIC/Resources/Images/CIC_Authorization.png)

Clovaアクセストークンは、次の順で取得できます。

<ol>
  <li>
    <p>クライアントは、ユーザーが{{ book.TargetServiceForClientAuth }}アカウントを認証できるインターフェースを提供します(<a href="{{ book.LoginAPIofTargetService }}" target="_blank">{{ book.TargetServiceForClientAuth }}IDでログインする</a>)。<strong>GUIを提供しないクライアント</strong>は、ユーザーの音声入力だけではアカウントを認証できないため、必ずClovaアプリまたはコンパニオンアプリを使用する必要があります。</p>
  </li>
  <li>
    <p>ユーザーが入力した{{ book.TargetServiceForClientAuth }}アカウント情報を使って、{{ book.TargetServiceForClientAuth }}アカウントの{{ "authorization code" if book.TargetCountryCode == "JP" else "access token" }}を取得します。.</p>
  </li>
  <li>
    <p>取得した{{ book.TargetServiceForClientAuth }}アカウントの{{ "authorization code" if book.TargetCountryCode == "JP" else "access token" }}と<a href="#ClientAuthInfo">クライアント認証情報</a>を使って、<a href="/CIC/References/Clova_Auth_API.html#RequestAuthorizationCode">認可コードをリクエスト</a>します。その際、<code>device_id</code>フィールドの値は、クライアントのMACアドレスを使用するか、またはUUIDのハッシュ値を作成して使用します。次は、認可コードをリクエストするサンプルです。</p>
    <pre><code>$ curl -H "Authorization: Bearer QHSDAKLFJASlk12jlkf+asldkjasdf=sldkjf123dsalsdflkvpasdFMrjvi23scjaf123klv"
    {{ book.AuthServerBaseURL }}authorize \
    --data-urlencode "client_id=c2Rmc2Rmc2FkZ2Fasdkjh234zZnNhZGZ" \
    --data-urlencode "device_id=aa123123d6-d900-48a1-b73b-aa6c156353206" \
    --data-urlencode "model_id=test_model" \
    --data-urlencode "response_type=code" \
    --data-urlencode "state=FKjaJfMlakjdfTVbES5ccZ"
</code></pre>
    <p>受信するレスポンスメッセージのボディは、次の通りです。<code>code</code>フィールドが認可コードです。</p>
    <pre><code>{
  "code": "cnl__eCSTdsdlkjfweyuxXvnlA",
  "state": "FKjaJfMlakjdfTVbES5ccZ"
}
</code></pre></li>
  <li>
    <p>もし、<a href="/CIC/References/Clova_Auth_API.html#RequestAuthorizationCode">認可コードのリクエスト</a>に対するレスポンスとして、<code>451 Unavailable For Legal Reasons</code>ステータスコードを受信した場合、レスポンスメッセージボディの<code>redirect_uri</code>フィールドに記載されているURIを使用して、ユーザーに利用規約への同意ページを表示する必要があります。次は、ステータスコードが<code>451 Unavailable For Legal Reasons</code>の場合、受信するレスポンスメッセージボディのサンプルです。</p>
    <pre><code>{
  "code": "4mrklvwoC_KNgDlvmslka",
  "redirect_uri": "https://ssl.pstatic.net/static/clova/service/terms/place/terms_3rd.html?code=4mrklvwoC_KNgDlvmslka&grant_type=code&state=FKjaJfMlakjdfTVbES5ccZ",
  "state": "FKjaJfMlakjdfTVbES5ccZ"
}
</code></pre>
    <p>ちなみに、ユーザーが利用規約に同意しない場合、Clovaアクセストークンの発行をリクエストできません。ユーザーが利用規約に同意し、その結果をサーバーに送信すると、クライアントは<code>302 Found</code>(URL Redirection)ステータスコードを含むレスポンスと次のURLを受信します。</p>
    <ul>
      <li><code>clova://agreement-success</code>：利用規約への同意に成功。クライアントは、続けてClovaアクセストークンの発行をリクエストすることができます。</li>
      <li><code>clova://agreement-failure</code>：サーバーのエラーにより、利用規約への同意に失敗。クライアントは、適切な例外処理をする必要があります。</li>
    </ul>
  </li>
  <li>
    <p>GUIを提供しないクライアントの場合、認可コードを実際のクライアントデバイスに送信します。</p>
  </li>
  <li>
    <p>取得した認可コードと<a href="#ClientAuthInfo">クライアント認証情報</a>をパラメータに入力し、<a href="/CIC/References/Clova_Auth_API.html#RequestClovaAccessToken">Clovaアクセストークンをリクエスト</a>します。次は、Clovaアクセストークンをリクエストするサンプルです。</p>
    <pre><code>$ curl {{ book.AuthServerBaseURL }}token?grant_type=authorization_code \
    --data-urlencode "client_id=c2Rmc2Rmc2FkZ2Fasdkjh234zZnNhZGZ" \
    --data-urlencode "client_secret=66qo65asdfasdfaA7JasdfasfOqwnOq1rOyfgeydtCDrvYasfasf%3D" \
    --data-urlencode "code=cnl__eCSTdsdlkjfweyuxXvnlA" \
    --data-urlencode "device_id=aa123123d6-d900-48a1-b73b-aa6c156353206" \
    --data-urlencode "model_id=test_model"
</code></pre>
    <p>次のようなClovaアクセストークンが返されます。</p>
    <pre><code>{
    "access_token": "XHapQasdfsdfFsdfasdflQQ7w",
    "expires_in": 332000,
    "refresh_token": "GW-Ipsdfasdfdfs3IbHFBA",
    "token_type": "Bearer"
}
</code></pre>
  </li>
</ol>

### CICに接続する {#CreateConnection}
クライアントが最初にCICに接続する際、[ダウンチャネルを構成する](/CIC/References/CIC_API.md#EstablishDownchannel)必要があります。ダウンチャネルは、CICからディレクティブを受信する際に使用されます。その際、受信するディレクティブは、クライアントのイベントに対するレスポンスとしてのものではなく、特定の条件や必要に応じて、CICで開始され(Cloud-initiated)、クライアントに送信されるディレクティブです。例えば、新しい通知(push)が届いた場合、ダウンチャネルでディレクティブが送信されます。

ダウンチャネルは、`/v1/directives`に`GET`リクエストを送信して構成することができます。一度構成すると、CICによって接続が維持されます。

{% raw %}

```
:method: GET
:scheme: https
:path: /v1/directives
User-Agent: {{User-Agent_string}}
Authorization: Bearer {{ClovaAccessToken}}
```

{% endraw %}

上記の接続リクエストの処理が成功すると、CICは次のような[`Clova.Hello`](/CIC/References/CICInterface/Clova.md#Hello)ディレクティブをレスポンスとして送信します。それは、ダウンチャネルで追加のディレクティブを送信する準備ができたことを示します。

{% raw %}

```
{
    "directive": {
        "header": {
            "messageId": "2ca2ec70-c39d-4741-8a34-8aedd3b24760",
            "namespace": "Clova",
            "name": "Hello"
        },
        "payload": {}
    }
}
```

{% endraw %}

<div class="note">
  <p><strong>メモ</strong></p>
  <ul>
    <li>クライアントは、CICと常時1つのダウンチャネルを維持する必要があります。もし、すでにダウンチャネルが構成された状態で、<code>/v1/directives</code>にダウンチャネル構成のリクエストが追加で送信されると、前のダウンチャネルは解除されます。</li>
    <li>ヘッダーに含まれるUser-Agentフィールドについての詳細は、<a href="#UserAgentString">User-Agent文字列</a>を参照してください。</li>
    <li>ヘッダーに含まれるAuthorizationフィールドについての詳細は、<a href="#Authorization">認証する</a>を参照してください。</li>
  </ul>
</div>

<div class="danger">
  <p><strong>注意</strong></p>
  <p>ダウンチャネルを構成しないと、CICに<a href="#SendEvent">イベントを送信する</a>ことができません。</p>
</div>

### 認証する {#Authorization}
クライアントがCICにリクエストを送る際、[Clovaアクセストークン](#CreateClovaAccessToken)を含める必要があります。次のように、ヘッダーのAuthorizationフィールドにClovaアクセストークンのタイプと値をスペースで区切って入力します。詳細については、[CIC API](/CIC/References/CIC_API.md)を参照してください。

{% raw %}

```
:method: {{GET|POST}}
:scheme: https
:path: {{/v1/events|/v1/directives}}
User-Agent: {{User-Agent_string}}
Authorization: Bearer {{ClovaAccessToken}}
```

{% endraw %}

次の図のように、クライアントは新しいリクエスト(イベント)を送信する度に、Clovaアクセストークンを含める必要があります。

![](/CIC/Resources/Images/CIC_Message_Interaction_Diagram.png)

### 接続を管理する {#ManageConnection}

クライアントとCICの間で接続が構成されると、クライアントは次の項目を管理する必要があります。

* [ダウンチャネルを維持する](#KeepDownchannel)
* [Pingを打つ](#DoPingpong)
* [アクセストークンを更新する](#RefreshAccessToken)

#### ダウンチャネルを維持する {#KeepDownchannel}
ダウンチャネルの接続が終了したり切断された場合、クライアントはすぐに新しい[ダウンチャネルを構成](#CreateConnection)して、CICから送信されるディレクティブを必ず受信できるようにする必要があります。

#### Pingを打つ {#DoPingpong}

CICとの接続状況を確認するために、クライアントは1分ごとにHTTP/2 PINGフレームをCICに送信する必要があります。CICからHTTP/2 PING ACKのレスポンスを受信しなかった場合、クライアントはすぐに新しい接続を構成して、クライアントとCICの接続を維持する必要があります。HTTP/2 PINGフレームについての詳細は、[HTTP/2 PING Payload Format](https://http2.github.io/http2-spec/#rfc.figure.12)を参照してください。

<div class="note">
  <p><strong>メモ</strong></p>
  <p>HTTP/2 PINGフレームを送信できない場合、クライアントは1分ごとに<code>GET</code>リクエストを<code>/ping</code>に対して送信する必要があります。すると、HTTP 204 No Contentのレスポンスを受信します。HTTP/2 PINGフレームのときと同じく、応答を受信しなかった場合、クライアントはすぐに新しい接続を構成する必要があります。</p>
  <p>次は、<code>/ping</code>に<code>GET</code>リクエストを送信するコードサンプルです。</p>
  <pre><code>:method = GET
:scheme = https
:path = /ping
User-Agent: [User-Agent_string]
Authorization: Bearer [YOUR_ACCESS_TOKEN]
</code></pre>
</div>

#### アクセストークンを更新する {#RefreshAccessToken}

クライアントは、アクセストークンを取得する際、`expires_in`フィールドから、そのアクセストークンがいつ期限切れになるのかを確認できます。期限が超過したり期限切れになったアクセストークンを使って、HTTP 401 Unauthorizedステータスコードが含まれた[エラーメッセージ](/CIC/References/CIC_API.md#Error)を受信した場合、アクセストークンを更新する必要があります。次のように、[Clovaアクセストークンを取得](/CIC/References/Clova_Auth_API.md#RequestClovaAccessToken)する際に受け取ったリフレッシュトークン(`refresh_token`)と、必要なパラメータを送信すると、[Clovaアクセストークンを更新](/CIC/References/Clova_Auth_API.md#RefreshClovaAccessToken)することができます。

<pre><code>$ curl {{ book.AuthServerBaseURL }}token?grant_type=refresh_token \
       --data-urlencode "client_id=c2Rmc2Rmc2FkZ2FzZnNhZGZ" \
       --data-urlencode "client_secret=66qo65asdfasdfaA7JasdfasfOqwnOq1rOyfgeydtCDrvYasfasf%3D" \
       --data-urlencode "refresh_token=GW-Ipsdfasdfdfs3IbHFBA" \
       --data-urlencode "device_id=aa123123d6-d900-48a1-b73b-aa6c156353206" \
       --data-urlencode "model_id=test_model"
</code></pre>
