# Alerts

Alerts는 알람 또는 타이머를 생성/조회/삭제할 때 사용되는 네임스페이스입니다. 알람과 타이머를 위해 클라이언트는 타이머나 알람을 제어하는 로컬 앱을 호출하거나 별도의 인터페이스를 제공해야 합니다. Alerts가 제공하는 이벤트 메시지와 지시 메시지는 다음과 같습니다.

| 메시지 이름         | 메시지 타입  | 메시지 설명                                   |
|------------------|-----------|---------------------------------------------|
| [`DeleteAlert`](#DeleteAlert) | Directive | 클라이언트에게 알람 혹은 타이머를 삭제하도록 지시합니다. |
| [`GetAlert`](#GetAlert)       | Directive | 클라이언트에게 알람 혹은 타이머를 조회하도록 지시합니다. |
| [`SetAlert`](#SetAlert)       | Directive | 클라이언트에게 알람 혹은 타이머를 설정하도록 지시합니다. |

## DeleteAlert directive {#DeleteAlert}
클라이언트에게 알람 또는 타이머를 삭제하도록 지시합니다. 클라이언트는 사용자의 알람 또는 타이머를 삭제할 수 있도록 로컬 앱을 호출하거나 별도의 인터페이스를 제공해야 합니다.

### Payload field

| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|---------|
| `type`          | string  | 타입 구분자 <ul><li><code>"ALARM"</code> : 알람</li><li><code>"TIMER"</code> : 타이머</li></ul> | 필수    |

### Message example

{% raw %}

```json
{
  "directive": {
    "header": {
      "namespace": "Alerts",
      "name": "DeleteAlert",
      "messageId": "795251cd-de1b-43d9-9fcd-36d07f12d549",
      "dialogRequestId": "afc4c163-a14a-4f3e-93db-38ce36531785"
    },
    "payload": {
      "type": "ALARM"
    }
  }
}
```

{% endraw %}

### See also
* [`SpeechRecognizer.Recognize`](/CIC/References/APIs/SpeechRecognizer.md#Recognize)

## GetAlert directive {#GetAlert}

클라이언트에게 알람 또는 타이머를 조회하도록 지시합니다. 클라이언트는 사용자의 알람 혹은 타이머를 조회할 수 있도록 로컬 앱을 호출하거나 별도의 인터페이스를 제공해야 합니다.

### Payload field

| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|---------|
| `type`          | string  | 타입 구분자 <ul><li><code>"ALARM"</code> : 알람</li><li><code>"TIMER"</code> : 타이머</li></ul>  | 필수    |

### Message example

{% raw %}

```json
{
  "directive": {
    "header": {
      "namespace": "Alerts",
      "name": "GetAlert",
      "messageId": "fa87aa2e-0825-427d-ab11-c3684b662861",
      "dialogRequestId": "185424fd-ce63-4f08-9965-86f7baea856e"
    },
    "payload": {
      "type": "ALARM"
    }
  }
}
```

{% endraw %}

### See also
* [`SpeechRecognizer.Recognize`](/CIC/References/APIs/SpeechRecognizer.md#Recognize)

## SetAlert directive {#SetAlert}

클라이언트에게 알람 또는 타이머를 설정하도록 지시합니다. 클라이언트는 사용자의 알람 혹은 타이머를 설정할 수 있도록 로컬 앱을 호출하거나 별도의 인터페이스를 제공해야 합니다.

### Payload field

| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|---------|
| `currentTime`   | string       | 현재 시간 ([ISO 8601](https://en.wikipedia.org/wiki/ISO_8601) 포맷). 타이머의 경우 CIC로부터 현재 시간이 전달됩니다.                | 선택    |
| `daysOfWeek[]`  | string array | 반복 요일이 포함된 배열. "monday", "tuesday", "wednesday", "thursday", "friday", "saturday", "sunday"와 같은 값이 올 수 있습니다. | 선택    |
| `scheduledTime` | string       | 알람 또는 타이머의 설정 시간 ([ISO 8601](https://en.wikipedia.org/wiki/ISO_8601) 포맷)                                        | 필수    |
| `token`         | string       | 알람 또는 타이머의 ID                                                                                                      | 필수    |
| `type`          | string       | 타입 구분자 <ul><li><code>"ALARM"</code> : 알람</li><li><code>"TIMER"</code> : 타이머</li></ul>                     | 필수    |

### Message example

{% raw %}

```json
{
  "directive": {
    "header": {
      "namespace": "Alerts",
      "name": "SetAlert",
      "messageId": "9f73fad4-f33c-49e3-927f-9c98892936fb",
      "dialogRequestId": "f9210731-1657-48b5-bd74-eccbb46452fb"
    },
    "payload": {
      "token": "test:test_device:1495785482",
      "type": "ALARM",
      "scheduledTime": "2017-05-27T15:00:00+09:00",
      "daysOfWeek": ["saturday", "sunday"]
    }
  }
}
```

{% endraw %}

### See also
* [`SpeechRecognizer.Recognize`](/CIC/References/APIs/SpeechRecognizer.md#Recognize)
