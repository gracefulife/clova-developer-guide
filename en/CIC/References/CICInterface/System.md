# System

The System namespace provides directives and events that are required when synchronizing information related to user accounts such as alarm and schedule between Clova and the client. Such synchronization is needed in the following cases:

* When a user has added another client to their account.
* When the client is reconnected to CIC due to network error or other issues.
* When the user account registered on the client has changed to a new user's.
* When the client is reset after getting disconnected from the pair app.

<div class="note">
  <p><strong>Note!</strong></p>
  <p>If the client experiences network disconnection or a user logs out from the client, you MUST delete all the information related to the user account.</p>
</div>

To synchronize information, a client sends the [`System.RequestSynchronizeState`](RequestSynchronizeState) event to CIC and CIC shares the server information with the client using the [`System.SynchronizeState`](#SynchronizeState) directive.

| Message name         | Message type  | Description                                 |
|------------------|-----------|-------------------------------------------|
| [`RequestSynchronizeState`](#RequestSynchronizeState)  | Event     | A message to notify CIC that the client needs to synchronize its data with Clova. |
| [`SynchronizeState`](#SynchronizeState)                | Directive | Instructs a client to synchronize its data with the data provided by Clova.                                |

<div class="note">
  <p><strong>Note!</strong></p>
  <p>Until further notice, the System namespace only provides an interface for synchronizing alarm details. More features are expected to be provided in the future.</p>
</div>

## RequestSynchronizeState event {#RequestSynchronizeState}

A message for reporting to CIC that the client needs to synchronize shared information stored in Clova's cloud. CIC will send the [`System.SynchronizeState`](#SynchronizeState) directive in return.

### Context fields

None

### Payload fields

None

### Message example

{% raw %}
```json
{
  "context": [],
  "event": {
    "header": {
      "namespace": "System",
      "name": "RequestSynchronizeState",
      "messageId": "b120c3e0-e6b9-4a3d-96de-71539e5f6214"
    },
    "payload": {}
  }
}
```
{% endraw %}

### See also

* [`System.SynchronizeState`](/CIC/References/CICInterface/System.md#SynchronizeState)

## SynchronizeState directive {#SynchronizeState}

Instructs a client to synchronize the data in the `payload` field. The client should modify the set value according to the data delivered from Clova.

### Payload fields

| Field name       | Type    | Description                     | Required |
|---------------|:---------:|-----------------------------|:---------:|
| `allAlerts[]`   | object array | Contains a list of alarms to synchronize. Alarm information is specified in the format used in the [`payload`](/CIC/References/CICInterface/Alerts.md#SetAlertPayload) of the [`Alerts.SetAlert`](/CIC/References/CICInterface/Alerts.md#SetAlert) directive.  | Required    |

### Remarks

Until further notice, the System namespace only provides an interface for synchronizing alarm details. More features are expected to be provided in the future.

### Message example

{% raw %}

```json
{
  "directive": {
    "header": {
      "namespace": "System",
      "name": "SynchronizeState",
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

* [`System.RequestSynchronizeState`](#RequestSynchronizeState)
