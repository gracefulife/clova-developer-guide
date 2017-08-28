# Clova

It consists of a set of directive messages that return recognition results for client requests. When user requests are sent by [`SpeechRecognizer.Recognize`](/CIC/References/APIs/SpeechRecognizer.md#Recognize) event messages, Clova analyzes their meaning. And CIC returns appropriate directive messages to your client based on recognition results. Then, your client processes the directive messages and provide requested Clova functions to users.

| Message name         | Message type  | Message description                                   |
|------------------|-----------|---------------------------------------------|
| [`AddMemo`](#AddMemo)                       | Directive | Instructs your client to add new memos.                  |
| [`AddReminder`](#AddReminder)               | Directive | Instructs your client to add new reminders.               |
| [`AddSchedule`](#AddSchedule)               | Directive | Instructs your client to add new schedules.                  |
| [`CountSchedule`](#CountSchedule)           | Directive | Instructs your client to count the number of schedules within a specified period. |
| [`DeleteMemo`](#DeleteMemo)                 | Directive | Instructs your client to delete memos.                       |
| [`DeleteReminder`](#DeleteReminder)         | Directive | Instructs your client to delete reminders.                    |
| [`DeleteSchedule`](#DeleteSchedule)         | Directive | Instructs your client to delete schedules.                       |
| [`FinishExtension`](#FinishExtension)       | Directive | Instructs your client to finish a specified extension.             |
| [`GetMemo`](#GetMemo)                       | Directive | Instructs your client to look up memos.                       |
| [`GetReminder`](#GetReminder)               | Directive | Instructs your client to look up reminders.                    |
| [`GetSchedule`](#GetSchedule)               | Directive | Instructs your client to look up schedules.                       |
| [`Hello`](#Hello)                           | Directive | Notifies your client that a downchannel connection has been established.       |
| [`RenderMemoList`](#RenderMemoList)         | Directive | Instructs your client to display a list of memos.                   |
| [`RenderReminderList`](#RenderReminderList) | Directive | Instructs your client to display a list of reminders.                |
| [`RenderTemplate`](#RenderTemplate)         | Directive | Instructs your client to display templates.                     |
| [`RenderText`](#RenderText)                 | Directive | Instructs your client to display text.                     |
| [`StartExtension`](#StartExtension)         | Directive | Instructs your client to start a specified extension.            |



## AddMemo directive {#AddMemo}

Instructs your client to add new memos. It also returns content of the memos recognized from user's speech input.

### Payload field

| Field name       | Type    | Field description                     | Required |
|---------------|---------|-----------------------------|---------|
| `content`       | string  | Content of the memo to add              | Yes     |
| `id`            | string  | The ID of the memo to add               | Yes     |

### Remarks

After successfully creating new memos, you must send the result to CIC, using a [`Memo.Created`](/CIC/References/APIs/Memo.md#Created) event message.

### Message example

{% raw %}

```json
{
  "directive": {
    "header": {
      "namespace": "Clova",
      "name": "AddMemo",
      "messageId": "23bdfff7-b655-46d4-8655-8bb473bf2bf5",
      "dialogRequestId": "3c6eef8b-8427-4b46-a367-0a7a46432519"
    },
    "payload": {
      "id": "8f88daef-ebc9-4b44-b46f-3c875c6981b7",
      "content": "와이파이 비밀번호 1234"
    }
  }
}
```

{% endraw %}

### See also
* [`Clova.DeleteMemo`](#DeleteMemo)
* [`Clova.GetMemo`](#GetMemo)
* [`Clova.RenderMemoList`](#RenderMemoList)
* [`Memo.Created`](/CIC/References/APIs/Memo.md#Created)

## AddReminder directive {#AddReminder}

Instructs your client to add new reminders. It also returns content of the reminders recognized from user's speech input.

### Payload field

| Field name       | Type    | Field description                     | Required |
|---------------|---------|-----------------------------|---------|
| `content`       | string  | Content of the reminder to add           | Yes     |
| `id`            | string  | The ID of the reminder to add            | Yes     |

### Remarks

After successfully creating new reminders, you must send the result to CIC, using a [`Reminder.Created`](/CIC/References/APIs/Reminder.md#Created) event message.

### Message example

{% raw %}

```json
{
  "directive": {
    "header": {
      "namespace": "Clova",
      "name": "AddReminder",
      "messageId": "4fef1142-99f5-4cf4-a2ac-8658c2dbef4d",
      "dialogRequestId": "6b4061db-fbc1-45a2-9c54-b7c62d366b98"
    },
    "payload": {
      "id": "f8747f49-4082-416d-b53e-f9a6069ed5e4",
      "content": "비타민 먹기"
    }
  }
}
```

{% endraw %}

### See also
* [`Clova.DeleteReminder`](#DeleteReminder)
* [`Clova.GetReminder`](#GetReminder)
* [`Clova.RenderReminderList`](#RenderReminderList)
* [`Reminder.Created`](/CIC/References/APIs/Reminder.md#Created)

## AddSchedule directive {#AddSchedule}

Instructs your client to add new schedules. It also returns content of the schedules recognized from user's speech input. To manage schedules, have your client call a local app or provide an interface for the task.

### Payload field

| Field name       | Type    | Field description                     | Required |
|---------------|---------|-----------------------------|---------|
| `content`       | string | Content of the schedule                                                                    | No    |
| `id`            | string | The ID of the schedule to add                                                              | Yes    |
| `period`        | string | The smallest unit of period recognized from user's speech input. The end time of the schedule is set to the value of `scheduledTime` added by `period`. <ul><li><code>"none"</code>: No period</li><li><code>"year"</code>: 1 year</li><li><code>"month"</code>: 1 month</li><li><code>"week"</code>: 1 week</li><li><code>"day"</code>: 1 day</li><li><code>"hour"</code>: 1 hour</li><li><code>"minute"</code>: 1 minute</li></ul>          | Yes    |
| `scheduledTime` | string | The start time of the schedule ([ISO 8601](https://en.wikipedia.org/wiki/ISO_8601) format) | Yes    |


### Remarks

Implement exception handling to deal with the situation of receiving a unit of period that is not processable by your client. For example, if your client does not support adding of a yearly schedule but has received `"year"` for `period`, you must handle it as an exception. If the period is undetermined, as in "Add a schedule", `period` is set to `"none"` and `scheduledTime` is set to a current time.

### Message example

{% raw %}

```json
{
  "directive": {
    "header": {
      "namespace": "Clova",
      "name": "AddSchedule",
      "messageId": "d53b1251-91f8-48da-bff4-bc49fe024cfe",
      "dialogRequestId": "4f63b5dd-282a-4876-b588-ae41c707e6cd"
    },
    "payload": {
      "id": "69385086-4bb6-46ae-a547-f8c24046b4dd",
      "scheduledTime": "2017-05-28T06:00:00Z",
      "period": "hour",
      "content": "친구 결혼식"
    }
  }
}
```

{% endraw %}

### See also

* [`Clova.CountSchedule`](#CountSchedule)
* [`Clova.DeleteSchedule`](#DeleteSchedule)
* [`Clova.GetSchedule`](#GetSchedule)

## CountSchedule directive {#CountSchedule}

Instructs your client to count the number of schedules that match specified conditions. It also returns the lookup conditions recognized from user's speech input. Have your client call a local app that manages schedules and find out how many schedules match specified conditions.

### Payload field

| Field name       | Type    | Field description                     | Required |
|---------------|---------|-----------------------------|---------|
| period        | string  | The smallest unit of period recognized from user's speech input. The end time of the lookup period is set to the value of `scheduledTime` added by `period`. <ul><li>"none": No period</li><li>"year": 1 year</li><li>"month": 1 month</li><li>"week": 1 week</li><li>"day": 1 day</li><li>"hour": 1 hour</li><li>"minute": 1 minute</li></ul>                | Yes    |
| scheduledTime | string  | The start time of the lookup period ([ISO 8601](https://en.wikipedia.org/wiki/ISO_8601) format) | Yes    |

### Remarks

Implement exception handling to deal with the situation of receiving a unit of period that is not processable by your client. For example, if your client does not support looking up of a yearly schedule but has received "year" for `period`, you must handle it as an exception. If the period is undetermined, as in "How many schedules are there", `period` is set to "none" and `scheduledTime` is set to a current time.


### Message example

{% raw %}

```json
{
  "directive": {
    "header": {
      "namespace": "Clova",
      "name": "CountSchedule",
      "messageId": "17c6bad6-da9b-4489-88f9-9017141e9fbe",
      "dialogRequestId": "00fb1927-35d2-4a83-9c8f-4c141db36d86"
    },
    "payload": {
      "scheduledTime": "2017-05-23T15:00:00Z",
      "period": "day"
    }
  }
}
```

{% endraw %}

### See also
* [`Clova.AddSchedule`](#AddSchedule)
* [`Clova.DeleteSchedule`](#DeleteSchedule)
* [`Clova.GetSchedule`](#GetSchedule)

## DeleteMemo directive {#DeleteMemo}

Instructs your client to delete memos. When a `DeleteMemo` directive message is returned, have your client provide a proper interface with which users can delete memos.

### Payload field

None

### Remarks

After successfully deleting memos, you must send the result to CIC, using a [`Memo.Deleted`](/CIC/References/APIs/Memo.md#Deleted) event message.

### Message example

{% raw %}

```json
{
  "directive": {
    "header": {
      "namespace": "Clova",
      "name": "DeleteMemo",
      "messageId": "8c831d6d-b610-40a7-bd8d-845bccd991f3",
      "dialogRequestId": "890a7a00-8481-4875-8e13-cd94e53e596b"
    },
    "payload": {}
  }
}
```

{% endraw %}

### See also
* [`Clova.AddMemo`](#AddMemo)
* [`Clova.GetMemo`](#GetMemo)
* [`Clova.RenderMemoList`](#RenderMemoList)
* [`Memo.Deleted`](/CIC/References/APIs/Memo.md#Deleted)

## DeleteReminder directive {#DeleteReminder}

Instructs your client to delete reminders. When a `DeleteReminder` directive message is returned, have your client provide a proper interface with which users can delete reminders.

### Payload field

None

### Remarks

After successfully deleting reminders, you must send the result to CIC, using a [`Reminder.Deleted`](/CIC/References/APIs/Reminder.md#Deleted) event message.

### Message example

{% raw %}

```json
{
  "directive": {
    "header": {
      "namespace": "Clova",
      "name": "DeleteReminder",
      "messageId": "39dc5dc0-194b-40af-be5e-b1155447f800",
      "dialogRequestId": "988f347b-9b98-421a-8779-47a753b8fba9"
    },
    "payload": {}
  }
}
```

{% endraw %}

### See also
* [`Clova.AddReminder`](#AddReminder)
* [`Clova.GetReminder`](#GetReminder)
* [`Clova.RenderReminderList`](#RenderReminderList)
* [`Reminder.Deleted`](/CIC/References/APIs/Reminder.md#Deleted)

## DeleteSchedule directive {#DeleteSchedule}

Instructs your client to delete schedules. It also returns the conditions recognized from user's speech input. To delete schedules that match specified conditions, have your client call a local app that manages schedules or provide an interface for the task.

### Payload field

| Field name       | Type    | Field description                     | Required |
|---------------|---------|-----------------------------|---------|
| `period`        | string  | The smallest unit of period recognized from user's speech input. The end time of the deletion period is set to the value of `scheduledTime` added by `period`. <ul><li><code>"none"</code>: No period</li><li><code>"year"</code>: 1 year</li><li><code>"month"</code>: 1 month</li><li><code>"week"</code>: 1 week</li><li><code>"day"</code>: 1 day</li><li><code>"hour"</code>: 1 hour</li><li><code>"minute"</code>: 1 minute</li></ul>                | Yes    |
| `scheduledTime` | string  | The start time of the deletion period ([ISO 8601](https://en.wikipedia.org/wiki/ISO_8601) format) | Yes    |

### Remarks

Implement exception handling to deal with the situation of receiving a unit of period that is not processable by your client. For example, if your client does not support deleting of a weekly schedule but has received `"week"` for `period`, you must handle it as an exception. If the period is undetermined, as in "Delete a schedule", `period` is set to `"none"` and `scheduledTime` is set to a current time.

### Message example

{% raw %}

```json
{
  "directive": {
    "header": {
      "namespace": "Clova",
      "name": "DeleteReminder",
      "messageId": "39dc5dc0-194b-40af-be5e-b1155447f800",
      "dialogRequestId": "988f347b-9b98-421a-8779-47a753b8fba9"
    },
    "payload": {}
  }
}
```

{% endraw %}

### See also
* [`Clova.AddSchedule`](#AddSchedule)
* [`Clova.CountSchedule`](#CountSchedule)
* [`Clova.GetSchedule`](#GetSchedule)

## FinishExtension directive {#FinishExtension}

Instructs your client to finish a specified extension. When a FinishExtension directive message is returned, have your client finish the extension that match a specified value.

### Payload field

| Field name       | Type    | Field description                     | Required |
|---------------|---------|-----------------------------|---------|
| `extension`     | string  | The name of the extension to finish          | Yes     |

### Remarks

The server currently provides an extension called the Freetalk mode by default. The Freetalk mode is available only in English at the moment. You can finish the mode by saying the trigger word, "See you later". Then, the FinishExtension directive message returns "freetalking" in the `extension` field.

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

## GetMemo directive {#GetMemo}

Instructs your client to look up memos. To look up memos, have your client call a local app or provide an interface for the task.

### Payload field

None

### Message example

{% raw %}

```json
{
  "directive": {
    "header": {
      "namespace": "Clova",
      "name": "GetMemo",
      "messageId": "73b838e6-133d-4819-a6d2-39f1920d860c",
      "dialogRequestId": "aa2b33da-0f7a-4138-b0e1-bfa4bca8f1f8"
    },
    "payload": {}
  }
}
```

{% endraw %}

### See also
* [`Clova.AddMemo`](#AddMemo)
* [`Clova.DeleteMemo`](#DeleteMemo)
* [`Clova.GetMemo`](#GetMemo)
* [`Clova.RenderMemoList`](#RenderMemoList)
* [`Memo.Get`](/CIC/References/APIs/Memo.md#Get)

## GetReminder directive {#GetReminder}

Instructs your client to look up reminders. To look up reminders, have your client call a local app or provide an interface for the task.

### Payload field

None

### Message example

{% raw %}

```json
{
  "directive": {
    "header": {
      "namespace": "Clova",
      "name": "GetReminder",
      "messageId": "13b501b0-2da8-4634-b36e-3126d2855c2f",
      "dialogRequestId": "c406adb7-c4da-4c7f-89eb-d4596e011bfb"
    },
    "payload": {}
  }
}
```

{% endraw %}

### See also
* [`Clova.AddReminder`](#AddReminder)
* [`Clova.DeleteReminder`](#DeleteReminder)
* [`Clova.RenderReminderList`](#RenderReminderList)
* [`Reminder.Get`](/CIC/References/APIs/Reminder.md#Get)

## GetSchedule directive {#GetSchedule}

Instructs your client to look up schedules. It also returns the lookup conditions recognized from user's speech input. To look up schedules, have your client call a local app or provide an interface for the task.

### Payload field

| Field name       | Type    | Field description                     | Required |
|---------------|---------|-----------------------------|---------|
| `period`        | string  | The smallest unit of period recognized from user's speech input. The end time of the lookup period is set to the value of `scheduledTime` added by `period`. <ul><li><code>"none"</code>: No period</li><li><code>"year"</code>: 1 year</li><li><code>"month"</code>: 1 month</li><li><code>"week"</code>: 1 week</li><li><code>"day"</code>: 1 day</li><li><code>"hour"</code>: 1 hour</li><li><code>"minute"</code>: 1 minute</li></ul>                | Yes    |
| `scheduledTime` | string  | The start time of the lookup period ([ISO 8601](https://en.wikipedia.org/wiki/ISO_8601) format) | Yes    |

### Remarks
Implement exception handling to deal with the situation of receiving a unit of period that is not processable by your client. For example, if your client does not support looking up of a yearly schedule but has received `"year"` for `period`, you must handle it as an exception. If the period is undetermined, as in "Look up my schedule", `period` is set to`"none"` and `scheduledTime` is set to a current time.

### Message example

{% raw %}

```json
{
  "directive": {
    "header": {
      "namespace": "Clova",
      "name": "GetSchedule",
      "messageId": "7c2acf9a-6e5b-4012-9221-9162992aa0a6",
      "dialogRequestId": "bfd2b60f-4369-445e-b30b-ac0ebd2ef66d"
    },
    "payload": {
      "scheduledTime": "2017-05-24T15:00:00Z",
      "period": "day"
    }
  }
}
```

{% endraw %}

### See also
* [`Clova.AddSchedule`](#AddSchedule)
* [`Clova.CountSchedule`](#CountSchedule)
* [`Clova.DeleteSchedule`](#DeleteSchedule)

## Hello directive {#Hello}

Notifies your client that a downchannel connection has been established. This directive message lets you confirm that the [connection attempt](/CIC/Guides/Interact_with_CIC.md#CreateConnection) has succeeded for the Clova service.

### Payload field

None.

### Remarks
This directive message does not have a dialog ID(`dialogRequestId`).

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

## RenderMemoList directive {#RenderMemoList}

Instructs your client to display a list of memos. It also returns a list of memos obtained by recognizing user's speech input.

### Payload field

| Field name       | Type    | Field description                     | Required |
|---------------|---------|-----------------------------|---------|
| `memo[]`           | object array | An object array containing a list of memos                                         | Yes    |
| `memo[].content`   | string  |     Content of the memo to display                                                      | Yes    |
| `memo[].id`        | string       | The ID of the memo to display                                                       | Yes    |
| `memo[].timestamp` | string       | The time when the memo was created ([ISO 8601](https://en.wikipedia.org/wiki/ISO_8601) format) | Yes    |

### Message example

{% raw %}

```json
{
  "directive": {
    "header": {
      "namespace": "Clova",
      "name": "RenderMemoList",
      "messageId": "18e242fb-fca3-4e42-b226-bc0130e94698",
      "dialogRequestId": "c8736000-b929-4000-aba3-6fbf008c81a8"
    },
    "payload": {
      "memo": [
        {
          "id": "105ab3125-bb08-4b36-980a-47fb46c25fc",
          "content": "홍길동 키는 175cm",
          "timestamp": "2017-05-22T11:13:49Z"
        },
        {
          "id": "b3637783-2357-4a78-906b-ba765b125eeb",
          "content": "와이파이 비밀번호 1234",
          "timestamp": "2017-05-22T11:12:12Z"
        }
      ]
    }
  }
}
```

{% endraw %}

### See also
* [`Clova.AddMemo`](#AddMemo)
* [`Clova.DeleteMemo`](#DeleteMemo)
* [`Clova.GetMemo`](#GetMemo)
* [`Clova.RenderReminderList`](#RenderReminderList)
* [`Clova.RenderTemplate`](#RenderTemplate)
* [`Clova.RenderText`](#RenderText)
* [`Memo.Get`](/CIC/References/APIs/Memo.md#Get)

## RenderReminderList directive {#RenderReminderList}

Instructs your client to display a list of reminders. It also returns a list of reminders obtained by recognizing user's speech input.

### Payload field

| Field name       | Type    | Field description                     | Required |
|---------------|---------|-----------------------------|---------|
| `reminder[]`         | object array | An object array containing a list of reminders | Yes    |
| `reminder[].content` | string       | Content of the reminder to display              | Yes    |
| `reminder[].done`    | boolean      | Whether the reminder was completed or not           | Yes    |
| `reminder[].id`      | string       | The ID of the reminder to display               | Yes    |

### Message example

{% raw %}

```json
{
  "directive": {
    "header": {
      "namespace": "Clova",
      "name": "RenderReminderList",
      "messageId": "0a44ccbb-7a62-4599-ab73-a07fcdef2f51",
      "dialogRequestId": "8d6556b1-31a7-4a7d-a00b-097be11906a4"
    },
    "payload": {
      "reminder": [
        {
          "id": "100ab3901-bb08-4b36-980a-47fb46c25fc",
          "content": "비타민 먹기",
          "done": false
        },
        {
          "id": "266008ed-2ec2-45f1-bdad-5c8ece8fff50",
          "content": "계좌이체하기",
          "done": false
        }
      ]
    }
  }
}
```

{% endraw %}

### See also
* [`Clova.AddReminder`](#AddReminder)
* [`Clova.DeleteReminder`](#DeleteReminder)
* [`Clova.GetReminder`](#GetReminder)
* [`Clova.RenderMemoList`](#RenderMemoList)
* [`Clova.RenderTemplate`](#RenderTemplate)
* [`Clova.RenderText`](#RenderText)
* [`Reminder.Get`](/CIC/References/APIs/Reminder.md#Get)

## RenderTemplate directive {#RenderTemplate}

Instructs your client to display data using a content template. It also returns the content obtained by recognizing user's speech input.

### Payload field
The format of the `payload` field can change depending which type of [content template](/CIC/References/Content_Templates.md) is used. Available content templates are as follows.

* Templates for content UI types
  * [CardList](/CIC/References/ContentTemplates/CardList.md)
  * [ImageList](/CIC/References/ContentTemplates/ImageList.md)
  * [ImageText](/CIC/References/ContentTemplates/ImageText.md)
  * [Text](/CIC/References/ContentTemplates/Text.md)

* Templates for route directions
  * [CarRoute](/CIC/References/ContentTemplates/CarRoute.md)
  * [TransportationRoute](/CIC/References/ContentTemplates/TransportationRoute.md)

* Templates for weather forecast
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
* [`Clova.RenderMemoList`](#RenderMemoList)
* [`Clova.RenderReminderList`](#RenderReminderList)
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
* [`Clova.RenderMemoList`](#RenderMemoList)
* [`Clova.RenderReminderList`](#RenderReminderList)
* [`Clova.RenderTemplate`](#RenderTemplate)

## StartExtension directive {#StartExtension}

Instructs your client to start a specified extension. When a StartExtension directive message is returned, have your client start the extension that matches to a specified value.

### Payload field

| Field name       | Type    | Field description                     | Required |
|---------------|---------|-----------------------------|---------|
| `extension`     | string  | The name of the extension to start          | Yes     |

### Remarks

The server currently provides an extension called the Freetalk mode by default. The Freetalk mode is available only in English at the moment. You can start the mode by saying a trigger word, such as "Start a conversation in English". Then, the `StartExtension` directive message returns `"freetalking"` in the `extension` field.

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
