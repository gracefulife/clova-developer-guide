# CIC API reference
CIC API is REST API provided for clients. The following covers topics related to CIC API.
* [API basics](#BasicInfo)
* [Establishing downchannel](#EstablishDownchannel)
* [Sending event message](#SendEvent)
* [Message format](#CICMessageFormat)
* [Interface](#CICInterface)

## API basics {#BasicInfo}
Understand the following basics before using CIC API.
* [Base URL](#BaseURL)
* [Multipart message](#MultipartMessage)

### Base URL {#BaseURL}
CIC API uses the following base URL.

<pre><code>{{ book.CICBaseURL }}
</code></pre>

### Multipart message {#MultipartMessage}
Clients send [event messages](#Event) in the form of a multipart message over the HTTP/2.

![](/CIC/Resources/Images/HTTP2_Structure.png)

For example, to send user's speech input to CIC, send a [SpeechRecognizer.Recognize](/CIC/References/APIs/SpeechRecognizer.md#Recognize) event message, with recorded speech data attached to it. Set `Content-Type` to `multipart/form-data`, fill in the first message block with JSON-format data containing an event message, and fill in the second message block with binary data containing user's speech audio.

Also, specify a message boundary term in `boundary` to separate messages. When adding a boundary term between message blocks, put two consecutive hyphens (-) on the left of the boundary term. At the end of the last message block, add a boundary term and put two consecutive hyphens (-) on both sides of the term. Make the boundary term invisible in the body of each message block.

To send user requests (event message) to CIC, clients usually send messages similar to the following example.

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

[[ binary audio attachment ]]

--this-is-boundary-text--

```
{% endraw %}

Usually, an HTTP response returns a [directive message](#Directive) with an [HTTP status code](https://tools.ietf.org/html/rfc7231#section-6) (200), which indicates success. It has a combination of the following messages.
* A [`Synthesizer.Speak`](/CIC/References/APIs/SpeechSynthesizer.md#Speak) directive message that plays speech audio. It returns speech data additionally.
* Along with a `Synthesizer.Speak` directive message, other directive messages containing additional information can be returned. For example, an [`AudioPlayer.Play`](/CIC/References/APIs/AudioPlayer.md#Play) directive message can be returned to provide streaming details.

As explained above, when responses are returned from CIC to a client, they take the form of a multipart message, consisting of multiple directive messages and speech data. The structure is as follows.

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

[[ binary audio attachment ]]

--this-is-boundary-text

...

--this-is-boundary-text--

```
{% endraw %}


## Establishing downchannel {#EstablishDownchannel}
A client's foremost task is to establishing a downchannel with CIC. A downchannel is used by CIC to send directive messages to clients on its own (cloud-initiated) when certain conditions are met or any needs arise. See [Connecting with CIC](/CIC/Guides/Interact_with_CIC.md#CreateConnection) for more details on how to establish a downchannel.

```
GET /v1/directives
```

### Request header

* Authorization: A Clova access token you have obtained
  * Bearer [Clova access token]

### Request example

<pre><code>GET /v1/directives HTTP/2
Host: {{ book.CICBaseURL }}
Authorization: Bearer XHapQasdfsdfFsdfasdflQQ7w
</code></pre>

### Response header

* Content-Type - Declare a [multipart message](#MultipartMessage) type and a boundary term
  * multipart/form-data; boundary=[boundary_term]

### Response message header

* Content-Disposition
  * form-data; name="[data]" format
* Content-Type
  * application/json; charset=UTF-8

### Response message
CIC returns an HTTP response by sending a [Clova.Hello](/CIC/References/APIs/Clova.md#Hello) directive message to a client. It indicates that a downchannel has been established.

### Status codes

| Status code       | Description                     |
|---------------|-------------------------|
| 200 OK                    | A downchannel has been properly connected and established. Now CIC can send directive messages on its own (cloud-initiated).        |
| 400 Bad Request           | The user request was sent in a wrong format.                       |
| 401 Unauthorized          | Failed to authenticate the user. Check if the access token is valid. |
| 500 Internal Server Error | An internal server error occurred.                                                      |

### Response Example

{% raw %}
```
// When the request succeeded
HTTP/2 200
Content-Type: multipart/related; boundary=b4bc211bbd32e5cb5989bc7ab2d3088fdd72dcc6696253151c98176f88ba;
date: Fri, 04 Aug 2017 05:27:12 GMT

--b4bc211bbd32e5cb5989bc7ab2d3088fdd72dcc6696253151c98176f88ba
Content-Disposition: form-data; name="helloDirective-836d8db7-5e72-4fb2-9834-7c59291e1f8e"
Content-Type: application/json; charset=utf-8

{
    "directive": {
        "header": {
            "messageId": "2ca2ec70-c39d-4741-8a34-8aedd3b24760",
            "namespace": "Clova",
            "name": "Hello"
        },
        "payload": {}
    }
}
--b4bc211bbd32e5cb5989bc7ab2d3088fdd72dcc6696253151c98176f88ba--

// When the request failed
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

## Sending event message {#SendEvent}
Clients send event messages to send user's speech input or to send information on its current state. Clients send event messages through HTTP requests and receive directive messages through HTTP responses. See [Sending event message](/CIC/Guides/Interact_with_CIC.md#SendEvent) and [Handling directive message](/CIC/Guides/Interact_with_CIC.md#HandleDirective) for more details on how to send and handle event or directive messages.

```
POST /v1/events
```

### Request header

* Authorization: A Clova access token you have obtained
  * Bearer [Clova access token]
* Content-Type - Declare a [multipart message](#MultipartMessage) type and a boundary term
  * multipart/form-data; boundary=[boundary_term]

### Request message header

* Content-Disposition
  * form-data; name="[data]" format
* Content-Type:
  * JSON data: application/json; charset=UTF-8
  * Binary audio data: application/octet-stream

### Request message
To send CIC a user request or client information, send an [event message](#Event) and additional speech data in the form of a [multipart message](#MultipartMessage). The content and configuration of an event message are determined by the type of information in an event message, which are categorized into [interfaces](#CICInterface).

### Request example

<pre><code>POST /v1/events HTTP/2
Host: {{ book.CICBaseURL }}
Accept: */*
Authorization: Bearer XHapQasdfsdfFsdfasdflQQ7w
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

[[ binary audio attachment ]]
--920d6335ba920d6337a319f--
</code></pre>

### Response header

* Content-Type - Declare a [multipart message](#MultipartMessage) type and a boundary term
  * multipart/form-data; boundary=[boundary_term]

### Response message header

* Content-Disposition: Specify a message processing type.
  * `form-data; name="[message processing type]-[UUID]"` format
  * Example of a directive message: form-data; name="speakDirective-836d8db7-5e72-4fb2-9834-7c59291e1f8e"
  * Example of binary audio data: form-data; name="attachment-39b2f844-b168-4dc2-bea7-d5c249e446e3"
* Content-Id: A message identifier
  * UUID format
  * Clients can identify a message to process by a `cid:[UUID]` value in the `payload` field.
* Content-Type:
  * JSON data: application/json; charset=UTF-8
  * Binary audio data: application/octet-stream

### Response message
CIC returns [directive messages](#Directives) and additional speech data in a [multipart message](#MultipartMessage). The content and configuration of a directive message are determined by which directive message CIC has returned, which are categorized into [interfaces](#CICInterface).

### Status codes

| Status code       | Description                     |
|---------------|-------------------------|
| 200 OK                    | CIC has successfully received an event message from a client and the response contains at least one directive message for the client. |
| 204 No Content            | CIC has successfully received an event message from a client and there is no directive message for the client.                    |
| 400 Bad Request           | The user request was sent in a wrong format.                   |
| 401 Unauthorized          | Failed to authenticate the user. Check if the access token is valid. |
| 500 Internal Server Error | An internal server error occurred.                                  |

### Response Example

{% raw %}
```
// When the request succeeded
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

[[ binary audio attachment ]]

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

// When the request failed
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

## Message format {#CICMessageFormat}
CIC APIs use following messages. Each message has a different format.

* [Event message](#Event)
* [Directive message](#Directive)
* [Error message](#Error)

### Event message {#Event}
Event messages are used when a client sends user's speech input or client information to CIC. One example of event messages is [`SpeechRecognizer.Recognize`](/CIC/References/APIs/SpeechRecognizer.md#Recognize), which requests CIC to receive user's speech input and recognize it.

#### Message structure

{% raw %}
```json
{
  "context": [
    {{AudioPlayer.PlaybackState}}
    {{Device.DeviceState}},
    {{Clova.FreetalkState}},
    {{Clova.Location}},
    {{Clova.SavedPlace}},
    {{Speaker.VolumeState}}
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

#### Message field

| Field name       | Type    | Field description                     | Required |
|---------------|---------|-----------------------------|---------|
| `context`                      | object array | An array containing client states to send to CIC. You can include the following [context](/CIC/References/Context_Objects.md) objects in the array. Include them in event messages as necessary.<ul><li><a href="/CIC/References/Context_Objects.html#PlaybackState"><code>AudioPlayer.PlaybackState</code></a>: Recent playback details</li><li><a href="/CIC/References/Context_Objects.html#DeviceState"><code>Device.DeviceState</code></a>: Device details</li><li><a href="/CIC/References/Context_Objects.html#FreetalkState"><code>Clova.FreetalkState</code></a>: Freetalk mode details</li><li><a href="/CIC/References/Context_Objects.html#Location"><code>Clova.Location</code></a>: Device location details</li><li><a href="/CIC/References/Context_Objects.html#SavedPlace"><code>Clova.SavedPlace</code></a>: Pre-defined location details</li><li><a href="/CIC/References/Context_Objects.html#VolumeState"><code>Speaker.VolumeState</code></a>: Speaker details</li></ul> | Yes |
| `event`                        | object       | An object containing the header and necessary data (payload) of the event message                                                                 | Yes |
| `event.header`                 | object       | The header of the event message                                                                                                 | Yes |
| `event.header.dialogRequestId` | string       | The dialog ID. It is used at a CIC side to figure out which dialog is associated with which response. You must enter a value in this field when sending [`SpeechRecognizer.Regcognize`](/CIC/References/APIs/SpeechRecognizer.md#Recognize) event messages. | No |
| `event.header.messageId`       | string       | The message ID. This is an identifier for distinguishing individual messages.                                                                 | Yes |
| `event.header.name`            | string       | The API name of the event message                                                                                             | Yes |
| `event.header.namespace`       | string       | The API namespace of the event message                                                                                       | Yes |
| `event.payload`                | object       | An object containing details of the event message. Configuration of the payload object and its field values can vary depending on which [CIC message interface](#CICInterface) is used. | Yes |

#### Message example

{% raw %}
```json
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
```
{% endraw %}

#### See also
* [Context information](/CIC/References/Context_Objects.md)
* [Interface](#CICInterface)

### Directive message {#Directive}
Directive messages are used when CIC returns responses for event messages (client requests), or when CIC sends information to clients under certain conditions. Directive messages are usually returned to instruct clients to perform specific actions after recognizing intent of a user's speech.

#### Message structure

{% raw %}
```json
{
  "directive": {
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


#### Message field

| Field name       | Type    | Field description                     | Required |
|---------------|---------|-----------------------------|---------|
| `directive`                        | object | An object containing the header and necessary data (`payload`) of the directive message                                                                 | Yes     |
| `directive.header`                 | object | The header of the directive message                                                                                                 | Yes     |
| `directive.header.dialogRequestId` | string | The dialog ID. It is used at a client side to figure out which dialog is associated with which response. A directive message may not include this field if the message is not a response to a [`SpeechRecognizer.Regcognize`](/CIC/References/APIs/SpeechRecognizer.md#Recognize) event message.  | No  |
| `directive.header.messageId`       | string | The message ID. This is an identifier for distinguishing individual messages.                                                                | Yes     |
| `directive.header.name`            | string | The API name of the directive message                                                                                             | Yes     |
| `directive.header.namespace`       | string | The API namespace of the directive message                                                                                       | Yes     |
| `directive.payload`                | object | An object containing details of the directive message. Configuration of the `payload` object and its field values can vary depending on which [interface](#CICInterface) is used. | Yes     |

#### Message example

{% raw %}
```json
{
  "directive": {
    "header": {
      "namespace": "SpeechSynthesizer",
      "name": "Speak",
      "messageId": "277b40c3-b046-4f61-a551-783b1547e7b7",
      "dialogRequestId": "4e4080d6-c440-498a-bb73-ae86c6312806"
    },
    "payload": {
      "format": "AUDIO_MPEG",
      "token": "b5fa5144-1e55-4193-8628-c70283083d9b",
      "ttsLang": "ko",
      "ttsText": "내일 날씨는 오전에는 맑다가 오후에는 구름이 많아지겠어요.",
      "url": "cid:9d5d37a3-0e70-41a6-a671-e1a40c7ea4d8",
      "x-clova-pause-before": 0
    }
  }
}
```
{% endraw %}

#### See also
* [Interface](#CICInterface)

### Error message {#Error}
If you send event messages using incorrect methods or wrong formats, or if internal server error occurs, Clova may not be able to provide its service properly. In such situations, CIC returns error messages to clients. Implement your client to check error messages and provide UX/UI accordingly.

#### Message structure

{% raw %}
```json
{
  "header": {
    "namespace": "System",
    "name": "Exception",
    "messageId": {{string}}
  },
  "payload": {
    "code": "{{string}}",
    "description": "{{string}}"
  }
}
```
{% endraw %}


#### Message field

| Field name       | Type    | Field description                     | Required |
|---------------|---------|-----------------------------|---------|
| `header`                 | object | The header of the error message                                             | Yes |
| `header.messageId`       | string | The message ID. This is an identifier for distinguishing individual messages.            | Yes |
| `header.name`            | string | The name of the error message. The value is always `"Exception"`.                | Yes |
| `header.namespace`       | string | The namespace of the error message. The value is always `"System"`.             | Yes |
| `payload`                | object | An object containing details of the error                                | Yes |
| `payload.code`           | string | The error code. It has the same value as the HTTP response code of the message.           | Yes |
| `payload.description`    | string | The error message.                                                  | Yes |

#### Error code reference

| Error code | Description                             |
|---------|---------------------------------|
| 400     | The user request was sent in a wrong format.                       |
| 401     | Failed to authenticate the user. Check if the access token is valid. |
| 500     | An internal server error occurred.                                                      |

<div class="note">
  <p><strong>Note!</strong></p>
  <p>Error codes will continue to be added.</p>
</div>

### Message example

{% raw %}
```json
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
```
{% endraw %}

#### See also
* [CIC API](/CIC/References/CIC_API.md)

## Interface {#CICInterface}

CIC messages are defined and categorized into namespaces by their functions and usage. You use these interfaces to create event messages to send to CIC or to interpret directive messages returned from CIC.

Available namespaces are as follows. Click each link to find out more about the namespaces.

* [Alerts](/CIC/References/APIs/Alerts.md)
* [AudioPlayer](/CIC/References/APIs/AudioPlayer.md)
* [Clova](/CIC/References/APIs/Clova.md)
* [DeviceControl](/CIC/References/APIs/DeviceControl.md)
* [Memo](/CIC/References/APIs/Memo.md)
* [PlaybackController](/CIC/References/APIs/PlaybackController.md)
* [Reminder](/CIC/References/APIs/Reminder.md)
* [SpeechRecognizer](/CIC/References/APIs/SpeechRecognizer.md)
* [SpeechSynthesizer](/CIC/References/APIs/SpeechSynthesizer.md)
* [TextRecognizer](/CIC/References/APIs/TextRecognizer.md)

See the following indexes for a full list of interfaces grouped into event and directive messages.
* [Event messages index](/CIC/References/APIs/Index_for_Events.md)
* [Directive messages index](/CIC/References/APIs/Index_for_Directives.md)
