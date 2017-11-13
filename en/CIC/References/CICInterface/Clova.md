# Clova

Returns recognition results of user requests to your client. When user requests are sent in [`SpeechRecognizer.Recognize`](/CIC/References/CICInterface/SpeechRecognizer.md#Recognize) event messages, Clova analyzes their meaning. Based on the recognition results, CIC returns appropriate directive messages to your client. Your client processes the directive messages and provide requested Clova functions to users.

| Message name         | Message type  | Message description                                   |
|------------------|-----------|---------------------------------------------|
| [`FinishExtension`](#FinishExtension)       | Directive | Instructs your client to finish a specified extension.             |
| [`Hello`](#Hello)                           | Directive | Notifies your client that a downchannel connection has been established.       |
| [`Help`](#Help)                             | Directive | Instructs your client to give pre-made help.       |
| [`RenderTemplate`](#RenderTemplate)         | Directive | Instructs your client to display templates.                     |
| [`RenderText`](#RenderText)                 | Directive | Instructs your client to display text.                     |
| [`StartExtension`](#StartExtension)         | Directive | Instructs your client to start a specified extension.            |

## FinishExtension directive {#FinishExtension}

Instructs your client to finish a specified extension. When a FinishExtension directive message is returned, have your client finish the extension that match a specified value.

### Payload field

| Field name       | Type    | Field description                     | Required |
|---------------|---------|-----------------------------|---------|
| `extension`     | string  | The name of the extension to finish          | Yes     |

### Remarks

The server currently provides an extension called the Freetalk mode by default. The Freetalk mode is available only in English at the moment. You can finish the mode by saying the trigger word, "See you later". A FinishExtension directive message returns "freetalking" in the `extension` field.

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
      "extension": "freetalking"
    }
  }
}
```

{% endraw %}

### See also
* [`Clova.StartExtension`](#StartExtension)

## Hello directive {#Hello}

Notifies your client that a downchannel connection has been established. This directive message lets you confirm that the [connection attempt](/CIC/Guides/Interact_with_CIC.md#CreateConnection) has succeeded for the Clova service.

### Payload field

None

### Remarks
This directive message does not have a dialog ID (`dialogRequestId`).

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

Instructs your client to give help for users. This directive message is returned when a user requests for help. Have your client deliver help by playing voice help or displaying help UI on a screen.

### Payload field

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

Instructs your client to display data using a content template. It also returns the content obtained by recognizing user's speech input.

### Payload field
The format of the `payload` field can vary depending on which type of [content template](/CIC/References/Content_Templates.md) is used. Available content templates are as follows.

* Templates for content UI types
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

* Templates for route directions
  * [CarRoute](/CIC/References/ContentTemplates/CarRoute.md)
  * [TransportationRoute](/CIC/References/ContentTemplates/TransportationRoute.md)

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

Instructs your client to display text messages. It also returns text to display to a user.

### Payload field

| Field name       | Type    | Field description                     | Required |
|---------------|---------|-----------------------------|---------|
| `text`          | string  | Text to display to a user          | Yes     |

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
      "text": "신나는 노래 들려드릴게요."
    }
  }
}
```

{% endraw %}

### See also
* [`Clova.RenderTemplate`](#RenderTemplate)

## StartExtension directive {#StartExtension}

Instructs your client to start a specified extension. When a StartExtension directive message is returned, have your client start the extension that matches a specified value.

### Payload field

| Field name       | Type    | Field description                     | Required |
|---------------|---------|-----------------------------|---------|
| `extension`     | string  | The name of the extension to start          | Yes     |

### Remarks

The server currently provides an extension called the Freetalk mode by default. The Freetalk mode is available only in English at the moment. You can start the mode by saying a trigger word, such as "Start a conversation in English". A `StartExtension` directive message returns `"freetalking"` in the `extension` field.

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
      "extension": "freetalking"
    }
  }
}
```

{% endraw %}

### See also

* [`Clova.FinishExtension`](#FinishExtension)
