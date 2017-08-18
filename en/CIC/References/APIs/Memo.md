# Memo

Creates, looks up or deletes user's memos. The Memo API provides the following event and directive messages.

| Message name  | Message type  | Message description  |
|------------------|-----------|---------------------------------------------|
| [`Created`](#Created) | Event  | Requests CIC to create a specified memo. |
| [`Deleted`](#Deleted) | Event  | Requests CIC to delete a specified memo. |
| [`Get`](#Get) | Event  | Requests CIC to get a full list of memos created by a user. |
| [`Updated`](#Updated) | Event  | Requests CIC to update a specified memo. |

## Created event {#Created}
Requests CIC to create a specified memo. Send this event message in the following scenario.

1. Your client sends CIC a user's spoken request to create a memo, using a [`SpeechRecognizer.Recognize`](/CIC/References/APIs/SpeechRecognizer.md#Recognize) event message.
2. The Clova platform recognizes the memo creation request and CIC returns it to your client, using a [`Clova.AddMemo`](/CIC/References/APIs/Clova.md#AddMemo) directive message.
3. Your client displays the memo creation request to confirm the intent of the user.
4. Your client receives final confirmation from the user.
   * **When the user accepts memo creation,** you send a `Memo.Created` event message to CIC.
   * **When the user rejects memo creation,** you do not have to send any event message.

### Context field

None

### Payload field

| Field name  | Type  | Field description  | Required |
|---------------|---------|-----------------------------|---------|
| `content`  | string  | Content of the memo to add  | Yes  |
| `id`  | string  | The ID of the memo to add  | Yes  |

### Remarks
* Depending on your UX design (usability), you may skip the scenario step 3, 4 and directly proceed to the step of sending the event message to CIC.

* You must return execution results when sending this event message to CIC. For example, display messages such as "Created a memo" or "Canceled memo creation."

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
* [`Clova.AddMemo`](/CIC/References/APIs/Clova.md#AddMemo)
* [`SpeechRecognizer.Recognize`](/CIC/References/APIs/SpeechRecognizer.md#Recognize)


## Deleted event {#Deleted}

Requests CIC to delete a specified memo. Send this event message in the following scenario.

1. Your client sends CIC a user's spoken request to delete a memo, using a [`SpeechRecognizer.Recognize`](/CIC/References/APIs/SpeechRecognizer.md#Recognize) event message.
2. The Clova platform recognizes the memo deletion request and CIC returns it to your client, using a [`Clova.DeleteMemo`](/CIC/References/APIs/Clova.md#DeleteMemo) directive message.
3. Your client displays the memo deletion request to confirm the intent of the user.
4. Your client receives final confirmation from the user.
  * **When the user accepts memo deletion,** you send a `Memo.Deleted` event message to CIC.
  * **When the user rejects the memo deletion,** you do not have to send any event message.

### Context field

None

### Payload field

| Field name  | Type  | Field description  | Required |
|---------------|---------|-----------------------------|---------|
| `id`  | string  | The ID of the memo to delete  | Yes  |

### Remarks
* Depending on your UX design (usability), you may skip the scenario step 3, 4 and directly proceed to the step of sending the event message to CIC.

* You must return execution results when sending this event message to CIC. For example, display messages such as "Deleted the memo" or "Canceled memo deletion."

* Deleting a memo requires the process of selecting the memo to delete. This means that you may have to send CIC a [`Memo.Get`](#Get) event message first so that the user can view a list of memos.

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
* [`Clova.DeleteMemo`](/CIC/References/APIs/Clova.md#DeleteMemo)
* [`Memo.Get`](#Get)
* [`SpeechRecognizer.Recognize`](/CIC/References/APIs/SpeechRecognizer.md#Recognize)

## Get event {#Get}

Requests CIC for information of all memos. Send this event message in the following scenario.

1. Your client sends CIC a user's spoken request to look up memos, using a [`SpeechRecognizer.Recognize`](/CIC/References/APIs/SpeechRecognizer.md#Recognize) event message.
2. The Clova platform recognizes the memo lookup request and CIC returns it to your client, using a [`Clova.GetMemo`](/CIC/References/APIs/Clova.md#GetMemo) directive message.
3. Your client displays the memo lookup request to confirm the intent of the user.
4. Your client receives final confirmation from the user.
   * **When the user accepts memo lookup,** you send a `Memo.Get` event message to CIC.
   * **When the user rejects memo lookup,** you do not have to send any event message.

### Context field

None

### Payload field

None

### Remarks
* Depending on your UX design (usability), you may skip the scenario step 3, 4 and directly proceed to the step of sending the event message to CIC.

* You must return execution results when sending this event message to CIC. For example, display messages such as "Looking up memos" or "Canceled memo lookup."

* After you send the `Memo.Get` event message to CIC, the user's list of memos are returned through a [`Clova.RenderMemoList`](/CIC/References/APIs/Clova.md#RenderMemoList) directive message.

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
* [`Clova.GetMemo`](/CIC/References/APIs/Clova.md#GetMemo)
* [`Clova.RenderMemoList`](/CIC/References/APIs/Clova.md#RenderMemoList)
* [`SpeechRecognizer.Recognize`](/CIC/References/APIs/SpeechRecognizer.md#Recognize)

## Updated event {#Updated}

Requests CIC to update a specified memo.

### Context field

None

### Payload field

| Field name  | Type  | Field description  | Required |
|---------------|---------|-----------------------------|---------|
| content  | string  | Content of the memo to update  | Yes  |
| id  | string  | The ID of the memo to update  | Yes  |

### Remarks

* To update a memo, the user must make changes to the memo on a UI screen, not with speech input. This means that the request does not require a preceding scenario, such as [memo creation](#Created) or [memo deletion](#Deleted).

* A `Memo.Updated` event message changes the entire `payload`. This means that, if the message has any field left empty, such field will be replaced with an empty value. Make sure not to send only thos fields to update.

* You can check field values for each memo when a [`Clova.RenderMemoList`](/CIC/References/APIs/Clova.md#RenderMemoList) directive message is returned in response to the [`Memo.Get`](#Get) event message.

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
* [`Memo.Get`](#Get)
* [`Clova.RenderMemoList`](/CIC/References/APIs/Clova.md#RenderMemoList)