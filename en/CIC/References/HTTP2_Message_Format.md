# HTTP/2 message
You use the [HTTP/2 protocol](https://tools.ietf.org/html/rfc7540) when interacting with CIC. This picture shows how an HTTP/2 message is structured when your client sends a message to CIC.

![](/CIC/Resources/Images/HTTP2_Structure.png)

This section explains the following topics.
* [HTTP request](#request)
  * [CIC base URL](#BaseURL)
  * [HTTP header](#Header)
  * [HTTP multipart message](#MultipartMessage)
* [HTTP response](#Response)

## HTTP request {#Request}
Send HTTP requests, through event messages, to send user requests from your client to CIC.

### CIC base URL {#BaseURL}
Clova uses the following base URL.

{% raw %}
```
https://prod-ni-cic.clova.ai/
```
{% endraw %}

### HTTP header {#Header}
The following header fields are required when connecting with CIC.

{% raw %}
```
:method = {{GET|POST}}
:scheme = https
:path = /{{API Version}}/{{events|directives}}
Authorization = Bearer {{Clova access token}}
content-type = multipart/form-data; boundary={{boundary_term}}
```
{% endraw %}

| Field name          | Message description                                    |
|------------------|---------------------------------------------|
| :method        | CIC supports the following methods. <ul><li>GET: To create a <a href="/CIC/Guides/Interact_with_CIC.html#CreateConnection">downchannel</a></li><li>POST: To send an <a href="/CIC/References/CIC_Message_Format.html#Event">event message</a></li></ul> |
| :scheme        | The CIC APIs support HTTPS communication.                                                                            |
| :path          | Use the following paths when sending event and directive messages. <ul><li>/v1/events</li><li>/v1/directives</li></ul> |
| authorization  | Enter an authorization token obtained from an Clova authorization server. You must include an authorization token in all request headers.                     |
| content-type   | The content type of an HTTP message. Always use *multipart/form-data* because the message type is multipart. Also, specify a message boundary term to separate messages and make the term invisible in a message body. Define the content type of each message in a message header. |

### HTTP multipart message {#MultipartMessage}
After an HTTP header is sent and a connection is established, a stream is created. Through this stream, clients send event messages and CIC returns directive messages. Each message carries JSON data containing information of a request or response, or, carries binary audio data recorded from user's speech input. Message structure is formed as follows depending on the data type.

#### Message structure of JSON data
A JSON-format message contains information of an event message or content. When sending JSON-format data, the message consists of header and body as follows.

{% raw %}
```
[ Message Header ]
Content-Disposition: form-data; name="metadata"
Content-Type: application/json; charset=UTF-8

[ Message Body ]
{
  "context": [
  ],
  "event": {
    "header": {
      "namespace": {{string}},
      "name": {{string}},
      "dialogRequestId": {{string}},
      "messageId": {{string}}
    },
    "payload": {{object}}
  }
}

```
{% endraw %}

Event messages have different configurations depending on which CIC API is in use. See [CIC message](/CIC/References/CIC_Message_Format.md) and [CIC API](/CIC/References/CIC_API.md) for more details on the message structure and API.

#### Message structure of audio data
Audio data has a header as follows and contains binary data in its body. See [SpeechRecognizer.Recognize](/CIC/References/APIs/SpeechRecognizer.md#Recognize) for more details.

{% raw %}
```
[ Message Header ]
Content-Disposition: form-data; name="audio"
Content-Type: application/octet-stream

[ PCM Audio Attachment ]
{{ Binary audio attachment }}
```
{% endraw %}

## HTTP response {#Response}
HTTP responses are directive messages returned from CIC. They have a combination of the following messages.
* [Synthesizer.Speak](/CIC/References/APIs/SpeechSynthesizer.md#Speak) directive message that generates audio output of synthesized speech. It returns audio data additionally.
* Along with a *Synthesizer.Speak* directive message, other directive messages containing additional information can be returned. For example, an [AudioPlayer.Play](/CIC/References/APIs/AudioPlayer.md#Play) directive message returns streaming information.

<div class="note">
  <p><strong>Note!</strong></p>
  <p>Currently, HTTP status codes return error information but exception responses will be available soon.</p>
</div>

## HTTP message example {#MessageExample}
These are examples of HTTP request and response sent and received between a client and CIC.

### Request Example
{% raw %}
```
:method = POST
:scheme = https
:path = /v1/events
authorization = Bearer {{clova-access-token}}
content-type = multipart/form-data; boundary=Boundary-Text

--Boundary-Text
Content-Disposition: form-data; name="metadata"
Content-Type: application/json; charset=UTF-8

{
  "context": [
    {
      "header": {
        "namespace": "Speaker",
        "name": "VolumeState"
      },
      "payload": {
        "volume": 25,
        "muted": false
      }
    }
  ],
  "event": {
    "header": {
      "namespace": "SpeechRecognizer",
      "name": "Recognize",
      "messageId": "277b40c3-b046-4f61-a551-783b1547e7b7",
      "dialogRequestId": "4e4080d6-c440-498a-bb73-ae86c6312806"
    },
    "payload": {
      "profile": "CLOSE_TALK"
    }
  }
}

--Boundary-Text

Content-Disposition: form-data; name="audio"
Content-Type: application/octet-stream

{{binary audio attachment}}
--Boundary-Text--

```
{% endraw %}

### Response Example
{% raw %}
```
:status = 200
content-type = multipart/related; boundary=Boundary-Text; type="application/json"

--Boundary-Text
Content-Type: application/json; charset=UTF-8

{
    "directive": {
        "header": {
            "namespace": "SpeechSynthesizer",
            "name": "Speak",
            "messageId": "277b40c3-b046-4f61-a551-783b1547e7b7",
            "dialogRequestId": "4e4080d6-c440-498a-bb73-ae86c6312806"
        },
        "payload": {
            "url": "cid:1234",
            "format": "AUDIO_MPEG"
            "token": "kr17447380422"
        }
    }
}

--Boundary-Text
Content-Type: application/octet-stream
Content-ID: <1234>

{{binary audio attachment}}
--Boundary-Text--
```
{% endraw %}
