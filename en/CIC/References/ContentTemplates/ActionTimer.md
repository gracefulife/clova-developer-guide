# ActionTimer Template
When the user creates an action timer, CIC passes the action timer details in ActionTimer template format to the client. The client should display the action timer details on the screen using the received template.

<div class="note">
<p><strong>Note!</strong></p>
<p>Currently, there are limits to the ActionTimer template as below.</p>
<ul>
  <li>With the voice command, the user can only request to add an action timer or to check the list.</li>
  <li>In order to modify or delete an action timer, the user should use the Clova app.</li>
</ul>
</div>

## Template field

| Field name       | Type    | Field description                     |
|---------------|---------|-----------------------------|
| `action`       | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject)      | An object containing an action set by the user on the added action timer. **Empty string(`""`) is being entered for now. The field is reserved for an extension in the future.** |
| `repeatDay`     | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject) array | An object array containing date information if it is a weekly repeated action timer |
| `repeatPeriod`  | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject)     | An object containing a repeated cycle. The `value` field of the object has the following values. <ul><li>Empty string(<code>""</code>) : One-time action timer</li><li><code>"daily"</code> : Daily repeated action timer</li><li><code>"weekly"</code> : Every week repeated action timer</li></ul> |
| `scheduledTime` | [DateTimeObject](/CIC/References/ContentTemplates/Shared_Objects.md#DateTimeObject) | An object containing date and time of when the action timer will ring      |
| `token`         | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject)     | An object containing identifier of an added action timer.   |
| `type`          | string                                                                              | A content template delimiter. It has an `"ActionTimer"` value.  |

## Template example

{% raw %}

```json
// One-time actiontimer
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

// Daily repeated actiontimer
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

// Every week repeated actiontimer
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

## Screen UI example {#UIExample}

<div class="note">
<p><strong>Note!</strong></p>
<p>Preparing for an example of a screen which applied an ActionTimer template.</p>
</div>

## See also
* [ActionTimerList](/CIC/References/ContentTemplates/ActionTimerList.md)
* [Alerts](/CIC/References/CICInterface/Alerts.md) Interface
