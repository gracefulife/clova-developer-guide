# Alerts

This API lets your client create, look up, or delete an alarm or a timer. Your client should call a local app for alarm and timer management, or provide an interface for the functionality. The Alerts API provides the following Event and Directive messages.

| Message name  | Message type  | Message description  |
|------------------|-----------|---------------------------------------------|
| [DeleteAlert](#DeleteAlert) | Directive | Instructs your client to delete an alarm or a timer. |
| [GetAlert](#GetAlert)  | Directive | Instructs your client to look up an alarm or a timer. |
| [SetAlert](#SetAlert)  | Directive | Instructs your client to set an alarm or a timer. |

## DeleteAlert Directive {#DeleteAlert}
Instructs your client to delete an alarm or a timer. Your client should call a local app to delete user's alarm or timer, or provide an interface for the functionality.

### Payload field

| Field name  | Type  | Field description  | Required |
|---------------|---------|-----------------------------|---------|
| type  | string  | Type delimiter <ul><li>ALARM: Alarm</li><li>TIMER: Timer</li></ul> | Yes  |

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
* [SpeechRecognizer.Recognize](/CIC/References/APIs/SpeechRecognizer.md#Recognize)

## GetAlert Directive {#GetAlert}

Instructs your client to look up an alarm or a timer. Your client should call a local app to look up user's alarm or timer, or provide an interface for the functionality.

### Payload field

| Field name  | Type  | Field description  | Required |
|---------------|---------|-----------------------------|---------|
| type  | string  | Type delimiter <ul><li>ALARM: Alarm</li><li>TIMER: Timer</li></ul>  | Yes  |

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
* [SpeechRecognizer.Recognize](/CIC/References/APIs/SpeechRecognizer.md#Recognize)

## SetAlert Directive {#SetAlert}

Instructs your client to set an alarm or a timer. Your client should call a local app to set user's alarm or timer, or provide an interface for the functionality.

### Payload field

| Field name  | Type  | Field description  | Required |
|---------------|---------|-----------------------------|---------|
| currentTime  | string  | Current time ([ISO 8601](https://en.wikipedia.org/wiki/ISO_8601) format). Timers receive the current time from CIC.  | No  |
| daysOfWeek[]  | string array | The array that contains recurring days of the week. It may include values such as "monday", "tuesday", "wednesday", "thursday", "friday", "saturday", "sunday". | No  |
| scheduledTime | string  | The scheduled time of the alarm or timer ([ISO 8601](https://en.wikipedia.org/wiki/ISO_8601) format)  | Yes  |
| token  | string  | The ID of the alarm or timer  | Yes  |
| type  | string  | Type delimiter <ul><li>ALARM: Alarm</li><li>TIMER: Timer</li></ul>  | Yes  |

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
* [SpeechRecognizer.Recognize](/CIC/References/APIs/SpeechRecognizer.md#Recognize)