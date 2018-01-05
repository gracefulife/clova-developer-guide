# AlarmList Template

The AlarmList template is used in providing information of multiple alarms for the client to display on the client's screen.
When the user requests for a list of alarms, CIC sends the list of alarms registered by the user to the client, in the form of the AlarmList template.

<div class="note">
<p><strong>Note!</strong></p>
<p>The following is the restrictions in using alarm:</p>
<ul>
  <li>Voice requests can be used only to add an alarm or to check a list of alarms.</li>
  <li>To modify or delete an alarm, the user must use the Clova app.</li>
</ul>
</div>

## Template fields

| Field name       | Type    | Description                     |
|---------------|---------|-----------------------------|
| `alarmList[]`               | object array  | Contains a list of alarms registered by the user.                                                                                          |
| `alarmList[].repeatDay`     | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject) array | The repeat day(s) for a _weekly_ alarm.  |
| `alarmList[].repeatPeriod`  | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject)     | The repeat cycle. Available cycles are: <ul><li><code>""</code>(Empty string): One-time alarm</li><li><code>"daily"</code>: Daily  alarm</li><li><code>"weekly"</code>: Weekly alarm</li></ul> |
| `alarmList[].scheduledTime` | [DateTimeObject](/CIC/References/ContentTemplates/Shared_Objects.md#DateTimeObject) | The date and time at which this alarm is to ring.                      |
| `alarmList[].token`         | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject)     | The ID of this alarm.                               |
| `type`                      | string                                                                              | The type of this template. The value is always `"AlarmList"`.             |

## Template example

{% raw %}

```json
{
  "type": "AlarmList",
  "alarmList": [
    {
      "token": {
        "type": "string",
        "value": "072c72b9-cfc5-4127-b4fe-557a10457232"
      },
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
      "token": {
        "type": "string",
        "value": "b5403bd0-1598-495b-a466-9385c2b1103a"
      },
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
      "token": {
        "type": "string",
        "value": "da740e2a-01cd-4f2e-aedf-6c4285bae785"
      },
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

## UI example {#UIExample}

<div class="note">
<p><strong>Note!</strong></p>
<p>An example for the AlarmList template is in preparation.</p>
</div>

## See also
* [Alarm](/CIC/References/ContentTemplates/Alarm.md)
* [Alerts](/CIC/References/CICInterface/Alerts.md) Interface
