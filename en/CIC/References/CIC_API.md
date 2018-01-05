# CIC API reference

The CIC API is a set of REST APIs provided for clients. The following covers topics related to CIC API.

* [API basics](#BasicInfo)
* [Establishing downchannel](#EstablishDownchannel)
* [Sending events](#SendEvent)
* [Message format](#CICMessageFormat)
* [Interface](#CICInterface)

## API basics {#BasicInfo}

Before using CIC, we recommend you take a look at the basics of the CIC API.

* [Base URL](#BaseURL)
* [Multipart messages](#MultipartMessage)

### Base URL {#BaseURL}
The base URL of the CIC API is as follows.

<pre><code>{{ book.CICBaseURL }}
</code></pre>

### Multipart messages {#MultipartMessage}

Send [events](#Event) to CIC as multipart messages over the HTTP/2 protocol.

![](/CIC/Resources/Images/HTTP2_Structure.png)

Suppose you are sending a user's voice request to CIC. You need to send the [SpeechRecognizer.Recognize](/CIC/References/CICInterface/SpeechRecognizer.md#Recognize) event to CIC along with the voice record, as a multipart message.

To compose a multipart message for your event:

* Set the `Content-Type` to `multipart/form-data`.
* Fill in the first message part with the event information, in JSON.
* Fill in the second message part with binary data containing user's voice recording.
* Specify a delimiter in the `boundary` field to distinguish message blocks.

When specifying the delimiter, add two consecutive hyphens as a prefix to the delimiter. To indicate a message part as the last, add an extra delimiter after the last message part, with a prefix _and_ a suffix, both consisting of two consecutive hyphens (--). Make sure the delimiters are not contained inside a message part.

The following is a general example of a user's request (event) to CIC as a multipart message.

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
      {
        "header": {
          "namespace": "Alerts",
          "name": "AlertsState"
        },
        "payload": {
          "allAlerts": [
            ...
          ],
          "activeAlerts": [
            ...
          ]
        }
      },
      ...
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
      "namespace": {{string}},
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

In general, an HTTP response would contain [directive(s)](#Directive) and an [HTTP status code](https://tools.ietf.org/html/rfc7231#section-6) (200), which indicates success. In our example, the following directives would be received.

* [`Synthesizer.Speak`](/CIC/References/APIs/SpeechSynthesizer.md#Speak): A directive instructing a client to play the given synthesized speech.
* Additional directives: For example, if the user's request had been to play some music, the [`AudioPlayer.Play`](/CIC/References/CICInterface/AudioPlayer.md#Play) directive with streaming information would be returned.

As explained previously, CIC's response to the client is also in the form of a multipart message, consisting of directives and speech data, as follows.

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
      "namespace": {{string}},
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


## Establishing a downchannel {#EstablishDownchannel}

```
GET /v1/directives
```

A client's foremost task is establishing a downchannel with CIC. A downchannel is used by CIC to send directives to clients on its own (cloud-initiated) when certain conditions are met or should needs arise. See [Connecting with CIC](/CIC/Guides/Interact_with_CIC.md#CreateConnection) for more details on how to establish a downchannel.

<div class="danger">
  <p><strong>Caution!</strong></p>
  <p>To <a href="#SendEvent">send events</a> to CIC you MUST create a downchannel. Otheriwse, you cannot send events to CIC.</p>
</div>

### Request header

| Request header | Description                                                                |
|----------------|--------------------------------------------------------------------|
| Authorization  | <p>The Clova access token acquired.</p><pre><code>Bearer [Clova access token]</code></pre> |
| User-Agent  | <p>The <a href="/CIC/Guides/Interact_with_CIC.html#UserAgentString">user-agent string</a>.</p><pre><code>User-Agent: [User-Agent string]</code></pre> |

### Request example

<pre><code>GET /v1/directives HTTP/2
Host: https://prod-ni-cic.clova.ai/
User-Agent: MyOrganizationName/MyAppName/2.1.2-release (Android 7.0;SettopBox;target=KR;other=sample)
Authorization: Bearer XHapQasdfsdfFsdfasdflQQ7w
</code></pre>

### Response header

| Response header | Description                                                       |
|-------------------------|--------------------------------------------------------------------|
| Content-Type    | <p>The content type of the HTTP response message. Set the content type as a <a href="#MultipartMessage">multipart message</a> type plus a delimiter as follows:</p><pre><code>multipart/form-data; boundary=[boundary_term]</code></pre> |

### Response message header

| Response message header | Description                                                       |
|-------------------------|--------------------------------------------------------------------|
| Content-Disposition     | <p>The content metadata for internal use.</p><pre><code>form-data; name="[data]"</code></pre>                   |
| Content-Type            | <p>The content type of the response message.</p><pre><code>application/json; charset=UTF-8</code></pre>            |

### Response message

As a response to the client's request, CIC returns an HTTP response containing the [Clova.Hello](/CIC/References/CICInterface/Clova.md#Hello) directive. This directive indicates that a downchannel has been established between CIC and the client.

### Status codes

| Status code       | Description                     |
|-------------------------|-------------------------|
| 200 OK                    | A status code that is returned when a downchannel has been created successfully and connection is established between a client and CIC. Now, the client can receive cloud-initiated messages, i.e. CIC can initiate sending directives to the client without having to receive a request from client first. |
| 400 Bad Request           | The user request sent to CIC was in a wrong format.                       |
| 401 Unauthorized          | Failed to authenticate the user. Check if the Clova access token is valid. |
| 500 Internal Server Error | An internal server error occurred.                                                      |

### Response example

{% raw %}
```
// If the request was successful
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

// If the request has failed
HTTP/2 400
Content-Type: multipart/related; boundary=883fd3b825c9b883f99b9ffb4d2a2cbd7a24c9c61bfa69d70c51140f34ca;
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

## Sending events to CIC {#SendEvent}

```
POST /v1/events
```

Clients use events to send CIC the user's voice request or the client's current state. Events are sent as HTTP requests and in return, an HTTP response comes containing directives. See [Sending events](/CIC/Guides/Interact_with_CIC.md#SendEvent) and [Handling directives](/CIC/Guides/Interact_with_CIC.md#HandleDirective) for more information.

### Request header

| Request header  | Description                                                                |
|-----------------|--------------------------------------------------------------------|
| Authorization   | <p>The Clova access token acquired.</p><pre><code>Bearer [Clova access token]</code></pre>  |
| Content-Type    | <p>The content type of the HTTP request message. Set the content type as a <a href="#MultipartMessage">multipart message</a> type plus a delimiter as follows:</p><pre><code>multipart/form-data; boundary=[boundary_term]</code></pre>  |

### Request message header

| Request message header  | Description                                                                |
|-------------------------|--------------------------------------------------------------------|
| Content-Disposition     | <p>The content metadata for internal use.</p><pre><code>form-data; name="[data]"</code></pre>                   |
| Content-Type            | <p>The content type of the request message.</p><ul><li>JSON data: <code>application/json; charset=UTF-8</code></li><li>Binary audio data: <code>application/octet-stream</code></li></ul> |

### Request message

To send CIC a user request or the client state, send an [event](#Event) and additional data (e.g. voice data) in the form of a [multipart message](#MultipartMessage). The content and structure of an event are determined by the type of information the event is delivering. This information type is categorized by [interfaces](#CICInterface).

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
        "namespace": "Alerts",
        "name": "AlertsState"
      },
      "payload": {
        "allAlerts": [
          ...
        ],
        "activeAlerts": [
          ...
        ]
      }
    },
    ...
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

| Response header | Description                                                                |
|-----------------|--------------------------------------------------------------------|
| Content-Type    | <p>The content type of the HTTP response message. The content type is specified as <a href="#MultipartMessage">multipart message</a> type plus a delimiter as follows:</p><pre><code>multipart/form-data; boundary=[boundary_term]</code></pre> |

### Response message header

| Response message header | Description                                                                |
|-------------------------|--------------------------------------------------------------------|
| Content-Disposition     | <p>The content metadata for internal use.</p><pre><code>multipart/form-data; boundary=[boundary_term]</code></pre>                                                    |
| Content-ID              | The message ID:<ul><li>UUID format</li><li>A client can identify the messages to be processed by the <code>cid:[UUID]</code> which can be found from the <code>payload</code> field of a directive. </li></ul> |
| Content-Type            | <p>The content type of the response message.</p><ul><li>JSON data: <code>application/json; charset=UTF-8</code></li><li>Binary audio data: <code>application/octet-stream</code></li></ul>  |

### Response message

CIC returns [directives](#Directive) and additional speech data in a [multipart message](#MultipartMessage). The content and configuration of a directive are determined by which directive CIC is sending, which are categorized into [interfaces](#CICInterface).

### Status codes

| Status code       | Description                     |
|---------------|-------------------------|
| 200 OK                    | CIC has successfully received an event from a client and the response contains at least one directive for the client. |
| 204 No Content            | CIC has successfully received an event from a client and there is no directive for the client.                    |
| 400 Bad Request           | The user request was sent in a wrong format.                   |
| 401 Unauthorized          | Failed to authenticate the user. Check if the Clova access token is valid. |
| 500 Internal Server Error | An internal server error occurred.                                  |

### Response example

{% raw %}
```
// If the request was successful
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
      "dialogRequestId":"4e4080d6-c440-498a-bb73-ae86c6312806"
    },
    "payload":{
      "format":"AUDIO_MPEG",
      "token":"e81f7dec-63fb-453d-8bd8-6944bed9a306",
      "ttsLang":"ko",
      "url":"cid:d329085c-379e-48aa-b871-7ecebdbe831d",
      "x-clova-pause-before":0
    }
  }
}

--b4bc211bbd32e5cb5989bc7ab2d3088fdd72dcc6696253151c98176f88ba
Content-Disposition: form-data; name="attachment-39b2f844-b168-4dc2-bea7-d5c249e446e3"
Content-ID: d329085c-379e-48aa-b871-7ecebdbe831d
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
      "dialogRequestId":"4e4080d6-c440-498a-bb73-ae86c6312806"
    },
    "payload":{
      "text":"Nice to meet you."
    }
  }
}

--b4bc211bbd32e5cb5989bc7ab2d3088fdd72dcc6696253151c98176f88ba--

// If the request has failed
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

## Message types {#CICMessageFormat}

The CIC API uses following types of messages, each with a different structure.

* [Events](#Event)
* [Directives](#Directive)
* [Error messages](#Error)

### Events {#Event}

Events are used by clients to send user's voice request or the client's state to CIC. One of the main events used is the [`SpeechRecognizer.Recognize`](/CIC/References/CICInterface/SpeechRecognizer.md#Recognize) event, which requests CIC to take _and_ recognize user's voice request.

#### Event structure

{% raw %}
```json
{
  "context": [
    {{Alerts.AlertsState}},
    {{AudioPlayer.PlaybackState}}
    {{Device.DeviceState}},
    {{Device.Display}},
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

#### Event fields

| Field name       | Type    | Description                     | Required |
|---------------|:---------:|-----------------------------|:---------:|
| `context[]`                      | object array | Contains the client state information to send to CIC. Available states, i.e. [context](/CIC/References/Context_Objects.md) objects are as follows: <ul><li><a href="/CIC/References/Context_Objects.md#AlertsState"><code>Alerts.AlertsState</code></a>: Alarm/timer state</li><li><a href="/CIC/References/Context_Objects.html#PlaybackState"><code>AudioPlayer.PlaybackState</code></a>: Recent playback state</li><li><a href="/CIC/References/Context_Objects.html#DeviceState"><code>Device.DeviceState</code></a>: Client device's state information</li><li><a href="/CIC/References/Context_Objects.html#Display"><code>Device.Display</code></a>: Client device's display information</li><li><a href="/CIC/References/Context_Objects.html#Location"><code>Clova.Location</code></a>: Client's location information</li><li><a href="/CIC/References/Context_Objects.html#SavedPlace"><code>Clova.SavedPlace</code></a>: Details of locations saved on a client</li><li><a href="/CIC/References/Context_Objects.html#VolumeState"><code>Speaker.VolumeState</code></a>: Client speaker's volume level and mute state</li></ul> | Required     |
| `event`                        | object       | Contains the header and the body data (payload) of the event.                                                                 | Required     |
| `event.header`                 | object       | The header of this event.                                                                                                 | Required     |
| `event.header.dialogRequestId` | string       | The dialog ID. When clients send the [`SpeechRecognizer.Regcognize`](/CIC/References/CICInterface/SpeechRecognizer.md#Recognize) event and the [`TextRecognizer.Recognize`](/CIC/References/CICInterface/TextRecognizer.md#Recognize) event, the clients must create and specify a [dialog ID](/CIC/CIC_Overview.md#DialogIDandClientOP).| Optional |
| `event.header.messageId`       | string       | The message ID. Identifies individual messages.                                                                 | Required     |
| `event.header.name`            | string       | The name of the event.                                                                                             | Required     |
| `event.header.namespace`       | string       | The namespace of the event.                                                                                       | Required     |
| `event.payload`                | object       | Contains event details. The structure and field values of the this object depend on the nature ([CIC interface](#CICInterface)) of this event. | Required     |


#### Event example

{% raw %}
```json
{
  "context": [
      {
        "header": {
          "namespace": "Alerts",
          "name": "AlertsState"
        },
        "payload": {
          "allAlerts": [
            ...
          ],
          "activeAlerts": [
            ...
          ]
        }
      },
      ...
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
* [Interfaces](#CICInterface)

### Directives {#Directive}

Directives are used for CIC to deliver instructions to clients either as responses to events (client requests) or as cloud-initiated messages. Directives are usually contain instructions for client to perform, as a result of user's request.

#### Directive structure

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


#### Directive fields

| Field name       | Type    | Description                     | Provided |
|---------------|:---------:|-----------------------------|:---------:|
| `directive`                        | object | Contains the header and the body (`payload`) of the directive.                                                                 | Always |
| `directive.header`                 | object | The header of this directive.                                                                                                 | Always     |
| `directive.header.dialogRequestId` | string | The dialog ID. Use this to identify the dialog associated with this directive. This field may not be provided if this directive is not a response to the [`SpeechRecognizer.Regcognize`](/CIC/References/CICInterface/SpeechRecognizer.md#Recognize) event.  | Conditional  |
| `directive.header.messageId`       | string | The message ID. Identifies individual messages.                                                        | Always |
| `directive.header.name`            | string | The name of this directive.                                                                                             | Always |
| `directive.header.namespace`       | string | The namespace of this directive.                                                                                        | Always |
| `directive.payload`                | object | Contains directive details. The structure and field values of this object depend on the nature ([interface](#CICInterface)) of this directive. | Always |

#### Directive example

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
      "url": "cid:9d5d37a3-0e70-41a6-a671-e1a40c7ea4d8",
      "x-clova-pause-before": 0
    }
  }
}
```
{% endraw %}

#### See also

* [Interfaces](#CICInterface)

### Error messages {#Error}

Clova may not be able to provide its service properly if you send events in a wrong format or in invalid ways, or if an internal server error occurs. In such cases, CIC returns error messages to clients. To handle errors, implement your client to provide corresponding UX or UI for the given error.

#### Error message structure

{% raw %}
```json
{
  "header": {
    "namespace": "System",
    "name": "Exception",
    "messageId": {{string}}
  },
  "payload": {
    "code": {{string}},
    "description": {{string}}
  }
}
```
{% endraw %}


#### Error fields

| Field name       | Type    | Description                     | Provided |
|---------------|:---------:|-----------------------------|:---------:|
| `header`                 | object | The header of the error message                                             | Always |
| `header.messageId`       | string | The message ID. This is an identifier for distinguishing error messages.            | Always |
| `header.name`            | string | The name of the error message. The value is always `"Exception"`.                | Always |
| `header.namespace`       | string | The namespace of the error message. The value is always `"System"`.             | Always |
| `payload`                | object | The details of the error.                                | Always |
| `payload.code`           | string | The error code. This has the same value as the HTTP response code of the message.           | Always |
| `payload.description`    | string | The error message.                                                  | Always |


#### Error code reference

| Error code | Description                             |
|---------|---------------------------------|
| 400     | The user request sent was in a wrong format.                       |
| 401     | Failed to authenticate the user. Check if the Clova access token is valid. |
| 500     | An internal server error occurred.                                                      |

<div class="note">
  <p><strong>Note!</strong></p>
  <p>More error codes are to be added.</p>
</div>

### Error message example

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

## Interfaces {#CICInterface}

CIC messages are defined and categorized into namespaces by their purpose and usage. Use these interfaces to create events to send to CIC or to interpret directives returned from CIC.

Available namespaces are as follows. Click each link to find out more about a namespace.

* [Alerts](/CIC/References/CICInterface/Alerts.md)
* [AudioPlayer](/CIC/References/CICInterface/AudioPlayer.md)
* [Clova](/CIC/References/CICInterface/Clova.md)
* [DeviceControl](/CIC/References/CICInterface/DeviceControl.md)
* [Notifier](/CIC/References/CICInterface/Notifier.md)
* [PlaybackController](/CIC/References/CICInterface/PlaybackController.md)
* [SpeechRecognizer](/CIC/References/CICInterface/SpeechRecognizer.md)
* [SpeechSynthesizer](/CIC/References/CICInterface/SpeechSynthesizer.md)
* [System](/CIC/References/CICInterface/System.md)
* [TextRecognizer](/CIC/References/CICInterface/TextRecognizer.md)

See the following indexes for a full list of interfaces grouped into events and directives.

* [Event messages index](/CIC/References/CICInterface/Index_for_Events.md)
* [Directive messages index](/CIC/References/CICInterface/Index_for_Directives.md)
