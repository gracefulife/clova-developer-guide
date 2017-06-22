# Reminder

This API lets your client create, look up, or delete a user's reminder. The Reminder API provides the following Event and Directive messages.

| Message name  | Message type  | Message description  |
|------------------|-----------|---------------------------------------------|
| [Created](#Created) | Event  | Asks CIC to create a reminder.  |
| [Deleted](#Deleted) | Event  | Asks CIC to delete a reminder.  |
| [Get](#Get)  | Event  | Asks CIC to provide the full list of reminders created by the user.  |
| [Updated](#Updated) | Event  | Asks CIC to update a reminder.  |

## Created Event {#Created}
Asks CIC to create a reminder. This Event message is sent in the following scenario.

1. Using a [SpeechRecognizer.Recognize](/CIC/References/APIs/SpeechRecognizer.md#Recognize) Event message, your client transmits user's speech input to CIC asking to create a reminder.
2. Once the Clova platform recognizes the request, it sends the request to your client using a [Clova.AddReminder](/CIC/References/APIs/Clova.md#AddReminder) Directive message.
3. Your client displays the reminder creation request to confirm the intent of the user.
4. Your client receives final confirmation from the user.
  * When the user accepts reminder creation: A Reminder.Created Event message is sent to CIC.
  * When the user rejects reminder creation: No Event message is sent.

### Context field

None

### Payload field
| Field name  | Type  | Field description  | Required |
|---------------|---------|-----------------------------|---------|
| content  | string  | The content of the reminder to add  | Yes  |
| done  | boolean | Whether the reminder was completed or not  | No  |
| id  | string  | The ID of the reminder to add  | Yes  |

### Remarks
* Depending on your UX design (usability), you may skip the scenario step 3 and 4 and proceed to send an Event message to CIC.

* When your client sends an Event message to CIC, it must return the result of the event. For example, your client should display a message such as "Created a reminder" or "Canceled reminder creation."

### Message example

{% raw %}

```json
{
  "context": [],
  "event": {
    "header": {
      "namespace": "Reminder",
      "name": "Created",
      "dialogRequestId": "c40588a1-7cf5-428a-aa2f-063d3932e375",
      "messageId": "447d7a2f-875c-4d70-84ce-61787811de8c"
    },
    "payload": {
      "id": "100ab3901-bb08-4b36-980a-47fb46c25fcd",
      "content": "비타민 먹기",
      "done": false
    }
  }
}
```
{% endraw %}

### See also
* [Clova.AddReminder](/CIC/References/APIs/Clova.md#AddReminder)
* [SpeechRecognizer.Recognize](/CIC/References/APIs/SpeechRecognizer.md#Recognize)


## Deleted Event {#Deleted}

Asks CIC to delete a reminder. This Event message is sent in the following scenario.

1. Using a [SpeechRecognizer.Recognize](/CIC/References/APIs/SpeechRecognizer.md#Recognize) Event message, your client transmits user's speech input to CIC asking to delete a reminder.
2. Once the request is recognized on the Clova platform, the request is sent to your client using a [Clova.DeleteReminder](/CIC/References/APIs/Clova.md#DeleteReminder) Directive message.
3. Your client displays the reminder deletion request to confirm the intent of the user.
4. Your client receives final confirmation from the user.
  * When the user accepts reminder deletion: A Reminder.Deleted Event message is sent to CIC.
  * When the user rejects reminder deletion: No Event message is sent.

### Context field

None

### Payload field

| Field name  | Type  | Field description  | Required |
|---------------|---------|-----------------------------|---------|
| id  | string  | The ID of the reminder to delete  | Yes  |

### Remarks
* Depending on your UX design (usability), you may skip the scenario step 3 and 4 and proceed to send an Event message to CIC.

* When your client sends an Event message to CIC, it must return the result of the event. For example, your client should display a message such as "Deleted a reminder" or "Canceled reminder deletion."

* To delete a reminder, the user has to select a reminder to delete. To do so, your client may have to send a preceding Event message ([Reminder.Get](#Get)) to look up reminders so that the user can view the list of reminders.

### Message example

{% raw %}

```json
{
  "context": [],
  "event": {
    "header": {
      "namespace": "Reminder",
      "name": "Deleted",
      "dialogRequestId": "004ef9d0-8b12-4be4-aef0-9558a4e12503",
      "messageId": "1ead8b31-aac4-46c6-9c6e-f6a302196065"
    },
    "payload": {
      "id": "100ab3901-bb08-4b36-980a-47fb46c25fcd"
    }
  }
}
```

{% endraw %}

### See also
* [Clova.DeleteReminder](/CIC/References/APIs/Clova.md#DeleteReminder)
* [Reminder.Get](#Get)
* [SpeechRecognizer.Recognize](/CIC/References/APIs/SpeechRecognizer.md#Recognize)

## Get Event {#Get}

Asks CIC to provide information of all reminders. This Event message is sent in the following scenario.

1. Using a [SpeechRecognizer.Recognize](/CIC/References/APIs/SpeechRecognizer.md#Recognize) Event message, your client transmits user's speech input to CIC asking to look up reminders.
2. Once the request is recognized on the Clova platform, the request is sent to your client using a [Clova.GetReminder](/CIC/References/APIs/Clova.md#GetReminder) Directive message.
3. Your client displays the reminder lookup request to confirm the intent of the user.
4. Your client receives final confirmation from the user.
  * When the user accepts reminder lookup: A Reminder.Get Event message is sent to CIC.
  * When the user rejects reminder lookup: No Event message is sent.

### Context field

None

### Payload field

None

### Remarks
* Depending on your UX design (usability), you may skip the scenario step 3 and 4 and proceed to send an Event message to CIC.

* When your client sends an Event message to CIC, it must return the result of the event. For example, your client should display a message such as "Looking up reminders" or "Canceled reminder lookup."

* Once a Get Event message is sent to CIC, the user's reminder list is delivered using a [Clova.RenderReminderList](/CIC/References/APIs/Clova.md#RenderReminderList) Directive message.

### Message example

{% raw %}

```json
{
  "context": [],
  "event": {
    "header": {
      "namespace": "Reminder",
      "name": "Get",
      "dialogRequestId": "f0d06cee-92a9-489e-a546-1f5d2e3a058d",
      "messageId": "2346313b-2b82-4522-85d8-385b43f2d981"
    },
    "payload": {}
  }
}
```

{% endraw %}

### See also
* [Clova.GetReminder](/CIC/References/APIs/Clova.md#GetReminder)
* [Clova.RenderReminderList](/CIC/References/APIs/Clova.md#RenderReminderList)
* [SpeechRecognizer.Recognize](/CIC/References/APIs/SpeechRecognizer.md#Recognize)

## Updated Event {#Updated}

Asks CIC to update a reminder.

### Context field

None

### Payload field

| Field name  | Type  | Field description  | Required |
|---------------|---------|-----------------------------|---------|
| content  | string  | The content of the reminder to update  | Yes  |
| id  | string  | The ID of the reminder to update  | Yes  |

### Remarks

* Updating a reminder cannot be done by speech input. The request must be sent by directly changing the content on a UI screen. As such, no preceding scenarios are necessary such as [Reminder creation](#Created) or [Reminder deletion](#Deleted).

* An Updated Event message changes the entire payload. So, if the message has any field left empty, it will change its corresponding field to an empty value. Be cautious not to send only the fields that need update. For example, if you send only the *done* field, the *content* field will be filled with an empty value.

* Your client can check the field values in each reminder when a [Clova.RenderReminderList](/CIC/References/APIs/Clova.md#RenderReminderList) Directive message is sent in response to a [Reminder.Get](#Get) Event message.

### Message example

{% raw %}

```json
{
  "context": [],
  "event": {
    "header": {
      "namespace": "Reminder",
      "name": "Updated",
      "dialogRequestId": "f107eac9-d8d5-4609-9892-49edb8ed4804",
      "messageId": "f1f0442f-720c-4264-b709-88f7b52dd14f"
    },
    "payload": {
      "id": "100ab3901-bb08-4b36-980a-47fb46c25fcd",
      "content": "비타민 먹기",
      "done": true
    }
  }
}
```

{% endraw %}

### See also
* [Reminder.Get](#Get)
* [Clova.RenderReminderList](/CIC/References/APIs/Clova.md#RenderReminderList)
