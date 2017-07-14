# Custom extension message
A custom extension message is used when your custom extension sends and receives information to and from CEK. A custom extension message is divided to [request message](#RequestMessage) and [response message](#ResponseMessage).

## Request message {#RequestMessage}
CEK sends a request message to your custom extension to send a user request analyzed by Clova (HTTPS request). The following explains the structure and fields of a request message and how the *request* field is configured differently in each type of request.

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
| Field name                               | Type                                     | Field description                        | Required |
| ---------------------------------------- | ---------------------------------------- | ---------------------------------------- | -------- |
| context                                  | object                                   | Object containing context information of the client | Yes      |
| context.AudioPlayer                      | object                                   | Object containing information of the media being currently played or was lastly played | No       |
| context.AudioPlayer.offsetInMilliseconds | number                                   | Last playback point (offset) of the recently played media. Unit is a millisecond. This field can be left empty when *playerActivity* is "IDLE". | No       |
| context.AudioPlayer.playerActivity       | string                                   | Indicates the state of the player. Available values are:<ul><li>IDLE: Player is in an idle state</li><li>PLAYING: Player is in a playing state</li><li>PAUSED: Player is in a paused state</li><li>STOPPED: Player is in a stopped state</li></ul> | Yes      |
| context.AudioPlayer.stream               | [AudioStreamObject](/CIC/References/APIs/AudioPlayer.md#AudioStreamObject) | Object containing details of currently playing media. This field can be left empty when *playerActivity* is "IDLE". | No       |
| context.AudioPlayer.totalInMilliseconds  | number                                   | Total length of the media recently played. Unit is a millisecond. This field can be left empty when *playerActivity* is "IDLE". | No       |
| context.System                           | object                                   | Object containing context information of the client system | Yes      |
| context.System.device                    | object                                   | Object containing information of the client device | Yes      |
| context.System.device.deviceId           | string                                   | Client device ID. Returns information that can help identify the user device, such as a combination of model name and device serial number. | Yes      |
| context.System.user                      | object                                   | Object containing information of the default user who has completed authentication in the client device | Yes      |
| context.System.user.userId               | string                                   | Clova ID of the device default user      | Yes      |
| context.System.user.accessToken          | string                                   | Access token for the user account of 3rd party service. The access token is passed on for the user account which is linked with default device user. CEK forwards the access token obtained from the authorization server of 3rd party service. See [Linking user account](/CEK/Guides/LinkUserAccount.md) for more details. | Yes      |
| request                                  | object                                   | Object containing analysis details of user's speech input. The field configuration can vary depending on the [request type](#RequestType). | Yes      |
| session                                  | object                                   | Object containing session information. A session is a logical unit that represents each individual user request. | Yes      |
| session.new                              | boolean                                  | Indicates whether the request message is from a new session or previous session. <ul><li>true: New session</li><li>false: Previous session</li></ul> | Yes      |
| session.sessionId                        | string                                   | Session ID                               | Yes      |
| session.user                             | object                                   | Object containing information of the current user. | Yes      |
| session.user.userId                      | string                                   | Clova ID of the current user. The value may not be the same as that of *context.System.user.userId*. | Yes      |
| session.user.accessToken                 | string                                   | Access token for the user account of 3rd party service. The access token is passed on for the user account which is linked with current user. CEK forwards the access token obtained from the authorization server of 3rd party service. See [Linking user account](/CEK/Guides/LinkUserAccount.md) for more details. | No       |
| version                                  | string                                   | Version of message format (CEK version)  | Yes      |


### Request type {#RequestType}
A request message is divided to three types as follows and each type has a *request* object with different field configuration.
* [LaunchRequest](#LaunchRequest)
* [IntentRequest](#IntentRequest)
* [SessionEndedRequest](#SessionEndedRequest)

#### LaunchRequest {#LaunchRequest}
The *LaunchRequest* type notifies that a user has started a particular extension. For example, a user can request to start a particular mode by saying, "Let's start conversation in English." Typically, this type of message is sent to an extension that provides a service by initiating a certain mode.

When the message type is *LaunchRequest*, the *request* object field is configured as follows.

{% raw %}
```json
{
  "type": "LaunchRequest"
}
```
{% endraw %}

| Field name | Type   | Field description                        | Required |
| ---------- | ------ | ---------------------------------------- | -------- |
| type       | string | Request message type. It is fixed to "LaunchRequest". | Yes      |

This is an example of LaunchRequest type message.

#### IntentRequest {#IntentRequest}
*IntentRequest* is used to send analysis details of a user request and perform appropriate actions accordingly. When you build a service, you must register an interaction model in Clova Developer Console to define how your extension will receive and handle user requests. Each individual user request is defined in a form of data called "intent". Analysis details of a user's speech input is converted to an intent and sent to your extension through the *intent* field.

<div class="note">
  <p><strong>Note!</strong></p>
  <p>Clova Developer Console is still under development. Contact your counterpart contact personnel to ask for help with defining an interaction model.</p>
</div>

When the message type is *IntentRequest*, the *request* object field is configured as follows.

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

| Field name   | Type   | Field description                        | Required |
| ------------ | ------ | ---------------------------------------- | -------- |
| type         | string | Request message type. It is fixed to "IntentRequest". | Yes      |
| intent       | object | Object containing analysis details of a user request (intent) | Yes      |
| intent.name  | string | Intent name. Use this field to identify the intent defined in the interaction model. | Yes      |
| intent.slots | object | Object containing slot information which your extension uses to process an intent. Its field configuration can vary depending on the *intent.name* field. | Yes      |


#### SessionEndedRequest {#SessionEndedRequest}
The *SessionEndedRequest* type notifies that a user has ended a particular extension. Your extension can receive this message when:
* A user requests to end an extension.
* A user does not give you any input for a specified time (timeout).
* An error occurs.

<div class="note">
  <p><strong>Note!</strong></p>
  <p>This message is not sent when your extension returns a <a href="ResponseMessage">response message</a> with the <em>shouldEndSession</em> field, declaring the end of session beforehand.</p>
</div>


When the message type is *SessionEndedRequest*, the *request* object field is configured as follows.

{% raw %}
```json
{
  "type": "EndRequest"
}
```
{% endraw %}

| Field name | Type   | Field description                        | Required |
| ---------- | ------ | ---------------------------------------- | -------- |
| type       | string | Request message type. It is fixed to "EndRequest". | Yes      |

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
Your extension must return a response message after processing a request message (HTTPS response). The following explains the structure and fields of a response message.

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
| Field name                             | Type                                     | Field description                        | Required |
| -------------------------------------- | ---------------------------------------- | ---------------------------------------- | -------- |
| response                               | object                                   | Object containing a response from extension | Yes      |
| response.card                          | object                                   | Data in the format of [Content Template](/CIC/References/Content_Templates.md). You can use this field to return content you want to display on a client screen. | Yes      |
| response.directives[]                  | object array                             | Directive message sent from extension to CEK. API will be provided in the future for the directive message that will be included in the *response.directives* field. | Yes      |
| response.directives[].header           | object                                   | Header of the directive message          | Yes      |
| response.directives[].header.messageId | string                                   | Message ID. It is used to identify individual messages (UUID). | Yes      |
| response.directives[].header.name      | string                                   | API name of the directive message        | Yes      |
| response.directives[].header.namespace | string       x`                          | API namespace of the directive message   | Yes      |
| response.directives[].payload          | object                                   | Object containing information of the directive message. You can configure payload object and field values for each directive message. | Yes      |
| response.outputSpeech                  | object                                   | Object containing speech data to be synthesized for audio output | Yes      |
| response.outputSpeech.brief            | [SpeechObject](#SpeechObject)            | Brief speech data to be synthesized for audio output. | No       |
| response.outputSpeech.type             | string                                   | Type of speech data to be synthesized for audio output. <ul><li>"SimpleSpeech": Speech output data in simple sentence format. This is the most basic type. When specifying this value, include <a href="#SpeechObject">SpeechObject</a> in the <em>response.outputSpeech.values</em> field.</li><li>"SpeechList": Speech output data in complex sentence format. It is used when speech output data consists of several sentences. When specifying this value, include <a href="#SpeechObject">SpeechObject</a> array in the <em>response.outputSpeech.values</em> field.</li><li>"SpeechSet": Speech output data in combined format. It is used to return speech output data consisting of brief and detailed information to a client device without screen. When specifying this value, use <em>response.outputSpeech.brief</em> and <em>response.outputSpeech.verbose</em> fields instead of <em>response.outputSpeech.values</em> field.</li></ul> | Yes      |
| response.outputSpeech.values           | [SpeechObject](#SpeechObject) or [SpeechObject](#SpeechObject) array | Object or object array containing speech data to be synthesized for audio output on a client device | No       |
| response.outputSpeech.verbose          | object                                   | It is used to return detailed speech output data to a client device without screen. | No       |
| response.outputSpeech.verbose.type     | string                                   | Type of speech data to be synthesized for audio output. You can input speech data only in simple and complex sentence format. <ul><li>"SimpleSpeech": Speech data in simple sentence format. It is used to return the most basic type of speech data. When specifying this value, include <a href="#SpeechObject">SpeechObject</a> in the <em>response.outputSpeech.verbose.values</em> field.</li><li>"SpeechList": Speech data in complex sentence format. It is used for speech output data consisting of several sentences. When specifying this value, include the <a href="#SpeechObject">SpeechObject</a> array in the <em>response.outputSpeech.verbose.values</em> field.</li></ul> | Yes      |
| response.outputSpeech.verbose.values   | [SpeechObject](#SpeechObject) or [SpeechObject](#SpeechObject) array | Object or object array containing detailed speech data to be synthesized for audio output on a client device | Yes      |
| response.shouldEndSession              | boolean                                  | Flag for the end of a session. It notifies a client that a particular extension has ended. It is used to notify that the extension has ended prior to receiving a [SessionEndedRequest](#SessionEndedRequest) message.<ul><li>true: End session</li><li>false: Do not end session</li></ul> | Yes      |
| sessionAttributes                      | object                                   | Field is reserved for future use         | Yes      |
| version                                | string                                   | Version of message format (CEK version)  | Yes      |

<div class="note">
  <p><strong>Note!</strong></p>
  <p>Prior consultation is necessary if you want your extension to send a directive message on its own using the <em>response.directives</em> field. Contact your counterpart contact personnel to discuss the matter.</p>
</div>

### SpeechObject {#SpeechObject}
SpeechObject is an object reused in *response.outputSpeech* of a response message. It contains speech output data in simple sentence format, which is the smallest unit of speech data. The object has the following fields.

| Field name | Type   | Description                              | Yes  |
| ---------- | ------ | ---------------------------------------- | ---- |
| lang       | string | Language code to by used for speech synthesis. Currently available values are:<ul><li>"ko": Korean</li><li>"en": English</li><li>"": This field has an empty string when <em>type</em> field is set to "URL".</li></ul> | Yes  |
| type       | string | Type of speech data for playback. Depending on the value in this field, value formats can vary. Currently available values are:<ul><li>"PlainText": Plain text</li><li>"URL": URI of audio or music for playback</li></ul> | Yes  |
| value      | string | Data to be synthesized to speech         | Yes  |

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
* [Content Template](/CIC/References/Content_Templates.md)