# Linking user accounts
Clova can provide 3rd party services that require permissions for user account access through a [custom extension](/CEK/Guides/Build_Custom_Extension.md) or [Clova Home extension](/CEK/Guides/Build_Clova_Home_Extension.md). For example, a music streaming service that is a paid content service or other services like shopping, finance, messenger, and home IoT can be connected to Clova. Clova supports account linking that connects the user account of the 3rd party service and the Clova user account through [OAuth 2.0](https://tools.ietf.org/html/rfc6749).

Account linking is used when a custom extension provides a 3rd party service that requires users to authenticate their accounts. Account linking is not required for 3rd party services that do not require authentication. If the service only requires information to identify users, you can use the combination of values for the device identifier (`context.System.device.deviceId`) and user account identifier (`context.System.user.userId` or `session.user.userId`) provided in the [custom extension message](/CEK/References/CEK_API.md#CustomExtMessage).

<div class="note">
<p><strong>Note!</strong></p>
<p>Clova Home extension must use account linking.</p>
</div>

This documentation includes the following topics:
* [Understanding account linking](#UnderstandAccountLinking)
* [Applying account linking](#ApplyAccountLinking)

## Understanding account linking {#UnderstandAccountLinking}
Before applying account linking to the extension, you must first understand how account linking works. This section covers the following topics:
* [Setting account linking](#SetupAccountLinking)
* [Invoking an extension after account linking](#ExtensionInvokingAfterAccountLinking)

### Setting account linking {#SetupAccountLinking}
When a user enables a custom extension or Clova Home extension that requires authentication, the account linking setup is conducted as follows:

![](/CEK/Resources/Images/CEK_Account_Linking_Setup_Sequence_Diagram.png)

1. The user enables a custom extension or Clova Home extension.

2. The login page of the 3rd party service is displayed on the client app or the app paired with the client device. This method uses the **[authorization URL](#BuildAuthServer)** of the authorization server registered by the extension developer.

3. Once the user completes the authentication, an authorization code or an access token is returned.

4. The received authorization code or access token is delivered to Clova through a redirect URL.

5. **If the authorization code was returned in Step 3,** Clova requests an access and refresh token to **[Access token URI](#RegisterAccountLinkingInfo)**. Then, the authorization code is delivered and the acquired access and refresh tokens are stored in the user’s Clova account information.

6. The user can now use the service that requires account authentication.

<div class="note">
<p><strong>Note!</strong></p>
<p>When a user disables a custom extension or Clova Home extension, the access token stored in the user’s Clova account is removed. Therefore, account linking must be performed again if the user enables the extension again.</p>
</div>

### Invoking an extension after account linking {#ExtensionInvokingAfterAccountLinking}
Once an account is linked, CEK invokes the extension as follows:

1. CEK invokes the extension as usual to handle the user request.

2. **If the access token is expired** a new access token is requested to **[Access token URI](#RegisterAccountLinkingInfo)** using the refresh token.

3. CEK sends user request by including the access token in the message to the extension.
   * If it is a custom extension, the access token is delivered to the `context.System.user.accessToken`and `session.user.accessToken` fields.
   * If it is a Clova Home extension, the access token is delivered to the `payload.accessToken` field.

4. The extension should respond as follows for the following conditions:
   * If the access token is valid, the extension must handle the user request and return the result.
   * If the access token is invalid, the extension must return the result to allow [setting account linking](#SetupAccountLinking).

## Applying account linking {#ApplyAccountLinking}
To apply account linking to the extension under development, complete the following steps:

1. [Building an authorization server](#BuildAuthServer)
2. [Implementing verification on account permissions](#AddValidationLogic)
3. [Registering account linking information](#RegisterAccountLinkingInfo)

### Building an authorization server {#BuildAuthServer}

To apply account linking to an extension, there must be a login page for the user to authenticate their account and also a server to issue an access token once authentication is complete.

The login page for user authentication must meet the following requirements:
* The page must be provided using the HTTPS protocol.
* The page must support mobile browsing.
* The page must not contain pop-up windows.
* The page must move to redirect URL(`redirect_uri`) once authentication is complete. And at this time, the authorization code or access token must be transferred as a parameter.
* The page must continue sending the `state` parameter to the redirect URL(`redirect_uri`).


The URL of the page providing the login UI for the user account authenticate is referred to as **Authorization URL** and it must be entered when [registering the extension](/DevConsole/Guides/CEK/Register_Extension.md) on the Clova developer console. When a user [sets to use account linking](/DevConsole/Guides/CEK/Register_Extension.md#SetAccountLinking) of the extension, **Authorization URL** is called along with the following parameters:

| Parameter     | Description                                         |
|---------------|---------------------------------------------|
| `state`         | State value used to check whether the authentication session has expired. This value expires after 5 minutes, so the user must re-authenticate once the session expires. |
| `client_id`     | The ID used by Clova to get the access token for the 3rd party service. You must register `cliend_id` in advance on the Clova developer console. |
| `response_type` | Parameter that has defined OAuth 2.0 authorization type (`"code"` or `"token"`). If high level of security if required, use the `"code"` type. Clova Home extensions always use the `"code"` type. You must register `reponse_type` in advance on the Clova developer console. |
| `scope`         | `scope` field of OAuth. You can define the access level. You must register `scope` in advance on the Clova developer console. |
| `redirect_uri`  | A URL to move to after authentication (redirect URL). The value of `redirect_uri` can be verified when [setting account linking](/DevConsole/Guides/CEK/Register_Extension.md#SetAccountLinking) to register the extension on the Clova developer console. Currently, `{{ book.RedirectURLforAccountLinking }}` is being used. |

<div class="note">
  <p><strong>Note!</strong></p>
  <p>For more information on parameters, see <a href="https://tools.ietf.org/html/rfc6749#section-4">Obtaining authorization</a> in the OAuth 2.0 authorization framework.</p>
</div>

Here is an example of a URL when a client app or app paired with a client device requests a login page.

<pre><code>https://yourdomain.com/login?state=qwer123
                            &client_id=clova-extension
                            &scope=listen_music%20basic_profile
                            &response_type=code
                            &redirect_uri={{ book.RedirectURLforAccountLinking }}
</code></pre>


<div class="note">
<p><strong>Note!</strong></p>
The <p><code>redirect_uri</code> can be found on the <a href="/DevConsole/Guides/CEK/Register_Extension.html#RedirectURI">Setting account linking</a> page of the Clova developer console.</p>
</div>


The URL to move after authentication (`redirect_uri`) must deliver the following parameters:

| Parameter     | Description                                        |
|---------------|---------------------------------------------|
| `vendorId`      | The ID assigned to the extension developer. This is an ID registered in the Clova developer console to differentiate a company or a 3rd party service. It is included in `redirect_uri` in advance. |
| `state`         | State value used to check whether the authentication session has expired. Enter the `state` parameter received from **Authorization URL**.    |
| `code`          | Authorization code. If the `response_type` value is `"code"`, enter the authorization code in the parameter.  |
| `access_token`  | Access token. If the `response_type` value is `"token"`, enter the access token in the parameter.               |
| `token_type`    | Type of access token. It must be delivered with `access_token` and the value is always set as `"Bearer"`.                        |

Here is an example of a redirect URL to move to once user account authentication is complete.

<pre><code>// Example 1: If authorization code grant method is used
{{ book.RedirectURLforAccountLinking }}?vendorId=YourServiceOrCompanyID
                                &state=qwer123
                                &code=nl__eCSTdsdlkjfweyuxXvnl

// Example 2: If implicit grant method is used
{{ book.RedirectURLforAccountLinking }}?vendorId=YourServiceOrCompanyID
                                &state=qwer123
                                &access_token=sdfljnFZFEjr1zCsicM
                                &token_type=Bearer
</code></pre>


If Clova acquires an authorization code for account linking (authorization code grant method), Clova requests an access token again to the **[access token URI](#RegisterAccountLinkingInfo)**, which is preregistered in the Clova developer console by the extension developer. Clova sends the acquired authorization code as a parameter, then the authorization server must issue an access token with permission to access the account of the 3rd party service and a refresh token to renew the access token.

If Clova immediately acquires an access token for account linking (implicit grant method), it does not receive a refresh token. Thus, you must perform account linking again once the access token is expired.

### Implementing verification on account permissions {#AddValidationLogic}
To apply account linking, the extension developer must write the code for verifying the validity of the access token. Each extension message delivered to the custom extension and Clova Home extension contains the `accessToken` fields as shown below.
Once you obtain the access token from the fields below, you must check the existence and validity of this value.

* Custom extension: `context.System.user.accessToken`, `session.user.accessToken`
* Clova Home extension: `payload.accessToken`

{% raw %}
```json
// Example 1: Example of a custom extension message
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
      "application": {
        "applicationId": "com.yourdomain.extension.pizzabot"
      },
      "user": {
        "userId": "V0qe",
        "accessToken": "XHapQasdfsdfFsdfasdflQQ7"
      },
      "device": {
        "deviceId": "096e6b27-1717-33e9-b0a7-510a48658a9b",
        "display": {
          "size": "l100",
          "orientation": "landscape",
          "dpi": 96,
          "contentLayer": {
            "width": 640,
            "height": 360
          }
        }
      }
    }
  },
  "request": {
    "type": "IntentRequest",
    "intent": {
      "name": "OrderPizza",
      "slots": {
        "pizzaType": {
          "name": "pizzaType",
          "value": "Pepperoni"
        }
      }
    }
  }
}

// Example 2: Example of a Clova Home extension message
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
  <p>If an access token does not exist or is invalid, the extension must send a response to CEK to ask the client to perform account linking again.</p>
</div>


### Registering account linking information {#RegisterAccountLinkingInfo}
Once building an authorization server and applying account linking to the extension are complete, you should register the information mentioned in [building an authorization server](#BuildAuthServer) on the [Clova developer console](/DevConsole/ClovaDevConsole_Overview.md). In the extension registered on the Clova developer console, [enter the account linking information](/DevConsole/Guides/CEK/Register_Extension.md#SetAccountLinking) as follows:

| Field           | Description                                         |
|-------------------|---------------------------------------------|
| Authorization URL | URL the user will access for [account authentication](#SetupAccountLinking)                            |
| Client ID         | Client ID granted to differentiate services when requesting the user [account authentication](#SetupAccountLinking) page    |
| Authorization grant type | Authorization method of OAuth 2.0. <ul><li>Implicit grant method (applicable to custom extensions)</li><li>Authorization code grant method (Applicable to custom extensions and Clova Home extensions)</li></ul>    |
| Access token URI  | Address to acquire an access token with the authorization code. Enter this field if the authorization code grant method is set. |
| Client secret     | Client secret that must be delivered with **Client ID** when acquiring an access token with the authorization code. Enter this field if the authorization code grant method is set. |
| Client authentication scheme | Scheme used when requesting access token with the access token URI.              |
| Privacy policy URL | Page where privacy policy details on the service are provided. It is displayed on the Clova app or paired app. |

