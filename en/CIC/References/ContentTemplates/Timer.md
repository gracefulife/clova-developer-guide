# Timer Template

The Timer template is used in providing timer information for the client to display on the client's screen.
When the user creates a timer, CIC sends the timer information to the client, in the form of the Timer template.

<div class="note">
<p><strong>Note!</strong></p>
<p>The following is the restrictions in using the Timer template:</p>
<ul>
  <li>Voice requests can be used only to add a timer or to check a list of timers.</li>
  <li>To modify or delete a timer, the user must use the Clova app.</li>
</ul>
</div>

## Template fields

| Field name       | Type    | Description                     |
|---------------|---------|-----------------------------|
| `scheduledTime` | [DateTimeObject](/CIC/References/ContentTemplates/Shared_Objects.md#DateTimeObject) | The date and time at which this timer is to ring.           |
| `token`         | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject)     | The ID of this timer.                     |
| `type`          | string                                                                              | The type of this template. The value is always `"Timer"`.        |

## Template example

{% raw %}

```json
{
  "type": "Timer",
  "token": {
    "type": "string",
    "value": "072c72b9-cfc5-4127-b4fe-557a10457232"
  },
  "scheduledTime": {
    "type": "datetime",
    "value": "2017-12-24T00:00:00Z"
  }
}
```

{% endraw %}

## UI example {#UIExample}

<div class="note">
<p><strong>Note!</strong></p>
<p>An example for the Timer template is in preparation.</p>
</div>

## See also

* [Alerts](/CIC/References/CICInterface/Alerts.md) Interface
* [TimerList](/CIC/References/ContentTemplates/TimerList.md)
