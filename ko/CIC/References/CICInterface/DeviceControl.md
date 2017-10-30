# DeviceControl

DeviceControl은 클라이언트 기기를 제어하거나 클라이언트 기기 제어 수행 결과를 CIC로 보고할 때 사용되는 네임스페이스입니다.

일부 사용자의 요청은 클라이언트 기기를 제어하는 요청일 수 있습니다. 분석된 사용자의 요청이 클라이언트 기기를 제어하는 요청이면 네임스페이스 `DeviceControl`인 지시 메시지를 받게 되며 클라이언트는 수신한 지시 메시지에 맞게 클라이언트 기기를 제어해야 합니다. 클라이언트 기기 제어를 수행한 후 그 결과를 이벤트 메시지를 사용하여 CIC에 전송해야 합니다.

DeviceControl이 제공하는 이벤트 메시지와 지시 메시지는 다음과 같습니다.

| 메시지 이름         | 메시지 타입  | 메시지 설명                                   |
|------------------|-----------|---------------------------------------------|
| [`ActionExecuted`](#ActionExecuted)       | Event     | 클라이언트는 기기 제어를 정상적으로 수행한 경우 이 이벤트 메시지를 CIC로 전송해야 합니다.           |
| [`ActionFailed`](#ActionFailed)           | Event     | 클라이언트는 기기 제어를 수행할 수 없거나 수행에 실패한 경우 이 이벤트 메시지를 CIC로 전송해야 합니다. |
| [`BtConnect`](#BtConnect)                 | Directive | 클라이언트에게 특정 블루투스 기기와 연결을 설정하도록 지시합니다.                               |
| [`BtDisconnect`](#BtDisconnect)           | Directive | 클라이언트에게 특정 블루투스 기기와 연결을 해제하도록 지시합니다.                               |
| [`BtStartPairing`](#BtStartPairing)       | Directive | 클라이언트에게 블루투스 페어링 모드를 시작하도록 지시합니다.                                   |
| [`BtStopPairing`](#BtStopPairing)         | Directive | 클라이언트에게 블루투스 페어링 모드로 중지하도록 지시합니다.                                   |
| [`Decrease`](#Decrease)                   | Directive | 클라이언트에게 스피커 볼륨 또는 화면 밝기를 기본 단위만큼 줄이도록 지시합니다.                     |
| [`ExpectReportState`](#ExpectReportState)  | Directive | 클라이언트에게 기기의 현재 상태를 CIC로 보고하도록 지시합니다.                             |
| [`Increase`](#Increase)                   | Directive | 클라이언트에게 스피커 볼륨 또는 화면 밝기를 기본 단위만큼 높이도록 지시합니다.                     |
| [`LaunchApp`](#LaunchApp)                 | Directive | 클라이언트에게 특정 앱을 실행하도록 지시합니다.                                             |
| [`OpenScreen`](#OpenScreen)               | Directive | 클라이언트에게 설정 화면을 열도록 지시합니다.                                              |
| [`ReportState`](#ReportState)             | Event     | 클라이언트는 기기의 현재 상태를 CIC로 보고할 때 이 메시지를 사용해야 합니다.                 |
| [`RequestStateSynchronization`](#RequestStateSynchronization) | Event   | 사용자의 계정에 등록된 다른 클라이언트 기기의 현재 상태를 파악하고자 할 때 이 이벤트 메시지를 CIC로 전송합니다.  |
| [`SetValue`](#SetValue)                   | Directive | 클라이언트에게 스피커 볼륨 또는 화면 밝기를 지정한 값으로 설정하도록 지시합니다.                    |
| [`SynchronizeState`](#SynchronizeState)     | Directive | 클라이언트에게 사용자 계정에 등록된 또 다른 클라이언트 기기의 상태를 업데이트하도록 지시합니다.         |
| [`TurnOff`](#TurnOff)                     | Directive | 클라이언트에게 지정한 기능이나 모드를 끄거나 비활성화하도록 지시합니다.                           |
| [`TurnOn`](#TurnOn)                       | Directive | 클라이언트에게 지정한 기능을 켜거나 활성화하도록 지시합니다.                                   |

<div class="note">
  <p><strong>Note!</strong></p>
  <p>DeviceControl API는 현재 구현 예정인 명세입니다. 사전 인터페이스 협의를 위해 미리 기술되었으며, 추후 내용이 변경될 수도 있습니다.</p>
</div>

## ActionExecuted event {#ActionExecuted}

클라이언트는 기기 제어를 정상적으로 수행한 경우 이 이벤트 메시지를 CIC로 전송해야 합니다.

### Payload field

| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|---------|
| `target`      | string  | 제어 대상.<ul><li><code>"airplane"</code>: 비행기 모드</li><li><code>"app"</code>: 앱</li><li><code>"bluetooth"</code>: 블루투스</li><li><code>"cellular"</code>: 모바일 통신</li><li><code>"channel"</code>: TV 채널</li><li><code>"flashlight"</code>: 플래시 조명</li><li><code>"gps"</code>: GPS</li><li><code>"powersave"</code>: 절전 모드</li><li><code>"screenbrightness"</code>: 화면 밝기</li><li><code>"soundmode"</code>: 사운드 모드</li><li><code>"volume"</code>: 스피커 볼륨</li><li><code>"wifi"</code>: 무선랜</li></ul> | 필수     |
| `command`     | string  | 정상 수행한 동작.  <ul><li>BtConnect</li><li>BtDisconnect</li><li>BtStartPairing</li><li>BtStopPairing</li><li>Decrease</li><li>Increase</li><li>OpenScreen</li><li>SetValue</li><li>TurnOn</li><li>TurnOff</li></ul> | 필수   |

### Remarks

CIC는 이 이벤트 메시지를 수신하면 사용자 계정에 등록된 모든 클라이언트에게 [`SynchronizeState`](#SynchronizeState) 지시 메시지를 전송하여 특정 클라이언트 기기의 변경된 상태 정보를 알립니다.

### Message example

{% raw %}

```json
{
  "event": {
    "header": {
      "namespace": "DeviceControl",
      "name": "ActionExecuted",
      "messageId": "23bdfff7-b655-46d4-8655-8bb473bf2bf5"
    },
    "payload": {
      "target": "gps",
      "command": "TurnOn"
    }
  }
}
```

{% endraw %}

### See also
* [`DeviceControl.ActionFailed`](#ActionFailed)
* [`DeviceControl.BtConnect`](#BtConnect)
* [`DeviceControl.BtDisconnect`](#BtDisconnect)
* [`DeviceControl.BtStartPairing`](#BtStartPairing)
* [`DeviceControl.BtStopPairing`](#BtStopPairing)
* [`DeviceControl.Decrease`](#Decrease)
* [`DeviceControl.Increase`](#Increase)
* [`DeviceControl.OpenScreen`](#OpenScreen)
* [`DeviceControl.SetValue`](#SetValue)
* [`DeviceControl.TurnOff`](#TurnOff)
* [`DeviceControl.TurnOn`](#TurnOn)

## ActionFailed event {#ActionFailed}

클라이언트는 기기 제어를 수행할 수 없거나 수행에 실패한 경우 이 이벤트 메시지를 CIC로 전송해야 합니다.

### Payload field

| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|---------|
| `target`      | string  | 제어 대상.<ul><li><code>"airplane"</code>: 비행기 모드</li><li><code>"app"</code>: 앱</li><li><code>"bluetooth"</code>: 블루투스</li><li><code>"cellular"</code>: 모바일 통신</li><li><code>"channel"</code>: TV 채널</li><li><code>"flashlight"</code>: 플래시 조명</li><li><code>"gps"</code>: GPS</li><li><code>"powersave"</code>: 절전 모드</li><li><code>"screenbrightness"</code>: 화면 밝기</li><li><code>"soundmode"</code>: 사운드 모드</li><li><code>"volume"</code>: 스피커 볼륨</li><li><code>"wifi"</code>: 무선랜</li></ul> | 필수     |
| `command`     | string  | 실패한 동작. <ul><li>BtConnect</li><li>BtDisconnect</li><li>BtStartPairing</li><li>BtStopPairing</li><li>Decrease</li><li>Increase</li><li>LaunchApp</li><li>OpenScreen</li><li>SetValue</li><li>TurnOn</li><li>TurnOff</li></ul> | 필수   |

### Remarks

* CIC는 이 이벤트 메시지를 수신하면 사용자 계정에 등록된 모든 클라이언트에게 [`SynchronizeState`](#SynchronizeState) 지시 메시지를 전송하여 특정 클라이언트 기기의 변경된 상태 정보를 알립니다.
* [`LaunchApp`](#LaunchApp) 지시 메시지를 수신한 후 앱 실행에 실패하면 `target` 필드는 `"app"`으로 설정합니다.

### Message example

{% raw %}

```json
{
  "event": {
    "header": {
      "namespace": "DeviceControl",
      "name": "ActionFailed",
      "messageId": "23bdfff7-b655-46d4-8655-8bb473bf2bf5"
    },
    "payload": {
      "target": "gps",
      "command": "TurnOn"
    }
  }
}
```

{% endraw %}

### See also
* [`DeviceControl.ActionExecuted`](#ActionExecuted)
* [`DeviceControl.BtConnect`](#BtConnect)
* [`DeviceControl.BtDisconnect`](#BtDisconnect)
* [`DeviceControl.BtStartPairing`](#BtStartPairing)
* [`DeviceControl.BtStopPairing`](#BtStopPairing)
* [`DeviceControl.Decrease`](#Decrease)
* [`DeviceControl.Increase`](#Increase)
* [`DeviceControl.LaunchApp`](#LaunchApp)
* [`DeviceControl.OpenScreen`](#OpenScreen)
* [`DeviceControl.SetValue`](#SetValue)
* [`DeviceControl.TurnOff`](#TurnOff)
* [`DeviceControl.TurnOn`](#TurnOn)

## BtConnect directive {#BtConnect}

클라이언트에게 페어링된 블루투스 기기 중 하나와 연결을 설정하도록 지시합니다. 한 대 이상의 기기와 페어링되어 있는 경우 각각의 클라이언트는 기준에 따라 어떤 기기와 연결을 설정할지 결정해야 합니다. 예를 들면, 가장 최근에 연결했던 순서대로 기기 연결을 시도할 수 있습니다.

### Payload field

없음

### Remarks

* 스피커 형태의 블루투스 기기만 지원합니다.
* 클라이언트는 맥락 정보인 [`Device.DeviceState`](/CIC/References/Context_Objects.md#DeviceState) 객체를 이용해 수시로 블루투스 기기 정보를 CIC에 전달해야 합니다.
* 클라이언트는 이 지시 메시지에 해당하는 내용을 처리한 후 [`DeviceControl.ActionExecuted`](#ActionExecuted) 또는 [`DeviceControl.ActionFailed`](#ActionFailed) 이벤트 메시지를 이용하여 결과를 CIC에 전달해야 합니다.

### Message example

{% raw %}

```json
{
    "directive": {
        "header": {
            "namespace": "DeviceControl",
            "name": "BtConnect",
            "messageId": "0f9950d1-c908-4e02-8c38-8e64e840634c",
            "dialogRequestId": "de0a1fd7-2ef1-4040-9469-3a5dd03ef46b"
        },
        "payload": {}
    }
}
```

{% endraw %}

### See also
* [`DeviceControl.ActionExecuted`](#ActionExecuted)
* [`DeviceControl.ActionFailed`](#ActionFailed)
* [`DeviceControl.BtDisconnect`](#BtDisconnect)
* [`DeviceControl.BtStartPairing`](#BtStartPairing)
* [`DeviceControl.BtStopPairing`](#BtStopPairing)
* [`DeviceControl.TurnOff`](#TurnOff)
* [`DeviceControl.TurnOn`](#TurnOn)

## BtDisconnect directive {#BtDisconnect}

클라이언트에게 연결된 블루투스 기기와 연결을 끊도록 지시합니다.

### Payload field

없음

### Remarks

* 스피커 형태의 블루투스 기기만 지원합니다.
* 클라이언트는 맥락 정보인 [`Device.DeviceState`](/CIC/References/Context_Objects.md#DeviceState) 객체를 이용해 수시로 블루투스 기기 정보를 CIC에 전달해야 합니다.
* 클라이언트는 이 지시 메시지에 해당하는 내용을 처리한 후 [`DeviceControl.ActionExecuted`](#ActionExecuted) 또는 [`DeviceControl.ActionFailed`](#ActionFailed) 이벤트 메시지를 이용하여 결과를 CIC에 전달해야 합니다.

### Message example

{% raw %}

```json
{
    "directive": {
        "header": {
            "namespace": "DeviceControl",
            "name": "BtDisconnect",
            "messageId": "0f9950d1-c908-4e02-8c38-8e64e840634c",
            "dialogRequestId": "de0a1fd7-2ef1-4040-9469-3a5dd03ef46b"
        },
        "payload": {}
    }
}
```

{% endraw %}

### See also
* [`DeviceControl.ActionExecuted`](#ActionExecuted)
* [`DeviceControl.ActionFailed`](#ActionFailed)
* [`DeviceControl.BtConnect`](#BtConnect)
* [`DeviceControl.BtStartPairing`](#BtStartPairing)
* [`DeviceControl.BtStopPairing`](#BtStopPairing)
* [`DeviceControl.TurnOff`](#TurnOff)
* [`DeviceControl.TurnOn`](#TurnOn)

## BtStartPairing directive {#BtStartPairing}

클라이언트에게 블루투스 페어링 모드를 시작하도록 지시합니다.

### Payload field

없음

### Remarks

* 스피커 형태의 블루투스 기기만 지원합니다.
* 클라이언트는 맥락 정보인 [`Device.DeviceState`](/CIC/References/Context_Objects.md#DeviceState) 객체를 이용해 수시로 블루투스 기기 정보를 CIC에 전달해야 합니다.
* 클라이언트는 이 지시 메시지에 해당하는 내용을 처리한 후 [`DeviceControl.ActionExecuted`](#ActionExecuted) 또는 [`DeviceControl.ActionFailed`](#ActionFailed) 이벤트 메시지를 이용하여 결과를 CIC에 전달해야 합니다.

### Message example

{% raw %}

```json
{
    "directive": {
        "header": {
            "namespace": "DeviceControl",
            "name": "BtStartPairing",
            "messageId": "0f9950d1-c908-4e02-8c38-8e64e840634c",
            "dialogRequestId": "de0a1fd7-2ef1-4040-9469-3a5dd03ef46b"
        },
        "payload": {}
    }
}
```

{% endraw %}

### See also
* [`DeviceControl.ActionExecuted`](#ActionExecuted)
* [`DeviceControl.ActionFailed`](#ActionFailed)
* [`DeviceControl.BtConnect`](#BtConnect)
* [`DeviceControl.BtDisconnect`](#BtDisconnect)
* [`DeviceControl.BtStopPairing`](#BtStopPairing)
* [`DeviceControl.TurnOff`](#TurnOff)
* [`DeviceControl.TurnOn`](#TurnOn)

## BtStopPairing directive {#BtStopPairing}

클라이언트에게 블루투스 페어링 모드를 중지하도록 지시합니다.

### Payload field

없음

### Remarks

* 스피커 형태의 블루투스 기기만 지원합니다.
* 클라이언트는 맥락 정보인 [`Device.DeviceState`](/CIC/References/Context_Objects.md#DeviceState) 객체를 이용해 수시로 블루투스 기기 정보를 CIC에 전달해야 합니다.
* 클라이언트는 이 지시 메시지에 해당하는 내용을 처리한 후 [`DeviceControl.ActionExecuted`](#ActionExecuted) 또는 [`DeviceControl.ActionFailed`](#ActionFailed) 이벤트 메시지를 이용하여 결과를 CIC에 전달해야 합니다.

### Message example

{% raw %}

```json
{
    "directive": {
        "header": {
            "namespace": "DeviceControl",
            "name": "BtStopPairing",
            "messageId": "0f9950d1-c908-4e02-8c38-8e64e840634c",
            "dialogRequestId": "de0a1fd7-2ef1-4040-9469-3a5dd03ef46b"
        },
        "payload": {}
    }
}
```

{% endraw %}

### See also
* [`DeviceControl.ActionExecuted`](#ActionExecuted)
* [`DeviceControl.ActionFailed`](#ActionFailed)
* [`DeviceControl.BtConnect`](#BtConnect)
* [`DeviceControl.BtDisconnect`](#BtDisconnect)
* [`DeviceControl.BtStartPairing`](#BtStopPairing)
* [`DeviceControl.TurnOff`](#TurnOff)
* [`DeviceControl.TurnOn`](#TurnOn)

## Decrease directive {#Decrease}

클라이언트에게 스피커 볼륨 또는 화면 밝기를 기본 단위만큼 줄이도록 지시하거나, TV 채널을 이전 채널로 변경하도록 지시합니다.

### Payload field

| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|---------|
| `target`      | string  | 제어 대상.<ul><li><code>"channel"</code>: TV 채널</li><li><code>"screenbrightness"</code>: 화면 밝기</li><li><code>"volume"</code>: 스피커 볼륨</li></ul> | 필수     |

### Remarks

* 기본 단위는 클라이언트측에서 직접 결정하면 됩니다.
* 클라이언트는 맥락 정보인 [`Device.DeviceState`](/CIC/References/Context_Objects.md#DeviceState) 객체를 이용해 수시로 스피커 볼륨 정보와 화면 밝기 정보를 CIC에 전달해야 합니다.
* 클라이언트는 이 지시 메시지에 해당하는 내용을 처리한 후 [`DeviceControl.ActionExecuted`](#ActionExecuted) 또는 [`DeviceControl.ActionFailed`](#ActionFailed) 이벤트 메시지를 이용하여 결과를 CIC에 전달해야 합니다.

### Message example

{% raw %}

```json
{
  "directive": {
    "header": {
      "namespace": "DeviceControl",
      "name": "Decrease",
      "messageId": "23bdfff7-b655-46d4-8655-8bb473bf2bf5",
      "dialogRequestId": "3c6eef8b-8427-4b46-a367-0a7a46432519"
    },
    "payload": {
      "target": "screenbrightness"
    }
  }
}
```

{% endraw %}

### See also
* [`DeviceControl.ActionExecuted`](#ActionExecuted)
* [`DeviceControl.ActionFailed`](#ActionFailed)
* [`DeviceControl.Increase`](#Increase)
* [`DeviceControl.SetValue`](#SetValue)

## ExpectReportState directive {#ExpectReportState}

클라이언트에게 기기의 현재 상태를 CIC로 보고하도록 지시합니다. 이 메시지를 받은 클라이언트는 즉시 [`DeviceControl.ReportState`](#ReportState) 이벤트 메시지를 사용하여 기기의 현재 상태를 보고해야 하며, 이후에는 `durationInSeconds` 필드에 지정된 시간 동안 `intervalInSeconds` 필드에 지정된 주기로 기기의 현재 상태를 보고해야 합니다.

### Payload field

| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|---------|
| `durationInSeconds` | number  | 보고 기간. 지정된 시간동안 기기의 현재 상태를 보고합니다. 단위는 초단위 입니다. 이 필드가 없는 경우 최초 1회만 보고를 수행합니다. | 선택     |
| `intervalInSeconds` | number  | 보고 주기. 지정된 주기로 기기의 형태 상태를 보고합니다. 단위는 초단위 입니다. 이 필드는 `durationInSeconds` 필드가 있을 경우에만 유효하며 없을 경우 함께 생략됩니다. | 선택     |

### Remarks

* `DeviceControl.ExpectReportState` 지시 메시지는 다른 클라이언트에서 동기화를 위해 [`DeviceControl.RequestStateSynchronization`](#RequestStateSynchronization) 이벤트 메시지를 CIC로 전송한 경우 수신됩니다.
* 이 지시 메시지는 이벤트 메시지에 대한 응답이 아닌 [downchannel](/CIC/Guides/Interact_with_CIC.md#CreateConnection)을 통해 전달됩니다.

### Message example

{% raw %}

```json
{
  "directive": {
    "header": {
      "namespace": "DeviceControl",
      "name": "ExpectReportState",
      "messageId": "23bdfff7-b655-46d4-8655-8bb473bf2bf5",
      "dialogRequestId": "3c6eef8b-8427-4b46-a367-0a7a46432519"
    },
    "payload": {
      "durationInSeconds": 600,
      "intervalInSeconds": 60
    }
  }
}
```

{% endraw %}

### See also
* [`DeviceControl.ReportState`](#ReportState)
* [`DeviceControl.RequestStateSynchronization`](#RequestStateSynchronization)

## Increase directive {#Increase}

클라이언트에게 스피커 볼륨 또는 화면 밝기를 기본 단위만큼 높이도록 지시하거나, TV 채널을 다음 채널로 변경하도록 지시합니다.

### Payload field

| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|---------|
| `target`      | string  | 제어 대상.<ul><li><code>"channel"</code>: TV 채널</li><li><code>"screenbrightness"</code>: 화면 밝기</li><li><code>"volume"</code>: 스피커 볼륨</li></ul> | 필수     |

### Remarks

* 기본 단위는 클라이언트측에서 직접 결정하면 됩니다.
* 클라이언트는 맥락 정보인 [`Device.DeviceState`](/CIC/References/Context_Objects.md#DeviceState) 객체를 이용해 수시로 스피커 볼륨 정보와 화면 밝기 정보를 CIC에 전달해야 합니다.
* 클라이언트는 이 지시 메시지에 해당하는 내용을 처리한 후 [`DeviceControl.ActionExecuted`](#ActionExecuted) 또는 [`DeviceControl.ActionFailed`](#ActionFailed) 이벤트 메시지를 이용하여 결과를 CIC에 전달해야 합니다.

### Message example

{% raw %}

```json
{
  "directive": {
    "header": {
      "namespace": "DeviceControl",
      "name": "Increase",
      "messageId": "23bdfff7-b655-46d4-8655-8bb473bf2bf5",
      "dialogRequestId": "3c6eef8b-8427-4b46-a367-0a7a46432519"
    },
    "payload": {
      "target": "screenbrightness"
    }
  }
}
```

{% endraw %}

### See also
* [`DeviceControl.ActionExecuted`](#ActionExecuted)
* [`DeviceControl.ActionFailed`](#ActionFailed)
* [`DeviceControl.Decrease`](#Decrease)
* [`DeviceControl.SetValue`](#SetValue)

## LaunchApp directive {#LaunchApp}

클라이언트에게 특정 앱을 실행하도록 지시합니다. 앱을 지정하는 값으로 앱의 custom URL scheme나 중계 페이지 URL 또는 앱 이름이 전달됩니다.

### Payload field

| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|---------|
| `target`      | string  | 대상 앱에 대한 정보. 다음과 같은 타입의 앱 정보를 가질 수 있습니다.<ul><li>custom URL scheme: 대상 앱의 custom URL scheme (예, <code>"naversearchapp://..."</code>)</li><li>중계 페이지 URL: 설치된 대상 앱이 있을 경우 해당 앱을 실행하는 중계 페이지 URL(예, <code>"http://naverapp.naver.com/..."</code>)</li><li>앱 이름: 사용자의 발화를 인식한 앱의 이름 (예, <code>"네이버앱"</code>)</li></ul> | 필수     |

### Remarks

* 앱을 실행할 수 없거나 앱 실행에 실패한 경우 [`DeviceControl.ActionFailed`](#ActionFailed) 이벤트 메시지를 이용하여 결과를 CIC에 전달해야 합니다.

### Message example

{% raw %}

```json
{
  "directive": {
    "header": {
      "namespace": "DeviceControl",
      "name": "LaunchApp",
      "messageId": "23bdfff7-b655-46d4-8655-8bb473bf2bf5",
      "dialogRequestId": "3c6eef8b-8427-4b46-a367-0a7a46432519"
    },
    "payload": {
      "target": "naversearchapp://..."
    }
  }
}
```

{% endraw %}

### See also
* [`DeviceControl.ActionFailed`](#ActionFailed)

## OpenScreen directive {#OpenScreen}

클라이언트에게 설정 화면을 열도록 지시합니다.

### Payload field

| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|---------|
| `target`      | string  | 표시할 화면. 현재는 설정 화면을 여는 값인 `"settings"`만 입력됩니다. | 필수     |

### Remarks

클라이언트는 이 지시 메시지에 해당하는 내용을 처리한 후 [`DeviceControl.ActionExecuted`](#ActionExecuted) 또는 [`DeviceControl.ActionFailed`](#ActionFailed) 이벤트 메시지를 이용하여 결과를 CIC에 전달해야 합니다.

### Message example

{% raw %}

```json
{
  "directive": {
    "header": {
      "namespace": "DeviceControl",
      "name": "OpenScreen",
      "messageId": "23bdfff7-b655-46d4-8655-8bb473bf2bf5",
      "dialogRequestId": "3c6eef8b-8427-4b46-a367-0a7a46432519"
    },
    "payload": {
      "target": "settings"
    }
  }
}
```

{% endraw %}

### See also
* [`DeviceControl.ActionExecuted`](#ActionExecuted)
* [`DeviceControl.ActionFailed`](#ActionFailed)

## ReportState event {#ReportState}

클라이언트는 기기의 현재 상태를 CIC로 보고할 때 이 메시지를 사용해야 합니다.

### Context field

클라이언트 기기의 현재 상태를 전달하기 위해 이벤트 메시지에 다음 [맥락 정보(Context)](/CIC/References/Context_Objects.md)를 포함하여 전송합니다.

* [`Device.DeviceState`](/CIC/References/Context_Objects.md#DeivceState)

### Payload field

없음

### Remarks

* CIC로부터 [`DeviceControl.ExpectReportState`](#ExpectReportState) 지시 메시지를 받은 경우 `DeviceControl.ReportState` 이벤트 메시지를 사용하여 현재 상태를 보고해야 합니다.
* 이 이벤트 메시지를 통해 보고된 상태 정보는 [`DeviceControl.SynchronizeState`](#SynchronizeState) 지시 메시지 통해 사용자 계정에 등록된 모든 클라이언트에게 보내집니다.

### Message example

{% raw %}

```json
{
  "context": {
    "header": {
      "namespace": "Device",
      "name": "DeviceState"
    },
    "payload": {
      "localTime": "2017-04-06T13:34:15.074361+08:28",
      "bluetooth": {
          "actions": [
              "BtConnect",
              "BtDisconnect",
              "BtStartPairing",
              "BtStopPairing",
              "TurnOff",
              "TurnOn"
          ],
          "btlist": [
              {
                  "name": "My Phone",
                  "address": "44:00:10:f1:1f:f5",
                  "connected": false
              },
              {
                  "name": "My Speaker",
                  "address": "29:01:11:1f:12:89",
                  "connected": true
              }
          ],
          "state": "on"
      },
      "wifi": {
          "actions": [
              "TurnOff",
              "TurnOn"
          ],
          "networks": [
            {
              "name": "home_wlan",
              "connected": true
            },
            {
              "name": "guest_wlan",
              "connected": false
            }
          ],
          "state": "on"
      },
      "battery": {
          "actions": [],
          "value": 99,
          "charging": true
      },
      "flashLight": {
          "actions": [
              "TurnOff",
              "TurnOn"
          ],
          "state": "off"
      }
    }
  },
  "event": {
    "header": {
      "namespace": "DeviceControl",
      "name": "ReportState",
      "messageId": "23bdfff7-b655-46d4-8655-8bb473bf2bf5"
    },
    "payload": {}
  }
}
```

{% endraw %}

### See also
* [`Device.DeviceState`](/CIC/References/Context_Objects.md#DeivceState)
* [`DeviceControl.ExpectReportState`](#ExpectReportState)
* [`DeviceControl.SynchronizeState`](#SynchronizeState)

## RequestStateSynchronization event {#RequestStateSynchronization}

사용자의 계정에 등록된 다른 클라이언트 기기의 현재 상태를 파악하고자 할 때 이 이벤트 메시지를 CIC로 전송합니다. CIC는 이 이벤트 메시지를 받으면, 사용자의 계정에 등록된 모든 클라이언트에게 [`DeviceControl.ExpectReportState`](#ExpectReportState) 지시 메시지를 전송합니다.

### Payload field

없음

### Remarks

이 이벤트 메시지에 대한 결과로 추후 [downchannel](/CIC/Guides/Interact_with_CIC.md#CreateConnection)을 통해 [`DeviceControl.SynchronizeState`](#SynchronizeState) 지시 메시지를 받게 됩니다.

### Message example

{% raw %}

```json
{
  "event": {
    "header": {
      "namespace": "DeviceControl",
      "name": "RequestStateSynchronization",
      "messageId": "23bdfff7-b655-46d4-8655-8bb473bf2bf5"
    },
    "payload": {}
  }
}
```

{% endraw %}

### See also
* [`DeviceControl.ExpectReportState`](#ExpectReportState)
* [`DeviceControl.SynchronizeState`](#SynchronizeState)

## SetValue directive {#SetValue}

클라이언트에게 스피커 볼륨 또는 화면 밝기를 지정한 값으로 설정하거나 특정 TV 채널 번호로 변경하도록 지시합니다.

### Payload field

| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|---------|
| `target`      | string  | 제어 대상.<ul><li><code>"channel"</code>: TV 채널</li><li><code>"screenbrightness"</code>: 화면 밝기</li><li><code>"volume"</code>: 스피커 볼륨</li></ul> | 필수     |
| `value`       | string  | 변경할 값 또는 TV 채널 번호       | 필수     |

### Remarks

* 클라이언트는 맥락 정보인 [`Device.DeviceState`](/CIC/References/Context_Objects.md#DeviceState) 객체를 이용해 수시로 스피커 볼륨 정보와 화면 밝기 정보를 CIC에 전달해야 합니다.
* 클라이언트는 이 지시 메시지에 해당하는 내용을 처리한 후 [`DeviceControl.ActionExecuted`](#ActionExecuted) 또는 [`DeviceControl.ActionFailed`](#ActionFailed) 이벤트 메시지를 이용하여 결과를 CIC에 전달해야 합니다.

### Message example

{% raw %}

```json
{
  "directive": {
    "header": {
      "namespace": "DeviceControl",
      "name": "SetValue",
      "messageId": "23bdfff7-b655-46d4-8655-8bb473bf2bf5",
      "dialogRequestId": "3c6eef8b-8427-4b46-a367-0a7a46432519"
    },
    "payload": {
      "target": "volume",
      "value": "30"
    }
  }
}
```

{% endraw %}

### See also
* [`DeviceControl.ActionExecuted`](#ActionExecuted)
* [`DeviceControl.ActionFailed`](#ActionFailed)
* [`DeviceControl.Decrease`](#Decrease)
* [`DeviceControl.Increase`](#Increase)
* [`DeviceControl.SetValue`](#SetValue)

## SynchronizeState directive {#SynchronizeState}

클라이언트에게 사용자 계정에 등록된 또 다른 클라이언트 기기의 상태 정보를 업데이트하도록 지시합니다. 사용자는 같은 사용자 계정으로 동시에 여러 클라이언트를 사용할 수 있습니다. 예를 들면, 클라이언트의 타입이 앱일 수도 있고 Wave와 같이 Clova 전용 기기인 스피커일 수도 있습니다. 앱 타입의 클라이언트는 스피커 타입의 다른 클라이언트를 제어할 수 있으며, 이때 다른 클라이언트를 제어한 결과를 `DeviceControl.SynchronizeState` 지시 메시지로 받을 수 있고, 이를 이용하여 변경된 클라이언트의 상태를 업데이트할 수 있습니다.

클라이언트는 다음과 같은 상황에 이 지시 메시지를 받을 수 있습니다.

* CIC가 [`DeviceControl.ActionExecuted`](#ActionExecuted) 또는 [`DeviceControl.ActionFailed`](#ActionFailed) 이벤트 메시지를 수신하면 사용자 계정에 등록된 모든 클라이언트에게 `DeviceControl.SynchronizeState` 지시 메시지를 이용하여 특정 클라이언트 기기의 변경된 상태 정보를 전달합니다.
* CIC가 [`DeviceControl.ReportState`](#ReportState) 이벤트 메시지를 수신하면 사용자 계정에 등록된 모든 클라이언트에게 `DeviceControl.SynchronizeState` 지시 메시지를 이용하여 특정 클라이언트 기기의 현재 상태 정보를 전달합니다.

### Payload field

| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|---------|
| `deviceId`    | string  | 상태가 업데이트된 클라이언트 기기의 ID. | 필수     |
| `deviceState` | [Device.DeviceState](/CIC/References/Context_Objects.md#DeviceState) object | 기기 상태 업데이트 정보가 담긴 객체.         | 필수     |

### Remarks

`DeviceControl.SynchronizeState` 지시 메시지는 [downchannel](/CIC/Guides/Interact_with_CIC.md#CreateConnection)을 통해 사용자 계정에 등록된 클라이언트 전체에 브로드캐스팅되며, [대화 ID(`dialogRequestId`)](/CIC/CIC_Overview.md#DialogModel)를 가지지 않습니다.

### Message example

{% raw %}

```json
{
  "directive": {
    "header": {
      "namespace": "DeviceControl",
      "name": "SynchronizeState",
      "messageId": "23bdfff7-b655-46d4-8655-8bb473bf2bf5"
    },
    "payload": {
      "deviceId": "{{CLOVA_OAUTH_CLIENT_ID}}",
      "deviceState": {{Device.DeviceState}}
    }
  }
}
```

{% endraw %}

### See also
* [`DeviceControl.ActionExecuted`](#ActionExecuted)
* [`DeviceControl.ActionFailed`](#ActionFailed)
* [`DeviceControl.ReportState`](#ReportState)

## TurnOff directive {#TurnOff}

클라이언트에게 지정한 기능이나 모드를 끄거나 비활성화하도록 지시합니다. 예를 들면, 이 지시 메시지를 통해 클라이언트 기기의 블루투스를 끄도록 할 수 있습니다.

### Payload field

| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|---------|
| `target`      | string  | 제어 대상.<ul><li><code>"airplane"</code>: 비행기 모드</li><li><code>"bluetooth"</code>: 블루투스</li><li><code>"cellular"</code>: 모바일 통신</li><li><code>"energysave"</code>: 에너지 절약 모드</li><li><code>"flashlight"</code>: 플래시 조명</li><li><code>"gps"</code>: GPS</li><li><code>"power"</code>: 전원 상태</li><li><code>"ring"</code>: 벨소리 모드</li><li><code>"silent"</code>: 무음 모드</li><li><code>"vibrate"</code>: 진동 모드</li><li><code>"wifi"</code>: 무선랜</li></ul> | 필수     |

### Remarks

* 일부 제어 대상을 끄거나 비활성화할 때 클라이언트 기기의 정책이나 상황에 맞춰 제어를 수행해야 합니다. 예를 들면, 벨소리 모드를 비활성화할 경우 진동 모드로 진입할지 음소거 모드로 진입할지는 클라이언트 기기에 따라 구현을 달리할 수 있습니다.
* 클라이언트는 맥락 정보인 [`Device.DeviceState`](/CIC/References/Context_Objects.md#DeviceState) 객체를 이용해 수시로 기능이나 모드의 상태 정보를 CIC에 전달해야 합니다.
* 클라이언트는 이 지시 메시지에 해당하는 내용을 처리한 후 [`DeviceControl.ActionExecuted`](#ActionExecuted) 또는 [`DeviceControl.ActionFailed`](#ActionFailed) 이벤트 메시지를 이용하여 결과를 CIC에 전달해야 합니다.

<div class="danger">
  <p><strong>Caution!</strong></p>
  <p><code>target</code> 필드의 값이 <code>"power"</code>일 경우 클라이언트 기기의 전원을 꺼야 합니다.</p>
</div>

### Message example

{% raw %}

```json
{
  "directive": {
    "header": {
      "namespace": "DeviceControl",
      "name": "TurnOff",
      "messageId": "23bdfff7-b655-46d4-8655-8bb473bf2bf5",
      "dialogRequestId": "3c6eef8b-8427-4b46-a367-0a7a46432519"
    },
    "payload": {
      "target": "bluetooth"
    }
  }
}
```

{% endraw %}

### See also
* [`DeviceControl.ActionExecuted`](#ActionExecuted)
* [`DeviceControl.ActionFailed`](#ActionFailed)
* [`DeviceControl.TurnOn`](#TurnOn)

## TurnOn directive {#TurnOn}

클라이언트에게 지정한 기능을 켜거나 활성화하도록 지시합니다. 예를 들면, 이 지시 메시지를 통해 클라이언트 기기의 블루투스를 켜도록 할 수 있습니다.

### Payload field

| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|---------|
| `target`      | string  | 제어 대상.<ul><li><code>"airplane"</code>: 비행기 모드</li><li><code>"bluetooth"</code>: 블루투스</li><li><code>"cellular"</code>: 모바일 통신</li><li><code>"energysave"</code>: 에너지 절약 모드</li><li><code>"flashlight"</code>: 플래시 조명</li><li><code>"gps"</code>: GPS</li><li><code>"power"</code>: 전원 상태</li><li><code>"ring"</code>: 벨소리 모드</li><li><code>"silent"</code>: 무음 모드</li><li><code>"vibrate"</code>: 진동 모드</li><li><code>"wifi"</code>: 무선랜</li></ul> | 필수     |

### Remarks

* 클라이언트는 맥락 정보인 [`Device.DeviceState`](/CIC/References/Context_Objects.md#DeviceState) 객체를 이용해 수시로 기능이나 모드의 상태 정보를 CIC에 전달해야 합니다.
* 클라이언트는 이 지시 메시지에 해당하는 내용을 처리한 후 [`DeviceControl.ActionExecuted`](#ActionExecuted) 또는 [`DeviceControl.ActionFailed`](#ActionFailed) 이벤트 메시지를 이용하여 결과를 CIC에 전달해야 합니다.

### Message example

{% raw %}

```json
{
  "directive": {
    "header": {
      "namespace": "DeviceControl",
      "name": "TurnOff",
      "messageId": "23bdfff7-b655-46d4-8655-8bb473bf2bf5",
      "dialogRequestId": "3c6eef8b-8427-4b46-a367-0a7a46432519"
    },
    "payload": {
      "target": "bluetooth"
    }
  }
}
```

{% endraw %}

### See also
* [`DeviceControl.ActionExecuted`](#ActionExecuted)
* [`DeviceControl.ActionFailed`](#ActionFailed)
* [`DeviceControl.TurnOn`](#TurnOn)
