## CIC 연결하기 {#ConnectToCIC}
클라이언트가 CIC와 연결하려면 다음과 같은 항목을 수행해야 합니다.
* [Clova access token 생성하기](#CreateClovaAccessToken)
* [연결 생성하기](#CreateConnection)
* [인증하기](#Authorization)
* [연결 관리하기](#ManageConnection)

### Clova access token 생성하기 {#CreateClovaAccessToken}
사용자는 {{ book.TargetServiceForClientAuth }} 계정을 클라이언트의 기기나 앱에 인증해야 Clova를 사용할 수 있습니다. {{ book.TargetServiceForClientAuth }} 계정 인증 정보까지 처리된 Clova access token을 Clova 인증 서버로부터 획득해야 클라이언트가 CIC로 연결을 시도할 수 있습니다. 이를 위해 [Clova 인증 API](/CIC/References/Clova_Auth_API.md)를 이용해야 합니다.

아래 그림은 클라이언트가 Clova access token은 획득하는 흐름을 나타내고 있습니다. 참고로 클라이언트는 두 가지 유형으로 구분되며, 각 유형에 따라 Clova access token을 획득하는 과정이 조금 달라집니다.
* **기기 타입의 클라이언트**: 스피커나 가전 제품에 임베드된 형태로 Clova 서비스를 제공하는 클라이언트입니다. 이런 기기 타입의 클라이언트는 사용자가 계정을 인증할 때 기기를 통해 인증 정보를 입력할 방법이 없거나 불편하기 때문에 이를 보조하기 위해 페어링 앱(paired app)을 제공합니다.
* **앱 타입의 클라이언트**: Clova 앱과 같이 소프트웨어 형태로 Clova 서비스를 제공하는 클라이언트입니다.

![](/CIC/Resources/Images/CIC_Authorization.png)

Clova access token을 획득하는 절차는 다음과 같습니다.

<ol>
  <li>
    <p>사용자가 {{ book.TargetServiceForClientAuth }} 계정을 인증할 수 있는 인터페이스를 클라이언트 앱 또는 클라이언트 기기와 페어링하는 앱에서 제공합니다(<a href="{{ book.LoginAPIofTargetService }}" target="_blank">{{ book.TargetServiceForClientAuth }} 아이디로 로그인하기 SDK</a>). 사용자 음성 입력만으로 계정 인증을 할 수 없기 때문에 반드시 클라이언트 앱이나 페어링 앱을 사용해야 합니다.</p>
  </li>
  <li>
    <p>사용자가 입력한 {{ book.TargetServiceForClientAuth }} 계정 정보를 이용하여 {{ book.TargetServiceForClientAuth }} 계정 access token을 획득합니다.</p>
  </li>
  <li>
    <p>획득한 {{ book.TargetServiceForClientAuth }} 계정 access token과 <a href="#ClientAuthInfo">클라이언트 인증 정보</a> 등의 정보를 이용하여 <a href="/CIC/References/Clova_Auth_API.html#RequestAuthorizationCode">authorization code를 요청</a>합니다. 이때, <code>device_id</code> 필드의 값으로 클라이언트의 MAC 주소를 사용하거나 UUID 해쉬 값을 생성해서 사용합니다. 다음은 authorization code를 요청한 예입니다.</p>
    <pre><code>$ curl -H "Authorization: Bearer QHSDAKLFJASlk12jlkf+asldkjasdf=sldkjf123dsalsdflkvpasdFMrjvi23scjaf123klv"
    {{ book.AuthServerBaseURL }}authorize \
    --data-urlencode "client_id=c2Rmc2Rmc2FkZ2Fasdkjh234zZnNhZGZ" \
    --data-urlencode "device_id=aa123123d6-d900-48a1-b73b-aa6c156353206" \
    --data-urlencode "model_id=test_model" \
    --data-urlencode "response_type=code" \
    --data-urlencode "state=FKjaJfMlakjdfTVbES5ccZ"
</code></pre>
    <p>수신하게 되는 응답 메시지의 본문은 다음과 같습니다. <code>code</code> 필드가 authorization code입니다.</p>
    <pre><code>{
  "code": "cnl__eCSTdsdlkjfweyuxXvnlA",
  "state": "FKjaJfMlakjdfTVbES5ccZ"
}
</code></pre></li>
  <li>
    <p>(만약, <a href="/CIC/References/Clova_Auth_API.html#RequestAuthorizationCode">authorization code를 요청</a>에 대한 응답으로 <code>451 Unavailable For Legal Reasons</code> 상태 코드를 수신한 경우) 응답 메시지 본문 <code>redirect_uri</code> 필드에 입력된 URI를 이용하여 사용자에게 이용 약관 동의 페이지를 보여줘야 합니다. 다음은 상태 코드가 <code>451 Unavailable For Legal Reasons</code>일 때 수신하게 되는 응답 메시지의 본문의 예 입니다.</p>
    <pre><code>{
  "code": "4mrklvwoC_KNgDlvmslka",
  "redirect_uri": "https://ssl.pstatic.net/static/clova/service/terms/place/terms_3rd.html?code=4mrklvwoC_KNgDlvmslka&grant_type=code&state=FKjaJfMlakjdfTVbES5ccZ",
  "state": "FKjaJfMlakjdfTVbES5ccZ"
}
</code></pre>
    <p>참고로 사용자가 이용 약관에 동의하지 않으면 다음 단계를 수행할 수 없습니다. 사용자가 이용 약관에 동의하고 동의한 결과를 서버에 전송하면 클라이언트는 <code>302 Found</code>(URL Redirection) 상태 코드를 가진 응답을 다음과 같은 URL과 함께 수신하게 됩니다.</p>
    <ul>
      <li><code>clova://agreement-success</code>: 사용자가 이용 약관 동의를 완료함. 클라이언트는 Clova access token 발급을 위해 다음 단계를 계속 진행할 수 있습니다.</li>
      <li><code>clova://agreement-failure</code>: 서버 오류로 이용 약관 동의에 실패함. 클라이언트는 적절한 예외 처리를 해야 합니다.</li>
    </ul>
  </li>
  <li>
    <p>(페어링 앱의 경우) authorization code를 실제 클라이언트 기기로 전송합니다.</p>
  </li>
  <li>
    <p>획득한 authorization code와 <a href="#ClientAuthInfo">클라이언트 인증 정보</a> 등의 정보를 파라미터로 입력하여 <a href="/CIC/References/Clova_Auth_API.html#RequestClovaAccessToken">Clova access token을 요청</a>합니다. 다음은 Clova access token을 요청한 예입니다.</p>
    <pre><code>$ curl {{ book.AuthServerBaseURL }}token?grant_type=authorization_code \
    --data-urlencode "client_id=c2Rmc2Rmc2FkZ2Fasdkjh234zZnNhZGZ" \
    --data-urlencode "client_secret=66qo65asdfasdfaA7JasdfasfOqwnOq1rOyfgeydtCDrvYasfasf%3D" \
    --data-urlencode "code=cnl__eCSTdsdlkjfweyuxXvnlA" \
    --data-urlencode "device_id=aa123123d6-d900-48a1-b73b-aa6c156353206" \
    --data-urlencode "model_id=test_model"
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

### CIC 연결하기 {#CreateConnection}
클라이언트가 CIC와 최초 연결 시 수행되어야 하는 작업은 [downchannel을 구성](/CIC/References/CIC_API.md#EstablishDownchannel)하는 것입니다. Downchannel은 CIC로부터 지시 메시지를 받을 때 사용됩니다. 이때 전달받는 지시 메시지는 클라이언트의 이벤트 메시지에 대한 응답으로 전달되는 지시 메시지가 아닌 특정 조건이나 필요에 의해 CIC가 주도(Cloud-initiated)하여 클라이언트에 보내는 지시 메시지입니다. 예를 들면, 새로운 알림(push)이 도착했다면 downchannel을 통해 지시 메시지가 전달될 것입니다.

Downchannel은 `/v1/directives` 경로로 `GET` 방식 요청을 보내면 구성할 수 있으며, CIC에 의해 연결이 계속 유지됩니다.

{% raw %}

```
:method: GET
:scheme: https
:path: /v1/directives
User-Agent: {{User-Agent_string}}
Authorization: Bearer {{ClovaAccessToken}}
```

{% endraw %}

위 연결 요청이 성공적으로 수행되면 CIC는 다음과 같은 [`Clova.Hello`](/CIC/References/CICInterface/Clova.md#Hello) 지시 메시지를 응답으로 보냅니다. 이는 downchannel을 통해 추가적인 지시 메시지가 전달될 준비가 되었음을 나타냅니다.

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
    <li>클라이언트는 CIC와 항시 하나의 downchannel을 유지하도록 해야 합니다. 만약, downchannel이 생성된 상태에서 <code>/v1/directives</code>으로 downchannel 생성하라는 추가 요청이 들어오면 기존 downchannel은 해제됩니다.</li>
    <li>헤더에 포함해야 하는 User-Agent 필드에 대한 내용은 <a href="#UserAgentString">User-Agent string</a>를 참조합니다.</li>
    <li>헤더에 포함해야 하는 Authorization 필드에 대한 내용은 <a href="#Authorization">인증하기</a>를 참조합니다.</li>
  </ul>
</div>

<div class="danger">
  <p><strong>Caution!</strong></p>
  <p>Downchannel을 구성하지 않으면 CIC로 <a href="#SendEvent">이벤트 메시지를 전송</a>할 수 없습니다.</p>
</div>

### 인증하기 {#Authorization}
클라이언트가 CIC에 요청을 보낼 때 [Clova access token](#CreateClovaAccessToken)을 함께 전달해야 합니다. 아래와 같이 헤더의 Authorization 필드에 Clova access token의 타입과 값을 공백 문자(space)로 구분하여 입력해야 합니다. 자세한 설명은 [CIC API](/CIC/References/CIC_API.md)를 참조합니다.

{% raw %}

```
:method: {{GET|POST}}
:scheme: https
:path: {{/v1/events|/v1/directives}}
User-Agent: {{User-Agent_string}}
Authorization: Bearer {{ClovaAccessToken}}
```

{% endraw %}

클라이언트가 새로운 요청(이벤트 메시지)을 보낼 때마다 다음 그림과 같이 Clova access token을 함께 전달해야 합니다.

![](/CIC/Resources/Images/CIC_Message_Interaction_Diagram.png)

### 연결 관리하기 {#ManageConnection}

클라이언트와 CIC 사이에 연결이 구성되면, 클라이언트는 다음과 같은 부분을 신경써서 관리해야 합니다.

* [DownChannel 유지](#KeepDownchannel)
* [Ping-pong 수행](#DoPingpong)
* [Access token 갱신](#RefreshAccessToken)

#### DownChannel 유지 {#KeepDownchannel}
Downchannel 연결이 종료되거나 끊어지면 클라이언트는 즉시 새로운 [downchannel을 구성](#CreateConnection)하여, CIC로부터 전달되는 지시 메시지를 받지 못하는 일이 없도록 해야합니다.

#### Ping-pong 수행 {#DoPingpong}

CIC와 연결이 유지되고 있는지 파악하기 위해 클라이언트는 1분 간격으로 HTTP/2 PING 프레임을 CIC로 전송해야 합니다. CIC로부터 HTTP/2 PING ACK 응답을 받지 못하면 클라이언트는 즉시 새로운 연결을 구성해 클라이언트와 CIC간의 연결이 지속될 수 있도록 해야합니다. HTTP/2 PING 프레임에 대한 자세한 설명은 [HTTP/2 PING Payload Format](https://http2.github.io/http2-spec/#rfc.figure.12)을 참조합니다.

<div class="note">
  <p><strong>Note!</strong></p>
  <p>HTTP/2 PING 프레임을 전송할 수 없으면 클라이언트는 1분마다 <code>GET</code> 요청을 <code>/ping</code>으로 보내야 합니다. 이때, HTTP 204 No Content 응답을 받게 됩니다. HTTP/2 PING 프레임을 사용할 때와 마찬가지로 응답을 받지 못하면, 클라이언트는 즉시 새로운 연결을 구성해야 합니다.</p>
  <p>다음은 <code>/ping</code>으로 <code>GET</code> 요청을 보내는 예제입니다.</p>
  <pre><code>:method = GET
:scheme = https
:path = /ping
User-Agent: [User-Agent_string]
Authorization: Bearer [YOUR_ACCESS_TOKEN]
</code></pre>
</div>

#### Access token 갱신 {#RefreshAccessToken}

클라이언트는 access token을 획득할 때 해당 access token이 언제 만료되는지 `expires_in` 필드에 명시된 만료 시간을 보고 파악해낼 수 있습니다. 이 시간이 만료되거나 만료된 access token을 사용하여 HTTP 401 Unauthorized의 상태 값을 가진 [오류 메시지](/CIC/References/CIC_API.md#Error)를 받은 경우 access token을 갱신해야 합니다. 아래와 같이 [Clova access token을 획득](/CIC/References/Clova_Auth_API.md#RequestClovaAccessToken)할 때 받았던 refresh token (`refresh_token`)과 갱신에 필요한 파라미터를 전달하면 [Clova access token을 갱신](/CIC/References/Clova_Auth_API.md#RefreshClovaAccessToken)할 수 있습니다.

<pre><code>$ curl {{ book.AuthServerBaseURL }}token?grant_type=refresh_token \
       --data-urlencode "client_id=c2Rmc2Rmc2FkZ2FzZnNhZGZ" \
       --data-urlencode "client_secret=66qo65asdfasdfaA7JasdfasfOqwnOq1rOyfgeydtCDrvYasfasf%3D" \
       --data-urlencode "refresh_token=GW-Ipsdfasdfdfs3IbHFBA" \
       --data-urlencode "device_id=aa123123d6-d900-48a1-b73b-aa6c156353206" \
       --data-urlencode "model_id=test_model"
</code></pre>
