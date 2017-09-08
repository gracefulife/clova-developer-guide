# DeviceControl

Controls client devices or reports to CIC on results of executing client device control.

Some user requests may involve controlling of a client device. If a user request is related to controlling of a client device, you will receive a directive message of `DeviceControl` namespace. Implement your client to control a device based on a received directive message. After executing device control, send the result to CIC using event messages.

DeviceControl provides the following event and directive messages.

| Message name         | Message type  | Message description                                   |
|------------------|-----------|---------------------------------------------|
| [`ActionExecuted`](#ActionExecuted)       | Event     | Send this event message to CIC after your client executes device control.           |
| [`ActionFailed`](#ActionFailed)           | Event     | Send this event message to CIC if your client cannot or fails to execute device control. |
| [`BtConnect`](#BtConnect)                 | Directive | Instructs your client to connect a specified Bluetooth device.                               |
| [`BtDisconnect`](#BtDisconnect)           | Directive | Instructs your client to disconnect a specified Bluetooth device.                               |
| [`BtStartPairing`](#BtStartPairing)       | Directive | Instructs your client to start a Bluetooth pairing mode.                                   |
| [`BtStopPairing`](#BtStopPairing)         | Directive | Instructs your client to stop a Bluetooth pairing mode.                                   |
| [`Decrease`](#Decrease)                   | Directive | Instructs your client to turn down speaker volume or decrease screen brightness by a default unit.                     |
| [`Increase`](#Increase)                   | Directive | Instructs your client to turn up speaker volume or increase screen brightness by a default unit.                     |
| [`LaunchApp`](#LaunchApp)                 | Directive | Instructs your client to launch a specified app.                                             |
| [`OpenScreen`](#OpenScreen)               | Directive | Instructs your client to open a setting screen.                                              |
| [`SetValue`](#SetValue)                   | Directive | Instructs your client to set speaker volume or screen brightness to a specified value.                    |
| [`TurnOff`](#TurnOff)                     | Directive | Instructs your client to turn off or disable a specified feature or mode.                           |
| [`TurnOn`](#TurnOn)                       | Directive | Instructs your client to turn on or enable a specified feature or mode.                                   |
| [`UpdateDeviceState`](#UpdateDeviceState) | Directive | Instructs your client to update states of other client devices registered to a user account.         |

<div class="note">
  <p><strong>Note!</strong></p>
  <p>The DeviceControl API is scheduled to be implemented soon. Its specification is described to define an interface and is subject to change.</p>
</div>

## ActionExecuted event {#ActionExecuted}

Send this event message to CIC after your client executes device control.

### Payload field

| Field name       | Type    | Field description                     | Required |
|---------------|---------|-----------------------------|---------|
| `target`      | string  | Target to control.<ul><li><code>"airplane"</code>: Airplane mode</li><li><code>"bluetooth"</code>: Bluetooth</li><li><code>"screenbrightness"</code>: Screen brightness</li><li><code>"cellular"</code>: Mobile communication</li><li><code>"flashlight"</code>: Flashlight</li><li><code>"gps"</code>: GPS</li><li><code>"powersave"</code>: Power saving mode</li><li><code>"soundmode"</code>: Sound mode</li><li><code>"volume"</code>: Speaker volume</li><li><code>"wifi"</code>: Wireless LAN</li></ul> | Yes     |
| `command`     | string  | Actions executed.  <ul><li>BtConnect</li><li>BtDisconnect</li><li>BtStartPairing</li><li>BtStopPairing</li><li>Decrease</li><li>Increase</li><li>OpenScreen</li><li>SetValue</li><li>TurnOn</li><li>TurnOff</li></ul> | Yes   |

### Remarks

When CIC receives this event message, it sends a [`UpdateDeviceState`](#UpdateDeviceState) directive message to all clients registered to a user account to notify the state change of the client device.

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

Send this event message to CIC if your client cannot or fails to execute device control.

### Payload field

| Field name       | Type    | Field description                     | Required |
|---------------|---------|-----------------------------|---------|
| `target`      | string  | Target to control.<ul><li><code>"airplane"</code>: Airplane mode</li><li><code>"app"</code>: App</li><li><code>"bluetooth"</code>: Bluetooth</li><li><code>"screenbrightness"</code>: Screen brightness</li><li><code>"cellular"</code>: Mobile communication</li><li><code>"flashlight"</code>: Flashlight</li><li><code>"gps"</code>: GPS</li><li><code>"powersave"</code>: Power saving mode</li><li><code>"soundmode"</code>: Sound mode</li><li><code>"volume"</code>: Speaker volume</li><li><code>"wifi"</code>: Wireless LAN</li></ul> | Yes     |
| `command`     | string  | Actions failed. <ul><li>BtConnect</li><li>BtDisconnect</li><li>BtStartPairing</li><li>BtStopPairing</li><li>Decrease</li><li>Increase</li><li>LaunchApp</li><li>OpenScreen</li><li>SetValue</li><li>TurnOn</li><li>TurnOff</li></ul> | Yes   |

### Remarks

* When CIC receives this event message, it sends an [`UpdateDeviceState`](#UpdateDeviceState) directive message to all clients registered to a user account to notify the state change of the client device.
* If you fail to launch an app after receiving a [`LaunchApp`](#LaunchApp) directive message, set the `target` field to `"app"`.

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
* [`LaunchApp`](#LaunchApp)
* [`OpenScreen`](#OpenScreen)
* [`SetValue`](#SetValue)
* [`TurnOff`](#TurnOff)
* [`TurnOn`](#TurnOn)

## BtConnect directive {#BtConnect}

Instructs your client to connect one of the paired Bluetooth devices. If it is paired with more than one device, the client must have defined criteria to decide which device it will connect to. For example, it can attempt to connect in the order of latest to oldest devices it connected to.

### Payload field

None

### Remarks

* Only speaker type Bluetooth devices are supported.
* Your client must send states of Bluetooth devices to CIC frequently, using a [`Device.DeviceState`](/CIC/References/Context_Objects.md#DeviceState) object.
* After your client processes this directive message, it must send the result to CIC, using [`ActionExecuted`](#ActionExecuted) or [`ActionFailed`](#ActionFailed) event message.

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

Instructs your client to disconnect a Bluetooth device.

### Payload field

None

### Remarks

* Only speaker type Bluetooth devices are supported.
* Your client must send states of Bluetooth devices to CIC frequently, using a [`Device.DeviceState`](/CIC/References/Context_Objects.md#DeviceState) object.
* After your client processes this directive message, it must send the result to CIC, using [`ActionExecuted`](#ActionExecuted) or [`ActionFailed`](#ActionFailed) event message.

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

Instructs your client to start a Bluetooth pairing mode.

### Payload field

None

### Remarks

* Only speaker type Bluetooth devices are supported.
* Your client must send states of Bluetooth devices to CIC frequently, using a [`Device.DeviceState`](/CIC/References/Context_Objects.md#DeviceState) object.
* After your client processes this directive message, it must send the result to CIC, using [`ActionExecuted`](#ActionExecuted) or [`ActionFailed`](#ActionFailed) event message.

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

Instructs your client to stop a Bluetooth pairing mode.

### Payload field

None

### Remarks

* Only speaker type Bluetooth devices are supported.
* Your client must send states of Bluetooth devices to CIC frequently, using a [`Device.DeviceState`](/CIC/References/Context_Objects.md#DeviceState) object.
* After your client processes this directive message, it must send the result to CIC, using [`ActionExecuted`](#ActionExecuted) or [`ActionFailed`](#ActionFailed) event message.

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

Instructs your client to turn down speaker volume or decrease screen brightness by a default unit, or change a TV channel to a previous channel.

### Payload field

| Field name       | Type    | Field description                     | Required |
|---------------|---------|-----------------------------|---------|
| `target`      | string  | Target to control.<ul><li><code>"channel"</code>: TV channel</li><li><code>"screenbrightness"</code>: Screen brightness</li><li><code>"volume"</code>: Speaker volume</li></ul> | Yes     |

### Remarks

* A default unit can be determined by a client side.
* Your client must send speaker volume and screen brightness to CIC frequently, using a [`Device.DeviceState`](/CIC/References/Context_Objects.md#DeviceState) context object.
* After your client processes this directive message, it must send the result to CIC, using [`ActionExecuted`](#ActionExecuted) or [`ActionFailed`](#ActionFailed) event message.

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

Instructs your client to turn up speaker volume or increase screen brightness by a default unit, or change a TV channel to a next channel.

### Payload field

| Field name       | Type    | Field description                     | Required |
|---------------|---------|-----------------------------|---------|
| `target`      | string  | Target to control.<ul><li><code>"channel"</code>: TV channel</li><li><code>"screenbrightness"</code>: Screen brightness</li><li><code>"volume"</code>: Speaker volume</li></ul> | Yes     |

### Remarks

* A default unit can be determined by a client side.
* Your client must send speaker volume and screen brightness to CIC frequently, using a [`Device.DeviceState`](/CIC/References/Context_Objects.md#DeviceState) context object.
* After your client processes this directive message, it must send the result to CIC, using [`ActionExecuted`](#ActionExecuted) or [`ActionFailed`](#ActionFailed) event message.

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

## LaunchApp directive {#LaunchApp}

Instructs your client to launch a specified app. To specify an app, it returns a custom URL scheme of the app, a relay page URL or the name of the app.

### Payload field

| Field name       | Type    | Field description                     | Required |
|---------------|---------|-----------------------------|---------|
| `target`      | string  | Information of the target app. It can have app information as follows.<ul><li>Custom URL scheme: A custom URL scheme of the target app (for example, <code>"naversearchapp://..."</code>)</li><li>Relay page URL: A relay page URL that launches the app if the app is already installed (for example, <code>"http://naverapp.naver.com/..."</code>)</li><li>App name: The name of the app recognized from user speech (for example, <code>"NAVER App"</code>)</li></ul> | Yes     |

### Remarks

* If your client cannot or fails to launch a specified app, send the result to CIC using an [`ActionFailed`](#ActionFailed) event message.

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
* [`ActionFailed`](#ActionFailed)

## OpenScreen directive {#OpenScreen}

Instructs your client to open a setting screen.

### Payload field

| Field name       | Type    | Field description                     | Required |
|---------------|---------|-----------------------------|---------|
| `target`      | string  | A screen to display. Currently only `"settings"` is entered, which is a value that opens a setting screen. | Yes     |

### Remarks

After your client processes this directive message, it must send the result to CIC, using [`ActionExecuted`](#ActionExecuted) or [`ActionFailed`](#ActionFailed) event message.

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

Instructs your client to set speaker volume or screen brightness to a specified value, or change to a specified TV channel.

### Payload field

| Field name       | Type    | Field description                     | Required |
|---------------|---------|-----------------------------|---------|
| `target`      | string  | Target to control.<ul><li><code>"channel"</code>: TV channel</li><li><code>"screenbrightness"</code>: Screen brightness</li><li><code>"volume"</code>: Speaker volume</li></ul> | Yes     |
| `value`       | string  | The value or TV channel number to change to       | Yes     |

### Remarks

* Your client must send speaker volume and screen brightness to CIC frequently, using a [`Device.DeviceState`](/CIC/References/Context_Objects.md#DeviceState) context object.
* After your client processes this directive message, it must send the result to CIC, using [`ActionExecuted`](#ActionExecuted) or [`ActionFailed`](#ActionFailed) event message.

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

Instructs your client to turn off or disable a specified feature or mode. For example, this directive message can instruct to turn off Bluetooth on a client device.

### Payload field

| Field name       | Type    | Field description                     | Required |
|---------------|---------|-----------------------------|---------|
| `target`      | string  | Target to control.<ul><li><code>"airplane"</code>: Airplane mode</li><li><code>"bluetooth"</code>: Bluetooth</li><li><code>"cellular"</code>: Mobile communication</li><li><code>"energysave"</code>: Energy saving mode</li><li><code>"flashlight"</code>: Flashlight</li><li><code>"gps"</code>: GPS</li><li><code>"power"</code>: Power state</li><li><code>"ring"</code>: Ring mode</li><li><code>"silent"</code>: Silent mode</li><li><code>"vibrate"</code>: Vibration mode</li><li><code>"wifi"</code>: Wireless LAN</li></ul> | Yes     |

### Remarks

* When turning off or disabling a certain control target, you must follow policies of the client device and execute device control appropriately to various situations. For example, to disable a ring mode, you may have to implement to enter a vibration mode or mute mode depending on the client device.
* Your client must send states of features or modes to CIC frequently, using a [`Device.DeviceState`](/CIC/References/Context_Objects.md#DeviceState) context object.
* After your client processes this directive message, it must send the result to CIC, using [`ActionExecuted`](#ActionExecuted) or [`ActionFailed`](#ActionFailed) event message.

<div class="danger">
  <p><strong>Caution!</strong></p>
  <p>A client device must be turned off when its <code>target</code> field is set to <code>"power"</code>.</p>
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

Instructs your client to turn on or enable a specified feature or mode. For example, this directive message can instruct to turn on Bluetooth on a client device.

### Payload field

| Field name       | Type    | Field description                     | Required |
|---------------|---------|-----------------------------|---------|
| `target`      | string  | Target to control.<ul><li><code>"airplane"</code>: Airplane mode</li><li><code>"bluetooth"</code>: Bluetooth</li><li><code>"cellular"</code>: Mobile communication</li><li><code>"energysave"</code>: Energy saving mode</li><li><code>"flashlight"</code>: Flashlight</li><li><code>"gps"</code>: GPS</li><li><code>"power"</code>: Power state</li><li><code>"ring"</code>: Ring mode</li><li><code>"silent"</code>: Silent mode</li><li><code>"vibrate"</code>: Vibration mode</li><li><code>"wifi"</code>: Wireless LAN</li></ul> | Yes     |

### Remarks

* Your client must send states of features or modes to CIC frequently, using a [`Device.DeviceState`](/CIC/References/Context_Objects.md#DeviceState) context object.
* After your client processes this directive message, it must send the result to CIC, using [`ActionExecuted`](#ActionExecuted) or [`ActionFailed`](#ActionFailed) event message.

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

Instructs your client to update states of other client devices registered to a user account. Users can use several clients simultaneously with one user account. A client can be an app or a device, such as Wave, speaker for Clova. An app-type client can control other speaker-type clients. It receives results of executing client control through `UpdateDeviceState` directive messages and update client states accordingly.

### Payload field

| Field name       | Type    | Field description                     | Required |
|---------------|---------|-----------------------------|---------|
| `deviceId`    | string  | The ID of the client device with an updated state. | Yes     |
| `deviceState` | [Device.DeviceState](/CIC/References/Context_Objects.md#DeviceState) object | An object containing an updated state of the device.         | Yes     |

### Remarks
* When CIC receives an [`ActionExecuted`](#ActionExecuted) or [`ActionFailed`](#ActionFailed) event message, it sends an `UpdateDeviceState` directive message to all clients registered to a user account to notify the state change of the client device.
* `UpdateDeviceState` directive messages are broadcast through a downchannel on all clients registered to a user account. They do not have a dialog ID (`dialogRequestId`).

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
