# Alerts

Alerts is a namespace controlled by the client to add, change, remove, start or stop an alert. The following table shows types of alarm.

| Types of alarm | Explanation                                |
|---------|------------------------------------|
| Alarm(`"ALARM"`)            | An alarm that rings at a set date and time                                             |
| Timer(`"TIMER"`)           | An alarm that rings after a set time has elapsed                                         |
| Action timer(`"ACTIONTIMER"`) | An alarm that conveys a specified action after a set time has elapsed                                |
| Reminder(`"REMINDER"`)      | An alarm that reminds the user of what the user has requested. If the user makes a request to "ring the alarm tomorrow at 7P.M. to take the medicine", the alarm will be scheduled to ring at 7.P.M and "Take the medicine" will become the actual alarm message. The alarm message will either be delivered as a voice notification or a voice notification and a UI display.  |


The user can add an alarm via voice command or the Clova app. Changing or removing the alarm can be done only through the app. Clova stores alarm details in cloud environment. Alarms added by the user are delivered to the client through CIC. In case of repeated alarm, Clova only delivers the most recent alarm to the client. When the alarm stops, it lets the client know the next repeated alarm.

In consequence, the client should carry out the following actions using alerts interface.
* Upon receiving a directive message from CIC, add, change or remove the alarm according to the message.
* Ring the alarm at the time when it should be rang.
* When add, change, remove, start or stop the alarm, a report should be made to CIC. Only when the report is made, a correspond result will be returned to the client from CIC.
* As delivering an event message, [`Alerts.AlertsState`](/CIC/References/Context_Objects.md#AlertsState) context object must be sent together to report the alarm status setup by the client.

<div class="note">
  <p><strong>Note!</strong></p>
  <p>Refer to <a href="#AlertsWorkFlow">Alarm work flow</a> to find out about structure of alarm actions (add, change, remove, start or stop).</p>
</div>

Alerts provide the following event and directive messages.

| Message name         | Message type  | Message description                                   |
|------------------|-----------|---------------------------------------------|
| [`AlertStarted`](#AlertStarted)                 | Event     | The message reports to CIC that the client has started an alarm.  |
| [`AlertStopped`](#AlertStopped)                 | Event     | The message reports to CIC that the client has stopped an alarm. |
| [`DeleteAlert`](#DeleteAlert)                   | Directive | Instructs your client to delete a specified alarm.  |
| [`DeleteAlertFailed`](#DeleteAlertFailed)       | Event     | The message reports to CIC that the client has failed to delete a specified alarm.  |
| [`DeleteAlertSucceeded`](#DeleteAlertSucceeded) | Event     | The message reports to CIC that the client has successfully deleted a specified alarm. |
| [`RequestAlertStop`](#RequestAlertStop)         | Event     | The message sends request to Clova to stop the ringing alarm.   |
| [`SetAlert`](#SetAlert)                         | Directive | Instructs your client to add an alarm or to change a specified alarm. |
| [`SetAlertFailed`](#SetAlertFailed)             | Event     | The message reports to CIC that the client has failed to add or change a specified alarm. |
| [`SetAlertSucceeded`](#SetAlertSucceeded)       | Event     | The message reports to CIC that the client has successfully added or changed a specified alarm. |
| [`StopAlert`](#StopAlert)                       | Directive | Instructs your client to stop a specified alarm.  |

## Alarm work flow {#AlertsWorkFlow}

The general flow from adding to stopping an alarm is as below.

1. The user requests([`SpeechRecognizer.Recognize`](/CIC/References/CICInterface/SpeechRecognizer.md#Recognize)) to add an alarm through a voice command.
2. After saving the user's alarm, Clova sends a [`Alerts.SetAlert`](#SetAlert) directive message to the user's client device so that it can add the alarm.
3. The client passes the result of attempting to add the alarm (By using [`Alerts.SetAlertSucceeded`](#SetAlertSucceeded) event message and [`Alerts.SetAlertFailed`](#SetAlertFailed) event message).
4. To return the result of adding the alarm to the user, Clova passes a [`SpeechSynthesizer.Speak`](/CIC/References/CICInterface/SpeechSynthesizer.md#Speak) directive message and a [`Clova.RenderTemplate`](/CIC/References/CICInterface/Clova.md#RenderTemplate) directive message to the client.
5. (When it is the designated time) The client should ring the alarm and report a [`Alerts.AlertStarted`](#AlertStarted) event message to CIC that the alarm has started. When the client is sending the [`Alerts.AlertStarted`](#AlertStarted) event message, fill up the ringing alarm details on `activeAlerts` field of [`Alert.AlertsState`](/CIC/References/Context_Objects.md#AlertsState) context information.
6. The user will request([`Alerts.RequestAlertStop`](#RequestAlertStop)) to stop the alarm through a voice command ([`SpeechRecognizer.Recognize`](/CIC/References/CICInterface/SpeechRecognizer.md#Recognize)) or by pressing a physical button (hardware method) or a GUI button (software method).
7. Clova will send a directive message to the client [`Alerts.StopAlert`](#StopAlert) to stop the alarm.
8. After stopping the alarm, the client should send a [`Alerts.AlertStopped`](#SetAlertSucceeded) event message to report that the alarm has stopped.

<div class="note">
<p><strong>Note!</strong></p>
<p>In case of a repeated alarm, only the nearest alarm from the current hour will be added and executed on the client. When the repeated alarm is stopped, a new repeated alarm will be passed to client from CIC. If network is disconnected for a long time, the repeated alarm may not work properly. </p>
</div>

The alarm can be changed or removed before the step 5 and they can only be done from the Clova app. Unless the directive message is not sent as a response to the user's voice request, it will be passed to the client through [downchannel](/CIC/Guides/Interact_with_CIC.md#CreateConnection).

The following are steps of how to change or remove the alarm.

1. The user attempts to change or remove the alarm from the Clove app.
2. To respond to the user's request, Clova sends a [`Alerts.SetAlert`](#SetAlert) directive message or a [`Alerts.DeleteAlert`](#DeleteAlert) directive message to the client.
3. The client passes the result of changing or removing the alarm to Clova (Through the related event message).

If the user's client is added or if partial or specified clients are reconnected after the network disconnection, they should go through below process to connect the user's alarm details from the server to the client.

1. If the client is connected or reconnected to CIC, it should pass a [`System.RequestSynchronizeState`](/CIC/References/CICInterface/System.md#RequestSynchronizeState) event message to CIC.
2. The client receives a [`System.SynchronizeState`](/CIC/References/CICInterface/System.md#SynchronizeState) directive message from CIC and at this point, the alarm data from `allAlerts` field should be synchronized with the alarm details from the device.

<div class="danger">
<p><strong>Caution!</strong></p>
<p>Note that if the client is disconnected from network due to above work flow, all alarm actions will not be conducted properly. </p>
</div>

## AlertStarted event {#AlertStarted}

The message reports to CIC that the client has started an alarm. The client must send the event message to CIC once the alarm starts and rings.

### Context field
Send the following [context information](/CIC/References/Context_Objects.md) together.

* [`Alerts.AlertsState`](/CIC/References/Context_Objects.md#AlertsState)

### Payload field

| Field name       | Type    | Field description                     | Required |
|---------------|---------|-----------------------------|---------|
| `token`   | string | Identifier of started alarms.                  | Yes |
| `type`    | string | Types of alarm. Available values are: <ul><li><code>ACTIONTIMER</code></li><li><code>"ALARM"</code></li><li><code>"REMINDER"</code></li><li><code>TIMER</code></li></ul>  | Yes |

### Message example
{% raw %}

```json
{
  "context": [
    {{Alerts.AlertState}},
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
* [`Alerts.AlertsState`](/CIC/References/Context_Objects.md#AlertsState)
* [`Alerts.AlertStopped`](#AlertStopped)

## AlertStopped event {#AlertStopped}

The message reports to CIC that the client has stopped an alarm. The client must send the event message to CIC once the alarm stops.
* **If a general alarm is stopped**, a [`Alerts.DeleteAlert`](#DeleteAlert) directive message will be sent from CIC.
* **If a repeated alarm is stopped**, a [`Alerts.SetAlert`](#SetAlert) directive message will be sent from CIC to set the next repeated alarm.

### Context field
Send the following [context information](/CIC/References/Context_Objects.md) together.

* [`Alerts.AlertsState`](/CIC/References/Context_Objects.md#AlertsState)

### Payload field

| Field name       | Type    | Field description                     | Required |
|---------------|---------|-----------------------------|---------|
| `token`   | string | Identifier of stopped alarms.                 | Yes |
| `type`    | string | Types of alarm. Available values are: <ul><li><code>ACTIONTIMER</code></li><li><code>"ALARM"</code></li><li><code>"REMINDER"</code></li><li><code>TIMER</code></li></ul>  | Yes |

### Message example
{% raw %}

```json
{
  "context": [
    {{Alerts.AlertState}},
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
* [`Alerts.AlertsState`](/CIC/References/Context_Objects.md#AlertsState)
* [`Alerts.AlertStarted`](#AlertStarted)

## DeleteAlert directive {#DeleteAlert}

Instructs your client to delete a specified alarm. The client must delete the specified alarm and report the result to CIC using the following directive message.

* [`Alerts.DeleteAlertSucceeded`](#DeleteAlertSucceeded) event message: If the client successfully deleted the specified alarm
* [`Alerts.DeleteAlertFailed`](#DeleteAlertSucceeded) event message: If the client failed to delete the specified alarm

### Payload field

| Field name       | Type    | Field description                     | Required |
|---------------|---------|-----------------------------|---------|
| `token`   | string | Identifier of to-be-deleted alarms.                 | Yes |
| `type`    | string | Types of alarm. Available values are: <ul><li><code>ACTIONTIMER</code></li><li><code>"ALARM"</code></li><li><code>"REMINDER"</code></li><li><code>TIMER</code></li></ul>  | Yes |

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

The message reports to CIC that the client has failed to delete a specified alarm. If the client fails to delete the specified alarm after receiving a [Alerts.DeleteAlert](#DeleteAlert) directive message, it must send the event message to CIC.

### Context field
Send the following [context information](/CIC/References/Context_Objects.md) together.

* [`Alerts.AlertsState`](/CIC/References/Context_Objects.md#AlertsState)

### Payload field

| Field name       | Type    | Field description                     | Required |
|---------------|---------|-----------------------------|---------|
| `token`   | string | Identifier of failed-to-delete alarms.                 | Yes |
| `type`    | string | Types of alarm. Available values are: <ul><li><code>ACTIONTIMER</code></li><li><code>"ALARM"</code></li><li><code>"REMINDER"</code></li><li><code>TIMER</code></li></ul>  | Yes |

### Message example
{% raw %}

```json
{
  "context": [
    {{Alerts.AlertState}},
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

The message reports to CIC that the client has successfully deleted a specified alarm. If the client successfully deletes the specified alarm after receiving a [Alerts.DeleteAlert](#DeleteAlert) directive message, it must send the event message to CIC.

### Context field
Send the following [context information](/CIC/References/Context_Objects.md) together.

* [`Alerts.AlertsState`](/CIC/References/Context_Objects.md#AlertsState)

### Payload field

| Field name       | Type    | Field description                     | Required |
|---------------|---------|-----------------------------|---------|
| `token`   | string | Identifier of deleted alarms.                 | Yes |
| `type`    | string | Types of alarm. Available values are: <ul><li><code>ACTIONTIMER</code></li><li><code>"ALARM"</code></li><li><code>"REMINDER"</code></li><li><code>TIMER</code></li></ul>  | Yes |

### Message example
{% raw %}

```json
{
  "context": [
    {{Alerts.AlertState}},
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

The message sends request to Clova to stop the ringing alarm. The client should send the event message to CIC when the user stopped the alarm with the software button instead of the physical button (Hardware). The client will receive a [`Alerts.StopAlert`](#StopAlert) directive message from CIC in the future once sending the event message to CIC.

### Context field
Send the following [context information](/CIC/References/Context_Objects.md) together.

* [`Alerts.AlertsState`](/CIC/References/Context_Objects.md#AlertsState)

### Payload field

| Field name       | Type    | Field description                     | Required |
|---------------|---------|-----------------------------|---------|
| `token`   | string | Identifier of to-be-stopped alarms.                 | Yes |
| `type`    | string | Types of alarm. Available values are: <ul><li><code>ACTIONTIMER</code></li><li><code>"ALARM"</code></li><li><code>"REMINDER"</code></li><li><code>TIMER</code></li></ul>  | Yes |

### Remarks
Even after the alarm has stopped as the user press the button on the client's device, it has to be ended after receiving a [`Alerts.StopAlert`](#StopAlert) directive message upon sending the event message to CIC. This alarm termination method will make a coherent pattern for the termination process and is helpful when synchronizing the alarm status. In case the stop button was pressed directly by the user, respond by removing the alarm sign arbitrarily or mute the alarm sound until receiving the [`Alerts.StopAlert`](#StopAlert) directive message since some loading time may take place until the termination.

### Message example
{% raw %}

```json
{
  "context": [
    {{Alerts.AlertState}},
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

## SetAlert directive {#SetAlert}

Instructs your client to add an alarm or to change a specified alarm. The client may add or change an alarm in the following condition.

* **If an alarm that has the same identifier as the `token` field value currently does not exist on the client device**,add the received alarm.
* **If an alarm that has the same identifier as the `token` field value currently does exist on the client device**, make change on the alarm.

The client should report the result to CIC using the following directive message.

* [`Alerts.SetAlertSucceeded`](#SetAlertSucceeded) event message: If the client successfully added or changed the specified alarm
* [`Alerts.SetAlertFailed`](#SetAlertFailed) event message: If the client failed to add or change the specified alarm

### Payload field (AlertObject) {#AlertObject}

| Field name       | Type    | Field description                     | Required |
|---------------|---------|-----------------------------|---------|
| `assets[]`         | object array | An object array containing TTS audio list that turns on when reminder (`"REMINDER"`) type or action timer (`"ACTIONTIMER"`) alarm rings. This field is included only if it is a reminder type or an action timer.    | No |
| `assets[].assetId` | string | Identifier of TTS audio       | Yes |
| `assets[].url`     | string | URL of TTS audio. If the value of the field is `"clova://bell"`, the client should ring a matching bell ring according to the types(`type`)of the alarm.    | Yes |
| `assetPlayOrder[]` | string array | An array storing TTS audio play order in `assets` field. TTS audio identifier(`assets[].assetId`) that will play the audio according to the array index is included. This field is included only if it is a reminder(`"REMINDER"`) type or an action timer(`"ACTIONTIMER"`).  | No  |
| `scheduledTime`  | string | Date and time when the alarm will ring (YYYY-MM-DDThh:mm:ssZ format)   | Yes |
| `token`          | string | Identifier of to-be-added/changed alarms.                       | Yes |
| `type`           | string | Types of alarm. Available values are: <ul><li><code>ACTIONTIMER</code></li><li><code>"ALARM"</code></li><li><code>"REMINDER"</code></li><li><code>TIMER</code></li></ul>  | Yes |

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
         "url": "clova://bell"
       },
       {
         "assetId": "b403ebe5-f911-4c5c-98b3-9f5320510235",
         "url": "http://abc.de.fe/tts2"
       }
     ],
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

The message reports to CIC that the client has failed to add or change a specified alarm. If the client fails to add or change the specified alarm after receiving a [Alerts.SetAlertFailed](#SetAlertFailed) directive message, it must send the event message to CIC.

### Context field
Send the following [context information](/CIC/References/Context_Objects.md) together.

* [`Alerts.AlertsState`](/CIC/References/Context_Objects.md#AlertsState)

### Payload field

| Field name       | Type    | Field description                     | Required |
|---------------|---------|-----------------------------|---------|
| `token`   | string | Identifier of failed-to-add/change alarms.                 | Yes |
| `type`    | string | Types of alarm. Available values are: <ul><li><code>ACTIONTIMER</code></li><li><code>"ALARM"</code></li><li><code>"REMINDER"</code></li><li><code>TIMER</code></li></ul>  | Yes |

### Message example
{% raw %}

```json
{
  "context": [
    {{Alerts.AlertState}},
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

The message reports to CIC that the client has successfully added or changed a specified alarm. If the client successfully added or changed the specified alarm after receiving a [Alerts.SetAlertFailed](#SetAlertFailed) directive message, it must send the event message to CIC.

### Context field
Send the following [context information](/CIC/References/Context_Objects.md) together.

* [`Alerts.AlertsState`](/CIC/References/Context_Objects.md#AlertsState)

### Payload field

| Field name       | Type    | Field description                     | Required |
|---------------|---------|-----------------------------|---------|
| `token`   | string | Identifier of added or changed alarms.                 | Yes |
| `type`    | string | Types of alarm. Available values are: <ul><li><code>ACTIONTIMER</code></li><li><code>"ALARM"</code></li><li><code>"REMINDER"</code></li><li><code>TIMER</code></li></ul>  | Yes |

### Message example
{% raw %}

```json
{
  "context": [
    {{Alerts.AlertState}},
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

Instructs your client to stop a specified alarm. The client must stop the specified alarm and report the result to CIC using the following [`AlertStopped`](#AlertStopped) directive message.


### Payload field

| Field name       | Type    | Field description                     | Required |
|---------------|---------|-----------------------------|---------|
| `token`   | string | Identifier of should-be-stopped alarms.                 | Yes |
| `type`    | string | Types of alarm. Available values are: <ul><li><code>ACTIONTIMER</code></li><li><code>"ALARM"</code></li><li><code>"REMINDER"</code></li><li><code>TIMER</code></li></ul>  | Yes |

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
