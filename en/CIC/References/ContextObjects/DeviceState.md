## Device.DeviceState {#DeviceState}
DeviceState is a message format that sends device states of a client.

### Message format
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
    "screenBrightness": {{ScreenBrightnessInfoObject}},
    "cellular": {{CellularInfoObject}},
    "flashLight" {{FlashLightInfoObject}},
    "gps": {{GPSInfoObject}},
    "localTime": {{string}},
    "powerSavingMode": {{PowerSavingModeInfoObject}},
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
| `airplane`        | [AirplaneInfoObject](#AirplaneInfoObject)               | An object containing an airplane mode setting of a client device      | No |
| `battery`         | [BatteryInfoObject](#BatteryInfoObject)                 | An object containing a battery state of a client device              | No |
| `bluetooth`       | [BluetoothInfoObject](#BluetoothInfoObject)             | An object containing a Bluetooth state of a client device, whether it is enabled and connected       | No |
| `screenBrightness` | [ScreenBrightnessInfoObject](#ScreenBrightnessInfoObject)           | An object containing screen brightness of a client device            | No |
| `cellular`        | [CellularInfoObject](#CellularInfoObject)               | An object containing a celluar activation state of a client device | No |
| `flashLight`      | [FlashLightInfoObject](#FlashLightInfoObject)           | An object containing a flashlight setting of a client device       | No |
| `gps`             | [GPSInfoObject](#GPSInfoObject)                         | An object containing a GPS setting of a client device            | No |
| `localTime`       | string | Current local time set in the client device ([ISO 8601](https://en.wikipedia.org/wiki/ISO_8601) format)              | No |
| `powerSavingMode` | [PowerSavingModeInfoObject](#powerSavingModeInfoObject) | An object containing a power saving mode setting of a client device        | No |
| `soundMode`       | [SoundModeInfoObject](#SoundModeInfoObject)             | An object containing a sound output setting of a client device        | No |
| `volume`          | [VolumeInfoObject](#VolumeInfoObject)                   | An object containing a speaker volume level of a client device           | No |
| `wifi`            | [WifiInfoObject](#WifiInfoObject)                       | An object containing a wireless network (Wi-Fi) state of a client device, whether it is enabled and connected    | No |

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
An object containing an airplane mode setting of a client device.

#### Object field

| Field name       | Type    | Field description                     | Required |
|---------------|---------|-----------------------------|---------|
| actions[]     | string array | A list of executable [`DeviceControl` APIs](/CIC/References/APIs/DeviceControl.md) for an airplane mode. Enter the following values if your client device can execute them.<ul><li>"TurnOff"</li><li>"TurnOn"</li></ul> | Yes |
| state         | string | The state of the airplane mode.<ul><li><code>"off"</code>: Turned off</li><li><code>"on"</code>: Turned on</li></ul> | Yes |

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
An object containing a battery state of a client device.

#### Object field

| Field name       | Type    | Field description                     | Required |
|---------------|---------|-----------------------------|---------|
| actions[]     | string array | A list of executable [`DeviceControl` APIs](/CIC/References/APIs/DeviceControl.md) for battery. No actions are currently supported. | Yes |
| value         | number | Remaining battery. Enter a number between 0 and 100. Unit is percentage (%). | Yes |
| charging      | boolean | Whether charging the battery or not.<ul><li><code>true</code>: Charging</li><li><code>false</code>: Not charing</li></ul> | Yes |

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
An object containing a Bluetooth state of a client device, whether it is enabled and connected.

#### Object field

| Field name       | Type    | Field description                     | Required |
|---------------|---------|-----------------------------|---------|
| actions[]          | string array | A list of executable [`DeviceControl` APIs](/CIC/References/APIs/DeviceControl.md) for Bluetooth connection. Enter the following values if your client device can execute them. <ul><li>"TurnOff"</li><li>"TurnOn"</li><li>"BtConnect"</li><li>"BtDisconnect"</li><li>"BtStartPairing"</li><li>"BtStopPairing"</li></ul> | Yes |
| btlist[]           | object array | An object containing details of a paired Bluetooth device         | Yes |
| btlist[].name      | string       | The name of the Bluetooth device                      | Yes |
| btlist[].address   | string       | The MAC address of the Bluetooth device                  | Yes |
| btlist[].connected | boolean      | Whether the Bluetooth device is connected or not. <ul><li><code>true</code>: Connected</li><li><code>false</code>: Not connected</li></ul> | Yes |
| state              | string       | Whether Bluetooth is enabled or not. <ul><li><code>"off"</code>: Disabled</li><li><code>"on"</code>: Enabled</li></ul> | Yes |

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

### ScreenBrightnessInfoObject {#ScreenBrightnessInfoObject}
An object containing screen brightness of a client device.

#### Object field

| Field name       | Type    | Field description                     | Required |
|---------------|---------|-----------------------------|---------|
| actions[]          | string array | A list of executable [`DeviceControl` APIs](/CIC/References/APIs/DeviceControl.md) for screen brightness. Enter the following values if your client device can execute them. <ul><li>"Decrease"</li><li>"Increase"</li><li>"SetPoint"</li></ul> | Yes |
| min                | number       | Minimum screen brightness of the client device    | Yes |
| max                | number       | Maximum screen brightness of the client device    | Yes |
| value              | number       | Current screen brightness of the client device                   | Yes |

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
            "Increse",
            "SetPoint"
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

### CellularInfoObject {#CellularInfoObject}
An object containing a cellular state of a client device, whether mobile communication is enabled or not.

#### Object field

| Field name       | Type    | Field description                     | Required |
|---------------|---------|-----------------------------|---------|
| actions[]          | string array | A list of executable [`DeviceControl` APIs](/CIC/References/APIs/DeviceControl.md) for mobile data communication. Enter the following values if your client device can execute them. <ul><li>"TurnOff"</li><li>"TurnOn"</li></ul> | Yes |
| state              | string       | Whether mobile data communication is enabled or not. <ul><li><code>"off"</code>: Disabled</li><li><code>"on"</code>: Enabled</li></ul> | Yes |

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

### FlashLightInfoObject {#FlashLightInfoObject}
An object containing a flashlight setting of a client device.

#### Object field

| Field name       | Type    | Field description                     | Required |
|---------------|---------|-----------------------------|---------|
| actions[]          | string array | A list of executable [`DeviceControl` APIs](/CIC/References/APIs/DeviceControl.md) for flashlight. Enter the following values if your client device can execute them. <ul><li>"TurnOff"</li><li>"TurnOn"</li></ul> | Yes |
| state              | string       | The current state of the flashlight. <ul><li><code>"off"</code>: Turned off</li><li><code>"on"</code>: Turned on</li></ul> | Yes |

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
An object containing a GPS state of a client device.

#### Object field

| Field name       | Type    | Field description                     | Required |
|---------------|---------|-----------------------------|---------|
| actions[]          | string array | A list of executable [`DeviceControl` APIs](/CIC/References/APIs/DeviceControl.md) for GPS. Enter the following values if your client device can execute them. <ul><li>"TurnOff"</li><li>"TurnOn"</li></ul> | Yes |
| state              | string       | The current GPS state. <ul><li><code>"off"</code>: Turned off</li><li><code>"on"</code>: Turned on</li></ul> | Yes |

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

### PowerSavingModeInfoObject {#PowerSavingModeInfoObject}
An object containing a power saving mode of a client device.

#### Object field

| Field name       | Type    | Field description                     | Required |
|---------------|---------|-----------------------------|---------|
| actions[]          | string array | A list of executable [`DeviceControl` APIs](/CIC/References/APIs/DeviceControl.md) for a power saving mode. Enter the following values if your client device can execute them. <ul><li>"TurnOff"</li><li>"TurnOn"</li></ul> | Yes |
| state              | string       | The state of the power saving mode. <ul><li><code>"off"</code>: Turned off</li><li><code>"on"</code>: Turned on</li></ul> | Yes |

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
    "powerSavingMode": {
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

### SoundModeInfoObject {#SoundModeInfoObject}
An object containing a sound mode of a client device.

#### Object field

| Field name       | Type    | Field description                     | Required |
|---------------|---------|-----------------------------|---------|
| actions[]          | string array | A list of executable [`DeviceControl` APIs](/CIC/References/APIs/DeviceControl.md) for a sound mode. Enter the following values if your client device can execute them. <ul><li>"TurnOff"</li><li>"TurnOn"</li></ul> | Yes |
| state              | string       | The state of the sound mode setting. <ul><li><code>"ring"</code>: Ring mode</li><li><code>"silent"</code>: Silent mode</li><li><code>"vibrate"</code>: Vibration mode</li></ul> | Yes |

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
An object containing a speaker volume level of a client device.

#### Object field

| Field name       | Type    | Field description                     | Required |
|---------------|---------|-----------------------------|---------|
| actions[]          | string array | A list of executable [`DeviceControl` APIs](/CIC/References/APIs/DeviceControl.md) for a speaker volume level. Enter the following values if your client device can execute them. <ul><li>"Decrease"</li><li>"Increase"</li><li>"SetPoint"</li></ul> | Yes |
| min                | number       | Minimum speaker volume of the client device    | Yes |
| max                | number       | Maximum speaker volume of the client device    | Yes |
| value              | number       | Current speaker volume of the client device               | Yes |

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
            "Increse",
            "SetPoint"
        ],
        "min": 0,
        "max": 60,
        "value": 40
    },
    ...
  }
}
```
{% endraw %}

### WifiInfoObject {#WifiInfoObject}
An object containing a wireless network (Wi-Fi) state of a client device, whether the wireless network is enabled and connected.

#### Object field

| Field name       | Type    | Field description                     | Required |
|---------------|---------|-----------------------------|---------|
| actions[]            | string array | A list of executable [`DeviceControl` APIs](/CIC/References/APIs/DeviceControl.md) for a wireless network. Enter the following values if your client device can execute them. <ul><li>"TurnOff"</li><li>"TurnOn"</li></ul>| Yes |
| networks[]           | object array | An object array containing details of wireless network found | Yes |
| networks[].name      | string       | The name of the wireless network                     | Yes |
| networks[].connected | boolean      | Whether the wireless network is connected or not. <ul><li><code>true</code>: Connected</li><li><code>false</code>: Not connected</li></ul> | Yes |
| state                | string       | Whether the wireless network is enabled or not. <ul><li><code>"off"</code>: Enabled</li><li><code>"on"</code>: Disabled</li></ul> | Yes |

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
* [`DeviceControl` API](/CIC/References/APIs/DeviceControl.md)
* [`SpeechRecognizer.Recognize`](/CIC/References/APIs/SpeechRecognizer.md#recognize-event)
