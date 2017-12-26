## Device.DeviceState {#DeviceState}
`Device.DeviceState` is a message format applied to report the state of the device of the client to CIC.

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

### Payload field

| Field name       | Type    | Field description                     | Required |
|---------------|---------|-----------------------------|---------|
| `airplane`        | [AirplaneInfoObject](#AirplaneInfoObject)               | An object used to report an airplane mode setting of a client device      | No |
| `battery`         | [BatteryInfoObject](#BatteryInfoObject)                 | An object used to report battery information of a client device              | No |
| `bluetooth`       | [BluetoothInfoObject](#BluetoothInfoObject)             | An object used to report the activation status and device connection details of a Bluetooth of the client device.       | No |
| `cellular`        | [CellularInfoObject](#CellularInfoObject)               | An object used to report a cellular state of a client device | No |
| `channel`         | [ChannelInfoObject](#ChannelInfoObject)                 | An object used to report a TV channel setting of a client device         | No |
| `energySavingMode` | [EnergySavingModeInfoObject](#EnergySavingModeInfoObject) | An object used to report an energy saving mode of a client device     | No |
| `flashLight`      | [FlashLightInfoObject](#FlashLightInfoObject)           | An object used to report a flash light setting of a client device       | No |
| `gps`             | [GPSInfoObject](#GPSInfoObject)                         | An object used to report a GPS setting of a client device            | No |
| `localTime`       | string | Current local time set in the client device ([ISO 8601](https://en.wikipedia.org/wiki/ISO_8601) format)              | No |
| `power`           | [PowerInfoObject](#PowerInfoObject)                 | An object used to report power status of a client device            | No |
| `screenBrightness` | [ScreenBrightnessInfoObject](#ScreenBrightnessInfoObject) | An object used to report screen brightness of a client device            | No |
| `soundMode`       | [SoundModeInfoObject](#SoundModeInfoObject)             | An object used to report a sound output setting of a client device        | No |
| `volume`          | [VolumeInfoObject](#VolumeInfoObject)                   | An object used to report speaker volume details of a client device           | No |
| `wifi`            | [WifiInfoObject](#WifiInfoObject)                       | An object used to report the activation and connection status of wireless network (Wi-Fi) of the client device.    | No |

### Message example
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
An object used to report an airplane mode setting of a client device.

#### Object field

| Field name       | Type    | Field description                     | Required |
|---------------|---------|-----------------------------|---------|
| `actions[]`     | string array | A list of executable [`DeviceControl` APIs](/CIC/References/CICInterface/DeviceControl.md) for airplane mode. Enter the following values if your client's device can execute them.<ul><li>"TurnOff"</li><li>"TurnOn"</li></ul> | Yes |
| `state`         | string | The state of the airplane mode.<ul><li><code>"off"</code>: Turned off</li><li><code>"on"</code>: Turned on</li></ul> | Yes |

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
An object used to report a battery state of a client device.

#### Object field

| Field name       | Type    | Field description                     | Required |
|---------------|---------|-----------------------------|---------|
| `actions[]`     | string array | A list of executable [`DeviceControl` APIs](/CIC/References/CICInterface/DeviceControl.md) for battery. No actions are currently supported. | Yes |
| `value`         | number | Remaining battery. Enter a number between 0 and 100. Unit is percentage (%). | Yes |
| `charging`      | boolean | Whether charging the battery or not<ul><li><code>true</code>: Charging</li><li><code>false</code>: Not charging</li></ul> | Yes |

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
An object used to report the activation status and device connection details of a Bluetooth of the client device.

#### Object field

| Field name       | Type    | Field description                     | Required |
|---------------|---------|-----------------------------|---------|
| `actions[]`          | string array | A list of executable [`DeviceControl` APIs](/CIC/References/CICInterface/DeviceControl.md) for Bluetooth connection. Enter the following values if your client's device can execute them. <ul><li>"TurnOff"</li><li>"TurnOn"</li><li>"BtConnect"</li><li>"BtDisconnect"</li><li>"BtStartPairing"</li><li>"BtStopPairing"</li></ul> | Yes |
| `btlist[]`           | object array | An object containing details of a paired Bluetooth device         | Yes |
| `btlist[].name`      | string       | The name of the Bluetooth device                      | Yes |
| `btlist[].address`   | string       | The MAC address of the Bluetooth device                  | Yes |
| `btlist[].connected` | boolean      | Whether the Bluetooth device is connected or not <ul><li><code>true</code>: Connected</li><li><code>false</code>: Not connected</li></ul> | Yes |
| `state`              | string       | Whether Bluetooth is turned on or not. <ul><li><code>"off"</code>: Turned off</li><li><code>"on"</code>: Turned on</li></ul> | Yes |

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
An object used to report the activation status of a cellular state of the client device.

#### Object field

| Field name       | Type    | Field description                     | Required |
|---------------|---------|-----------------------------|---------|
| `actions[]`          | string array | A list of executable [`DeviceControl` APIs](/CIC/References/CICInterface/DeviceControl.md) for mobile data communication. Enter the following values if your client's device can execute them. <ul><li>"TurnOff"</li><li>"TurnOn"</li></ul> | Yes |
| `state`              | string       | Whether mobile data communication is turned on or not <ul><li><code>"off"</code>: Turned off</li><li><code>"on"</code>: Turned on</li></ul> | Yes |

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
An object used to report a TV channel setting of a client device

#### Object field

| Field name       | Type    | Field description                     | Required |
|---------------|---------|-----------------------------|---------|
| `actions[]`     | string array | A list of executable [`DeviceControl` APIs](/CIC/References/CICInterface/DeviceControl.md) for TV channel settings. Enter the following values if your client's device can execute them.<ul><li>"Decrease"</li><li>"Increase"</li><li>"SetValue"</li></ul> | Yes |

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
An object used to report an energy saving mode of a client device.

#### Object field

| Field name       | Type    | Field description                     | Required |
|---------------|---------|-----------------------------|---------|
| `actions[]`          | string array | A list of executable [`DeviceControl` APIs](/CIC/References/CICInterface/DeviceControl.md) for sleep mode. Enter the following values if your client's device can execute them. <ul><li>"TurnOff"</li><li>"TurnOn"</li></ul> | Yes |
| `state`              | string       | The state of the power saving mode. <ul><li><code>"off"</code>: Turned off</li><li><code>"on"</code>: Turned on</li></ul> | Yes |

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
An object used to report a flash light setting of a client device

#### Object field

| Field name       | Type    | Field description                     | Required |
|---------------|---------|-----------------------------|---------|
| `actions[]`          | string array | A list of executable [`DeviceControl` APIs](/CIC/References/CICInterface/DeviceControl.md) for flashlight. Enter the following values if your client's device can execute them. <ul><li>"TurnOff"</li><li>"TurnOn"</li></ul> | Yes |
| `state`              | string       | The current state of the flashlight. <ul><li><code>"off"</code>: Turned off</li><li><code>"on"</code>: Turned on</li></ul> | Yes |

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
An object used to report GPS state of a client device.

#### Object field

| Field name       | Type    | Field description                     | Required |
|---------------|---------|-----------------------------|---------|
| `actions[]`          | string array | A list of executable [`DeviceControl` APIs](/CIC/References/CICInterface/DeviceControl.md) for GPS. Enter the following values if your client's device can execute them. <ul><li>"TurnOff"</li><li>"TurnOn"</li></ul> | Yes |
| `state`              | string       | The current GPS state. <ul><li><code>"off"</code>: Turned off</li><li><code>"on"</code>: Turned on</li></ul> | Yes |

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
An object used to report power state of a client device.

#### Object field

| Field name       | Type    | Field description                     | Required |
|---------------|---------|-----------------------------|---------|
| `actions[]`          | string array | A list of executable [`DeviceControl` APIs](/CIC/References/CICInterface/DeviceControl.md) for power state. Enter the following values if your client's device can execute them. <ul><li>"TurnOff"</li><li>"TurnOn"</li></ul> | Yes |
| `state`              | string       | The power state. <ul><li><code>"active"</code>: The client device is turned on</li><li><code>"idle"</code>: The client device is turned off</li></ul> | Yes |

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
An object used to report screen brightness state of a client device.

#### Object field

| Field name       | Type    | Field description                     | Required |
|---------------|---------|-----------------------------|---------|
| `actions[]`          | string array | A list of executable [`DeviceControl` APIs](/CIC/References/CICInterface/DeviceControl.md) for screen brightness. Enter the following values if your client's device can execute them. <ul><li>"Decrease"</li><li>"Increase"</li><li>"SetValue"</li></ul> | Yes |
| `min`                | number       | The minimum screen brightness of the client device    | Yes |
| `max`                | number       | The maximum screen brightness of the client device    | Yes |
| `value`              | number       | The current screen brightness of the client device                   | Yes |

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
An object used to report a sound mode of a client device.

#### Object field

| Field name       | Type    | Field description                     | Required |
|---------------|---------|-----------------------------|---------|
| `actions[]`          | string array | A list of executable [`DeviceControl` APIs](/CIC/References/CICInterface/DeviceControl.md) for sound mode. Enter the following values if your client's device can execute them. <ul><li>"TurnOff"</li><li>"TurnOn"</li></ul> | Yes |
| `state`              | string       | The state of the sound mode setting. <ul><li><code>"ring"</code>: Ring mode</li><li><code>"silent"</code>: Silent mode</li><li><code>"vibrate"</code>: Vibration mode</li></ul> | Yes |

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
An object used to report a speaker volume level of a client device.

#### Object field

| Field name       | Type    | Field description                     | Required |
|---------------|---------|-----------------------------|---------|
| `actions[]`          | string array | A list of executable [`DeviceControl` APIs](/CIC/References/CICInterface/DeviceControl.md) for speaker volume size. Enter the following values if your client's device can execute them. <ul><li>"Decrease"</li><li>"Increase"</li><li>"SetValue"</li></ul> | Yes |
| `min`                | number       | The minimum speaker volume of the client device    | Yes |
| `max`                | number       | The maximum speaker volume of the client device    | Yes |
| `warning`            | number       | The warning value which appears when the speaker setting of the client device exceeds a certain level. The value of the field is `8` and if the user sets the volume higher than `8`, it give warning message saying, "Volume 10 is very loud. Would you like to lower the volume?" | No |
| `value`              | number       | The current speaker volume of the client device               | Yes |

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
An object used to report the activation and connection status of wireless network (Wi-Fi) of the client device.

#### Object field

| Field name       | Type    | Field description                     | Required |
|---------------|---------|-----------------------------|---------|
| `actions[]`            | string array | A list of executable [`DeviceControl` APIs](/CIC/References/CICInterface/DeviceControl.md) for wireless network. Enter the following values if your client's device can execute them. <ul><li>"TurnOff"</li><li>"TurnOn"</li></ul>| Yes |
| `networks[]`           | object array | An object array containing details of wireless network found | Yes |
| `networks[].name`      | string       | The name of the wireless network (SSID)                      | Yes |
| `networks[].connected` | boolean      | Whether the wireless network is connected or not. <ul><li><code>true</code>: Connected</li><li><code>false</code>: Not connected</li></ul> | Yes |
| `state`                | string       | Whether the wireless network is turned on or not. <ul><li><code>"off"</code>: Turned off</li><li><code>"on"</code>: Turned on</li></ul> | Yes |

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
