# Schedule Template
When the user creates a schedule on the calendar, CIC passes the schedule detail in Schedule template format to the client. The client should display the schedule details on the screen using the received template.

<div class="note">
<p><strong>Note!</strong></p>
<p>Currently, there are limits to the Schedule template as below.</p>
<ul>
  <li>In order to create, modify, delete a calendar account, the user should use the Clova app.</li>
  <li>With the voice command, the user can only request to add a calendar schedule or to check the list.</li>
  <li>In order to modify or delete a calendar schedule, the user should use the Clova app.</li>
</ul>
</div>

## Template field

| Field name       | Type    | Field description                     |
|---------------|---------|-----------------------------|
| `content`       | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject)     | An object containing contents of an added schedule entered by the user. |
| `end`           | [DateTimeObject](/CIC/References/ContentTemplates/Shared_Objects.md#DateTimeObject) or [DateObject](/CIC/References/ContentTemplates/Shared_Objects.md#DateObject)  | Termination date and time of the added schedule. In case of all day schedule, it is in DateObject format type with date information only. |
| `start`         | [DateTimeObject](/CIC/References/ContentTemplates/Shared_Objects.md#DateTimeObject) or [DateObject](/CIC/References/ContentTemplates/Shared_Objects.md#DateObject)  | Starting date and time of the added schedule. In case of all day schedule, it is in DateObject format type with date information only. |
| `repeatDay`     | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject) array | An object array containing repeated date information if it is a weekly repeated alarm. |
| `repeatPeriod`  | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject)     | An object containing repeat cycle. The `value` field of the object has the following values. <ul><li>Empty string(<code>""</code>) : One-time schedule </li><li><code>"daily"</code> : Daily repeated schedule</li><li><code>"weekly"</code> : Every week repeated schedule</li></ul> |
| `type`        | string                                                                              | A content template delimiter. The value is always `"Schedule"`.             |

## Template Example

{% raw %}

```json
// One-time schedule
{
  "type": "Schedule",
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
    "value": "친구 결혼식"
  },
  "repeatPeriod": {
    "type": "string",
    "value": ""
  },
  "repeatDay": []
}

// Daily repeated schedule
{
  "type": "Schedule",
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
    "value": "데일리 스크럼"
  },
  "repeatPeriod": {
    "type": "string",
    "value": "daily"
  },
  "repeatDay": []
}

// Every week repeated schedule
{
  "type": "Schedule",
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
    "value": "주간 회의"
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

// All day schedule
{
  "type": "Schedule",
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
    "value": "플레이숍"
  },
  "repeatPeriod": {
    "type": "string",
    "value": ""
  },
  "repeatDay": []
}
```

{% endraw %}

## Screen UI example {#UIExample}

<div>
<p><strong>Note!</strong></p>
<p>Preparing for an example of a screen which applied a Schedule template.</p>
</div>

## See also
* [Alerts](/CIC/References/CICInterface/Alerts.md) Interface
* [ScheduleList](/CIC/References/ContentTemplates/ScheduleList.md)
