## Handling a custom extension request {#HandleCustomExtensionRequest}
The custom extension receives user requests with the format of [custom extension messages](/CEK/References/CEK_API.md#CustomExtMessage) from CEK (HTTPS request). The customer extension must typically handle and respond as shown below.

![](/CEK/Resources/Images/CEK_Custom_Extension_Sequence_Diagram.png)

A user request, like in this example, may be a single-turn dialogue, but it can also be a multi-turn dialogue that needs to maintain the context of a conversation.

![](/CEK/Resources/Images/CEK_Custom_Extension_Multi-turn_Sequence_Diagram.png)

User requests for multi-turn dialogs are classified into three types. A custom extension developer must design the code to handle jobs corresponding to the message.
The three types of requests and the user utterance patterns for each request type are as follows:

| Request type | User utterance pattern | Sample utterance |
|---------|--------------|---------|
|[LaunchRequest](#HandleLaunchRequest) | _[extension invocation name]_ + "start/open/operate" | "Start Pizzabot" |
| [IntentRequest](#HandleIntentRequest) | _[execution commands registered per extension]_ + "to/from/by/with" + _[extension invocation name]_, or <br/>(after receiving the `LaunchRequest` type request) _[execution commands registered per extension]_ | "Order a pizza from Pizzabot" <br/> (In the state of starting the Pizzabot) "Update me on the delivery status" |
| [SessionEndedRequest](#HandleSessionEndedRequest) | (In the state of receiving the `LaunchRequest` type request) "Exit/close/stop" | "Exit (Pizzabot)" |

### Handling a LaunchRequest {#HandleLaunchRequest}
[`LaunchRequest` type](/CEK/References/CEK_API.md#CustomExtLaunchRequest) request is used to declare that the user has requested to use a specific extension. For example, when the user makes a command, such as "Start Pizzabot" or "Open Pizzabot," CEK sends a `LaunchRequest` type request to the extension providing the pizza delivery service. Once the request is received, the extension must prepare to receive the next request of the user.

In the LaunchRequest type message, the `request.type` field has a `"LaunchRequest"` value and the `request` field does not contain the analyzed information of the user utterance. The extension developer should develop the code so that the extension handles preparations for the service at the receipt of this message type or sends a [response message](#ReturnCustomExtensionResponse) to the user that the preparations for the services are complete.

After receiving this message until receiving the [`SessionEndedRequest` type](#HandleSessionEndedRequest) request message, the extension will receive [`IntentRequest` type](#HandleIntentRequest) messages. The `session.sessionId` field will remain the same as the previous message.

Below is an example of a `LaunchRequest` type request message.

{% raw %}
```json
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
```
{% endraw %}

The fields used in the example above represent the following information:

* `version`: The current version of the custom extension message format is v0.1.0.
* `session`: As a **new session**, this contains the session ID to use for new sessions and user information (ID, accessToken).
* `context`: Information on the client device containing device ID and basic user information.
* `request`: As a `LaunchRequest` type request, it notifies of the start of using the extension. It does not contain the analysis of the user utterance.

### Handling an IntentRequest {#HandleIntentRequest}

[`IntentRequest` type](/CEK/References/CEK_API.md#CustomExtIntentRequest) of request is used by the CEK to send user requests to the extension based on the predefined [interaction model](/Design/Design_Guideline_For_Extension.md#DefineInteractionModel). `IntentRequest` is sent to the extension when the user makes a command by specifying the extension invocation name or when the user makes a command without specifying the extension invocation name after the `LaunchRequest` is generated. For example, if the user says "Order a pizza from Pizzabot" or starts the service with another command and then says a command, like "Order pizza", CEK sends a `IntentRequest` type request to the extension providing the pizza delivery service. `IntentRequest` type request is also used when handling multi-turn dialogue requests as well as single-turn requests.

In the IntentRequest type message, the `request.type` field has a `"IntentRequest"` value. You can find the name of the called intent and the analysis of utterance information in the `request.intent` field. After handling the user request by analyzing this field, you can send the [response message](#ReturnCustomExtensionResponse).

Below is an example of a `IntentRequest` type request message.

{% raw %}
```json
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
```
{% endraw %}

The fields used in the example above represent the following information:

* `version`: The current version of the custom extension message format is v0.1.0.
* `session`: As a **user request continued on the existing session**, this contains the ID of the existing session and user information (ID, accessToken).
* `context`: Information on the client device containing device ID and basic user information.
* `request`: As an `IntentRequest` type request, the [intent](/Design/Design_Guideline_For_Extension.md#Intent) registered with the name `"OrderPizza"` has been called. The `"pizzaType"` [slot](/Design/Design_Guideline_For_Extension.md#Slot) is sent together with the intent, as the required information, and holds the value called `"Pepperoni"`.

<div class="note">
  <p><strong>Note!</strong></p>
  <p><code>IntentRequest</code> type request can handle requests by starting a new session regardless of the <code>LaunchRequest</code> type request.</p>
</div>

### Handling a SessionEndedRequest {#HandleSessionEndedRequest}

[`SessionEndedRequest` type request](/CEK/References/CEK_API.md#CustomExtSessionEndedRequest) is used to declare that the user has requested to stop using a specific mode or customer extension. When the user makes a command like "Exit" or "Stop," the client stops using the extension and CEK sends a `SessionEndedRequest` type request to the extension providing the dialogue service.

In the `SessionEndedRequest` type message, the `request.type` field has a `"SessionEndedRequest"` value and the `request` field does not contain the analyzed details of user utterance, like the `LaunchRequest` type. The extension developer can write the code used to exit the service.

Below is an example of a `SessionEndedRequest` type request message.


{% raw %}
```json
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

The fields used in the example above represent the following information:

* `version`: The current version of the custom extension message format is v0.1.0.
* `session`: As a **user request continued on the existing session**, this contains the ID of the existing session and user information (ID, accessToken).
* `context`: Information on the client device containing device ID and basic user information.
* `request`: As a `SessionEndedRequest` type request, it notifies of the end of using the extension. It does not contain the analysis of the user utterance.

<div class="danger">
  <p><strong>Caution!</strong></p>
  <p>Once CEK sends the <code>SessionEndedRequest</code> type request to the extension, CEK will ignore all responses by the extension.</p>
</div>
