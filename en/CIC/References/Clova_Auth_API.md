# Clova Auth API
To connect your client with CIC, you must [create a Clova access token](/CIC/Guides/Interact_with_CIC.md#CreateClovaAccessToken). This section explains the Clova Auth API, which is provided by the Clova authorization server to help you with the token creation.

## Base URL
The base URL of the Clova authorization server is as follows.

<pre><code>{{ book.AuthServerBaseURL }}
</code></pre>

## /authorize {#authorize}
Returns an authorization code by receiving a {{ book.TargetServiceForClientAuth }} account access token and [client credentials](/CIC/Guides/Interact_with_CIC.md#ClientAuthInfo) as parameters. An authorization code is credential information necessary for requesting issuance of a Clova access token.

<div class="note">
  <p><strong>Note!</strong></p>
  <p>Typically, user authentication is handled on an app paired with a client device. However, having a paired app return a Clova access token to a client may have a security issue. As such, it returns an authorization code instead. Once an authorization code is returned to a client, the client passes the code to the parameter of <a href="#token">/token</a> API and obtains a Clova access token.</p>
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
| Field name       | Type    | Field description                     | Required |
|---------------|---------|-----------------------------|---------|
| client_id     | string  | Client ID (See [Client credentials](/CIC/Guides/Interact_with_CIC.md#ClientAuthInfo))          | Yes |
| device_id     | string  | The UUID of a client device created                                                                      | Yes |
| model_id      | string  | The model ID of a client device                                                                          | No |
| response_type | string  | Response type. Only "code" is supported at the moment.                                                               | Yes |
| state         | string  | The value of a state token (URL encoding applied) used by a client to prevent cross-site request forgery attacks | Yes |

### Request Example

<pre><code>{{ book.AuthServerBaseURL }}/authorize?client_id=7Jlaksjdflq1rOuTpA%3D%3D
                               &amp;device_id=test_device
                               &amp;model_id=test_model
                               &amp;response_type=code
                               &amp;state=95%2FKjaJfMlakjdfTVbES5ccZQ%3D%3D
</code></pre>

### Response field
| Field name       | Type    | Field description                     |
|---------------|---------|-----------------------------|
| code  | string | An authorization code issued from an authorization server                                                        |
| state | string | The value of a decrypted state token (URL decoding applied) passed from a client to prevent cross-site request forgery attacks |


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
Creates, refreshes or deletes a Clova access token, using an authorization code issued with the [/authorize](#authorize) API. Depending on the *grant_type* parameter value, it performs different actions and returns different values.

### Scheme, method, path
{% raw %}
```
:method = {{GET|POST}}
:scheme = https
:path = token
```
{% endraw %}

### Parameter
| Field name       | Type    | Field description                     | Required |
|---------------|---------|-----------------------------|---------|
| access_token  | string  | A Clova access token issued when authorization succeeds. This field is required when *grant_type* is "delete".                                   | No |
| client_id     | string  | Client ID (See [Client credentials](/CIC/Guides/Interact_with_CIC.md#ClientAuthInfo))                                  | Yes |
| client_secret | string  | Client Secret (See [Client credentials](/CIC/Guides/Interact_with_CIC.md#ClientAuthInfo))                              | Yes |
| code          | string  | An authorization code issued with the [/authorize](#authorize) API. This field is required when *grant_type* is "authorization_code".        | No |
| device_id     | string  | The UUID of a client device created                                                                                              | Yes |
| grant_type    | string  | Action identifier. <ul><li>"authorization_code": Issues a token</li><li>"refresh_token": Refreshes a token</li><li>"delete": Deletes a token</li></ul> | Yes |
| model_id      | string  | The model ID of a client device                                                                                                 | No |
| refresh_token | string  | A refresh token issued when authorization succeeds. This field is required when *grant_type* is "refresh_token".                                        | No |
| response_type | string  | Response type. Only "code" is supported at the moment.                                                                                      | Yes |

### Request Example

<pre><code>{{ book.AuthServerBaseURL }}/token?client_id=7JWI64WVIsdfasdfrOuTpA%3D%3D
                           &amp;client_secret=66qo65asdfasdfaA7JasdfasfOqwnOq1rOyfgeydtCDrvYasfasf%3D
                           &amp;code=cnl__eCSTdsdlkjfweyuxXvnlA
                           &amp;device_id=test_device
                           &amp;grant_type=authorization_code
                           &amp;model_id=test_model
</code></pre>


### Response field
| Field name       | Type    | Field description                     |
|---------------|---------|-----------------------------|
| access_token  | string  | Clova access token                               |
| expires_in    | number  | The time that a Clova access token remains valid (in seconds)              |
| refresh_token | string  | A refresh token for refreshing a Clova access token           |
| token_type    | string  | The type of a Clova access token. Always returns "Bearer". |

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