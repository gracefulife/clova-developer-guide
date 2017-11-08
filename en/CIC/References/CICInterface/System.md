# System

The system provides directive messages and event messages that are required when synchronizing information between Clova and the client. To synchronize information, client will send a ['System.RequestSynchronizeState'](RequestSynchronizeState) event message to CIC and CIC will share the server information to the client using a [`System.SynchronizeState`](#SynchronizeState) directive message.

| Message name         | Message type  | Message description                                 |
|------------------|-----------|-------------------------------------------|
| [`RequestSynchronizeState`](#RequestSynchronizeState)  | Event     | Send this event message to CIC when the client needs to synchronize shared information stored in Clova's cloud environment. |
| [`SynchronizeState`](#SynchronizeState)                | Directive | Instructs your client to synchronize the data in `payload` field.  |


<div class="note">
  <p><strong>Note!</strong></p>
  <p>Currently, the system namespace is used to synchronize alarm details added by the user. The number of synchronized information may increase in the future. </p>
</div>

## RequestSynchronizeState event {#RequestSynchronizeState}
Send this event message to CIC when the client needs to synchronize shared information stored in Clova's cloud environment. CIC will pass a [`System.SynchronizeState`](#SynchronizeState) directive message to the client upon receiving the event message.

### Context field

There is no required state information

### Payload field

None

### Message example
{% raw %}
```json
{
  "context":[],
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
Instructs your client to synchronize the data in `payload` field. The client should modify the set value according to the data delivered from Clova.

### Payload field

| Field name       | Type    | Field description                     | Required |
|---------------|---------|-----------------------------|---------|
| `allAlerts`   | [AlertObject] array | An object array containing a list of alarm that the client should synchronize. It has the same format as `payload` object used for a [`Alerts.SetAlert`](/CIC/References/CICInterface/Alerts.md#SetAlert) directive message.  | Yes    |

### Remarks
Currently, the system namespace is used to synchronize alarm details added by the user. The number of synchronized information may increase in the future.

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
              "url": "http://abc.de.fe/tts1"
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
