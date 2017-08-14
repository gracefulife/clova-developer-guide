# Clova 인증 API
클라이언트가 CIC에 연결하려면 [Clova access token을 생성](/CIC/Guides/Interact_with_CIC.md#CreateClovaAccessToken)해야 합니다. Clova 인증 서버는 위 단계에 필요한 API를 제공하고 있으며, 이 문서는 Clova 인증 API에 대해 설명합니다.

## Base URL
Clova 인증 서버의 base URL은 다음과 같습니다.

<pre><code>{{ book.AuthServerBaseURL }}
</code></pre>

## /authorize {#authorize}
{{ book.TargetServiceForClientAuth }} 계정 access token 및 [클라이언트 인증 정보](/CIC/Guides/Interact_with_CIC.md#ClientAuthInfo) 등의 정보를 파라미터로 입력받아 authorization code를 응답 메시지로 반환합니다. authorization code는 Clova access token을 발급받기 전 단계의 인증 정보입니다.

<div class="note">
  <p><strong>Note!</strong></p>
  <p>일반적으로 사용자 인증을 받기 위해 클라이언트 기기와 페어링(Pairing)된 앱에서 인증을 처리합니다. 다만, 페어링된 앱에서 클라이언트 쪽으로 Clova access token을 전송하는 것은 보안상 이슈가 있기 때문에 이 코드를 대신 클라이언트로 보냅니다. 클라이언트는 전달받은 authorization code를 <a href="#token">/token</a> API의 파라미터로 전달하여 Clova access token을 획득해야 합니다.</p>
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

| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|---------|
| `client_id`     | string  | 클라이언트 ID ([클라이언트 인증 정보](/CIC/Guides/Interact_with_CIC.md#ClientAuthInfo) 참조)          | 필수 |
| `device_id`     | string  | 생성한 클라이언트 기기의 UUID. MAC 주소를 사용하거나 UUID 해쉬 값을 생성하면 됩니다.                          | 필수 |
| `model_id`      | string  | 클라이언트 기기의 모델 ID                                                                          | 선택 |
| `response_type` | string  | 응답 유형. 현재는 `"code"`만 지원합니다.                                                           | 필수 |
| `state`         | string  | 요청 위조(cross-site request forgery) 공격을 방지하기 위해 클라이언트에서 사용하는 상태 토큰 값(URL 인코딩 적용) | 필수 |

### Request Example

<pre><code>{{ book.AuthServerBaseURL }}authorize?client_id=7Jlaksjdflq1rOuTpA%3D%3D
                               &amp;device_id=test_device
                               &amp;model_id=test_model
                               &amp;response_type=code
                               &amp;state=95%2FKjaJfMlakjdfTVbES5ccZQ%3D%3D
</code></pre>

### Response field

| 필드 이름       | 자료형    | 필드 설명                     |
|---------------|---------|-----------------------------|
| `code`  | string | 인증 서버로부터 발급받은 authorization code                                                        |
| `state` | string | 요청 위조(cross-site request forgery) 공격을 방지하기 위해 클라이언트에서 전달받은 상태 토큰을 복호화한 값(URL 디코딩 적용) |


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
* [클라이언트 인증 정보](/CIC/Guides/Interact_with_CIC.md#ClientAuthInfo)
* [Clova access token 생성하기](/CIC/Guides/Interact_with_CIC.md#CreateClovaAccessToken)
* [`/token`](#token)


## /token {#token}
[/authorize](#authorize) API를 통해 발급받은 authorization code를 사용하여 Clova access token을 생성/갱신/삭제합니다. `grant_type` 파라미터의 값에 따라 동작이 구분되며 반환 값도 달라집니다.

### Scheme, method, path
{% raw %}
```
:method = {{GET|POST}}
:scheme = https
:path = token
```
{% endraw %}

### Parameter

| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|---------|
| `access_token`  | string  | 인증 성공 후 발급받은 Clova access token. `grant_type` 필드 값이 `"delete"`이면 필수입니다.                                 | 선택 |
| `client_id`     | string  | 클라이언트 ID([클라이언트 인증 정보](/CIC/Guides/Interact_with_CIC.md#ClientAuthInfo) 참조)                                  | 필수 |
| `client_secret` | string  | 클라이언트 Secret([클라이언트 인증 정보](/CIC/Guides/Interact_with_CIC.md#ClientAuthInfo) 참조)                              | 필수 |
| `code`          | string  | [/authorize](#authorize) API로 발급받은 authorization code. `grant_type` 필드 값이 `"authorization_code"`이면 필수입니다.        | 선택 |
| `device_id`     | string  | 생성한 클라이언트 기기의 UUID                                                                                              | 필수 |
| `grant_type`    | string  | 동작 구분자. <ul><li><code>"authorization_code"</code>: 토큰 발급</li><li><code>"refresh_token"</code>: 토큰 갱신</li><li><code>"delete"</code>: 토큰 삭제</li></ul> | 필수 |
| `model_id`      | string  | 클라이언트 기기의 모델 ID                                                                                                 | 선택 |
| `refresh_token` | string  | 인증 성공 후 발급받은 갱신 토큰. `grant_type` 필드 값이 `"refresh_token"`이면 필수입니다.                                      | 선택 |
| `response_type` | string  | 응답 유형. 현재는 `"code"`만 지원합니다.                                                                                  | 필수 |

### Request Example

<pre><code>{{ book.AuthServerBaseURL }}token?client_id=7JWI64WVIsdfasdfrOuTpA%3D%3D
                           &amp;client_secret=66qo65asdfasdfaA7JasdfasfOqwnOq1rOyfgeydtCDrvYasfasf%3D
                           &amp;code=cnl__eCSTdsdlkjfweyuxXvnlA
                           &amp;device_id=test_device
                           &amp;grant_type=authorization_code
                           &amp;model_id=test_model
</code></pre>


### Response field

| 필드 이름       | 자료형    | 필드 설명                     |
|---------------|---------|-----------------------------|
| `access_token`  | string  | Clova access token                               |
| `expires_in`    | number  | Clova access token의 유효 기간(초 단위)              |
| `refresh_token` | string  | Clova access token을 갱신하기 위한 갱신 토큰           |
| `token_type`    | string  | Clova access token의 타입. "Bearer"로 고정 반환됩니다. |

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
* [클라이언트 인증 정보](/CIC/Guides/Interact_with_CIC.md#ClientAuthInfo)
* [Clova access token 생성하기](/CIC/Guides/Interact_with_CIC.md#CreateClovaAccessToken)
* [`/authorize`](#authorize)
