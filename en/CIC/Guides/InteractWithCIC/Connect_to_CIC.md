## Connecting with CIC {#ConnectToCIC}
To connect your client with CIC, complete the following steps.
* [Creating Clova access token](#CreateClovaAccessToken)
* [Creating connection](#CreateConnection)
* [Getting authorization](#Authorization)
* [Managing connection](#ManageConnection)

### Creating Clova access token {#CreateClovaAccessToken}
To use Clova, users must authenticate their {{ book.TargetServiceForClientAuth }} account on your client (device or app). And, to attempt to connect your client with CIC, you must obtain a Clova access token, which has been authorized with its {{ book.TargetServiceForClientAuth }} account credentials. You use [Clova Auth API](/CIC/References/Clova_Auth_API.md) for this process.

![](/CIC/Resources/Images/CIC_Authorization.png)

Below are the steps to obtain a Clova access token.

<ol>
<li><p>In your client app or app paired with a client device, add an interface for users to authenticate their {{ book.TargetServiceForClientAuth }} account (<a href="{{ book.LoginAPIofTargetService }}" target="_blank">{{ book.TargetServiceForClientAuth }} Login SDK</a>). You must use client app or paired app because user's speech input alone cannot handle account authentication.</p>
</li>
<li><p>Obtain an access token for the {{ book.TargetServiceForClientAuth }} account, using the {{ book.TargetServiceForClientAuth }} account information entered by the user.</p>
</li>
<li><p><a href="/CIC/Clova_Auth_API.html#RequestAuthorizationCode">Request an authorization code</a> by providing the {{ book.TargetServiceForClientAuth }} account access token and <a href="#ClientAuthInfo">client credentials</a>. Below is an example of requesting an authorization code.</p>
<pre><code>$ curl -H 'Authorization: Bearer QHSDAKLFJASlk12jlkf+asldkjasdf=sldkjf123dsalsdflkvpasdFMrjvi23scjaf123klv'
       {{ book.AuthServerBaseURL }}authorize \
       --data-urlencode 'client_id=c2Rmc2Rmc2FkZ2Fasdkjh234zZnNhZGZ' \
       --data-urlencode 'device_id=aa123123d6-d900-48a1-b73b-aa6c156353206' \
       --data-urlencode 'model_id=test_model' \
       --data-urlencode 'response_type=code' \
       --data-urlencode 'state=FKjaJfMlakjdfTVbES5ccZ'
</code></pre>
<p>The authorization code is returned as follows.</p>
<pre><code>{
    "code": "cnl__eCSTdsdlkjfweyuxXvnlA",
    "state": "FKjaJfMlakjdfTVbES5ccZ"
}
</code></pre></li>
<li><p>(If it is a paired app) Forward the authorization code to the client device.</p>
</li>
<li><p>Pass the authorization code and <a href="#ClientAuthInfo">client credentials</a> as parameters and <a href="/CIC/References/Clova_Auth_API.html#RequestClovaAccessToken">request a Clova access token</a>. Below is an example of requesting a Clova access token.</p>
<pre><code>$ curl {{ book.AuthServerBaseURL }}token?grant_type=authorization_code \
       --data-urlencode 'client_id=c2Rmc2Rmc2FkZ2Fasdkjh234zZnNhZGZ' \
       --data-urlencode 'client_secret=66qo65asdfasdfaA7JasdfasfOqwnOq1rOyfgeydtCDrvYasfasf%3D' \
       --data-urlencode 'code=cnl__eCSTdsdlkjfweyuxXvnlA' \
       --data-urlencode 'device_id=aa123123d6-d900-48a1-b73b-aa6c156353206' \
       --data-urlencode 'model_id=test_model'
</code></pre>
<p>The Clova access token is returned as follows.</p>
<pre><code>{
    "access_token": "XHapQasdfsdfFsdfasdflQQ7w",
    "expires_in": 332000,
    "refresh_token": "GW-Ipsdfasdfdfs3IbHFBA",
    "token_type": "Bearer"
}
</code></pre>
</li>
</ol>

<div class="note">
<p><strong>Note!</strong></p>
<p>When obtaining a Clova access token using user's {{ book.TargetServiceForClientAuth }} account credentials, you may have to ask the user to agree to the terms of use or display a WebView explaining about age verification. Detailed guidelines will be available soon. When developing with a test account, use the Clova mobile app to agree to the terms of use and complete age verification.</p>
</div>


### Creating CIC connection {#CreateConnection}
To establish an initial connection between your client and CIC, the first thing to do is [creating a downchannel](/CIC/References/CIC_API.md#EstablishDownchannel). A downchannel is used when you receive directive messages from CIC. These directive messages are not responses prompted by event messages. They are messages initiated exclusively by CIC (cloud-initiated) when certain conditions are met or when any needs arise. For example, when a new alarm (push) arrives, a directive message will be sent through a downchannel.

To create a downchannel, send a `GET` request to `/v1/directives`. Once a downchannel is established, CIC keeps the connection open.

{% raw %}
```
:method: GET
:scheme: https
:path = /v1/directives
Authorization: Bearer {{ClovaAccessToken}}
```
{% endraw %}

When the connection request is processed successfully, CIC returns a [`Clova.Hello`](/CIC/References/APIs/Clova.md#Hello) directive message as a response. It indicates that CIC is ready to send more directive messages through the downchannel.

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
<p><strong>Note!</strong></p>
<ul><li>Once a client app or device has started, it must always maintain one active downchannel with CIC. If any new request is sent to <code>/v1/directives</code> when an active downchannel already exists, that existing downchannel will be closed.</li><li>See <a href="#Authorization">Getting authorization</a> for more details on filling in the Authorization header field.</li></ul>
</div>


### Getting authorization {#Authorization}
When sending requests to CIC, you must send [Clova access tokens](#CreateClovaAccessToken) along with the requests. Enter Clova access token's type and value, separated by a space, in the Authorization header field as follows. See [CIC API reference](/CIC/References/CIC_API.md) for more details.

{% raw %}
```
:method: {{GET|POST}}
:scheme: https
:path = {{/v1/events|/v1/directives}}
Authorization: Bearer {{ClovaAccessToken}}
```
{% endraw %}

Every time you send a new request (event message), you must send a Clova access token together as shown in the picture below.

![](/CIC/Resources/Images/CIC_Message_Interaction_Diagram.png)

### Managing connection {#ManageConnection}

Once a connection is established between your client and CIC, manage the connection by running the following tasks.

* [Maintaining downchannel](#KeepDownchannel)
* [Performing ping-pong](#DoPingpong)
* [Refreshing access token](#RefreshAccessToken)

#### Maintaining downchannel {#KeepDownchannel}
When an existing downchannel is closed or disconnected, [create a new downchannel](#CreateConnection) immediately to prevent from failing to receive directive messages from CIC.

#### Performing ping-pong {#DoPingpong}

Send HTTP/2 PING frames to CIC in every 1 minute to confirm connectivity with CIC. When failing to receive HTTP/2 PING ACK responses from CIC, establish a new connection immediately to maintain a connection between your client and CIC. Refer to [HTTP/2 PING Payload Format](https://http2.github.io/http2-spec/#rfc.figure.12) for more details on the HTTP/2 PING frame.

<div class="note">
<p><strong>Note!</strong></p>
<p>If your client cannot send HTTP/2 PING frames, it must send <code>GET</code> requests to <code>/ping</code> every 1 minute, at which points, it will receive an HTTP 204 No Content response. As is the case with HTTP/2 PING frames, if it fails to receive responses, establish a new connection immediately.</p><p>This is an example of sending a <code>GET</code> request to <code>/ping</code>.</p>
<pre><code>:method = GET
:scheme = https
:path = /ping
Authorization = Bearer {{YOUR_ACCESS_TOKEN}}
</code></pre>
</div>

#### Refreshing access token {#RefreshAccessToken}

When obtaining an access token, you can check its expiry time from the `expires_in` field. If the time expires, or if you receive an [error message](/CIC/References/CIC_API.md#Error) that reads, "HTTP 401 Unauthorized", you must refresh the access token. [To refresh the Clova access token](/CIC/References/Clova_Auth_API.md#RefreshClovaAccessToken), send the refresh token (`refresh_token`) you have received when [obtaining the Clova access token](/CIC/References/Clova_Auth_API.md#RequestClovaAccessToken) and pass required parameters, as shown below.

<pre><code>$ curl {{ book.AuthServerBaseURL }}token?grant_type=refresh_token \
       --data-urlencode 'client_id=c2Rmc2Rmc2FkZ2FzZnNhZGZ' \
       --data-urlencode 'client_secret=66qo65asdfasdfaA7JasdfasfOqwnOq1rOyfgeydtCDrvYasfasf%3D' \
       --data-urlencode 'refresh_token=GW-Ipsdfasdfdfs3IbHFBA' \
       --data-urlencode 'device_id=aa123123d6-d900-48a1-b73b-aa6c156353206' \
       --data-urlencode 'model_id=test_model'
</code></pre>