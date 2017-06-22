# Clova

The Clova API consists of a set of Direct messages that delivers the recognized result of a client request. When a user request is sent using a [SpeechRecognizer.Recognize](/CIC/References/APIs/SpeechRecognizer.md#Recognize) Event message, Clova analyzes the meaning. CIC, based on the recognized result, sends the following Directive messages to your client. Your client must process these Directive messages to provide the functionalities of Clova to your users.

| Message name  | Message type  | Message description  |
|------------------|-----------|---------------------------------------------|
| [AddMemo](#AddMemo)  | Directive | Instructs your client to add a new memo.  |
| [AddReminder](#AddReminder)  | Directive | Instructs your client to add a new reminder.  |
| [AddSchedule](#AddSchedule)  | Directive | Instructs your client to add a new schedule.  |
| [CountSchedule](#CountSchedule)  | Directive | Instructs your client to count the number of schedules within the specified period. |
| [DeleteMemo](#DeleteMemo)  | Directive | Instructs your client to delete a memo.  |
| [DeleteReminder](#DeleteReminder)  | Directive | Instructs your client to delete a reminder.  |
| [DeleteSchedule](#DeleteSchedule)  | Directive | Instructs your client to delete a schedule.  |
| [FinishExtension](#FinishExtension)  | Directive | Instructs your client to finish an extension.  |
| [GetMemo](#GetMemo)  | Directive | Instructs your client to look up a memo.  |
| [GetReminder](#GetReminder)  | Directive | Instructs your client to look up a reminder.  |
| [GetSchedule](#GetSchedule)  | Directive | Instructs your client to look up a schedule.  |
| [RenderMemoList](#RenderMemoList)  | Directive | Instructs your client to display the list of memos.  |
| [RenderReminderList](#RenderReminderList) | Directive | Instructs your client to display the list of reminders.  |
| [RenderTemplate](#RenderTemplate)  | Directive | Instructs your client to display a template.  |
| [RenderText](#RenderText)  | Directive | Instructs your client to display a text.  |
| [StartExtension](#StartExtension)  | Directive | Instructs your client to start an extension.  |



## AddMemo Directive {#AddMemo}

Instructs your client to add a new memo. The content of the memo recognized from user's speech input is delivered together.

### Payload field

| Field name  | Type  | Field description  | Required |
|---------------|---------|-----------------------------|---------|
| content  | string  | The content of the memo to add  | Yes  |
| id  | string  | The ID of the memo to add  | Yes  |

### Remarks

When a new reminder is created, the result should be reported to CIC using a [Memo.Created](/CIC/References/APIs/Memo.md#Created) Event message.

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
* [Clova.DeleteMemo](#DeleteMemo)
* [Clova.GetMemo](#GetMemo)
* [Clova.RenderMemoList](#RenderMemoList)
* [Memo.Created](/CIC/References/APIs/Memo.md#Created)

## AddReminder Directive {#AddReminder}

Instructs your client to add a new reminder. The content of the reminder recognized from user's speech input is delivered together.

### Payload field

| Field name  | Type  | Field description  | Required |
|---------------|---------|-----------------------------|---------|
| content  | string  | The content of the reminder to add  | Yes  |
| id  | string  | The ID of the reminder to add  | Yes  |

### Remarks

When a new reminder is added, the result should be reported to CIC using a [Reminder.Created](/CIC/References/APIs/Reminder.md#Created) Event message.

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
* [Clova.DeleteReminder](#DeleteReminder)
* [Clova.GetReminder](#GetReminder)
* [Clova.RenderReminderList](#RenderReminderList)
* [Reminder.Created](/CIC/References/APIs/Reminder.md#Created)

## AddSchedule Directive {#AddSchedule}

Instructs your client to add a new schedule. The content of the schedule recognized from user's speech input is delivered together. Your client should call a local app for schedule management, or provide an interface for the functionality.

### Payload field

| Field name  | Type  | Field description  | Required |
|---------------|---------|-----------------------------|---------|
| content  | string | The content of the schedule  | No  |
| id  | string | The ID of the schedule to add  | Yes  |
| period  | string | The smallest unit of period recognized from user's speech input. Schedule end time is set to the the value of *scheduledTime* added by *period*. <ul><li>"none": Unknown period</li><li>"year": 1 year</li><li>"month": 1 month</li><li>"week": 1 week</li><li>"day": 1 day</li><li>"hour": 1 hour</li><li>"minute": 1 minute</li></ul>  | Yes  |
| scheduledTime | string | The start time of the schedule to add ([ISO 8601](https://en.wikipedia.org/wiki/ISO_8601) format) | Yes  |


### Remarks

If your client receives a unit of period it does not support, proper exception handling must be implemented. For example, if your client does not support adding of a yearly schedule but received "year" for *period*, it must be handled as an exception. If your client cannot know the period, as in "Add a schedule for me," *period* is set to "none" and *scheduledTime* is set to the current time.

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

* [Clova.CountSchedule](#CountSchedule)
* [Clova.DeleteSchedule](#DeleteSchedule)
* [Clova.GetSchedule](#GetSchedule)

## CountSchedule Directive {#CountSchedule}

Instructs your client to count the number of schedules that match the specified condition. The lookup condition recognized from user's speech input is delivered together. Your client should find out the number of schedules that match the specified condition using a local app for schedule management.

### Payload field

| Field name  | Type  | Field description  | Required |
|---------------|---------|-----------------------------|---------|
| period  | string  | The smallest unit of period recognized from user's speech input. The end time of the period for schedule lookup is set to the value of *scheduledTime* added by *period*. <ul><li>"none": Unknown period</li><li>"year": 1 year</li><li>"month": 1 month</li><li>"week": 1 week</li><li>"day": 1 day</li><li>"hour": 1 hour</li><li>"minute": 1 minute</li></ul>  | Yes  |
| scheduledTime | string  | The start time of the period for schedule lookup ([ISO 8601](https://en.wikipedia.org/wiki/ISO_8601) format) | Yes  |

### Remarks

If your client receives a unit of period it does not support, proper exception handling must be implemented. For example, if your client does not support looking up of a yearly schedule but received "year" for *period*, it must be handled as an exception. If your client cannot know the period, as in "How many schedules are there," *period* is set to "none" and *scheduledTime* is set to the current time.


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
* [Clova.AddSchedule](#AddSchedule)
* [Clova.DeleteSchedule](#DeleteSchedule)
* [Clova.GetSchedule](#GetSchedule)

## DeleteMemo Directive {#DeleteMemo}

Instructs your client to delete a memo. When your client receives a DeleteMemo Directive message, it should provide a proper interface with which your user can delete the memo.

### Payload field

None

### Remarks

When a memo is deleted, the result should be reported to CIC using a [Memo.Deleted](/CIC/References/APIs/Memo.md#Deleted) Event message.

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
* [Clova.AddMemo](#AddMemo)
* [Clova.GetMemo](#GetMemo)
* [Clova.RenderMemoList](#RenderMemoList)
* [Memo.Deleted](/CIC/References/APIs/Memo.md#Deleted)

## DeleteReminder Directive {#DeleteReminder}

Instructs your client to delete a reminder. When your client receives a DeleteReminder Directive message, it should provide a proper interface with which your user can delete the reminder.

### Payload field

None

### Remarks

When a reminder is deleted, the result should be reported to CIC using a [Reminder.Deleted](/CIC/References/APIs/Reminder.md#Deleted) Event message.

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
* [Clova.AddReminder](#AddReminder)
* [Clova.GetReminder](#GetReminder)
* [Clova.RenderReminderList](#RenderReminderList)
* [Reminder.Deleted](/CIC/References/APIs/Reminder.md#Deleted)

## DeleteSchedule Directive {#DeleteSchedule}

Instructs your client to delete a schedule. The condition recognized from user's speech input is delivered together. Your client should call a local app for schedule management to delete a schedule that matches the specified condition, or provide an interface for the functionality.

### Payload field

| Field name  | Type  | Field description  | Required |
|---------------|---------|-----------------------------|---------|
| period  | string  | The smallest unit of period recognized from user's speech input. The end time of the period for schedule deletion is set to the value of *scheduledTime* added by *period*. <ul><li>"none": Unknown period</li><li>"year": 1 year</li><li>"month": 1 month</li><li>"week": 1 week</li><li>"day": 1 day</li><li>"hour": 1 hour</li><li>"minute": 1 minute</li></ul>  | Yes  |
| scheduledTime | string  | The start time of the period for schedule deletion ([ISO 8601](https://en.wikipedia.org/wiki/ISO_8601) format) | Yes  |

### Remarks

If your client receives a unit of period it does not support, proper exception handling must be implemented. For example, if your client does not support deleting of a weekly schedule but received "week" for *period*, it must be handled as an exception. If your client cannot know the period, as in "Delete my schedule," *period* is set to "none" and *scheduledTime* is set to the current time.

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
* [Clova.AddSchedule](#AddSchedule)
* [Clova.CountSchedule](#CountSchedule)
* [Clova.GetSchedule](#GetSchedule)

## FinishExtension Directive {#FinishExtension}

Instructs your client to finish an extension. When your client receives a FinishExtension Directive message, it should finish the extension that corresponds to the specified value.

### Payload field

| Field name  | Type  | Field description  | Required |
|---------------|---------|-----------------------------|---------|
| extension  | string  | The name of the extension to finish  | Yes  |

### Remarks

The server supports an extension called Freetalk mode by default. The Freetalk mode is available only in English at the moment. The mode is can be finished with a trigger word, "See you later". At this point, "freetalking" is passed to the *extension* field of the FinishExtension Directive message.

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
* [Clova.StartExtension](#StartExtension)

## GetMemo Directive {#GetMemo}

Instructs your client to look up a memo. Your client should call a local app to look up a memo, or provide an interface for the functionality.

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
* [Clova.AddMemo](#AddMemo)
* [Clova.DeleteMemo](#DeleteMemo)
* [Clova.GetMemo](#GetMemo)
* [Clova.RenderMemoList](#RenderMemoList)
* [Memo.Get](/CIC/References/APIs/Memo.md#Get)

## GetReminder Directive {#GetReminder}

Instructs your client to look up a reminder. Your client should call a local app to look up a reminder, or provide an interface for the functionality.

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
* [Clova.AddReminder](#AddReminder)
* [Clova.DeleteReminder](#DeleteReminder)
* [Clova.RenderReminderList](#RenderReminderList)
* [Reminder.Get](/CIC/References/APIs/Reminder.md#Get)

## GetSchedule Directive {#GetSchedule}

Instructs your client to look up a schedule. The lookup condition recognized from user's speech input is delivered together. Your client should call a local app to look up a reminder, or provide an interface for the functionality.

### Payload field

| Field name  | Type  | Field description  | Required |
|---------------|---------|-----------------------------|---------|
| period  | string  | The smallest unit of period recognized from user's speech input. The end time of the period for schedule lookup is set to the value of *scheduledTime* added by *period*. <ul><li>"none": Unknown period</li><li>"year": 1 year</li><li>"month": 1 month</li><li>"week": 1 week</li><li>"day": 1 day</li><li>"hour": 1 hour</li><li>"minute": 1 minute</li></ul>  | Yes  |
| scheduledTime | string  | The start time of the period for schedule lookup ([ISO 8601](https://en.wikipedia.org/wiki/ISO_8601) format) | Yes  |

### Remarks
If your client receives a unit of period it does not support, proper exception handling must be implemented. For example, if your client does not support looking up of a yearly schedule but received "year" for *period*, it must be handled as an exception. If your client cannot know the period, as in "Look up my schedule," *period* is set to "none" and *scheduledTime* is set to the current time.

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
* [Clova.AddSchedule](#AddSchedule)
* [Clova.CountSchedule](#CountSchedule)
* [Clova.DeleteSchedule](#DeleteSchedule)

## RenderMemoList Directive {#RenderMemoList}

Instructs your client to display the list of memos. The list of memos obtained as a result of recognizing user's speech input is delivered together.

### Payload field

| Field name  | Type  | Field description  | Required |
|---------------|---------|-----------------------------|---------|
| memo[]  | object array | The object array containing the list of memos  | Yes  |
| memo[].content  | string  | The content of memo to display  | Yes  |
| memo[].id  | string  | The ID of the memo to display  | Yes  |
| memo[].timestamp | string  | The time of the memo creation ([ISO 8601](https://en.wikipedia.org/wiki/ISO_8601) format) | Yes  |

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
* [Clova.AddMemo](#AddMemo)
* [Clova.DeleteMemo](#DeleteMemo)
* [Clova.GetMemo](#GetMemo)
* [Clova.RenderReminderList](#RenderReminderList)
* [Clova.RenderTemplate](#RenderTemplate)
* [Clova.RenderText](#RenderText)
* [Memo.Get](/CIC/References/APIs/Memo.md#Get)

## RenderReminderList Directive {#RenderReminderList}

Instructs your client to display the list of reminders. The list of reminders obtained as a result of recognizing user's speech input is delivered together.

### Payload field

| Field name  | Type  | Field description  | Required |
|---------------|---------|-----------------------------|---------|
| reminder[]  | object array | The object array containing the list of reminders | Yes  |
| reminder[].content | string  | The content of the reminder to display  | Yes  |
| reminder[].done  | boolean  | Whether the reminder was completed or not  | Yes  |
| reminder[].id  | string  | The ID of the reminder to display  | Yes  |

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
* [Clova.AddReminder](#AddReminder)
* [Clova.DeleteReminder](#DeleteReminder)
* [Clova.GetReminder](#GetReminder)
* [Clova.RenderMemoList](#RenderMemoList)
* [Clova.RenderTemplate](#RenderTemplate)
* [Clova.RenderText](#RenderText)
* [Reminder.Get](/CIC/References/APIs/Reminder.md#Get)

## RenderTemplate Directive {#RenderTemplate}

Instructs your client to display data using a Content Template. The content obtained as a result of recognizing user's speech input is delivered together.

### Payload field
The format of the *payload* field can be different depending on the types of [Content Template](/CIC/References/Content_Templates.md). Currently available Content Templates are as follows.

* [Image List](/CIC/References/Content_Templates.md#ImageList)
* [Image & Text](/CIC/References/Content_Templates.md#ImageText)
* [Card List](/CIC/References/Content_Templates.md#CardList)
* [Text](/CIC/References/Content_Templates.md#Text)

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
* [Clova.RenderMemoList](#RenderMemoList)
* [Clova.RenderReminderList](#RenderReminderList)
* [Clova.RenderText](#RenderText)
* [Content Template](/CIC/References/Content_Templates.md)

## RenderText Directive {#RenderText}

Instructs your client to display the text message. The text requested by the user is delivered together.

### Payload field

| Field name  | Type  | Field description  | Required |
|---------------|---------|-----------------------------|---------|
| text  | string  | The text delivered according to the user request  | Yes  |

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
* [Clova.RenderMemoList](#RenderMemoList)
* [Clova.RenderReminderList](#RenderReminderList)
* [Clova.RenderTemplate](#RenderTemplate)

## StartExtension Directive {#StartExtension}

Instructs your client to start an extension. When your client receives a StartExtension Directive message, it starts the extension that corresponds to the specified value.

### Payload field

| Field name  | Type  | Field description  | Required |
|---------------|---------|-----------------------------|---------|
| extension  | string  | The name of the extension to start  | Yes  |

### Remarks

The server supports an extension called Freetalk mode by default. The Freetalk mode is available only in English at the moment. You can start the mode by saying a trigger word such as "Start conversation in English". At this point, "freetalking" is passed to the *extension* field of the StartExtension Directive message.

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

- [Clova.FinishExtension](#FinishExtension)
