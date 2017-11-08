# Alarm Template
When the user creates an alarm, CIC passes the alarm detail in Alarm template format to the client. The client should display the alarm details on the screen using the received template.

<div class="note">
<p><strong>Note!</strong></p>
<p>Currently, there are limits to the Alarm template as below.</p>
<ul>
  <li>With the voice command, the user can only request to add an alarm or to check the list.</li>
  <li>In order to modify or delete an alarm, the user should use the Clova app.</li>
</ul>
</div>

## Template field

| Field name       | Type    | Field description                     |
|---------------|---------|-----------------------------|
| `repeatDay`     | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject) array | An object array containing repeated date information if it is a weekly repeated alarm. |
| `repeatPeriod`  | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject)     | An object containing a repeated cycle. The `value` field of the object has the following values. <ul><li>Empty string(<code>""</code>) : One-time alarm </li><li><code>"daily"</code> : Daily repeated alarm</li><li><code>"weekly"</code> : Every week repeated alarm</li></ul> |
| `scheduledTime` | [DateTimeObject](/CIC/References/ContentTemplates/Shared_Objects.md#DateTimeObject) | An object containing date and time of when the alarm will ring.  |
| `type`        | string                                                                              | A content template delimiter. It has an `"Alarm"` value.             |

## Template Example

{% raw %}

```json

// One-time alarm
{
  "type": "Alarm",
  "scheduledTime": {
    "type": "datetime",
    "value": "2017-10-09T09:00:00Z"
  },
  "repeatPeriod": {
    "type": "string",
    "value": ""
  },
  "repeatDay": []
}

// Daily repeated alarm
{
  "type": "Alarm",
  "scheduledTime": {
    "type": "datetime",
    "value": "2017-10-09T09:00:00Z"
  },
  "repeatPeriod": {
    "type": "string",
    "value": "daily"
  },
  "repeatDay": []
}

// Every week repeated alarm
{
  "type": "Alarm",
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
  ]
}
```

{% endraw %}

## Screen UI example {#UIExample}

<div>
<p><strong>Note!</strong></p>
<p>Preparing for an example of a screen which applied an Alarm template.</p>
</div>

## See also
* [AlarmList](/CIC/References/ContentTemplates/AlarmList.md)
* [Alerts](/CIC/References/CICInterface/Alerts.md) Interface
