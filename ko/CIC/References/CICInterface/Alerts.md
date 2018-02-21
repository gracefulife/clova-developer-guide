# Alerts

Alerts 인터페이스는 클라이언트에서 알람을 등록/수정/제거/시작/중지할 때 사용되는 네임스페이스입니다. 알람의 종류는 다음 표와 같습니다.

| 알람 종류 | 설명                                |
|---------|------------------------------------|
| 액션 타이머(`"ACTIONTIMER"`) | 지정한 시간이 경과한 후 특정 동작을 수행하는 알람                               |
| 알람(`"ALARM"`)            | 지정한 날짜와 시간에 울리는 알람                                            |
| 리마인더(`"REMINDER"`)      | 지정한 날짜와 시간에 사용자가 입력한 내용을 표시하거나 들려주면서 울리는 알람. 예를 들면 사용자가 "내일 7시에 약 먹을 시간이라고 알려줘"라고 하면 "내일 7시"는 알람을 울려야 하는 시간되고 "약 먹을 시간"은 알람을 울리 때 알려줘야 하는 내용이됩니다. 클라이언트는 알람이 울릴 때 사용자에게 알려줘야 하는 내용을 화면에 표시하거나 음성으로 들려줘야 합니다.       |
| 타이머(`"TIMER"`)           | 지정한 시간이 경과한 후 울리는 알람                                         |

사용자는 알람을 음성이나 Clova 앱으로 추가할 수 있고 Clova 앱으로만 알람을 수정 및 삭제할 수 있습니다. Clova는 알람과 관련된 정보를 클라우드 환경에 보관하며, 사용자가 등록한 알람을 CIC를 통해 클라이언트에게 전달합니다. Clova는 반복 알람의 경우 현재 시간에 가장 근접한 알람만 클라이언트에게 전달하며, 해당 알람이 중지될 때 다음 차례의 반복 알람을 클라이언트에게 전달합니다.

