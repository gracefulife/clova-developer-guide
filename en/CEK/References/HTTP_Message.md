## HTTP message {#HTTPMessage}
CEK and the extension communicate via the HTTP/1.1 protocol and exchange basic HTTPS requests and HTTPS responses. During this communication, a JSON format message is contained in the HTTP message body. This section explains the configuration of the HTTP message exchanged between CEK and the extension.

### HTTP header {#HTTPHeader}
An HTTPS request is used when CEK sends the analyzed information of user utterance to the extension. The HTTPS request header is configured as follows:

{% raw %}
```
POST /APIpath HTTP/1.1
Host: your.extension.endpoint
Content-Type: application/json;charset-UTF-8
Accept: application/json
Accept-Charset: utf-8
```
{% endraw %}

* HTTPS communication is performed with the HTTP/1.1 version and the POST method is used.
* The values for the host and request target path are filled with the URI defined by the extension developer.
* The body data type is in JSON format and UTF-8 encoding is used.


However, an HTTPS response is used when the extension sends processed result to CEK. The HTTPS response header can just configure basics as follows:
{% raw %}
```
HTTP/1.1 200 OK
Content-Type: application/json;charset-UTF-8
```
{% endraw %}
* As a response to the HTTPS request from CEK, it returns the processed result.
* The body data type is in JSON format and UTF-8 encoding is used.

### HTTP body {#HTTPBody}
Both the body of the HTTPS request message and response message are in JSON format, and it contains the information on user utterance analysis or the processed result of the extension. The configuration of each message varies depending on the extension type. For more information on message configurations, see [Custom extension messages](#CustomExtMessage) and [Clova Home extension messages](#ClovaHomeExtMessage).

