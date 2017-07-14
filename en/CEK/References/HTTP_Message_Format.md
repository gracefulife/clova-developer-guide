# HTTP message
CEK and your extension communicates over the HTTP/1.1 protocols, sending and receiving simple HTTPS requests and responses. When CEK and your extension communicates with each other, a JSON format message is included in the body of the HTTP message. The following explains how an HTTP message is constructed for communication between CEK and your extension.

## HTTP header {#HTTPHeader}
An HTTPS request is used when CEK sends analysis details of user's speech input to your extension. The header of an HTTPS request is constructed as follows.

{% raw %}
```
POST /APIpath HTTP/1.1
Host: your.extension.endpoint
Content-Type: application/json;charset-UTF-8
Accept:  application/json
Accept-Charset : utf-8
```
{% endraw %}

* Use HTTPS connection (HTTP/1.1 version) and POST method.
* Fill the host and target path with a pre-defined URI.
* Message body is in JSON format and uses UTF-8 encoding.


Conversely, an HTTPS response is used when your extension returns processing results to CEK. You only need to include the very basics in the header of an HTTPS response as follows.
{% raw %}
```
HTTP/1.1 200 OK
Content-Type: application/json;charset-UTF-8
```
{% endraw %}
* Return processing results in response to an HTTPS request sent from CEK.
* Message body is in JSON format and uses UTF-8 encoding.

## HTTP body {#HTTPBody}
For both request and response, the HTTP body is in JSON format and contains analysis details of user's speech input or processing results from your extension. Each message is constructed in different ways depending on which type of extension you use. See [custom extension message](/CEK/References/Custom_Extension_Message_Format.md) and [Clova Home extension message](/CEK/References/Clova_Home_Extension_Message_Format.md) for more details on constructing a message.