따라서 클라이언트는 Alerts 인터페이스를 이용해 다음과 같은 동작을 수행해야 합니다.
* CIC로부터 지시 메시지를 전달받으면 지시 메시지의 내용에 따라 알람을 등록/수정/삭제해야 합니다.
* 알람이 동작해야 하는 시간에 맞춰 알람을 울려줘야 합니다.
* 알람을 생성/수정/삭제/시작/중지한 경우 반드시 이를 CIC로 보고해야 그에 상응하는 결과를 CIC가 클라이언트에게 보내줄 수 있습니다.
* 이벤트 메시지를 보낼 때 반드시 [`Alerts.AlertsState`](/CIC/References/Context_Objects.md#AlertsState) 맥락 객체를 함께 전송하여 클라이언트에 설정된 알람의 상태를 보고해야 합니다.

<div class="note">
  <p><strong>Note!</strong></p>
  <p>알람이 등록/수정/제거/시작/중지되는 구조는 <a href="#AlertsWorkFlow">알람 동작 구조</a>를 참조합니다.</p>
</div>

Alerts가 제공하는 이벤트 메시지와 지시 메시지는 다음과 같습니다.

| 메시지 이름         | 메시지 타입  | 메시지 설명                                   |
|------------------|-----------|---------------------------------------------|
| [`AlertStarted`](#AlertStarted)                 | Event     | 클라이언트가 알람이 시작되었음을 CIC로 보고하기 위해 사용됩니다. |
| [`AlertStopped`](#AlertStopped)                 | Event     | 클라이언트가 알람이 중지되었음을 CIC로 보고하기 위해 사용됩니다. |
| [`DeleteAlert`](#DeleteAlert)                   | Directive | 클라이언트에게 특정 알람을 삭제하도록 지시합니다. |
| [`DeleteAlertFailed`](#DeleteAlertFailed)       | Event     | 클라이언트가 클라이언트에 설정된 특정 알람을 삭제하는데 실패했음을 CIC로 보고하기 위해 사용됩니다. |
| [`DeleteAlertSucceeded`](#DeleteAlertSucceeded) | Event     | 클라이언트가 클라이언트에 설정된 특정 알람을 삭제하는데 성공했음을 CIC로 보고하기 위해 사용됩니다. |
| [`RequestAlertStop`](#RequestAlertStop)         | Event     | 클라이언트가 현재 울리고 있는 알람을 중지하도록 Clova에게 요청할 때 사용됩니다.  |
| [`RequestSynchronizeAlert`](#RequestSynchronizeAlert) | Event | 클라이언트가 Clova의 클라우드 환경에 저장된 사용자의 알람 정보를 동기화해야 할 때 이 이벤트 메시지를 CIC로 전송합니다. |
| [`SetAlert`](#SetAlert)                         | Directive | 클라이언트에게 알람을 새로 추가하거나 특정 알람을 수정하도록 지시합니다. |
| [`SetAlertFailed`](#SetAlertFailed)             | Event     | 클라이언트가 특정 알람을 추가 또는 수정하는데 실패했음을 CIC로 보고하기 위해 사용됩니다. |
| [`SetAlertSucceeded`](#SetAlertSucceeded)       | Event     | 클라이언트가 특정 알람을 추가 또는 수정하는데 성공했음을 CIC로 보고하기 위해 사용됩니다. |
| [`StopAlert`](#StopAlert)                       | Directive | 클라이언트에게 특정 알람을 중지하도록 지시합니다.  |
| [`SynchronizeAlert`](#SynchronizeAlert)         | Directive | 클라이언트에게 `payload` 필드에 있는 사용자의 알람 데이터를 동기화하도록 지시합니다.  |

위 메시지 중 [`RequestSynchronizeAlert`](#RequestSynchronizeAlert) 이벤트 메시지와 [`SynchronizeAlert`](#SynchronizeAlert) 지시 메시지는 Clova와 클라이언트 사이에 알람, 일정과 같이 사용자 계정 관련된 정보를 동기화해야 할 때 사용됩니다. 이런 동기화 작업은 다음과 같은 상황에서 발생할 수 있습니다.

* 사용자 계정을 이용하는 클라이언트 기기가 추가되었을 때
* 클라이언트가 네트워크 접속 장애 등의 이유로 CIC에 다시 연결될 때
* 다른 사용자가 사용을 시작하여 클라이언트 기기에 등록된 사용자 계정이 변경될 때
* 클라이언트 기기가 페어링 앱과 연결이 해제된 후 다시 설정될 때

<div class="note">
  <p><strong>Note!</strong></p>
  <p>네트워크가 끊어지거나 사용자 계정 연결이 해제될 경우 사용자 계정에 등록된 알람 정보를 기기에서 제거해야 합니다.</p>
</div>

## 알람 동작 구조 {#AlertsWorkFlow}

일반적으로 알람의 등록부터 중지되는 순간까지 전체적인 흐름은 다음과 같습니다.

![](/CIC/Resources/Images/CIC_Alerts_Work_Flow.png)

1. 사용자가 알람 등록을 발화로 요청([`SpeechRecognizer.Recognize`](/CIC/References/CICInterface/SpeechRecognizer.md#Recognize))합니다.
2. Clova는 사용자의 발화를 분석하고 사용자의 클라이언트 기기가 알람을 추가할 수 있도록 [`Alerts.SetAlert`](#SetAlert) 지시 메시지를 보냅니다.
3. 클라이언트가 알람 등록을 시도한 후 그 결과를 Clova에게 전달합니다.([`Alerts.SetAlertSucceeded`](#SetAlertSucceeded) 이벤트 메시지, [`Alerts.SetAlertFailed`](#SetAlertFailed) 이벤트 메시지 사용)
4. Clova는 알람이 등록된 결과를 사용자에게 알려주기 위해 [`SpeechSynthesizer.Speak`](/CIC/References/CICInterface/SpeechSynthesizer.md#Speak) 지시 메시지와 [`Clova.RenderTemplate`](/CIC/References/CICInterface/Clova.md#RenderTemplate) 지시 메시지를 클라이언트에게 전달합니다.
5. (지정한 시간이 되면) 클라이언트는 알람을 울려야 하며, 알람이 시작되었음을 [`Alerts.AlertStarted`](#AlertStarted) 이벤트 메시지로 CIC에게 보고해야 합니다. 알람이 시작되면 클라이언트는 CIC로 전송하는 모든 이벤트 메시지에 현재 울리고 있는 알람 정보를 채워 보내야 합니다. 이 때, [`Alert.AlertsState`](/CIC/References/Context_Objects.md#AlertsState) 맥락 정보의 `activeAlerts` 필드를 사용해야 합니다.
6. 사용자는 발화([`SpeechRecognizer.Recognize`](/CIC/References/CICInterface/SpeechRecognizer.md#Recognize))나 물리적 버튼(하드웨어 방식) 또는 GUI 버튼(소프트웨어 방식)으로 알람을 중지하도록 요청([`Alerts.RequestAlertStop`](#RequestAlertStop))할 것입니다.
7. Clova는 클라이언트가 알람을 중지하도록 클라이언트에게 [`Alerts.StopAlert`](#StopAlert) 지시 메시지를 보냅니다.
8. 클라이언트는 알람을 중지한 후 알람이 중지되었음을 [`Alerts.AlertStopped`](#SetAlertSucceeded) 이벤트 메시지로 보고해야 합니다.
9. (액션 타이머 알람인 경우) Clova는 클라이언트에게 사용자가 예약한 동작에 해당하는 지시 메시지를 전달합니다.

<div class="note">
<p><strong>Note!</strong></p>
<p>반복되는 알람의 경우 현재 시간에서 가장 가까운 반복 알람 한 건만 클라이언트에 등록 및 실행하며, 클라이언트에 등록된 반복 알람이 실행 후 중지되면 다음 차례의 반복 알람을 CIC로부터 새로 받게 됩니다. 만약 네트워크가 장시간 연결되지 않는다면 반복 알람은 제대로 동작하지 않을 수 있습니다.</p>
</div>

위의 흐름에서 5번 단계 이전에 알람을 수정하거나 삭제할 수 있으며, 오직 Clova 앱을 통해서 수정 및 삭제할 수 있습니다. 참고로 사용자의 발화에 대한 응답으로 전송되는 지시 메시지가 아니면 해당 지시 메시지는 [downchannel](/CIC/Guides/Interact_with_CIC.md#CreateConnection)을 통해 클라이언트에게 전달됩니다.

알람을 수정하거나 삭제하는 흐름은 다음과 같습니다.

1. 사용자가 Clova 앱에서 알람을 수정하거나 삭제를 시도합니다.
2. Clova는 사용자 요청을 처리하기 위해 [`Alerts.SetAlert`](#SetAlert) 지시 메시지 또는 [`Alerts.DeleteAlert`](#DeleteAlert) 지시 메시지를 클라이언트에게 보냅니다.
3. 클라이언트가 알람을 수정하거나 삭제한 그 결과를 Clova에게 전달합니다. (관련 이벤트 메시지 사용)

사용자의 클라이언트가 추가되거나 일부 또는 특정 클라이언트가 네트워크 연결이 끊긴 후 재접속되는 경우 또는 클라이언트에 등록된 사용자의 계정이 변경되는 경우에는 다음과 같은 절차를 거쳐 서버에 등록된 사용자의 알람 정보를 클라이언트로 가져와서 동기화해야 합니다.

1. 클라이언트는 CIC에 연결 또는 재연결되면 [`System.RequestSynchronizeState`](/CIC/References/CICInterface/System.md#RequestSynchronizeState) 이벤트 메시지를 CIC로 전송해야 합니다.
2. 클라이언트는 CIC로부터 [`System.SynchronizeState`](/CIC/References/CICInterface/System.md#SynchronizeState) 지시 메시지를 수신하게 되며, 이 때 `allAlerts` 필드에 있는 알람 데이터를 기기 알람 정보와 동기화 해야 합니다.

<div class="danger">
<p><strong>Caution!</strong></p>
<p>위와 같은 동작 구조로 인해 클라이언트가 네트워크에 연결되지 않으면 알람과 관련된 모든 동작이 제대로 수행되지 않게 됩니다.</p>
</div>

## AlertStarted event {#AlertStarted}

클라이언트가 알람이 시작되었음을 CIC로 보고하기 위해 사용됩니다. 클라이언트는 알람이 시작되어 울리게 된 경우 반드시 이 이벤트 메시지를 CIC에게 전송해야 합니다.

### Context fields

{% include "/CIC/References/CICInterface/Context_Objects_List.md" %}

### Payload fields

| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|:---------:|
| `token`   | string | 시작된 알람의 식별자                  | 필수 |
| `type`    | string | 알람의 종류. 다음과 같은 값을 가집니다. <ul><li><code>"ACTIONTIMER"</code></li><li><code>"ALARM"</code></li><li><code>"REMINDER"</code></li><li><code>"TIMER"</code></li></ul>  | 필수 |

### Message example
{% raw %}

```json
{
  "context": [
    {{Alerts.AlertsState}},
    {{AudioPlayer.PlayerState}},
    {{Device.DeviceState}},
    {{Device.Display}},
    {{Clova.Location}},
    {{Clova.SavedPlace}},
    {{Speaker.VolumeState}},
    {{SpeechSynthesizer.SpeechState}}
  ],
  "event": {
    "header": {
      "namespace": "Alerts",
      "name": "AlertStarted",
      "messageId": "4e4080d6-c440-498a-bb73-ae86c6312806"
    },
    "payload": {
      "token": "876afa88-8ad5-427b-9878-2edb5b103117",
      "type": "ALARM"
    }
  }
}
```

{% endraw %}

### See also
* [`Alerts.AlertStopped`](#AlertStopped)

## AlertStopped event {#AlertStopped}

클라이언트가 알람이 중지되었음을 CIC로 보고하기 위해 사용됩니다. 클라이언트는 울리던 알람이 중지된 경우 반드시 이 이벤트 메시지를 CIC에게 전송해야 합니다.
* **일반 알람이 중지된 경우** CIC로부터 [`Alerts.DeleteAlert`](#DeleteAlert) 지시 메시지를 받게 됩니다.
* **반복 알람이 중지된 경우** CIC로부터 다음 반복 알람을 설정하기 위해 [`Alerts.SetAlert`](#SetAlert) 지시 메시지를 받게 됩니다.

### Context fields

{% include "/CIC/References/CICInterface/Context_Objects_List.md" %}

### Payload fields

| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|:---------:|
| `token`   | string | 중지된 알람의 식별자                  | 필수 |
| `type`    | string | 알람의 종류. 다음과 같은 값을 가집니다. <ul><li><code>"ACTIONTIMER"</code></li><li><code>"ALARM"</code></li><li><code>"REMINDER"</code></li><li><code>"TIMER"</code></li></ul>  | 필수 |

### Message example
{% raw %}

```json
{
  "context": [
    {{Alerts.AlertsState}},
    {{AudioPlayer.PlayerState}},
    {{Device.DeviceState}},
    {{Device.Display}},
    {{Clova.Location}},
    {{Clova.SavedPlace}},
    {{Speaker.VolumeState}},
    {{SpeechSynthesizer.SpeechState}}
  ],
  "event": {
    "header": {
      "namespace": "Alerts",
      "name": "AlertStopped",
      "messageId": "4e4080d6-c440-498a-bb73-ae86c6312806"
    },
    "payload": {
      "token": "876afa88-8ad5-427b-9878-2edb5b103117",
      "type": "ALARM"
    }
  }
}
```

{% endraw %}

### See also
* [`Alerts.AlertStarted`](#AlertStarted)

## DeleteAlert directive {#DeleteAlert}

클라이언트에게 특정 알람을 삭제하도록 지시합니다. 클라이언트는 특정 알람을 삭제해야 하며, 다음과 같은 이벤트 메시지를 사용하여 그 결과를 CIC에게 보고해야 합니다.

* [`Alerts.DeleteAlertSucceeded`](#DeleteAlertSucceeded) 이벤트 메시지: 특정 알람을 삭제하는데 성공한 경우
* [`Alerts.DeleteAlertFailed`](#DeleteAlertFailed) 이벤트 메시지: 특정 알람을 삭제하는데 실패한 경우

### Payload fields

| 필드 이름       | 자료형    | 필드 설명                     | 포함 여부 |
|---------------|---------|-----------------------------|:---------:|
| `token`   | string | 삭제해야 할 알람의 식별자              | 항상 |
| `type`    | string | 알람의 종류. 다음과 같은 값을 가집니다. <ul><li><code>"ACTIONTIMER"</code></li><li><code>"ALARM"</code></li><li><code>"REMINDER"</code></li><li><code>"TIMER"</code></li></ul>  | 항상 |

### Message example
{% raw %}

```json
{
  "directive": {
    "header": {
      "namespace": "Alerts",
      "name": "DeleteAlert",
      "messageId": "4e4080d6-c440-498a-bb73-ae86c6312806",
      "dialogRequestId": "6b4061db-fbc1-45a2-9c54-b7c62d366b98"
    },
    "payload": {
      "token": "876afa88-8ad5-427b-9878-2edb5b103117",
      "type": "ALARM"
    }
  }
}
```

{% endraw %}

### See also
* [`Alerts.DeleteAlertFailed`](#DeleteAlertFailed)
* [`Alerts.DeleteAlertSucceeded`](#DeleteAlertSucceeded)

## DeleteAlertFailed event {#DeleteAlertFailed}

클라이언트가 클라이언트에 설정된 특정 알람을 삭제하는데 실패했음을 CIC로 보고하기 위해 사용됩니다. 클라이언트는 [Alerts.DeleteAlert](#DeleteAlert) 지시 메시지를 수신한 후 특정 알람을 삭제하는데 실패하면 반드시 이 이벤트 메시지를 CIC에게 전송해야 합니다.

### Context fields

{% include "/CIC/References/CICInterface/Context_Objects_List.md" %}

### Payload fields

| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|:---------:|
| `token`   | string | 삭제하지 못한 알람의 식별자             | 필수 |
| `type`    | string | 알람의 종류. 다음과 같은 값을 가집니다. <ul><li><code>"ACTIONTIMER"</code></li><li><code>"ALARM"</code></li><li><code>"REMINDER"</code></li><li><code>"TIMER"</code></li></ul>  | 필수 |

### Message example
{% raw %}

```json
{
  "context": [
    {{Alerts.AlertsState}},
    {{AudioPlayer.PlayerState}},
    {{Device.DeviceState}},
    {{Device.Display}},
    {{Clova.Location}},
    {{Clova.SavedPlace}},
    {{Speaker.VolumeState}},
    {{SpeechSynthesizer.SpeechState}}
  ],
  "event": {
    "header": {
      "namespace": "Alerts",
      "name": "DeleteAlertFailed",
      "messageId": "4e4080d6-c440-498a-bb73-ae86c6312806"
    },
    "payload": {
      "token": "876afa88-8ad5-427b-9878-2edb5b103117",
      "type": "ALARM"
    }
  }
}
```

{% endraw %}

### See also
* [`Alerts.DeleteAlert`](#DeleteAlert)
* [`Alerts.DeleteAlertSucceeded`](#DeleteAlertSucceeded)

## DeleteAlertSucceeded event {#DeleteAlertSucceeded}

클라이언트가 클라이언트에 설정된 특정 알람을 삭제하는데 성공했음을 CIC로 보고하기 위해 사용됩니다. 클라이언트는 [Alerts.DeleteAlert](#DeleteAlert) 지시 메시지를 수신한 후 특정 알람을 삭제하는데 성공하면 반드시 이 이벤트 메시지를 CIC에게 전송해야 합니다.

### Context fields

{% include "/CIC/References/CICInterface/Context_Objects_List.md" %}

### Payload fields

| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|:---------:|
| `token`   | string | 삭제한 알람의 식별자                  | 필수 |
| `type`    | string | 알람의 종류. 다음과 같은 값을 가집니다. <ul><li><code>"ACTIONTIMER"</code></li><li><code>"ALARM"</code></li><li><code>"REMINDER"</code></li><li><code>"TIMER"</code></li></ul>  | 필수 |

### Message example
{% raw %}

```json
{
  "context": [
    {{Alerts.AlertsState}},
    {{AudioPlayer.PlayerState}},
    {{Device.DeviceState}},
    {{Device.Display}},
    {{Clova.Location}},
    {{Clova.SavedPlace}},
    {{Speaker.VolumeState}},
    {{SpeechSynthesizer.SpeechState}}
  ],
  "event": {
    "header": {
      "namespace": "Alerts",
      "name": "DeleteAlertSucceeded",
      "messageId": "4e4080d6-c440-498a-bb73-ae86c6312806"
    },
    "payload": {
      "token": "876afa88-8ad5-427b-9878-2edb5b103117",
      "type": "ALARM"
    }
  }
}
```

{% endraw %}

### See also
* [`Alerts.DeleteAlert`](#DeleteAlert)
* [`Alerts.DeleteAlertFailed`](#DeleteAlertFailed)

## RequestAlertStop event {#RequestAlertStop}

클라이언트가 현재 울리고 있는 알람을 중지하도록 Clova에게 요청할 때 사용됩니다. 클라이언트는 사용자가 발화가 아닌 물리 버튼(Hardware)이나 소프트웨어 버튼으로 알람을 중지했을 때 CIC에게 이 이벤트 메시지를 전송해야 합니다. 클라이언트가 CIC에게 이 이벤트를 전송하면 추후 CIC로부터 [`Alerts.StopAlert`](#StopAlert) 지시 메시지를 받게됩니다.

### Context fields

{% include "/CIC/References/CICInterface/Context_Objects_List.md" %}

### Payload fields

| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|:---------:|
| `token`   | string | 중지할 알람의 식별자                  | 필수 |
| `type`    | string | 알람의 종류. 다음과 같은 값을 가집니다. <ul><li><code>"ACTIONTIMER"</code></li><li><code>"ALARM"</code></li><li><code>"REMINDER"</code></li><li><code>"TIMER"</code></li></ul>  | 필수 |

### Remarks
클라이언트의 기기에서 사용자가 버튼을 눌러 직접 알람을 중지하더라도 이 이벤트 메시지를 CIC로 전송해서 [`Alerts.StopAlert`](#StopAlert) 지시 메시지를 받은 후 알람을 종료해야 합니다. 이는 알람을 종료하는 프로세스를 일관된 패턴을 일관되게 만들며, 알람의 상태를 동기화하는데 도움이 됩니다. 다만, 알람을 종료하기까지 시간이 걸릴 수 있으므로 사용자가 버튼을 눌러 직접 알람을 중지한 경우 [`Alerts.StopAlert`](#StopAlert) 지시 메시지를 받기 전까지 알람 표시를 임의로 없애거나 알람 소리를 무음으로 바꾸는 방식으로 대응하면 됩니다.

### Message example
{% raw %}

```json
{
  "context": [
    {{Alerts.AlertsState}},
    {{AudioPlayer.PlayerState}},
    {{Device.DeviceState}},
    {{Device.Display}},
    {{Clova.Location}},
    {{Clova.SavedPlace}},
    {{Speaker.VolumeState}},
    {{SpeechSynthesizer.SpeechState}}
  ],
  "event": {
    "header": {
      "namespace": "Alerts",
      "name": "RequestAlertStop",
      "messageId": "4e4080d6-c440-498a-bb73-ae86c6312806"
    },
    "payload": {
      "token": "876afa88-8ad5-427b-9878-2edb5b103117",
      "type": "ALARM"
    }
  }
}
```

{% endraw %}

### See also
* [`Alerts.StopAlert`](#StopAlert)

## RequestSynchronizeAlert event {#RequestSynchronizeAlert}

클라이언트가 Clova의 클라우드 환경에 저장된 사용자의 알람 정보를 동기화해야 할 때 이 이벤트 메시지를 CIC로 전송합니다. CIC는 이 이벤트 메시지를 받으면, 클라이언트에게 [`Alerts.SynchronizeAlert`](#SynchronizeAlert) 지시 메시지를 전송합니다.

### Context fields

{% include "/CIC/References/CICInterface/Context_Objects_List.md" %}

### Payload fields

없음

### Message example
{% raw %}
```json
{
  "context": [
    {{Alerts.AlertsState}},
    {{AudioPlayer.PlayerState}},
    {{Device.DeviceState}},
    {{Device.Display}},
    {{Clova.Location}},
    {{Clova.SavedPlace}},
    {{Speaker.VolumeState}},
    {{SpeechSynthesizer.SpeechState}}
  ],
  "event": {
    "header": {
      "namespace": "Alerts",
      "name": "RequestSynchronizeAlert",
      "messageId": "dd4f2794-6b14-4cc4-ae1b-5bfa1c469028"
    },
    "payload": {}
  }
}
```
{% endraw %}

### See also
* [`System.SynchronizeAlert`](/CIC/References/CICInterface/Alerts.md#SynchronizeAlert)

## SetAlert directive {#SetAlert}

클라이언트에게 알람을 새로 추가하거나 특정 알람을 수정하도록 지시합니다. 클라이언트는 다음과 같이 알람 추가나 알람 수정을 수행할 수 있습니다.

* **`token` 필드의 값과 같은 식별자를 가진 알람이 현재 클라이언트의 기기에 없으면** 전달받은 알람을 추가합니다.
* **`token` 필드의 값과 같은 식별자를 가진 알람이 현재 클라이언트의 기기에 있으면** 해당 알람을 수정합니다.

또한, 다음과 같은 이벤트 메시지를 사용하여 그 결과를 CIC에게 보고해야 합니다.

* [`Alerts.SetAlertSucceeded`](#SetAlertSucceeded) 이벤트 메시지: 특정 알람을 추가/수정하는데 성공한 경우
* [`Alerts.SetAlertFailed`](#SetAlertFailed) 이벤트 메시지: 특정 알람을 추가/수정하는데 실패한 경우

### Payload field {#SetAlertPayload}

| 필드 이름       | 자료형    | 필드 설명                     | 포함 여부 |
|---------------|---------|-----------------------------|:---------:|
| `assets[]`         | object array | 리마인더(`"REMINDER"`) 타입이나 액션 타이머(`"ACTIONTIMER"`)의 알람을 울릴 때 들려줄 TTS 오디오 목록을 가지는 객체 배열. 리마인더 타입과 액션 타이머일 경우에만 이 필드가 포함됩니다.   | 조건부 |
| `assets[].assetId` | string | TTS 오디오의 식별자       | 항상 |
| `assets[].url`     | string | TTS 오디오의 URL. 만약, 이 필드의 값이 `"clova://alert/bell/{type}"` 형태이면, 클라이언트는 알람의 종류(`type`)에 따라 클라이언트가 보유하고 있는 벨소리 중 그에 맞는 벨소리를 울려야 합니다. 현재 다음과 같은 값이 올 수 있습니다. <ul><li><code>"clova://alert/bell/reminder"</code>: 리마인더용 벨소리 재생</li></ul>    | 항상 |
| `assetPlayOrder[]` | string array | `assets` 필드에 있는 TTS 오디오의 재생 순서를 저장하고 있는 배열. 배열의 인덱스 순서에 맞춰 재생할 TTS 오디오의 식별자(`assets[].assetId`)가 입력되어 있습니다. 리마인더(`"REMINDER"`) 타입이나 액션 타이머(`"ACTIONTIMER"`)의 알람일 경우에만 이 필드가 포함됩니다.  | 조건부  |
| `label`          | string | 리마인더나 액션 타이머의 내용                             | 조건부 |
| `scheduledTime`  | string | 알람이 울릴 날짜와 시간 정보(YYYY-MM-DDThh:mm:ssZ 포맷)   | 항상 |
| `token`          | string | 추가 또는 수정해야 할 알람의 식별자                        | 항상 |
| `type`           | string | 알람의 종류. 다음과 같은 값을 가집니다. <ul><li><code>"ACTIONTIMER"</code></li><li><code>"ALARM"</code></li><li><code>"REMINDER"</code></li><li><code>"TIMER"</code></li></ul>  | 항상 |

### Message example
{% raw %}

```json
{
 "directive": {
   "header": {
     "namespace": "Alerts",
     "name": "SetAlert",
     "messageId": "9a440fa9-983a-48a8-8ad5-faee1250abde",
     "dialogRequestId": "688b051d-6832-4bfd-8cf8-5ff073cd2a82"
   },
   "payload": {
     "type": "REMINDER",
     "token": "77179dbd-b65f-4341-a579-c1b2b97fc5b7",
     "scheduledTime": "2017-09-25T09:00:50+09:00",
     "assets": [
       {
         "assetId": "5141f693-5b39-46b7-80e4-3d71ed5508da",
         "url": "clova://alert/bell/reminder"
       },
       {
         "assetId": "b403ebe5-f911-4c5c-98b3-9f5320510235",
         "url": "http://abc.de.fe/tts2"
       }
     ],
     "label": "입금하기",
     "assetPlayOrder": ["5141f693-5b39-46b7-80e4-3d71ed5508da", "b403ebe5-f911-4c5c-98b3-9f5320510235"]
   }
 }
}
```

{% endraw %}

### See also
* [`Alerts.SetAlertFailed`](#SetAlertFailed)
* [`Alerts.SetAlertSucceeded`](#SetAlertSucceeded)

## SetAlertFailed event {#SetAlertFailed}

클라이언트가 특정 알람을 추가 또는 수정하는데 실패했음을 CIC로 보고하기 위해 사용됩니다. 클라이언트는 [Alerts.SetAlert](#SetAlert) 지시 메시지를 수신한 후 특정 알람을 추가 또는 수정하는데 실패하면 반드시 이 이벤트 메시지를 CIC에게 전송해야 합니다.

### Context fields

{% include "/CIC/References/CICInterface/Context_Objects_List.md" %}

### Payload fields

| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|:---------:|
| `token`   | string | 추가 또는 수정하지 못한 알람의 식별자     | 필수 |
| `type`    | string | 알람의 종류. 다음과 같은 값을 가집니다. <ul><li><code>"ACTIONTIMER"</code></li><li><code>"ALARM"</code></li><li><code>"REMINDER"</code></li><li><code>"TIMER"</code></li></ul>  | 필수 |

### Message example
{% raw %}

```json
{
  "context": [
    {{Alerts.AlertsState}},
    {{AudioPlayer.PlayerState}},
    {{Device.DeviceState}},
    {{Device.Display}},
    {{Clova.Location}},
    {{Clova.SavedPlace}},
    {{Speaker.VolumeState}},
    {{SpeechSynthesizer.SpeechState}}
  ],
  "event": {
    "header": {
      "namespace": "Alerts",
      "name": "SetAlertFailed",
      "messageId": "4e4080d6-c440-498a-bb73-ae86c6312806"
    },
    "payload": {
      "token": "876afa88-8ad5-427b-9878-2edb5b103117",
      "type": "ALARM"
    }
  }
}
```

{% endraw %}

### See also
* [`Alerts.SetAlert`](#SetAlert)
* [`Alerts.SetAlertSucceeded`](#SetAlertSucceeded)


## SetAlertSucceeded event {#SetAlertSucceeded}

클라이언트가 특정 알람을 추가 또는 수정하는데 성공했음을 CIC로 보고하기 위해 사용됩니다. 클라이언트는 [Alerts.SetAlert](#SetAlert) 지시 메시지를 수신한 후 특정 알람을 추가 또는 수정하는데 성공하면 반드시 이 이벤트 메시지를 CIC에게 전송해야 합니다.

### Context fields

{% include "/CIC/References/CICInterface/Context_Objects_List.md" %}

### Payload fields

| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|:---------:|
| `token`   | string | 추가 또는 수정한 알람의 식별자          | 필수 |
| `type`    | string | 알람의 종류. 다음과 같은 값을 가집니다. <ul><li><code>"ACTIONTIMER"</code></li><li><code>"ALARM"</code></li><li><code>"REMINDER"</code></li><li><code>"TIMER"</code></li></ul>  | 필수 |

### Message example
{% raw %}

```json
{
  "context": [
    {{Alerts.AlertsState}},
    {{AudioPlayer.PlayerState}},
    {{Device.DeviceState}},
    {{Device.Display}},
    {{Clova.Location}},
    {{Clova.SavedPlace}},
    {{Speaker.VolumeState}},
    {{SpeechSynthesizer.SpeechState}}
  ],
  "event": {
    "header": {
      "namespace": "Alerts",
      "name": "SetAlertSucceeded",
      "messageId": "4e4080d6-c440-498a-bb73-ae86c6312806"
    },
    "payload": {
      "token": "876afa88-8ad5-427b-9878-2edb5b103117",
      "type": "ALARM"
    }
  }
}
```

{% endraw %}

### See also
* [`Alerts.SetAlert`](#SetAlert)
* [`Alerts.SetAlertFailed`](#SetAlertFailed)

## StopAlert directive {#StopAlert}

클라이언트에게 특정 알람을 중지하도록 지시합니다. 클라이언트는 지정된 알람을 중지해야 하며, [`AlertStopped`](#AlertStopped) 이벤트 메시지를 사용하여 그 결과를 CIC에게 보고해야 합니다.


### Payload fields

| 필드 이름       | 자료형    | 필드 설명                     | 포함 여부 |
|---------------|---------|-----------------------------|:---------:|
| `token`   | string | 중지해야 할 알람의 식별자              | 항상 |
| `type`    | string | 알람의 종류. 다음과 같은 값을 가집니다. <ul><li><code>"ACTIONTIMER"</code></li><li><code>"ALARM"</code></li><li><code>"REMINDER"</code></li><li><code>"TIMER"</code></li></ul>  | 항상 |

### Message example
{% raw %}

```json
{
  "directive": {
    "header": {
      "namespace": "Alerts",
      "name": "DeleteAlert",
      "messageId": "4e4080d6-c440-498a-bb73-ae86c6312806",
      "dialogRequestId": "6b4061db-fbc1-45a2-9c54-b7c62d366b98"
    },
    "payload": {
      "token": "876afa88-8ad5-427b-9878-2edb5b103117",
      "type": "ALARM"
    }
  }
}
```

{% endraw %}

### See also
* [`Alerts.AlertStopped`](#AlertStopped)

## SynchronizeAlert directive {#SynchronizeAlert}
클라이언트에게 `payload` 필드에 있는 사용자의 알람 데이터를 동기화하도록 지시합니다. 클라이언트는 Clova로부터 전달된 데이터에 맞게 클라이언트에 설정된 알람 값을 변경해야 합니다.

### Payload fields

| 필드 이름       | 자료형    | 필드 설명                     | 포함 여부 |
|---------------|---------|-----------------------------|:---------:|
| `allAlerts[]`   | object array | 클라이언트가 동기화해야 할 알람 목록을 가지는 객체 배열. [`Alerts.SetAlert`](#SetAlert) 지시 메시지에 사용되는 [`payload`](#SetAlertPayload) 객체와 같은 포맷을 가집니다. | 항상    |

### Message example

{% raw %}

```json
// Deprecated example
{
  "directive": {
    "header": {
      "namespace": "Alerts",
      "name": "SynchronizeAlert",
      "messageId": "29745c13-0d70-408e-a4cc-946afba67524"
    },
    "payload": {
      "allAlerts": [
        {
          "type": "REMINDER",
          "token": "77179dbd-b65f-4341-a579-c1b2b97fc5b7",
          "scheduledTime": "2017-09-25T09:00:50+09:00",
          "assets": [
            {
              "assetId": "5141f693-5b39-46b7-80e4-3d71ed5508da",
              "url": "clova://alert/bell/reminder"
            },
            {
              "assetId": "b403ebe5-f911-4c5c-98b3-9f5320510235",
              "url": "http://abc.de.fe/tts2"
            }
          ],
          "assetPlayOrder": ["5141f693-5b39-46b7-80e4-3d71ed5508da", "b403ebe5-f911-4c5c-98b3-9f5320510235"]
        },
        {
          "type": "ALARM",
          "token": "ee4da70c-8328-4456-ab6f-c28cec626ae6",
          "scheduledTime": "2017-09-26T11:00:50+09:00"
        },
        ...
      ]
    }
  }
}
```

{% endraw %}

### See also
* [`Alerts.RequestSynchronizeAlert`](#RequestSynchronizeAlert)
