## Custom extension 요청 처리하기 {#HandleCustomExtensionRequest}
Custom extension은 CEK로부터 [custom extension 메시지](/CEK/References/CEK_API.md#CustomExtMessage) 형태의 사용자 요청을 수신합니다(HTTPS Request). Custom extension은 일반적으로 다음과 같이 요청을 처리하고 응답해야 합니다.

![](/CEK/Resources/Images/CEK_Custom_Extension_Sequence_Diagram.png)

이런 사용자의 요청은 단번에 끝나는 요청일 수도 있지만 대화 모드(Freetalk mode)와 같이 계속 맥락이 유지되어야 하는 multi-turn 대화일 수도 있습니다.

![](/CEK/Resources/Images/CEK_Custom_Extension_Multi-turn_Sequence_Diagram.png)

이를 위해 사용자의 요청을 다음과 같이 세 가지 타입의 요청으로 구분하고 있습니다. Custom extension 개발자는 각 메시지에 따라 그에 상응하는 작업을 처리해야 합니다.

* [LaunchRequest 요청을 받은 경우](#HandleLaunchRequest)
* [IntentRequest 요청을 받은 경우](#HandleIntentRequest)
* [SessionEndedRequest 요청을 받은 경우](#HandleSessionEndedRequest)

### LaunchRequest 요청 처리 {#HandleLaunchRequest}
[`LaunchRequest` 타입 요청](/CEK/References/CEK_API.md#CustomExtLaunchRequest)은 사용자가 특정 모드나 특정 custom extension을 사용하기로 선언한 것을 알릴 때 사용됩니다. 예를 들면, "영어 대화하자"와 같은 명령을 사용자가 내린 경우 클라이언트는 대화 모드(Freetalk mode)를 수행하며, CEK는 영어 대화 서비스를 제공하는 extension에게 `LaunchRequest` 타입 요청을 전달합니다.

LaunchRequest 타입 메시지는 `request.type` 필드에 `"LaunchRequest"`라는 값을 가지며 `request` 필드에 사용자의 발화가 분석된 정보를 포함하고 있지 않습니다. Extension 개발자는 이 메시지를 받은 경우 사전 준비 사항을 처리하거나 사용자에게 서비스를 제공할 준비가 되었다는 [응답 메시지](#ReturnCustomExtensionResponse)를 보내면 됩니다.

이 메시지를 받은 후부터 [`SessionEndedRequest` 타입](#HandleSessionEndedRequest) 요청 메시지를 받기 전까지 [`IntentRequest` 타입](#HandleIntentRequest)의 요청 메시지를 받게 되며, `session.sessionId` 필드는 이전 메시지와 같은 값을 가지게 됩니다.

다음은 `LaunchReqeust` 타입의 요청 메시지 예입니다.

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

위 예제에서 각 필드의 의미는 다음과 같습니다.

* `version` : 현재 사용하는 custom extension 메시지 포맷의 버전이 v0.1.0입니다.
* `session` : **새로운 세션이며**, 새로운 세션에 사용될 세션의 ID와 사용자의 정보(ID, accessToken)가 담겨 있습니다.
* `context` : 클라이언트 기기에 대한 정보이며, 기기 ID와 기기의 기본 사용자 정보가 담겨 있습니다.
* `request` : `LaunchRequest` 타입 요청으로 현재 extension의 사용 시작을 알립니다. 사용자의 발화가 분석된 정보는 없습니다.

### IntentRequest 요청 처리 {#HandleIntentRequest}
[`IntentRequest` 타입 요청](/CEK/References/CEK_API.md#CustomExtIntentRequest)은 미리 정의해 둔 [Interaction 모델](#InteractionModel)에 따라 CEK로부터 요청 메시지를 받습니다. `IntentRequest` 타입 요청은 일회적인 요청 뿐만 아니라 연속되는 사용자 요청(Multi-turn request)을 처리할 때 사용됩니다.

IntentRequest 타입 메시지는 `request.type` 필드에 `"IntentRequest"`라는 값을 가집니다. 호출된 intent의 이름과 분석된 사용자의 발화 정보는 `request.intent` 필드를 통해 확인할 수 있습니다. 이 필드를 분석하여 사용자의 요청을 처리한 후 [응답 메시지](#ReturnCustomExtensionResponse)를 보내면 됩니다.

다음은 `IntentRequest` 타입의 요청 메시지 예입니다.

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

위 예제에서 각 필드의 의미는 다음과 같습니다.

* `version` : 현재 사용하는 custom extension 메시지 포맷의 버전이 v0.1.0입니다.
* `session` : **기존 세션에 이어지는 사용자의 요청이며**, 기존 세션의 ID와 사용자의 정보(ID, accessToken)가 담겨 있습니다.
* `context` : 클라이언트 기기에 대한 정보이며, 기기 ID와 기기의 기본 사용자 정보가 담겨 있습니다.
* `request` : `IntentRequest` 타입 요청이며, `"FreeTalk"`라는 이름으로 등록된 `intent`를 호출했습니다. 해당 `intent`의 필요 정보로 `"q"`라는 `slot`이 함께 전달되었고 해당 `slot`은 `"How are you"`라는 값을 가지고 있습니다.

<div class="note">
  <p><strong>Note!</strong></p>
  <p><code>IntentRequest</code> 타입 요청은 <code>LaunchRequest</code> 타입 요청과 상관없이 없이 새로운 세션을 시작하여 요청을 처리할 수 있습니다.</p>
</div>

### SessionEndedRequest 요청 처리 {#HandleSessionEndedRequest}

[`SessionEndedRequest` 타입 요청](/CEK/References/CEK_API.md#CustomExtSessionEndedRequest)은 사용자가 특정 모드나 특정 custom extension의 사용을 중지하기로 선언한 것을 알릴 때 사용됩니다. "See you later"와 같은 명령을 사용자가 내린 경우 클라이언트는 대화 모드(Freetalk mode)를 중지하며, CEK는 대화 서비스를 제공하는 extension에게 `SessionEndedRequest` 타입 요청을 전달합니다.

`SessionEndedReqeust` 타입 메시지는 `request.type` 필드에 `"EndRequest"`라는 값을 가지며 `LaunchRequest` 타입과 마찬가지로 `request` 필드에 사용자의 발화가 분석된 정보를 포함하고 있지 않습니다. Extension 개발자는 이 메시지를 받은 경우 서비스 제공을 종료하고 사용자에게 사용 종료 상황의 인사 정도를 [응답 메시지](#ReturnCustomExtensionResponse)로 보내면 됩니다.

다음은 `SessionEndedRequest` 타입의 요청 메시지 예입니다.


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

위 예제에서 각 필드의 의미는 다음과 같습니다.

* `version` : 현재 사용하는 custom extension 메시지 포맷의 버전이 v0.1.0입니다.
* `session` : **기존 세션에 이어지는 사용자의 요청이며**, 기존 세션의 ID와 사용자의 정보(ID, accessToken)가 담겨 있습니다.
* `context` : 클라이언트 기기에 대한 정보이며, 기기 ID와 기기의 기본 사용자 정보가 담겨 있습니다.
* `request` : `SessionEndedRequest` 타입 요청으로 현재 extension의 사용을 중지했음을 알립니다. 사용자의 발화가 분석된 정보는 없습니다.
