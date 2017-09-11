# Memo

Memo는 사용자의 메모를 생성/조회/삭제할 때 사용되는 네임스페이스입니다. Memo가 제공하는 이벤트 메시지와 지시 메시지는 다음과 같습니다.

| 메시지 이름         | 메시지 타입  | 메시지 설명                                   |
|------------------|-----------|---------------------------------------------|
| [`Created`](#Created) | Event  | CIC에 특정 메모를 등록하도록 요청합니다. |
| [`Deleted`](#Deleted) | Event  | CIC에 특정 메모를 삭제하도록 요청합니다. |
| [`Get`](#Get) | Event  | CIC에 사용자가 생성한 모든 메모 목록을 요청합니다. |
| [`Updated`](#Updated) | Event  | CIC에 특정 메모를 갱신하도록 요청합니다. |

## Created event {#Created}
CIC에 특정 메모를 등록하도록 요청합니다. 이 이벤트 메시지를 보내기 위해 필요한 사전 시나리오는 다음과 같습니다.

1. 클라이언트는 [`SpeechRecognizer.Recognize`](/CIC/References/CICInterface/SpeechRecognizer.md#Recognize) 이벤트 메시지로 메모 생성을 요청한 사용자 음성을 CIC로 전송합니다.
2. CIC는 Clova 플랫폼에서 인식된 메모 생성 요청을 [`Clova.AddMemo`](/CIC/References/CICInterface/Clova.md#AddMemo) 지시 메시지를 통해 클라이언트에 전달합니다.
3. 클라이언트는 인식된 사용자의 메모 생성 요청을 표시하여 의도한 것이 맞는지 확인합니다.
4. 클라이언트는 사용자로부터 최종 확인을 받습니다.
   * **사용자가 메모 생성을 수락하면** `Memo.Created` 이벤트 메시지를 CIC에 전송합니다.
   * **사용자가 메모 생성을 거부하면** 따로 이벤트 메시지를 보내지 않아도 됩니다.

### Context field

필수 상태 정보 없음

### Payload field

| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|---------|
| `content`       | string  | 추가할 메모의 내용              | 필수     |
| `id`            | string  | 추가할 메모의 ID               | 필수     |

### Remarks
* 사전 시나리오의 3번, 4번 단계는 UX 디자인(사용자 편의)에 따라 생략하고 바로 이벤트 메시지를 CIC로 전송할 수도 있습니다.

* 클라이언트는 이 이벤트 메시지를 CIC로 보낼 때 수행 결과에 대한 피드백을 돌려줘야 합니다. 예를 들면, "메모가 생성되었습니다." 또는 "메모 생성이 취소되었습니다."와 같은 메시지를 표시해야 합니다.

### Message example

{% raw %}

```json
{
  "context": [],
  "event": {
    "header": {
      "namespace": "Memo",
      "name": "Created",
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
* [`Clova.AddMemo`](/CIC/References/CICInterface/Clova.md#AddMemo)
* [`SpeechRecognizer.Recognize`](/CIC/References/CICInterface/SpeechRecognizer.md#Recognize)


## Deleted event {#Deleted}

CIC에 특정 메모를 삭제하도록 요청합니다. 이 이벤트 메시지를 보내기 위해 필요한 사전 시나리오는 다음과 같습니다.

1. 클라이언트는 [`SpeechRecognizer.Recognize`](/CIC/References/CICInterface/SpeechRecognizer.md#Recognize) 이벤트 메시지로 메모 삭제를 요청한 사용자의 음성을 CIC로 전송합니다.
2. CIC는 Clova 플랫폼에서 인식된 메모 삭제 요청을 [`Clova.DeleteMemo`](/CIC/References/CICInterface/Clova.md#DeleteMemo) 지시 메시지를 통해 클라이언트에 전달합니다.
3. 클라이언트는 인식된 사용자의 메모 삭제 요청을 표시하여 의도한 것이 맞는지 확인합니다.
4. 클라이언트는 사용자로부터 최종 확인을 받습니다.
   * **사용자가 메모 삭제를 수락하면** `Memo.Deleted` 이벤트 메시지를 CIC에 전송합니다.
   * **사용자가 메모 삭제를 거부하면** 따로 이벤트 메시지를 보내지 않아도 됩니다.

### Context field

필수 상태 정보 없음

### Payload field

| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|---------|
| `id`            | string  | 삭제할 메모의 ID               | 필수     |

### Remarks
* 사전 시나리오의 3번, 4번 단계는 UX 디자인(사용자 편의)에 따라 생략하고 바로 이벤트 메시지를 CIC로 전송할 수도 있습니다.

* 클라이언트는 이 이벤트 메시지를 CIC로 보낼 때 수행 결과에 대한 피드백을 돌려줘야 합니다. 예를 들면, "메모가 삭제되었습니다." 또는 "메모 삭제가 취소되었습니다."와 같은 메시지를 표시해야 합니다.

* 사용자가 메모를 삭제하려면 우선 삭제하려는 메모를 선택하는 과정이 필요합니다. 이를 위해 우선 사용자가 메모 목록을 볼 수 있도록 메모를 조회하는 이벤트 메시지([`Memo.Get`](#Get))를 선행하여 CIC에 요청해야 할 수 있습니다.

### Message example

{% raw %}

```json
{
  "context": [],
  "event": {
    "header": {
      "namespace": "Memo",
      "name": "Deleted",
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
* [`Clova.DeleteMemo`](/CIC/References/CICInterface/Clova.md#DeleteMemo)
* [`Memo.Get`](#Get)
* [`SpeechRecognizer.Recognize`](/CIC/References/CICInterface/SpeechRecognizer.md#Recognize)

## Get event {#Get}

CIC에 모든 메모의 정보를 요청합니다. 이 이벤트 메시지를 보내기 위해 필요한 사전 시나리오는 다음과 같습니다.

1. 클라이언트는 [`SpeechRecognizer.Recognize`](/CIC/References/CICInterface/SpeechRecognizer.md#Recognize) 이벤트 메시지로 메모 조회를 요청한 사용자의 음성을 CIC로 전송합니다.
2. CIC는 Clova 플랫폼에서 인식된 메모 조회 요청을 [`Clova.GetMemo`](/CIC/References/CICInterface/Clova.md#GetMemo) 지시 메시지를 통해 클라이언트에 전달합니다.
3. 클라이언트는 인식된 사용자의 메모 조회 요청을 표시하여 의도한 것이 맞는지 확인합니다.
4. 클라이언트는 사용자로부터 최종 확인을 받습니다.
   * **사용자가 메모 조회를 수락하면** `Memo.Get` 이벤트 메시지를 CIC에 전송합니다.
   * **사용자가 메모 조회를 거부하면** 따로 이벤트 메시지를 보내지 않아도 됩니다.

### Context field

필수 상태 정보 없음

### Payload field

없음

### Remarks
* 사전 시나리오의 3번, 4번 단계는 UX 디자인(사용자 편의)에 따라 생략하고 바로 이벤트 메시지를 CIC로 전송할 수도 있습니다.

* 클라이언트는 이 이벤트 메시지를 CIC로 보낼 때 수행 결과에 대한 피드백을 돌려줘야 합니다. 예를 들면, "메모를 조회합니다." 또는 "메모 조회가 취소되었습니다."와 같은 메시지를 표시해야 합니다.

* `Memo.Get` 이벤트 메시지를 CIC로 보내면 해당 사용자의 메모 목록을 [`Clova.RenderMemoList`](/CIC/References/CICInterface/Clova.md#RenderMemoList) 지시 메시지를 통해 전달합니다.

### Message example

{% raw %}

```json
{
  "context": [],
  "event": {
    "header": {
      "namespace": "Memo",
      "name": "Get",
      "messageId": "c6c5cbf2-8452-49cd-8af4-6437183cbf30"
    },
    "payload": {}
  }
}
```

{% endraw %}

### See also
* [`Clova.GetMemo`](/CIC/References/CICInterface/Clova.md#GetMemo)
* [`Clova.RenderMemoList`](/CIC/References/CICInterface/Clova.md#RenderMemoList)
* [`SpeechRecognizer.Recognize`](/CIC/References/CICInterface/SpeechRecognizer.md#Recognize)

## Updated event {#Updated}

CIC에 특정 메모의 갱신을 요청합니다.

### Context field

필수 상태 정보 없음

### Payload field

| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|---------|
| content       | string  | 갱신할 메모 내용                | 필수     |
| id            | string  | 갱신할 메모의 ID               | 필수     |

### Remarks

* 메모 갱신은 사용자의 음성 입력이 아닌 UI 화면에서 직접 변경한 내용을 가지고 요청합니다. 따라서, [메모 생성](#Created)이나 [삭제](#Deleted)와 같이 사전 시나리오가 존재하지 않습니다.

* `Memo.Updated` 이벤트 메시지는 `payload` 전체를 변경하므로 어떤 필드 값이 비어 있으면 해당 필드는 빈 값으로 변경되므로 갱신하고자 하는 특정 필드만 보내지 않도록 유의합니다.

* 각 메모의 필드 값은 [`Memo.Get`](#Get) 이벤트 메시지의 응답으로 전달되는 [`Clova.RenderMemoList`](/CIC/References/CICInterface/Clova.md#RenderMemoList) 지시 메시지를 통해 확인할 수 있습니다.

### Message example

{% raw %}

```json
{
  "context": [],
  "event": {
    "header": {
      "namespace": "Memo",
      "name": "Updated",
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
* [`Clova.RenderMemoList`](/CIC/References/CICInterface/Clova.md#RenderMemoList)
