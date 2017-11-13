# ReminderList Template
When the user requests for a list of reminder, CIC passes the reminder list registered to the user in ReminderList template format to the client. The client should display the reminder list registered by the user on the screen using the received template.

<div class="note">
<p><strong>Note!</strong></p>
<p>Currently, there are limits to the ReminderList template as below.</p>
<ul>
  <li>With the voice command, the user can only request to add a reminder or to check the list.</li>
  <li>In order to modify or delete a reminder, the user should use the Clova app.</li>
</ul>
</div>

## Template field

| Field name       | Type    | Field description                     |
|---------------|---------|-----------------------------|
| `reminderList[]`               | object array  | An object array containing the reminder list registered by the user.                                                                                          |
| `reminderList[].content`       | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject)     | An object containing contents of the reminder entered by the user. |
| `reminderList[].repeatDay`     | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject) array | An object array containing repeated date information if it is a weekly repeated reminder. |
| `reminderList[].repeatPeriod`  | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject)     | An object containing a repeated cycle. The `value` field of the object has the following values. <ul><li>Empty string(<code>""</code>) : One-time reminder</li><li><code>"daily"</code> : Daily repeated reminder</li><li><code>"weekly"</code> : Every week repeated reminder</li></ul> |
| `reminderList[].status`        | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject)     | An object displaying a process of the reminder. The `value` field of the object has the following values. <ul><li><code>"TODO"</code> : An unfinished reminder</li><li><code>"DONE"</code> : A finished reminder</li></ul> |
| `reminderList[].scheduledTime` | [DateTimeObject](/CIC/References/ContentTemplates/Shared_Objects.md#DateTimeObject) | An object containing date and time of when the reminder will ring.      |
| `type`        | string                                                                                                | A content template delimiter. It has an `"ReminderList"` value.             |

## Template Example

{% raw %}

```json
{
  "type": "ReminderList",
  "reminderList": [
    {
      "scheduledTime": {
        "type": "datetime",
        "value": "2017-10-01T14:00:00Z"
      },
      "content": {
        "type": "string",
        "value": "입금하기"
      }
    },
    {
      "scheduledTime": {
        "type": "datetime",
        "value": "2017-10-01T14:00:00Z"
      },
      "content": {
        "type": "string",
        "value": "소개팅 준비"
      }
    }
  ]
}
```

{% endraw %}

## Screen UI example {#UIExample}

<div>
<p><strong>Note!</strong></p>
<p>Preparing for an example of a screen which applied a ReminderList template.</p>
</div>

## See also
* [Alerts](/CIC/References/CICInterface/Alerts.md) Interface
* [Reminder](/CIC/References/ContentTemplates/Reminder.md)
