# 사용자 계정 연결하기
Clova는 [custom extension](/CEK/Guides/Build_Custom_Extension.md)이나 [Clova Home extension](/CEK/Guides/Build_Clova_Home_Extension.md)을 통해 사용자 계정 권한이 필요한 외부 서비스를 제공할 수 있습니다. 예를 들면, 유료 콘텐츠 서비스인 음악 스트리밍 서비스나 쇼핑, 금융, 메신저, 홈 IoT 등과 같은 서비스가 Clova에 연동될 수 있습니다. 이를 위해, Clova는 외부 서비스의 사용자 계정과 Clova 사용자 계정을 연결하는 계정 연결(account linking)을 지원하며, 이 기술은 [OAuth 2.0](https://tools.ietf.org/html/rfc6749)을 이용합니다.

계정 연결은 사용자의 계정 인증(authentication)이 필요한 외부 서비스를 custom extension이 제공해야 할 때 사용됩니다. 계정 인증이 필요 없는 외부 서비스는 계정 연결을 하지 않아도 되며, 사용자 식별이 가능한 수준의 정보가 요구되는 서비스는 일반적으로 [custom extension 메시지](/CEK/References/CEK_API.md#CustomExtMessage)가 제공하는 기기 식별자(`context.System.device.deviceId`)와 사용자 계정 식별자(`context.System.user.userId` 또는 `session.user.userId`)를 조합한 값을 이용합니다.

<div class="note">
<p><strong>Note!</strong></p>
<p>Clova Home extension은 반드시 계정 연결을 해야 합니다.</p>
</div>

이 문서는 다음과 같은 내용을 다룹니다.
* [계정 연결 동작 이해하기](#UnderstandAccountLinking)
* [계정 연결 적용하기](#ApplyAccountLinking)

## 계정 연결 동작 이해하기 {#UnderstandAccountLinking}
계정 연결을 extension에 적용하기 전에 우선 계정 연결 동작에 대해 이해할 필요가 있습니다. 여기에서는 다음과 같은 내용을 설명합니다.
* [계정 연결 설정](#SetupAccountLinking)
* [계정 연결 후 extension 호출](#ExtensionInvokingAfterAccountLinking)

### 계정 연결 설정 {#SetupAccountLinking}
사용자가 계정 인증이 필요한 custom extension이나 Clova Home extension을 활성화하면 다음과 같이 계정 연결 설정을 시도합니다.

![](/CEK/Resources/Images/CEK_Account_Linking_Setup_Sequence_Diagram.png)

1. 사용자가 특정 custom extension이나 Clova Home extension을 활성화합니다.

2. 클라이언트 앱 또는 클라이언트 기기와 페어링하는 앱에서 외부 서비스의 로그인 페이지를 표시합니다. 이때, extension 개발자가 미리 등록해 둔 인증 서버의 **[Authorization URL](#BuildAuthServer)**을 이용합니다.

3. 사용자가 계정 인증을 완료하면 authorization code 혹은 access token이 반환됩니다.

4. 전달받은 authorization code 혹은 access token은 redirect URL을 통해 Clova로 전달됩니다.

5. **(3번 단계에서 authorization code를 받은 경우)** Clova는 **[Access Token URI](#RegisterAccountLinkingInfo)**로 access token과 refresh token을 요청합니다. 이때 authorization code를 전달하며, 사용자의 Clova 계정 정보에 획득한 access token과 refresh token을 저장합니다.

6. 이제 사용자는 계정 인증이 필요한 서비스를 사용할 수 있습니다.

<div class="note">
<p><strong>Note!</strong></p>
<p>사용자가 특정 custom extension이나 Clova Home extension을 비활성화한 경우 사용자의 Clova 계정에 저장된 access token을 제거합니다. 따라서, 사용자가 해당 extension을 재활성화하면, 계정 연결을 다시 수행해야 합니다.</p>
</div>

### 계정 연결 후 extension 호출 {#ExtensionInvokingAfterAccountLinking}
계정 연결이 완료된 상태에서 CEK는 다음과 같은 순서로 extension을 호출하게 됩니다.

1. 사용자의 요청을 처리하기 위해 평상시처럼 extension을 호출합니다.

2. **(만약 access token이 만료된 경우)** refresh token을 이용하여 **[Access Token URI](#RegisterAccountLinkingInfo)**에 새로운 access token을 요청합니다.

3. Extension에 전달하는 메시지에 access token을 포함시켜 사용자의 요청을 전달합니다.
   * Custom extension의 경우 `context.System.user.accessToken`와 `session.user.accessToken` 필드에 access token이 전달됩니다.
   * Clova Home extension의 경우 `payload.accessToken` 필드에 access token이 전달됩니다.

4. Extension은 상황에 따라 다음과 같이 응답해야 합니다.
   * Access token이 유효한 경우, 사용자의 요청을 처리하고 그 결과를 반환해야 합니다.
   * Access token이 유효하지 않은 경우, [계정 연결 설정](#SetupAccountLinking)이 진행될 수 있도록 결과를 반환해야 합니다.

## 계정 연결 적용하기 {#ApplyAccountLinking}
개발하는 extension에 계정 연결을 적용하려면 다음을 수행해야 합니다.

1. [인증 서버 구축](#BuildAuthServer)
2. [계정 권한 검증 구현](#AddValidationLogic)
3. [계정 연결 정보 등록](#RegisterAccountLinkingInfo)

### 인증 서버 구축 {#BuildAuthServer}

Extension에 계정 연결을 적용하려면 우선 사용자가 계정 인증을 수행할 수 있는 로그인 페이지를 제공해야 하며, 인증 처리 후 access token을 발급하는 서버를 구축해야 합니다.

사용자 인증을 위해 제공할 로그인 페이지는 다음과 같은 사항을 만족하거나 수행해야 합니다.
* HTTPS 프로토콜로 페이지를 제공해야 합니다.
* 모바일용 페이지를 지원해야 합니다.
* 팝업 형태의 창을 제공하면 안됩니다.
* 인증이 완료되면 redirect URL(`redirect_uri`)로 이동해야 합니다. 이때, authorization code 또는 access token을 파라미터로 전송해야 합니다.
* `state` 파라미터를 redirect URL(`redirect_uri`)로 계속 전달해야 합니다.


사용자가 계정을 인증할 수 있도록 로그인 UI를 제공하는 페이지의 주소를 **Authorization URL**이라 부르며, Clova Developer Console에 미리 등록해야 합니다. 사용자가 extension의 계정 연결을 사용하도록 설정할 때 이 URL이 다음 파라미터와 함께 호출됩니다.

| 파라미터 이름     | 설명                                         |
|---------------|---------------------------------------------|
| `state`         | 인증 세션의 시간 만료 여부를 확인하는 상태 값. 이 값은 5분 뒤에 만료되므로 사용자가 인증을 5분 안에 마치지 않으면 인증을 다시 시도해야 합니다. |
| `client_id`     | Clova가 외부 서비스의 access token을 발급 받기 위해 사용할 ID. 개발자는 Clova Developer Console을 통해 미리 `cliend_id`를 등록해둬야 합니다. |
| `response_type` | OAuth 2.0 인가 타입(`"code"` 또는 `"token"`)을 정의해 둔 파라미터. 높은 보안이 필요한 경우 `"code"` 타입을 사용합니다. Clova Home extension은 항상 `"code"` 타입을 사용합니다. Clova Developer Console를 통해 미리 `reponse_type`을 등록해둬야 합니다. |
| `scope`         | OAuth의 `scope` 필드. 접근 수준을 정의할 수 있습니다. Clova Developer Console를 통해 미리 `scope`를 등록해둬야 합니다. |
| `redirect_uri`  | 계정 인증 후 이동할 URL(redirect URL)이며, `redirect_uri`의 값은 Clova Developer Console에서 통해 미리 확인할 수 있습니다. |

<div class="note">
<p><strong>Note!</strong></p>
<p>파라미터에 대한 자세한 설명은 OAuth 2.0 Authorization Framework의 <a href="https://tools.ietf.org/html/rfc6749#section-4">Obtaining Authorization</a>을 참고합니다.</p>
</div>

다음은 클라이언트 앱 또는 클라이언트 기기와 페어링하는 앱이 로그인 페이지를 요청하는 URL 예입니다.

{% raw %}
```
https://yourdomain.com/login?state=qwer123
                            &client_id=clova-extension
                            &scope=listen_music%20basic_profile
                            &response_type=code
                            &redirect_uri=ToBeDetermined
```
{% endraw %}


<div class="note">
<p><strong>Note!</strong></p>
<p><code>redirect_uri</code>는 추후 Clova Developer Console를 통해 제공될 예정입니다. 따라서, <code>redirect_uri</code>에 대한 정보는 제휴 담당자에게 문의하기 바랍니다.</p>
</div>


계정 인증 후 이동할 URL(`redirect_uri`)에는 다음과 같은 파라미터를 전달해야 합니다.

| 파라미터 이름     | 설명                                        |
|---------------|---------------------------------------------|
| `vendorId`      | Extension 개발자에게 부여된 ID. 외부 서비스 또는 기업을 구분하기 위해 Clova Developer Console에 등록된 ID입니다. `redirect_uri`에 미리 포함되어 있습니다. |
| `state`         | 인증 세션의 시간 만료 여부를 확인하는 상태 값. **Authorization URL**을 통해 전달받은 `state` 파라미터를 그대로 입력합니다.    |
| `code`          | Authorization code. `response_type` 값이 `"code"`이면, 이 파라미터에 authorization code를 입력합니다.  |
| `access_token`  | Access token. `response_type` 값이 `"token"`이면, 이 파라미터에 access token을 입력합니다.               |
| `token_type`    | Access token의 타입. `access_token`과 함께 전달해야 하며, `"Bearer"`로 고정됩니다.                        |



다음은 사용자의 계정 인증이 완료된 후 이동할 redirect URL 예입니다.

{% raw %}
```
// 예제 1: Authorization code grant 방식을 사용할 경우
https://ToBeDetermined/?vendorId=YourServiceOrCompanyID
                                &state=qwer123
                                &code=nl__eCSTdsdlkjfweyuxXvnl

// 예제 2: Implicit grant 방식을 사용할 경우
https://ToBeDetermined/?vendorId=YourServiceOrCompanyID
                                &state=qwer123
                                &access_token=sdfljnFZFEjr1zCsicM
                                &token_type=Bearer
```
{% endraw %}


Clova가 사용자 계정 연결을 위해 Authorization code를 획득한 경우(authorization code grant 방식), Clova는 다시 extension 개발자가 Clova Developer Console에 미리 등록해 둔 **[Access Token URI](#RegisterAccountLinkingInfo)**로 access token을 요청하게 됩니다. 이때, Clova는 획득한 authorization code를 파라미터로 전송하게 되며, 인증 서버는 외부 서비스의 계정 권한이 부여된 access token과 access token을 갱신할 수 있는 refresh token을 발급해야 합니다.

Clava가 사용자 계정 연결을 위해 access token을 바로 획득한 경우(implicit grant 방식), refresh token을 발급받지 않으며 access token이 만료되면 사용자 계정 연결을 다시 시도해야 합니다.

<div class="note">
  <p><strong>Note!</strong></p>
  <p>현재 Clova Developer Console을 개발하는 중입니다. 따라서, Clova Developer Console를 통해 미리 등록해야 하는 <code>Authorization URL</code>, <code>Access Token URI</code>나 파라미터 값은 제휴 담당자를 통해 전달하면 됩니다.</p>
</div>

### 계정 권한 검증 구현 {#AddValidationLogic}
계정 연결을 적용하려면 extension 개발자는 access token이 유효한지 검증하는 코드를 작성해야 합니다. Custom extension과 Clova Home extension으로 전달되는 extension 메시지는 각각 다음과 같은 `accessToken` 필드를 가지고 있습니다.
아래 필드에서 access token을 확인한 후 해당 access token이 존재하며 유효한 값인지 확인해야 합니다.

* Custom extension : `context.System.user.accessToken`, `session.user.accessToken`
* Clova Home extension : `payload.accessToken`

{% raw %}
```json
// 예제 1: Custom extension 메시지 예
{
  "version": "0.1.0",
  "session": {
    "new": false,
    "sessionAttributes": {},
    "sessionId": "a29cfead-c5ba-474d-8745-6c1a6625f0c5",
    "user": {
      "userId": "V0qe",
      "accessToken": "XHapQasdfsdfFsdfasdflQQ7"
    }
  },
  "context": {
    "System": {
      "user": {
        "userId": "V0qe",
        "accessToken": "XHapQasdfsdfFsdfasdflQQ7"
      },
      "device": {
        "deviceId": "096e6b27-1717-33e9-b0a7-510a48658a9b",
        "displayType": "m100"
      }
    }
  },
  "request": {
    "type": "IntentRequest",
    "intent": {
      "name": "FreeTalk",
      "slots": {
        "q": {
          "name": "q",
          "value": "How are you"
        }
      }
    }
  }
}

// 예제 2: Clova Home extension 메시지 예
{
  "header": {
    "messageId": "33da6561-0149-4532-a30b-e0de8f75c4cf",
    "name": "HealthCheckRequest",
    "namespace": "ClovaHome",
    "payloadVersion": "1.0"
  },
  "payload": {
    "accessToken": "92ebcb67fe33"
  }
}
```
{% endraw %}

<div class="note">
  <p><strong>Note!</strong></p>
  <p>만약, access token이 존재하지 않거나 유효하지 않다면 클라이언트가 사용자 계정을 다시 연결하도록 CEK에게 응답을 보내야 합니다.</p>
</div>



### 계정 연결 정보 등록 {#RegisterAccountLinkingInfo}
인증 서버 구축과 extension에 계정 연결을 적용하는 것이 완료되면 Clova Developer Console에 [인증 서버 구축](#BuildAuthServer)에서 언급했던 정보를 등록해야 합니다. Clova Developer Console에 등록된 extension에서 다음과 같은 계정 연결 정보를 입력합니다.

| 필드 이름           | 설명                                         |
|-------------------|---------------------------------------------|
| Authorization URL | 사용자가 [계정 인증](#SetupAccountLinking)을 위해 접속할 URL                            |
| Client ID         | 사용자 [계정 인증](#SetupAccountLinking) 페이지를 요청할 때 서비스를 식별하기 위해 부여한 ID    |
| Authorization Grant Type | OAuth 2.0의 인가 방식. <ul><li>Implicit grant 방식(custom extension 적용 가능)</li><li>Authorization code grant 방식(custom extension, Clova Home extension 적용 가능)</li></ul>    |
| Access Token URI  | Authorization code로 access token을 획득하기 위한 주소. Authorization code grant 방식을 설정한 경우 입력합니다. |
| Client Secret     | Authorization code로 access token을 획득할 때 **Client ID**와 함께 전달되어야 하는 Secret. Authorization code grant 방식을 설정한 경우 입력합니다. |
| Client Authentication Scheme | Access Token URI로 access token을 요청할 때 사용하는 scheme              |
| Privacy Policy URL | 서비스와 관련하여 개인 정보 보호 정책과 관련된 내용이 제공되는 페이지. Clova App이나 페어링 앱에 표시됩니다. |

<div class="note">
  <p><strong>Note!</strong></p>
  <p>현재 Clova Developer Console을 개발하는 중입니다. 따라서, Clova Developer Console를 통해 미리 등록해야 하는 정보는 제휴 담당자를 통해 등록하시기 바랍니다.</p>
</div>
