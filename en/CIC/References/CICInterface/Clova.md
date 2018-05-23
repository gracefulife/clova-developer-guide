# Clova

The Clova namespace provides interfaces that return the result for a user voice request. When the user request is sent to CIC as a [`SpeechRecognizer.Recognize`](/CIC/References/CICInterface/SpeechRecognizer.md#Recognize) event, CIC analyzes the request. The directives below are returned to the client according to the analyzed result. The client needs to handle these directives and provide Clova services to users.

| Message name         | Type  | Description                                   |
|------------------|-----------|---------------------------------------------|
| [`ExpectLogin`](#ExpectLogin)                    | Directive | Instructs the client to prompt its user to authenticate their {{ book.OrientedService }} account. |
| [`FinishExtension`](#FinishExtension)            | Directive | Instructs the client to end the specified extension.             |
| [`HandleDelegatedEvent`](#HandleDelegatedEvent)  | Directive | Instructs the client to [handle the user request delegated](/CIC/Guides/Interact_with_CIC.md#HandleDelegation) from the Clova app.   |
| [`Hello`](#Hello)                                | Directive | Notifies the client that a downchannel has been established between the client and CIC.       |
| [`Help`](#Help)                                  | Directive | Instructs the client to provide the existing Help guide to the user.       |
| [`LaunchURI`](#LaunchURI)                        | Directive | Instructs the client to either launch or execute the site or the app expressed as a URI.                         |
| [`ProcessDelegatedEvent`](#ProcessDelegatedEvent) | Event    | Requests CIC for the result of handling the [delegated user request](/CIC/Guides/Interact_with_CIC.md#HandleDelegation).  |
| [`RenderTemplate`](#RenderTemplate)              | Directive | Instructs the client to display the given template.                     |
| [`RenderText`](#RenderText)                      | Directive | Instructs the client to display the given text.                     |
| [`StartExtension`](#StartExtension)              | Directive | Instructs the client to start the specified extension.            |

## ExpectLogin directive {#ExpectLogin}

Instructs the client to prompt its user to authenticate their {{ book.OrientedService }} account. CIC sends this directive to a client to provide a service that requires the {{ book.OrientedService }} account authentication while running in the [guest mode](/CIC/References/Clova_Auth_API.md#GuestMode).

### Payload fields

None

### Remarks
Once the user gets authenticated successfully, CIC stops handling old requests of the user. If needed, the user has to make the request again.

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
* [Creating Clova access tokens](/CIC/Guides/Interact_with_CIC.md#CreateClovaAccessToken)
* [Guest mode](/CIC/References/Clova_Auth_API.md#GuestMode)

## FinishExtension directive {#FinishExtension}

Instructs the client to end the specified extension. The client must end the specified extension upon receipt of this directive.

### Payload fields

| Field name       | Data type    | Description                     | Included |
|---------------|---------|-----------------------------|:---------:|
| `extension`   | string  | The name of the extension to end.          | Always     |

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
      "extension": "SampleExtension"
    }
  }
}
```

{% endraw %}

### See also
* [`Clova.StartExtension`](#StartExtension)

## HandleDelegatedEvent directive {#HandleDelegatedEvent}

Instructs the client to [handle the user request delegated](/CIC/Guides/Interact_with_CIC.md#HandleDelegation) from the Clova app. A user can delegate another client device of the user—that is not the Clova app—to receive the handling results of requests made while using the Clova app. This directive is sent to the client device that has been delegated to handle the result. That client device must then send the [`ProcessDelegatedEvent`](#ProcessDelegatedEvent) event to CIC to receive the handled result.

### Payload fields

| Field name       | Data type    | Description                     | Included |
|---------------|---------|-----------------------------|:---------:|
| `delegationId` | string  | The ID of the delegated request. Make sure to include this value in `payload` when sending [`ProcessDelegatedEvent`](#ProcessDelegatedEvent) events after delegation.         | Always     |

### Remarks

This directive is sent through a [downchannel](/CIC/Guides/Interact_with_CIC.md#CreateConnection), not as a response to an event.

### Message example

{% raw %}

```json
{
  "directive": {
    "header": {
      "messageId": "b17df741-2b5b-4db4-a608-85ecb1307b33",
      "namespace": "Clova",
      "name": "HandleDelegatedEvent"
    },
    "payload": {
      "delegationId": "99e86204-710a-4e94-b949-a763e78348a7"
    }
  }
}
```

{% endraw %}

### See also
* [Clova.ProcessDelegatedEvent](#ProcessDelegatedEvent)
* [Handling delegated user requests](/CIC/Guides/Interact_with_CIC.md#HandleDelegation)

## Hello directive {#Hello}

Notifies the client that a downchannel has been established between the client and CIC. This directive is a confirmation for the [connection attempt](/CIC/Guides/Interact_with_CIC.md#CreateConnection) required to use Clova.

### Payload fields

None

### Remarks
This directive does not have a dialogue ID (`dialogRequestId`).

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

Instructs the client to provide the Help guide to the user. This directive is returned when a user requests help for using Clova. Upon receipt, the client must provide a guide by audio or visual display.

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

## LaunchURI directive {#LaunchURI}

Instructs the client to either launch or execute the site or the app expressed as a URI. Upon receiving this directive, the client must execute the site or the app using the `targets[].uri` field.

### Payload fields

| Field name       | Data type    | Description                     | Included |
|---------------|---------|-----------------------------|:---------:|
| `targets[]`              | object array | The object array that has URI information.                       | Always     |
| `targets[].description`  | string       | The description of the target expressed as a URI (app or site).           | Optional     |
| `targets[].iconImageUrl` | string       | The icon image of the target expressed as a URI.                 | Optional     |
| `targets[].marketUrl`    | string       | **If the target expressed as a URI is an app**, the address of app store.  | Optional     |
| `targets[].packageName`  | string       | **If the target expressed as a URI is an app**, the package name of app.  | Optional     |
| `targets[].title`        | string       | The title of the target expressed as a URI.                        | Required     |
| `targets[].uri`          | string       | The information of the target URI.                                  | Required     |

### Remarks

* The client can display the preview using the <a href="http://ogp.me/" target="_blank">Open Graph protocol</a> data from the `targets[].uri` URI, and can also use the `targets[].iconImageUrl`, `targets[].title`, and `targets[].description` fields to instantly display partial data.
* **If the target expressed as a URI is an app**, `targets[].marketUrl` and `targets[].packageName` fields may be used. `targets[].marketUrl` is used when the target app cannot be executed due to not being installed and `targets[].packageName` is the additional information for reference when the app cannot be executed with `targets[].uri`.
* The client does not have to launch or execute all targets in the array of the `targets[]` field. The client must try to launch or execute the target using the first element of the URI in the array. If the attempt fails, the client must attempt the same action using the next element in the array. Basically, an array is used to include alternatives in case an element cannot be executed.

### Message example

```json
// App type example
{
  "directive": {
    "header": {
      "namespace": "Clova",
      "name": "LaunchURI",
      "messageId": "086ccadf-cd88-4cff-9706-cc4f0801c929",
      "dialogRequestId": "de20ea1a-ea39-4c2a-a033-73fa014b2fd5"
    },
    "payload": {
      "targets": [
        {
          "uri": "sampleapp2://main",
          "title": "Sample app2",
          "iconImageUrl": "https://yourdomain.com/sampleappicon.png",
          "marketUrl": "https://play.google.com/store/apps/details?id=com.yourdomain.sampleapp",
          "packageName": "com.yourdomain.sampleapp",
          "description": "Sample app2"
        },
        {
          "uri": "sampleapp://main",
          "title": "Sample app",
          "iconImageUrl": "https://yourdomain.com/sampleappicon.png",
          "marketUrl": "https://play.google.com/store/apps/details?id=com.yourdomain.sampleapp",
          "packageName": "com.yourdomain.sampleapp",
          "description": "Sample app"
        }
      ]
    }
  }
}

// Site type example
{
  "directive": {
    "header": {
      "namespace": "Clova",
      "name": "LaunchURI",
      "messageId": "fcb0919e-9847-46ec-90bc-ab0fe8216771",
      "dialogRequestId": "9ab7256a-6add-4b4a-a0b8-481f41d36a9d"
    },
    "payload": {
      "targets": [
        {
          "uri": "http://example.org",
          "title": "Example Domain"
        }
      ]
    }
  }
}
```

### See also
None

## ProcessDelegatedEvent event {#ProcessDelegatedEvent}

Requests CIC for the result of handling the [delegated user request](/CIC/Guides/Interact_with_CIC.md#HandleDelegation). When sending this event to CIC, make sure to include the `delegationId` value received through the [`HandleDelegatedEvent`](#HandleDelegatedEvent) directive in the `payload` of this message. The client will receive the result on the request which the user had made through Clova app as a response to this directive.

### Context fields

{% include "/CIC/References/CICInterface/Context_Objects_List.md" %}

### Payload fields

| Field name       | Data type    | Description                     | Required |
|---------------|---------|-----------------------------|:---------:|
| `delegationId` | string  | The ID of the delegated request. The `delegationId` field value received through the [`HandleDelegatedEvent`](#HandleDelegatedEvent) directive must be entered without any alteration.         | Required     |

### Message example
{% raw %}
```json
{
  "context": [
    {{Alerts.AlertsState}},
    {{AudioPlayer.PlayerState}},
    {{Device.DeviceState}},
    {{Device.Display}},
    {{Clova.Location}},
    {{Clova.SavedPlace}},
    {{Speaker.VolumeState}},
    {{SpeechSynthesizer.SpeechState}}
  ],
  "event": {
    "header": {
      "namespace": "Clova",
      "name": "ProcessDelegatedEvent",
      "messageId": "b120c3e0-e6b9-4a3d-96de-71539e5f6214"
    },
    "payload": {
      "delegationId": "99e86204-710a-4e94-b949-a763e78348a7"
    }
  }
}
```
{% endraw %}

### See also
* [`Clova.HandleDelegatedEvent`](#HandleDelegatedEvent)
* [`SpeechRecognizer.Recognize`](/CIC/References/CICInterface/SpeechRecognizer.md#Recognize)
* [Handling delegated user requests](/CIC/Guides/Interact_with_CIC.md#HandleDelegation)

## RenderTemplate directive {#RenderTemplate}

Instructs the client to display data according to the content template. The result of contents from speech recognition is also sent to the client.

### Payload fields
The format of the `payload` varies depending on the type of [content template](/CIC/References/Content_Templates.md) used. Available content templates are as follows.

* Templates per UI type
  * [CardList](/CIC/References/ContentTemplates/CardList.md)
  * [ImageList](/CIC/References/ContentTemplates/ImageList.md)
  * [ImageText](/CIC/References/ContentTemplates/ImageText.md)
  * [Popup](/CIC/References/ContentTemplates/Popup.md)
  * [Text](/CIC/References/ContentTemplates/Text.md)

* PIMS templates
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

* Weather templates
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

Instructs the client to display the given text message. The text message to display to the user is also sent.

### Payload fields

| Field name       | Data type    | Description                     | Included |
|---------------|---------|-----------------------------|:---------:|
| `text`          | string  | The text to show to the user.        | Always     |

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
      "text": "I will play some upbeat music for you."
    }
  }
}
```

{% endraw %}

### See also
* [`Clova.RenderTemplate`](#RenderTemplate)

## StartExtension directive {#StartExtension}

Instructs the client to start the specified extension. Upon receiving the directive, the client must start the specified extension.

### Payload fields

| Field name       | Data type    | Description                     | Included |
|---------------|---------|-----------------------------|:---------:|
| `extension`   | string  | The name of the extension to start.          | Always     |

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
      "extension": "SampleExtension"
    }
  }
}
```

{% endraw %}

### See also
* [`Clova.FinishExtension`](#FinishExtension)
