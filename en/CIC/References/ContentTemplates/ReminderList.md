# ReminderList Template

The ReminderList template is used in providing information of multiple reminders for the client to display on the client's screen.
When the user requests for a list of reminders, CIC sends the list of reminders registered by the user to the client, in the form of the ReminderList template.

<div class="note">
<p><strong>Note!</strong></p>
<p>The following is the restrictions in using reminder:</p>
<ul>
  <li>Voice requests can be used only to add a reminder or to check a list of reminders.</li>
  <li>To modify or delete a reminder, the user must use the Clova app.</li>
</ul>
</div>

## Template fields

| Field name       | Type    | Description                     |
|---------------|---------|-----------------------------|
| `reminderList[]`               | object array  | Contains a list of reminders registered by the user.                                                                                          |
| `reminderList[].content`       | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject)     | Contains the reminder message. |
| `reminderList[].repeatDay[]`     | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject) array | The repeat day(s) for a _weekly_ reminder |
| `reminderList[].repeatPeriod`  | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject)     | The repeat cycle. Available cycles are: <ul><li><code>""</code>(empty string): One-time reminder</li><li><code>"daily"</code>: Daily reminder</li><li><code>"weekly"</code>: Weekly reminder</li></ul> |
| `reminderList[].status`        | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject)     | Specifies whether the task of the reminder is completed or not. Available statuses are: <ul><li><code>"TODO"</code>: Remaining reminder</li><li><code>"DONE"</code>: Completed reminder</li></ul> |
| `reminderList[].scheduledTime` | [DateTimeObject](/CIC/References/ContentTemplates/Shared_Objects.md#DateTimeObject) | The date and time at which this reminder is to go off.  |
| `reminderList[].token`         | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject)     | The ID of this reminder.  |
| `type`                         | string                                                                              | The type of this template. The value is always `"ReminderList"`.             |

## Template example

{% raw %}

```json
{
  "type": "ReminderList",
  "reminderList": [
    {
      "token": {
        "type": "string",
        "value": "072c72b9-cfc5-4127-b4fe-557a10457232"
      },
      "scheduledTime": {
        "type": "datetime",
        "value": "2017-10-01T14:00:00Z"
      },
      "content": {
        "type": "string",
        "value": "Charge my LINE points"
      }
    },
    {
      "token": {
        "type": "string",
        "value": "b5403bd0-1598-495b-a466-9385c2b1103a"
      },
      "scheduledTime": {
        "type": "datetime",
        "value": "2017-10-01T11:30:00Z"
      },
      "content": {
        "type": "string",
        "value": "Watch LINE LIVE"
      }
    }
  ]
}
```

{% endraw %}

## UI example {#UIExample}

<div class="note">
<p><strong>Note!</strong></p>
<p>An example for the ReminderList template is in preparation.</p>
</div>

## See also
* [Alerts](/CIC/References/CICInterface/Alerts.md) Interface
* [Reminder](/CIC/References/ContentTemplates/Reminder.md)
