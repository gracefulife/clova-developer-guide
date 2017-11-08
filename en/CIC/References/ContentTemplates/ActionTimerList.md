# ActionTimerList Template
When the user requests for a list of action timer, CIC passes the action timer list registered to the user in action timerList template format to the client. The client should display the action timer list registered by the user on the screen using the received template.

<div class="note">
<p><strong>Note!</strong></p>
<p>Currently, there are limits to the ActionTimerList template as below.</p>
<ul>
  <li>With the voice command, the user can only request to add an action timer or to check the list.</li>
  <li>In order to modify or delete an action timer, the user should use the Clova app.</li>
</ul>
</div>

## Template field

| Field name       | Type    | Field description                     |
|---------------|---------|-----------------------------|
| `actionTimerList[]`               | object array  | An object array containing the action timer list registered by the user.                                          |
| `actionTimerList[].action`       | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject)     | An object containing an action set by the user on the action timer. **An empty string(`""`) is entered for now. The field is reserved for an extension in the future.** |
| `actionTimerList[].repeatDay`     | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject) array | An object array containing date information if it is a weekly repeated action timer. |
| `actionTimerList[].repeatPeriod`  | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject)     | An object containing repeat cycle. The `value` field of the object has the following values. <ul><li>Empty string(<code>""</code>) : One-time action timer</li><li><code>"daily"</code> : Daily repeated actiontimer</li><li><code>"weekly"</code> : Every week repeated action timer</li></ul> |
| `actionTimerList[].scheduledTime` | [DateTimeObject](/CIC/References/ContentTemplates/Shared_Objects.md#DateTimeObject) | An object containing date and time of when the action timer will ring      |
| `type`        | string                                                                                                | A content template delimiter. It has an `"ActionTimerList"` value.             |

## Template Example

{% raw %}

```json
{
  "type": "ActionTimerList",
  "actionTimerList": [
    {
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
    },
    {
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
    },
    {
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
  ]
}
```

{% endraw %}

## Screen UI example {#UIExample}

<div>
<p><strong>Note!</strong></p>
<p>Preparing for an example of a screen which applied an ActionTimerList template.</p>
</div>

## See also
* [ActionTimer](/CIC/References/ContentTemplates/ActionTimer.md)
* [Alerts](/CIC/References/CICInterface/Alerts.md) Interface
