# Clova

클라이언트의 요청이 인식된 결과를 클라이언트로 전달하는 지시 메시지의 일부 집합입니다. 사용자의 요청이 [`SpeechRecognizer.Recognize`](/CIC/References/APIs/SpeechRecognizer.md#Recognize) 이벤트 메시지로 전달되면 Clova에서 그 의미를 분석합니다. CIC는 인식된 결과에 따라 아래 지시 메시지를 클라이언트에게 전달합니다. 클라이언트는 아래 지시 메시지들을 처리하여 Clova에서 제공하는 기능을 사용자에게 제공해야 합니다.

| 메시지 이름         | 메시지 타입  | 메시지 설명                                   |
|------------------|-----------|---------------------------------------------|
| [`AddMemo`](#AddMemo)                       | Directive | 클라이언트에게 새로운 메모를 추가하도록 지시합니다.                  |
| [`AddReminder`](#AddReminder)               | Directive | 클라이언트에게 새로운 리마인더를 추가하도록 지시합니다.               |
| [`AddSchedule`](#AddSchedule)               | Directive | 클라이언트에게 새로운 일정을 추가하도록 지시합니다.                  |
| [`CountSchedule`](#CountSchedule)           | Directive | 클라이언트에게 지정한 기간 사이에 있는 일정 개수를 확인하도록 지시합니다. |
| [`DeleteMemo`](#DeleteMemo)                 | Directive | 클라이언트에게 메모를 삭제하도록 지시합니다.                       |
| [`DeleteReminder`](#DeleteReminder)         | Directive | 클라이언트에게 리마인더를 삭제하도록 지시합니다.                    |
| [`DeleteSchedule`](#DeleteSchedule)         | Directive | 클라이언트에게 일정을 삭제하도록 지시합니다.                       |
| [`FinishExtension`](#FinishExtension)       | Directive | 클라이언트에게 특정 Extension을 종료하도록 지시합니다.             |
| [`GetMemo`](#GetMemo)                       | Directive | 클라이언트에게 메모를 조회하도록 지시합니다.                       |
| [`GetReminder`](#GetReminder)               | Directive | 클라이언트에게 리마인더를 조회하도록 지시합니다.                    |
| [`GetSchedule`](#GetSchedule)               | Directive | 클라이언트에게 일정을 조회하도록 지시합니다.                       |
| [`Hello`](#Hello)                           | Directive | 클라이언트에게 downchannel 연결 설정이 완료되었음을 알립니다.       |
| [`RenderMemoList`](#RenderMemoList)         | Directive | 클라이언트에게 메모 목록을 표시하도록 지시합니다.                   |
| [`RenderReminderList`](#RenderReminderList) | Directive | 클라이언트에게 리마인더 목록을 표시하도록 지시합니다.                |
| [`RenderTemplate`](#RenderTemplate)         | Directive | 클라이언트에게 템플릿을 표시하도록 지시합니다.                     |
| [`RenderText`](#RenderText)                 | Directive | 클라이언트에게 텍스트를 표시하도록 지시합니다.                     |
| [`StartExtension`](#StartExtension)         | Directive | 클라이언트에게 특정 Extension을 시작하도록 지시합니다.            |



## AddMemo directive {#AddMemo}

클라이언트에게 새로운 메모를 추가하도록 지시합니다. 사용자의 음성 인식으로 파악된 결과가 메모 내용으로 함께 전달됩니다.

### Payload field

| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|---------|
| `content`       | string  | 추가할 메모의 내용              | 필수     |
| `id`            | string  | 추가할 메모의 ID               | 필수     |

### Remarks

새로운 메모 생성이 완료되면 그 결과를 [`Memo.Created`](/CIC/References/APIs/Memo.md#Created) 이벤트 메시지를 통해 CIC로 전달해야 합니다.

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

클라이언트에게 새로운 리마인더를 추가하도록 지시합니다. 사용자의 음성 인식으로 파악된 결과가 리마인더 내용으로 함께 전달됩니다.

### Payload field

| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|---------|
| `content`       | string  | 추가할 리마인더의 내용           | 필수     |
| `id`            | string  | 추가할 리마인더의 ID            | 필수     |

### Remarks

새로운 리마인더 생성이 완료되면 그 결과를 [`Reminder.Created`](/CIC/References/APIs/Reminder.md#Created) 이벤트 메시지를 통해 CIC로 전달해야 합니다.

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

클라이언트에게 새로운 일정을 추가하도록 지시합니다. 사용자의 음성 인식으로 파악된 결과가 일정 내용으로 함께 전달됩니다. 클라이언트는 일정을 관리하는 로컬 앱을 호출하거나 별도의 인터페이스를 제공해야 합니다.

### Payload field

| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|---------|
| `content`       | string | 일정 내용                                                                    | 선택    |
| `id`            | string | 추가할 일정의 ID                                                              | 필수    |
| `period`        | string | 사용자의 음성 인식으로 파악된 가장 작은 단위의 기간입니다. 일정 종료 시간은 `scheduledTime`에 `period` 만큼 더한 값으로 설정합니다. <ul><li><code>"none"</code> : 기간 없음</li><li><code>"year"</code> : 1년</li><li><code>"month"</code> : 1개월</li><li><code>"week"</code> : 1주</li><li><code>"day"</code> : 1일</li><li><code>"hour"</code> : 1시간</li><li><code>"minute"</code> : 1분</li></ul>          | 필수    |
| `scheduledTime` | string | 추가할 일정의 시작 시간([ISO 8601](https://en.wikipedia.org/wiki/ISO_8601) 포맷) | 필수    |


### Remarks

클라이언트가 처리할 수 없는 기간 단위를 전달받으면, 적절한 예외 처리를 구현해야 합니다. 예를 들어, 클라이언트가 연간 일정 등록을 지원하지 않는데 `period` 값으로 `"year"`를 수신하면 예외 처리를 해야 합니다. "일정 추가해줘"처럼 기간을 알 수 없다면 `period`는 `"none"`, `scheduledTime`은 현재 시간이 전달됩니다.

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

클라이언트에게 조건에 일치하는 일정이 몇 개인지 표시하도록 지시합니다. 사용자의 음성 인식으로 파악된 조회 조건이 함께 전달됩니다. 클라이언트는 일정을 관리하는 로컬 앱 등에서 조건에 일치하는 일정이 몇 개인지 파악해야 합니다.

### Payload field

| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|---------|
| period        | string  | 사용자의 음성 인식으로 파악된 가장 작은 단위의 기간입니다. 조회할 범위의 종료 시간은 `scheduledTime`에 `period` 만큼 더한 값으로 설정합니다. <ul><li>"none": 기간 없음</li><li>"year": 1년</li><li>"month": 1개월</li><li>"week": 1주</li><li>"day": 1일</li><li>"hour": 1시간</li><li>"minute": 1분</li></ul>                | 필수    |
| scheduledTime | string  | 일정을 조회할 범위의 시작 시간([ISO 8601](https://en.wikipedia.org/wiki/ISO_8601) 포맷) | 필수    |

### Remarks

클라이언트가 처리할 수 없는 조회 기간 단위를 전달받으면, 적절한 예외 처리를 구현해야 합니다. 예를 들어, 클라이언트가 연간 일정 조회를 지원하지 않는데 `period` 값으로 "year"를 수신하면 예외 처리를 해야 합니다. "일정이 몇 개야"처럼 기간을 알 수 없다면 `period`는 "none", `scheduledTime`은 현재 시간이 전달됩니다.


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

클라이언트에게 메모 삭제를 진행하도록 지시합니다. 클라이언트는 `DeleteMemo` 지시 메시지를 전달받으면 사용자가 메모를 삭제할 수 있는 적절한 인터페이스를 제공해야 합니다.

### Payload field

없음

### Remarks

메모 삭제가 완료되면 그 결과를 [`Memo.Deleted`](/CIC/References/APIs/Memo.md#Deleted) 이벤트 메시지를 통해 CIC로 전달해야 합니다.

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

클라이언트에게 리마인더 삭제를 진행하도록 지시합니다. 클라이언트는 `DeleteReminder` 지시 메시지를 전달받으면 사용자가 리마인더를 삭제할 수 있는 적절한 인터페이스를 제공해야 합니다.

### Payload field

없음

### Remarks

리마인더 삭제가 완료되면 그 결과를 [`Reminder.Deleted`](/CIC/References/APIs/Reminder.md#Deleted) 이벤트 메시지를 통해 CIC로 전달해야 합니다.

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

클라이언트에게 일정을 삭제하도록 지시합니다. 사용자의 음성 인식으로 파악된 조건이 함께 전달됩니다. 클라이언트는 해당 조건에 일치하는 일정을 삭제하기 위해 일정을 관리하는 로컬 앱을 호출하거나 별도의 인터페이스를 제공해야 합니다.

### Payload field

| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|---------|
| `period`        | string  | 사용자의 음성 인식으로 파악된 가장 작은 단위의 기간입니다. 삭제할 범위의 종료 시간은 `scheduledTime`에 `period` 만큼 더한 값으로 설정합니다. <ul><li><code>"none"</code> : 기간 없음</li><li><code>"year"</code> : 1년</li><li><code>"month"</code> : 1개월</li><li><code>"week"</code> : 1주</li><li><code>"day"</code> : 1일</li><li><code>"hour"</code> : 1시간</li><li><code>"minute"</code> : 1분</li></ul>                | 필수    |
| `scheduledTime` | string  | 일정을 삭제할 범위의 시작 시간([ISO 8601](https://en.wikipedia.org/wiki/ISO_8601) 포맷) | 필수    |

### Remarks

클라이언트가 처리할 수 없는 기간 단위를 전달받으면, 적절한 예외 처리를 구현해야 합니다. 예를 들어, 클라이언트가 주간 일정 삭제를 지원하지 않는데 `period` 값으로 `"week"`를 수신하면 예외 처리를 해야 합니다. "일정 삭제해줘"처럼 기간을 알 수 없다면 `period`는 `"none"`, `scheduledTime`은 현재 시간이 전달됩니다.

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

클라이언트에게 특정 Extension을 종료하도록 지시합니다. 클라이언트는 FinishExtension 지시 메시지를 수신하면 해당 값에 대응하는 Extension을 종료해야 합니다.

### Payload field

| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|---------|
| `extension`     | string  | 종료할 Extension 이름          | 필수     |

### Remarks

현재 서버에서 기본적으로 제공하는 Extension으로는 대화 모드(Freetalk mode)가 있습니다. 대화 모드는 현재 영어 버전만 제공하고 있으며, "See you later" 발화로 모드 종료가 가능합니다. 이때, FinishExtension 지시 메시지의 `extension` 필드 값으로 "freetalking"이 전달됩니다.

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

클라이언트에게 메모 조회를 진행하도록 지시합니다. 클라이언트는 메모를 조회할 수 있는 로컬 앱을 호출하거나 별도의 인터페이스를 제공해야 합니다.

### Payload field

없음

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

클라이언트에게 리마인더 조회를 진행하도록 지시합니다. 클라이언트는 리마인더를 조회할 수 있는 로컬 앱을 호출하거나 별도의 인터페이스를 제공해야 합니다.

### Payload field

없음

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

클라이언트에게 일정 조회를 진행하도록 지시합니다. 사용자의 음성 인식으로 파악된 결과가 조회 조건으로 함께 전달됩니다. 클라이언트는 일정 조회할 수 있는 로컬 앱을 호출하거나 별도의 인터페이스를 제공해야 합니다.

### Payload field

| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|---------|
| `period`        | string  | 사용자의 음성 인식으로 파악된 가장 작은 단위의 기간입니다. 조회할 범위의 종료 시간은 `scheduledTime`에 `period` 만큼 더한 값으로 설정합니다. <ul><li><code>"none"</code> : 기간 없음</li><li><code>"year"</code> : 1년</li><li><code>"month"</code> : 1개월</li><li><code>"week"</code> : 1주</li><li><code>"day"</code> : 1일</li><li><code>"hour"</code> : 1시간</li><li><code>"minute"</code> : 1분</li></ul>                | 필수    |
| `scheduledTime` | string  | 일정을 조회할 범위의 시작 시간([ISO 8601](https://en.wikipedia.org/wiki/ISO_8601) 포맷) | 필수    |

### Remarks
클라이언트가 처리할 수 없는 기간 단위를 전달받으면, 적절한 예외 처리를 구현해야 합니다. 예를 들어, 클라이언트가 연간 일정 조회를 지원하지 않는데 `period` 값으로 `"year"`를 수신하면 예외 처리를 해야 합니다. "일정 조회해줘"처럼 기간을 알 수 없다면 `period`는 `"none"`, `scheduledTime`은 현재 시간이 전달됩니다.

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

클라이언트에게 downchannel 연결 설정이 완료되었음을 알립니다. 클라이언트는 이 지시 메시지를 통해 Clova 서비스에 대한 [접속 시도](/CIC/Guides/Interact_with_CIC.md#CreateConnection)가 제대로 수행되었는지 확인할 수 있습니다.

### Payload field

없음.

### Remarks
이 지시 메시지는 대화 ID(`dialogRequestId`)를 가지지 않습니다.

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
* [CIC 연결하기](/CIC/Guides/Interact_with_CIC.md#ConnectToCIC)

## RenderMemoList directive {#RenderMemoList}

클라이언트에게 메모 목록을 표시하도록 지시합니다. 사용자의 음성 인식으로 파악된 메모 목록이 함께 전달됩니다.

### Payload field

| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|---------|
| `memo[]`           | object array | 메모 목록을 포함하고 있는 객체 배열                                         | 필수    |
| `memo[].content`   | string       | 표시할 메모의 내용                                                      | 필수    |
| `memo[].id`        | string       | 표시할 메모의 ID                                                       | 필수    |
| `memo[].timestamp` | string       | 메모 생성 시간([ISO 8601](https://en.wikipedia.org/wiki/ISO_8601) 포맷) | 필수    |

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

클라이언트에게 리마인더 목록을 표시하도록 지시합니다. 사용자의 음성 인식으로 파악된 리마인더 목록이 함께 전달됩니다.

### Payload field

| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|---------|
| `reminder[]`         | object array | 리마인더 목록을 포함하고 있는 객체 배열 | 필수    |
| `reminder[].content` | string       | 표시할 리마인더의 내용              | 필수    |
| `reminder[].done`    | boolean      | 리마인더를 완료했는지 여부           | 필수    |
| `reminder[].id`      | string       | 표시할 리마인더의 ID               | 필수    |

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

클라이언트에게 데이터를 content template에 따라 표시하도록 지시합니다. 사용자 음성 인식으로 파악된 결과 콘텐츠가 함께 전달됩니다.

### Payload field
`payload` 필드는 [content template](/CIC/References/Content_Templates.md) 종류에 따라 포맷이 달라집니다. 현재 다음과 같은 content template을 제공하고 있습니다.

* 콘텐츠 UI 유형별 템플릿
  * [CardList](/CIC/References/ContentTemplates/CardList.md)
  * [ImageList](/CIC/References/ContentTemplates/ImageList.md)
  * [ImageText](/CIC/References/ContentTemplates/ImageText.md)
  * [Text](/CIC/References/ContentTemplates/Text.md)

* 길찾기 템플릿
  * [CarRoute](/CIC/References/ContentTemplates/CarRoute.md)
  * [TransportationRoute](/CIC/References/ContentTemplates/TransportationRoute.md)

* 날씨 템플릿
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

클라이언트에게 텍스트 메시지를 표시하도록 지시합니다. 사용자에게 보여줄 텍스트가 함께 전달됩니다.

### Payload field

| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|---------|
| `text`          | string  | 사용자에게 보여줄 텍스트          | 필수     |

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

클라이언트에게 특정 Extension을 시작하도록 지시합니다. 클라이언트는 StartExtension 지시 메시지를 수신하면 해당 값에 대응하는 Extension을 시작합니다.

### Payload field

| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|---------|
| `extension`     | string  | 시작할 Extension 이름          | 필수     |

### Remarks

현재 서버에서 기본적으로 제공하는 Extension으로는 대화 모드(Freetalk mode)가 있습니다. 대화 모드는 현재 영어 버전만 제공하고 있으며, "영어 대화 시작"과 같은 발화로 모드 시작이 가능합니다. 이때, `StartExtension` 지시 메시지의 `extension` 필드 값으로 `"freetalking"`이 전달됩니다.

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
