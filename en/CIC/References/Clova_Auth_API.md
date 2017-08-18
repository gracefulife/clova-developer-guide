# Clova Auth API
To connect your client with CIC, you must [create a Clova access token](/CIC/Guides/Interact_with_CIC.md#CreateClovaAccessToken). In the following, we will explain the Clova Auth API, which is provided by the Clova authorization server to help you with the token creation.

## Base URL
The base URL of the Clova authorization server is as follows.

<pre><code>{{ book.AuthServerBaseURL }}
</code></pre>

## /authorize {#authorize}
Returns an authorization code by receiving {{ book.TargetServiceForClientAuth }} account access token and [client credentials](/CIC/Guides/Interact_with_CIC.md#ClientAuthInfo) as parameters. An authorization code is credential information necessary for requesting issuance of a Clova access token.

<div class="note">
  <p><strong>Note!</strong></p>
  <p>Typically, user authentication is handled by an app paired with a client device. However, transferring a Clova access token from paired app to client may have a potential security issue. As such, the paired app returns an authorization code instead. Then, the client passes the authorization code to the parameter of the <a href="#token">/token</a> API and obtains a Clova access token.</p>
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
| `client_id`  | string  | The client ID (See [Client credentials](/CIC/Guides/Interact_with_CIC.md#ClientAuthInfo))  | Yes |
| `device_id`  | string  | The UUID of the client device. Use a MAC address or create a UUID hash value.  | Yes |
| `model_id`  | string  | The model ID of the client device  | No |
| `response_type` | string  | The response type. Only **"code"** is supported at the moment.  | Yes |
| `state`  | string  | The state token value (URL encoding applied) used by the client to prevent cross-site request forgery attacks | Yes |

### Request Example

<pre><code>{{ book.AuthServerBaseURL }}/authorize?client_id=7Jlaksjdflq1rOuTpA%3D%3D
                               &amp;device_id=test_device
                               &amp;model_id=test_model
                               &amp;response_type=code
                               &amp;state=95%2FKjaJfMlakjdfTVbES5ccZQ%3D%3D
</code></pre>

### Response field

| Field name  | Type  | Field description  |
|---------------|---------|-----------------------------|
| `code`  | string | The authorization code issued from the authorization server  |
| `state` | string | The decrypted state token value (URL decoding applied) passed from the client to prevent cross-site request forgery attacks |


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
* [`/token`](#token)


## /token {#token}
Creates, refreshes or deletes Clova access tokens using authorization codes issued through the [/authorize](#authorize) API. Depending on the `grant_type` parameter value, it performs different actions and returns different values.

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
| `access_token`  | string  | The Clova access token issued after authorization succeeds. This field is required when `grant_type` is set to **"delete"**.  | No |
| `client_id`  | string  | The client ID (See [Client credentials](/CIC/Guides/Interact_with_CIC.md#ClientAuthInfo))  | Yes |
| `client_secret` | string  | The client secret (See [Client credentials](/CIC/Guides/Interact_with_CIC.md#ClientAuthInfo))  | Yes |
| `code`  | string  | The authorization code issued through the [/authorize](#authorize) API. This field is required when `grant_type` is set to **"authorization_code"**.  | No |
| `device_id`  | string  | The UUID of the client device  | Yes |
| `grant_type`  | string  | An action identifier. <ul><li><strong>"authorization_code"</strong>: Issues a token</li><li><strong>"refresh_token"</strong>: Refreshes a token</li><li><strong>"delete"</strong>: Deletes a token</li></ul> | Yes |
| `model_id`  | string  | The model ID of the client device  | No |
| `refresh_token` | string  | The refresh token issued when authorization succeeds. This field is required when `grant_type` is set to **"refresh_token"**.  | No |
| `response_type` | string  | The response type. Only **"code"** is supported at the moment.  | Yes |

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
| `access_token`  | string  | The Clova access token  |
| `expires_in`  | number  | The amount of time that the Clova access token is deemed to be valid (in seconds)  |
| `refresh_token` | string  | The refresh token to refresh the Clova access token  |
| `token_type`  | string  | The type of the Clova access token. Always returns "Bearer". |

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
* [`/authorize`](#authorize)