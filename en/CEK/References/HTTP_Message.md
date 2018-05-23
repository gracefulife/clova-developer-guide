## HTTP message {#HTTPMessage}
CEK and the extensions communicate via the HTTP/1.1 protocol and exchange basic HTTPS requests and HTTPS responses. During this communication, a JSON format message is contained in the HTTP message body. This section explains the configuration of the HTTP message exchanged between CEK and the extension.

* [HTTP header](#HTTPHeader)
* [HTTP body](#HTTPBody)
* [Validating request messages](#RequestMessageValidation)

### HTTP header {#HTTPHeader}
An HTTPS request is used when CEK sends the analyzed information of a user utterance to the extension. The HTTPS request header is configured as follows:

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

* HTTPS communication is performed with HTTP/1.1 and the POST method is used.
* The values for the host and request target path are filled with the URI defined by the extension developer.
* The body data type is in JSON format and UTF-8 encoding is used.
* You can [validate whether or not a request is sent from CEK](#RequestMessageValidation) using the `SignatureCEK` and `SignatureCEKCertChainUrl` fields.

However, an HTTPS response is used when the extension sends processed result to CEK. The HTTPS response header can just configure basic information as follows:
{% raw %}
```
HTTP/1.1 200 OK
Content-Type: application/json;charset-UTF-8
```
{% endraw %}
* The processed results are returned as a response to the HTTPS request from CEK.
* The body data type is in JSON format and UTF-8 encoding is used.

### HTTP body {#HTTPBody}
Both the body of the HTTPS request message and response message are in JSON format, and it contains the information on user utterance analysis or the processed result of the extension. The configuration of each message varies depending on the extension type. For more information on message configurations, see [Custom extension messages](#CustomExtMessage) and [Clova Home extension messages](#ClovaHomeExtMessage).

### Validating request messages {#RequestMessageValidation}
When the extension receives an HTTP request from CEK, you need to validate the integrity of the request meaning that the request was sent from Clova and not from a third party. Using the `SignatureCEK` and `SignatureCEKCertChainUrl` fields in the [HTTP header](#HTTPHeader), you can validate the request message as follows:

**Obtain the certificate from `SignatureCEKCertChainUrl` for validation**
1. Check that `SignatureCEKCertChainUrl` is an HTTPS URL and includes a `{{ book.SignatureSubPath }}`.
2. Download the X.509 certificate (PEM) from the URL of `SignatureCEKCertChainUrl`.
3. Check that the value of the Subject Alternative Name (SAN) field in the downloaded certificate is `{{ book.SignatureSANDomain }}`.
4. Check that all chains have been created using a trusted root certificate.
5. Check that the downloaded certificate is valid.

**Generate a hash value and validate the message**
1. Decode the value of `SignatureCEK` in Base64.
2. Using the downloaded public key of the certificate, decrypt the decoded value of `SignatureCEK`.
3. Generate an SHA-1 hash value using the body of HTTPS request message.
4. Compare the decrypted value in step 2 and the hash value generated in step 3 and check that the two values are identical.

<div class="note">
  <p><strong>Note!</strong></p>
  <p>If the certificate cannot be trusted or if the two values compared in the <strong>generate a hash value and validate the message</strong> process are different, we recommend that you discard the corresponding request.</p>
</div>
