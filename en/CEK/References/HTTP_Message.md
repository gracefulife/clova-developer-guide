## HTTP message {#HTTPMessage}
CEK and your extension communicates over the HTTP/1.1 protocol, sending HTTPS requests and responses back and forth. When CEK and your extension communicates with each other, a JSON format message is included in the HTTP message body. The following explains how an HTTP message is constructed when CEK and your extension exchange messages.

### HTTP header {#HTTPHeader}
When CEK sends analysis details of user's speech input to your extension, it uses an HTTPS request. The header of an HTTPS request is constructed as follows.

{% raw %}

```
POST /APIpath HTTP/1.1
Host: your.extension.endpoint
Content-Type: application/json;charset-UTF-8
Accept:  application/json
Accept-Charset : utf-8
```

{% endraw %}

* Uses HTTPS connection (HTTP/1.1 version) and POST method.
* The host and target path is filled with a pre-defined URI.
* The body uses a JSON format and UTF-8 encoding.


Conversely, when your extension returns processing results back to CEK, it uses an HTTPS response. The header of an HTTPS response consists of basic entries as follows.

{% raw %}

```
HTTP/1.1 200 OK
Content-Type: application/json;charset-UTF-8
```

{% endraw %}

* Returns processing results in response to HTTPS requests sent from CEK.
* The body uses a JSON format and UTF-8 encoding.

### HTTP body {#HTTPBody}
For both request and response, the HTTPS message body uses a JSON format, and it contains analysis details of user's speech input or processing results of your extension. Messages are constructed differently depending on which type of extension is used. See [Custom extension message](#CustomExtMessage) and [Clova Home extension message](#ClovaHomeExtMessage) for more details on constructing a message.