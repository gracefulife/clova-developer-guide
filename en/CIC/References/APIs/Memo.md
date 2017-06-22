# Memo

This API let's your client create, look up, or delete a user's memo. The Memo API provides the following Event and Directive message.

| Message name  | Message type  | Message description  |
|------------------|-----------|---------------------------------------------|
| [Created](#Created) | Event  | Asks CIC to creat a memo. |
| [Deleted](#Deleted) | Event  | Asks CIC to delete a memo. |
| [Get](#Get) | Event  | Asks CIC to provide the full list of memos created by the user. |
| [Updated](#Updated) | Event  | Asks CIC to update a memo. |

## Created Event {#Created}
Asks CIC to create a memo. This Event message is sent in the following scenario.

1. Using a [SpeechRecognizer.Recognize](/CIC/References/APIs/SpeechRecognizer.md#Recognize) Event message, your client transmits user's speech input to CIC asking to create a memo.
2. Once the Clova platform recognizes the request, it sends the request to client using a [Clova.AddMemo](/CIC/References/APIs/Clova.md#AddMemo) Directive message.
3. Your client displays the memo creation request to confirm the intent of the user.
4. Your client receives final confirmation from the user.
  * When the user accepts memo creation: A Memo.Created Event message is sent to CIC.
  * When the user rejects memo creation: No Event message is sent.

### Context field

None

### Payload field
| Field name  | Type  | Field description  | Required |
|---------------|---------|-----------------------------|---------|
| content  | string  | The content of the memo to add  | Yes  |
| id  | string  | The ID of the memo to add  | Yes  |

### Remarks
* Depending on your UX design (usability), you may skip the scenario step 3 and 4 and proceed to send an Event message to CIC.

* When your client sends an Event message to CIC, it must return the result of the event. For example, your client should display a message such as "Created a memo" or "Canceled memo creation."

### Message example

{% raw %}

```json
{
  "context": [],
  "event": {
    "header": {
      "namespace": "Memo",
      "name": "Created",
      "dialogRequestId": "277b40c3-b046-4f61-a551-783b1547e7b7",
      "messageId": "4e4080d6-c440-498a-bb73-ae86c6312806"
    },
    "payload": {
      "id": "67883659-9945-4d63-bc55-4d669da833ea",
      "content": "와이파이 비밀번호 1234",
    }
  }
}
```
{% endraw %}

### See also
* [Clova.AddMemo](/CIC/References/APIs/Clova.md#AddMemo)
* [SpeechRecognizer.Recognize](/CIC/References/APIs/SpeechRecognizer.md#Recognize)


## Deleted Event {#Deleted}

Asks CIC to delete a memo. This Event message is sent in the following scenario.

1. Using a [SpeechRecognizer.Recognize](/CIC/References/APIs/SpeechRecognizer.md#Recognize) Event message, your client transmits user's speech input to CIC asking to delete a memo.
2. Once the Clova platform recognizes the request, it sends the request to your client using a [Clova.DeleteMemo](/CIC/References/APIs/Clova.md#DeleteMemo) Directive message.
3. Your client displays the memo deletion request to confirm the intent of the user.
4. Your client receives final confirmation from the user.
  * When the user accepts memo deletion: A Memo.Deleted Event message is sent to CIC.
  * When the user rejects memo deletion: No Event message is sent.

### Context field

None

### Payload field

| Field name  | Type  | Field description  | Required |
|---------------|---------|-----------------------------|---------|
| id  | string  | The ID of the memo to delete  | Yes  |

### Remarks
* Depending on your UX design (usability), you may skip the scenario step 3 and 4 and proceed to send an Event message to CIC.

* When your client sends an Event message to CIC, it must return the result of the event. For example, your client should display a message such as "Deleted the memo" or "Canceled memo deletion."

* To delete a memo, the user has to select a memo to delete. To do so, you client may have to send a preceding Event message ([Memo.Get](#Get)) to look up memos so that the user can view the list of memos.

### Message example

{% raw %}

```json
{
  "context": [],
  "event": {
    "header": {
      "namespace": "Memo",
      "name": "Deleted",
      "dialogRequestId": "4cc0d166-7580-4158-bfbc-1b9234b9995f",
      "messageId": "c7dd9664-7594-4a17-ad58-c88fdaf80e61"
    },
    "payload": {
      "id": "67883659-9945-4d63-bc55-4d669da833ea"
    }
  }
}
```

{% endraw %}

### See also
* [Clova.DeleteMemo](/CIC/References/APIs/Clova.md#DeleteMemo)
* [Memo.Get](#Get)
* [SpeechRecognizer.Recognize](/CIC/References/APIs/SpeechRecognizer.md#Recognize)

## Get Event {#Get}

Asks CIC to provide information of all memos. This Event message is sent in the following scenario.

1. Using a [SpeechRecognizer.Recognize](/CIC/References/APIs/SpeechRecognizer.md#Recognize) Event message, your client transmits user's speech input to CIC asking to look up memos.
2. Once the Clova platform recognizes the request, it sends the request to your client using a [Clova.GetMemo](/CIC/References/APIs/Clova.md#GetMemo) Directive message.
3. Your client displays the memo lookup request to confirm the intent of the user.
4. Your client receives final confirmation from the user.
  * When the user accepts memo lookup: A Memo.Get Event message is sent to CIC.
  * When the user rejects memo lookup: No Event message is sent.

### Context field

None

### Payload field

None

### Remarks
* Depending on your UX design (usability), you may skip the scenario step 3 and 4 and proceed to send an Event message to CIC.

* When your client sends an Event message to CIC, it must return the result of the event. For example, your client should display a message such as "Looking up memos" or "Canceled memo lookup."

* Once a Get Event message is sent to CIC, the user's memo list is delivered using a [Clova.RenderMemoList](/CIC/References/APIs/Clova.md#RenderMemoList) Directive message.

### Message example

{% raw %}

```json
{
  "context": [],
  "event": {
    "header": {
      "namespace": "Memo",
      "name": "Get",
      "dialogRequestId": "2315186e-7242-47f0-9673-b4a84118d513",
      "messageId": "c6c5cbf2-8452-49cd-8af4-6437183cbf30"
    },
    "payload": {}
  }
}
```

{% endraw %}

### See also
* [Clova.GetMemo](/CIC/References/APIs/Clova.md#GetMemo)
* [Clova.RenderMemoList](/CIC/References/APIs/Clova.md#RenderMemoList)
* [SpeechRecognizer.Recognize](/CIC/References/APIs/SpeechRecognizer.md#Recognize)

## Updated Event {#Updated}

Asks CIC to update a memo.

### Context field

None

### Payload field

| Field name  | Type  | Field description  | Required |
|---------------|---------|-----------------------------|---------|
| content  | string  | The content of the memo to update  | Yes  |
| id  | string  | The ID of the memo to update  | Yes  |

### Remarks

* Updating a memo cannot be done by speech input. The request must be sent by directly changing the content on a UI screen. As such, no preceding scenarios are necessary such as [Memo creation](#Created) or [Memo deletion](#Deleted).

* An Updated Event message changes the entire payload. So, if the message has any field left empty, it will change its corresponding field to an empty value. Be cautious not to send only the fields that need update.

* Your client can check the field values in each memo when a [Clova.RenderMemoList](/CIC/References/APIs/Clova.md#RenderMemoList) Directive message is sent in response to a [Memo.Get](#Get) Event message.

### Message example

{% raw %}

```json
{
  "context": [],
  "event": {
    "header": {
      "namespace": "Memo",
      "name": "Updated",
      "dialogRequestId": "ec270ebc-7329-4c7c-9440-1d9ceb73e345",
      "messageId": "9c5a243f-21ed-4c37-bfd3-986bea8aab62"
    },
    "payload": {
      "id": "67883659-9945-4d63-bc55-4d669da833ea",
      "content": "와이파이 비밀번호 12345678",
    }
  }
}
```

{% endraw %}

### See also
* [Memo.Get](#Get)
* [Clova.RenderMemoList](/CIC/References/APIs/Clova.md#RenderMemoList)
