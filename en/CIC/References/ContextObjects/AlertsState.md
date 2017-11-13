## Alerts.AlertsState {#AlertsState}
`Alerts.AlertsState` is a message format applied to report the alarm information of the client to CIC.

<div class="danger">
  <p><strong>Deprecated!</strong></p>
  <p>Input the alarm information exactly as it is sent from the <a href="/CIC/References/CICInterface/Alerts.html">Alerts</a> directive message when writing the context information. </p>
</div>

### Message structure
{% raw %}

```json
{
  "header": {
    "namespace": "Alerts",
    "name": "AlertsState"
  },
  "payload": {
    "allAlerts": [
      {
        "token": "{{string}}",
        "type": "{{string}}",
        "scheduledTime": "{{string}}"
      },
      {
        "token": "{{string}}",
        "type": "{{string}}",
        "scheduledTime": "{{string}}"
      }
    ],
    "activeAlerts": [
      {
        "token": "{{string}}",
        "type": "{{string}}",
        "scheduledTime": "{{string}}"
      }
    ]
  }
}
```

{% endraw %}


### Payload field

| Field name       | Type    | Field description                     | Required |
|---------------|---------|-----------------------------|---------|
| `allAlerts`    | [AlertObject](#AlertObject) | An object array containing a list of all alarms set on the client. Enter all alarm information set on the client on this array.     | Yes |
| `activeAlerts` | [AlertObject](#AlertObject) | An object array containing a list of alarms currently ringing on the client. Input an empty array if there is no alarm ringing.   | Yes |

### Message example

{% raw %}

```json
{
  "context": [
    {
      "header": {
        "namespace": "Alerts",
        "name": "AlertsState"
      },
      "payload": {
        "allAlerts": [
          {
            "token": "78434957-c0db-47d9-9104-3d7899df3d4e",
            "type": "ALARM",
            "scheduledTime": "2017-09-23T11:11:11Z"
          },
          {
            "token": "26346794-0a23-446a-a34f-a0f5d957bd88",
            "type": "TIMER",
            "scheduledTime": "2017-09-14T22:22:22Z"
          },
          {
            "token": "5b3eb1a0-3a98-43ca-b28b-040462c2d2c9",
            "type": "ALARM",
            "scheduledTime": "2017-09-16T12:33:44Z"
          }
        ],
        "activeAlerts": [
          {
            "token": "5b3eb1a0-3a98-43ca-b28b-040462c2d2c9",
            "type": "ALARM",
            "scheduledTime": "2017-09-16T12:33:44Z"
          }
        ]
      }
    }
  ],
  "event": {
    "header": {
      "namespace": "Alerts",
      "name": "AlertStopped",
      "messageId": "b19028a9-e566-4ad9-90c0-4c5fecc9b336",
      "dialogRequestId": "862f996c-69cc-4e53-94df-9aed82b23579"
    },
    "payload": {
      "token": "26346794-0a23-446a-a34f-a0f5d957bd88",
      "type": "TIMER",
      "scheduledTime": "2017-09-14T22:22:22Z"
    }
  }
}
```

{% endraw %}

### AlertObject {#AlertObject}
An object containing an individual alarm. Input the individual alarm details according to the object format.

#### Object field

| Field name       | Type    | Field description                     | Required |
|---------------|---------|-----------------------------|---------|
| `scheduledTime` | string | Date and time when the alarm will ring (YYYY-MM-DDThh:mm:ssZ format)   | Yes |
| `token`         | string | Identifier of the alarms.                   | Yes |
| `type`          | string | Types of alarm. Available values are: <ul><li><code>ACTIONTIMER</code></li><li><code>"ALARM"</code></li><li><code>"REMINDER"</code></li><li><code>TIMER</code></li></ul>  | Yes |

#### Object example

{% raw %}

```json
Example 1 : ALARM type
{
  "token": "5b3eb1a0-3a98-43ca-b28b-040462c2d2c9",
  "type": "ALARM",
  "scheduledTime": "2017-09-16T12:33:44Z"
}

Example 2 : TIMER type
{
  "token": "26346794-0a23-446a-a34f-a0f5d957bd88",
  "type": "TIMER",
  "scheduledTime": "2017-09-14T22:22:22Z"
}

Example 3 : REMINDER type
{
  "token": "26346794-0a23-446a-a34f-a0f5d957bd88",
  "type": "TIMER",
  "scheduledTime": "2017-09-14T22:22:22Z"
}

```

{% endraw %}

### See also
* [`Alerts`](/CIC/References/CICInterface/Alerts.md)
