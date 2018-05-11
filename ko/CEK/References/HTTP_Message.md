## HTTP 메시지 {#HTTPMessage}
CEK와 extension이 통신할 때 HTTP/1.1 프로토콜을 사용하며, 기본적인 HTTPS 요청과 HTTPS 응답을 주고 받습니다. CEK와 extension이 서로 통신할 때 HTTP 메시지 본문(body)에는 JSON 포맷의 메시지가 포함되어 있습니다. 여기에서는 CEK와 extension 사이에서 주고 받는 HTTP 메시지가 어떻게 구성되는지 설명합니다.

* [HTTP 헤더](#HTTPHeader)
* [HTTP 본문](#HTTPBody)
* [요청 메시지 검증](#RequestMessageValidation)

### HTTP 헤더 {#HTTPHeader}
CEK가 extension으로 분석된 사용자의 발화 정보를 보낼 때 HTTPS 요청을 사용합니다. 이때 HTTPS 요청 헤더는 다음과 같이 구성됩니다.

{% raw %}

```
POST /APIpath HTTP/1.1
Host: your.extension.endpoint
Content-Type: application/json;charset-UTF-8
Accept: application/json
Accept-Charset: utf-8
SignatureCEK: {{ SignatureCEK }}
SignatureCEKCertChainUrl: {{ SignatureCEKCertChainUrl }}
```
{% endraw %}

* HTTP/1.1 버전으로 HTTPS 통신을 수행하며, method로 POST 방식을 사용합니다.
* Host와 요청 대상 path는 extension 개발자가 미리 정의해 둔 URI로 채워집니다.
* 본문의 데이터 형식은 JSON 포맷으로 되어 있으며, UTF-8 인코딩을 사용합니다.
* `SignatureCEK`와 `SignatureCEKCertChainUrl` 필드를 이용하여 [CEK로부터 전송된 요청인지 검증](#RequestMessageValidation)할 수 있습니다.

이와 반대로 extension이 CEK로 처리 결과를 보낼 때 HTTPS 응답을 사용합니다. 이때 HTTPS 응답 헤더는 다음과 같이 기본적인 것만 구성하면 됩니다.
{% raw %}
```
HTTP/1.1 200 OK
Content-Type: application/json;charset-UTF-8
```
{% endraw %}
* CEK가 보낸 HTTPS 요청에 대한 응답으로 처리 결과를 전달합니다.
* 본문의 데이터 형식은 JSON 포맷으로 되어 있으며, UTF-8 인코딩을 사용합니다.

### HTTP 본문 {#HTTPBody}
HTTPS 요청 메시지와 응답 메시지의 본문은 JSON 포맷이며, 분석된 사용자의 발화 정보나 extension의 처리 결과가 담긴 정보입니다. 각 메시지의 구성은 어떤 종류의 extension을 사용하느냐에 따라 달라집니다. 메시지의 구성에 대한 자세한 정보는 [custom extension 메시지](#CustomExtMessage)와 [Clova Home extension 메시지](#ClovaHomeExtMessage)를 참조합니다.

### 요청 메시지 검증 {#RequestMessageValidation}
Extension이 CEK로부터 HTTPS 요청을 받을 때, 해당 요청이 제 3자가 아닌 Clova로부터 전송된 신뢰할 수 있는 요청인지 검증할 필요가 있습니다. [HTTP 헤더](#HTTPHeader)에 있는 `SignatureCEK`와 `SignatureCEKCertChainUrl` 필드를 사용하여 다음과 같이 요청 메시지를 검증할 수 있습니다.

**`SignatureCEKCertChainUrl`로부터 인증서 확보 및 검증**
1. `SignatureCEKCertChainUrl`의 URL이 HTTPS 방식이며, `{{ book.SignatureSubPath }}`이 포함되어 있는지 확인합니다.
2. `SignatureCEKCertChainUrl`의 URL로부터 X.509 인증서(PEM)를 다운로드합니다.
3. 다운로드한 인증서의 Subject Alternative Name(SAN) 필드 값이 `{{ book.SignatureSANDomain }}`인지 확인합니다.
4. 신뢰할 수 있는 root 인증서를 통해 모든 체인이 만들어졌는지 확인합니다.
5. 다운로드한 인증서의 유효 기간이 만료되지 않았는지 확인합니다.

**해쉬 값 생성 및 메시지 검증**
1. `SignatureCEK`의 값을 Base64 디코딩합니다.
2. 앞서 다운로드한 인증서의 공개키를 사용하여 `SignatureCEK`를 디코딩한 값을 복호화합니다.
3. HTTPS 요청 메시지 본문을 이용하여 SHA-1 해쉬 값을 생성합니다.
4. 2번 항목에서 복호화한 값과 3번 항목에서 생성한 해쉬 값을 비교하여 두 값이 같은지 확인합니다.

<div class="note">
  <p><strong>Note!</strong></p>
  <p>신뢰할 수 없는 인증서이거나 <strong>해쉬 값 생성 및 메시지 검증</strong>에서 비교한 두 값이 다르면 해당 요청 폐기를 권장합니다.</p>
</div>
