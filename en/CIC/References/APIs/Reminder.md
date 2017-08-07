# Reminder

Creates, looks up or deletes user's reminders. The Reminder API provides the following event and directive messages.

| Message name  | Message type  | Message description  |
|------------------|-----------|---------------------------------------------|
| [Created](#Created) | Event  | Requests CIC to create a specified reminder.  |
| [Deleted](#Deleted) | Event  | Requests CIC to delete a specified reminder.  |
| [Get](#Get)  | Event  | Requests CIC to get a full list of reminders created by a user.  |
| [Updated](#Updated) | Event  | Requests CIC to update a specified reminder.  |

## Created event {#Created}
Requests CIC to create a specified reminder. Send this event message in the following scenario.

1. Your client sends CIC user's speech requesting to create a reminder, using a [SpeechRecognizer.Recognize](/CIC/References/APIs/SpeechRecognizer.md#Recognize) event message.
2. The Clova platform recognizes the reminder creation request and CIC returns it to your client, using a [Clova.AddReminder](/CIC/References/APIs/Clova.md#AddReminder) directive message.
3. Your client displays the reminder creation request to confirm the intent of the user.
4. Your client receives final confirmation from the user.
  * When the user accepts reminder creation: You send a Reminder.Created event message to CIC.
  * When the user rejects reminder creation: You do not have to send any event message.

### Context field

None

### Payload field
| Field name  | Type  | Field description  | Required |
|---------------|---------|-----------------------------|---------|
| content  | string  | Content of a reminder to add  | Yes  |
| done  | boolean | Whether the reminder was completed or not  | No  |
| id  | string  | ID of a reminder to add  | Yes  |

### Remarks
* Depending on your UX design (usability), you may skip the scenario step 3, 4 and directly proceed to the step of sending the event message to CIC.

* You must return the result of sending this event message to CIC. For example, display messages such as "Created a reminder" or "Canceled reminder creation."

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


## Deleted event {#Deleted}

Requests CIC to delete a specified reminder. Send this event message in the following scenario.

1. Your client sends CIC user's speech requesting to delete a reminder, using a [SpeechRecognizer.Recognize](/CIC/References/APIs/SpeechRecognizer.md#Recognize) event message.
2. The Clova platform recognizes the reminder deletion request and CIC returns it to your client, using a [Clova.DeleteReminder](/CIC/References/APIs/Clova.md#DeleteReminder) directive message.
3. Your client displays the reminder deletion request to confirm the intent of the user.
4. Your client receives final confirmation from the user.
  * When the user accepts reminder deletion: You send a Reminder.Deleted event message to CIC.
  * When the user rejects reminder deletion: You do not have to send any event message.

### Context field

None

### Payload field

| Field name  | Type  | Field description  | Required |
|---------------|---------|-----------------------------|---------|
| id  | string  | ID of a reminder to delete  | Yes  |

### Remarks
* Depending on your UX design (usability), you may skip the scenario step 3, 4 and directly proceed to the step of sending the event message to CIC.

* You must return the result of sending this event message to CIC. For example, display messages such as "Deleted the reminder" or "Canceled reminder deletion."

* Deleting a reminder requires the process of selecting the reminder to delete. This means that you may have to send CIC a [Reminder.Get](#Get) event message first so that the user can see a list of reminders.

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

## Get event {#Get}

Requests CIC for information of all reminders. Send this event message in the following scenario.

1. Your client sends CIC user's speech requesting to look up reminders, using a [SpeechRecognizer.Recognize](/CIC/References/APIs/SpeechRecognizer.md#Recognize) event message.
2. The Clova platform recognizes the reminder lookup request and CIC returns it to your client, using a [Clova.GetReminder](/CIC/References/APIs/Clova.md#GetReminder) directive message.
3. Your client displays the reminder lookup request to confirm the intent of the user.
4. Your client receives final confirmation from the user.
  * When the user accepts reminder lookup: You send a Reminder.Get event message to CIC.
  * When the user rejects reminder lookup: You do not have to send any event message.

### Context field

None

### Payload field

None

### Remarks
* Depending on your UX design (usability), you may skip the scenario step 3, 4 and directly proceed to the step of sending the event message to CIC.

* You must return the result of sending this event message to CIC. For example, display messages such as "Looking up reminders" or "Canceled reminder lookup."

* After sending a Get event message to CIC, a list of reminders is returned, using a [Clova.RenderReminderList](/CIC/References/APIs/Clova.md#RenderReminderList) directive message.

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

## Updated event {#Updated}

Requests CIC to update a specified reminder.

### Context field

None

### Payload field

| Field name  | Type  | Field description  | Required |
|---------------|---------|-----------------------------|---------|
| content  | string  | Content of a reminder to update  | Yes  |
| id  | string  | ID of a reminder to update  | Yes  |

### Remarks

* To update a reminder, the user must make changes to the reminder on a UI screen, not with speech input. This means that the request does not require a preceding scenario, such as [reminder creation](#Created) or [reminder deletion](#Deleted).

* Be noted that an Updated event message changes the entire payload. This means that, if the message has any field left empty, such field will be replaced with an empty value. Make sure not to send only those fields to be updated. For example, if you send only the *done* field, the *content* field will be filled with an empty value.

* You can check field values for each reminder when a [Clova.RenderReminderList](/CIC/References/APIs/Clova.md#RenderReminderList) directive message is returned in response to a [Reminder.Get](#Get) event message.

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