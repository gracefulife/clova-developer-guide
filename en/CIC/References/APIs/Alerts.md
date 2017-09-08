# Alerts

Creates, looks up or deletes alarms or timers. To manage alarms or timers, have your client call a local app or provide an interface for the task. Alerts provides the following event and directive messages.

| Message name         | Message type  | Message description                                   |
|------------------|-----------|---------------------------------------------|
| [`DeleteAlert`](#DeleteAlert) | Directive | Instructs your client to delete alarms or timers. |
| [`GetAlert`](#GetAlert)       | Directive | Instructs your client to look up alarms or timers. |
| [`SetAlert`](#SetAlert)       | Directive | Instructs your client to set alarms or timers. |

## DeleteAlert directive {#DeleteAlert}
Instructs your client to delete alarms or timers. To delete alarms or timers, have your client call a local app or provide an interface for the task.

### Payload field

| Field name       | Type    | Field description                     | Required |
|---------------|---------|-----------------------------|---------|
| `type`          | string  | A type delimiter <ul><li><code>"ALARM"</code>: Alarm</li><li><code>"TIMER"</code>: Timer</li></ul> | Yes    |

### Message example

{% raw %}

```json
{
  "directive": {
    "header": {
      "namespace": "Alerts",
      "name": "DeleteAlert",
      "messageId": "795251cd-de1b-43d9-9fcd-36d07f12d549",
      "dialogRequestId": "afc4c163-a14a-4f3e-93db-38ce36531785"
    },
    "payload": {
      "type": "ALARM"
    }
  }
}
```

{% endraw %}

### See also
* [`SpeechRecognizer.Recognize`](/CIC/References/APIs/SpeechRecognizer.md#Recognize)

## GetAlert directive {#GetAlert}

Instructs your client to look up alarms or timers. To look up alarms or timers, have your client call a local app or provide an interface for the task.

### Payload field

| Field name       | Type    | Field description                     | Required |
|---------------|---------|-----------------------------|---------|
| `type`          | string  | A type delimiter <ul><li><code>"ALARM"</code>: Alarm</li><li><code>"TIMER"</code>: Timer</li></ul>  | Yes    |

### Message example

{% raw %}

```json
{
  "directive": {
    "header": {
      "namespace": "Alerts",
      "name": "GetAlert",
      "messageId": "fa87aa2e-0825-427d-ab11-c3684b662861",
      "dialogRequestId": "185424fd-ce63-4f08-9965-86f7baea856e"
    },
    "payload": {
      "type": "ALARM"
    }
  }
}
```

{% endraw %}

### See also
* [`SpeechRecognizer.Recognize`](/CIC/References/APIs/SpeechRecognizer.md#Recognize)

## SetAlert directive {#SetAlert}

Instructs your client to set alarms or timers. To set alarms or timers, have your client call a local app or provide an interface for the task.

### Payload field

| Field name       | Type    | Field description                     | Required |
|---------------|---------|-----------------------------|---------|
| `currentTime`   | string       | The current time ([ISO 8601](https://en.wikipedia.org/wiki/ISO_8601) format). Timers receive a current time from CIC.                | No    |
| `daysOfWeek[]`  | string array | An array containing recurring days of the week. It can have values such as "monday", "tuesday", "wednesday", "thursday", "friday", "saturday", "sunday". | No    |
| `scheduledTime` | string       | The time that the alarm or timer is set for ([ISO 8601](https://en.wikipedia.org/wiki/ISO_8601) format)                                        | Yes    |
| `token`         | string       | The ID of the alarm or timer                                                                                                      | Yes    |
| `type`          | string       | A type delimiter <ul><li><code>"ALARM"</code>: Alarm</li><li><code>"TIMER"</code>: Timer</li></ul>                     | Yes    |

### Message example

{% raw %}

```json
{
  "directive": {
    "header": {
      "namespace": "Alerts",
      "name": "SetAlert",
      "messageId": "9f73fad4-f33c-49e3-927f-9c98892936fb",
      "dialogRequestId": "f9210731-1657-48b5-bd74-eccbb46452fb"
    },
    "payload": {
      "token": "test:test_device:1495785482",
      "type": "ALARM",
      "scheduledTime": "2017-05-27T15:00:00+09:00",
      "daysOfWeek": ["saturday", "sunday"]
    }
  }
}
```

{% endraw %}

### See also
* [`SpeechRecognizer.Recognize`](/CIC/References/APIs/SpeechRecognizer.md#Recognize)
