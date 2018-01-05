# TimerList Template

The TimerList template is used in providing information of multiple timers for the client to display on the client's screen.
When the user requests for a list of timers, CIC sends the list of timers registered by the user to the client, in the form of the TimerList template.

<div class="note">
<p><strong>Note!</strong></p>
<p>The following is the restrictions in using the TimerList template:</p>
<ul>
  <li>Voice requests can be used only to add a timer or to check a list of timers.</li>
  <li>To modify or delete a timer, the user must use the Clova app.</li>
</ul>
</div>


## Template fields

| Field name       | Type    | Description                     |
|---------------|---------|-----------------------------|
| `timerList[]`               | object array  | Contains a list of timers registered by the user.                                                                                        |
| `timerList[].scheduledTime` | [DateTimeObject](/CIC/References/ContentTemplates/Shared_Objects.md#DateTimeObject) | The date and time at which this timer is to ring.                    |
| `timerList[].token`         | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject)     | The ID of this timer.                             |
| `type`                      | string                                                                              | The type of this template. The value is always `"TimerList"`.      |

## Template example

{% raw %}

```json
{
  "type": "Timer",
  "timerList": [
    {
      "token": {
        "type": "string",
        "value": "072c72b9-cfc5-4127-b4fe-557a10457232"
      },
      "scheduledTime": {
        "type": "datetime",
        "value": "2017-12-24T00:00:10Z"
      }
    },
    {
      "token": {
        "type": "string",
        "value": "b5403bd0-1598-495b-a466-9385c2b1103a"
      },
      "scheduledTime": {
        "type": "datetime",
        "value": "2017-12-24T00:00:20Z"
      }
    },
    {
      "token": {
        "type": "string",
        "value": "da740e2a-01cd-4f2e-aedf-6c4285bae785"
      },
      "scheduledTime": {
        "type": "datetime",
        "value": "2017-12-24T00:01:00Z"
      }
    }
  ]
}
```

{% endraw %}

## UI example {#UIExample}

<div class="note">
<p><strong>Note!</strong></p>
<p>An example for the TimerList template is in preparation.</p>
</div>

## See also

* [Alerts](/CIC/References/CICInterface/Alerts.md) Interface
* [Timer](/CIC/References/ContentTemplates/Timer.md)
