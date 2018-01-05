# Reminder Template

The Reminder template is used in providing reminder information for the client to display on the client's screen.
When the user creates a reminder, CIC sends the reminder information to the client, in the form of the Reminder template.

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
| `content`       | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject)     | Contains the reminder message. |
| `repeatDay`     | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject) array | The repeat day(s) for a _weekly_ reminder. |
| `repeatPeriod`  | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject)     | The repeat cycle. Available cycles are: <ul><li><code>""</code> (empty string): One-time reminder</li><li><code>"daily"</code>: Daily reminder</li><li><code>"weekly"</code>: Weekly reminder</li></ul> |
| `status`        | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject)     | Specifies whether the task of the reminder is completed or not. Available statuses are: <ul><li><code>"TODO"</code>: Remaining reminder</li><li><code>"DONE"</code>: Completed reminder</li></ul> |
| `scheduledTime` | [DateTimeObject](/CIC/References/ContentTemplates/Shared_Objects.md#DateTimeObject) | The date and time at which this reminder is to go off. |
| `token`         | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject)     | The ID of this reminder. |
| `type`          | string                                                                              | The type of this template. It has an `"Reminder"` value.  |

## Template example

{% raw %}

```json
// One-time reminder
{
  "type": "Reminder",
  "token": {
    "type": "string",
    "value": "072c72b9-cfc5-4127-b4fe-557a10457232"
  },
  "scheduledTime": {
    "type": "datetime",
    "value": "2017-10-09T09:00:00Z"
  },
  "repeatPeriod": {
    "type": "string",
    "value": ""
  },
  "repeatDay": [],
  "content": {
    "type": "string",
    "value": "Charge my LINE points"
  },
  "status": {
    "type": "string",
    "value": "DONE"
  }
}

// Daily reminder
{
  "type": "Reminder",
  "token": {
    "type": "string",
    "value": "b5403bd0-1598-495b-a466-9385c2b1103a"
  },
  "scheduledTime": {
    "type": "datetime",
    "value": "2017-10-09T09:00:00Z"
  },
  "repeatPeriod": {
    "type": "string",
    "value": "daily"
  },
  "repeatDay": [],
  "content": {
    "type": "string",
    "value": "Update my LINE Timeline"
  },
  "status": {
    "type": "string",
    "value": "TODO"
  }
}

// Weekly reminder
{
  "type": "Reminder",
  "token": {
    "type": "string",
    "value": "da740e2a-01cd-4f2e-aedf-6c4285bae785"
  },
  "scheduledTime": {
    "type": "datetime",
    "value": "2017-10-09T09:00:00Z"
  },
  "repeatPeriod": {
    "type": "string",
    "value": "weekly"
  },
  "repeatDay": [
    {
      "type": "string",
      "value": "monday"
    }
  ],
  "content": {
    "type": "string",
    "value": "Check the latest stickers on LINE STORE"
  },
  "status": {
    "type": "string",
    "value": "TODO"
  }
}

```

{% endraw %}

## UI example {#UIExample}

<div class="note">
<p><strong>Note!</strong></p>
<p>An example for the Reminder template is in preparation.</p>
</div>

## See also

* [Alerts](/CIC/References/CICInterface/Alerts.md) Interface
* [ReminderList](/CIC/References/ContentTemplates/ReminderList.md)
