# HTTP/2 message
Use the [HTTP/2 protocol](https://tools.ietf.org/html/rfc7540) when interacting with CIC. The picture below shows the structure of HTTP/2 message you send from your client to CIC.

![](/CIC/Resources/Images/HTTP2_Structure.png)

In the following, we will explain:
* [HTTP request](#request)
  * [CIC base URL](#BaseURL)
  * [HTTP header](#Header)
  * [Multipart message](#MultipartMessage)
* [HTTP response](#Response)
* [HTTP message example](#MessageExample)

## HTTP request {#Request}
You usually use HTTP requests to pass on user requests from your client to CIC. In short, event messages are sent through HTTP requests.

### CIC base URL {#BaseURL}
Clova uses the following base URL.

<pre><code>{{ book.CICBaseURL }}
</code></pre>

### HTTP header {#Header}
The following header fields are required when connecting with CIC.

{% raw %}
```
:method = {{GET|POST}}
:scheme = https
:path = /{{API Version}}/{{events|directives}}
Authorization = Bearer {{Clova access token}}
Content-Type = multipart/form-data; boundary={{boundary_term}}
```
{% endraw %}

| Field name  | Message description  |
|------------------|---------------------------------------------|
| :method  | CIC supports the following methods. <ul><li><code>GET</code>: Use when creating a <a href="/CIC/Guides/Interact_with_CIC.html#CreateConnection">downchannel</a></li><li><code>POST</code>: Use when sending an <a href="/CIC/References/CIC_Message_Format.html#Event">event message</a></li></ul> |
| :scheme  | The CIC APIs support HTTPS communication.  |
| :path  | Use the following paths. <ul><li><code>/v1/directives</code>: Use when creating a <a href="/CIC/Guides/Interact_with_CIC.html#CreateConnection">downchannel</a></li><li><code>/v1/events</code>: Use when sending an <a href="/CIC/References/CIC_Message_Format.html#Event">event message</a></li></ul> |
| authorization  | Enter an authorization token obtained from a Clova authorization server. You must include an authorization token in all request headers.  |

## Multipart message {#MultipartMessage}
Usually, [event messages](/CIC/References/CIC_Message_Format.md#Event) are sent in the form of a multipart message.

For example, to send user's speech input to CIC, you send a [SpeechRecognizer.Recognize](/CIC/References/APIs/SpeechRecognizer.md#Recognize) event message, and along with the message, recorded speech data of a user. Set the `Content-Type` to **multipart/form-data**. Fill in the first message block with JSON-formatted data of an event message and fill in the second message block with binary data containing user's speech.

Also, specify a message boundary term in `boundary` to separate messages. When adding a boundary term between message blocks, put two consecutive hyphens (-) on the left of the boundary term. At the end of the last message block, add a boundary term and put two consecutive hyphens (-) on both sides of the term. Also, make the boundary term invisible in the body of each message block.

This is an example message that a client sends to CIC to send a user request (event message).

{% raw %}
```
:method = POST
:scheme = https
:path = /v1/events
authorization = Bearer {{clova-access-token}}
Content-Type = multipart/form-data; boundary=this-is-boundary-text

--this-is-boundary-text
[ Message Header ]
Content-Disposition: form-data; name="metadata"
Content-Type: application/json; charset=UTF-8

[ Message Body ]
{
  "context": [
  ],
  "event": {
    "header": {
      "namespace": "{{string}}",
      "name": {{string}},
      "dialogRequestId": {{string}},
      "messageId": {{string}}
    },
    "payload": {{object}}
  }
}

--this-is-boundary-text
[ Message Header ]
Content-Disposition: form-data; name="audio"
Content-Type: application/octet-stream

[ PCM Audio Attachment ]
{{ Binary audio attachment }}

--this-is-boundary-text--

```
{% endraw %}

<div class="note">
  <p><strong>Note!</strong></p>
  <p>Sending an HTTP request to <code>/v1/directives</code> to create a <a href="/CIC/Guides/Interact_with_CIC.md#CreateConnection">downchannel</a> does not require other message and you do not have to set <code>Content-Type</code>. Write <code>Content-Type</code> appropriately when it is necessary.</p>
</div>

## HTTP response {#Response}
HTTP responses return directive messages or error messages from CIC. Usually, responses return [directive messages](/CIC/References/CIC_Message_Format.md#Directive) along with an [HTTP status code](https://tools.ietf.org/html/rfc7231#section-6) (200) indicating success. They have a combination of the following messages.
* [`Synthesizer.Speak`](/CIC/References/APIs/SpeechSynthesizer.md#Speak) directive message that plays speech audio. It returns speech data additionally.
* Along with a `Synthesizer.Speak` directive message, other directive messages containing additional information can be returned. For example, an [`AudioPlayer.Play`](/CIC/References/APIs/AudioPlayer.md#Play) directive message returns streaming details.

As explained above, when responses are returned from CIC to your client, they take the form of a [multipart message](#MultipartMessage), consisting of multiple directive messages and speech data. Their structure is as follows.

{% raw %}
```
HTTP/2 {{HTTP STATUS CODE}}
Content-Type: multipart/related; boundary=this-is-boundary-text;
date: {{DATETIME}}

--this-is-boundary-text
[ Message Header ]
Content-Disposition: form-data; name="metadata"
Content-Type: application/json; charset=UTF-8

[ Message Body ]
{
  "directive": {
    "header": {
      "namespace": "{{string}}",
      "name": {{string}},
      "dialogRequestId": {{string}},
      "messageId": {{string}}
    },
    "payload": {{object}}
  }
}

--this-is-boundary-text
[ Message Header ]
Content-Disposition: form-data; name="audio"
Content-Type: application/octet-stream

[ PCM Audio Attachment ]
{{ Binary audio attachment }}

--this-is-boundary-text

...

--this-is-boundary-text--

```
{% endraw %}

**If you send a user request in an inaccurate format or if an internal server error occurs,** you will receive an [error message](/CIC/References/CIC_Message_Format.md#Error) along with a corresponding [HTTP status code](https://tools.ietf.org/html/rfc7231#section-6) (4XX or 5XX). Although a single message block is sent in this case, `Content-Type` is still set to **multipart/form-data**. The structure of an error message is as follows.

{% raw %}
```
HTTP/2 400
Content-Type: multipart/related; boundary=this-is-boundary-text;
date: Thu, 03 Aug 2017 01:23:14 GMT

--this-is-boundary-text
Content-Disposition: form-data; name="metadata"
Content-Type: application/json; charset=UTF-8

{
  "header": {
    "namespace": "System",
    "name": "Exception",
    "messageId": {{string}}
  },
  "payload": {{object}
}
--this-is-boundary-text--
```
{% endraw %}

## HTTP message example {#MessageExample}
These are examples of HTTP request/response sent and received between a client and CIC.

### Request Example
{% raw %}
```
POST /v1/events HTTP/2
Host: https://prod-ni-cic.clova.ai/
Accept: */*
Authorization: Bearer {{clova-access-token}}
> Content-Length: 456
> Content-Type: multipart/form-data; boundary=920d6335ba920d6337a319f

--920d6335ba920d6337a319f
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

--920d6335ba920d6337a319f
Content-Disposition: form-data; name="audio"
Content-Type: application/octet-stream

{{binary audio attachment}}
--920d6335ba920d6337a319f--

```
{% endraw %}

### Response Example - When a request succeeds
{% raw %}
```
HTTP/2 200
Content-Type: multipart/related; boundary=b4bc211bbd32e5cb5989bc7ab2d3088fdd72dcc6696253151c98176f88ba;
date: Fri, 04 Aug 2017 05:27:12 GMT

--b4bc211bbd32e5cb5989bc7ab2d3088fdd72dcc6696253151c98176f88ba
Content-Disposition: form-data; name="speakDirective-836d8db7-5e72-4fb2-9834-7c59291e1f8e"
Content-Type: application/json; charset=utf-8

{
  "directive":{
    "header":{
      "namespace":"SpeechSynthesizer",
      "name":"Speak",
      "messageId":"dd4d463e-85a3-4514-927e-c90103c2dd02",
      "dialogRequestId":"dialog-id-here-1"
    },
    "payload":{
      "format":"AUDIO_MPEG",
      "token":"e81f7dec-63fb-453d-8bd8-6944bed9a306",
      "ttsLang":"ko",
      "ttsText":"만나서 반가워요",
      "url":"cid:d329085c-379e-48aa-b871-7ecebdbe831d",
      "x-clova-pause-before":0
    }
  }
}

--b4bc211bbd32e5cb5989bc7ab2d3088fdd72dcc6696253151c98176f88ba
Content-Disposition: form-data; name="attachment-39b2f844-b168-4dc2-bea7-d5c249e446e3"
Content-Id: d329085c-379e-48aa-b871-7ecebdbe831d
Content-Type: application/octet-stream

{{binary audio attachment}}

--b4bc211bbd32e5cb5989bc7ab2d3088fdd72dcc6696253151c98176f88ba
Content-Disposition: form-data; name="renderTextDirective-b2c92b0f-27af-4f5c-b7e7-af7a270c464b"
Content-Type: application/json; charset=utf-8

{
  "directive":{
    "header":{
      "namespace":"Clova",
      "name":"RenderText",
      "messageId":"0fa1b36f-e86c-4979-9494-b00a162c4515",
      "dialogRequestId":"dialog-id-here-1"
    },
    "payload":{
      "text":"만나서 반가워요"
    }
  }
}

--b4bc211bbd32e5cb5989bc7ab2d3088fdd72dcc6696253151c98176f88ba--
```
{% endraw %}

### Response Example - When a request fails
{% raw %}
```
HTTP/2 400
content-type: multipart/related; boundary=883fd3b825c9b883f99b9ffb4d2a2cbd7a24c9c61bfa69d70c51140f34ca;
date: Fri, 04 Aug 2017 09:42:46 GMT

--883fd3b825c9b883f99b9ffb4d2a2cbd7a24c9c61bfa69d70c51140f34ca
Content-Disposition: form-data; name="exception-bde71903-dab4-46c5-9714-416cf12debf0"
Content-Type: application/json; charset=utf-8

{
  "header": {
    "namespace": "System",
    "name": "Exception",
    "messageId": "369b362b-258c-4104-bdf8-dc276548fe51"
  },
  "payload": {
    "code": 400,
    "description": "Could not decode multipart"
  }
}
--883fd3b825c9b883f99b9ffb4d2a2cbd7a24c9c61bfa69d70c51140f34ca--
```
{% endraw %}
