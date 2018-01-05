# Schedule Template

The Schedule template is used in providing schedule information for the client to display on the client's screen.
When the user creates a schedule on the calendar, CIC sends the schedule information to the client, in the form of the Schedule template.

<div class="note">
<p><strong>Note!</strong></p>
<p>The following is the restrictions in using schedule:</p>
<ul>
  <li>To register, modify or delete the account for calendar, the user must use the Clova app.</li>
  <li>Voice requests can be used only to add a schedule or to check a list of schedules.</li>
  <li>To modify or delete a schedule, the user must use the Clova app.</li>
</ul>
</div>

## Template fields

| Field name       | Type    | Description                     |
|---------------|---------|-----------------------------|
| `content`       | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject)     | Contains the schedule message. |
| `end`           | [DateTimeObject](/CIC/References/ContentTemplates/Shared_Objects.md#DateTimeObject) or [DateObject](/CIC/References/ContentTemplates/Shared_Objects.md#DateObject)  | The end date and time of this schedule. If `DateObject` is used, this schedule is an _all-day_ schedule. |
| `start`         | [DateTimeObject](/CIC/References/ContentTemplates/Shared_Objects.md#DateTimeObject) or [DateObject](/CIC/References/ContentTemplates/Shared_Objects.md#DateObject)  | The start date and time of this schedule. If `DateObject` is used, this schedule is an _all-day_ schedule.  |
| `repeatDay[]`     | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject) array | The repeat day(s) for a _weekly_ schedule.  |
| `repeatPeriod`  | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject)     | The repeat cycle. Available cycles are: <ul><li><code>""</code> (empty string): One-time schedule </li><li><code>"daily"</code>: Daily schedule</li><li><code>"weekly"</code>: Weekly schedule</li></ul> |
| `token`         | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject)     | The ID of the schedule.  |
| `type`          | string                                                                              | The type of this template. The value is always `"Schedule"`.             |

## Template example

{% raw %}

```json
// One-time schedule
{
  "type": "Schedule",
  "token": {
    "type": "string",
    "value": "072c72b9-cfc5-4127-b4fe-557a10457232"
  },
  "start": {
    "type": "datetime",
    "dateTime": "2017-09-30T12:00:00+09:00"
  },
  "end": {
    "type": "datetime",
    "dateTime": "2017-09-30T13:00:00+09:00"
  },
  "content": {
    "type": "string",
    "value": "Moon's wedding"
  },
  "repeatPeriod": {
    "type": "string",
    "value": ""
  },
  "repeatDay": []
}

// Daily schedule
{
  "type": "Schedule",
  "token": {
    "type": "string",
    "value": "b5403bd0-1598-495b-a466-9385c2b1103a"
  },
  "start": {
    "type": "datetime",
    "dateTime": "2017-08-02T10:00:00+09:00"
  },
  "end": {
    "type": "datetime",
    "dateTime": "2017-08-02T11:00:00+09:00"
  },
  "content": {
    "type": "string",
    "value": "Daily scrum"
  },
  "repeatPeriod": {
    "type": "string",
    "value": "daily"
  },
  "repeatDay": []
}

// Weekly schedule
{
  "type": "Schedule",
  "token": {
    "type": "string",
    "value": "da740e2a-01cd-4f2e-aedf-6c4285bae785"
  },
  "start": {
    "type": "datetime",
    "dateTime": "2017-08-02T10:00:00+09:00"
  },
  "end": {
    "type": "datetime",
    "dateTime": "2017-08-02T11:00:00+09:00"
  },
  "content": {
    "type": "string",
    "value": "Weekly meeting"
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
  ]
}

// All-day schedule
{
  "type": "Schedule",
  "token": {
    "type": "string",
    "value": "5c8b4f7b-d8bd-4817-a1c3-eb9c9522277e"
  },
  "start": {
    "type": "date",
    "dateTime": "2017-09-29"
  },
  "end": {
    "type": "datetime",
    "dateTime": "2017-09-29"
  },
  "content": {
    "type": "string",
    "value": "LINE DEVELOPER DAY"
  },
  "repeatPeriod": {
    "type": "string",
    "value": ""
  },
  "repeatDay": []
}
```

{% endraw %}

## UI example {#UIExample}

<div class="note">
<p><strong>Note!</strong></p>
<p>An example for the Schedule template is in preparation.</p>
</div>

## See also

* [Alerts](/CIC/References/CICInterface/Alerts.md) Interface
* [ScheduleList](/CIC/References/ContentTemplates/ScheduleList.md)
