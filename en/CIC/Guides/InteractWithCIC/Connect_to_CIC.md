## Connecting with CIC {#ConnectToCIC}

To connect a client with CIC, complete the following steps.

* [Creating Clova access token](#CreateClovaAccessToken)
* [Creating connection](#CreateConnection)
* [Getting authorization](#Authorization)
* [Managing connection](#ManageConnection)

### Creating Clova access token {#CreateClovaAccessToken}

To use Clova, users must authenticate their {{ book.TargetServiceForClientAuth }} account on a client, whether be it a device or an app. For a client to connect with CIC, you need to have a Clova access token issued for the user's {{ book.TargetServiceForClientAuth }} account. Clova access tokens are obtainable from the Clova authorization server using the [Clova Auth API](/CIC/References/Clova_Auth_API.md).

The following diagram illustrates the process of a client obtaining a Clova access token. Note that the process differs for each client type. Clova defines the following two types of clients for providing Clova services:

* Device type: Clients embedded in devices like speakers or home appliances. The device types come with paired apps to provide better user experience, especially for user authentication.
* App type: Clients as an app, just like the Clova app.

![](/CIC/Resources/Images/CIC_Authorization.png)

To obtain a Clova access token, we need to have the user authenticate their {{ book.TargetServiceForClientAuth }} account on your client through a UI. Authenticating verbally is not supported. If your client is an app, then simply use your client app. If your client is a device, then use a pair app.

Obtain a Clova access token by following the instructions provided below:

<ol>
  <li>
    <p>Prompt a user to log into {{ book.TargetServiceForClientAuth }} (<a href="{{ book.LoginAPIofTargetService }}" target="_blank">{{ book.TargetServiceForClientAuth }} Login SDK</a>) on your client app or pair app (device type).</p>
  </li>
  <li>
    <p>Obtain an access token for the {{ book.TargetServiceForClientAuth }} account, using the {{ book.TargetServiceForClientAuth }} account information entered by the user.</p>
  </li>
  <li>
    <p><a href="/CIC/References/Clova_Auth_API.html#RequestAuthorizationCode">Request an authorization code</a> with the {{ book.TargetServiceForClientAuth }} access token and <a href="#ClientAuthInfo">client credentials</a>. Define the <code>device_id</code> field either with the client's MAC address or with the hash value of UUID generated on your own. The following is an example of requesting an authorization code.</p>
    <pre><code>$ curl -H 'Authorization: Bearer QHSDAKLFJASlk12jlkf+asldkjasdf=sldkjf123dsalsdflkvpasdFMrjvi23scjaf123klv'
    {{ book.AuthServerBaseURL }}authorize \
    --data-urlencode 'client_id=c2Rmc2Rmc2FkZ2Fasdkjh234zZnNhZGZ' \
    --data-urlencode 'device_id=aa123123d6-d900-48a1-b73b-aa6c156353206' \
    --data-urlencode 'model_id=test_model' \
    --data-urlencode 'response_type=code' \
    --data-urlencode 'state=FKjaJfMlakjdfTVbES5ccZ'
</code></pre>
    <p>As a response to your request, you will receive a response, containing the authorization code in the body as shown below. The <code>code</code> field holds the authorization code.</p>
    <pre><code>{
  "code": "cnl__eCSTdsdlkjfweyuxXvnlA",
  "state": "FKjaJfMlakjdfTVbES5ccZ"
}
</code></pre></li>
  <li>
    <p>(If you receive the <code>451 Unavailable For Legal Reasons</code> status code as a response to your request for an <a href="/CIC/References/Clova_Auth_API.html#RequestAuthorizationCode">authorization code </a>) Show the user the terms and conditions agreement page which is accessible with the <code>redirect_uri</code>, contained in the response body. See an example of a response message for the status code <code>451 Unavailable For Legal Reasons</code>.</p>
    <pre><code>{
      "code": "4mrklvwoC_KNgDlvmslka",
      "redirect_uri": "https://ssl.pstatic.net/static/clova/service/terms/place/terms_3rd.html?code=4mrklvwoC_KNgDlvmslka&grant_type=code&state=FKjaJfMlakjdfTVbES5ccZ",
      "state": "FKjaJfMlakjdfTVbES5ccZ"
    }
    </code></pre>
    <p>If the user does not agree to the terms and conditions, the user cannot proceed to the next step. When the user submits the agreement, the client will receive a response containing the <code>302 Found</code>(URL Redirection) status code along with either one of the following URLs:</p>
    <ul>
      <li><code>clova://agreement-success</code>: The user agreement has been processed successfully. The client is allowed to proceed onto the next step, creating the Clova access token.</li>
      <li><code>clova://agreement-failure</code>: Processing the user agreement has failed to due a server error. We recommend you to take appropriate actions regarding the failure.</li>
    </ul>
  </li>
  <li>
    <p>(For device types only) Forward the authorization code from your pair app to the client device.</p>
  </li>
  <li>
    <p>From the client, <a href="/CIC/References/Clova_Auth_API.html#RequestClovaAccessToken">request a Clova access token</a> with the authorization code and <a href="#ClientAuthInfo">client credentials</a> as the parameters, as shown below.</p>
    <pre><code>$ curl {{ book.AuthServerBaseURL }}token?grant_type=authorization_code \
    --data-urlencode 'client_id=c2Rmc2Rmc2FkZ2Fasdkjh234zZnNhZGZ' \
    --data-urlencode 'client_secret=66qo65asdfasdfaA7JasdfasfOqwnOq1rOyfgeydtCDrvYasfasf%3D' \
    --data-urlencode 'code=cnl__eCSTdsdlkjfweyuxXvnlA' \
    --data-urlencode 'device_id=aa123123d6-d900-48a1-b73b-aa6c156353206' \
    --data-urlencode 'model_id=test_model'
</code></pre>
    <p>As a response to your request, a Clova access token will be returned containing the following information.</p>
    <pre><code>{
    "access_token": "XHapQasdfsdfFsdfasdflQQ7w",
    "expires_in": 332000,
    "refresh_token": "GW-Ipsdfasdfdfs3IbHFBA",
    "token_type": "Bearer"
}
</code></pre>
  </li>
</ol>

### Creating CIC connection {#CreateConnection}

To establish an initial connection between a client and CIC, the first thing to do is [creating a downchannel](/CIC/References/CIC_API.md#EstablishDownchannel). A downchannel is used for a client to receive directives from CIC. Directives sent through the downchannel are _not_ responses to events, but are initiated by CIC (cloud-initiated) when conditions are met or when needs arise. For example, when a new push message arrives for a user, CIC will send a directive through a downchannel to inform the client of the arrival.

To create a downchannel, send a `GET` request to `/v1/directives`. Once a downchannel is established, CIC keeps the connection open.

{% raw %}

```
:method: GET
:scheme: https
:path = /v1/directives
Authorization: Bearer {{ClovaAccessToken}}
```

{% endraw %}

When a connection is successfully established, CIC responds with the [`Clova.Hello`](/CIC/References/CICInterface/Clova.md#Hello) directive, to inform the client that CIC is ready to send more directives through the downchannel.

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
  <ul>
    <li>At least one downchannel shall remain active after a client app or a device client is turned on.
    If any extra request is made to <code>/v1/directives</code> to create a downchannel while an active downchannel remains, the active downchannel will get closed.</li>
    <li>See <a href="#UserAgentString">User-Agent string</a> for more details on what and how to write in the user-agent string which is a must in an HTTP header.</li>
    <li>See <a href="#Authorization">Getting authorization</a> for more details on the Authorization header field.</li>
  </ul>
</div>

<div class="danger">
  <p><strong>Caution!</strong></p>
  <p>To <a href="#SendEvent">send events</a> to CIC, you MUST create a downchannel. Otherwise, you cannot send any events to CIC.</p>
</div>


### Getting authorization {#Authorization}

When sending requests to CIC, you must send a [Clova access token](#CreateClovaAccessToken) along with the requests. Enter Clova access token type and value, separated by a space, in the Authorization header field as follows. See [CIC API reference](/CIC/References/CIC_API.md) for more details.

{% raw %}

```
:method: {{GET|POST}}
:scheme: https
:path = {{/v1/events|/v1/directives}}
Authorization: Bearer {{ClovaAccessToken}}
```

{% endraw %}

Every time you send a new request (event), you must send a Clova access token in the request, as shown in the picture below.

![](/CIC/Resources/Images/CIC_Message_Interaction_Diagram.png)

### Managing connection {#ManageConnection}

Once a connection is established between a client and CIC, manage the connection as instructed:

* [Maintaining downchannel](#KeepDownchannel)
* [Ping pong](#DoPingpong)
* [Refreshing access token](#RefreshAccessToken)

#### Maintaining downchannel {#KeepDownchannel}

When a downchannel is closed, either by request or network disconnection, [create a new downchannel](#CreateConnection) immediately to guarantee receiving directives from CIC.

#### Ping pong {#DoPingpong}

To check connectivity with CIC, send an HTTP/2 PING frame to CIC every minute. If you fail to receive an HTTP/2 PING ACK response from CIC,  establish a new connection immediately. You must maintain a connection between a client and CIC all the time. Refer to [HTTP/2 PING Payload Format](https://http2.github.io/http2-spec/#rfc.figure.12) for more detail on HTTP/2 PING frame.

<div class="note">
  <p><strong>Note!</strong></p>
  <p>If a client cannot send an HTTP/2 PING frame, send a <code>GET</code> request to <code>/ping</code> every minute. You will receive an HTTP 204 No Content response for your request. If you fail to receive a response, establish a new connection with CIC immediately.</p>
  <p>This is an example of a <code>GET</code> request to <code>/ping</code>.</p>
  <pre><code>:method = GET
:scheme = https
:path = /ping
Authorization = Bearer {{YOUR_ACCESS_TOKEN}}
</code></pre>
</div>

#### Refreshing access token {#RefreshAccessToken}

You can find the expiry time of a Clova access token by the `expires_in` field when you obtain the token. If the token expires, or if you receive an "HTTP 401 Unauthorized" [error message](/CIC/References/CIC_API.md#Error) for using the token, you must refresh the token. [To refresh the Clova access token](/CIC/References/Clova_Auth_API.md#RefreshClovaAccessToken), add the `refresh_token` you have received when [obtaining the Clova access token](/CIC/References/Clova_Auth_API.md#RequestClovaAccessToken) to the parameters, as shown below.

<pre><code>$ curl {{ book.AuthServerBaseURL }}token?grant_type=refresh_token \
       --data-urlencode 'client_id=c2Rmc2Rmc2FkZ2FzZnNhZGZ' \
       --data-urlencode 'client_secret=66qo65asdfasdfaA7JasdfasfOqwnOq1rOyfgeydtCDrvYasfasf%3D' \
       --data-urlencode 'refresh_token=GW-Ipsdfasdfdfs3IbHFBA' \
       --data-urlencode 'device_id=aa123123d6-d900-48a1-b73b-aa6c156353206' \
       --data-urlencode 'model_id=test_model'
</code></pre>
