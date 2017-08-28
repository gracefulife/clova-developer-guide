# Clova 인증 API
클라이언트가 CIC에 연결하려면 [Clova access token을 생성](/CIC/Guides/Interact_with_CIC.md#CreateClovaAccessToken)해야 합니다. Clova 인증 서버는 위 단계에 필요한 API를 제공하고 있으며, 이 문서는 Clova 인증 API에 대해 설명합니다.

## Base URL
Clova 인증 서버의 base URL은 다음과 같습니다.

<pre><code>{{ book.AuthServerBaseURL }}
</code></pre>

## Authorization code 요청 {#RequestAuthorizationCode}
{{ book.TargetServiceForClientAuth }} 계정 access token 및 [클라이언트 인증 정보](/CIC/Guides/Interact_with_CIC.md#ClientAuthInfo) 등의 정보를 파라미터로 입력받아 authorization code를 응답 메시지로 반환합니다. authorization code는 Clova access token을 발급받기 전 단계의 인증 정보입니다.

```
GET|POST /authorize
```

### Request headers

* Accept
  * application/json
* Authorization - [획득한 {{ book.TargetServiceForClientAuth }} access token](/CIC/Guides/Interact_with_CIC.md#CreateClovaAccessToken)을 입력합니다.
  * Bearer [{{ book.TargetServiceForClientAuth }} access token]

### Query parameter

| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|---------|
| `client_id`     | string  | 클라이언트 ID ([클라이언트 인증 정보](/CIC/Guides/Interact_with_CIC.md#ClientAuthInfo) 참조)          | 필수 |
| `device_id`     | string  | 생성한 클라이언트 기기의 UUID. MAC 주소를 사용하거나 UUID 해쉬 값을 생성하면 됩니다.                          | 필수 |
| `model_id`      | string  | 클라이언트 기기의 모델 ID                                                                          | 선택 |
| `response_type` | string  | 응답 유형. 현재는 `"code"`만 지원합니다.                                                             | 필수 |
| `state`         | string  | 요청 위조(cross-site request forgery) 공격을 방지하기 위해 클라이언트에서 사용하는 상태 토큰 값(URL 인코딩 적용) | 필수 |

### Request Example

<pre><code>$ curl -H 'Authorization: Bearer QHSDAKLFJAS123scjaf123klv'
       {{ book.AuthServerBaseURL }}authorize \
       --data-urlencode 'client_id=c2Rmc2Rmc2FkZ2FzZnNhZGZ' \
       --data-urlencode 'device_id=test_device' \
       --data-urlencode 'model_id=test_model' \
       --data-urlencode 'response_type=code' \
       --data-urlencode 'state=FKjaJfMlakjdfTVbES5ccZ'
</code></pre>

### Response header

* Content-Type
  * appliacation/json

### Response JSON object field

| 필드 이름       | 자료형    | 필드 설명                     |
|---------------|---------|-----------------------------|
| `code`  | string | 인증 서버로부터 발급받은 authorization code                                                                 |
| `state` | string | 요청 위조(cross-site request forgery) 공격을 방지하기 위해 클라이언트에서 전달받은 상태 토큰을 복호화한 값(URL 디코딩 적용) |

### Status codes

| 상태 코드       | 설명                     |
|---------------|-------------------------|
| 200 OK           | 요청 처리 성공                      |
| 400 Bad Request  | `client_id` 필드와 같이 필수 파라미터를 입력하지 않거나 유효하지 않은 데이터를 파라미터로 입력한 경우 발생하는 실패 |
| 403 Forbidden    | 헤더에 포함 시킨 {{ book.TargetServiceForClientAuth }} access token이 유효하지 않은 경우 |
| 500 Server Internal Error | 서버 내부 오류로 인한 authorization code 발급 실패 |

### Response Example
{% raw %}
```json
{
    "code": "cnl__eCSTdsdlkjfweyuxXvnlA",
    "state": "95/KjaJfMlakjdfTVbES5ccZQ=="
}
```
{% endraw %}

### Remarks
일반적으로 사용자 인증을 받기 위해 클라이언트 기기와 페어링(Pairing)된 앱에서 인증을 처리합니다. 다만, 페어링된 앱에서 클라이언트 쪽으로 Clova access token을 전송하는 것은 보안상 이슈가 있기 때문에 이 코드를 대신 클라이언트로 보냅니다. 클라이언트는 전달받은 authorization code를 다시 Clova 인증 서버로 전달하여 [Clova access token을 요청](#RequestClovaAccessToken)해야 합니다.

### See also
* [클라이언트 인증 정보](/CIC/Guides/Interact_with_CIC.md#ClientAuthInfo)
* [Clova access token 생성하기](/CIC/Guides/Interact_with_CIC.md#CreateClovaAccessToken)
* [Clova access token 요청](#RequestClovaAccessToken)


## Clova access token 요청 {#RequestClovaAccessToken}
[발급받은 authorization code](#RequestAuthorizationCode)를 사용하여 Clova 인증 서버에 Clova access token을 요청합니다.

```
GET|POST /token?grant_type=authorization_code
```

### Request header

* Accept
  * application/json

### Query parameter

| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|---------|
| `client_id`     | string  | 클라이언트 ID([클라이언트 인증 정보](/CIC/Guides/Interact_with_CIC.md#ClientAuthInfo) 참조)                                  | 필수 |
| `client_secret` | string  | 클라이언트 Secret([클라이언트 인증 정보](/CIC/Guides/Interact_with_CIC.md#ClientAuthInfo) 참조)                              | 필수 |
| `code`          | string  | [발급받은 authorization code](#RequestAuthorizationCode).             | 필수 |
| `device_id`     | string  | 생성한 클라이언트 기기의 UUID                                                                                              | 필수 |
| `model_id`      | string  | 클라이언트 기기의 모델 ID                                                                                                 | 선택 |

### Request Example

<pre><code>$ curl {{ book.AuthServerBaseURL }}token?grant_type=authorization_code \
       --data-urlencode 'client_secret=66qo65asdfasdfaA7JasdfasfOqwnOq1rOyfgeydtCDrvYasfasf%3D' \
       --data-urlencode 'code=cnl__eCSTdsdlkjfweyuxXvnlA' \
       --data-urlencode 'device_id=test_device' \
       --data-urlencode 'model_id=test_model'
</code></pre>

### Response header

* Content-Type
  * appliacation/json

### Response JSON object field

| 필드 이름       | 자료형    | 필드 설명                     |
|---------------|---------|-----------------------------|
| `access_token`  | string  | Clova access token                               |
| `expires_in`    | number  | Clova access token의 유효 기간(초 단위)              |
| `refresh_token` | string  | Clova access token을 갱신하기 위한 refresh token.          |
| `token_type`    | string  | Clova access token의 타입. "Bearer"로 고정 반환됩니다. |

### Status codes

| 상태 코드       | 설명                     |
|---------------|-------------------------|
| 200 OK        | 요청 처리 성공                      |
| 400 Bad Request  | `client_id` 필드와 같이 필수 파라미터를 입력하지 않거나 유효하지 않은 데이터를 파라미터로 입력한 경우 발생하는 실패 |
| 500 Interal Server Error | 서버 내부 오류로 인한 access token 발급 실패 |

### Response Example
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
* [클라이언트 인증 정보](/CIC/Guides/Interact_with_CIC.md#ClientAuthInfo)
* [Clova access token 생성하기](/CIC/Guides/Interact_with_CIC.md#CreateClovaAccessToken)
* [Authorization code 요청하기](#RequestAuthorizationCode)


## Clova access token 갱신 {#RefreshClovaAccessToken}
발급받은 refresh token을 사용하여 Clova access token을 갱신합니다.

```
GET|POST /token?grant_type=refresh_token
```

### Request header

* Accept
  * application/json

### Query parameter

| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|---------|
| `client_id`     | string  | 클라이언트 ID([클라이언트 인증 정보](/CIC/Guides/Interact_with_CIC.md#ClientAuthInfo) 참조)                                  | 필수 |
| `client_secret` | string  | 클라이언트 Secret([클라이언트 인증 정보](/CIC/Guides/Interact_with_CIC.md#ClientAuthInfo) 참조)                              | 필수 |
| `device_id`     | string  | 생성한 클라이언트 기기의 UUID                                                    | 필수 |
| `model_id`      | string  | 클라이언트 기기의 모델                                                           | 선택 |
| `refresh_token` | string  | 인증 성공 후 발급받은 refresh token.                                            | 필수 |

### Request Example

<pre><code>$ curl {{ book.AuthServerBaseURL }}token?grant_type=refresh_token \
       --data-urlencode 'client_id=c2Rmc2Rmc2FkZ2FzZnNhZGZ' \
       --data-urlencode 'client_secret=66qo65asdfasdfaA7JasdfasfOqwnOq1rOyfgeydtCDrvYasfasf%3D' \
       --data-urlencode 'refresh_token=GW-Ipsdfasdfdfs3IbHFBA' \
       --data-urlencode 'device_id=test_device' \
       --data-urlencode 'model_id=test_model'
</code></pre>

### Response header

* Content-Type
  * appliacation/json

### Response JSON object field

| 필드 이름       | 자료형    | 필드 설명                     |
|---------------|---------|-----------------------------|
| `access_token`  | string  | Clova access token                               |
| `expires_in`    | number  | Clova access token의 유효 기간(초 단위)              |
| `refresh_token` | string  | Clova access token을 갱신하기 위한 refresh token.    |
| `token_type`    | string  | Clova access token의 타입. "Bearer"로 고정 반환됩니다. |

### Status codes

| 상태 코드       | 설명                     |
|---------------|-------------------------|
| 200 OK        | 요청 처리 성공                      |
| 400 Bad Request  | `client_id` 필드와 같이 필수 파라미터를 입력하지 않거나 유효하지 않은 데이터를 파라미터로 입력한 경우 발생하는 실패 |
| 500 Internal Server Error | 서버 내부 오류로 인한 access token 갱신 실패 |

### Response Example
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
* [클라이언트 인증 정보](/CIC/Guides/Interact_with_CIC.md#ClientAuthInfo)
* [Clova access token 요청](#RequestClovaAccessToken)


## Clova access token 삭제 {#DeleteClovaAccessToken}
[발급받은 Clova access token](#RequestClovaAccessToken)을 삭제합니다.

```
GET|POST /token?grant_type=delete
```

### Request header

* Accept
  * application/json

### Query Parameter

| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|---------|
| `access_token`  | string  | 인증 성공 후 발급받은 Clova access token.                                 | 필수 |
| `client_id`     | string  | 클라이언트 ID([클라이언트 인증 정보](/CIC/Guides/Interact_with_CIC.md#ClientAuthInfo) 참조)                                  | 필수 |
| `client_secret` | string  | 클라이언트 Secret([클라이언트 인증 정보](/CIC/Guides/Interact_with_CIC.md#ClientAuthInfo) 참조)                              | 필수 |
| `device_id`     | string  | 생성한 클라이언트 기기의 UUID                                                     | 필수 |
| `model_id`      | string  | 클라이언트 기기의 모델                                                           | 선택 |

### Request Example

<pre><code>$ curl {{ book.AuthServerBaseURL }}token?grant_type=delete \
       --data-urlencode 'access_token=xFcH08vYQcahQWouqIzWOw' \
       --data-urlencode 'client_id=c2Rmc2Rmc2FkZ2FzZnNhZGZ' \
       --data-urlencode 'client_secret=66qo65asdfasdfaA7JasdfasfOqwnOq1rOyfgeydtCDrvYasfasf%3D' \
       --data-urlencode 'device_id=test_device' \
       --data-urlencode 'model_id=test_model'
</code></pre>

### Response header

* Content-Type
  * appliacation/json

### Response JSON object field

| 필드 이름       | 자료형    | 필드 설명                     |
|---------------|---------|-----------------------------|
| `access_token`  | string  | Clova access token                               |
| `client_id`     | string  | 클라이언트 ID.                                      |
| `expires_in`    | number  | Clova access token의 유효 기간(초 단위)              |

### Status codes

| 상태 코드       | 설명                     |
|---------------|-------------------------|
| 200 OK        | 요청 처리 성공                      |
| 400 Bad Request  | `client_id` 필드와 같이 필수 파라미터를 입력하지 않거나 유효하지 않은 데이터를 파라미터로 입력한 경우 발생하는 실패 |
| 401 Unauthorized | 유효하지 않은 클라이언트 인증 정보(`client_id` 또는 `client_secret`) 또는 사용자 정보(`device_id` 또는 `model_id`)를 파라미터로 전달한 경우 발생하는 실패 |
| 500 Internal Server Error | 서버 내부 오류로 인한 access token 삭제 실패 |

### Response Example
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
* [클라이언트 인증 정보](/CIC/Guides/Interact_with_CIC.md#ClientAuthInfo)
* [Clova access token 요청](#RequestClovaAccessToken)
