# Alerts

The Alerts namespace provides interfaces for you to add, change, remove, start, or stop an alert. Available alarm types are as follows.

| Alarm Type | Description                                |
|---------|------------------------------------|
| Alarm (`"ALARM"`)            | An alarm that rings at a set date and time.                                            |
| Timer (`"TIMER"`)           | An alarm that rings after a set time has elapsed.                                         |
| Action timer (`"ACTIONTIMER"`) | An alarm that executes a certain action after a set time has elapsed.                               |
| Reminder (`"REMINDER"`)      | An alarm that reminds the user of what the user has requested. If the user makes a request to "Ring the alarm tomorrow at 7 p.m. to take the medicine", the alarm will be scheduled to ring at 7 p.m. and "Take the medicine" will be the alarm message. When it is time to ring the alarm, play and display the alarm message provided by CIC. |

A user can add an alarm by voice request or through the Clova app, but changing or removing the alarm is only available through the app. Clova stores alarm details on the cloud and through CIC informs clients to alert user. Of repeated alarms, Clova informs the client only of the first upcoming alarm, instead of giving the bulk alarm information at once. After the first upcoming alarm rings and stops, Clova lets the client know of the next repeated alarm.

You must implement the following on a client, using the Alerts interfaces:

* Upon receiving a directive from CIC, add, change, or remove the alarm as instructed by the directive.
* Ring the alarm at the set time.
* Report to CIC when adding, changing, removing, starting, or stopping the alarm. Only by then a corresponding result will be returned to the client from CIC.
* Include the [`Alerts.AlertsState`](/CIC/References/Context_Objects.md#AlertsState) context object in your events to report to CIC the alarm state on the client.

<div class="note">
  <p><strong>Note!</strong></p>
  <p> See the <a href="#AlertsWorkFlow">Overall process</a> section for handling alarm actions such as adding, changing, removing, starting and stopping.</p>
</div>

The Alerts namespace provides the following events and directives.

| Name    | Message type  | Description                                   |
|------------------|-----------|---------------------------------------------|
| [`AlertStarted`](#AlertStarted)                 | Event     | A message to report to CIC that the client has started ringing an alarm. |
| [`AlertStopped`](#AlertStopped)                 | Event     | A message to report to CIC that the client has stopped an alarm. |
| [`DeleteAlert`](#DeleteAlert)                   | Directive | Instructs a client to delete the specified alarm. |
| [`DeleteAlertFailed`](#DeleteAlertFailed)       | Event     | A message to report to CIC that the client has failed to delete the specified alarm. |
| [`DeleteAlertSucceeded`](#DeleteAlertSucceeded) | Event     | A message to report to CIC that the client has successfully deleted the specified alarm. |
| [`RequestAlertStop`](#RequestAlertStop)         | Event     | A message to request to Clova to stop the ringing alarm.  |
| [`SetAlert`](#SetAlert)                         | Directive | Instructs a client to add an alarm or to change the specified alarm. |
| [`SetAlertFailed`](#SetAlertFailed)             | Event     | A message to report to CIC that the client has failed to add or change the specified alarm. |
| [`SetAlertSucceeded`](#SetAlertSucceeded)       | Event     | A message to report to CIC that the client has successfully added or changed the specified alarm. |
| [`StopAlert`](#StopAlert)                       | Directive | Instructs a client to stop the specified alarm.  |

## Overall process {#AlertsWorkFlow}

The general flow of adding an alarm to stopping an alarm is as follows.

1. A user makes a voice request ([`SpeechRecognizer.Recognize`](/CIC/References/CICInterface/SpeechRecognizer.md#Recognize)) to add an alarm.
2. Clova saves the requested alarm and then sends the [`Alerts.SetAlert`](#SetAlert) directive to the user's client for the client to add the alarm.
3. The client adds the alarm and informs CIC of the result by using the [`Alerts.SetAlertSucceeded`](#SetAlertSucceeded) event and the [`Alerts.SetAlertFailed`](#SetAlertFailed) event.
4. To inform the user of the result for the request, Clova sends the  [`SpeechSynthesizer.Speak`](/CIC/References/CICInterface/SpeechSynthesizer.md#Speak) directive and the [`Clova.RenderTemplate`](/CIC/References/CICInterface/Clova.md#RenderTemplate) directive to the client.
5. The client rings the alarm at the set time and report to CIC with the [`Alerts.AlertStarted`](#AlertStarted) event that the client has started ringing the alarm. The client MUST include the alarm information in every event that is sent to CIC until alarm stop. You can include the details of the ringing alarm through the `activeAlerts` field of the [`Alert.AlertsState`](/CIC/References/Context_Objects.md#AlertsState) context information.
6. The user requests to stop the alarm ([`Alerts.RequestAlertStop`](#RequestAlertStop)) with a voice command ([`SpeechRecognizer.Recognize`](/CIC/References/CICInterface/SpeechRecognizer.md#Recognize)) or by pressing a button on the client device or client app.
7. Clova sends the [`Alerts.StopAlert`](#StopAlert) directive to the client to stop the alarm.
8. The client stops the alarm and sends the [`Alerts.AlertStopped`](#SetAlertSucceeded) event to CIC to report that the client has stopped the alarm.

<div class="note">
<p><strong>Note!</strong></p>
<p>For a repeated alarm, CIC informs the client only of the first upcoming alarm. Only after the given alarm has rang and stopped, the client will get the information of the upcoming alarm of the repeated alarm. If a client loses network connection for a while, repeated alarms will not work properly, since no succeeding alarm information would be received.</p>
</div>

### Changing and removing alarms

Alarms can be changed or removed before step 5 of the [overall process](#AlertsWorkFlow) and only through the Clova app. A directive for this request will be sent through a [downchannel](/CIC/Guides/Interact_with_CIC.md#CreateConnection). The reason being that the directives not as responses to a voice request are designed to be forwarded to the client through a downchannel.

Have a look at the following process of changing or removing an alarm.

1. The user attempts to change or remove an alarm on the Clove app.
2. To respond to the user's request, Clova sends the [`Alerts.SetAlert`](#SetAlert) directive or the [`Alerts.DeleteAlert`](#DeleteAlert) directive to the client.
3. The client attempts to change or remove the alarm and then passes the result to Clova with an event.

### Synchronizing alarm information

Synchronize alarm information in any of the following cases:

* When the user has added a client to the user's account.
* If any of the user's client has reconnected with CIC after network disconnection.
* If the user account authenticated on a client has changed to a different account.

To synchronize alarm information:

1. After establishing or re-establishing a connection with CIC, send the [`System.RequestSynchronizeState`](/CIC/References/CICInterface/System.md#RequestSynchronizeState) event to CIC. CIC will send the [`System.SynchronizeState`](/CIC/References/CICInterface/System.md#SynchronizeState) directive in return.
2. Synchronize the alarm information on the client with the information contained in the  `allAlerts` field of the [`System.SynchronizeState`](/CIC/References/CICInterface/System.md#SynchronizeState) directive.

<div class="danger">
<p><strong>Caution!</strong></p>
<p>Note that maintaining network connection is crucial in providing the alarm service, since alarm information is provided by CIC.</p>
</div>

## AlertStarted event {#AlertStarted}

A message for reporting to CIC that the client has started ringing an alarm. You MUST send this event to CIC once you start ringing the alarm.

### Context fields

Send the following [context information](/CIC/References/Context_Objects.md) with this event.

* [`Alerts.AlertsState`](/CIC/References/Context_Objects.md#AlertsState)

### Payload fields

| Field name       | Type    | Description                     | Required |
|---------------|:---------:|-----------------------------|:---------:|
| `token`   | string | The ID of the ringing alarm.                 | Required |
| `type`    | string | The alarm type. Available types are: <ul><li><code>"ACTIONTIMER"</code></li><li><code>"ALARM"</code></li><li><code>"REMINDER"</code></li><li><code>"TIMER"</code></li></ul>  | Required |

### Message example

{% raw %}

```json
{
  "context": [
    {{Alerts.AlertState}}
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

A message for reporting to CIC that the client has stopped ringing an alarm. You MUST send this event to CIC once you stop ringing the alarm. As a response to this event, CIC will send a directive depending on the stopped alarm's repeat settings:

* **If a regular alarm is stopped**: The [`Alerts.DeleteAlert`](#DeleteAlert) directive is sent.
* **If a repeated alarm is stopped**: The [`Alerts.SetAlert`](#SetAlert) directive is sent for the client to set the succeeding alarm.

### Context fields

Send the following [context information](/CIC/References/Context_Objects.md) with this event.

* [`Alerts.AlertsState`](/CIC/References/Context_Objects.md#AlertsState)

### Payload fields

| Field name       | Type    | Description                    | Required |
|---------------|:---------:|-----------------------------|:---------:|
| `token`   | string | The ID of the stopped alarm.                 | Required |
| `type`    | string | The alarm type. Available types are: <ul><li><code>"ACTIONTIMER"</code></li><li><code>"ALARM"</code></li><li><code>"REMINDER"</code></li><li><code>"TIMER"</code></li></ul>  | Required |

### Message example
{% raw %}

```json
{
  "context": [
    {{Alerts.AlertState}}
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

Instructs a client to delete the specified alarm. When you receive this directive, delete the specified alarm and report the result to CIC using either one of the following events:

* [`Alerts.DeleteAlertSucceeded`](#DeleteAlertSucceeded) event: If the client has successfully deleted the specified alarm.
* [`Alerts.DeleteAlertFailed`](#DeleteAlertFailed) event: If the client has failed to delete the specified alarm.

### Payload fields

| Field name       | Type    | Description                    | Provided |
|---------------|:---------:|-----------------------------|:---------:|
| `token`   | string | The ID of the alarm to delete.                 | Always |
| `type`    | string | The alarm type. Available types are: <ul><li><code>"ACTIONTIMER"</code></li><li><code>"ALARM"</code></li><li><code>"REMINDER"</code></li><li><code>"TIMER"</code></li></ul>  | Always |

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

A message for reporting to CIC that the client has failed to delete the specified alarm. Send this event to CIC if you fail to delete the specified alarm for the [Alerts.DeleteAlert](#DeleteAlert) directive.

### Context fields

Send the following [context information](/CIC/References/Context_Objects.md) with this event.

* [`Alerts.AlertsState`](/CIC/References/Context_Objects.md#AlertsState)

### Payload fields

| Field name       | Type    | Description                    | Required |
|---------------|:---------:|-----------------------------|:---------:|
| `token`   | string | The ID of the alarm the client has failed to delete.                 | Required |
| `type`    | string | The alarm type. Available types are: <ul><li><code>"ACTIONTIMER"</code></li><li><code>"ALARM"</code></li><li><code>"REMINDER"</code></li><li><code>"TIMER"</code></li></ul>  | Required |

### Message example
{% raw %}

```json
{
  "context": [
    {{Alerts.AlertState}}
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

A message for reporting to CIC that the client has successfully deleted the specified alarm. Send this event to CIC once you delete the specified alarm successfully for the [Alerts.DeleteAlert](#DeleteAlert) directive.

### Context fields

Send the following [context information](/CIC/References/Context_Objects.md) with this event.

* [`Alerts.AlertsState`](/CIC/References/Context_Objects.md#AlertsState)

### Payload fields

| Field name       | Type    | Description                    | Required |
|---------------|:---------:|-----------------------------|:---------:|
| `token`   | string | The ID of the alarm deleted.                | Required |
| `type`    | string | The alarm type. Available types are: <ul><li><code>"ACTIONTIMER"</code></li><li><code>"ALARM"</code></li><li><code>"REMINDER"</code></li><li><code>"TIMER"</code></li></ul>  | Required |

### Message example
{% raw %}

```json
{
  "context": [
    {{Alerts.AlertState}}
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

A message for requesting Clova to stop the ringing alarm. Send this event to CIC when the user stops the alarm _not_ with a voice command, but by pressing a button on the client device or the client app. CIC will send the [`Alerts.StopAlert`](#StopAlert) directive as a response to this event.

### Context fields

Send the following [context information](/CIC/References/Context_Objects.md) with this event.

* [`Alerts.AlertsState`](/CIC/References/Context_Objects.md#AlertsState)

### Payload fields

| Field name       | Type    | Description                    | Required |
|---------------|:---------:|-----------------------------|:---------:|
| `token`   | string | The ID of the alarm to stop.                 | Required |
| `type`    | string | The alarm type. Available types are: <ul><li><code>"ACTIONTIMER"</code></li><li><code>"ALARM"</code></li><li><code>"REMINDER"</code></li><li><code>"TIMER"</code></li></ul>  | Required |

### Remarks

Stopping a ringing alarm requires informing CIC of the stopping and getting confirmation from CIC to stop. So, a user pressing a button to stop the alarm is not the end of the task. You will send this event to inform CIC, and CIC will return the [`Alerts.StopAlert`](#StopAlert) directive.
Such process guarantees consistency in stopping an alarm and is helpful for synchronizing alarm information between clients and CIC. Yet, to provide seamless UX to users, you have an option to remove the alarm display or muting the ringing while waiting for the [`Alerts.StopAlert`](#StopAlert) directive from CIC.

### Message example
{% raw %}

```json
{
  "context": [
    {{Alerts.AlertState}}
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

Instructs a client to add an alarm or to change the specified alarm. Add an alarm or change the specified alarm, based on the following guide:

* Add an alarm **if the client has no alarm with the ID identical to the `token` field** of this directive.
* Make a change on the alarm **if the client already has an alarm with the ID identical to the `token` field** of this directive.

Report the result of executing the instruction to CIC using either one of the following events:

* [`Alerts.SetAlertSucceeded`](#SetAlertSucceeded) event: If the client has successfully added or changed the specified alarm.
* [`Alerts.SetAlertFailed`](#SetAlertFailed) event: If the client has failed to add or change the specified alarm.

### Payload fields {#SetAlertPayload}

| Field name       | Type    | Description                    | Provided |
|---------------|:---------:|-----------------------------|:---------:|
| `assets[]`         | object array | Contains a list of audio clips (TTS audio or ringtone) to play when ringing a reminder alarm or action timer. This field is provided only if the `type` value is `"REMINDER"` or `"ACTIONTIMER"`.   | Conditional |
| `assets[].assetId` | string | The ID of an audio clip. | Always |
| `assets[].url`     | string | The URL of the audio clip to play. If the value is in the `"clova://alert/bell/{alarm_type}"` format, ring the sound set for the given alarm type. Available values are:  <ul><li><code>"clova://alert/bell/reminder"</code>: Play a reminder ringtone</li></ul>    | Always |
| `assetPlayOrder[]` | string array | Defines the order for playing the TTS audio clips contained in the `assets` array. Play the audio clips in the order the `assets[].assetId` are placed in this array. This field is returned only if the `type` value is `"REMINDER"` or `"ACTIONTIMER"`.  | Conditional |
| `scheduledTime`  | string | The date and time for the alarm to ring. (Format: YYYY-MM-DDThh:mm:ssZ)   | Always |
| `token`          | string | The ID of the alarm to be added or to be changed.                     | Always |
| `type`           | string | The alarm type. Available types are: <ul><li><code>"ACTIONTIMER"</code></li><li><code>"ALARM"</code></li><li><code>"REMINDER"</code></li><li><code>"TIMER"</code></li></ul>  | Always |

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

A message for reporting to CIC that the client has failed to add or change the specified alarm. Send this event to CIC if you failed to add or change the specified alarm for the [Alerts.SetAlert](#SetAlert) directive.

### Context fields

Send the following [context information](/CIC/References/Context_Objects.md) with this event.

* [`Alerts.AlertsState`](/CIC/References/Context_Objects.md#AlertsState)

### Payload fields

| Field name       | Type    | Description                    | Required |
|---------------|:---------:|-----------------------------|:---------:|
| `token`   | string | The ID of the alarm the client has failed to add or change.               | Required |
| `type`    | string | The alarm type. Available types are: <ul><li><code>"ACTIONTIMER"</code></li><li><code>"ALARM"</code></li><li><code>"REMINDER"</code></li><li><code>"TIMER"</code></li></ul>  | Required |

### Message example

{% raw %}

```json
{
  "context": [
    {{Alerts.AlertState}}
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

A message for reporting to CIC that the client has successfully added or changed the specified alarm. Send this event when you succeed in adding or changing the specified alarm for the  [Alerts.SetAlert](#SetAlert) directive.

### Context fields

Send the following [context information](/CIC/References/Context_Objects.md) with this event.

* [`Alerts.AlertsState`](/CIC/References/Context_Objects.md#AlertsState)

### Payload fields

| Field name       | Type    | Description                    | Required |
|---------------|:---------:|-----------------------------|:---------:|
| `token`   | string | The ID of the alarm added or changed.                 | Required |
| `type`    | string | The alarm type. Available types are: <ul><li><code>"ACTIONTIMER"</code></li><li><code>"ALARM"</code></li><li><code>"REMINDER"</code></li><li><code>"TIMER"</code></li></ul>  | Required |

### Message example

{% raw %}

```json
{
  "context": [
    {{Alerts.AlertState}}
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

Instructs a client to stop the specified alarm. Stop the specified alarm and report the result to CIC with the [`AlertStopped`](#AlertStopped) event.


### Payload fields

| Field name       | Type    | Description                    | Provided |
|---------------|:---------:|-----------------------------|:---------:|
| `token`   | string | The ID of the alarm to stop.                 | Always |
| `type`    | string | The alarm type. Available types are: <ul><li><code>"ACTIONTIMER"</code></li><li><code>"ALARM"</code></li><li><code>"REMINDER"</code></li><li><code>"TIMER"</code></li></ul>  | Always |

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
