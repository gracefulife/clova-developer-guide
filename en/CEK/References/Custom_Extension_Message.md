## Custom extension message {#CustomExtMessage}
When CEK and your custom extension exchange information, they use custom extension messages. A custom extension message is divided into a [request message](#CustomExtRequestMessage) and a [response message](#CustomExtResponseMessage). A request message is dinstinguished into three types such as `LaunchRequest`, `IntentRequest` and `SessionEndedRequest` according to [request types](#CustomExtRequestType).

### Request message {#CustomExtRequestMessage}
Once Clova analyzes a user request, CEK forwards a request message to your custom extension to send the user request (HTTPS request). The following explains the structure and fields of a request message and how the `request` field is configured for each type of request.

#### Message structure

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
    "sessionAttributes": {{object}},
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

#### Message field
| Field name       | Type    | Field description                     | Required |
|---------------|---------|-----------------------------|---------|
| `context`                                  | object  | An object containing context information of the client                                | Yes |
| `context.AudioPlayer`                      | object  | An object containing details of media currently playing or previously played | No |
| `context.AudioPlayer.offsetInMilliseconds` | number  | The last playback point (offset) of the recently played media. Unit is millisecond. This field can be empty if `playerActivity` is set to "IDLE".                                       | No |
| `context.AudioPlayer.playerActivity`       | string  | Indicates the state of the player. Available values are:<ul><li><code>"IDLE"</code>: Player is idle</li><li><code>"PLAYING"</code>: Player is playing</li><li><code>"PAUSED"</code>: Player paused playing</li><li><code>"STOPPED"</code>: Player stopped playing</li></ul> | Yes |
| `context.AudioPlayer.stream`               | [AudioStreamObject](/CIC/References/CICInterface/AudioPlayer.md#AudioStreamObject) | An object containing details of the currently playing media. This field can be empty if `playerActivity` is set to `"IDLE"`.    | No |
| `context.AudioPlayer.totalInMilliseconds`  | number  | The total length of the recently played media. Unit is millisecond. This field can be empty if `playerActivity` is set to "IDLE".                                                                  | No |
| `context.System`                           | object  | An object containing context information of the client system                          | Yes |
| `context.System.device`                    | object  | An object containing information of the client device                               | Yes |
| `context.System.device.deviceId`           | string  | The client device ID. Returns information that can help identify the user device, such as a combination of model name and device serial number. | Yes |
| `context.System.user`                      | object  | An object containing information of the default user who has been authenticated in the client device                 | Yes |
| `context.System.user.userId`               | string  | The Clova ID of the default device user                                    | Yes |
| `context.System.user.accessToken`          | string  | The access token for the user's service account. The access token belongs to a user account which is associated with a default device user. CEK forwards the access token by obtaining it from the authorization server of the 3rd party service. See [Linking user account](/CEK/Guides/LinkUserAccount.md) for more details. | Yes |
| `request`                                 | object  | An object containing analysis details of user's speech input. Field configuration can vary depending on the [request type](#CustomExtRequestType). | Yes |
| `session`                                  | object  | An object containing session information. A session is a logical unit that distinguishes individual user requests.     | Yes |
| `session.new`                              | boolean | Distinguishes whether the request message is from a new session or previous session. <ul><li>true: New session</li><li>false: Previous session</li></ul>  | Yes |
| `session.sessionAttributes`                       | object  | An object that stores information necessary for having a multi-turn dialog with users. Your custom extension returns intermediate information to CEK using the `response.sessionAttributes` field in a [response message](#CustomExtResponseMessage) and receives the same information from the `session.sessionAttributes` field in a request message when it receives additional requests from a user. The object consists of a key-value pair. You can define it when implementing your custom extension. If there is no stored value, an empty object is sent.   | Yes |
| `session.sessionId`                        | string  | A session ID                                                    | Yes |
| `session.user`                            | object  | An object containing information of the current user.                             | Yes |
| `session.user.userId`                      | string  | The Clova ID of the current user. It can be different from the `context.System.user.userId` value. | Yes |
| `session.user.accessToken`                 | string  | The access token for the user's service account. The access token belongs to a user account which is associated with a current user. CEK forwards the access token by obtaining it from the authorization server of the 3rd party service. See [Linking user account](/CEK/Guides/LinkUserAccount.md) for more details. | No |
| `version`                                  | string  | The version of the message format (CEK version)                          | Yes |

#### Message example

{% raw %}

```json
// Example 1: LaunchRequest type
{
  "version": "0.1.0",
  "session": {
    "new": true,
    "sessionAttributes": {},
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
    "sessionAttributes": {},
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
    "sessionAttributes": {},
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

#### See also
* [Handling custom extension request](/CEK/Guides/Build_Custom_Extension.md#HandleCustomExtensionRequest)
* [AudioStreamObject](/CIC/References/CICInterface/AudioPlayer.md#AudioStreamObject)

### Request type {#CustomExtRequestType}
A request message is divided into three types as follows. For each type, the `request` object has different field configuration.
* [`LaunchRequest`](#CustomExtLaunchRequest)
* [`IntentRequest`](#CustomExtIntentRequest)
* [`SessionEndedRequest`](#CustomExtSessionEndedRequest)

#### LaunchRequest {#CustomExtLaunchRequest}
The `LaunchRequest` type notifies that a user has started an extension. For example, a user can request to start a certain mode by saying, "Let's talk in English." Typically, this type of message is sent to an extensions that provides a requested service by initiating a mode.

When the message type is `LaunchRequest`, the `request` object field is configured as follows.

{% raw %}

```json
{
  "type": "LaunchRequest"
}
```
{% endraw %}

| Field name       | Type    | Field description                     | Required |
|---------------|---------|-----------------------------|---------|
| `type`          | string  | The type of the request message. The value is always `"LaunchRequest"`. | Yes |

This is an example of LaunchRequest type message.

#### IntentRequest {#CustomExtIntentRequest}
The `IntentRequest` type sends analysis details of a user request and asks to perform appropriate actions. When you build a service, you must register an interaction model in the Clova Developer Console to define how your extension will receive and handle user requests. Every individual user request is defined into a form of data called "intent". Analyzed results of a user's speech input is converted to an intent and is sent to your extension through the `intent` field.

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

| Field name       | Type    | Field description                     | Required |
|---------------|---------|-----------------------------|---------|
| `type`          | string  | The type of the request message. The value is always `"IntentRequest"`.                                                       | Yes |
| `intent`        | object  | An object (intent) containing analysis details of a user request                                                                | Yes |
| `intent.name`   | string  | The name of the intent. This field lets you identify the intent defined in the interaction model.                                          | Yes |
| `intent.slots`  | object  | An object containing slots necessary for your extension to process the intent. The configuration of this field can vary depending on the `intent.name` field. | Yes |


#### SessionEndedRequest {#CustomExtSessionEndedRequest}
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

| Field name       | Type    | Field description                     | Required |
|---------------|---------|-----------------------------|---------|
| `type`          | string  | The type of the request message. The value is always `"EndRequest"`. | Yes |

### Response message {#CustomExtResponseMessage}
After your extension completes processing of a request message, it returns a response message (HTTPS response). The following explains the structure and fields of a response message.

#### Message structure

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

#### Message field
| Field name       | Type    | Field description                     | Required |
|---------------|---------|-----------------------------|---------|
| `response`                               | object       | An object containing response details of the extension                            | Yes |
| `response.card`                          | object       | Data in the format of a [content template](/CEK/References/Content_Templates.md). It returns content to display on a client screen.           | Yes |
| `response.directives[]`                  | object array | A directive message which an extension returns to CEK. The directive message API for the `response.directives` field will be available in the future. | Yes |
| `response.directives[].header`           | object       | The header of the directive message                                          | Yes |
| `response.directives[].header.messageId` | string       | The message ID. It is an identifier that distinguishes individual messages (UUID).   | Yes |
| `response.directives[].header.name`      | string       | The API name of the directive message                                      | Yes |
| `response.directives[].header.namespace` | string       | The API namespace of the directive message                                | Yes |
| `response.directives[].payload`          | object       | An object containing details of the directive message. You can configure payload object and field values differently for each directive message.         | Yes |
| `response.outputSpeech`                  | object       | An object containing speech data to be synthesized for audio output. Synthesized speech data is returned to a client through CIC.              | Yes |
| `response.outputSpeech.brief`            | [SpeechObject](#CustomExtSpeechObject) | Brief speech data to be synthesized for audio output.                    | No |
| `response.outputSpeech.type`             | string       | The type of speech data to be synthesized for audio output. <ul><li>"SimpleSpeech": Speech data in a simple sentence format. This is the most basic type. When specifying this value, the <code>response.outputSpeech.values</code> field requires a <a href="#CustomExtSpeechObject"><code>SpeechObject</code></a> object.</li><li><code>"SpeechList"</code>: Speech data in a complex sentence format. Returns speech data consisting of several sentences. When specifying this value, the <code>response.outputSpeech.values</code> field requires a <a href="#CustomExtSpeechObject"><code>SpeechObject</code></a> object array.</li><li><code>"SpeechSet"</code>: Speech data in a combined format. Returns speech data consisting of brief and detailed information to a client device without screen. When specifying this value, <code>response.outputSpeech.brief</code> and <code>response.outputSpeech.verbose</code> fields are required, instead of the <code>response.outputSpeech.values</code> field.</li></ul> | Yes |
| `response.outputSpeech.values`           | [SpeechObject](#CustomExtSpeechObject) or [SpeechObject](#CustomExtSpeechObject) array | An object or object array containing speech data to be synthesized for audio output on a client device | No |
| `response.outputSpeech.verbose`          | object       | Returns detailed speech data to a client device without screen. | No |
| `response.outputSpeech.verbose.type`     | string       | The type of speech data to be synthesized for audio output. You can input speech data only in simple and complex sentence format. <ul><li><code>"SimpleSpeech"</code>: Speech data in a simple sentence format. Returns the most basic type of speech data. When specifying this value, the <code>response.outputSpeech.verbose.values</code> field requires a <a href="#CustomExtSpeechObject"><code>SpeechObject</code></a> object.</li><li><code>"SpeechList"</code>: Speech data in a complex sentence format. Returns speech data consisting of several sentences. When specifying this value, the <code>response.outputSpeech.verbose.values</code> field requires a <a href="#CustomExtSpeechObject"><code>SpeechObject</code></a> object array.</li></ul> | Yes |
| `response.outputSpeech.verbose.values`           | [SpeechObject](#CustomExtSpeechObject) or [SpeechObject](#CustomExtSpeechObject) array | An object or object array containing detailed speech data to be synthesized for audio output on a client device | Yes |
| `response.shouldEndSession`              | boolean      | A flag for a session end. It notifies a client that the extension has ended. It notifies ending of an extension prior to receiving a [`SessionEndedRequest`](#CustomExtSessionEndedRequest) message.<ul><li>true: Ends the extension.</li><li>false: Keeps using the extension.</li></ul> | Yes |
| `sessionAttributes`                      | object       | An object that stores information necessary for having a multi-turn dialog with users. Your custom extension returns intermediate information to CEK using the `sessionAttributes` field and receives the same information from the `session.sessionAttributes` field in a [request message](#CustomExtRequestMessage) when it receives additional requests from a user. The object consists of a key-value pair. You can define it when implementing your custom extension. If there is no value to store, enter an empty object. | Yes |
| `version`                                | string       | The version of the message format (CEK version)                        | Yes |

<div class="note">
  <p><strong>Note!</strong></p>
  <p>To make your extension return directive messages via the <code>response.directives</code> field, prior consultation is necessary. Contact your counterpart contact personnel to discuss the matter.</p>
</div>

#### SpeechObject {#CustomExtSpeechObject}
SpeechObject is an object reused by `response.outputSpeech` in response messages. It contains speech data in a simple sentence format, in short, the smallest unit of speech data. The object has the following fields.

| Field name        | Type         | Description                                                                | Yes |
|----------------|--------------|--------------------------------------------------------------------|-----|
| `lang`           | string       | The language code for speech synthesis. Available values are:<ul><li><code>"ko"</code>: Korean</li><li><code>"en"</code>: English</li><li><code>""</code>: This field has an empty string when the <code>type</code> field is set to <code>"URL"</code>.</li></ul>         | Yes |
| `type`           | string       | The type of the speech audio to play. Depending on the value of this field, the `value` field changes its value. Available values are:<ul><li><code>"PlainText"</code>: Plain text</li><li><code>"URL"</code>: A URI of a file that can play speech audio or music</li></ul>            | Yes |
| `value`          | string       | Content to be synthesized into speech audio                                                       | Yes |

#### Message example

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

// Example 4: Stores intermediate information during multi-turn dialog - use sessionAttributes
{
  "version": "0.1.0",
  "sessionAttributes": {
    "RequestedIntent": "OrderPizza",
    "PizzaType": "페퍼로니 피자"
  },
  "response": {
    "outputSpeech": {
      "type": "SimpleSpeech",
      "values" : {
          "type": "PlainText",
          "lang": "ko",
          "value": "몇 판 주문할까요?"
      }
    },
    "card": {},
    "directives": [],
    "shouldEndSession": false
  }
}
```

{% endraw %}

#### See also
* [Returning custom extension response](/CEK/Guides/Build_Custom_Extension.md#ReturnCustomExtensionResponse)
* [Content template](/CEK/References/Content_Templates.md)
