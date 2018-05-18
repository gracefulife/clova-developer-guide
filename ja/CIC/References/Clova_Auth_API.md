# Clova認証APIのリファレンス
クライアントがCICに接続するには、[Clovaアクセストークンを作成する](/CIC/Guides/Interact_with_CIC.md#CreateClovaAccessToken)必要があります。Clova認可サーバーは、Clovaアクセストークンの作成および管理に必要なClova認証APIを提供しています。ここでは、Clova認証APIについて説明しています。

## Base URL
Clova認可サーバーのベースURLは、次の通りです。

<pre><code>{{ book.AuthServerBaseURL }}
</code></pre>

## 認可コードをリクエストする {#RequestAuthorizationCode}

```
GET|POST /authorize
```

{{ book.TargetServiceForClientAuth }}アカウントのアクセストークンおよび[クライアント認証情報](/CIC/Guides/Interact_with_CIC.md#ClientAuthInfo)などをパラメーターに渡して、認可コードをリクエストします。認可コードは、Clovaアクセストークンを取得する際に使用されます。

通常、ユーザー認証は、クライアントデバイスとペアリングされたアプリで行われます。ですが、ペアリングされたアプリからクライアントにClovaアクセストークンを送信するのはセキュリティ上の問題があるため、代わりにこのコードをクライアントに渡します。クライアントは、渡された認可コードをClova認可サーバーに送信して、[Clovaアクセストークンをリクエスト](#RequestClovaAccessToken)します。

### Request header

| リクエストヘッダー | 説明                                                                |
|----------------|--------------------------------------------------------------------|
| Accept         | <p>次の値を入力します。</p><p><pre><code>application/json</code></pre></p>  |
| Authorization  | <p><a href="/CIC/Guides/Interact_with_CIC.html#CreateClovaAccessToken">取得した{{ book.TargetServiceForClientAuth }}アクセストークン</a>を入力します：</p><p><pre><code>Bearer [{{ book.TargetServiceForClientAuth }} access token]</code></pre></p>  |

### Query parameter

| フィールド名       | データ型    | 説明                     | 必須/任意 |
|---------------|---------|-----------------------------|:---------:|
| `client_id`     | string  | クライアントID([クライアント認証情報](/CIC/Guides/Interact_with_CIC.md#ClientAuthInfo)を参照)          | 必須 |
| `device_id`     | string  | クライアントデバイスのMACアドレスまたは生成したUUID                                                              | 必須 |
| `model_id`      | string  | クライアントデバイスのモデルID                                                                          | 選択 |
| `response_type` | string  | 応答タイプ現在、`"code"`のみサポートされています。                                                             | 必須 |
| `state`         | string  | クロスサイトリクエストフォージェリ(cross-site request forgery)攻撃を防ぐために、クライアントによって使用される状態トークンの値(URLエンコーディングを使用する) | 必須 |

### Request example

<pre><code>$ curl -H "Authorization: Bearer QHSDAKLFJASlk12jlkf+asldkjasdf=sldkjf123dsalsdflkvpasdFMrjvi23scjaf123klv"
       {{ book.AuthServerBaseURL }}authorize \
       --data-urlencode "client_id=c2Rmc2Rmc2FkZ2Fasdkjh234zZnNhZGZ" \
       --data-urlencode "device_id=aa123123d6-d900-48a1-b73b-aa6c156353206" \
       --data-urlencode "model_id=test_model" \
       --data-urlencode "response_type=code" \
       --data-urlencode "state=FKjaJfMlakjdfTVbES5ccZ"
</code></pre>

### Response header

| レスポンスヘッダー | 説明                                                                |
|-----------------|--------------------------------------------------------------------|
| Content-Type    | <p>次の値が含まれます。</p><p><pre><code>application/json</code></pre></p>                   |

### Response JSON object fields

| フィールド名       | データ型    | 説明                     | 包含 |
|---------------|---------|-----------------------------|:---------:|
| `code`          | string | 認可サーバーから取得した認可コード。HTTPレスポンスメッセージが`200`または`451`のステータスコードを持つ場合、HTTPレスポンスのボディーに含まれています。      | 常時      |
| `redirect_uri`  | string | サービスの利用規約を提供するページのURI。HTTPレスポンスメッセージが`451 Unavailable For Legal Reasons`のステータスコードを持つ場合、HTTPレスポンスメッセージのボディに含まれています。クライアントは、このフィールドに含まれたURIにリダイレクトして、ページを表示する必要があります。ユーザーが利用規約に同意すると、クライアントは、`302 Found`(URL redirection)のステータスコードを持つレスポンスを、次のURLと共に受信します。<ul><li><code>clova://agreement-success</code>：ユーザーが利用規約に同意した場合。クライアントは、Clovaアクセストークンを取得するために、次のステップに進みます。</li><li><code>clova://agreement-failure</code>：サーバーのエラーにより、利用規約に同意できなかった場合。クライアントは、適切な例外処理をする必要があります。</li></ul> | 常時      |
| `state`         | string | クロスサイトリクエストフォージェリ(cross-site request forgery)攻撃を防ぐために、クライアントから受け取った状態のトークンを復号化した値(URLデコーディングを適用)。HTTPレスポンスメッセージが`200`または`451`のステータスコードを持つ場合、HTTPレスポンスのボディーに含まれています。 | 常時      |

### Status codes

| ステータスコード       | 説明                     |
|---------------|-------------------------|
| 200 OK           | リクエスト成功を示します。                      |
| 400 Bad Request  | `client_id`など、必須パラメーターを入力しなかったか、パラメーターに無効なデータを入力したことを示します。 |
| 403 Forbidden    | ヘッダーに含まれた{{ book.TargetServiceForClientAuth }}アクセストークンが無効なことを示します。 |
| 451 Unavailable For Legal Reasons | ユーザーが利用規約に同意しなかったことを示します。クライアントはこのレスポンスを受信すると、`redirect_uri`フィールド内のURIにリダイレクトする必要があります。リダイレクトするURIは、ユーザーに利用規約への同意を求めるページです。  |
| 500 Server Internal Error | サーバー内部にエラーが発生し、認可コードを取得できなかったことを示します。 |

### Response example

{% raw %}

```json
//サンプル1：HTTPレスポンスメッセージが200 OKのステータスコードを持つ場合
{
    "code": "cnl__eCSTdsdlkjfweyuxXvnlA",
    "state": "FKjaJfMlakjdfTVbES5ccZ"
}

//サンプル2：HTTPレスポンスメッセージが451 Unavailable For Legal Reasonsのステータスコードを持つ場合
{
  "code":"4mrklvwoC_KNgDlvmslka",
  "redirect_uri":"https://ssl.pstatic.net/static/clova/service/terms/place/terms_3rd.html?code=4mrklvwoC_KNgDlvmslka&grant_type=code&state=FKjaJfMlakjdfTVbES5ccZ",
  "state":"FKjaJfMlakjdfTVbES5ccZ"
}
```

{% endraw %}

{% include "/CIC/References/CICAuthAPI/Guest_Mode.md" %}

### 次の項目も参照してください。
* [クライアント認証情報](/CIC/Guides/Interact_with_CIC.md#ClientAuthInfo)
* [Clovaアクセストークンを作成する](/CIC/Guides/Interact_with_CIC.md#CreateClovaAccessToken)
* [Clovaアクセストークンをリクエストする](#RequestClovaAccessToken)


## Clovaアクセストークンをリクエストする {#RequestClovaAccessToken}

```
GET|POST /token?grant_type=authorization_code
```

[取得した認可コード](#RequestAuthorizationCode)を使って、Clova認可サーバーにClovaアクセストークンをリクエストします。

### Request header

| リクエストヘッダー | 説明                                                                |
|----------------|--------------------------------------------------------------------|
| Accept         | <p>次の値を入力します。</p><p><pre><code>application/json</code></pre></p>                   |

### Query parameter

| フィールド名       | データ型    | 説明                     | 必須/任意 |
|---------------|---------|-----------------------------|:---------:|
| `client_id`     | string  | クライアントID([クライアント認証情報](/CIC/Guides/Interact_with_CIC.md#ClientAuthInfo)を参照)                                  | 必須 |
| `client_secret` | string  | クライアントシークレット([クライアント認証情報](/CIC/Guides/Interact_with_CIC.md#ClientAuthInfo)を参照)                              | 必須 |
| `code`          | string  | [取得した認可コード](#RequestAuthorizationCode)                                                               | 必須 |
| `device_id`     | string  | クライアントデバイスのMACアドレスまたは生成したUUID                                                                                     | 必須 |
| `model_id`      | string  | クライアントデバイスのモデルID                                                                                                 | 選択 |

### Request example

<pre><code>$ curl {{ book.AuthServerBaseURL }}token?grant_type=authorization_code \
       --data-urlencode "client_id=c2Rmc2Rmc2FkZ2Fasdkjh234zZnNhZGZ" \
       --data-urlencode "client_secret=66qo65asdfasdfaA7JasdfasfOqwnOq1rOyfgeydtCDrvYasfasf%3D" \
       --data-urlencode "code=cnl__eCSTdsdlkjfweyuxXvnlA" \
       --data-urlencode "device_id=aa123123d6-d900-48a1-b73b-aa6c156353206" \
       --data-urlencode "model_id=test_model"
</code></pre>

### Response header

| レスポンスヘッダー | 説明                                                                |
|-----------------|--------------------------------------------------------------------|
| Content-Type    | <p>次の値が含まれます。</p><p><pre><code>application/json</code></pre></p>                   |

### Response JSON object fields

| フィールド名       | データ型    | 説明                     | 包含 |
|---------------|---------|-----------------------------|:---------:|
| `access_token`  | string  | Clovaアクセストークン                               | 常時      |
| `expires_in`    | number  | Clovaアクセストークンの有効期限(秒単位)              | 常時      |
| `refresh_token` | string  | Clovaアクセストークンを更新するためのリフレッシュトークン     | 常時      |
| `token_type`    | string  | Clovaアクセストークンのタイプ。「Bearer」で固定されています。 | 常時      |

### Status codes

| ステータスコード       | 説明                     |
|---------------|-------------------------|
| 200 OK        | リクエスト成功を示します。                                                                                   |
| 400 Bad Request  | `client_id`など、必須パラメーターを入力しなかったか、パラメーターに無効なデータを入力したことを示します。 |
| 500 Internal Server Error | サーバー内部にエラーが発生し、アクセストークンを取得できなかったことを示します。                                             |

### Response example
{% raw %}
```json
{
    "access_token": "XHapQasdfsdfFsdfasdflQQ7w",
    "expires_in": 332000,
    "refresh_token": "GW-Ipsdfasdfdfs3IbHFBA",
    "token_type": "Bearer"
}
```
{% endraw %}

### 次の項目も参照してください。
* [クライアント認証情報](/CIC/Guides/Interact_with_CIC.md#ClientAuthInfo)
* [Clovaアクセストークンを作成する](/CIC/Guides/Interact_with_CIC.md#CreateClovaAccessToken)
* [認可コードをリクエストする](#RequestAuthorizationCode)


## Clovaアクセストークンを更新する {#RefreshClovaAccessToken}

```
GET|POST /token?grant_type=refresh_token
```

取得したリフレッシュトークンを使って、Clovaアクセストークンを更新します。

### Request header

| リクエストヘッダー | 説明                                                                |
|----------------|--------------------------------------------------------------------|
| Accept         | <p>次の値を入力します。</p><p><pre><code>application/json</code></pre></p>                   |

### Query parameter

| フィールド名       | データ型    | 説明                     | 必須/任意 |
|---------------|---------|-----------------------------|:---------:|
| `client_id`     | string  | クライアントID([クライアント認証情報](/CIC/Guides/Interact_with_CIC.md#ClientAuthInfo)を参照)                                  | 必須 |
| `client_secret` | string  | クライアントシークレット([クライアント認証情報](/CIC/Guides/Interact_with_CIC.md#ClientAuthInfo)を参照)                              | 必須 |
| `device_id`     | string  | クライアントデバイスのMACアドレスまたは生成したUUID                                            | 選択 |
| `model_id`      | string  | クライアントデバイスのモデル                                                           | 選択 |
| `refresh_token` | string  | 認証に成功して取得したリフレッシュトークン                                              | 必須 |

### Request example

<pre><code>$ curl {{ book.AuthServerBaseURL }}token?grant_type=refresh_token \
       --data-urlencode "client_id=c2Rmc2Rmc2FkZ2FzZnNhZGZ" \
       --data-urlencode "client_secret=66qo65asdfasdfaA7JasdfasfOqwnOq1rOyfgeydtCDrvYasfasf%3D" \
       --data-urlencode "refresh_token=GW-Ipsdfasdfdfs3IbHFBA" \
       --data-urlencode "device_id=aa123123d6-d900-48a1-b73b-aa6c156353206" \
       --data-urlencode "model_id=test_model"
</code></pre>

### Response header

| レスポンスヘッダー | 説明                                                                |
|-----------------|--------------------------------------------------------------------|
| Content-Type    | <p>次の値が含まれます。</p><p><pre><code>application/json</code></pre></p>                   |

### Response JSON object fields

| フィールド名       | データ型    | 説明                     | 包含 |
|---------------|---------|-----------------------------|:---------:|
| `access_token`  | string  | Clovaアクセストークン                               | 常時      |
| `expires_in`    | number  | Clovaアクセストークンの有効期限(秒単位)              | 常時      |
| `refresh_token` | string  | Clovaアクセストークンを更新するためのリフレッシュトークン     | 常時      |
| `token_type`    | string  | Clovaアクセストークンのタイプ。「Bearer」で固定されています。 | 常時      |

### Status codes

| ステータスコード       | 説明                     |
|---------------|-------------------------|
| 200 OK                    | リクエスト成功を示します。                                                                                |
| 400 Bad Request           | `client_id`など、必須パラメーターを入力しなかったか、パラメーターに無効なデータを入力したことを示します。 |
| 500 Internal Server Error | サーバー内部にエラーが発生し、アクセストークンを更新できなかったことを示します。                                                      |

### Response example
{% raw %}
```json
{
    "access_token": "xFcH08vYQcahQWouqIzWOw",
    "expires_in": 12960000,
    "refresh_token": "drJK-soIQI6vqEukqsLU2g",
    "token_type": "Bearer"
}
```
{% endraw %}

### 次の項目も参照してください。
* [クライアント認証情報](/CIC/Guides/Interact_with_CIC.md#ClientAuthInfo)
* [Clovaアクセストークンをリクエストする](#RequestClovaAccessToken)


## Clovaアクセストークンを削除する {#DeleteClovaAccessToken}

```
GET|POST /token?grant_type=delete
```

[取得したClovaアクセストークン](#RequestClovaAccessToken)を削除します。削除したClovaアクセストークンの情報がレスポンスとして返されます。

### Request header

| リクエストヘッダー | 説明                                                                |
|----------------|--------------------------------------------------------------------|
| Accept         | <p>次の値を入力します。</p><p><pre><code>application/json</code></pre></p>                   |

### Query parameter

| フィールド名       | データ型    | 説明                     | 必須/任意 |
|---------------|---------|-----------------------------|:---------:|
| `access_token`  | string  | 認証に成功して取得したClovaアクセストークン                                                                                 | 必須 |
| `client_id`     | string  | クライアントID([クライアント認証情報](/CIC/Guides/Interact_with_CIC.md#ClientAuthInfo)を参照)                                  | 必須 |
| `client_secret` | string  | クライアントシークレット([クライアント認証情報](/CIC/Guides/Interact_with_CIC.md#ClientAuthInfo)を参照)                              | 必須 |
| `device_id`     | string  | クライアントデバイスのMACアドレスまたは生成したUUID                                            | 必須 |
| `model_id`      | string  | クライアントデバイスのモデル                                                           | 選択 |

### Request example

<pre><code>$ curl {{ book.AuthServerBaseURL }}token?grant_type=delete \
       --data-urlencode "access_token=xFcH08vYQcahQWouqIzWOw" \
       --data-urlencode "client_id=c2Rmc2Rmc2FkZ2Fasdkjh234zZnNhZGZ" \
       --data-urlencode "client_secret=66qo65asdfasdfaA7JasdfasfOqwnOq1rOyfgeydtCDrvYasfasf%3D" \
       --data-urlencode "device_id=aa123123d6-d900-48a1-b73b-aa6c156353206" \
       --data-urlencode "model_id=test_model"
</code></pre>

### Response header

| レスポンスヘッダー | 説明                                                                |
|-----------------|--------------------------------------------------------------------|
| Content-Type    | <p>次の値が含まれます。</p><p><pre><code>application/json</code></pre></p>                   |

### Response JSON object fields

| フィールド名       | データ型    | 説明                     | 包含 |
|---------------|---------|-----------------------------|:---------:|
| `access_token`  | string  | 削除したClovaアクセストークン                               | 常時      |
| `client_id`     | string  | クライアントID                                       | 常時      |
| `expires_in`    | number  | 削除したClovaアクセストークンが持っていた有効期限(秒単位)              | 常時      |

### Status codes

| ステータスコード       | 説明                     |
|---------------|-------------------------|
| 200 OK                    | リクエスト成功を示します。                                                                                                                       |
| 400 Bad Request           | `client_id`など、必須パラメーターを入力しなかったか、パラメーターに無効なデータを入力したことを示します。                                        |
| 401 Unauthorized          | 無効なクライアント認証情報(`client_id`もしくは`client_secret`)、またはユーザー情報(`device_id`または`model_id`)をパラメーターに渡したことを示します。 |
| 500 Internal Server Error | サーバー内部にエラーが発生し、アクセストークンを削除できなかったことを示します。                                                                                             |

### Response example
{% raw %}
```json
{
    "access_token": "xFcH08vYQcahQWouqIzWOw",
    "expires_in": 12960000,
    "client_id": "c2Rmc2Rmc2FkZ2FzZnNhZGZ"
}
```
{% endraw %}

### 次の項目も参照してください。
* [クライアント認証情報](/CIC/Guides/Interact_with_CIC.md#ClientAuthInfo)
* [Clovaアクセストークンをリクエストする](#RequestClovaAccessToken)
