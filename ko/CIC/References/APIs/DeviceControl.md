# DeviceControl

클라이언트 기기를 제어하거나 클라이언트 기기 제어 수행 결과를 CIC로 보고할 때 사용하는 API입니다.

일부 사용자의 요청은 클라이언트 기기를 제어하는 요청일 수 있습니다. 분석된 사용자의 요청이 클라이언트 기기를 제어하는 요청이면 네임스페이스 `DeviceControl`인 지시 메시지를 받게 되며 클라이언트는 수신한 지시 메시지에 맞게 클라이언트 기기를 제어해야 합니다. 클라이언트 기기 제어를 수행한 후 그 결과를 이벤트 메시지를 사용하여 CIC에 전송해야 합니다.

DeviceControl API가 제공하는 이벤트 메시지와 지시 메시지는 다음과 같습니다.

| 메시지 이름         | 메시지 타입  | 메시지 설명                                   |
|------------------|-----------|---------------------------------------------|
| [`ActionExecuted`](#ActionExecuted)       | Event     | 클라이언트는 기기 제어를 정상적으로 수행한 경우 이 이벤트 메시지를 CIC로 전송해야 합니다.           |
| [`ActionFailed`](#ActionFailed)           | Event     | 클라이언트는 기기 제어를 수행할 수 없거나 수행에 실패한 경우 이 이벤트 메시지를 CIC로 전송해야 합니다. |
| [`BtConnect`](#BtConnect)                 | Directive | 클라이언트에게 특정 블루투스 기기와 연결을 설정하도록 지시합니다.                             |
| [`BtDisconnect`](#BtDisconnect)           | Directive | 클라이언트에게 특정 블루투스 기기와 연결을 해제하도록 지시합니다.                             |
| [`BtStartPairing`](#BtStartPairing)       | Directive | 클라이언트에게 블루투스 페어링 모드를 시작하도록 지시합니다.                                 |
| [`BtStopPairing`](#BtStopPairing)         | Directive | 클라이언트에게 블루투스 페어링 모드로 중지하도록 지시합니다.                                 |
| [`Decrease`](#Decrease)                   | Directive | 클라이언트에게 스피커 볼륨 또는 화면 밝기를 기본 단위만큼 줄이도록 지시합니다.                   |
| [`Increase`](#Increase)                   | Directive | 클라이언트에게 스피커 볼륨 또는 화면 밝기를 기본 단위만큼 높이도록 지시합니다.                   |
| [`OpenScreen`](#OpenScreen)               | Directive | 클라이언트에게 설정 화면을 열도록 지시합니다.                                            |
| [`SetValue`](#SetValue)                   | Directive | 클라이언트에게 스피커 볼륨 또는 화면 밝기를 지정한 값으로 설정하도록 지시합니다.                  |
| [`TurnOff`](#TurnOff)                     | Directive | 클라이언트에게 지정한 기능이나 모드를 끄거나 비활성화하도록 지시합니다.                         |
| [`TurnOn`](#TurnOn)                       | Directive | 클라이언트에게 지정한 기능을 켜거나 활성화하도록 지시합니다.                                 |
| [`UpdateDeviceState`](#UpdateDeviceState) | Directive | 클라이언트에게 사용자 계정에 등록된 또 다른 클라이언트 기기의 상태를 업데이트하도록 지시합니다.       |

<div class="note">
  <p><strong>Note!</strong></p>
  <p>DeviceControl API는 현재 구현 예정인 명세입니다. 사전 인터페이스 협의를 위해 미리 기술되었으며, 추후 내용이 변경될 수도 있습니다.</p>
</div>

## ActionExecuted event {#ActionExecuted}

클라이언트는 기기 제어를 정상적으로 수행한 경우 이 지시 메시지를 CIC로 전송해야 합니다.

### Payload field

| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|---------|
| `target`      | string  | 제어 대상.<ul><li><code>"airplane"</code> : 비행기 모드</li><li><code>"bluetooth"</code> : 블루투스</li><li><code>"screenbrightness"</code> : 화면 밝기</li><li><code>"cellular"</code> : 모바일 통신</li><li><code>"flashlight"</code> : 플래시 조명</li><li><code>"gps"</code> : GPS</li><li><code>"powersave"</code> : 절전 모드</li><li><code>"soundmode"</code> : 사운드 모드</li><li><code>"volume"</code> : 스피커 볼륨</li><li><code>"wifi"</code> : 무선랜</li></ul> | 필수     |
| `command`     | string  | 정상 수행한 동작.  <ul><li>BtConnect</li><li>BtDisconnect</li><li>BtStartPairing</li><li>BtStopPairing</li><li>Decrease</li><li>Increase</li><li>OpenScreen</li><li>SetValue</li><li>TurnOn</li><li>TurnOff</li></ul> | 필수   |

### Remarks

CIC는 이 이벤트 메시지를 수신하면 사용자 계정에 등록된 모든 클라이언트에게 [`UpdateDeviceState`](#UpdateDeviceState) 지시 메시지를 전송하여 특정 클라이언트 기기의 변경된 상태 정보를 알립니다.

### Message example

{% raw %}

```json
{
  "directive": {
    "header": {
      "namespace": "DeviceControl",
      "name": "ActionExecuted",
      "messageId": "23bdfff7-b655-46d4-8655-8bb473bf2bf5",
      "dialogRequestId": "3c6eef8b-8427-4b46-a367-0a7a46432519"
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
* [`ActionFailed`](#ActionFailed)
* [`BtConnect`](#BtConnect)
* [`BtDisconnect`](#BtDisconnect)
* [`BtStartPairing`](#BtStartPairing)
* [`BtStopPairing`](#BtStopPairing)
* [`Decrease`](#Decrease)
* [`Increase`](#Increase)
* [`OpenScreen`](#OpenScreen)
* [`SetValue`](#SetValue)
* [`TurnOff`](#TurnOff)
* [`TurnOn`](#TurnOn)

## ActionFailed event {#ActionFailed}

클라이언트는 기기 제어를 수행할 수 없거나 수행에 실패한 경우 이 지시 메시지를 CIC로 전송해야 합니다.

### Payload field

| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|---------|
| `target`      | string  | 제어 대상.<ul><li><code>"airplane"</code> : 비행기 모드</li><li><code>"bluetooth"</code> : 블루투스</li><li><code>"screenbrightness"</code> : 화면 밝기</li><li><code>"cellular"</code> : 모바일 통신</li><li><code>"flashlight"</code> : 플래시 조명</li><li><code>"gps"</code> : GPS</li><li><code>"powersave"</code> : 절전 모드</li><li><code>"soundmode"</code> : 사운드 모드</li><li><code>"volume"</code> : 스피커 볼륨</li><li><code>"wifi"</code> : 무선랜</li></ul> | 필수     |
| `command`     | string  | 실패한 동작. <ul><li>BtConnect</li><li>BtDisconnect</li><li>BtStartPairing</li><li>BtStopPairing</li><li>Decrease</li><li>Increase</li><li>OpenScreen</li><li>SetValue</li><li>TurnOn</li><li>TurnOff</li></ul> | 필수   |

### Remarks

CIC는 이 이벤트 메시지를 수신하면 사용자 계정에 등록된 모든 클라이언트에게 [`UpdateDeviceState`](#UpdateDeviceState) 지시 메시지를 전송하여 특정 클라이언트 기기의 변경된 상태 정보를 알립니다.

### Message example

{% raw %}

```json
{
  "directive": {
    "header": {
      "namespace": "DeviceControl",
      "name": "ActionFailed",
      "messageId": "23bdfff7-b655-46d4-8655-8bb473bf2bf5",
      "dialogRequestId": "3c6eef8b-8427-4b46-a367-0a7a46432519"
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
* [`ActionExecuted`](#ActionExecuted)
* [`BtConnect`](#BtConnect)
* [`BtDisconnect`](#BtDisconnect)
* [`BtStartPairing`](#BtStartPairing)
* [`BtStopPairing`](#BtStopPairing)
* [`Decrease`](#Decrease)
* [`Increase`](#Increase)
* [`OpenScreen`](#OpenScreen)
* [`SetValue`](#SetValue)
* [`TurnOff`](#TurnOff)
* [`TurnOn`](#TurnOn)

## BtConnect directive {#BtConnect}

클라이언트에게 페어링된 블루투스 기기 중 하나와 연결을 설정하도록 지시합니다. 한 대 이상의 기기와 페어링되어 있는 경우 각각의 클라이언트는 기준에 따라 어떤 기기와 연결을 설정할지 결정해야 합니다. 예를 들면, 가장 최근에 연결했던 순서대로 기기 연결을 시도할 수 있습니다.

### Payload field

없음

### Remarks

* 스피커 형태의 블루투스 기기만 지원합니다.
* 클라이언트는 맥락 정보인 [`Device.DeviceState`](/CIC/References/Context_Objects.md#DeviceState) 객체를 이용해 수시로 블루투스 기기 정보를 CIC에 전달해야 합니다.
* 클라이언트는 이 지시 메시지에 해당하는 내용을 처리한 후 [`ActionExecuted`](#ActionExecuted) 또는 [`ActionFailed`](#ActionFailed) 이벤트 메시지를 이용하여 결과를 CIC에 전달해야 합니다.

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
* [`ActionExecuted`](#ActionExecuted)
* [`ActionFailed`](#ActionFailed)
* [`BtDisconnect`](#BtDisconnect)
* [`BtStartPairing`](#BtPairing)
* [`BtStopPairing`](#BtStopPairing)
* [`TurnOff`](#TurnOff)
* [`TurnOn`](#TurnOn)

## BtDisonnect directive {#BtDisonnect}

클라이언트에게 연결된 블루투스 기기와 연결을 끊도록 지시합니다.

### Payload field

없음

### Remarks

* 스피커 형태의 블루투스 기기만 지원합니다.
* 클라이언트는 맥락 정보인 [`Device.DeviceState`](/CIC/References/Context_Objects.md#DeviceState) 객체를 이용해 수시로 블루투스 기기 정보를 CIC에 전달해야 합니다.
* 클라이언트는 이 지시 메시지에 해당하는 내용을 처리한 후 [`ActionExecuted`](#ActionExecuted) 또는 [`ActionFailed`](#ActionFailed) 이벤트 메시지를 이용하여 결과를 CIC에 전달해야 합니다.

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
* [`ActionExecuted`](#ActionExecuted)
* [`ActionFailed`](#ActionFailed)
* [`BtConnect`](#BtConnect)
* [`BtStartPairing`](#BtPairing)
* [`BtStopPairing`](#BtStopPairing)
* [`TurnOff`](#TurnOff)
* [`TurnOn`](#TurnOn)

## BtStartPairing directive {#BtStartPairing}

클라이언트에게 블루투스 페어링 모드를 시작하도록 지시합니다.

### Payload field

없음

### Remarks

* 스피커 형태의 블루투스 기기만 지원합니다.
* 클라이언트는 맥락 정보인 [`Device.DeviceState`](/CIC/References/Context_Objects.md#DeviceState) 객체를 이용해 수시로 블루투스 기기 정보를 CIC에 전달해야 합니다.
* 클라이언트는 이 지시 메시지에 해당하는 내용을 처리한 후 [`ActionExecuted`](#ActionExecuted) 또는 [`ActionFailed`](#ActionFailed) 이벤트 메시지를 이용하여 결과를 CIC에 전달해야 합니다.

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
* [`ActionExecuted`](#ActionExecuted)
* [`ActionFailed`](#ActionFailed)
* [`BtConnect`](#BtConnect)
* [`BtDisconnect`](#BtDisconnect)
* [`BtStopPairing`](#BtStopPairing)
* [`TurnOff`](#TurnOff)
* [`TurnOn`](#TurnOn)

## BtStopPairing directive {#BtStopPairing}

클라이언트에게 블루투스 페어링 모드를 중지하도록 지시합니다.

### Payload field

없음

### Remarks

* 스피커 형태의 블루투스 기기만 지원합니다.
* 클라이언트는 맥락 정보인 [`Device.DeviceState`](/CIC/References/Context_Objects.md#DeviceState) 객체를 이용해 수시로 블루투스 기기 정보를 CIC에 전달해야 합니다.
* 클라이언트는 이 지시 메시지에 해당하는 내용을 처리한 후 [`ActionExecuted`](#ActionExecuted) 또는 [`ActionFailed`](#ActionFailed) 이벤트 메시지를 이용하여 결과를 CIC에 전달해야 합니다.

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
* [`ActionExecuted`](#ActionExecuted)
* [`ActionFailed`](#ActionFailed)
* [`BtConnect`](#BtConnect)
* [`BtDisconnect`](#BtDisconnect)
* [`BtStartPairing`](#BtStopPairing)
* [`TurnOff`](#TurnOff)
* [`TurnOn`](#TurnOn)

## Decrease directive {#Decrease}

클라이언트에게 스피커 볼륨 또는 화면 밝기를 기본 단위만큼 줄이도록 지시하거나, TV 채널을 이전 채널로 변경하도록 지시합니다.

### Payload field

| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|---------|
| `target`      | string  | 제어 대상.<ul><li><code>"channel"</code> : TV 채널</li><li><code>"screenbrightness"</code> : 화면 밝기</li><li><code>"volume"</code> : 스피커 볼륨</li></ul> | 필수     |

### Remarks

* 기본 단위는 클라이언트측에서 직접 결정하면 됩니다.
* 클라이언트는 맥락 정보인 [`Device.DeviceState`](/CIC/References/Context_Objects.md#DeviceState) 객체를 이용해 수시로 스피커 볼륨 정보와 화면 밝기 정보를 CIC에 전달해야 합니다.
* 클라이언트는 이 지시 메시지에 해당하는 내용을 처리한 후 [`ActionExecuted`](#ActionExecuted) 또는 [`ActionFailed`](#ActionFailed) 이벤트 메시지를 이용하여 결과를 CIC에 전달해야 합니다.

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
* [`ActionExecuted`](#ActionExecuted)
* [`ActionFailed`](#ActionFailed)
* [`Increase`](#Increase)
* [`SetValue`](#SetValue)

## Increase directive {#Increase}

클라이언트에게 스피커 볼륨 또는 화면 밝기를 기본 단위만큼 높이도록 지시하거나, TV 채널을 다음 채널로 변경하도록 지시합니다.

### Payload field

| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|---------|
| `target`      | string  | 제어 대상.<ul><li><code>"channel"</code> : TV 채널</li><li><code>"screenbrightness"</code> : 화면 밝기</li><li><code>"volume"</code> : 스피커 볼륨</li></ul> | 필수     |

### Remarks

* 기본 단위는 클라이언트측에서 직접 결정하면 됩니다.
* 클라이언트는 맥락 정보인 [`Device.DeviceState`](/CIC/References/Context_Objects.md#DeviceState) 객체를 이용해 수시로 스피커 볼륨 정보와 화면 밝기 정보를 CIC에 전달해야 합니다.
* 클라이언트는 이 지시 메시지에 해당하는 내용을 처리한 후 [`ActionExecuted`](#ActionExecuted) 또는 [`ActionFailed`](#ActionFailed) 이벤트 메시지를 이용하여 결과를 CIC에 전달해야 합니다.

### Message example

{% raw %}

```json
{
  "directive": {
    "header": {
      "namespace": "DeviceControl",
      "name": "Increse",
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
* [`ActionExecuted`](#ActionExecuted)
* [`ActionFailed`](#ActionFailed)
* [`Decrease`](#Decrease)
* [`SetValue`](#SetValue)

## OpenScreen directive {#OpenScreen}

클라이언트에게 설정 화면을 열도록 지시합니다.

### Payload field

| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|---------|
| `target`      | string  | 표시할 화면. 현재는 설정 화면을 여는 값인 `"settings"`만 입력됩니다. | 필수     |

### Remarks

클라이언트는 이 지시 메시지에 해당하는 내용을 처리한 후 [`ActionExecuted`](#ActionExecuted) 또는 [`ActionFailed`](#ActionFailed) 이벤트 메시지를 이용하여 결과를 CIC에 전달해야 합니다.

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
* [`ActionExecuted`](#ActionExecuted)
* [`ActionFailed`](#ActionFailed)

## SetValue directive {#SetValue}

클라이언트에게 스피커 볼륨 또는 화면 밝기를 지정한 값으로 설정하거나 특정 TV 채널 번호로 변경하도록 지시합니다.

### Payload field

| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|---------|
| `target`      | string  | 제어 대상.<ul><li><code>"channel"</code> : TV 채널</li><li><code>"screenbrightness"</code> : 화면 밝기</li><li><code>"volume"</code> : 스피커 볼륨</li></ul> | 필수     |
| `value`       | string  | 변경할 값 또는 TV 채널 번호       | 필수     |

### Remarks

* 클라이언트는 맥락 정보인 [`Device.DeviceState`](/CIC/References/Context_Objects.md#DeviceState) 객체를 이용해 수시로 스피커 볼륨 정보와 화면 밝기 정보를 CIC에 전달해야 합니다.
* 클라이언트는 이 지시 메시지에 해당하는 내용을 처리한 후 [`ActionExecuted`](#ActionExecuted) 또는 [`ActionFailed`](#ActionFailed) 이벤트 메시지를 이용하여 결과를 CIC에 전달해야 합니다.

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
* [`ActionExecuted`](#ActionExecuted)
* [`ActionFailed`](#ActionFailed)
* [`Decrease`](#Decrease)
* [`Increase`](#Increase)
* [`SetValue`](#SetValue)

## TurnOff directive {#TurnOff}

클라이언트에게 지정한 기능이나 모드를 끄거나 비활성화하도록 지시합니다. 예를 들면, 이 지시 메시지를 통해 클라이언트 기기의 블루투스를 끄도록 할 수 있습니다.

### Payload field

| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|---------|
| `target`      | string  | 제어 대상.<ul><li><code>"airplane"</code> : 비행기 모드</li><li><code>"bluetooth"</code> : 블루투스</li><li><code>"cellular"</code> : 모바일 통신</li><li><code>"energysave"</code> : 에너지 절약 모드</li><li><code>"flashlight"</code> : 플래시 조명</li><li><code>"gps"</code> : GPS</li><li><code>"power"</code> : 전원 상태</li><li><code>"ring"</code> : 벨소리 모드</li><li><code>"silent"</code> : 무음 모드</li><li><code>"vibrate"</code> : 진동 모드</li><li><code>"wifi"</code> : 무선랜</li></ul> | 필수     |

### Remarks

* 일부 제어 대상을 끄거나 비활성화할 때 클라이언트 기기의 정책이나 상황에 맞춰 제어를 수행해야 합니다. 예를 들면, 벨소리 모드를 비활성화할 경우 진동 모드로 진입할지 음소거 모드로 진입할지는 클라이언트 기기에 따라 구현을 달리할 수 있습니다.
* 클라이언트는 맥락 정보인 [`Device.DeviceState`](/CIC/References/Context_Objects.md#DeviceState) 객체를 이용해 수시로 기능이나 모드의 상태 정보를 CIC에 전달해야 합니다.
* 클라이언트는 이 지시 메시지에 해당하는 내용을 처리한 후 [`ActionExecuted`](#ActionExecuted) 또는 [`ActionFailed`](#ActionFailed) 이벤트 메시지를 이용하여 결과를 CIC에 전달해야 합니다.

<div class="danger">
  <p><strong>Cautiona!</strong></p>
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
* [`ActionExecuted`](#ActionExecuted)
* [`ActionFailed`](#ActionFailed)
* [`TurnOn`](#TurnOn)

## TurnOn directive {#TurnOn}

클라이언트에게 지정한 기능을 켜거나 활성화하도록 지시합니다. 예를 들면, 이 지시 메시지를 통해 클라이언트 기기의 블루투스를 켜도록 할 수 있습니다.

### Payload field

| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|---------|
| `target`      | string  | 제어 대상.<ul><li><code>"airplane"</code> : 비행기 모드</li><li><code>"bluetooth"</code> : 블루투스</li><li><code>"cellular"</code> : 모바일 통신</li><li><code>"energysave"</code> : 에너지 절약 모드</li><li><code>"flashlight"</code> : 플래시 조명</li><li><code>"gps"</code> : GPS</li><li><code>"power"</code> : 전원 상태</li><li><code>"ring"</code> : 벨소리 모드</li><li><code>"silent"</code> : 무음 모드</li><li><code>"vibrate"</code> : 진동 모드</li><li><code>"wifi"</code> : 무선랜</li></ul> | 필수     |

### Remarks

* 클라이언트는 맥락 정보인 [`Device.DeviceState`](/CIC/References/Context_Objects.md#DeviceState) 객체를 이용해 수시로 기능이나 모드의 상태 정보를 CIC에 전달해야 합니다.
* 클라이언트는 이 지시 메시지에 해당하는 내용을 처리한 후 [`ActionExecuted`](#ActionExecuted) 또는 [`ActionFailed`](#ActionFailed) 이벤트 메시지를 이용하여 결과를 CIC에 전달해야 합니다.

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
* [`ActionExecuted`](#ActionExecuted)
* [`ActionFailed`](#ActionFailed)
* [`TurnOn`](#TurnOn)


## UpdateDeviceState directive {#UpdateDeviceState}

클라이언트에게 사용자 계정에 등록된 또 다른 클라이언트 기기의 상태 정보를 업데이트하도록 지시합니다. 사용자는 같은 사용자 계정으로 동시에 여러 클라이언트를 사용할 수 있습니다. 클라이언트의 타입이 앱일 수도 있고 Wave와 같이 Clova 전용 기기인 스피커일 수도 있습니다. 앱 타입의 클라이언트는 스피커 타입의 다른 클라이언트를 제어할 수 있으며, 이때 다른 클라이언트를 제어한 결과를 `UpdateDeviceState` 지시 메시지로 받을 수 있고, 이를 이용하여 변경된 클라이언트의 상태를 업데이트할 수 있습니다.

### Payload field

| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|---------|
| `deviceId`    | string  | 상태가 업데이트된 클라이언트 기기의 ID. | 필수     |
| `deviceState` | [Device.DeviceState](/CIC/References/Context_Objects.md#DeviceState) object | 기기 상태 업데이트 정보가 담긴 객체.         | 필수     |

### Remarks
* CIC는 [`ActionExecuted`](#ActionExecuted) 또는 [`ActionFailed`](#ActionFailed) 이벤트 메시지를 수신하면 사용자 계정에 등록된 모든 클라이언트에게 `UpdateDeviceState` 지시 메시지를 이용하여 특정 클라이언트 기기의 변경된 상태 정보를 전달합니다.
* `UpdateDeviceState` 지시 메시지는 Downchannel을 통해 사용자 계정에 등록된 클라이언트 전체에 브로드캐스팅되며, 대화 ID(`dialogRequestId`)를 가지지 않습니다.

### Message example

{% raw %}

```json
{
  "directive": {
    "header": {
      "namespace": "DeviceControl",
      "name": "UpdateDeviceState",
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
* [`ActionExecuted`](#ActionExecuted)
* [`ActionFailed`](#ActionFailed)
