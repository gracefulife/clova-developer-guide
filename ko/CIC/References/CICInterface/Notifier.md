# Notifier

Notifier 인터페이스는 CIC가 클라이언트기기에 알림이 있음을 표시하도록 지시하거나 사용자 계정에 등록된 모든 클라이언트에게 알림 표시를 없애도록 지시합니다. CIC는 클라이언트가 사용자 알림 확인 상태를 최신으로 유지하게 만들기 위해 클라이언트 요청이 없어도 다음과 같은 지시 메시지를 전달합니다.

| 메시지 이름         | 메시지 타입  | 메시지 설명                                   |
|------------------|-----------|---------------------------------------------|
| [`ClearIndicator`](#ClearIndicator)         | Directive | 클라이언트에게 알림을 나타내는 표시를 모두 끄도록 지시합니다. |
| [`SetIndicator`](#SetIndicator)             | Directive | 클라이언트에게 확인하지 않은 알림이 있음을 나타내는 표시를 켜도록 지시합니다. |

## ClearIndicator directive {#ClearIndicator}
클라이언트에게 알림을 나타내는 표시를 모두 끄도록 지시합니다. 알림을 표시하는 조명이나 소리 효과를 모두 꺼야 합니다.

### Payload field
없음

### Remarks
해당 지시 메시지는 이벤트 메시지에 대한 응답이 아닌 [downchannel](/CIC/Guides/Interact_with_CIC.md#CreateConnection)을 통해 전달됩니다.

### Message example

{% raw %}

```json
{
  "directive": {
    "header": {
      "namespace": "Notifier",
      "name": "ClearIndicator",
      "messageId": "29745c13-0d70-408e-a4cc-946afba67524"
    },
    "payload": {}
  }
}
```

{% endraw %}

### See also
* [`Notifier.SetIndicator`](#SetIndicator)

## SetIndicator directive {#SetIndicator}
클라이언트에게 알림 표시를 켜도록 지시합니다.

### Payload field
| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|---------|
| `new`         | boolean | 새로운 알림에 대한 지시 메시지인지 알려주는 필드입니다. <ul><li><code>true</code>: 새로운 알림인 경우</li><li><code>false</code>: 새로운 알림이 아닌 경우</li></ul> | 필수    |
| `light`       | string  | 조명 설정 정보<ul><li><code>"on"</code>: 사용자가 확인하지 않은 알림이 있는 경우입니다. 주로 알림 표시용 조명을 점등하게 됩니다.</li><li><code>"off"</code>: 사용자가 확인하지 않은 알림이 없는 경우입니다.</li></ul> | 필수    |

### Remarks
해당 지시 메시지는 이벤트 메시지에 대한 응답이 아닌 [downchannel](/CIC/Guides/Interact_with_CIC.md#CreateConnection)을 통해 전달됩니다.

### Message example

{% raw %}

```json
{
  "directive": {
    "header": {
      "namespace": "Notifier",
      "name": "SetIndicator",
      "messageId": "29745c13-0d70-408e-a4cc-946afba67524"
    },
    "payload": {
      "new": true,
      "light": "on"
    }
  }
}
```

{% endraw %}

### See also
* [`Notifier.ClearIndicator`](#ClearIndicator)
