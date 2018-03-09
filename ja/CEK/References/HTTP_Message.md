## HTTPメッセージ {#HTTPMessage}
CEKとExtensionが通信する際、HTTP/1.1プロトコルを使用して基本的なHTTPSリクエストとHTTPSレスポンスをやり取りします。CEKとExtensionが通信する際、HTTPメッセージのボディには、JSON形式のメッセージが含まれます。ここでは、CEKとExtensionがやり取りするHTTPメッセージの構成について説明します。

### HTTPヘッダー {#HTTPHeader}
CEKがExtensionに解析されたユーザーの発話情報を渡す際、HTTPSリクエストを使用します。その際、HTTPSリクエストのヘッダーは、次のように構成されます。

{% raw %}
```
POST /APIpath HTTP/1.1
Host: your.extension.endpoint
Content-Type: application/json;charset-UTF-8
Accept: application/json
Accept-Charset: utf-8
```
{% endraw %}

* HTTP/1.1バージョンでHTTPS通信し、POSTメソッドを使用します。
* Hostとリクエストパスは、Extensionの開発者があらかじめ定義したURIに設定されます。
* ボディのデータはJSON形式で、UTF-8エンコーディングを使用します。


逆に、ExtensionがCEKに処理結果を返す際、HTTPSレスポンスを使用します。その際、HTTPSレスポンスのヘッダーは、次のように基本的なものだけで構成されます。
{% raw %}
```
HTTP/1.1 200 OK
Content-Type: application/json;charset-UTF-8
```
{% endraw %}
* CEKから渡されたHTTPSリクエストに対するレスポンスとして、処理結果を返します。
* ボディのデータはJSON形式で、UTF-8エンコーディングを使用します。

### HTTPボディ {#HTTPBody}
HTTPSリクエストメッセージとレスポンスメッセージのボディはJSON形式で、解析されたユーザーの発話情報や、Extensionの処理結果が含まれています。それぞれのメッセージの構成は、使用するExtensionの種類によって異なります。メッセージ構成の詳細については、[Custom Extensionメッセージ](#CustomExtMessage)と[Clova Home Extensionメッセージ](#ClovaHomeExtMessage)を参照してください。
