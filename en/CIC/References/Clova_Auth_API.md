# Clova Auth API
To establish a connection between your client and CIC, it is required to [create a Clova access token](/CIC/Guides/Interact_with_CIC.md#CreateClovaAccessToken). This document explains the Clova Auth API, which is provided by the Clova authorization server to help you with the token creation.


## Base URL
The base URL of the Clova authorization server is as follows.

<pre><code>{{ book.AuthServerBaseURL }}
</code></pre>

## /authorize {#authorize}
Returns a response message containing an authorization code by receiving a {{ book.TargetServiceForClientAuth }} account access token and [client credentials](/CIC/Guides/Interact_with_CIC.md#ClientAuthInfo) provided as parameters. An authorization code is credential information which is returned at a step prior to issuance of a Clova access token.

<div class="note">
  <p><strong>Note!</strong></p>
  <p>Typically, user authentication is handled by an app paired with a client device. However, transferring a Clova access token directly to a client from a paired app may have a security issue. As such, an authorization code is sent to your client alternatively. Your client should provide the returned authorization code to the <a href="#token">/token</a> API parameters and obtain a Clova access token.</p>
</div>

### Scheme, method, path
{% raw %}
```
:method = {{GET|POST}}
:scheme = https
:path = /authorize
```
{% endraw %}

### Parameter
| Field name  | Type  | Field description  | Required |
|---------------|---------|-----------------------------|---------|
| client_id  | string  | Client ID (See [Client credentials](/CIC/Guides/Interact_with_CIC.md#ClientAuthInfo))  | Yes |
| device_id  | string  | The UUID of the client device created  | Yes |
| model_id  | string  | The model ID of the client device  | No |
| response_type | string  | Response type. Only "code" is supported at the moment. | Yes  |
| state  | string  | The value of the state token (URL encoding applied) used by a client to prevent cross-site request forgery attacks | Yes |

### Request Example

<pre><code>{{ book.AuthServerBaseURL }}/authorize?client_id=7Jlaksjdflq1rOuTpA%3D%3D
                                            &device_id=test_device
                                            &model_id=test_model
                                            &response_type=code
                                            &state=95%2FKjaJfMlakjdfTVbES5ccZQ%3D%3D
</code></pre>

### Response field
| Field name  | Type  | Field description  |
|---------------|---------|-----------------------------|
| code  | string | The authorization code issued from the authorization server  |
| state | string | The decrypted value of the state token (URL decoding applied) passed from a client to prevent cross-site request forgery attacks |


### Response Example
{% raw %}
```
{
    "code": "cnl__eCSTdsdlkjfweyuxXvnlA",
    "state": "95/KjaJfMlakjdfTVbES5ccZQ=="
}
```
{% endraw %}

### See also
* [Client credentials](/CIC/Guides/Interact_with_CIC.md#ClientAuthInfo)
* [Creating Clova access token](/CIC/Guides/Interact_with_CIC.md#CreateClovaAccessToken)
* [/token](#token)


## /token {#token}
Creates, refreshes, or deletes a Clova access token using an authorization code issued by the [/authorize](#authorize) API. The API performs different actions and returns different values depending on the value of the *grant_type* parameter.

### Scheme, method, path
{% raw %}
```
:method = {{GET|POST}}
:scheme = https
:path = token
```
{% endraw %}

### Parameter
| Field name  | Type  | Field description  | Required |
|---------------|---------|-----------------------------|---------|
| access_token  | string  | The Clova access token issued after authorization succeeded. This field is required when *grant_type* is "delete".  | No |
| client_id  | string  | Client ID (See [Client credentials](/CIC/Guides/Interact_with_CIC.md#ClientAuthInfo))  | Yes |
| client_secret | string  | Client Secret (See [Client credentials](/CIC/Guides/Interact_with_CIC.md#ClientAuthInfo))  | Yes |
| code  | string  | The authorization code issued by the [/authorize](#authorize) API. This field is required when *grant_type* is "authorization_code".  | No |
| device_id  | string  | The UUID of the client device created  | Yes |
| grant_type  | string  | Action identifier. <ul><li>"authorization_code": Token is issued</li><li>"refresh_token": Token is refreshed</li><li>"delete": Token is deleted</li></ul> | Yes |
| model_id  | string  | The model ID of the client device  | No |
| refresh_token | string  | The refresh token issued after authorization succeeded. This field is required when *grant_type* is "refresh_token".  | No |
| response_type | string  | Response type. Only "code" is supported at the moment. | Yes  |

### Request Example

<pre><code>{{ book.AuthServerBaseURL }}/token?client_id=7JWI64WVIsdfasdfrOuTpA%3D%3D
                                        &amp;client_secret=66qo65asdfasdfaA7JasdfasfOqwnOq1rOyfgeydtCDrvYasfasf%3D
                                        &amp;code=cnl__eCSTdsdlkjfweyuxXvnlA
                                        &amp;device_id=test_device
                                        &amp;grant_type=authorization_code
                                        &amp;model_id=test_model
</code></pre>

### Response field
| Field name  | Type  | Field description  |
|---------------|---------|-----------------------------|
| access_token  | string  | Clova access token  |
| expires_in  | number  | The valid time of the Clova access token (in seconds)  |
| refresh_token | string  | The refresh token to refresh the Clova access token  |
| token_type  | string  | The type of the Clova access token. Returns "Bearer". |

### Response Example
{% raw %}
```
{
    "access_token": "XHapQasdfsdfFsdfasdflQQ7w",
    "expires_in": 332000,
    "refresh_token": "GW-Ipsdfasdfdfs3IbHFBA",
    "token_type": "Bearer"
}
```
{% endraw %}

### See also
* [Client credentials](/CIC/Guides/Interact_with_CIC.md#ClientAuthInfo)
* [Creating Clova access token](/CIC/Guides/Interact_with_CIC.md#CreateClovaAccessToken)
* [/authorize](#authorize)
