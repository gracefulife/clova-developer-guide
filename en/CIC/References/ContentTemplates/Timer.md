# Timer Template
When the user creates a timer, CIC passes the timer details in Timer template format to the client. The client should display the timer details on the screen using the received template.

<div class="note">
<p><strong>Note!</strong></p>
<p>Currently, there are limits to the Timer template as below.</p>
<ul>
  <li>With the voice command, the user can only request to add a timer or to check the list.</li>
  <li>In order to modify or delete a timer, the user should use the Clova app.</li>
</ul>
</div>

## Template field

| Field name       | Type    | Field description                     |
|---------------|---------|-----------------------------|
| `scheduledTime` | [DateTimeObject](/CIC/References/ContentTemplates/Shared_Objects.md#DateTimeObject) | An object containing date and time of when the timer will ring.      |
| `type`          | string                                                                              | A content template delimiter. It has an `"Timer"` value.  |

## Template Example

{% raw %}

```json
{
  "type": "Timer",
  "scheduledTime": {
    "type": "datetime",
    "value": "2017-12-24T00:00:00Z"
  }
}
```

{% endraw %}

## Screen UI example {#UIExample}

<div>
<p><strong>Note!</strong></p>
<p>Preparing for an example of a screen which applied a Timer template.</p>
</div>

## See also
* [Alerts](/CIC/References/CICInterface/Alerts.md) Interface
* [TimerList](/CIC/References/ContentTemplates/TimerList.md)
