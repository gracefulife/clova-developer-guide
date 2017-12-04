# Clova Auth API reference
To connect your client with CIC, you must [create a Clova access token](/CIC/Guides/Interact_with_CIC.md#CreateClovaAccessToken). The following explains the Clova Auth API, which is provided by a Clova authorization server to help you with generating and managing Clova access tokens.

## Base URL
The base URL of the Clova authorization server is as follows.

<pre><code>{{ book.AuthServerBaseURL }}
</code></pre>

## Requesting authorization code {#RequestAuthorizationCode}
Requests an authorization code by passing {{ book.TargetServiceForClientAuth }} account access token and [client credentials](/CIC/Guides/Interact_with_CIC.md#ClientAuthInfo) as parameters. The authorization code will be used when generating a Clova access token.

Typically, user authentication is processed on an app paired with a client device. However, transferring a Clova access token from a paired app to a client may have a potential security issue and thus the app forwards an authorization code instead. Upon receiving authorization code, the client should pass it to Clova authentication server and [request a Clova access token](#RequestClovaAccessToken).

```
GET|POST /authorize
```

### Request header

| Request header | Explanations                                                                |
|----------------|--------------------------------------------------------------------|
| Accept         | `application/json`                                                 |
| Authorization  | <p><a href="/CIC/Guides/Interact_with_CIC.html#CreateClovaAccessToken">Enter the aquired {{ book.TargetServiceForClientAuth }} access token</a>:</p><p><pre><code>Bearer [{{ book.TargetServiceForClientAuth }} access token]</code></pre></p>  |

### Query parameter

| Field name       | Type    | Field description                     | Required |
|---------------|---------|-----------------------------|---------|
| `client_id`     | string  | The client ID (See [Client credentials](/CIC/Guides/Interact_with_CIC.md#ClientAuthInfo))          | Yes |
| `device_id`     | string  | The UUID of the client device. Use a MAC address or create a UUID hash value.                          | Yes |
| `model_id`      | string  | The model ID of the client device                                                                          | No |
| `response_type` | string  | The response type. Only `"code"` is supported at the moment.                                                             | Yes |
| `state`         | string  | The state token (URL encoding applied) used by the client to prevent cross-site request forgery attacks | Yes |

### Request example

<pre><code>$ curl -H 'Authorization: Bearer QHSDAKLFJASlk12jlkf+asldkjasdf=sldkjf123dsalsdflkvpasdFMrjvi23scjaf123klv'
       {{ book.AuthServerBaseURL }}authorize \
       --data-urlencode 'client_id=c2Rmc2Rmc2FkZ2Fasdkjh234zZnNhZGZ' \
       --data-urlencode 'device_id=aa123123d6-d900-48a1-b73b-aa6c156353206' \
       --data-urlencode 'model_id=test_model' \
       --data-urlencode 'response_type=code' \
       --data-urlencode 'state=FKjaJfMlakjdfTVbES5ccZ'
</code></pre>

### Response header

| Response header | Explanations                                                                |
|-----------------|--------------------------------------------------------------------|
| Content-Type    | <p><pre><code>appliacation/json</code></pre></p>                   |

### Response JSON object field

| Field name       | Type    | Field description                     |
|---------------|---------|-----------------------------|
| `code`          | string | The authorization code generated from the authorization server It is a field included in the body of a HTTP response message when the message is having `200`or `451` status code.      |
| `redirect_uri`  | string | A URI page providing terms and conditions for the service. It is a field included in the body of a HTTP response message when the message is having `451 Unavailable For Legal Reasons` status code. The client should move to URI included in this field and mark the page. When the user agree to the terms and conditions, the client will receive a response containing a `302 Found`(URL redirection) status code along with the following URL. <ul><li><code>clova://agreement-success</code> : The user successfully agreed to the terms and conditions. The client can continue to the next process to create a Clova access token.</li><li><code>clova://agreement-failure</code> : The user failed to agree to the terms and conditions due to a server error. The client should exclude the failure properly.</li></ul> |
| `state`         | string | The decrypted state token (URL decoding applied) passed from the client to prevent cross-site request forgery attacks | It is a field included in the body of a HTTP response message when the message is having `200`or `451` status code. |

### Status codes

| Status code       | Description                     |
|---------------|-------------------------|
| 200 OK           | The response will be received if a request is processed successfully                      |
| 400 Bad Request  | The response will be received if entered an invalid data as a parameter or missed entering the required parameter just as `client_id` field |
| 451 Unavailable For Legal Reasons | The response will be received if the user did not agree to the terms and conditions. Upon receiving the response, the client should move to the address found from `redirect_uri` field and mark the web page. The URI is a page asking users to agree to the terms and conditions.  |
| 403 Forbidden    | The response is received when the {{ book.TargetServiceForClientAuth }} access token contained in the header is invalid |
| 500 Server Internal Error | The response is received when failed to generate an authorization code due to an internal server error |

### Response example
{% raw %}
```json
// Example 1: If HTTP response message has 200 OK status code
{
    "code": "cnl__eCSTdsdlkjfweyuxXvnlA",
    "state": "FKjaJfMlakjdfTVbES5ccZ"
}

// Example 2: If HTTP response message has 451 Unavailable For Legal Reasons status code
{
  "code":"4mrklvwoC_KNgDlvmslka",
  "redirect_uri":"https://ssl.pstatic.net/static/clova/service/terms/place/terms_3rd.html?code=4mrklvwoC_KNgDlvmslka&grant_type=code&state=FKjaJfMlakjdfTVbES5ccZ",
  "state":"FKjaJfMlakjdfTVbES5ccZ"
}
```
{% endraw %}

{% include "./CICAuthAPI/GuestMode.md" %}

### See also
* [Client credentials](/CIC/Guides/Interact_with_CIC.md#ClientAuthInfo)
* [Creating Clova access token](/CIC/Guides/Interact_with_CIC.md#CreateClovaAccessToken)
* [Requesting Clova access token](#RequestClovaAccessToken)


## Requesting Clova access token {#RequestClovaAccessToken}
Requests a Clova access token to a Clova authorization server with an [obtained authorization code](#RequestAuthorizationCode).

```
GET|POST /token?grant_type=authorization_code
```

### Request header

| Request header | Explanations                                                                |
|----------------|--------------------------------------------------------------------|
| Accept         | <p><pre><code>appliacation/json</code></pre></p>                   |

### Query parameter

| Field name       | Type    | Field description                     | Required |
|---------------|---------|-----------------------------|---------|
| `client_id`     | string  | The client ID (See [Client credentials](/CIC/Guides/Interact_with_CIC.md#ClientAuthInfo))                                  | Yes |
| `client_secret` | string  | The client secret (See [Client credentials](/CIC/Guides/Interact_with_CIC.md#ClientAuthInfo))                              | Yes |
| `code`          | string  | [The obtained authorization code](#RequestAuthorizationCode).             | Yes |
| `device_id`     | string  | The UUID of the client device                                                                                              | Yes |
| `model_id`      | string  | The model ID of the client device                                                                                                 | No |

### Request example

<pre><code>$ curl {{ book.AuthServerBaseURL }}token?grant_type=authorization_code \
       --data-urlencode 'client_id=c2Rmc2Rmc2FkZ2Fasdkjh234zZnNhZGZ' \
       --data-urlencode 'client_secret=66qo65asdfasdfaA7JasdfasfOqwnOq1rOyfgeydtCDrvYasfasf%3D' \
       --data-urlencode 'code=cnl__eCSTdsdlkjfweyuxXvnlA' \
       --data-urlencode 'device_id=aa123123d6-d900-48a1-b73b-aa6c156353206' \
       --data-urlencode 'model_id=test_model'
</code></pre>

### Response header

| Response header | Explanations                                                                |
|-----------------|--------------------------------------------------------------------|
| Content-Type    | <p><pre><code>appliacation/json</code></pre></p>                   |

### Response JSON object field

| Field name       | Type    | Field description                     |
|---------------|---------|-----------------------------|
| `access_token`  | string  | The Clova access token                               |
| `expires_in`    | number  | The amount of time that the Clova access token is deemed to be valid (in seconds)              |
| `refresh_token` | string  | The refresh token to refresh the Clova access token.          |
| `token_type`    | string  | The type of the Clova access token. Always returns "Bearer". |

### Status codes

| Status code       | Description                     |
|---------------|-------------------------|
| 200 OK        | The request was processed successfully                      |
| 400 Bad Request  | Failed to process the request because required parameters such as `client_id` were not provided or provided parameters were invalid |
| 500 Internal Server Error | Failed to generate an access token due to an internal server error |

### Response example
{% raw %}
```json
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
* [Requesting authorization code](#RequestAuthorizationCode)


## Refreshing Clova access token {#RefreshClovaAccessToken}
Refreshes a Clova access token with a refresh token.

```
GET|POST /token?grant_type=refresh_token
```

### Request header

| Request header | Explanations                                                                |
|----------------|--------------------------------------------------------------------|
| Accept         | <p><pre><code>appliacation/json</code></pre></p>                   |

### Query parameter

| Field name       | Type    | Field description                     | Required |
|---------------|---------|-----------------------------|---------|
| `client_id`     | string  | The client ID (See [Client credentials](/CIC/Guides/Interact_with_CIC.md#ClientAuthInfo))                                  | Yes |
| `client_secret` | string  | The client secret (See [Client credentials](/CIC/Guides/Interact_with_CIC.md#ClientAuthInfo))                              | Yes |
| `device_id`     | string  | The UUID of the client device                                                    | Yes |
| `model_id`      | string  | The model of the client device                                                           | No |
| `refresh_token` | string  | The refresh token generated after authorization succeeds.                                            | Yes |

### Request example

<pre><code>$ curl {{ book.AuthServerBaseURL }}token?grant_type=refresh_token \
       --data-urlencode 'client_id=c2Rmc2Rmc2FkZ2FzZnNhZGZ' \
       --data-urlencode 'client_secret=66qo65asdfasdfaA7JasdfasfOqwnOq1rOyfgeydtCDrvYasfasf%3D' \
       --data-urlencode 'refresh_token=GW-Ipsdfasdfdfs3IbHFBA' \
       --data-urlencode 'device_id=aa123123d6-d900-48a1-b73b-aa6c156353206' \
       --data-urlencode 'model_id=test_model'
</code></pre>

### Response header

| Response header | Explanations                                                                |
|-----------------|--------------------------------------------------------------------|
| Content-Type    | <p><pre><code>appliacation/json</code></pre></p>                   |

### Response JSON object field

| Field name       | Type    | Field description                     |
|---------------|---------|-----------------------------|
| `access_token`  | string  | The Clova access token                               |
| `expires_in`    | number  | The amount of time that the Clova access token is deemed to be valid (in seconds)              |
| `refresh_token` | string  | The refresh token to refresh the Clova access token.    |
| `token_type`    | string  | The type of the Clova access token. Always returns "Bearer". |

### Status codes

| Status code       | Description                     |
|---------------|-------------------------|
| 200 OK        | The request was processed successfully                      |
| 400 Bad Request  | Failed to process the request because required parameters such as `client_id` were not provided or provided parameters were invalid |
| 500 Internal Server Error | Failed to refresh the access token due to an internal server error |

### Response example
{% raw %}
```json
{
    "access_token": "xFcH08vYQcahQWouqIzWOw",
    "expires_in": 12960000,
    "refresh_token": "drJK-soIQI6vqEukqsLU2g",
    "token_type": "Bearer"
}
```
{% endraw %}

### See also
* [Client credentials](/CIC/Guides/Interact_with_CIC.md#ClientAuthInfo)
* [Requesting Clova access token](#RequestClovaAccessToken)


## Deleting Clova access token {#DeleteClovaAccessToken}
Deletes a [generated Clova access token](#RequestClovaAccessToken).

```
GET|POST /token?grant_type=delete
```

### Request header

| Request header | Explanations                                                                |
|----------------|--------------------------------------------------------------------|
| Accept         | <p><pre><code>appliacation/json</code></pre></p>                   |

### Query parameter

| Field name       | Type    | Field description                     | Required |
|---------------|---------|-----------------------------|---------|
| `access_token`  | string  | The Clova access token generated after authorization succeeds.                                 | Yes |
| `client_id`     | string  | The client ID (See [Client credentials](/CIC/Guides/Interact_with_CIC.md#ClientAuthInfo))                                  | Yes |
| `client_secret` | string  | The client secret (See [Client credentials](/CIC/Guides/Interact_with_CIC.md#ClientAuthInfo))                              | Yes |
| `device_id`     | string  | The UUID of the client device                                                     | Yes |
| `model_id`      | string  | The model of the client device                                                           | No |

### Request example

<pre><code>$ curl {{ book.AuthServerBaseURL }}token?grant_type=delete \
       --data-urlencode 'access_token=xFcH08vYQcahQWouqIzWOw' \
       --data-urlencode 'client_id=c2Rmc2Rmc2FkZ2Fasdkjh234zZnNhZGZ' \
       --data-urlencode 'client_secret=66qo65asdfasdfaA7JasdfasfOqwnOq1rOyfgeydtCDrvYasfasf%3D' \
       --data-urlencode 'device_id=aa123123d6-d900-48a1-b73b-aa6c156353206' \
       --data-urlencode 'model_id=test_model'
</code></pre>

### Response header

| Response header | Explanations                                                                |
|-----------------|--------------------------------------------------------------------|
| Content-Type    | <p><pre><code>appliacation/json</code></pre></p>                   |

### Response JSON object field

| Field name       | Type    | Field description                     |
|---------------|---------|-----------------------------|
| `access_token`  | string  | The Clova access token                               |
| `client_id`     | string  | The client ID.                                      |
| `expires_in`    | number  | The amount of time that the Clova access token is deemed to be valid (in seconds)              |

### Status codes

| Status code       | Description                     |
|---------------|-------------------------|
| 200 OK        | The request was processed successfully                      |
| 400 Bad Request  | Failed to process the request because required parameters such as `client_id` were not provided or provided parameters were invalid |
| 401 Unauthorized | The client credentials (`client_id` or `client_secret`) or user information (`device_id` or `model_id`) which were passed as parameters are invalid |
| 500 Internal Server Error | Failed to delete the access token due to an internal server error |

### Response example
{% raw %}
```json
{
    "access_token": "xFcH08vYQcahQWouqIzWOw",
    "expires_in": 12960000,
    "client_id": "c2Rmc2Rmc2FkZ2FzZnNhZGZ"
}
```
{% endraw %}

### See also
* [Client credentials](/CIC/Guides/Interact_with_CIC.md#ClientAuthInfo)
* [Requesting Clova access token](#RequestClovaAccessToken)
