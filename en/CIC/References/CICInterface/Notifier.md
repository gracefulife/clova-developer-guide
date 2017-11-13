# Notifier

Notifier instructs CIC to display an alarm notification or to delete alarm displays from all clients registered on the user's account. CIC sends the following directive message even without a request from the client to make the client keep the alarm notification as the lastest.

| Message name         | Message type  | Message description                                   |
|------------------|-----------|---------------------------------------------|
| [`ClearIndicator`](#ClearIndicator)         | Directive | Instructs your client to turn off all displays indicating the alarm. |
| [`SetIndicator`](#SetIndicator)             | Directive | Instructs your client to turn on a display indicating an unchecked alarm. |

## ClearIndicator directive {#ClearIndicator}
Instructs your client to turn off all displays indicating the alarm. Must turn off all lights or sound effects indicating the alarm.

### Payload field
None

### Remarks
This directive message is sent through a [downchannel](/CIC/Guides/Interact_with_CIC.md#CreateConnection), which means that the message is not a response to an event message.

### Message example

{% raw %}

```json
{
  "directive": {
    "header": {
      "namespace": "Notifier",
      "name": "ClearIndicator",
      "messageId": "29745c13-0d70-408e-a4cc-946afba67524"
    },
    "payload": {}
  }
}
```

{% endraw %}

### See also
* [`Notifier.SetIndicator`](#SetIndicator)

## SetIndicator directive {#SetIndicator}
Instructs your client to turn on the alarm display.

### Payload field
| Field name       | Type    | Field description                     | Required |
|---------------|---------|-----------------------------|---------|
| `new`         | boolean | A field notifying if the message is a directive message for a new alarm. <ul><li><code>true</code> : If it is a new alarm</li><li><code>false</code> : If it is not a new alarm</li></ul> | Yes    |
| `light`       | string  | Light setting information<ul><li><code>"on"</code> : There are alarms unchecked by the user. Usually turns on the light indicating an alarm. </li><li><code>"off"</code> : All alarms are checked by the user.</li></ul> | Yes    |

### Remarks
This directive message is sent through a [downchannel](/CIC/Guides/Interact_with_CIC.md#CreateConnection), which means that the message is not a response to an event message.

### Message example

{% raw %}

```json
{
  "directive": {
    "header": {
      "namespace": "Notifier",
      "name": "SetIndicator",
      "messageId": "29745c13-0d70-408e-a4cc-946afba67524"
    },
    "payload": {
      "new" : true,
      "light" : "on"
    }
  }
}
```

{% endraw %}

### See also
* [`Notifier.ClearIndicator`](#ClearIndicator)
