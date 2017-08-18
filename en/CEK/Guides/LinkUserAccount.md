# Linking user account
Through your [custom extension](/CEK/Guides/Build_Custom_Extension.md) or [Clova Home extension](/CEK/Guides/Build_Clova_Home_Extension.md), Clova can provide 3rd party services that require access to user accounts. You can make Clova interact with a paid content service (like music streaming) or 3rd party services for shopping, banking, messaging, and home IoT. To this end, Clova supports account linking on a basis of [OAuth 2.0](https://tools.ietf.org/html/rfc6749) technology, in short, linking user accounts of a 3rd party service with those of Clova.

Implement account linking if your custom extension provides a 3rd party service that requires users to authenticate their accounts. If the 3rd party service does not require account authentication, account linking is not necessary. If the service requires information just enough to identify users, you can use the combination of values for device identifier (`context.System.device.deviceId`) and user account identifier (`context.System.user.userId` or `session.user.userId`), both of which are included in [custom extension messages](/CEK/References/Custom_Extension_Message_Format.md).

<div class="note">
<p><strong>Note!</strong></p>
<p>Clova Home extensions always require account linking.</p>
</div>

In the following, we will explain:
* [Understanding how account linking works](#UnderstandAccountLinking)
* [Applying account linking](#ApplyAccountLinking)

## Understanding how account linking works {#UnderstandAccountLinking}
Before applying account linking to your extension, you have to understand how account linking works. Here, the following topics are covered.
* [Setting up account linking](#SetupAccountLinking)
* [Invoking extension after account is linked](#ExtensionInvokingAfterAccountLinking)

### Setting up account linking {#SetupAccountLinking}
When a user enables a custom extension or Clova Home extension that requires account authentication, the user tries to link his or her account in the following steps.

![](/CEK/Resources/Images/CEK_Account_Linking_Setup_Sequence_Diagram.png)

1. The user enables a custom extension or Clova Home extension.

2. A client app or app paired with a client device displays a login page of the 3rd party service, using the *[Authorization URL](#BuildAuthServer)* which you have previously registered for the authorization server.

3. When the user completes account authentication, an authorization code or access token is returned.

4. The authorization code or access token is forwarded to Clova through the specified redirect URL.

5. **(If received an authorization code in step 3)** Clova requests access token and refresh token to the *[Access Token URI](#RegisterAccountLinkingToCEK)*. At which point, the authorization code is passed on and the access token and refresh token are stored in the user's Clova account information.

6. The user is now able to use the service that requires account authentication.

<div class="note">
<p><strong>Note!</strong></p>
<p>When a user disables a custom extension or Clova Home extension, the access token previously stored in the user's Clova account will be removed. In other words, the user will have to link the account again to re-enable the extension.</p>
</div>

### Invoking extension after account is linked {#ExtensionInvokingAfterAccountLinking}
After account linking is completed, CEK invokes the extension in the following steps.

1. Invokes the extension as usual to process a user request.

2. **(If the access token has expired)** Using the refresh token, requests a new access token to the *[Access Token URI](#RegisterAccountLinkingToCEK)*.

3. Sends a user request to the extension with the access token.
  * If it is a custom extension, the access token is passed to the `context.System.user.accessToken` and `session.user.accessToken` fields.
  * If it is a Clova Home extension, the access token is passed to the `payload.accessToken` field.

4. The extension responds as follows.
   * If the access token is valid, processes the user request and returns the result.
   * If the access token is invalid, returns the result to proceed to [setting up account linking](#SetupAccountLinking).

## Applying account linking {#ApplyAccountLinking}
To apply account linking to your extension, complete the following steps.

1. [Building authorization server](#BuildAuthServer)
2. [Validating account access permission](#AddValidationLogic)
3. [Registering account linking information](#RegisterAccountLinkingInfo)

### Building authorization server {#BuildAuthServer}

To apply account linking to your extension, prepare a login page where users can authenticate their accounts and build a server for issuing access tokens when authentication is complete.

The login page for user authentication must meet the following requirements.
* The page shall support the HTTPS protocol.
* The page shall support pages for mobile.
* The page shall not provide any pop-up window.
* The page shall be redirected to a specified URL (`redirect_uri`) after authentication is complete. And, at which point, an authorization code or access token shall be passed on as a parameter.
* The page shall keep sending the `state` parameter to the redirect URL (`redirect_uri`).


*Authorization URL* is an address of a login page where users can authenticate their accounts. You must register the URL in the Clova Developer Console in advance. This URL is called with the following parameters when users try to link their account with your extension.

| Parameter name  | Description  |
|---------------|---------------------------------------------|
| `state`  | A value that checks whether the authentication session has timed out or not. This value expires in 5 minutes, which means that users must retry authentication if they fail to complete it in 5 minutes. |
| `client_id`  | An ID which Clova uses to issue an access token for a 3rd party service. You must register `cliend_id` in advance in the Clova Developer Console. |
| `response_type` | A parameter that defines the OAuth 2.0 authorization type (**"code"** or **"token"**). Use the **"code"** type if high level security is required. Clova Home extensions always use **"code"**. You must register `reponse_type` in advance in the Clova Developer Console. |
| `scope`  | OAuth `scope` field. It defines an access level. You must register `scope` in advance in the Clova Developer Console. |
| `redirect_uri`  | A URL to be redirected to after account authentication is complte. You can obtain the `redirect_uri` value in advance from the Clova Developer Console. |

<div class="note">
<p><strong>Note!</strong></p>
<p>Refer to <a href="https://tools.ietf.org/html/rfc6749#section-4">Obtaining Authorization</a> in OAuth 2.0 Authorization Framework for more details on the parameters.</p>
</div>

This is an example URL when a client app or app paired with a client device requests a login page.

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
<p><code>redirect_uri</code> will be available in the Clova Developer Console in the future. In the meantime, contact your counterpart contact personnel to ask for help with obtaining <code>redirect_uri</code>.</p>
</div>


Pass the following parameters to the URL (`redirect_uri`) to be redirected to after account authentication is complete.

| Parameter name  | Description  |
|---------------|---------------------------------------------|
| `vendorId`  | An ID given to the extension developer. This ID is registered in the Clova Developer Console to identify 3rd party service or company. It is pre-included in `redirect_uri`. |
| `state`  | A value that checks whether the authentication session has timed out or not. Enter the `state` parameter passed from the *Authorization URL*.  |
| `code`  | Authorization code. If `response_type` is **"code"**, enter the authorization code to this parameter.  |
| `access_token`  | Access token. If `response_type` is **"token"**, enter the access token to this parameter.  |
| `token_type`  | The type of the access token. It is passed along with `access_token` and the value is always **"Bearer"**.  |



This is an example URL to be redirected to after user authentication is complete.

{% raw %}
```
// Example 1: Authorization code grant
https://ToBeDetermined/?vendorId=YourServiceOrCompanyID
                                &state=qwer123
                                &code=nl__eCSTdsdlkjfweyuxXvnl

// Example 2: Implicit grant
https://ToBeDetermined/?vendorId=YourServiceOrCompanyID
                                &state=qwer123
                                &access_token=sdfljnFZFEjr1zCsicM
                                &token_type=Bearer
```
{% endraw %}


If Clova has obtained an authorization code (authorization code grant), it requests an access token once more to the *[Access Token URI](#RegisterAccountLinkingToCEK)*, which you have previously registered in the Clova Developer Console. At which point, Clova passes the authorization code as a parameter. Then the authorization server issues an access token granting account access for the 3rd party service and a refresh token for refreshing the access token.

If Clova has obtained an access token (implicit grant), it does not receive a refresh token. This means that the user must retry account linking if the access token expires.

<div class="note">
  <p><strong>Note!</strong></p>
  <p>The Clova Developer Console is currently under development. Contact your counterpart contact personnel to ask for help with obtaining <code>Authorization URL</code>, <code>Access Token URI</code> or any other parameters which you have to register in advance in the Clova Developer Console.</p>
</div>

### Validating account access permission {#AddValidationLogic}
To apply account linking, write code for checking validity of access tokens. When extension messages are sent to custom extension or Clova Home extension, each has the following `accessToken` field.
Verify that the access token is present in the field and that it is valid.

* Custom extension : `context.System.user.accessToken`, `session.user.accessToken`
* Clova Home extension : `payload.accessToken`

{% raw %}
```json
// Example 1: Custom extension message
{
  "version": "0.1.0",
  "session": {
    "new": false,
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
        "deviceId": "096e6b27-1717-33e9-b0a7-510a48658a9b"
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

// Example 2: Clova Home extension message
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
  <p>If the access token does not exist or is not valid, your extension must send a response to CEK and ask the client to try account linking.</p>
</div>



### Registering account linking information {#RegisterAccountLinkingInfo}
Once you are done with building an authorization server and applying account linking to your extension, register the information mentioned in [Building authorization server](#BuildAuthServer) at the Clova Developer Console. Go to the Clova Developer Console and add the following account linking information in your extension.

| Field name           | Description                                         |
|-------------------|---------------------------------------------|
| Authorization URL | The URL to connect to for [account authentication](#SetupAccountLinking)                            |
| Client ID         | The ID for identifying services when requesting for an [account authentication](#SetupAccountLinking) page    |
| Authorization Grant Type | OAuth 2.0 authorization method. <ul><li>Implicit grant (applicable for custom extensions)</li><li>Authorization code grant (applicable for both custom extensions and Clova Home extensions)</li></ul>    |
| Access Token URI  | An address for obtaining an access token using an authorization code. Enter this field when the method is set to the authorization code grant. |
| Client Secret     | A secret which has to be passed along with *Client ID* when obtaining an access token using an authorization code. Enter this field when the method is set to the authorization code grant. |
| Client Authentication Scheme | Scheme used when requesting an access token to Access Token URI              |
| Privacy Policy URL | A page that provides privacy policy for the service. It is displayed on Clova App or paired app. |

<div class="note">
  <p><strong>Note!</strong></p>
  <p>The Clova Developer Console is currently under development. Contact your counterpart contact personnel to ask for help with registering information in Clova Developer Console.</p>
</div>
