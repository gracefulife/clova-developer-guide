# Clova Auth API reference
To connect your client with CIC, you must [create a Clova access token](/CIC/Guides/Interact_with_CIC.md#CreateClovaAccessToken). The following explains the Clova Auth API, which is provided by a Clova authorization server to help you with generating and managing Clova access tokens.

## Base URL
The base URL of the Clova authorization server is as follows.

<pre><code>{{ book.AuthServerBaseURL }}
</code></pre>

## Requesting authorization code {#RequestAuthorizationCode}
Requests an authorization code by passing {{ book.TargetServiceForClientAuth }} account access token and [client credentials](/CIC/Guides/Interact_with_CIC.md#ClientAuthInfo) as parameters. An authorization code is credential information necessary for generation of a Clova access token.

```
GET|POST /authorize
```

### Request header

* Accept
  * application/json
* Authorization: Enter an [obtained {{ book.TargetServiceForClientAuth }} access token](/CIC/Guides/Interact_with_CIC.md#CreateClovaAccessToken).
  * Bearer [{{ book.TargetServiceForClientAuth }} access token]

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

* Content-Type
  * appliacation/json

### Response JSON object field

| Field name       | Type    | Field description                     |
|---------------|---------|-----------------------------|
| `code`  | string | The authorization code generated from the authorization server                                                                 |
| `state` | string | The decrypted state token (URL decoding applied) passed from the client to prevent cross-site request forgery attacks |

### Status codes

| Status code       | Description                     |
|---------------|-------------------------|
| 200 OK           | The request was processed successfully                      |
| 400 Bad Request  | Failed to process the request because required parameters such as `client_id` were not provided or provided parameters were invalid |
| 403 Forbidden    | The {{ book.TargetServiceForClientAuth }} access token contained in the header is invalid |
| 500 Server Internal Error | Failed to generate an authorization code due to an internal server error |

### Response example

{% raw %}
```json
{
    "code": "cnl__eCSTdsdlkjfweyuxXvnlA",
    "state": "FKjaJfMlakjdfTVbES5ccZ"
}
```
{% endraw %}

### Remarks
Typically, user authentication is processed on an app paired with a client device. However, transferring a Clova access token from a paired app to a client may have a potential security issue, so the app forwards an authorization code instead. The client receives the authorization code, passes it to a Clova authorization server and [requests a Clova access token](#RequestClovaAccessToken).

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

* Accept
  * application/json

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

* Content-Type
  * appliacation/json

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

* Accept
  * application/json

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

* Content-Type
  * appliacation/json

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

* Accept
  * application/json

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

* Content-Type
  * appliacation/json

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