## Custom extension messages {#CustomExtMessage}
Custom extension messages are used when exchanging information between CEK and the custom extension. Custom extension messages are classified as [request message](#CustomExtRequestMessage) and [response message](#CustomExtResponseMessage). Request messages are classified into three types, including `LaunchRequest`, `IntentRequest` and `SessionEndedRequest` depending on the [request type](#CustomExtRequestType).

### Request messages {#CustomExtRequestMessage}
CEK uses a request message to send the user intents analyzed by Clova to the customer extension (HTTPS Request). This section explains the structure of request messages, message fields, request types, and the `request` field that varies by type.

#### Message structure

{% raw %}
```json
{
  "context": {
    "AudioPlayer": {
      "offsetInMilliseconds": {{number}},
      "playerActivity": {{string}},
      "stream": {{AudioStreamInfoObject}},
      "totalInMilliseconds": {{number}},
    },
    "System": {
      "application": {
        "applicationId": {{string}}
      },
      "device": {
        "deviceId": {{string}},
        "display": {
          "contentLayer": {
            "width": {{number}},
            "height": {{number}}
          },
          "dpi": {{number}},
          "orientation": {{string}},
          "size": {{string}}
        }
      },
      "user": {
        "userId": {{string}},
        "accessToken": {{string}}
      }
    }
  },
  "request": {{object}},
  "session": {
    "new": {{boolean}},
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

#### Message fields
| Field       | Data Type    | Description                     | Included |
|---------------|---------|-----------------------------|:---------:|
| `context`                                  | object  | The object that has the context information of the client.                                | Always |
| `context.AudioPlayer`                      | object  | The object that holds the details of media content currently being played or played last. | Conditional |
| `context.AudioPlayer.offsetInMilliseconds` | number  | The most recent playback position (offset) of the recently played media. The unit is milliseconds and this field value may be empty if the `playerActivity` value is "IDLE."                                       | Conditional |
| `context.AudioPlayer.playerActivity`       | string  | The value for indicating the state of player. Values are:<ul><li><code>"IDLE"</code>: Deactivated</li><li><code>"PLAYING"</code>: Playing</li><li><code>"PAUSED"</code>: Paused</li><li><code>"STOPPED"</code>: Stopped</li></ul> | Always |
| `context.AudioPlayer.stream`               | [AudioStreamInfoObject](/CIC/References/CICInterface/AudioPlayer.md#AudioStreamInfoObject) | The object that contains the details of the currently playing media. This field value may be empty if the `playerActivity` value is `"IDLE"`.    | Conditional |
| `context.AudioPlayer.totalInMilliseconds`  | number  | The total duration of the recently played media. The unit is milliseconds and this field value may be empty if the `playerActivity` value is "IDLE."                                                                  | Conditional |
| `context.System`                           | object  | The object that has the context information of the client system.                          | Always |
| `context.System.application`               | object  | The object that has the information of the extension that must be executed by the user intent,       | Always |
| `context.System.application.applicationId` | string  | The extension ID.                                                 | Always |
| `context.System.device`                    | object  | The object that has the context information of the client device.                               | Always |
| `context.System.device.deviceId`           | string  | The client device ID. The device identification information is sent with the combined information of the model name and device serial number. | Always |
| `context.System.device.display`            | object  | The object that has the display information of the client device.                                                 | Always |
| `context.System.device.display.contentLayer`        | object | The object that contains the resolution of the client display used for content. This field is omitted if the value of `context.System.device.display.size` is `"none"`.  | Conditional |
| `context.System.device.display.contentLayer.width`  | number | The width of the content area shown on the display. The unit is pixel (px).             | Always |
| `context.System.device.display.contentLayer.height` | number | The height of the content area shown on the display. The unit is pixel (px).             | Always |
| `context.System.device.display.dpi`         | number | The DPI of the display. This field is omitted if the value of `context.System.device.display.size` is `"none"`.          | Conditional |
| `context.System.device.display.orientation` | string | The direction of the display. This field is omitted if the value of `context.System.device.display.size` is `"none"`.<ul><li><code>"landscape"</code>: Horizontal display</li><li><code>"portrait"</code>: Vertical display</li></ul>                      | Conditional |
| `context.System.device.display.size`        | string | The resolution of the display. A predefined size value or a random value for the resolution size (`"custom"`) may be entered already. Value (`"none"`) may also be entered if there is no display device. <ul><li><code>"none"</code>: No display in client device</li><li><code>"s100"</code>: Low resolution (160px X 107px)</li><li><code>"m100"</code>: Medium resolution (427px X 240px)</li><li><code>"l100"</code>: High resolution (640px X 360px)</li><li><code>"xl100"</code>: Ultrahigh resolution (xlarge type, 899px X 506px)</li><li><code>"custom"</code>: Resolution is not in a predefined specification.</li></ul><div class="note"><p><strong>Note!</strong></p><p>You must provide media content with image quality that is appropriate for screen ratio and DPI of the client device.</p></div> | Always |
| `context.System.user`                      | object  | The object that has authenticated basic user information in the client device.                 | Always |
| `context.System.user.userId`               | string  | Clova ID of the device default user.                                    | Always |
| `context.System.user.accessToken`          | string  | Access token of the user account for a specific service. The access token for the user account connected with the default device user is delivered. CEK sends the access token of a user account acquired from the authorization server of a 3rd party service. For more information, see [Linking user account](/CEK/Guides/Link_User_Account.md). | Always |
| `request`                                 | object  | The object that has the analyzed details of the user utterance. The field configuration will vary depending on the [request type](#CustomExtRequestType). | Always |
| `session`                                  | object  | The object that has the session information. A session is a logical unit used to distinguish user requests.     | Always |
| `session.new`                              | boolean | Distinguishes whether the request message is for a new session or the existing session. <ul><li>true: New session</li><li>false: Existing session</li></ul>  | Always |
| `session.sessionAttributes`                       | object  | The object that stores the information necessary for multi-turn dialog with the user. Custom extension sends temporary information to CEK using the `response.sessionAttributes` field of [response message](#CustomExtResponseMessage) and receives the corresponding information for the `session.sessionAttributes` field again when receiving additional user requests. The object consists of a key-value pair and can be defined arbitrarily when implementing the custom extension. If there is no stored value, an empty object is delivered.   | Always |
| `session.sessionId`                        | string  | Session ID                                                    | Always |
| `session.user`                             | object  | The object that has the information of the current user.                             | Always |
| `session.user.userId`                      | string  | Clova ID of the current user. The value may be different from `context.System.user.userId`. | Always |
| `session.user.accessToken`                 | string  | Access token of the user account for a specific service. The access token for the user account connected with the current user is delivered. CEK sends the access token of a user account acquired from the authorization server of a 3rd party service. For more information, see [Linking user account](/CEK/Guides/Link_User_Account.md).| Conditional |
| `version`                                  | string  | Version of message format (CEK version).                          | Always |

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
      "application": {
        "applicationId": "com.yourdomain.extension.pizzabot"
      },
      "user": {
        "userId": "V0qe",
        "accessToken": "XHapQasdfsdfFsdfasdflQQ7"
      },
      "device": {
        "deviceId": "096e6b27-1717-33e9-b0a7-510a48658a9b",
        "display": {
          "size": "l100",
          "orientation": "landscape",
          "dpi": 96,
          "contentLayer": {
            "width": 640,
            "height": 360
          }
        }
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
      "application": {
        "applicationId": "com.yourdomain.extension.pizzabot"
      },
      "user": {
        "userId": "V0qe",
        "accessToken": "XHapQasdfsdfFsdfasdflQQ7"
      },
      "device": {
        "deviceId": "096e6b27-1717-33e9-b0a7-510a48658a9b",
        "display": {
          "size": "l100",
          "orientation": "landscape",
          "dpi": 96,
          "contentLayer": {
            "width": 640,
            "height": 360
          }
        }
      }
    }
  },
  "request": {
    "type": "IntentRequest",
    "intent": {
      "name": "OrderPizza",
      "slots": {
        "pizzaType": {
          "name": "pizzaType",
          "value": "Pepperoni"
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
      "application": {
        "applicationId": "com.yourdomain.extension.pizzabot"
      },
      "user": {
        "userId": "V0qe",
        "accessToken": "XHapQasdfsdfFsdfasdflQQ7"
      },
      "device": {
        "deviceId": "096e6b27-1717-33e9-b0a7-510a48658a9b",
        "display": {
          "size": "l100",
          "orientation": "landscape",
          "dpi": 96,
          "contentLayer": {
            "width": 640,
            "height": 360
          }
        }
      }
    }
  },
  "request": {
    "type": "SessionEndedRequest"
  }
}
```
{% endraw %}

#### See also
* [Handling a custom extension request](/CEK/Guides/Build_Custom_Extension.md#HandleCustomExtensionRequest)
* [AudioStreamInfoObject](/CIC/References/CICInterface/AudioPlayer.md#AudioStreamInfoObject)

### Request Type {#CustomExtRequestType}
Request messages are classified into the following three types, and the field configuration of the request message `request` object varies for each request type.
* [`LaunchRequest`](#CustomExtLaunchRequest)
* [`IntentRequest`](#CustomExtIntentRequest)
* [`SessionEndedRequest`](#CustomExtSessionEndedRequest)

#### LaunchRequest {#CustomExtLaunchRequest}
`LaunchRequest` type is a request type that indicates that a user has started using a specific extension. For example, the user has declared to access a specific mode by saying “Let's start talking in English." This type of message is mainly sent to extensions providing services that must enter a specific mode to receive a service.

The `request` object field configuration of the `LaunchRequest` type message is as follows:

{% raw %}
```json
{
  "type": "LaunchRequest"
}
```
{% endraw %}

| Field       | Data Type    | Description                     | Included |
|---------------|---------|-----------------------------|:---------:|
| `type`          | string  | The type of request message. The value is always set to `"LaunchRequest"`. | Always |

Below is an example of a LaunchRequest type request message.

#### IntentRequest {#CustomExtIntentRequest}
`IntentRequest` type is a request type that delivers a user request in order to have its details executed. When developing the service, the extension developer must [define an interaction model](/Design/Design_Guideline_For_Extension.md#DefineInteractionModel) for how to receive a user request, and the interaction model can be registered via the [Clova developer console](/DevConsole/ClovaDevConsole_Overview.md). At this time, the distinguished user request is defined as information type called an “intent.” The analyzed utterance information of the user is converted to an intent and gets delivered to the extension via the `intent` field.

The `request` object field configuration of the `IntentRequest` type message is as follows:

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

| Field       | Data Type    | Description                     | Included |
|---------------|---------|-----------------------------|:---------:|
| `type`          | string  | The type of request message. The value is always set to `"IntentRequest"`.                                                                              | Always |
| `intent`        | object  | Object that stores the analyzed details of a user request [intent](/Design/Design_Guideline_For_Extension.md#Intent).                          | Always |
| `intent.name`   | string  | The name of Intent. The [intent](/Design/Design_Guideline_For_Extension.md#Intent) defined in the interaction model can be identified with this field.  | Always |
| `intent.slots`  | object  | The object that stores the information required when the extension handles the intent (slot). Configuration of this field may vary depending on the [intent](/Design/Design_Guideline_For_Extension.md#Intent) entered in `intent.name` field. | Always |


#### SessionEndedRequest {#CustomExtSessionEndedRequest}
`SessionEndedRequest` type is a request type that indicates that a user has finished using a specific extension. This message will be received in the following situations:
* When the user has requested to exit extension
* When there is no user input for a specific period of time (Timeout)
* When an error has occurred

<div class="note">
  <p><strong>Note!</strong></p>
  <p>If the extension first declares the end of the session using the <code>shouldEndSession</code> field of <a href="#CustomExtResponseMessage">response message</a>, this message will not be received.</p>
</div>


The `request` object field configuration of the `SessionEndedRequest` type message is as follows:

{% raw %}
```json
{
  "type": "SessionEndedRequest"
}
```
{% endraw %}

| Field       | Data Type    | Description                     | Included |
|---------------|---------|-----------------------------|:---------:|
| `type`          | string  | The type of request message. The value is always set to `"SessionEndedRequest"`. | Always |

### Response message {#CustomExtResponseMessage}
The extension must deliver a response messages after handling the request messages (HTTPS Response). This section explains the structure and the fields of the response message.

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
      "values": {{SpeechInfoObject|SpeechInfoObject array}},
      "brief": {{SpeechInfoObject}},
      "verbose": {
        "type": {{string}},
        "values": {{SpeechInfoObject|SpeechInfoObject array}},
      }
    },
    "reprompt": {
      "outputSpeech": {
        "type": {{string}},
        "values": {{SpeechInfoObject|SpeechInfoObject array}},
        "brief": {{SpeechInfoObject}},
        "verbose": {
          "type": {{string}},
          "values": {{SpeechInfoObject|SpeechInfoObject array}},
        }
      }
    },
    "shouldEndSession": {{boolean}},
  },
  "sessionAttibutes": {{object}},
  "version": {{string}}
}
```
{% endraw %}

#### Message fields
| Field       | Data Type    | Description                     | Required |
|---------------|---------|-----------------------------|:---------:|
| `response`                               | object       | The object containing the response information of the extension.                            | Required |
| `response.card`                          | object       | The data is in the [content template](/CIC/References/Content_Templates.md) format and can be displayed on the client screen via this field. If data exists in this field, CIC sends the [Clova.RenderTemplate](/CIC/References/CICInterface/Clova.md#RenderTemplate) directive message to the client. If the object is empty, CIC delivers the [Clova.RenderText](/CIC/References/CICInterface/Clova.md#RenderText) directive message to the client to display the values in the `response.outputSpeech.values` field.        | Required |
| `response.directives[]`                  | object array | The directive message that the extension delivers to CEK. The directive message API for the `response.directives` field will be provided in the future. | Required |
| `response.directives[].header`           | object       | Header of the directive message.                                          | Required |
| `response.directives[].header.messageId` | string       | The message ID (UUID). It is an identifier used to distinguish individual messages.   | Required |
| `response.directives[].header.name`      | string       | The API name of directive message.                                      | Required |
| `response.directives[].header.namespace` | string       | The API namespace of the directive message.                                | Required |
| `response.directives[].payload`          | object       | The object that contains information related to the directive message. You can configure the payload object and the field values differently based on the directive message.         | Required |
| `response.outputSpeech`                  | object       | The object that contains the information to be synthesized as a voice. The synthesized voice information is delivered to the client via CIC.              | Required |
| `response.outputSpeech.brief`            | [SpeechInfoObject](#CustomExtSpeechInfoObject) | Summary information for voice output.                    | Optional |
| `response.outputSpeech.type`             | string       | The type of voice information to output. <ul><li><code>"SimpleSpeech"</code>: Voice information in a simple sentence format. This is the most basic type, and the <code>response.outputSpeech.values</code> field must have a <a href="#CustomExtSpeechInfoObject"><code>SpeechInfoObject</code></a> object if this value is designated.</li><li><code>"SpeechList"</code>: Voice information with a complex sentence type. This is used when outputting many sentences. If this value is designated, the <code>response.outputSpeech.values</code> field must have <a href="#CustomExtSpeechInfoObject"><code>SpeechInfoObject</code></a> object array.</li><li><code>"SpeechSet"</code>: Voice information in a combined format. This is used to deliver the summary of the voice information and detailed voice information to a screenless client device. If this value is designated, it must have the <code>response.outputSpeech.brief</code> and <code>response.outputSpeech.verbose</code> fields instead of the <code>response.outputSpeech.values</code> field.</li></ul> | Required |
| `response.outputSpeech.values[]`           | [SpeechInfoObject](#CustomExtSpeechInfoObject) or [SpeechInfoObject](#CustomExtSpeechInfoObject) array | The object or object array that contains the voice information to output from the client device. | Optional |
| `response.outputSpeech.verbose`          | object       | It is used when delivering content to a screenless client device and contains detailed voice information. | Optional |
| `response.outputSpeech.verbose.type`     | string       | The type of voice information to output. Only the voice information in simple and complex sentence formats can be entered. <ul><li><code>"SimpleSpeech"</code>: Voice information in a simple sentence format. Used when delivering the most basic voice information. If this value is designated, the <code>response.outputSpeech.verbose.values</code> field must have <a href="#CustomExtSpeechInfoObject"><code>SpeechInfoObject</code></a> object.</li><li><code>"SpeechList"</code>: Voice information in a complex sentence format. It is used when outputting many sentences. If this value is designated, the <code>response.outputSpeech.verbose.values</code> field must have <a href="#CustomExtSpeechInfoObject"><code>SpeechInfoObject</code></a> object array.</li></ul> | Required |
| `response.outputSpeech.verbose.values[]`           | [SpeechInfoObject](#CustomExtSpeechInfoObject) or [SpeechInfoObject](#CustomExtSpeechInfoObject) array | The object or object array that contains the detailed voice information to output from the client device. | Required |
| `response.reprompt`                               | object       | The object that contains voice information to encourage additional user utterances. If the `response.reprompt` field is used, the intention to continue multi-turn dialog can be asked to the user or the user can be encouraged to enter additionalmandatory information. Generally, if there is no additional utterance from the user during a multi-turn dialog, the multi-turn dialog exits automatically after the waiting time for input is exceeded. But if the `response.reprompt` field is used, the Clova outputs the voice written in the `response.reprompt` field after the client exceeds the waiting time for input to deliver the [`SpeechSynthesizer.Speak`](/CIC/References/CICInterface/SpeechSynthesizer.md#Speak) directive message and the [`SpeechRecognizer.ExpectSpeech`](/CIC/References/CICInterface/SpeechRecognizer.md#ExpectSpeech) directive message to the client to receive additional utterances of the user.<div class="note"><p><strong>Note!</strong></p><p><code>response.reprompt</code> The field is valid when the <code>response.shouldEndSession</code> field value is entered as <code>false</code>. It is recommended to send voice information in a short sentence format (<code>"SimpleSpeech"</code>). If the <code>response.reprompt</code> field is used, the input waiting time can be extended only once.</p></div> | Optional |
| `response.reprompt.outputSpeech`                  | object       | The object that contains the information to be synthesized as a voice. The synthesized voice information is delivered to the client via CIC.              | Required |
| `response.reprompt.outputSpeech.brief`            | [SpeechInfoObject](#CustomExtSpeechInfoObject) | Summary information for voice output.                    | Optional |
| `response.reprompt.outputSpeech.type`             | string       | The type of voice information to output. <ul><li>"SimpleSpeech": Voice information in a simple sentence format. This is the most basic type, and the <code>response.outputSpeech.values</code> field must have a <a href="#CustomExtSpeechInfoObject"><code>SpeechInfoObject</code></a> object if this value is designated.</li><li><code>"SpeechList"</code>: Voice information with a complex sentence type. This is used when outputting many sentences. If this value is designated, the <code>response.outputSpeech.values</code> field must have <a href="#CustomExtSpeechInfoObject"><code>SpeechInfoObject</code></a> object array.</li><li><code>"SpeechSet"</code>: Voice information in a combined format. This is used to deliver the summary of the voice information and detailed voice information to a screenless client device. If this value is designated, it must have the <code>response.outputSpeech.brief</code> and <code>response.outputSpeech.verbose</code> fields instead of the <code>response.outputSpeech.values</code> field.</li></ul> | Required |
| `response.reprompt.outputSpeech.values[]`           | [SpeechInfoObject](#CustomExtSpeechInfoObject) or [SpeechInfoObject](#CustomExtSpeechInfoObject) array | The object or object array that contains the voice information to output from the client device. | Optional |
| `response.reprompt.outputSpeech.verbose`          | object       | It is used when delivering content to a screenless client device and contains detailed voice information. | Optional |
| `response.reprompt.outputSpeech.verbose.type`     | string       | The type of voice information to output. Only the voice information in simple and complex sentence formats can be entered. <ul><li><code>"SimpleSpeech"</code>: Voice information in a simple sentence format. Used when delivering the most basic voice information. If this value is designated, the <code>response.outputSpeech.verbose.values</code> field must have <a href="#CustomExtSpeechInfoObject"><code>SpeechInfoObject</code></a> object.</li><li><code>"SpeechList"</code>: Voice information in a complex sentence format. It is used when outputting many sentences. If this value is designated, the <code>response.outputSpeech.verbose.values</code> field must have <a href="#CustomExtSpeechInfoObject"><code>SpeechInfoObject</code></a> object array.</li></ul> | Required |
| `response.reprompt.outputSpeech.verbose.values[]`           | [SpeechInfoObject](#CustomExtSpeechInfoObject) or [SpeechInfoObject](#CustomExtSpeechInfoObject) array | The object or object array that contains the detailed voice information to output from the client device. | Required |
| `response.shouldEndSession`              | boolean      | Session end flag A field that indicates that a user has finished using a specific extension. Used when the extension notifies the end of use first before receiving the request message of [`SessionEndedRequest`](#CustomExtSessionEndedRequest) type.<ul><li>true: End of use</li><li>false: Continue use A multi-turn dialog with the user is attempted.</li></ul> | Required |
| `sessionAttributes`                      | object       | The object to store information necessary for a multi-turn dialog with the user. A custom extension sends intermediate information to CEK using the `sessionAttributes` field and receives the corresponding information to the `session.sessionAttributes` field of the [request message](#CustomExtRequestMessage) when receiving additional user requests. `sessionAttributes` The object must be configured as a key-value pair and can be defined arbitrarily when implementing the custom extension. If there is no value to store, enter an empty object. | Required |
| `version`                                | string       | Version of message format (CEK version).                        | Required |

<div class="note">
  <p><strong>Note!</strong></p>
  <p>A prior arrangement is necessary in case of having to send an arbitrary directive message of the extension through the <code>response.directives</code> field. Contact the partnership team for consultation.</p>
</div>

#### SpeechInfoObject {#CustomExtSpeechInfoObject}
SpeechInfoObject is reused in the `response.outputSpeech` of response message. It is the simple utterance information in the smallest unit of voice information to be output to the user. This object has the following fields:

| Field        | Data Type         | Description                                                                | Required |
|----------------|--------------|--------------------------------------------------------------------|:-----:|
| `lang`           | string       | Code of the language to use for voice synthesis. The current values are as follows:<ul><li><code>"en"</code>: English</li><li><code>"ja"</code>: Japanese</li><li><code>"ko"</code>: Korean</li><li><code>""</code>: If the <code>type</code> field value is <code>"URL"</code>, this field has an empty string.</li></ul>         | Required |
| `type`           | string       | Type of voice to use. The type of `value` field value varies depending on the value of this field. The current values are as follows:<ul><li><code>"PlainText"</code>: regular text</li><li><code>"URL"</code>: URI of the file that can play voice and music.</li></ul>            | Required |
| `value`          | string       | Content to synthesize voice or URI of audio file.                                    | Required |

#### Message example
{% raw %}
```json
// Example 1: Return SimpleSpeech voice information - regular text
{
  "version": "0.1.0",
  "sessionAttributes": {},
  "response": {
    "outputSpeech": {
      "type": "SimpleSpeech",
      "values": {
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

// Example 2: Return SpeechList voice information - use regular text, URL type
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
          "value": “I will sing a song."
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

// Example 3: Return SpeechSet voice information - summary, detailed voice information
{
  "version": "0.1.0",
  "sessionAttributes": {},
  "response": {
    "outputSpeech": {
      "type": "SpeechSet",
      "brief": {
        "type": "PlainText",
        "lang": "ko",
        "value": "Here is the weather forecast."
      },
      "verbose": {
        "type": "SpeechList",
        "values": [
          {
              "type": "PlainText",
              "lang": "ko",
              "value": "Monsoon rains throughout the country until the weekend…The heat wave has died down."
          },
          {
              "type": "PlainText",
              "lang": "ko",
              "value": "Monsoon rains throughout the country tomorrow…Watch out for torrential rain in various regions."
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

// Example 4: Stores intermediate information in multi-turn dialog - use of sessionAttributes
{
  "version": "0.1.0",
  "sessionAttributes": {
    "RequestedIntent": "OrderPizza",
    "pizzaType": "Pepperoni pizza"
  },
  "response": {
    "outputSpeech": {
      "type": "SimpleSpeech",
      "values": {
          "type": "PlainText",
          "lang": "ko",
          "value": "How many boxes of pizza do you want to order?"
      }
    },
    "card": {},
    "directives": [],
    "shouldEndSession": false
  }
}

// Example 5: Encourages additional user utterances in multi-turn dialog - use of reprompt
{
  "version": "0.1.0",
  "sessionAttributes": {
    "RequestedIntent": "OrderPizza",
    "pizzaType": "Pepperoni pizza"
  },
  "response": {
    "outputSpeech": {
      "type": "SimpleSpeech",
      "values": {
          "type": "PlainText",
          "lang": "ko",
          "value": "How many boxes of pizza do you want to order?"
      }
    },
    "card": {},
    "reprompt" : {
      "outputSpeech" : {
        "type" : "SimpleSpeech",
        "values" : {
          "type" : "PlainText",
          "lang" : "ko",
          "value" : "If you have nothing to say, would you like to cancel the order?"
        }
      }
    },
    "shouldEndSession": false
  }
}
```
{% endraw %}

#### See also
* [Returning a custom extension response](/CEK/Guides/Build_Custom_Extension.md#ReturnCustomExtensionResponse)
* [Content template](/CIC/References/Content_Templates.md)

