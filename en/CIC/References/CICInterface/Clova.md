# Clova

The Clova namespace provides interfaces that return the result for user's voice request. When user requests are sent to Clova through the [`SpeechRecognizer.Recognize`](/CIC/References/CICInterface/SpeechRecognizer.md#Recognize) events, Clova analyzes the request, identifies what the user wants and uses the following directives to return the result for the request. The client is to process these directives and provide the Clova service user wants.

| Message name         | Message type  | Message description                                   |
|------------------|-----------|---------------------------------------------|
| [`ExpectLogin`](#ExpectLogin)               | Directive | Instructs a client to prompt a user to authenticate their {{ book.OrientedService }} account (i.e. login). |
| [`FinishExtension`](#FinishExtension)       | Directive | Instructs a client to end the specified extension.             |
| [`Hello`](#Hello)                           | Directive | Notifies a client that a downchannel connection has been established.       |
| [`Help`](#Help)                             | Directive | Instructs a client to provide pre-made help to the user.       |
| [`RenderTemplate`](#RenderTemplate)         | Directive | Instructs a client to render the given template.                     |
| [`RenderText`](#RenderText)                 | Directive | Instructs a client to display the given text.                     |
| [`StartExtension`](#StartExtension)         | Directive | Instructs a client to start running the given extension.            |

## ExpectLogin directive {#ExpectLogin}

Instructs a client to prompt its user to authenticate their {{ book.OrientedService }} account. CIC sends this directive to a client to provide a service that requires the {{ book.OrientedService }} account authentication while running in the [guest mode](/CIC/References/Clova_Auth_API.md#GuestMode).

### Payload fields

None

### Remarks

After the user gets authenticated successfully, CIC does not pick up the user's previously made request. If needed, the user has to make the request again.

### Message example

{% raw %}

```json
{
    "directive": {
        "header": {
            "messageId": "2ca2ec70-c39d-4741-8a34-8aedd3b24760",
            "namespace": "Clova",
            "name": "RequestLogin"
        },
        "payload": {}
    }
}
```

{% endraw %}

### See also

* [Creating Clova access token](/CIC/Guides/Interact_with_CIC.md#CreateClovaAccessToken)
* [Guest mode](/CIC/References/Clova_Auth_API.md#GuestMode)

## FinishExtension directive {#FinishExtension}

Instructs a client to end the specified extension. End the given extension when you receive this directive.

### Payload fields

| Field name       | Type    | Description                     | Provided |
|---------------|:---------:|-----------------------------|:---------:|
| `extension`     | string  | The name of the extension to finish.          | Always |


### Message example

{% raw %}

```json
{
  "directive": {
    "header": {
      "namespace": "Clova",
      "name": "FinishExtension",
      "messageId": "80855309-77b8-403f-bec5-b50f565d24a2",
      "dialogRequestId": "3db18cee-caac-4101-891f-b5f5c2e7fa9c"
    },
    "payload": {
      "extension": "Sample Extension"
    }
  }
}
```

{% endraw %}

### See also

* [`Clova.StartExtension`](#StartExtension)

## Hello directive {#Hello}

Notifies a client that a downchannel has been established between the client and CIC. This directive is a confirmation for the [connection attempt](/CIC/Guides/Interact_with_CIC.md#CreateConnection) required to use Clova.

### Payload fields

None

### Remarks

This directive does not have a dialog ID (`dialogRequestId`).

### Message example

{% raw %}

```json
{
    "directive": {
        "header": {
            "messageId": "2ca2ec70-c39d-4741-8a34-8aedd3b24760",
            "namespace": "Clova",
            "name": "Hello"
        },
        "payload": {}
    }
}
```

{% endraw %}

### See also

* [Connecting with CIC](/CIC/Guides/Interact_with_CIC.md#ConnectToCIC)

## Help directive {#Help}

Instructs a client to give help for users. This directive is returned when a user requests help for using Clova. Provide a guide by audio or UI through the client screen when you receive this directive.

### Payload fields

None

### Message example

{% raw %}

```json
{
    "directive": {
        "header": {
            "messageId": "2ca2ec70-c39d-4741-8a34-8aedd3b24760",
            "namespace": "Clova",
            "name": "Help"
        },
        "payload": {}
    }
}
```

{% endraw %}

### See also

None

## RenderTemplate directive {#RenderTemplate}

Instructs a client to display data, the result of recognizing user's voice request, filled in the given content template.

### Payload fields

The format of the `payload` field differs depending on the type of [content template](/CIC/References/Content_Templates.md) used. Available content templates are as follows.

* Templates for different UI layouts
  * [CardList](/CIC/References/ContentTemplates/CardList.md)
  * [ImageList](/CIC/References/ContentTemplates/ImageList.md)
  * [ImageText](/CIC/References/ContentTemplates/ImageText.md)
  * [Popup](/CIC/References/ContentTemplates/Popup.md)
  * [Text](/CIC/References/ContentTemplates/Text.md)

* PIMS template
  * [ActionTimer](/CIC/References/ContentTemplates/ActionTimer.md)
  * [ActionTimerList](/CIC/References/ContentTemplates/ActionTimerList.md)
  * [Alarm](/CIC/References/ContentTemplates/Alarm.md)
  * [AlarmList](/CIC/References/ContentTemplates/AlarmList.md)
  * [Memo](/CIC/References/ContentTemplates/Memo.md)
  * [MemoList](/CIC/References/ContentTemplates/MemoList.md)
  * [Reminder](/CIC/References/ContentTemplates/Reminder.md)
  * [ReminderList](/CIC/References/ContentTemplates/ReminderList.md)
  * [Schedule](/CIC/References/ContentTemplates/Schedule.md)
  * [ScheduleList](/CIC/References/ContentTemplates/ScheduleList.md)
  * [Timer](/CIC/References/ContentTemplates/Timer.md)
  * [TimerList](/CIC/References/ContentTemplates/TimerList.md)

* Templates for weather forecast
  * [Atmosphere](/CIC/References/ContentTemplates/Atmosphere.md)
  * [Humidity](/CIC/References/ContentTemplates/Humidity.md)
  * [TodayWeather](/CIC/References/ContentTemplates/TodayWeather.md)
  * [TomorrowWeather](/CIC/References/ContentTemplates/TomorrowWeather.md)
  * [WeeklyWeather](/CIC/References/ContentTemplates/WeeklyWeather.md)
  * [WindSpeed](/CIC/References/ContentTemplates/WindSpeed.md)

### Message example

{% raw %}

```json
{
  "directive": {
    "header": {
      "namespace": "Clova",
      "name": "RenderTemplate",
      "messageId": "c7b9882e-d3bf-45b6-b6f4-2fc47d04e60e",
      "dialogRequestId": "ca10e609-1d24-4418-bc2a-21b70c5ea1a7"
    },
    "payload": {
        {{TemplateFormat}}
    }
  }
}
```

{% endraw %}

### See also

* [`Clova.RenderText`](#RenderText)
* [Content template](/CIC/References/Content_Templates.md)

## RenderText directive {#RenderText}

Instructs a client to display the given text message.

### Payload fields

| Field name       | Type    | Description                     | Required |
|---------------|:---------:|-----------------------------|:---------:|
| `text`          | string  | The text message to display to a user.          | Required |

### Message example

{% raw %}

```json
{
  "directive": {
    "header": {
      "namespace": "Clova",
      "name": "RenderText",
      "messageId": "6f9d8b54-21dc-4811-8e14-b9b60717cbd4",
      "dialogRequestId": "5690395e-8c0d-4123-9d3f-937eaa9285dd"
    },
    "payload": {
      "text": "I will play an exciting song for you."
    }
  }
}
```

{% endraw %}

### See also

* [`Clova.RenderTemplate`](#RenderTemplate)

## StartExtension directive {#StartExtension}

Instructs a client to start the specified extension. Start the given extension when you receive this directive.

### Payload fields

| Field name       | Type    | Description                     | Provided |
|---------------|:---------:|-----------------------------|:---------:|
| `extension`     | string  | The name of the extension to start          | Always |

### Message example

{% raw %}

```json
{
  "directive": {
    "header": {
      "namespace": "Clova",
      "name": "StartExtension",
      "messageId": "103b8847-9109-42a5-8d3f-fc370a243d6f",
      "dialogRequestId": "8b509a36-9081-4783-b1cd-58d406205956"
    },
    "payload": {
      "extension": "Sample Extension"
    }
  }
}
```

{% endraw %}

### See also

* [`Clova.FinishExtension`](#FinishExtension)
