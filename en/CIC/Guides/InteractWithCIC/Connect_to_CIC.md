## Connecting with CIC {#ConnectToCIC}
To connect your client with CIC, do the following.
* [Creating Clova access token](#CreateClovaAccessToken)
* [Creating connection](#CreateConnection)
* [Authorization](#Authorization)
* [Managing connection](#ManageConnection)

### Creating Clova access token {#CreateClovaAccessToken}
To use Clova, a user must authenticate his or her {{ book.TargetServiceForClientAuth }} account on your client (device of app). And your client must obtain a Clova access token, with authorized {{ book.TargetServiceForClientAuth }} account credentials, from the Clova authorization server before trying to connect with CIC. You must use [Clova Auth API](/CIC/References/Clova_Auth_API.md) for this process.

![](/CIC/Resources/Images/CIC_Authorization.png)

Below are the steps to obtain a Clova access token.

<ol>
<li><p>In your client app or app paired with a client device, add an interface for authenticating a {{ book.TargetServiceForClientAuth }} account (<a href="{{ book.LoginAPIofTargetService }}" target="_blank">{{ book.TargetServiceForClientAuth }} Login SDK</a>). You must use a client app or a paired app to complete this step because user's speech input alone cannot handle account authentication.</p>
</li>
<li><p>Obtain a {{ book.TargetServiceForClientAuth }} account authentication token using the {{ book.TargetServiceForClientAuth }} account information provided from the user.</p>
</li>
<li><p>Obtain an authorization code by passing the {{ book.TargetServiceForClientAuth }} account access token and <a href="#ClientAuthInfo">client credentials</a> to the parameters of the <a href="/CIC/Clova_Auth_API.html#authorize">/authorize</a> API. Below is an example of requesting an authorization code.</p>
<pre><code>{{ book.AuthServerBaseURL }}/authorize?client_id=7Jlaksjdflq1rOuTpA%3D%3D
                               &amp;device_id=test_device
                               &amp;model_id=test_model
                               &amp;response_type=code
                               &amp;state=95%2FKjaJfMlakjdfTVbES5ccZQ%3D%3D
</code></pre>
<p>The authorization code is returned as follows.</p>
<pre><code>{
    "code": "cnl__eCSTdsdlkjfweyuxXvnlA",
    "state": "95/KjaJfMlakjdfTVbES5ccZQ=="
}
</code></pre></li>
<li><p>(If it is a paired app) Forward the authorization code to the client device.</p>
</li>
<li><p>Obtain a Clova access token by passing the authorization code and <a href="#ClientAuthInfo">client credentials</a> to the parameters of the <a href="/CIC/References/Clova_Auth_API.html#token">/token</a> API. Below is an example of requesting a Clova access token.</p>
<pre><code>{{ book.AuthServerBaseURL }}/token?client_id=7JWI64WVIsdfasdfrOuTpA%3D%3D
                           &amp;client_secret=66qo65asdfasdfaA7JasdfasfOqwnOq1rOyfgeydtCDrvYasfasf%3D
                           &amp;code=cnl__eCSTdsdlkjfweyuxXvnlA
                           &amp;device_id=test_device
                           &amp;grant_type=authorization_code
                           &amp;model_id=test_model
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
<p>When obtaining a Clova access token using {{ book.TargetServiceForClientAuth }} account credentials, you may have to ask your users to agree to the terms of use or display a WebView with age verification information. Related guidelines will be ready soon. In the meantime, when developing with a test account, use the Clova mobile app to agree to the terms of use and complete age verification.</p>
</div>


### Creating CIC connection {#CreateConnection}
To connect with CIC using the HTTP/2 protocol, use the following base URL.

{% raw %}
```
https://prod-ni-cic.clova.ai/
```
{% endraw %}

When your client attempts to establish an initial connection with CIC, the first thing to do is creating a "downchannel." A downchannel is used When CIC sends directive messages. These directive messages are not response messages prompted by event messages. They are messages initiated by CIC itself (cloud-initiated) when certain conditions are met or when any special needs arise. For example, when a new alarm (push) arrives, a directive message will be sent through a downchannel.

To create a downchannel, send a request to */v1/directives* using *GET*. Once a downchannel is created, CIC maintains the connection.

{% raw %}
```
:method: GET
:scheme: https
:path = /v1/directives
Authorization: Bearer {{ClovaAccessToken}}
```
{% endraw %}

<div class="note">
<p><strong>Note!</strong></p>
<ul><li>Once a client app or device has started, it must always maintain one active downchannel with CIC. If any new request is sent to */v1/directives* while one active downchannel is already present, that downchannel will be closed.</li><li>See <a href="#Authorization">Authorization</a> for more details on the Authorization header field.</li></ul>
</div>


### Authorization {#Authorization}
When sending a request to CIC, you must send a [Clova access token](#CreateClovaAccessToken) along with the request. Enter the type and value of a Clova access token, separated by a space, in the Authorization header field as follows. See [HTTP/2 message](/CIC/References/HTTP2_Message_Format.md) for more details on the HTTP format.

{% raw %}
```
:method: {{GET|POST}}
:scheme: https
:path = /v1/events
Authorization: Bearer {{ClovaAccessToken}}
```
{% endraw %}

Every time you send a new request (event message), you must send a Clova access token together as the following picture shows.

![](/CIC/Resources/Images/CIC_Message_Interaction_Diagram.png)

### Managing connection {#ManageConnection}

Once you have established a connection between your client and CIC, manage the connection in the following manner.

| Task      | Description                               |
|----------|-----------------------------------|
| Maintaining downchannel | When an existing downchannel is closed or disconnected, [create a new downchannel](#CreateConnection) immediately to prevent from failing to receive any directive message from CIC. |
| Performing ping-pong | Send HTTP/2 PING frames to CIC in every 1 minute. When failing to receive HTTP/2 PING ACK responses from CIC, create a new connection immediately to ensure that a connection is kept open between your client and CIC. Refer to [HTTP/2 PING Payload Format](https://http2.github.io/http2-spec/#rfc.figure.12) for more details on the HTTP/2 PING frame. |

<div class="note">
<p><strong>Note!</strong></p>
<p>If you cannot send HTTP/2 PING frames, you must send GET requests to /ping every 1 minute, at which point, an HTTP 204 No Content response is returned. As is the case with HTTP/2 PING frames, if you fail to receive a response, you must create a new connection immediately.</p>
<p>This is an example of sending a GET request to /ping.</p>
<pre><code>:method = GET
:scheme = https
:path = /ping
Authorization = Bearer {{YOUR_ACCESS_TOKEN}}
</code></pre>
</div>
