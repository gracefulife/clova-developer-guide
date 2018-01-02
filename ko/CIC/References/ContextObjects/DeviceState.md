## Device.DeviceState {#DeviceState}
`Device.DeviceState`는 클라이언트의 기기의 상태 정보를 CIC에게 보고할 때 사용하는 메시지 포맷입니다.

### Object structure
{% raw %}

```json
{
  "header": {
    "namespace": "Device",
    "name": "DeviceState"
  },
  "payload": {
    "airplane": {{AirplaneInfoObject}},
    "battery": {{BatteryInfoObject}},
    "bluetooth": {{BluetoothInfoObject}},
    "cellular": {{CellularInfoObject}},
    "channel": {{ChannelInfoObject}},
    "energySavingMode": {{EnergySavingModeInfoObject}},
    "flashLight" {{FlashLightInfoObject}},
    "gps": {{GPSInfoObject}},
    "localTime": {{string}},
    "power": {{{PowerInforObject}},
    "screenBrightness": {{ScreenBrightnessInfoObject}},
    "soundMode": {{SoundModeInfoObject}},
    "volume": {{VolumeInfoObject}},
    "wifi": {{WifiInfoObject}}
  }
}
```

{% endraw %}

### Payload fields

| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|---------|
| `airplane`        | [AirplaneInfoObject](#AirplaneInfoObject)               | 클라이언트 기기의 비행기 모드 설정 정보를 보고할 때 사용하는 객체      | 선택 |
| `battery`         | [BatteryInfoObject](#BatteryInfoObject)                 | 클라이언트 기기의 배터리 정보를 보고할 때 사용하는 객체              | 선택 |
| `bluetooth`       | [BluetoothInfoObject](#BluetoothInfoObject)             | 클라이언트 기기의 블루투스 활성화 상태 및 블루투스 기기 연결 상태 정보를 보고할 때 사용하는 객체       | 선택 |
| `cellular`        | [CellularInfoObject](#CellularInfoObject)               | 클라이언트 기기의 모바일 통신 활성화 상태 정보를 보고할 때 사용하는 객체 | 선택 |
| `channel`         | [ChannelInfoObject](#ChannelInfoObject)                 | 클라이언트 기기의 TV 채널 설정 정보를 보고할 때 사용하는 객체         | 선택 |
| `energySavingMode` | [EnergySavingModeInfoObject](#EnergySavingModeInfoObject) | 클라이언트 기기의 에너지 절약 모드 정보를 보고할 때 사용하는 객체     | 선택 |
| `flashLight`      | [FlashLightInfoObject](#FlashLightInfoObject)           | 클라이언트 기기의 플래시 조명 설정 정보를 보고할 때 사용하는 객체       | 선택 |
| `gps`             | [GPSInfoObject](#GPSInfoObject)                         | 클라이언트 기기의 GPS 설정 정보를 보고할 때 사용하는 객체            | 선택 |
| `localTime`       | string | 클라이언트 기기에 설정된 현지 시간([ISO 8601](https://en.wikipedia.org/wiki/ISO_8601) 포맷)              | 선택 |
| `power`           | [PowerInfoObject](#PowerInfoObject)                     | 클라이언트 기기의 전원 상태 정보를 보고할 때 사용하는 객체            | 선택 |
| `screenBrightness` | [ScreenBrightnessInfoObject](#ScreenBrightnessInfoObject) | 클라이언트 기기의 화면 밝기 정보를 보고할 때 사용하는 객체            | 선택 |
| `soundMode`       | [SoundModeInfoObject](#SoundModeInfoObject)             | 클라이언트 기기의 소리 출력 설정 정보를 보고할 때 사용하는 객체        | 선택 |
| `volume`          | [VolumeInfoObject](#VolumeInfoObject)                   | 클라이언트 기기의 스피커 볼륨 정보를 보고할 때 사용하는 객체           | 선택 |
| `wifi`            | [WifiInfoObject](#WifiInfoObject)                       | 클라이언트 기기의 무선 네트워크(Wi-Fi) 기능 활성화 상태와 무선 네트워크 연결 정보를 보고할 때 사용하는 객체    | 선택 |

### Object example
{% raw %}

```json
{
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
}
```

{% endraw %}

### AirplaneInfoObject {#AirplaneInfoObject}
클라이언트 기기의 비행기 모드 설정 정보를 보고할 때 사용하는 객체입니다.

#### Object fields

| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|---------|
| `actions[]`     | string array | 비행기 모드와 관련하여 수행할 수 있는 [`DeviceControl`](/CIC/References/CICInterface/DeviceControl.md) API 목록. 다음 동작 목록 중 클라이언트 기기가 실제로 수행할 수 있는 동작을 입력합니다.<ul><li>"TurnOff"</li><li>"TurnOn"</li></ul> | 필수 |
| `state`         | string | 비행기 모드 설정 상태.<ul><li><code>"off"</code>: 꺼짐</li><li><code>"on"</code>: 켜짐</li></ul> | 필수 |

#### Object example

{% raw %}

```json
{
  "header": {
    "namespace": "Device",
    "name": "DeviceState"
  },
  "payload": {
    ...
    "airplane": {
        "actions": [
            "TurnOff",
            "TurnOn"
        ],
        "state": "on"
    },
    ...
  }
}
```

{% endraw %}

### BatteryInfoObject {#BatteryInfoObject}
클라이언트 기기의 배터리 상태 정보를 보고할 때 사용하는 객체입니다.

#### Object fields

| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|---------|
| `actions[]`     | string array | 배터리와 관련하여 수행할 수 있는 [`DeviceControl`](/CIC/References/CICInterface/DeviceControl.md) API 목록. 현재 지원하는 동작이 없습니다. | 필수 |
| `value`         | number | 배터리 잔량. 0에서 100 사이의 숫자를 입력해야 하며, 단위는 퍼센트(%) 입니다. | 필수 |
| `charging`      | boolean | 충전 중인지 여부.<ul><li><code>true</code>: 충전 중인 상태</li><li><code>false</code>: 충전 중이지 않은 상태</li></ul> | 필수 |

#### Object example

{% raw %}

```json
{
  "header": {
    "namespace": "Device",
    "name": "DeviceState"
  },
  "payload": {
    ...
    "battery": {
        "actions": [],
        "value": 98,
        "charging": false
    },
    ...
  }
}
```

{% endraw %}

### BluetoothInfoObject {#BluetoothInfoObject}
클라이언트 기기의 블루투스 활성화 상태 및 블루투스 기기 연결 상태 정보를 보고할 때 사용하는 객체입니다.

#### Object fields

| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|---------|
| `actions[]`          | string array | 블루투스 연결과 관련하여 수행할 수 있는 [`DeviceControl`](/CIC/References/CICInterface/DeviceControl.md) API 목록. 다음 동작 목록 중 클라이언트 기기가 실제로 수행할 수 있는 동작을 입력합니다. <ul><li>"TurnOff"</li><li>"TurnOn"</li><li>"BtConnect"</li><li>"BtDisconnect"</li><li>"BtStartPairing"</li><li>"BtStopPairing"</li></ul> | 필수 |
| `btlist[]`           | object array | 페어링된 블루투스 기기 정보를 가지는 객체 배열         | 필수 |
| `btlist[].name`      | string       | 블루투스 기기의 이름                      | 필수 |
| `btlist[].address`   | string       | 블루투스 기기의 MAC 주소                  | 필수 |
| `btlist[].connected` | boolean      | 블루투스 기기와의 연결 여부. <ul><li><code>true</code>: 연결된 상태</li><li><code>false</code>: 연결되어 있지 않은 상태</li></ul> | 필수 |
| `state`              | string       | 블루투스 활성화 상태. <ul><li><code>"off"</code>: 꺼짐</li><li><code>"on"</code>: 켜짐</li></ul> | 필수 |

#### Object example

{% raw %}

```json
{
  "header": {
    "namespace": "Device",
    "name": "DeviceState"
  },
  "payload": {
    ...
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
    ...
  }
}
```

{% endraw %}

### CellularInfoObject {#CellularInfoObject}
클라이언트 기기의 모바일 통신 활성화 상태 정보를 보고할 때 사용하는 객체입니다.

#### Object fields

| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|---------|
| `actions[]`          | string array | 모바일 데이터 통신과 관련하여 수행할 수 있는 [`DeviceControl`](/CIC/References/CICInterface/DeviceControl.md) API 목록. 다음 동작 목록 중 클라이언트 기기가 실제로 수행할 수 있는 동작을 입력합니다. <ul><li>"TurnOff"</li><li>"TurnOn"</li></ul> | 필수 |
| `state`              | string       | 모바일 데이터 통신 활성화 여부. <ul><li><code>"off"</code>: 꺼짐</li><li><code>"on"</code>: 켜짐</li></ul> | 필수 |

#### Object example

{% raw %}

```json
{
  "header": {
    "namespace": "Device",
    "name": "DeviceState"
  },
  "payload": {
    ...
    "cellular": {
        "actions": [
            "TurnOff",
            "TurnOn"
        ],
        "state": "off"
    },
    ...
  }
}
```

{% endraw %}

### ChannelInfoObject {#ChannelInfoObject}
클라이언트 기기의 TV 채널 설정 정보를 보고할 때 사용하는 객체입니다.

#### Object fields

| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|---------|
| `actions[]`     | string array | TV 채널 설정과 관련하여 수행할 수 있는 [`DeviceControl`](/CIC/References/CICInterface/DeviceControl.md) API 목록. 다음 동작 목록 중 클라이언트 기기가 실제로 수행할 수 있는 동작을 입력합니다.<ul><li>"Decrease"</li><li>"Increase"</li><li>"SetValue"</li></ul> | 필수 |

#### Object example

{% raw %}

```json
{
  "header": {
    "namespace": "Device",
    "name": "DeviceState"
  },
  "payload": {
    ...
    "channel": {
        "actions": [
            "Decrease",
            "Increase",
            "SetValue"
        ]
    },
    ...
  }
}
```

{% endraw %}


### EnergySavingModeInfoObject {#EnergySavingModeInfoObject}
클라이언트 기기의 에너지 절약 모드 정보를 보고할 때 사용하는 객체입니다.

#### Object fields

| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|---------|
| `actions[]`          | string array | 절전 모드와 관련하여 수행할 수 있는 [`DeviceControl`](/CIC/References/CICInterface/DeviceControl.md) API 목록. 다음 동작 목록 중 클라이언트 기기가 실제로 수행할 수 있는 동작을 입력합니다. <ul><li>"TurnOff"</li><li>"TurnOn"</li></ul> | 필수 |
| `state`              | string       | 절전 모드 설정 상태. <ul><li><code>"off"</code>: 꺼짐</li><li><code>"on"</code>: 켜짐</li></ul> | 필수 |

#### Object example

{% raw %}

```json
{
  "header": {
    "namespace": "Device",
    "name": "DeviceState"
  },
  "payload": {
    ...
    "energySavingMode": {
        "actions": [
            "TurnOff",
            "TurnOn"
        ],
        "state": "off"
    },
    ...
  }
}
```

{% endraw %}


### FlashLightInfoObject {#FlashLightInfoObject}
클라이언트 기기의 플래시 조명 설정 정보를 보고할 때 사용하는 객체입니다.

#### Object fields

| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|---------|
| `actions[]`          | string array | 플래시 조명과 관련하여 수행할 수 있는 [`DeviceControl`](/CIC/References/CICInterface/DeviceControl.md) API 목록. 다음 동작 목록 중 클라이언트 기기가 실제로 수행할 수 있는 동작을 입력합니다. <ul><li>"TurnOff"</li><li>"TurnOn"</li></ul> | 필수 |
| `state`              | string       | 플래시 조명의 현재 상태. <ul><li><code>"off"</code>: 꺼짐</li><li><code>"on"</code>: 켜짐</li></ul> | 필수 |

#### Object example

{% raw %}

```json
{
  "header": {
    "namespace": "Device",
    "name": "DeviceState"
  },
  "payload": {
    ...
    "flashLight": {
        "actions": [
            "TurnOff",
            "TurnOn"
        ],
        "state": "off"
    },
    ...
  }
}
```

{% endraw %}

### GPSInfoObject {#GPSInfoObject}
클라이언트 기기의 GPS 상태 정보를 보고할 때 사용하는 객체입니다.

#### Object fields

| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|---------|
| `actions[]`          | string array | GPS와 관련하여 수행할 수 있는 [`DeviceControl`](/CIC/References/CICInterface/DeviceControl.md) API 목록. 다음 동작 목록 중 클라이언트 기기가 실제로 수행할 수 있는 동작을 입력합니다. <ul><li>"TurnOff"</li><li>"TurnOn"</li></ul> | 필수 |
| `state`              | string       | GPS의 현재 상태. <ul><li><code>"off"</code>: 꺼짐</li><li><code>"on"</code>: 켜짐</li></ul> | 필수 |

#### Object example

{% raw %}

```json
{
  "header": {
    "namespace": "Device",
    "name": "DeviceState"
  },
  "payload": {
    ...
    "gps": {
        "actions": [
            "TurnOff",
            "TurnOn"
        ],
        "state": "off"
    },
    ...
  }
}
```

{% endraw %}

### PowerInfoObject {#PowerInfoObject}
클라이언트 기기의 전원 상태 정보를 보고할 때 사용하는 객체입니다.

#### Object fields

| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|---------|
| `actions[]`          | string array | 전원 상태와 관련하여 수행할 수 있는 [`DeviceControl`](/CIC/References/CICInterface/DeviceControl.md) API 목록. 다음 동작 목록 중 클라이언트 기기가 실제로 수행할 수 있는 동작을 입력합니다. <ul><li>"TurnOff"</li><li>"TurnOn"</li></ul> | 필수 |
| `state`              | string       | 전원 상태. <ul><li><code>"active"</code>: 클라이언트 기기 켜짐</li><li><code>"idle"</code>: 클라이언트 기기 꺼짐</li></ul> | 필수 |

#### Object example

{% raw %}

```json
{
  "header": {
    "namespace": "Device",
    "name": "DeviceState"
  },
  "payload": {
    ...
    "power": {
        "actions": [
            "TurnOff",
            "TurnOn"
        ],
        "state": "active"
    },
    ...
  }
}
```

{% endraw %}

### ScreenBrightnessInfoObject {#ScreenBrightnessInfoObject}
클라이언트 기기의 화면 밝기 상태 정보를 보고할 때 사용하는 객체입니다.

#### Object fields

| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|---------|
| `actions[]`          | string array | 화면 밝기와 관련하여 수행할 수 있는 [`DeviceControl`](/CIC/References/CICInterface/DeviceControl.md) API 목록. 다음 동작 목록 중 클라이언트 기기가 실제로 수행할 수 있는 동작을 입력합니다. <ul><li>"Decrease"</li><li>"Increase"</li><li>"SetValue"</li></ul> | 필수 |
| `min`                | number       | 클라이언트 기기 화면에 설정할 수 있는 밝기의 최소치    | 필수 |
| `max`                | number       | 클라이언트 기기 화면에 설정할 수 있는 밝기의 최대치    | 필수 |
| `value`              | number       | 현재 클라이언트 기기의 화면 밝기                   | 필수 |

#### Object example

{% raw %}

```json
{
  "header": {
    "namespace": "Device",
    "name": "DeviceState"
  },
  "payload": {
    ...
    "screenBrightness": {
        "actions": [
            "Decrease",
            "Increase",
            "SetValue"
        ],
        "min": 0,
        "max": 100,
        "value": 70
    },
    ...
  }
}
```

{% endraw %}

### SoundModeInfoObject {#SoundModeInfoObject}
클라이언트 기기의 사운드 모드 정보를 보고할 때 사용하는 객체입니다.

#### Object fields

| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|---------|
| `actions[]`          | string array | 사운드 모드와 관련하여 수행할 수 있는 [`DeviceControl`](/CIC/References/CICInterface/DeviceControl.md) API 목록. 다음 동작 목록 중 클라이언트 기기가 실제로 수행할 수 있는 동작을 입력합니다. <ul><li>"TurnOff"</li><li>"TurnOn"</li></ul> | 필수 |
| `state`              | string       | 사운드 모드 설정 상태. <ul><li><code>"ring"</code>: 벨소리 모드</li><li><code>"silent"</code>: 무음 모드</li><li><code>"vibrate"</code>: 진동 모드</li></ul> | 필수 |

#### Object example

{% raw %}

```json
{
  "header": {
    "namespace": "Device",
    "name": "DeviceState"
  },
  "payload": {
    ...
    "soundMode": {
        "actions": [
            "TurnOff",
            "TurnOn"
        ],
        "state": "vibrate"
    },
    ...
  }
}
```

{% endraw %}

### VolumeInfoObject {#VolumeInfoObject}
클라이언트 기기의 스피커 볼륨 크기 정보를 보고할 때 사용하는 객체입니다.

#### Object fields

| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|---------|
| `actions[]`          | string array | 스피커 볼륨 크기와 관련하여 수행할 수 있는 [`DeviceControl`](/CIC/References/CICInterface/DeviceControl.md) API 목록. 다음 동작 목록 중 클라이언트 기기가 실제로 수행할 수 있는 동작을 입력합니다. <ul><li>"Decrease"</li><li>"Increase"</li><li>"SetValue"</li></ul> | 필수 |
| `min`                | number       | 클라이언트 기기 스피커에 설정할 수 있는 볼륨의 최소치    | 필수 |
| `max`                | number       | 클라이언트 기기 스피커에 설정할 수 있는 볼륨의 최대치    | 필수 |
| `warning`            | number       | 클라이언트 기기 스피커에 특정 수치 이상 설정할 경우 경고할 값. 이 필드의 값이 `8`이고, 사용자가 `8` 이상의 값을 볼륨으로 설정하게 되면 사용자에게 "볼륨 10은 무척 큰 소리에요. 변경을 원하시나요?"라고 되묻습니다. | 선택 |
| `value`              | number       | 클라이언트 기기의 현재 스피커 볼륨 크기               | 필수 |

#### Object example

{% raw %}

```json
{
  "header": {
    "namespace": "Device",
    "name": "DeviceState"
  },
  "payload": {
    ...
    "volume": {
        "actions": [
            "Decrease",
            "Increase",
            "SetValue"
        ],
        "min": 0,
        "max": 60,
        "warning": 50,
        "value": 40
    },
    ...
  }
}
```

{% endraw %}

### WifiInfoObject {#WifiInfoObject}
클라이언트 기기의 무선 네트워크(Wi-Fi) 기능 활성화 상태와 무선 네트워크 연결 정보를 보고할 때 사용하는 객체입니다.

#### Object fields

| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|---------|
| `actions[]`            | string array | 무선 네트워크과 관련하여 수행할 수 있는 [`DeviceControl`](/CIC/References/CICInterface/DeviceControl.md) API 목록. 다음 동작 목록 중 클라이언트 기기가 실제로 수행할 수 있는 동작을 입력합니다. <ul><li>"TurnOff"</li><li>"TurnOn"</li></ul>| 필수 |
| `networks[]`           | object array | 검색된 무선 네트워크 정보를 가지는 객체 배열 | 필수 |
| `networks[].name`      | string       | 무선 네트워크 이름(SSID)               | 필수 |
| `networks[].connected` | boolean      | 무선 네트워크 연결 여부. <ul><li><code>true</code>: 연결된 상태</li><li><code>false</code>: 연결되어 있지 않은 상태</li></ul> | 필수 |
| `state`                | string       | 무선 네트워크 기능 활성화 상태. <ul><li><code>"off"</code>: 꺼짐</li><li><code>"on"</code>: 켜짐</li></ul> | 필수 |

#### Object example

{% raw %}

```json
{
  "header": {
    "namespace": "Device",
    "name": "DeviceState"
  },
  "payload": {
    ...
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
    ...
  }
}
```

{% endraw %}

### See also
* [`DeviceControl` API](/CIC/References/CICInterface/DeviceControl.md)
* [`SpeechRecognizer.Recognize`](/CIC/References/CICInterface/SpeechRecognizer.md#Recognize)
