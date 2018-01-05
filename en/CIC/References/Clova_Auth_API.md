# Clova Auth API reference

To connect a client with CIC, you must [create a Clova access token](/CIC/Guides/Interact_with_CIC.md#CreateClovaAccessToken). The Clova authorization server provides the Clova Authorization API for you to create and manage Clova access tokens.

## Base URL

The base URL of the Clova authorization server is as follows.

<pre><code>{{ book.AuthServerBaseURL }}
</code></pre>

## Requesting an authorization code {#RequestAuthorizationCode}

```
GET|POST /authorize
```

This API requests an authorization code. Specify the parameters with the {{ book.TargetServiceForClientAuth }} account access token and the [client credentials](/CIC/Guides/Interact_with_CIC.md#ClientAuthInfo). The authorization code obtained will be used in generating a Clova access token.

Typically, user authentication is processed on the pair app. However, transferring a Clova access token from the pair app to the client may have a potential security issue. To avoid security issues, the app forwards the authorization code to the client instead of the Clova access token. Upon receiving an authorization code, the client is to pass the code to the Clova authorization server and [request a Clova access token](#RequestClovaAccessToken).

### Request header

| Request header | Description                                                                |
|----------------|--------------------------------------------------------------------|
| Accept         | <p>Set the header with the following:</p><p><pre><code>`application/json`</code></pre><p>                                              |
| Authorization  | <p>Use the <a href="/CIC/Guides/Interact_with_CIC.html#CreateClovaAccessToken">{{ book.TargetServiceForClientAuth }} access token</a> acquired:</p><p><pre><code>Bearer [{{ book.TargetServiceForClientAuth }} access token]</code></pre></p>  |

### Query parameters

| Field name       | Type    | Description                     | Required |
|---------------|:---------:|-----------------------------|:---------:|
| `client_id`     | string  | The client ID. (See [Client credentials](/CIC/Guides/Interact_with_CIC.md#ClientAuthInfo))          | Required |
| `device_id`     | string  | The client's MAC address or a hashed UUID created by you.                          | Required |
| `model_id`      | string  | The model ID of the client device.                                                                          | Optional |
| `response_type` | string  | The response type. The value is always `"code"`.                                                            | Required |
| `state`         | string  | The state token (URL encoding applied) used by the client to prevent cross-site request forgery attacks. | Required |

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

| Response header | Description                                                                |
|-----------------|--------------------------------------------------------------------|
| Content-Type    | <p>Specifies the content type of the HTTP response.</p> <p><pre><code>application/json</code></pre></p>                   |

### Response object

| Field name       | Type    | Description                     |
|---------------|:---------:|-----------------------------|
| `code`          | string | The authorization code issued by the Clova authorization server. This field is returned in the body of the HTTP response message if the status code is `200`or `451`.      |
| `redirect_uri`  | string | The URI of the terms and conditions page. The field is returned in the body of the HTTP response message if the status code is `451 Unavailable For Legal Reasons`. Display the page of the URI. When the user agrees to the terms and conditions, the client will receive the following URL, with the status code `302 Found`(URL redirection): <ul><li><code>clova://agreement-success</code>: The user has successfully agreed to the terms and conditions. The client can continue to the next process to create a Clova access token.</li><li><code>clova://agreement-failure</code>: The user has failed to agree to the terms and conditions due to a server error. Handle the error appropriately.</li></ul> |
| `state`         | string | The state token from the client, decrypted (URL decoding) to prevent cross-site request forgery attacks. This field is returned in the body of the HTTP response message if the status code is `200`or `451`. |

### Status codes

| Status code       | Description                     |
|---------------|-------------------------|
| 200 OK           | The user's request has been processed successfully.                     |
| 400 Bad Request  | Required parameters such as `client_id` are missing or invalid parameters have been used. |
| 451 Unavailable For Legal Reasons | The user has not agreed to the terms and conditions. Open the webpage specified by the `redirect_uri` field. The URI points to the terms and conditions page.  |
| 403 Forbidden    | The {{ book.TargetServiceForClientAuth }} access token specified in the header is invalid. |
| 500 Server Internal Error | Failed to issue an authorization code due to an internal server error. |

### Response example

{% raw %}
```json
// Example 1: If the HTTP response message has 200 OK
{
    "code": "cnl__eCSTdsdlkjfweyuxXvnlA",
    "state": "FKjaJfMlakjdfTVbES5ccZ"
}

// Example 2: If the HTTP response message has 451 Unavailable For Legal Reasons
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
* [Creating a Clova access token](/CIC/Guides/Interact_with_CIC.md#CreateClovaAccessToken)
* [Requesting a Clova access token](#RequestClovaAccessToken)


## Requesting a Clova access token {#RequestClovaAccessToken}

```
GET|POST /token?grant_type=authorization_code
```

This API requests for a Clova access token to the Clova authorization server with the [authorization code obtained](#RequestAuthorizationCode).

### Request header

| Request header | Description                                                                |
|----------------|--------------------------------------------------------------------|
| Accept         | <p>Set the header with the following:</p><p><pre><code>`application/json`</code></pre><p>                    |

### Query parameters

| Field name       | Type    | Description                     | Required |
|---------------|:---------:|-----------------------------|:---------:|
| `client_id`     | string  | The client ID. (See [Client credentials](/CIC/Guides/Interact_with_CIC.md#ClientAuthInfo))                                  | Required |
| `client_secret` | string  | The client secret. (See [Client credentials](/CIC/Guides/Interact_with_CIC.md#ClientAuthInfo))                              | Required |
| `code`          | string  | [The obtained authorization code](#RequestAuthorizationCode).             | Required |
| `device_id`     | string  | The client's MAC address or a hashed UUID created by you.                                                                                               | Required |
| `model_id`      | string  | The model ID of the client device.                                                                                                 | Optional |

### Request example

<pre><code>$ curl {{ book.AuthServerBaseURL }}token?grant_type=authorization_code \
       --data-urlencode 'client_id=c2Rmc2Rmc2FkZ2Fasdkjh234zZnNhZGZ' \
       --data-urlencode 'client_secret=66qo65asdfasdfaA7JasdfasfOqwnOq1rOyfgeydtCDrvYasfasf%3D' \
       --data-urlencode 'code=cnl__eCSTdsdlkjfweyuxXvnlA' \
       --data-urlencode 'device_id=aa123123d6-d900-48a1-b73b-aa6c156353206' \
       --data-urlencode 'model_id=test_model'
</code></pre>

### Response header

| Response header | Description                                                                |
|-----------------|--------------------------------------------------------------------|
| Content-Type    | <p>Specifies the content type of the HTTP response.</p> <p><pre><code>application/json</code></pre></p>                   |

### Response object

| Field name       | Type    | Description                     |
|---------------|:---------:|-----------------------------|
| `access_token`  | string  | The Clova access token issued.                               |
| `expires_in`    | number  | Specifies how long the Clova access token is valid for, in seconds.              |
| `refresh_token` | string  | The refresh token to required to refresh the Clova access token.          |
| `token_type`    | string  | The type of the Clova access token. The value is always `"Bearer"`. |

### Status codes

| Status code       | Description                     |
|---------------|-------------------------|
| 200 OK        | The request was processed successfully.                      |
| 400 Bad Request  | Required parameters such as `client_id` are missing or invalid parameters have been used. |
| 500 Internal Server Error | Failed to issue an access token due to an internal server error |

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
* [Creating a Clova access token](/CIC/Guides/Interact_with_CIC.md#CreateClovaAccessToken)
* [Requesting an authorization code](#RequestAuthorizationCode)


## Refreshing a Clova access token {#RefreshClovaAccessToken}

```
GET|POST /token?grant_type=refresh_token
```

This API refreshes the Clova access token with a refresh token.

### Request header

| Request header | Description                                                                |
|----------------|--------------------------------------------------------------------|
| Accept         | <p>Set the header with the following:</p><p><pre><code>`application/json`</code></pre><p>                     |

### Query parameters

| Field name       | Type    | Description                     | Required |
|---------------|:---------:|-----------------------------|:---------:|
| `client_id`     | string  | The client ID. (See [Client credentials](/CIC/Guides/Interact_with_CIC.md#ClientAuthInfo))                                  | Required |
| `client_secret` | string  | The client secret. (See [Client credentials](/CIC/Guides/Interact_with_CIC.md#ClientAuthInfo))                              | Required |
| `device_id`     | string  | The client's MAC address or a hashed UUID created by you.                                                     | Required |
| `model_id`      | string  | The model of the client device.                                                           | Optional |
| `refresh_token` | string  | The refresh token issued with the Clova access token.                                           | Required |

### Request example

<pre><code>$ curl {{ book.AuthServerBaseURL }}token?grant_type=refresh_token \
       --data-urlencode 'client_id=c2Rmc2Rmc2FkZ2FzZnNhZGZ' \
       --data-urlencode 'client_secret=66qo65asdfasdfaA7JasdfasfOqwnOq1rOyfgeydtCDrvYasfasf%3D' \
       --data-urlencode 'refresh_token=GW-Ipsdfasdfdfs3IbHFBA' \
       --data-urlencode 'device_id=aa123123d6-d900-48a1-b73b-aa6c156353206' \
       --data-urlencode 'model_id=test_model'
</code></pre>

### Response header

| Response header | Description                                                                |
|-----------------|--------------------------------------------------------------------|
| Content-Type    | <p>Specifies the content type of the HTTP response.</p> <p><pre><code>application/json</code></pre></p>                  |

### Response object

| Field name       | Type    | Description                     |
|---------------|:---------:|-----------------------------|
| `access_token`  | string  | The Clova access token refreshed.                              |
| `expires_in`    | number  | Specifies how long the Clova access token is valid for, in seconds.              |
| `refresh_token` | string  | The refresh token required to refresh the Clova access token with.    |
| `token_type`    | string  | The type of the Clova access token. The value is always `"Bearer"`. |

### Status codes

| Status code       | Description                     |
|---------------|-------------------------|
| 200 OK        | The request was processed successfully.                      |
| 400 Bad Request  | Required parameters such as `client_id` are missing or invalid parameters have been used. |
| 500 Internal Server Error | Failed to refresh the access token due to an internal server error. |

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
* [Requesting a Clova access token](#RequestClovaAccessToken)


## Deleting a Clova access token {#DeleteClovaAccessToken}

```
GET|POST /token?grant_type=delete
```

This API deletes the [Clova access token issued](#RequestClovaAccessToken).

### Request header

| Request header | Description                                                                |
|----------------|--------------------------------------------------------------------|
| Accept         | <p>Specifies the content type of the HTTP response.</p> <p><pre><code>application/json</code></pre></p>                  |

### Query parameters

| Field name       | Type    | Description                     | Required |
|---------------|:---------:|-----------------------------|:---------:|
| `access_token`  | string  | The Clova access token to delete.                                | Required |
| `client_id`     | string  | The client ID. (See [Client credentials](/CIC/Guides/Interact_with_CIC.md#ClientAuthInfo))                                  | Required |
| `client_secret` | string  | The client secret. (See [Client credentials](/CIC/Guides/Interact_with_CIC.md#ClientAuthInfo))                              | Required |
| `device_id`     | string  | The client's MAC address or a hashed UUID created by you.                                                     | Required |
| `model_id`      | string  | The model of the client device.                                                           | Optional |

### Request example

<pre><code>$ curl {{ book.AuthServerBaseURL }}token?grant_type=delete \
       --data-urlencode 'access_token=xFcH08vYQcahQWouqIzWOw' \
       --data-urlencode 'client_id=c2Rmc2Rmc2FkZ2Fasdkjh234zZnNhZGZ' \
       --data-urlencode 'client_secret=66qo65asdfasdfaA7JasdfasfOqwnOq1rOyfgeydtCDrvYasfasf%3D' \
       --data-urlencode 'device_id=aa123123d6-d900-48a1-b73b-aa6c156353206' \
       --data-urlencode 'model_id=test_model'
</code></pre>

### Response header

| Response header | Description                                                                |
|-----------------|--------------------------------------------------------------------|
| Content-Type    | <p>Specifies the content type of the HTTP response.</p> <p><pre><code>application/json</code></pre></p>                  |

### Response object

| Field name       | Type    | Description                     |
|---------------|:---------:|-----------------------------|
| `access_token`  | string  | The Clova access token deleted.                              |
| `client_id`     | string  | The client ID.                                      |
| `expires_in`    | number  | The expiry time the deleted Clova access token had, in seconds. |

### Status codes

| Status code       | Description                     |
|---------------|-------------------------|
| 200 OK        | The request was processed successfully.                      |
| 400 Bad Request  | Required parameters such as `client_id` are missing or invalid parameters have been used. |
| 401 Unauthorized | The client credentials (`client_id` or `client_secret`) or the client information (`device_id` or `model_id`) passed as parameters are invalid. |
| 500 Internal Server Error | Failed to delete the access token due to an internal server error. |

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
* [Requesting a Clova access token](#RequestClovaAccessToken)
