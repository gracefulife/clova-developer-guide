## Handling custom extension request {#HandleCustomExtensionRequest}
A custom extension receives a user request in a [custom extension message](/CEK/References/Custom_Extension_Message_Format.md) sent from CEK (HTTPS request). Typically, a custom extension handles requests and responses as follows.

![](/CEK/Resources/Images/CEK_Custom_Extension_Sequence_Diagram.png)

A user request can be a one-time request but it can also be a multi-turn request that prompts subsequent requests in the consistent context. The Freetalk mode is one such example.

![](/CEK/Resources/Images/CEK_Custom_Extension_Multi-turn_Sequence_Diagram.png)

A user request can be one of the following three types. Implement your custom extension to perform appropriate actions depending on which type the message is.

* [When receiving LaunchRequest](#HandleLaunchRequest)
* [When receiving IntentRequest](#HandleIntentRequest)
* [When receiving SessionEndedRequest](#HandleSessionEndedRequest)

### Handling LaunchRequest {#HandleLaunchRequest}
 [LaunchRequest](/CEK/References/Custom_Extension_Message_Format.md#LaunchRequest) is used to notify that a user has requested to start a particular mode or extension. For example, when a user gives a command such as "Let's have a conversation in English", the client starts the Freetalk mode and CEK sends *LaunchRequest* to the extension that provides English conversation service.

When the message type is LaunchRequest, the *request.type* field is set to "LaunchRequest" and the *request* field does not contain analysis details of the user's speech request input. When you receive this message, make the necessary preparations or return a [response message](#ReturnCustomExtensionResponse) to the user to notify that the requested service is ready.

After receiving this message and before receiving a [SessionEndedRequest](#HandleSessionEndedRequest) message, you will be receiving an [IntentRequest](#HandleIntentRequest) message that has the same *session.sessionId* value as the previous message.

This is an example of a *LaunchReqeust* type message.

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

* *version*: The message format version of current custom extension is v0.1.0.
* *session*: Indicates a **new session**. It contains new session ID and user details (ID, accessToken).
* *context*: Contains information of the client device, with device ID and details of default device user.
* *request*: Request type is *LaunchRequest*. It notifies that the current extension has started. It does not contain analysis details of the user's speech input.

### Handling IntentRequest {#HandleIntentRequest}
 [IntentRequest](/CEK/References/Custom_Extension_Message_Format.md#IntentRequest) is used to receive a request message from CEK as specified by the pre-defined [interaction model](#InteractionModel). You can use *IntentRequest* for both one-time request and multi-turn request.

When the message type is IntentRequest, the *request.type* field is set to "IntentRequest". The *request.intent* field contains the name of intent invoked and analysis details of the user's speech input. You can analyze the field, process the user request, and return a [response message](#ReturnCustomExtensionResponse).

This is an example of a *IntentRequest* type message.

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

* *version*: The message format version of current custom extension is v0.1.0.
* *session*: Indicates that **the user request has continued from the previous session**. It contains previous session ID and user details (ID, accessToken).
* *context*: Contains information of the client device, with device ID and details of default device user.
* *request*: Request type is *IntentRequest*. It has called an *intent* named "FreeTalk". The *intent* has *slot* named "q" with the value, "How are you".

<div class="note">
  
<p><strong>Note!</strong></p>  <p>The <em>IntentRequest</em> type can start a new session to process a new request, regardless of <em>LaunchRequest</em> type.</p>
</div>

### Handling SessionEndedRequest {#HandleSessionEndedRequest}

[SessionEndedRequest](/CEK/References/Custom_Extension_Message_Format.md#SessionEndedRequest) is used to notify that a user has requested to end a particular mode or extension. When a user gives a command such as "See you later", the client stops the Freetalk mode and CEK sends *SessionEndedRequest* to the extension that provides English conversation service.

When the message type is *SessionEndedReqeust*, the *request.type* field is set to "EndRequest". Same as the *LaunchRequest* type, the *request* field does not contain analysis details of the user's speech input. When you receive this message, end the service and return a [response message](#ReturnCustomExtensionResponse) to notify that the service has ended.

This is an example of a *SessionEndedRequest* type message.


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

* *version*: The message format version of current custom extension is v0.1.0.
* *session*: Indicates that **the user request has continued from the previous session**. It contains previous session ID and user details (ID, accessToken).
* *context*: Contains information of the client device, with device ID and details of default device user.
* *request*: Request type is *SessionEndedRequest*. It notifies that the current extension has ended. It does not contain analysis details of the user's speech request input.
