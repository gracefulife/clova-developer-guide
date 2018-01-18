## Device.DeviceState {#DeviceState}

`Device.DeviceState` is a format for reporting the state of the client device to CIC.

### Message structure

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

| Field        | Type    | Description                     | Required |
|---------------|:---------:|-----------------------------|:---------:|
| `airplane`        | [AirplaneInfoObject](#AirplaneInfoObject)               | The airplane mode settings of a client device      | Optional |
| `battery`         | [BatteryInfoObject](#BatteryInfoObject)                 | The battery information of a client device              | Optional |
| `bluetooth`       | [BluetoothInfoObject](#BluetoothInfoObject)             | The Bluetooth status and information of paired devices of a client device.      | Optional |
| `cellular`        | [CellularInfoObject](#CellularInfoObject)               | The cellular network settings of a client device | Optional |
| `channel`         | [ChannelInfoObject](#ChannelInfoObject)                 | The TV channel settings of a client device         | Optional |
| `energySavingMode` | [EnergySavingModeInfoObject](#EnergySavingModeInfoObject) | The energy saving mode of a client device     | Optional |
| `flashLight`      | [FlashLightInfoObject](#FlashLightInfoObject)           | The flash light settings of a client device       | Optional |
| `gps`             | [GPSInfoObject](#GPSInfoObject)                         | The GPS settings of a client device            | Optional |
| `localTime`       | string | The current local time set on a client device. Format: [ISO 8601](https://en.wikipedia.org/wiki/ISO_8601)             | Optional |
| `power`           | [PowerInfoObject](#PowerInfoObject)                 | The power status of a client device            | Optional |
| `screenBrightness` | [ScreenBrightnessInfoObject](#ScreenBrightnessInfoObject) | The screen brightness level of a client device            | Optional |
| `soundMode`       | [SoundModeInfoObject](#SoundModeInfoObject)             | The sound settings of a client device        | Optional |
| `volume`          | [VolumeInfoObject](#VolumeInfoObject)                   | The speaker volume level of a client device           | Optional |
| `wifi`            | [WifiInfoObject](#WifiInfoObject)                       | The WiFi settings and connection state of a client device.    | Optional |

### Example

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

Contains the airplane mode settings of a client device.

#### Object fields

| Field        | Type    | Description                     | Required |
|---------------|:---------:|-----------------------------|:---------:|
| `actions[]`     | string array | A list of the [`DeviceControl` APIs](/CIC/References/CICInterface/DeviceControl.md) the client can support for airplane mode, from the following: <ul><li>"TurnOff"</li><li>"TurnOn"</li></ul> | Required |
| `state`         | string | Indicates whether the airplane mode is on or off:<ul><li><code>"off"</code>: Airplane mode is off</li><li><code>"on"</code>: Airplane mode is on</li></ul> | Required |

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

Contains the battery state of a client device.

#### Object fields

| Field        | Type    | Description                     | Required |
|---------------|:---------:|-----------------------------|:---------:|
| `actions[]`     | string array | A list of the [`DeviceControl` APIs](/CIC/References/CICInterface/DeviceControl.md) the client can support for battery. Add an empty array as there are no APIs available. | Required |
| `value`         | number | The percentage of remaining battery. Range: [0–100] | Required |
| `charging`      | boolean | Indicates whether the client is charging or not:<ul><li><code>true</code>: The client is charging</li><li><code>false</code>: The client is not charging</li></ul> | Required |

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

Contains the Bluetooth information including Bluetooth status and paired devices.

#### Object fields

| Field        | Type    | Description                     | Required |
|---------------|:---------:|-----------------------------|:---------:|
| `actions[]`          | string array | A list of the [`DeviceControl` APIs](/CIC/References/CICInterface/DeviceControl.md) the client can support for Bluetooth, from the following: <ul><li>"TurnOff"</li><li>"TurnOn"</li><li>"BtConnect"</li><li>"BtDisconnect"</li><li>"BtStartPairing"</li><li>"BtStopPairing"</li></ul> | Required |
| `btlist[]`           | object array | Contains details of Bluetooth devices paired to the client.         | Required |
| `btlist[].name`      | string       | The name of This Bluetooth device.                      | Required |
| `btlist[].address`   | string       | The MAC address of this Bluetooth device.                  | Required |
| `btlist[].connected` | boolean      | Indicates whether this Bluetooth device is connected to the client device or not. <ul><li><code>true</code>: Connected</li><li><code>false</code>: Not connected</li></ul> | Required |
| `state`              | string       | Indicates whether Bluetooth is on or off: <ul><li><code>"off"</code>: Bluetooth is turned off</li><li><code>"on"</code>: Bluetooth is turned on</li></ul> | Required |

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

Contains the cellular network settings of a client device.

#### Object fields

| Field        | Type    | Description                     | Required |
|---------------|:---------:|-----------------------------|:---------:|
| `actions[]`          | string array | A list of the  [`DeviceControl` APIs](/CIC/References/CICInterface/DeviceControl.md) the client can support for cellular network settings, from the following: <ul><li>"TurnOff"</li><li>"TurnOn"</li></ul> | Required |
| `state`              | string       | Indicates whether cellular network is turned on or off: <ul><li><code>"off"</code>: Cellular network is turned off</li><li><code>"on"</code>: Cellular network is turned on</li></ul> | Required |

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

Contains the TV channel settings of a client device.

#### Object fields

| Field        | Type    | Description                     | Required |
|---------------|:---------:|-----------------------------|:---------:|
| `actions[]`     | string array | A list of the  [`DeviceControl` APIs](/CIC/References/CICInterface/DeviceControl.md) the client can support for TV channel settings, from the following: <ul><li>"Decrease"</li><li>"Increase"</li><li>"SetValue"</li></ul> | Required |

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

Contains the energy saving mode of a client device.

#### Object fields

| Field        | Type    | Description                     | Required |
|---------------|:---------:|-----------------------------|:---------:|
| `actions[]`          | string array | A list of the [`DeviceControl` APIs](/CIC/References/CICInterface/DeviceControl.md) the client can support for sleep mode, from the following: <ul><li>"TurnOff"</li><li>"TurnOn"</li></ul> | Required |
| `state`              | string       | Indicates whether the power saving mode is on or not: <ul><li><code>"off"</code>: Power saving mode is off</li><li><code>"on"</code>: Power saving mode is on</li></ul> | Required |

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

Contains the flash light settings of a client device.

#### Object fields

| Field        | Type    | Description                     | Required |
|---------------|:---------:|-----------------------------|:---------:|
| `actions[]`          | string array | A list of the  [`DeviceControl` APIs](/CIC/References/CICInterface/DeviceControl.md) the client can support for flashlight, from the following. <ul><li>"TurnOff"</li><li>"TurnOn"</li></ul> | Required |
| `state`              | string       | Indicates whether the flashlight on or off: <ul><li><code>"off"</code>: Flashlight is off</li><li><code>"on"</code>: Flashlight is on</li></ul> | Required |

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

Contains the GPS state of a client device.

#### Object fields

| Field        | Type    | Description                     | Required |
|---------------|:---------:|-----------------------------|:---------:|
| `actions[]`          | string array | A list of the [`DeviceControl` APIs](/CIC/References/CICInterface/DeviceControl.md) the client can support for GPS, from the following: <ul><li>"TurnOff"</li><li>"TurnOn"</li></ul> | Required |
| `state`              | string       | Indicates whether GPS is turned on or off: <ul><li><code>"off"</code>: GPS is turned off</li><li><code>"on"</code>: GPS is turned on</li></ul> | Required |

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

Contains the power state of a client device.

#### Object fields

| Field        | Type    | Description                     | Required |
|---------------|:---------:|-----------------------------|:---------:|
| `actions[]`          | string array | A list of the  [`DeviceControl` APIs](/CIC/References/CICInterface/DeviceControl.md) the client can support for power state, from the following: <ul><li>"TurnOff"</li><li>"TurnOn"</li></ul> | Required |
| `state`              | string       | Indicates whether the client device is turned on or off: <ul><li><code>"active"</code>: The client device is turned on</li><li><code>"idle"</code>: The client device is turned off</li></ul> | Required |

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

Contains the screen brightness level of a client device.

#### Object fields

| Field        | Type    | Description                     | Required |
|---------------|:---------:|-----------------------------|:---------:|
| `actions[]`          | string array | A list of the [`DeviceControl` APIs](/CIC/References/CICInterface/DeviceControl.md) the client can support for brightness, from the following: <ul><li>"Decrease"</li><li>"Increase"</li><li>"SetValue"</li></ul> | Required |
| `min`                | number       | The minimum screen brightness level available on the client device    | Required |
| `max`                | number       | The maximum screen brightness level available on the client device    | Required |
| `value`              | number       | The current screen brightness level of the client device.                    | Required |

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

Contains the sound mode of a client device.

#### Object fields

| Field        | Type    | Description                     | Required |
|---------------|:---------:|-----------------------------|:---------:|
| `actions[]`          | string array | A list of the [`DeviceControl` APIs](/CIC/References/CICInterface/DeviceControl.md) the client can support for sound mode, from the following: <ul><li>"TurnOff"</li><li>"TurnOn"</li></ul> | Required |
| `state`              | string       | Indicates the active sound mode on the client device: <ul><li><code>"ring"</code>: Ring mode</li><li><code>"silent"</code>: Silent mode</li><li><code>"vibrate"</code>: Vibration mode</li></ul> | Required |

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

Contains the speaker volume level of a client device.

#### Object fields

| Field        | Type    | Description                     | Required |
|---------------|:---------:|-----------------------------|:---------:|
| `actions[]`          | string array | A list of the [`DeviceControl` APIs](/CIC/References/CICInterface/DeviceControl.md) the client can speaker for speaker volume, from the following: <ul><li>"Decrease"</li><li>"Increase"</li><li>"SetValue"</li></ul> | Required |
| `min`                | number       | The minimum speaker volume level available on the client device.    | Required |
| `max`                | number       | The maximum speaker volume level available on the client device.    | Required |
| `warning`            | number       | The volume level at which to warn the user if the user sets the volume to this level or higher. For example, if this field is set to `8` and if the user sets the volume to `10`, Clova will send a message to the client to inform the user, "Volume 10 is very loud. Would you like to lower the volume?" | Optional |
| `value`              | number       | The current speaker volume level of the client device.               | Required |

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

Contains the Wifi state of a client device.

#### Object fields

| Field        | Type    | Description                     | Required |
|---------------|:---------:|-----------------------------|:---------:|
| `actions[]`            | string array | A list of the [`DeviceControl` APIs](/CIC/References/CICInterface/DeviceControl.md) the client can support for WiFi, from the following: <ul><li>"TurnOff"</li><li>"TurnOn"</li></ul>| Required |
| `networks[]`           | object array | Contains the details of WiFi networks detected. | Required |
| `networks[].name`      | string       | The name of the wireless network (SSID).                      | Required |
| `networks[].connected` | boolean      | Indicates whether the client is connected to this WiFi network or not: <ul><li><code>true</code>: Connected</li><li><code>false</code>: Not connected</li></ul> | Required |
| `state`                | string       | Indicates whether WiFi is turned on or not: <ul><li><code>"off"</code>: WiFi is turned on</li><li><code>"on"</code>: WiFi is turned off</li></ul> | Required |

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
