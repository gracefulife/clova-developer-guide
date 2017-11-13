# AlarmList Template
When the user requests for a list of alarm, CIC passes the alarm list registered to the user in AlarmList template format to the client. The client should display the alarm list registered by the user on the screen using the received template.

<div class="note">
<p><strong>Note!</strong></p>
<p>Currently, there are limits to the AlarmList template as below.</p>
<ul>
  <li>With the voice command, the user can only request to add an alarm or to check the list.</li>
  <li>In order to modify or delete an alarm, the user should use the Clova app.</li>
</ul>
</div>

## Template field

| Field name       | Type    | Field description                     |
|---------------|---------|-----------------------------|
| `alarmList[]`               | object array  | An object array containing the alarm list registered by the user.                                                                                          |
| `alarmList[].repeatDay`     | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject) array | An object array containing repeated date information if it is a weekly repeated alarm. |     |
| `alarmList[].repeatPeriod`  | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject)     | An object containing repeat cycle. The `value` field of the object has the following values. <ul><li>Empty string(<code>""</code>) : One-time alarm</li><li><code>"daily"</code> : Daily repeated alarm</li><li><code>"weekly"</code> : Every week repeated alarm</li></ul> |
| `alarmListList[].scheduledTime` | [DateTimeObject](/CIC/References/ContentTemplates/Shared_Objects.md#DateTimeObject) | An object containing date and time of when the alarm will ring.                       |
| `type`        | string                                                                                                | A content template delimiter. The value is always `"AlarmList"`.             |

## Template Example

{% raw %}

```json
{
  "type": "AlarmList",
  "alarmList": [
    {
      "scheduledTime": {
        "type": "datetime",
        "value": "2017-12-23T13:00:00Z"
      },
      "repeatPeriod": {
        "type": "string",
        "value": ""
      },
      "repeatDay": []
    },
    {
      "scheduledTime": {
        "type": "datetime",
        "value": "2017-12-24T00:00:00Z"
      },
      "repeatPeriod": {
        "type": "string",
        "value": "daily"
      },
      "repeatDay": []
    },
    {
      "scheduledTime": {
        "type": "datetime",
        "value": "2017-12-25T01:00:00Z"
      },
      "repeatPeriod": {
        "type": "string",
        "value": "weekly"
      },
      "repeatDay": [
        {
          "type": "string",
          "value": "saturday"
        },
        {
          "type": "string",
          "value": "sunday"
        }
      ]
    }
  ]
}
```

{% endraw %}

## Screen UI example {#UIExample}

<div>
<p><strong>Note!</strong></p>
<p>Preparing for an example of a screen which applied an AlarmList template.</p>
</div>

## See also
* [Alarm](/CIC/References/ContentTemplates/Alarm.md)
* [Alerts](/CIC/References/CICInterface/Alerts.md) Interface
