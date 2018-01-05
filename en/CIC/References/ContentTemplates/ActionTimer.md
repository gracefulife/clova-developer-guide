# ActionTimer Template

The ActionTimer template is used in providing action timer information for the client to display on the client's screen.
When the user creates an action timer, CIC sends the action timer information to the client, in the form of the ActionTimer template.

<div class="note">
<p><strong>Note!</strong></p>
<p>The following is the restrictions in using action timers:</p>
<ul>
  <li>Voice requests can be used only to add an action timer or to check a list of action timers.</li>
  <li>To modify or delete an action timer, the user must use the Clova app.</li>
</ul>
</div>

## Template fields

| Field name       | Type    | Description                     |
|---------------|---------|-----------------------------|
| `action`       | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject)      | The action the user has set on this action timer. **The value is always an empty string(`""`). This field is reserved for future extension.** |
| `repeatDay[]`     | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject) array | The repeat day(s) for a _weekly_ action timer. |
| `repeatPeriod`  | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject)     | The repeat cycle for this action timer. Available cycles are: <ul><li><code>""</code>(Empty string): One-time action timer</li><li><code>"daily"</code>: Daily action timer</li><li><code>"weekly"</code>: Weekly action timer</li></ul> |
| `scheduledTime` | [DateTimeObject](/CIC/References/ContentTemplates/Shared_Objects.md#DateTimeObject) | The date and time at which this action timer is to go off.      |
| `token`         | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject)     | The ID of this action timer.   |
| `type`          | string                                                                              | The type of this template. The value is always `"ActionTimer"`.  |

## Template example

{% raw %}

```json
// One-time action timer
{
  "type": "ActionTimer",
  "token": {
    "type": "string",
    "value": "072c72b9-cfc5-4127-b4fe-557a10457232"
  },
  "scheduledTime": {
    "type": "datetime",
    "value": "2017-10-01T14:00:00Z"
  },
  "action": {
    "type": "string",
    "value": ""
  },
  "repeatPeriod": {
    "type": "string",
    "value": ""
  },
  "repeatDay": []
}

// Daily action timer
{
  "type": "ActionTimer",
  "token": {
    "type": "string",
    "value": "b5403bd0-1598-495b-a466-9385c2b1103a"
  },
  "scheduledTime": {
    "type": "datetime",
    "value": "2017-10-02T09:00:00Z"
  },
  "action": {
    "type": "string",
    "value": ""
  },
  "repeatPeriod": {
    "type": "string",
    "value": "daily"
  },
  "repeatDay": []
}

// Weekly action timer
{
  "type": "ActionTimer",
  "token": {
    "type": "string",
    "value": "da740e2a-01cd-4f2e-aedf-6c4285bae785"
  },
  "scheduledTime": {
    "type": "datetime",
    "value": "2017-10-03T11:00:00Z"
  },
  "action": {
    "type": "string",
    "value": ""
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

## UI example {#UIExample}

<div class="note">
<p><strong>Note!</strong></p>
<p>An example for the ActionTimer template is in preparation.</p>
</div>

## See also

* [ActionTimerList](/CIC/References/ContentTemplates/ActionTimerList.md)
* [Alerts](/CIC/References/CICInterface/Alerts.md) Interface
