# Notifier

The Notifier namespace provides interfaces for CIC to instruct a client to turn on notification indicators or to turn off notification indicators on all the clients registered to the user's account. For clients to keep the notification check status up to date, CIC sends the following directives, without having received events from clients:

| Message name         | Message type  | Message description                                   |
|------------------|-----------|---------------------------------------------|
| [`ClearIndicator`](#ClearIndicator)         | Directive | Instructs a client to turn off all the notification indicators. |
| [`SetIndicator`](#SetIndicator)             | Directive | Instructs a client to turn on notification indicators for unchecked notifications. |

## ClearIndicator directive {#ClearIndicator}

Instructs a client to turn off notification indicators. Turn off all light indicators or sound effects for notification.

### Payload fields

None

### Remarks

This directive is sent through a [downchannel](/CIC/Guides/Interact_with_CIC.md#CreateConnection), which means that this directive is not a response to an event.

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

Instructs a client to turn on the notification indicator.

### Payload fields
| Field name       | Type    | Description                     | Provided |
|---------------|:---------:|-----------------------------|:---------:|
| `new`         | boolean | Indicates if the notification to turn the indicator on is a new notification. <ul><li><code>true</code>: The notification is new.</li><li><code>false</code>: The notification is not new.</li></ul> | Always |
| `light`       | string  | Indicates whether to tun on the light indicator<ul><li><code>"on"</code>: Indicates there are notifications unchecked by the user. Turn on the light indicator.</li><li><code>"off"</code>: All notifications have been checked by the user.</li></ul> | Always |

### Remarks

This directive is sent through a [downchannel](/CIC/Guides/Interact_with_CIC.md#CreateConnection), which means that this directive is not a response to an event.

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
      "new": true,
      "light": "on"
    }
  }
}
```

{% endraw %}

### See also

* [`Notifier.ClearIndicator`](#ClearIndicator)
