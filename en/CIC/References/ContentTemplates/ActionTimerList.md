# ActionTimerList Template
When the user request for a list of action timer, CIC passes the actiontimer list registered to the user in ActionTimerList template format to the client. The client should display the actiontimer list registered by the user on the screen using the received template.

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
| `actionTimerList[]`               | object array  | An object array containing the action timer list registered by the user.                                         |
| `actionTimerList[].action`       | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject)     | An object containing an action set by the user on the action timer. **Empty string(`""`) is being entered for now. The field is reserved for an extension in the future.** |
| `actionTimerList[].repeatDay`     | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject) array | An object array containing date information if it is a weekly repeated action timer |
| `actionTimerList[].repeatPeriod`  | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject)     | An object containing a repeated cycle. The `value` field of the object has the following values. <ul><li>Empty string(<code>""</code>) : One-time action timer</li><li><code>"daily"</code> : Daily repeated action timer</li><li><code>"weekly"</code> : Every week repeated action timer</li></ul> |
| `actionTimerList[].scheduledTime` | [DateTimeObject](/CIC/References/ContentTemplates/Shared_Objects.md#DateTimeObject) | An object containing date and time of when the action timer will ring      |
| `actionTimerList[].token`         | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject)     | An object containing identifier of an action timer.              |
| `type`        | string                                                                                                | A content template delimiter. It has an `"ActionTimerList"` value.             |

## Template example

{% raw %}

```json
{
  "type": "ActionTimerList",
  "actionTimerList": [
    {
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
    },
    {
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
    },
    {
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
  ]
}
```

{% endraw %}

## Screen UI example {#UIExample}

<div class="note">
<p><strong>Note!</strong></p>
<p>Preparing for an example of a screen which applied an ActionTimerList template.</p>
</div>

## See also
* [ActionTimer](/CIC/References/ContentTemplates/ActionTimer.md)
* [Alerts](/CIC/References/CICInterface/Alerts.md) Interface