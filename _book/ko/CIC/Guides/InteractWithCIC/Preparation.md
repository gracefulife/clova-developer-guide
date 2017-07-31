## 사전 준비사항 {#Preparation}
클라이언트는 HTTP/2 프로토콜을 사용하여 CIC에 연결해야 합니다. 따라서, CIC에 연결하기 전에 다음을 미리 준비해야 합니다.

* HTTP/2 프로토콜 연결을 위한 [라이브러리](#RequiredLibrary)
* Clova access token 생성을 위한 [클라이언트 인증 정보](#ClientAuthInfo)


### 필요 라이브러리 {#RequiredLibrary}
HTTP/2 프로토콜 연결을 위해 클라이언트 개발 시 다음과 같은 라이브러리 사용을 권장합니다.

| 개발 언어 | 라이브러리                            |
|---------|------------------------------------|
| C/C++   | [nghttp2](https://nghttp2.org/), [libcurl](https://curl.haxx.se/libcurl/) |
| Java    | [OkHttp](http://square.github.io/okhttp/), [Netty](http://netty.io/), [Jetty](http://www.eclipse.org/jetty/) |


### 클라이언트 인증 정보 {#ClientAuthInfo}
사용자는 클라이언트에서 {{ book.TargetServiceForClientAuth }} 계정을 인증해야 Clova가 제공하는 서비스를 사용할 수 있습니다. 클라이언트는 사용자로부터 입력받은 {{ book.TargetServiceForClientAuth }}의 계정 정보를 토대로 {{ book.TargetServiceForClientAuth }} 계정 access token을 획득할 수 있습니다. 이 토큰을 다시 Clova 인증 서버로 전달하여 [Clova access token를 획득](#CreateClovaAccessToken)해야 합니다.

{{ book.TargetServiceForClientAuth }} 계정 access token뿐만 아니라 Clova Developer Console을 통해 획득한 클라이언트 인증 정보를 함께 인증 서버로 전달해야 합니다([Clova 인증 API](/CIC/References/Clova_Auth_API.md) 사용). 따라서 Clova Developer Console을 통해 클라이언트 인증 정보를 미리 확보해야 해야 합니다. 클라이언트 인증 정보는 다음과 같습니다.

| 인증 정보                   | 설명                                              |
|---------------------------|--------------------------------------------------|
| CLOVA_OAUTH_CLIENT_ID     | Clova Developer Console에 등록한 클라이언트 ID        |
| CLOVA_OAUTH_CLIENT_SECRET | Clova Developer Console을 통해 획득한 클라이언트 인증 키 |

<div class="note">
  <p><strong>Note!</strong></p>
  <p>현재 Clova Developer Console을 개발하는 중입니다. 따라서, 클라이언트 인증 정보는 제휴 담당자를 통해 확보하면 됩니다.</p>
</div>
