## Handling custom extension request {#HandleCustomExtensionRequest}
Custom extensions receive user requests by receiving [custom extension messages](/CEK/References/Custom_Extension_Message_Format.md) from CEK (HTTPS request). Custom extensions handle requests and responses as follows.

![](/CEK/Resources/Images/CEK_Custom_Extension_Sequence_Diagram.png)

A user request can be a one-time request but it can also be a multi-turn request that has to maintain context. The Freetalk mode is one such example.

![](/CEK/Resources/Images/CEK_Custom_Extension_Multi-turn_Sequence_Diagram.png)

A user request can be one of the following three types. Implement your custom extension to perform appropriate actions depending on which type the message is.

* [When receiving LaunchRequest](#HandleLaunchRequest)
* [When receiving IntentRequest](#HandleIntentRequest)
* [When receiving SessionEndedRequest](#HandleSessionEndedRequest)

### Handling LaunchRequest {#HandleLaunchRequest}
[`LaunchRequest`](/CEK/References/Custom_Extension_Message_Format.md#LaunchRequest) notifies that a user has requested to start a certain mode or custom extension. For example, when a user gives a command such as "Let's talk in English", the client starts the Freetalk mode and CEK sends `LaunchRequest` to the extension that provides English conversation service.

When the message type is LaunchRequest, the `request.type` field is set to **"LaunchRequest"** and the `request` field does not contain analysis details of the user's speech. When you receive this message, make the necessary preparations or return a [response message](#ReturnCustomExtensionResponse) to the user to notify that the requested service is ready.

After receiving this message and before receiving a [`SessionEndedRequest`](#HandleSessionEndedRequest) message, you will be receiving [`IntentRequest`](#HandleIntentRequest) messages that have the `session.sessionId` value same as the previous message.

This is an example of a `LaunchReqeust` type message.

{% raw %}
```json
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
```
{% endraw %}

Each field in this example indicates the following.

* `version`: The message format version of the current custom extension is v0.1.0.
* `session`: **This is a new session**. It contains the session ID and user details (ID, accessToken) for the new session.
* `context`: Details of the client device. It contains the device ID and details of the default device user.
* `request`: The request type is `LaunchRequest`. It notifies that the current extension has started. It does not contain analysis details of the user's speech input.

### Handling IntentRequest {#HandleIntentRequest}
[`IntentRequest`](/CEK/References/Custom_Extension_Message_Format.md#IntentRequest) receives request messages from CEK as specified by pre-defined [interaction ](#InteractionModel). You can use `IntentRequest` for both one-time request and multi-turn request.

When the message type is IntentRequest, the `request.type` field is set to **"IntentRequest"**. You can check the name of the intent and analysis details of the user's speech input from the `request.intent` field. Then, you analyze the field, process the user request, and return a [response message](#ReturnCustomExtensionResponse).

This is an example of a `IntentRequest` type message.

{% raw %}
```json
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
```
{% endraw %}

Each field in this example indicates the following.

* `version`: The message format version of the current custom extension is v0.1.0.
* `session`: **The request is from the previous session**. It contains the previous session ID and user details (ID, accessToken).
* `context`: Information of the client device. It contains the device ID and details of the default device user.
* `request`: The request type is `IntentRequest`. It has called an `intent` named **"FreeTalk"**. The `intent` has a `slot` named **"q"** and the `slot` value is **"How are you"**.

<div class="note">
  <p><strong>Note!</strong></p>
  <p>The <code>IntentRequest</code> type can start a new session to process a request, regardless of <code>LaunchRequest</code>.</p>
</div>

### Handling SessionEndedRequest {#HandleSessionEndedRequest}

[`SessionEndedRequest`](/CEK/References/Custom_Extension_Message_Format.md#SessionEndedRequest) notifies that your user has requested to end a certain mode or custom extension. When your user gives a command such as "See you later", the client stops the Freetalk mode and CEK sends `SessionEndedRequest` to the extension that provides the conversation service.

When the message type is `SessionEndedReqeust`, the `request.type` field is set to **"EndRequest"**. Same as the `LaunchRequest` type, the `request` field does not contain analysis details of the user's speech. When you receive this message, end the service and return a [response message](#ReturnCustomExtensionResponse) to notify that the service has ended.

This is an example of a `SessionEndedRequest` type message.


{% raw %}
```json
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

Each field in this example indicates the following.

* `version`: The message format version of the current custom extension is v0.1.0.
* `session`: **The request is from the previous session**. It contains the previous session ID and user details (ID, accessToken).
* `context`: Details of the client device. It contains the device ID and details of the default device user.
* `request`: The request type is `SessionEndedRequest`. It notifies that the current extension has ended. It does not contain analysis details of the user's speech input.
