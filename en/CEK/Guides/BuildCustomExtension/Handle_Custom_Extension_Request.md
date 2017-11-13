## Handling custom extension request {#HandleCustomExtensionRequest}
Custom extensions receive user requests by receiving [custom extension messages](/CEK/References/CEK_API.md#CustomExtMessage) from CEK (HTTPS request). Custom extensions handle requests and responses as follows.

![](/CEK/Resources/Images/CEK_Custom_Extension_Sequence_Diagram.png)

A user request can be a one-time request but it can also be a multi-turn request that has to maintain context. The Freetalk mode is one such example.

![](/CEK/Resources/Images/CEK_Custom_Extension_Multi-turn_Sequence_Diagram.png)

A user request can be one of the following three types. Implement your custom extension to perform appropriate actions depending on the message type.

* [When receiving LaunchRequest](#HandleLaunchRequest)
* [When receiving IntentRequest](#HandleIntentRequest)
* [When receiving SessionEndedRequest](#HandleSessionEndedRequest)

### Handling LaunchRequest {#HandleLaunchRequest}
[`LaunchRequest`](/CEK/References/CEK_API.md#CustomExtLaunchRequest) notifies that a user has requested to start a certain mode or custom extension. For example, when a user gives a command such as "Let's talk in English", the client starts the Freetalk mode and CEK sends `LaunchRequest` to an extension that provides English conversation service.

When the message type is LaunchRequest, the `request.type` field is set to `"LaunchRequest"` and `request` field does not contain analysis details of the user's speech. When your extension receives this message, make the necessary preparations or return a [response message](#ReturnCustomExtensionResponse) to the user to notify that the requested service is ready.

After receiving this message and before receiving a [`SessionEndedRequest`](#HandleSessionEndedRequest) message, you will be receiving [`IntentRequest`](#HandleIntentRequest) messages that have the same `session.sessionId` as the previous message.

This is an example of a `LaunchReqeust` type message.

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

```

{% endraw %}

Each field in this example indicates the following.

* `version`: The message format version of the current custom extension is v0.1.0.
* `session`: **This is a new session**. It contains the session ID and user details (ID, accessToken) for the new session.
* `context`: This provides details of the client device. It contains the device ID and details of the default device user.
* `request`: The request type is `LaunchRequest`. It notifies that the current extension has started. It does not contain analysis details of the user's speech input.

### Handling IntentRequest {#HandleIntentRequest}
[`IntentRequest`](/CEK/References/CEK_API.md#CustomExtIntentRequest) receives request messages from CEK as specified by the pre-defined [interaction model](#InteractionModel). You can use `IntentRequest` for both one-time request and multi-turn request.

When the message type is IntentRequest, `request.type` field is set to `"IntentRequest"`. You can check the name of the intent and analysis details of the user's speech input from the `request.intent` field. Analyze the field, process the user request, and return a [response message](#ReturnCustomExtensionResponse).

This is an example of an `IntentRequest` type message.

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

```

{% endraw %}

Each field in this example indicates the following.

* `version`: The message format version of the current custom extension is v0.1.0.
* `session`: **The request is from a previous session**. It contains the previous session ID and user details (ID, accessToken).
* `context`: This provides details of the client device. It contains the device ID and details of the default device user.
* `request`: The request type is `IntentRequest`. It has called an `intent` named `"FreeTalk"`. The `intent` has a `slot` named `"q"` and the `slot` has a value of `"How are you"`.

<div class="note">
  <p><strong>Note!</strong></p>
  <p>The <code>IntentRequest</code> type can start a new session to process a request, regardless of <code>LaunchRequest</code>.</p>
</div>

### Handling SessionEndedRequest {#HandleSessionEndedRequest}

[`SessionEndedRequest`](/CEK/References/CEK_API.md#CustomExtSessionEndedRequest) notifies that a user has requested to end a certain mode or custom extension. When your user gives a command such as "See you later", the client stops the Freetalk mode and CEK sends `SessionEndedRequest` to the extension that provides the conversation service.

When the message type is `SessionEndedReqeust`, the `request.type` field is set to `"EndRequest"`. Same as the `LaunchRequest` type, the `request` field does not contain analysis details of the user's speech. When you receive this message, end the service and return a [response message](#ReturnCustomExtensionResponse) to notify that the service has ended.

This is an example of a `SessionEndedRequest` type message.


{% raw %}

```json

{
  "version": "0.1.0",
  "session": {
    "new": false,
    "sessionAttributes": {}
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

Each field in this example indicates the following.

* `version`: The message format version of the current custom extension is v0.1.0.
* `session`: **The request is from a previous session**. It contains the previous session ID and user details (ID, accessToken).
* `context`: This provides details of the client device. It contains the device ID and details of the default device user.
* `request`: The request type is `SessionEndedRequest`. It notifies that the current extension has ended. It does not contain analysis details of the user's speech input.
