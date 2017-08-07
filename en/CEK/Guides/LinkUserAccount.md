# Linking user account
Clova lets you provide 3rd party services that require access to users' accounts by using [custom extension](/CEK/Guides/Build_Custom_Extension.md) or [Clova Home extension](/CEK/Guides/Build_Clova_Home_Extension.md). For example, services that provide paid music streaming, shopping, banking, messaging or home IoT can connect with Clova. To this end, Clova provides the account linking feature with which you can link user accounts of the 3rd party service with those of Clova, using [OAuth 2.0](https://tools.ietf.org/html/rfc6749) technology.

Account linking is necessary if your custom extension provides a service that requires authentication of user accounts. If the 3rd party service does not require user authentication, you do no have to provide account linking. If the service requires information just enough to identify users, you can combine device identifier (*context.System.device.deviceId*) and user account identifier (*context.System.user.userId* or *session.user.userId*), both of which are provided in a [custom extension message](/CEK/References/Custom_Extension_Message_Format.md).

<div class="note">
<p><strong>Note!</strong></p>
<p>Clova Home extension always requires account linking.</p>
</div>

This page covers the following topics.
* [Understanding how account linking works](#UnderstandAccountLinking)
* [Applying account linking](#ApplyAccountLinking)

## Understanding how account linking works {#UnderstandAccountLinking}
Before applying account linking to your extension, you have to understand how account linking works. This section explains the following:
* [Setting up account linking](#SetupAccountLinking)
* [Invoking extension after account linking](#ExtensionInvokingAfterAccountLinking)

### Setting up account linking {#SetupAccountLinking}
When a user enables a custom extension or Clova Home extension that requires account authentication, the user can try to link his or her account in the following steps.

![](/CEK/Resources/Images/CEK_Account_Linking_Setup_Sequence_Diagram.png)

1. The user enables a custom extension or Clova Home extension.

2. A client app or app paired with a client device displays a login page of the 3rd party service, using the *[authorization URL](#BuildAuthServer)* previously registered for the authorization server.

3. When the user completes account authentication, an authorization code or access token is returned.

4. The authorization code or access token is forwarded to Clova using the specified redirect URL.

5. **(If the user received authorization code in step 3)** Clova requests access token and refresh token to *[Access Token URI](#RegisterAccountLinkingToCEK)*. At which point, the authorization code is passed on and the access token and refresh token are stored in the user's Clova account information.

6. The user is now able to use the service that requires account authentication.

<div class="note">
<p><strong>Note!</strong></p>
<p>When a user disables a custom extension or Clova Home extension, the existing access token stored in the user's Clova account will be removed. This means the user will have to do account linking again when the person enables the extension again.</p>
</div>

### Invoking extension after account linking {#ExtensionInvokingAfterAccountLinking}
After account linking is completed, CEK invokes the extension in the following steps.

1. Invokes the extension as usual to process a user request.

2. **(If the access token has expired)** Requests a new access token to *[Access Token URI](#RegisterAccountLinkingToCEK)* using the refresh token.

3. Sends a user request to the extension with the access token.
   * In case of custom extension, the access token is passed to *context.System.user.accessToken* and *session.user.accessToken* fields.
   * In case of Clova Home extension, the access token is passed to *payload.accessToken* field.

4. The extension responds as follows.
   * If the access token is valid, it must process the user request and return a result.
   * If the access token is invalid, it must return a result to proceed [account linking](#SetupAccountLinking).

## Applying account linking {#ApplyAccountLinking}
To apply account linking to your extension, do as follows.

1. [Build authorization server](#BuildAuthServer)
2. [Validate account access permission](#AddValidationLogic)
3. [Register account linking information](#RegisterAccountLinkingInfo)

### Build authorization server {#BuildAuthServer}

To apply account linking to your extension, you must prepare a login page where users can authenticate their accounts and build a server that issues an access token after users complete authentication.

The login page for user authentication must meet the following requirements.
* The page shall support the HTTPS protocol.
* The page shall support pages for mobile.
* The page shall not provide any pop-up window.
* The page shall be redirected to a specified URL (*redirect_uri*) after authentication is complete. And, at which point, the authorization code or access token shall be passed as a parameter.
* The page shall keep sending the *state* parameter to the redirect URL (*redirect_uri*).


You must register an *Authorization URL* in Clova Developer Console in advance, which is the address of a login page where users can authenticate their accounts. This URL is called with the following parameters when users try account linking with your extension.

| Parameter name     | Description                                         |
|---------------|---------------------------------------------|
| state         | State value used to check whether the authentication session has timed out or not. The value expires in 5 minutes. If the user fails to complete authentication in 5 minutes, the user must try authentication again. |
| client_id     | ID used when Clova requests a 3rd party service to issue an access token. You must register *client_id* in Clova Developer Console in advance. |
| response_type | Parameter that defines the OAuth 2.0 authorization type ("code" or "token"). Use "code" if high level security is required. Clova Home extension always uses the "code" type. You must register *reponse_type* in Clova Developer Console in advance. |
| scope         | scope field in OAuth. It defines access level. You must register *scope* in Clova Developer Console in advance. |
| redirect_uri  | URL to be redirected to after account authentication is complete (redirect URL). You can obtain the value of *redirect_uri* in Clova Developer Console in advance. |

<div class="note">
<p><strong>Note!</strong></p>
<p>Refer to <a href="https://tools.ietf.org/html/rfc6749#section-4">Obtaining Authorization</a> in OAuth 2.0 Authorization Framework for more details on the parameter.</p>
</div>

This is an example URL used when a client app or app paired with a client device requests a login page.

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
<p><em>redirect_uri</em> will be available in Clova Developer Console in the future. Contact your counterpart contact personnel to ask for help with obtaining <em>redirect_uri</em>.</p>
</div>


You must pass the following parameters to the URL (*redirect_uri*) to be redirected to after account authentication is complete.

| Parameter name     | Description                                        |
|---------------|---------------------------------------------|
| vendorId      | ID given to the extension developer. The ID is registered in Clova Developer Console to identify 3rd party service or company. It is pre-included in *redirect_uri*. |
| state         | State value used to check whether the authentication session has timed out or not. Enter the *state* parameter passed in the *Authorization URL*.    |
| code          | Authorization code. If *response_type* is "code", enter "authorization code" to this parameter.  |
| access_token  | Access token. If *response_type* is "token", enter "access token" to this parameter.               |
| token_type    | Type of the access token. It is passed along with *access_token*. The value is fixed to "Bearer".                        |



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


If Clova has obtained an authorization code (authorization code grant), Clova requests access token to the *[Access Token URI](#RegisterAccountLinkingToCEK)* previously registered in Clova Developer Console. At which point, Clova passes the authorization code as a parameter. Then the authorization server issues an access token granting account access for the 3rd party service and a refresh token for refreshing the access token.

If Clova has obtained an access token directly (implicit grant), it does not receive a refresh token. Therefore, when the access token expires, the user must try account linking again.

<div class="note">

<p><strong>Note!</strong></p>  <p>Clova Developer Console is still under development. Contact your counterpart contact personnel to ask for help with obtaining <em>Authorization URL</em>, <em>Access Token URI</em> or any other parameter values.</p>
</div>

### Validating account access permission {#AddValidationLogic}
To apply account linking, you must write code for checking the validity of an access token. When an extension message is sent to custom extension or Clova Home extension, the following *accessToken* field is included in each message.
You must verify that the access token is present in the field and that it is valid.

* Custom extension: *context.System.user.accessToken*, *session.user.accessToken*
* Clova Home extension: *payload.accessToken*

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

<p><strong>Note!</strong></p>  <p>If the access token is missing or invalid, you must return a response to CEK asking the client to retry account linking.</p>
</div>



### Registering account linking information {#RegisterAccountLinkingInfo}
Once you are done with building an authorization server and applying account linking to your extension, you must register the information mentioned in [Building authorization server](#BuildAuthServer) in Clova Developer Console. Go to Clova Developer Console and add the following account linking information in your extension.

| Field name           | Description                                         |
|-------------------|---------------------------------------------|
| Authorization URL | URL to access for [account authentication](#SetupAccountLinking)                            |
| Client ID         | Unique ID used to identify a service when requesting [account authentication](#SetupAccountLinking) page    |
| Authorization Grant Type | OAuth 2.0 authorization method. <ul><li>Implicit grant (applicable to custom extension)</li><li>Authorization code grant (applicable to custom extension and Clova Home extension)</li></ul>    |
| Access Token URI  | Address for obtaining an access token using an authorization code. Enter an appropriate value when you have selected authorization code grant. |
| Client Secret     | Secret which has to be passed along with *Client ID* when obtaining an access token using an authorization code. Enter an appropriate value when you have selected authorization code grant. |
| Client Authentication Scheme | Scheme used when requesting an access token to Access Token URI              |
| Privacy Policy URL | Page that provides privacy policy for the service. It is displayed on Clova App or paired app. |

<div class="note">
  <p><strong>Note!</strong></p>
  <p>Clova Developer Console is still under development. Contact your counterpart contact personnel to ask for help with registering information in Clova Developer Console.</p>
</div>
