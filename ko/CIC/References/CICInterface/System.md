# System

System은 Clova와 클라이언트 사이에 공유해야 할 정보를 동기화할 때 필요한 지시 메시지와 이벤트 메시지를 제공합니다. 클라이언트가 정보를 동기화하기 위해 ['System.RequestSynchronizeState'](RequestSynchronizeState) 이벤트 메시지를 CIC에게 보내며, CIC는 [`System.SynchronizeState`](#SynchronizeState) 지시 메시지를 이용하여 서버의 정보를 클라이언트에게 공유합니다.

| 메시지 이름         | 메시지 타입  | 메시지 설명                                 |
|------------------|-----------|-------------------------------------------|
| [`RequestSynchronizeState`](#RequestSynchronizeState)  | Event     | 클라이언트가 Clova의 클라우드 환경에 저장된 공유 정보를 동기화해야 할 때 이 이벤트 메시지를 CIC로 전송합니다. |
| [`SynchronizeState`](#SynchronizeState)                | Directive | 클라이언트에게 `payload` 필드에 있는 데이터를 동기화하도록 지시합니다. |


<div class="note">
  <p><strong>Note!</strong></p>
  <p>현재는 System 네임스페이스는 사용자가 등록한 알람 정보(Alerts)를 동기화하는데 사용되고 있습니다. 추후 동기화 대상이되는 정보가 더 많아질 수 있습니다.</p>
</div>

## RequestSynchronizeState event {#RequestSynchronizeState}
클라이언트가 Clova의 클라우드 환경에 저장된 공유 정보를 동기화해야 할 때 이 이벤트 메시지를 CIC로 전송합니다. CIC는 이 이벤트 메시지를 받으면, 클라이언트에게 [`System.SynchronizeState`](#SynchronizeState) 지시 메시지를 전송합니다.

### Context field

필수 상태 정보 없음

### Payload field

없음

### Message example
{% raw %}
```json
{
  "context":[],
  "event": {
    "header": {
      "namespace": "System",
      "name": "RequestSynchronizeState",
      "messageId": "b120c3e0-e6b9-4a3d-96de-71539e5f6214"
    },
    "payload": {}
  }
}
```
{% endraw %}

### See also
* [`System.SynchronizeState`](/CIC/References/CICInterface/System.md#SynchronizeState)

## SynchronizeState directive {#SynchronizeState}
클라이언트에게 `payload` 필드에 있는 데이터를 동기화하도록 지시합니다. 클라이언트는 Clova로부터 전달된 데이터에 맞게 클라이언트에 설정된 값을 변경해야 합니다.

### Payload field

| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|---------|
| `allAlerts`   | [AlertObject] array | 클라이언트가 동기화해야 할 알람 목록을 가지는 객체 배열. [`Alerts.SetAlert`](/CIC/References/CICInterface/Alerts.md#SetAlert) 지시 메시지에 사용되는 `payload` 객체와 같은 포맷을 가지는 객체 배열입니다. | 필수    |

### Remarks
현재는 System 네임스페이스는 사용자가 등록한 말람 정보(Alerts)를 동기화하는데 사용되고 있습니다. 추후 동기화 대상이되는 정보가 더 많아질 수 있습니다.

### Message example

{% raw %}

```json
{
  "directive": {
    "header": {
      "namespace": "System",
      "name": "SynchronizeState",
      "messageId": "29745c13-0d70-408e-a4cc-946afba67524"
    },
    "payload": {
      "allAlerts": [
        {
          "type": "REMINDER",
          "token": "77179dbd-b65f-4341-a579-c1b2b97fc5b7",
          "scheduledTime": "2017-09-25T09:00:50+09:00",
          "assets": [
            {
              "assetId": "5141f693-5b39-46b7-80e4-3d71ed5508da",
              "url": "http://abc.de.fe/tts1"
            },
            {
              "assetId": "b403ebe5-f911-4c5c-98b3-9f5320510235",
              "url": "http://abc.de.fe/tts2"
            }
          ],
          "assetPlayOrder": ["5141f693-5b39-46b7-80e4-3d71ed5508da", "b403ebe5-f911-4c5c-98b3-9f5320510235"]
        },
        {
          "type": "ALARM",
          "token": "ee4da70c-8328-4456-ab6f-c28cec626ae6",
          "scheduledTime": "2017-09-26T11:00:50+09:00"
        },
        ...
      ]
    }
  }
}
```

{% endraw %}

### See also
* [`System.RequestSynchronizeState`](#RequestSynchronizeState)
