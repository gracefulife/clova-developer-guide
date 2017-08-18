# Custom extension message
When CEK and your custom extension exchange information, they use custom extension messages. A custom extension message is divided into [request message](#RequestMessage) and [response message](#ResponseMessage).

## Request message {#RequestMessage}
When CEK sends a user request (analyzed by Clova) to your custom extension, it sends a request message (HTTPS request). The following explains the structure and fields of a request message and how the `request` field is configured for each type of request.

### Message format

{% raw %}
```json
{
  "context": {
    "AudioPlayer": {
      "offsetInMilliseconds": {{number}},
      "playerActivity": {{string}},
      "stream": {{AudioStreamObject}},
      "totalInMilliseconds": {{number}},
    },
    "System": {
      "device": {
        "deviceId": {{string}}
      },
      "user": {
        "userId": {{string}},
        "accessToken": {{string}}
      }
    }
  },
  "request": {{object}},
  "session": {
    "new": {{bolean}},
    "sessionId": {{string}},
    "user": {
      "userId": {{string}},
      "accessToken": {{string}}
    }
  },
  "version": {{string}}
}
```
{% endraw %}

### Message field
| Field name  | Type  | Field description  | Required |
|---------------|---------|-----------------------------|---------|
| `context`  | object  | An object containing context information of the client  | Yes |
| `context.AudioPlayer`  | object  | An object containing details of media currently playing or previously played | No |
| `context.AudioPlayer.offsetInMilliseconds` | number  | The last playback point (offset) of the recently played media. Unit is millisecond. This field can be empty if `playerActivity` is set to "IDLE".  | No |
| `context.AudioPlayer.playerActivity`  | string  | Indicates the state of the player. Available values are:<ul><li><strong>"IDLE"</strong>: Player is idle</li><li><strong>"PLAYING"</strong>: Player is playing</li><li><strong>"PAUSED"</strong>: Player paused playing</li><li><strong>"STOPPED"</strong>: Player stopped playing</li></ul> | Yes |
| `context.AudioPlayer.stream`  | [AudioStreamObject](/CIC/References/APIs/AudioPlayer.md#AudioStreamObject) | An object containing details of the currently playing media. This field can be empty if `playerActivity` is set to **"IDLE"**.  | No |
| `context.AudioPlayer.totalInMilliseconds`  | number  | The total length of the recently played media. Unit is millisecond. This field can be empty if `playerActivity` is set to "IDLE".  | No |
| `context.System`  | object  | An object containing context information of the client system  | Yes |
| `context.System.device`  | object  | An object containing information of the client device  | Yes |
| `context.System.device.deviceId`  | string  | The ID of the client device. Returns information that helps identify the user device, such as a combination of model name and device serial number. | Yes |
| `context.System.user`  | object  | An object containing information of the default user who has been authenticated in the client device  | Yes |
| `context.System.user.userId`  | string  | The Clova ID of the default device user  | Yes |
| `context.System.user.accessToken`  | string  | The access token for the user's service account. The access token belongs to a user account which is associated with a default device user. CEK forwards the access token by obtaining it from the authorization server of a 3rd party service. See [Linking user account](/CEK/Guides/LinkUserAccount.md) for more details. | Yes |
| `request`  | object  | An object containing analysis details of user's speech input. Field configuration can change depending on the [request type](#RequestType). | Yes |
| `session`  | object  | An object containing session information. A session is a logical unit that distinguishes individual user request.  | Yes |
| `session.new`  | boolean | Distinguishes whether the request message is from a new session or previous session. <ul><li>true: New session</li><li>false: Previous session</li></ul>  | Yes |
| `session.sessionId`  | string  | A session ID  | Yes |
| `session.user`  | object  | An object containing information on the current user.  | Yes |
| `session.user.userId`  | string  | The Clova ID of the current user. It can be different from the `context.System.user.userId` value. | Yes |
| `session.user.accessToken`  | string  | The access token for the user's service account. The access token belongs to a user account which is associated with a current user. CEK forwards the access token by obtaining it from the authorization server of a 3rd party service. See [Linking user account](/CEK/Guides/LinkUserAccount.md) for more details. | No |
| `version`  | string  | The version of the message format (CEK version)  | Yes |


### Request type {#RequestType}
A request message is divided into three types as follows. For each type, the `request` object has different field configuration.
* [`LaunchRequest`](#LaunchRequest)
* [`IntentRequest`](#IntentRequest)
* [`SessionEndedRequest`](#SessionEndedRequest)

#### LaunchRequest {#LaunchRequest}
The `LaunchRequest` type notifies that a user has started an extension. For example, a user can request to start a certain mode by saying, "Let's talk in English." Typically, this type of message is sent to extensions that provide a requested service by initiating a mode.

When the message type is `LaunchRequest`, the `request` object field is configured as follows.

{% raw %}
```json
{
  "type": "LaunchRequest"
}
```
{% endraw %}

| Field name  | Type  | Field description  | Required |
|---------------|---------|-----------------------------|---------|
| `type`  | string  | The type of the request message. The value is always **"LaunchRequest"**. | Yes |

This is an example of LaunchRequest type message.

#### IntentRequest {#IntentRequest}
The `IntentRequest` type sends analyzed user requests to perform appropriate actions. When you build a service, you must register an interaction model in the Clova Developer Console to define how your extension will receive and handle user requests. Every individual user request is defined into a form of data called "intent". Analyzed results of a user's speech input is converted to an intent and is sent to your extension through the `intent` field.

<div class="note">
  <p><strong>Note!</strong></p>
  <p>The Clova Developer Console is currently under development. Contact your counterpart contact personnel to ask for help with defining an interaction model.</p>
</div>

When the message type is `IntentRequest`, the `request` object field is configured as follows.

{% raw %}
```json
{
  "type": "IntentRequest",
  "intent": {
    "name": {{string}},
    "slots": {{object}}
  }
}
```
{% endraw %}

| Field name  | Type  | Field description  | Required |
|---------------|---------|-----------------------------|---------|
| `type`  | string  | The type of the request message. The value is always **"IntentRequest"**.  | Yes |
| `intent`  | object  | An object (intent) containing analysis details of a user request  | Yes |
| `intent.name`  | string  | The name of the intent. This field lets you identify the intent defined in the interaction model.  | Yes |
| `intent.slots`  | object  | An object containing slot information which your extension uses to process the intent. The configuration of this field can change depending on the `intent.name` field. | Yes |


#### SessionEndedRequest {#SessionEndedRequest}
The `SessionEndedRequest` type notifies that a user has ended an extension. Your extension can receive this message when:
* The user has requested to end an extension.
* The user did not give any input for a specified time (timeout).
* An error has occurred.

<div class="note">
  <p><strong>Note!</strong></p>
  <p>You will not receive this message if the extension declares its ending beforehand by returning a <a href="ResponseMessage">response message</a> with the <code>shouldEndSession</code> field.</p>
</div>


When the message type is `SessionEndedRequest`, the `request` object field is configured as follows.

{% raw %}
```json
{
  "type": "EndRequest"
}
```
{% endraw %}

| Field name  | Type  | Field description  | Required |
|---------------|---------|-----------------------------|---------|
| `type`  | string  | The type of the request message. The value is always **"EndRequest"**. | Yes |

### Message example
{% raw %}
```json
// Example 1: LaunchRequest type
{
  "version": "0.1.0",
  "session": {
    "new": true,
    "sessionId": "a29cfead-c5ba-474d-8745-6c1a6625f0c5",
    "user": {
      "userId": "V0qe",
      "accessToken": "XHapQasdfsdfFsdfasdflQQ7"
    }
  },
  "context": {
    "System": {
      "user": {
        "userId": "V0qe",
        "accessToken": "XHapQasdfsdfFsdfasdflQQ7"
      },
      "device": {
        "deviceId": "096e6b27-1717-33e9-b0a7-510a48658a9b"
      }
    }
  },
  "request": {
    "type": "LaunchRequest"
  }
}

// Example 2: IntentRequest type
{
  "version": "0.1.0",
  "session": {
    "new": false,
    "sessionId": "a29cfead-c5ba-474d-8745-6c1a6625f0c5",
    "user": {
      "userId": "V0qe",
      "accessToken": "XHapQasdfsdfFsdfasdflQQ7"
    }
  },
  "context": {
    "System": {
      "user": {
        "userId": "V0qe",
        "accessToken": "XHapQasdfsdfFsdfasdflQQ7"
      },
      "device": {
        "deviceId": "096e6b27-1717-33e9-b0a7-510a48658a9b"
      }
    }
  },
  "request": {
    "type": "IntentRequest",
    "intent": {
      "name": "FreeTalk",
      "slots": {
        "q": {
          "name": "q",
          "value": "How are you"
        }
      }
    }
  }
}

// Example 3: SessionEndedRequest type
{
  "version": "0.1.0",
  "session": {
    "new": false,
    "sessionId": "a29cfead-c5ba-474d-8745-6c1a6625f0c5",
    "user": {
      "userId": "V0qe",
      "accessToken": "XHapQasdfsdfFsdfasdflQQ7"
    }
  },
  "context": {
    "System": {
      "user": {
        "userId": "V0qe",
        "accessToken": "XHapQasdfsdfFsdfasdflQQ7"
      },
      "device": {
        "deviceId": "096e6b27-1717-33e9-b0a7-510a48658a9b"
      }
    }
  },
  "request": {
    "type": "EndRequest"
  }
}
```
{% endraw %}

### See also
* [Handling custom extension request](/CEK/Guides/Build_Custom_Extension.md#HandleCustomExtensionRequest)
* [AudioStreamObject](/CIC/References/APIs/AudioPlayer.md#AudioStreamObject)

## Response message {#ResponseMessage}
After your extension completes processing of a request message, it returns a response message (HTTPS response). The following explains the structure and fields of a response message.

### Message format
{% raw %}
```json
{
  "response": {
    "card": {{object}},
    "directives": [
      {
        "header": {
          "messageId": {{string}},
          "name": {{string}},
          "namespace": {{string}}
        },
        "payload": {{object}}
      }
    ],
    "outputSpeech": {
          "type": {{string}},
          "values": {{SpeechObject|SpeechObject array}},
          "brief": {{SpeechObject}},
          "verbose": {
            "type" : {{string}},
            "values": {{SpeechObject|SpeechObject array}},
          }
    },
    "shouldEndSession": {{boolean}},
  },
  "sessionAttibutes": {{object}},
  "version": {{string}}
}
```
{% endraw %}

### Message field
| Field name  | Type  | Field description  | Required |
|---------------|---------|-----------------------------|---------|
| `response`  | object  | An object containing response details of the extension  | Yes |
| `response.card`  | object  | Data in the format of a [content template](/CIC/References/Content_Templates.md). Returns content to display on a client screen.  | Yes |
| `response.directives[]`  | object array | A directive message which an extension returns to CEK. The directive message API for the `response.directives` field will be available in the future. | Yes |
| `response.directives[].header`  | object  | The header of the directive message  | Yes |
| `response.directives[].header.messageId` | string  | The message ID. It is an identifier that distinguishes individual messages (UUID).  | Yes |
| `response.directives[].header.name`  | string  | The API name of the directive message  | Yes |
| `response.directives[].header.namespace` | string  | The API namespace of the directive message  | Yes |
| `response.directives[].payload`  | object  | An object containing details of the directive message. You can configure payload object and field values differently for each directive message.  | Yes |
| `response.outputSpeech`  | object  | An object containing speech data to be synthesized for audio output. Synthesized speech data is returned to a client through CIC.  | Yes |
| `response.outputSpeech.brief`  | [SpeechObject](#SpeechObject) | Brief speech data to be synthesized for audio output.  | No |
| `response.outputSpeech.type`  | string  | The type of speech data to be synthesized for audio output. <ul><li>"SimpleSpeech": Speech data in a simple sentence format. This is the most basic type. When specifying this value, the <code>response.outputSpeech.values</code> field requires the <a href="#SpeechObject"><code>SpeechObject</code></a> object.</li><li><strong>"SpeechList"</strong>: Speech data in a complex sentence format. Returns speech data consisting of several sentences. When specifying this value, the <code>response.outputSpeech.values</code> field requires the <a href="#SpeechObject"><code>SpeechObject</code></a> object array.</li><li><strong>"SpeechSet"</strong>: Speech data in a combined format. Returns speech data consisting of brief and detailed information to a client device without screen. When specifying this value, <code>response.outputSpeech.brief</code> and <code>response.outputSpeech.verbose</code> fields are required, instead of the <code>response.outputSpeech.values</code> field.</li></ul> | Yes |
| `response.outputSpeech.values`  | [SpeechObject](#SpeechObject) or [`SpeechObject`](#SpeechObject) array | An object or object array containing speech data to be synthesized for audio output on a client device | No |
| `response.outputSpeech.verbose`  | object  | Returns detailed speech data to a client device without screen. | No |
| `response.outputSpeech.verbose.type`  | string  | The type of speech data to be synthesized for audio output. You can input speech data only in simple and complex sentence format. <ul><li><strong>"SimpleSpeech"</strong>: Speech data in a simple sentence format. Returns the most basic type of speech data. When specifying this value, the <code>response.outputSpeech.verbose.values</code> field requires the <a href="#SpeechObject"><code>SpeechObject</code></a> object.</li><li><strong>"SpeechList"</strong>: Speech data in a complex sentence format. Returns speech data consisting of several sentences. When specifying this value, the <code>response.outputSpeech.verbose.values</code> field requires the <a href="#SpeechObject"><code>SpeechObject</code></a> object array.</li></ul> | Yes |
| `response.outputSpeech.verbose.values`  | [SpeechObject](#SpeechObject) or [SpeechObject](#SpeechObject) array | An object or object array containing detailed speech data to be synthesized for audio output on a client device | Yes |
| `response.shouldEndSession`  | boolean  | A flag for a session end. It notifies a client that the extension has ended. It notifies the end of the extension prior to receiving a [`SessionEndedRequest`](#SessionEndedRequest) message.<ul><li>true: Ends the extension.</li><li>false: Keeps using the extension.</li></ul> | Yes |
| `sessionAttributes`  | object  | A field reserved for future use  | Yes |
| `version`  | string  | The version of the message format (CEK version)  | Yes |

<div class="note">
  <p><strong>Note!</strong></p>
  <p>To make your extension return directive messages using the <code>response.directives</code> field, prior consultation is necessary. Contact your counterpart contact personnel to discuss the matter.</p>
</div>

### SpeechObject {#SpeechObject}
SpeechObject is an object reused by `response.outputSpeech` in response messages. It contains speech data in a simple sentence format, in short, the smallest unit of speech data. The object has the following fields.

| Field name  | Type  | Description  | Yes |
|----------------|--------------|--------------------------------------------------------------------|-----|
| `lang`  | string  | The language code for speech synthesis. Available values are:<ul><li><strong>"ko"</strong>: Korean</li><li><strong>"en"</strong>: English</li><li><strong>""</strong>: This field has an empty string when the <code>type</code> field is set to <strong>"URL"</strong>.</li></ul>  | Yes |
| `type`  | string  | The type of the speech data to play. The format of the `value` field value can change depending on the value of this field. Available values are:<ul><li><strong>"PlainText"</strong>: Plain text</li><li><strong>"URL"</strong>: The URI of a file that can play speech audio or music</li></ul>  | Yes |
| `value`  | string  | Data to be synthesized into speech audio  | Yes |

### Message example
{% raw %}
```json
// Example 1: Returns speech data in simple sentence format (SimpleSpeech) - plain text
{
  "version": "0.1.0",
  "sessionAttributes": {},
  "response": {
    "outputSpeech": {
      "type": "SimpleSpeech",
      "values" : {
          "type": "PlainText",
          "lang": "en",
          "value": "Hi, nice to meet you"
      }
    },
    "card": {},
    "directives": [],
    "shouldEndSession": false
  }
}

// Example 2: Returns speech data in complex sentence format (SpeechList) - plain text, URL type
{
  "version": "0.1.0",
  "sessionAttributes": {},
  "response": {
    "outputSpeech": {
      "type": "SpeechList",
      "values": [
        {
          "type": "PlainText",
          "lang": "ko",
          "value": "노래를 불러볼게요."
        },
        {
          "type": "URL",
          "lang": "" ,
          "value": "https://tts.com/song.mp3"
        }
      ]
    },
    "card": {},
    "directives": [],
    "shouldEndSession": true
  }
}

// Example 3: Returns speech data in combined format (SpeechSet) - brief and detailed information
{
  "version": "0.1.0",
  "sessionAttributes": {},
  "response": {
    "outputSpeech": {
      "type": "SpeechSet",
      "brief": {
        "type": "PlainText",
        "lang": "ko",
        "value": "날씨 뉴스 입니다."
      },
      "verbose": {
        "type": "SpeechList",
        "values": [
          {
              "type": "PlainText",
              "lang": "ko",
              "value": "주말까지 전국 장맛비…폭염 누그러져."
          },
          {
              "type": "PlainText",
              "lang": "ko",
              "value": "내일 전국 장맛비…곳곳 국지성 호우 주의."
          }
          ...
        ]
      }
    },
    "card": {},
    "directives": [],
    "shouldEndSession": true
  }
}
```
{% endraw %}

### See also
* [Returning custom extension response](/CEK/Guides/Build_Custom_Extension.md#ReturnCustomExtensionResponse)
* [Content template](/CIC/References/Content_Templates.md)
