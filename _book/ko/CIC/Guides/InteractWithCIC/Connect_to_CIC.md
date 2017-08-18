## CIC 연결하기 {#ConnectToCIC}
클라이언트가 CIC와 연결하려면 다음과 같은 항목을 수행해야 합니다.
* [Clova access token 생성하기](#CreateClovaAccessToken)
* [연결 생성하기](#CreateConnection)
* [인증하기](#Authorization)
* [연결 관리하기](#ManageConnection)

### Clova access token 생성하기 {#CreateClovaAccessToken}
사용자는 {{ book.TargetServiceForClientAuth }} 계정을 클라이언트의 기기나 앱에 인증해야 Clova를 사용할 수 있습니다. {{ book.TargetServiceForClientAuth }} 계정 인증 정보까지 처리된  Clova access token을 Clova 인증 서버로부터 획득해야 클라이언트가 CIC로 연결을 시도할 수 있습니다. 이를 위해 [Clova 인증 API](/CIC/References/Clova_Auth_API.md)를 이용해야 합니다.

![](/CIC/Resources/Images/CIC_Authorization.png)

Clova access token을 획득하는 절차는 다음과 같습니다.

<ol>
<li><p>사용자가 {{ book.TargetServiceForClientAuth }} 계정을 인증할 수 있는 인터페이스를 클라이언트 앱 또는 클라이언트 기기와 페어링하는 앱에서 제공합니다(<a href="{{ book.LoginAPIofTargetService }}" target="_blank">{{ book.TargetServiceForClientAuth }} 아이디로 로그인하기 SDK</a>). 사용자 음성 입력만으로 계정 인증을 할 수 없기 때문에 반드시 클라이언트 앱이나 페어링 앱을 사용해야 합니다.</p>
</li>
<li><p>사용자가 입력한 {{ book.TargetServiceForClientAuth }} 계정 정보를 이용하여 {{ book.TargetServiceForClientAuth }} 계정 access token을 획득합니다.</p>
</li>
<li><p>획득한 {{ book.TargetServiceForClientAuth }} 계정 access token과 <a href="#ClientAuthInfo">클라이언트 인증 정보</a> 등의 정보를 <a href="/CIC/Clova_Auth_API.html#authorize">/authorize</a> API의 파라미터로 입력하여 authorization code를 획득합니다. 다음은 authorization code를 요청한 예입니다.</p>
<pre><code>{{ book.AuthServerBaseURL }}authorize?client_id=7Jlaksjdflq1rOuTpA%3D%3D
                               &amp;device_id=test_device
                               &amp;model_id=test_model
                               &amp;response_type=code
                               &amp;state=95%2FKjaJfMlakjdfTVbES5ccZQ%3D%3D
</code></pre>
<p>다음과 같은 authorization code가 반환됩니다.</p>
<pre><code>{
    "code": "cnl__eCSTdsdlkjfweyuxXvnlA",
    "state": "95/KjaJfMlakjdfTVbES5ccZQ=="
}
</code></pre></li>
<li><p>(페어링 앱의 경우) authorization code를 실제 클라이언트 기기로 전송합니다.</p>
</li>
<li><p>획득한 authorization code와 <a href="#ClientAuthInfo">클라이언트 인증 정보</a> 등의 정보를 <a href="/CIC/References/Clova_Auth_API.html#token">/token</a> API의 파라미터로 입력하여 Clova access token을 획득합니다. 다음은 Clova access token을 요청한 예입니다.</p>
<pre><code>{{ book.AuthServerBaseURL }}token?client_id=7JWI64WVIsdfasdfrOuTpA%3D%3D
                           &amp;client_secret=66qo65asdfasdfaA7JasdfasfOqwnOq1rOyfgeydtCDrvYasfasf%3D
                           &amp;code=cnl__eCSTdsdlkjfweyuxXvnlA
                           &amp;device_id=test_device
                           &amp;grant_type=authorization_code
                           &amp;model_id=test_model
</code></pre>
<p>다음과 같은 Clova access token이 반환됩니다.</p>
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
<p>{{ book.TargetServiceForClientAuth }} 계정 인증 정보를 사용하여 Clova access token을 획득할 때, 사용자에게 추가적인 약관 동의를 얻어야 하거나 성인 인증 관련 정보를 WebView로 표시해야 할 수 있습니다. 이 내용에 대한 가이드는 현재 준비 중입니다. 개발 시 테스트를 위해 우선 모바일용 Clova 앱에서 약관 동의 및 성인 인증이 완료된 계정을 이용해주시기 바랍니다.</p>
</div>


### CIC 연결하기 {#CreateConnection}
CIC는 HTTP/2 프로토콜을 사용하며, CIC에 연결할 때 사용하는 base URL은 다음과 같습니다.

<pre><code>{{ book.CICBaseURL }}
</code></pre>

클라이언트가 CIC와 최초 연결 시 수행되어야 하는 작업은 downchannel을 구성하는 것입니다. Downchannel은 CIC로부터 지시 메시지를 받을 때 사용됩니다. 이때 전달받는 지시 메시지는 클라이언트의 이벤트 메시지에 대한 응답으로 전달되는 지시 메시지가 아닌 특정 조건이나 필요에 의해 CIC의 주도(Cloud-initiated)로 클라이언트에 보내는 지시 메시지입니다. 예를 들면, 새로운 알림(push)이 도착했다면 downchannel을 통해 지시 메시지가 전달될 것입니다.

Downchannel은 `/v1/directives` 경로로 `GET` 방식 요청을 보내면 구성할 수 있으며, CIC에 의해 연결이 계속 유지됩니다.

{% raw %}
```
:method: GET
:scheme: https
:path = /v1/directives
Authorization: Bearer {{ClovaAccessToken}}
```
{% endraw %}

위 연결 요청이 성공적으로 수행되면 CIC는 다음과 같은 [`Clova.Hello`](/CIC/References/APIs/Clova.md#Hello) 지시 메시지를 응답으로 보냅니다. 이는 downchannel을 통해 추가적인 지시 메시지 전달될 준비가 되었음을 나타냅니다.

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
<ul><li>클라이언트 앱이나 기기가 시작되면, CIC와 연결하여 항시 하나의 downchannel을 유지하도록 해야 합니다. 만약, downchannel이 생성된 상태에서 <code>/v1/directives</code>으로 추가 요청이 들어오면 기존 downchannel은 해제됩니다.</li><li>헤더에 포함해야 하는 Authorization 필드에 대한 내용은 <a href="#Authorization">인증하기</a>를 참조합니다.</li></ul>
</div>


### 인증하기 {#Authorization}
클라이언트가 CIC에 요청을 보낼 때 [Clova access token](#CreateClovaAccessToken)을 함께 전달해야 합니다. 아래와 같이 헤더의 Authorization 필드에 Clova access token의 타입과 값을 공백 문자(space)로 구분하여 입력해야 합니다. HTTP 포맷에 대한 자세한 설명은 [HTTP/2 메시지](/CIC/References/HTTP2_Message_Format.md)을 참조합니다.

{% raw %}
```
:method: {{GET|POST}}
:scheme: https
:path = /v1/events
Authorization: Bearer {{ClovaAccessToken}}
```
{% endraw %}

클라이언트가 새로운 요청(이벤트 메시지)을 보낼 때마다 다음 그림과 같이 Clova access token을 함께 전달해야 합니다.

![](/CIC/Resources/Images/CIC_Message_Interaction_Diagram.png)

### 연결 관리하기 {#ManageConnection}

클라이언트와 CIC 사이에 연결이 구성되면, 클라이언트는 다음과 같이 연결을 관리해야 합니다.

| 구분      | 설명                               |
|----------|-----------------------------------|
| DownChannel 유지 | Downchannel 연결이 종료되거나 끊어지면 클라이언트는 즉시 새로운 [downchannel을 구성](#CreateConnection)하여, CIC로부터 전달되는 지시 메시지를 받지 못하는 일이 없도록 해야합니다. |
| Ping-pong 수행 | CIC와 연결이 유지되고 있는지 파악하기 위해 클라이언트는 1분 간격으로 HTTP/2 PING 프레임을 CIC로 전송해야 합니다. CIC로부터 HTTP/2 PING ACK 응답을 받지 못하면 클라이언트는 즉시 새로운 연결을 구성해 클라이언트와 CIC간의 연결이 지속될 수 있도록 해야합니다. HTTP/2 PING 프레임에 대한 자세한 설명은 [HTTP/2 PING Payload Format](https://http2.github.io/http2-spec/#rfc.figure.12)을 참조합니다.|

<div class="note">
<p><strong>Note!</strong></p>
<p>HTTP/2 PING 프레임을 전송할 수 없으면 클라이언트는 1분마다 <code>GET</code> 요청을 <code>/ping</code>으로 보내야 합니다. 이때, HTTP 204 No Content 응답을 받게 됩니다. HTTP/2 PING 프레임을 사용할 때와 마찬가지로 응답을 받지 못하면, 클라이언트는 즉시 새로운 연결을 구성해야 합니다.</p>
<p>다음은 <code>/ping</code>으로 <code>GET</code> 요청을 보내는 예제입니다.</p>
<pre><code>:method = GET
:scheme = https
:path = /ping
Authorization = Bearer {{YOUR_ACCESS_TOKEN}}
</code></pre>
</div>
