# Reminder Template
When the user creates a reminder, CIC passes the reminder detail in Reminder template format to the client. The client should display the reminder details on the screen using the received template.

<div class="note">
<p><strong>Note!</strong></p>
<p>Currently, there are limits to the Reminder template as below.</p>
<ul>
  <li>With the voice command, the user can only request to add a reminder and check the list.</li>
  <li>In order to modify or delete a reminder, the user should use the Clova app.</li>
</ul>
</div>

## Template field

| Field name       | Type    | Field description                     |
|---------------|---------|-----------------------------|
| `content`       | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject)     | An object containing contents of the added reminder entered by the user |
| `repeatDay`     | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject) array | An object array containing repeated date information if it is a weekly repeated reminder |
| `repeatPeriod`  | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject)     | An object containing a repeated cycle. The `value` field of the object has the following values. <ul><li>Empty string(<code>""</code>) : One-time reminder</li><li><code>"daily"</code> : Daily repeated reminder</li><li><code>"weekly"</code> : Every week repeated reminder</li></ul> |
| `status`        | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject)     | An object displaying process of a reminder. The `value` field of the object has the following values. <ul><li><code>"TODO"</code> : An undone reminder</li><li><code>"DONE"</code> : A done reminder</li></ul> |
| `scheduledTime` | [DateTimeObject](/CIC/References/ContentTemplates/Shared_Objects.md#DateTimeObject) | An object containing date and time of when the reminder will ring      |
| `token`         | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject)     | An object containing identifier of an added reminder.  |
| `type`          | string                                                                              | A content template delimiter. It has an `"Reminder"` value.  |

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
    "value": "입금하기"
  },
  "status": {
    "type": "string",
    "value": "DONE"
  }
}

// Daily repeated reminder
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
    "value": "비타민 먹기"
  },
  "status": {
    "type": "string",
    "value": "TODO"
  }
}

// Every week repeated reminder
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
    "value": "청소하기"
  },
  "status": {
    "type": "string",
    "value": "TODO"
  }
}

```

{% endraw %}

## Screen UI example {#UIExample}

<div class="note">
<p><strong>Note!</strong></p>
<p>Preparing for an example of a screen which applied a Reminder template.</p>
</div>

## See also
* [Alerts](/CIC/References/CICInterface/Alerts.md) Interface
* [ReminderList](/CIC/References/ContentTemplates/ReminderList.md)
