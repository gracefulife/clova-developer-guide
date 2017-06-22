# HTTP/2 message
All communications with CIC is done over the HTTP/2 protocol. This picture shows how an HTTP/2 message is structured when your client sends a message to CIC.

![](/CIC/Resources/Images/HTTP2_Structure.png)

The following topics are covered in this section.
* [HTTP request](#request)
  * [CIC base URL](#BaseURL)
  * [HTTP header](#Header)
  * [HTTP multipart message](#MultipartMessage)
* [HTTP response](#Response)

## HTTP request {#Request}
Typically, an HTTP request is sent when your client delivers a user request to CIC using an Event message.

### CIC base URL {#BaseURL}
Clova uses the following URL as a base URL.

{% raw %}
```
https://prod-ni-cic.clova.ai/
```
{% endraw %}

### HTTP header {#Header}
The following header is required when connecting to CIC.

{% raw %}
```
:method = {{GET|POST}}
:scheme = https
:path = /{{API Version}}/{{events|directives}}
Authorization = Bearer {{Clova access token}}
content-type = multipart/form-data; boundary={{boundary_term}}
```
{% endraw %}

| Field name  | Message description  |
|------------------|---------------------------------------------|
| :method  | CIC supports the following methods. <ul><li>GET: Used when creating a <a href="/CIC/Guides/Interact_with_CIC.html#CreateConnection">Downchannel</a></li><li>POST: Used when sending an <a href="/CIC/References/CIC_Message_Format.html#Event">Event message</a></li></ul> |
| :scheme  | The CIC APIs support HTTPS communication.  |
| :path  | Event and Directive messages use the following paths. <ul><li>/v1/events</li><li>/v1/directives</li></ul> |
| authorization  | Enter an authorization token obtained from the Clova authorization server. An authorization token should be included in the header of all requests.  |
| content-type  | The content type of the HTTP message. Use *multipart/form-data* because it is a multipart message. Also, specify a message boundary term to separate messages and make the term invisible in the message body. The content type of each message is defined in its message header. |

### HTTP multipart message {#MultipartMessage}
Once an HTTP header is transferred and a connection is established, a stream is created. Both CIC and your client send Event or Directive messages through this stream. Each message may carry JSON data containing information of a request or a response, or it may contain binary audio data recorded from user's speech input. Each message is structured as follows depending on the data type.

#### Message structure of JSON data
You use a JSON-format message when you want to send a message containing information about an Event message or content. When a message contains JSON data, the message consists of a header and a body as follows.

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

Each Event message may have different components depending on the CIC API. See [CIC message format](/CIC/References/CIC_Message_Format.md) and [CIC API](/CIC/References/CIC_API.md) for more details on the message structure and API.

#### Message structure of audio data
Audio data has a header as below and contains binary data in the body. See [SpeechRecognizer.Recognize](/CIC/References/APIs/SpeechRecognizer.md#Recognize) for more details.

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
Typically, an HTTP response is a Directive message sent from CIC. It may send the following messages in combination.
* [Synthesizer.Speak](/CIC/References/APIs/SpeechSynthesizer.md#Speak) is a Directive message that produces audio output. It delivers audio data additionally.
* [AudioPlayer.Play](/CIC/References/APIs/AudioPlayer.md#Play) is a Directive message that requires additional information. The message should contain JSON data such as playback streaming information.

<div class="note">
  <p><strong>Note!</strong></p>
  <p>Currently, we are relying on HTTP status code to provide error information but we are preparing to provide responses for exception handling soon.</p>
</div>

## HTTP message example {#MessageExample}
This is an example of an HTTP request/response message sent and received between a client and CIC.

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