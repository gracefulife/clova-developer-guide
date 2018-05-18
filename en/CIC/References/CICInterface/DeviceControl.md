# DeviceControl

The DeviceControl namespace provides interfaces for controlling client devices or reporting to CIC the result of changing client device settings.

Users may request to manipulate their client devices. If the user request is for controlling the client device, the client will receive a directive of this namespace, `DeviceControl`. The client has to perform the task instructed by the directive and then send the result to CIC. For more information, see the [Client device control workflow](#DeviceContorlWorkFlow).

The client device can be connected to a third party Bluetooth speaker using the `DeviceControl` message. CIC controls the connection to a third party Bluetooth device by sending a directive for Bluetooth pairing and connection to the client. Then the client will frequently report the information related to the paired Bluetooth speaker using the [`BluetoothInfoObject`](/CIC/References/Context_Objects.md#BluetoothInfoObject) of the [`Device.DeviceState`](/CIC/References/Context_Objects.md#DeviceState) context. For more information on creating a connection, refer to each directive and event.

The DeviceControl namespace provides the following events and directives.

| Message name         | Type  | Description                                   |
|------------------|-----------|---------------------------------------------|
| [`ActionExecuted`](#ActionExecuted)       | Event     | Reports to CIC that the client has taken an action on the specified feature or mode.           |
| [`ActionFailed`](#ActionFailed)           | Event     | Reports to CIC that the client cannot or has failed to take an action on the specified feature or mode. |
| [`BtConnect`](#BtConnect)                 | Directive | Instructs the client to connect to a Bluetooth speaker.                               |
| [`BtConnectByPINCode`](#BtConnectByPINCode) | Directive | Instructs the client to connect to the Bluetooth speaker that has requested a PIN code.                        |
| [`BtDisconnect`](#BtDisconnect)           | Directive | Instructs the client to disconnect from the Bluetooth speaker.                               |
| [`BtRequestForPINCode`](#BtRequestForPINCode) | Event | Sends the PIN code input request of the Bluetooth speaker to CIC.               |
| [`BtRequestToCancelPinCodeInput`](#BtRequestToCancelPinCodeInput) | Event | Sends the cancellation request for the PIN code input from the Bluetooth speaker to CIC. |
| [`BtStartPairing`](#BtStartPairing)       | Directive | Instructs the client to start the Bluetooth pairing mode.                                   |
| [`BtStopPairing`](#BtStopPairing)         | Directive | Instructs the client to turn off the Bluetooth pairing mode.                                   |
| [`Decrease`](#Decrease)                   | Directive | Instructs the client to turn down the speaker volume or lower screen brightness by a default unit.                     |
| [`ExpectReportState`](#ExpectReportState) | Directive | Instructs the client to report the current state of the client to CIC.                                 |
| [`Increase`](#Increase)                   | Directive | Instructs the client to turn up the speaker volume or increase screen brightness by a default unit.                     |
| [`LaunchApp`](#LaunchApp)                 | Directive | Instructs the client to launch a specified app.                                             |
| [`OpenScreen`](#OpenScreen)               | Directive | Instructs the client to open the settings screen.                                              |
| [`ReportState`](#ReportState)             | Event     | Reports to CIC of the current device state.                     |
| [`RequestStateSynchronization`](#RequestStateSynchronization) | Event   | Requests for the current state of other client devices registered to the current user account.  |
| [`SetValue`](#SetValue)                   | Directive | Instructs the client to set the speaker volume or screen brightness to a specified value.                    |
| [`SynchronizeState`](#SynchronizeState)   | Directive | Instructs the client to update states of other client devices registered on the user account.         |
| [`TurnOff`](#TurnOff)                     | Directive | Instructs the client to turn off or disable a specified feature or mode.                           |
| [`TurnOn`](#TurnOn)                       | Directive | Instructs the client to turn on or enable a specified feature or mode.                                   |

## Client device control workflow {#DeviceContorlWorkFlow}

The general process of controlling a client device is as follows:

![](/CIC/Resources/Images/CIC_DeviceControl_Work_Flow1.png)

1. The user makes a voice request ([`SpeechRecognizer.Recognize`](/CIC/References/CICInterface/SpeechRecognizer.md#Recognize)) to control the client device. For this process, the [`Device.DeviceState`](/CIC/References/Context_Objects.md#DeviceState) context must be included in the event.
2. CIC determines whether the client can perform the control request of the user by analyzing the `actions[]` field in the [`Device.DeviceState`](/CIC/References/Context_Objects.md#DeviceState) context.
3. If the client is able to handle the request, CIC sends a directive of DeviceControl API that contains the control request.
4. After handling the directive, the client must send the result to CIC using the [`DeviceControl.ActionExecuted`](#ActionExecuted) or [`DeviceControl.ActionFailed`](#ActionFailed) event.

There are times when the Clova app needs to check the states of client devices registered in the user account. The general process of requesting for device states is as follows:

![](/CIC/Resources/Images/CIC_DeviceControl_Work_Flow2.png)

1. The client (usually the Clova app) sends the [`DeviceControl.RequestStateSynchronization`](#RequestStateSynchronization) event to CIC.
2. CIC sends the [`DeviceControl.ExpectReportState`](#ExpectReportState) directive to all clients (excluding the Clova app) registered in the user account through the [downchannel](/CIC/Guides/Interact_with_CIC.md#CreateConnection).
3. Upon receiving the [`DeviceControl.ExpectReportState`](#ExpectReportState) directive, the client must report its current state by sending the [`DeviceControl.ReportState`](#ReportState) event to CIC.
4. CIC uses the [`DeviceControl.SynchronizeState`](#SynchronizeState) directive to send the collected state information to the Clova app using the [downchannel](/CIC/Guides/Interact_with_CIC.md#CreateConnection).
5. Once receiving the [`DeviceControl.SynchronizeState`](#SynchronizeState) directive, the Clova app updates the state of other client devices.

<div class="note">
  <p><strong>Note!</strong></p>
  <p>The client will receives the <a href="#ExpectReportState"><code>DeviceControl.ExpectReportState</code></a> directive when it is newly added to the user account or is reconnected to CIC. The client can perform the same actions for the directive just like for the process of sharing the state information with the Clova app.</p>
</div>

## ActionExecuted event {#ActionExecuted}

Reports to CIC that the client has taken an action on the specified feature or mode.

### Context fields

{% include "/CIC/References/CICInterface/Context_Objects_List.md" %}

### Payload fields

| Field name       | Data type    | Description                     | Required |
|---------------|---------|-----------------------------|:---------:|
| `target`      | string  | The control target.<ul><li><code>"airplane"</code>: Airplane mode</li><li><code>"app"</code>: App</li><li><code>"bluetooth"</code>: Bluetooth</li><li><code>"cellular"</code>: Cellular network</li><li><code>"channel"</code>: TV channel</li><li><code>"flashlight"</code>: Flashlight</li><li><code>"gps"</code>: GPS</li><li><code>"powersave"</code>: Power saving mode</li><li><code>"screenbrightness"</code>: Screen brightness</li><li><code>"soundmode"</code>: Sound mode</li><li><code>"volume"</code>: Speaker volume</li><li><code>"wifi"</code>: Wi-Fi</li></ul> | Required     |
| `command`     | string  | Completed action.<ul><li> <code>"BtConnect"</code></li><li><code>"BtConnectByPINCode"</code></li><li><code>"BtDisconnect"</code></li><li><code>"BtStartPairing"</code></li><li><code>"BtStopPairing"</code></li><li><code>"Decrease"</code></li><li><code>"Increase"</code></li><li><code>"OpenScreen"</code></li><li><code>"SetValue"</code></li><li><code>"TurnOn"</code></li><li><code>"TurnOff"</code></li></ul> | Required   |

### Remarks

Upon receiving this event, CIC sends the [`SynchronizeState`](#SynchronizeState) directive to all the clients registered to the user account to inform the state change on a specified client device.

### Message example

{% raw %}

```json
{
  "context": [
    {{Alerts.AlertsState}},
    {{AudioPlayer.PlayerState}},
    {{Device.DeviceState}},
    {{Device.Display}},
    {{Clova.Location}},
    {{Clova.SavedPlace}},
    {{Speaker.VolumeState}},
    {{SpeechSynthesizer.SpeechState}}
  ],
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
* [`DeviceControl.BtConnectByPINCode`](#BtConnectByPINCode)
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

Reports to CIC that the client cannot or has failed to take an action on the specified feature or mode.

### Context fields

{% include "/CIC/References/CICInterface/Context_Objects_List.md" %}

### Payload fields

| Field name       | Data type    | Description                     | Required |
|---------------|---------|-----------------------------|:---------:|
| `target`      | string  | The control target.<ul><li><code>"airplane"</code>: Airplane mode</li><li><code>"app"</code>: App</li><li><code>"bluetooth"</code>: Bluetooth</li><li><code>"cellular"</code>: Cellular network</li><li><code>"channel"</code>: TV channel</li><li><code>"flashlight"</code>: Flashlight</li><li><code>"gps"</code>: GPS</li><li><code>"powersave"</code>: Power saving mode</li><li><code>"screenbrightness"</code>: Screen brightness</li><li><code>"soundmode"</code>: Sound mode</li><li><code>"volume"</code>: Speaker volume</li><li><code>"wifi"</code>: Wi-Fi</li></ul> | Required     |
| `command`     | string  | Failed action. <ul><li><code>"BtConnect"</code></li><li><code>"BtConnectByPINCode"</code></li><li><code>"BtDisconnect"</code></li><li><code>"BtStartPairing"</code></li><li><code>"BtStopPairing"</code></li><li><code>"Decrease"</code></li><li><code>"Increase"</code></li><li><code>"OpenScreen"</code></li><li><code>"SetValue"</code></li><li><code>"TurnOn"</code></li><li><code>"TurnOff"</code></li></ul> | Required   |

### Remarks

* Upon receiving this event, CIC sends the [`SynchronizeState`](#SynchronizeState) directive to all the clients registered to the user account to notify the state change of the client device.
* If the client has failed to launch an app after receiving the [`LaunchApp`](#LaunchApp) directive, set the `target` field to `"app"`.

### Message example

{% raw %}

```json
{
  "context": [
    {{Alerts.AlertsState}},
    {{AudioPlayer.PlayerState}},
    {{Device.DeviceState}},
    {{Device.Display}},
    {{Clova.Location}},
    {{Clova.SavedPlace}},
    {{Speaker.VolumeState}},
    {{SpeechSynthesizer.SpeechState}}
  ],
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
* [`DeviceControl.BtConnectByPINCode`](#BtConnectByPINCode)
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

Instructs the client to connect to one of the paired Bluetooth speakers. CIC may or may not specify the Bluetooth device to connect.
* When the device is not specified, the client must have its own standard to determine which of the paired devices to connect to. For example, a client may have a policy to attempt connecting in the order of the latest connected devices.
* When the device is specified, the client must attempt connecting with the specified device.

### Payload fields

* To not specify a device to connect to:

  None

* To specify a device to connect to:

| Field name       | Data type    | Description                     | Included |
|---------------|---------|-----------------------------|:---------:|
| `name`       | string  | The name of the Bluetooth device to connect to.         | Always     |
| `address`    | string  | The MAC address of the Bluetooth device to connect to.     | Always     |
| `connected`  | boolean | Indicates the connection with the specified Bluetooth device. <ul><li><code>true</code>: Connected</li><li><code>false</code>: Not connected</li></ul>      | Always     |
| `role`       | string  | The role of the Bluetooth device to connect.<ul><li><code>"sink"</code></li><li><code>"source"</code></li></ul> | Always     |

### Remarks

* This directive is only for Bluetooth speakers.
* If the received directive does not contain the `payload`, the client must attempt connection with one of the paired Bluetooth devices.
* After handling the directive, the client must send the result to CIC, using the [`DeviceControl.ActionExecuted`](#ActionExecuted) or [`DeviceControl.ActionFailed`](#ActionFailed) event.
* When reporting to CIC, the client must include the actual connection result in the [`Device.DeviceState`](/CIC/References/Context_Objects.md#DeviceState) context of the [`DeviceControl.ReportState`](#ReportState) event.

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

## BtConnectByPINCode directive {#BtConnectByPINCode}

Instructs the client to connect to the Bluetooth speaker that has requested a PIN code. CIC provides the user input PIN code in response to this message.

### Payload fields

| Field name       | Data type    | Description                     | Included |
|---------------|---------|-----------------------------|:---------:|
| `pinCode`     | string  | The PIN code of the Bluetooth speaker. The client must stop pairing if this field is an empty string (`""`). | Always     |

### Remarks

* Do not send this directive when requesting to connect with a Bluetooth speaker that does not use a PIN code.
* After handling the directive, the client must send the result to CIC, using the [`DeviceControl.ActionExecuted`](#ActionExecuted) or [`DeviceControl.ActionFailed`](#ActionFailed) event.
* When reporting to CIC, the client must include the actual connection result in the [`Device.DeviceState`](/CIC/References/Context_Objects.md#DeviceState) context of the [`DeviceControl.ReportState`](#ReportState) event.

### Message example

{% raw %}
```json
{
  "directive": {
    "header": {
      "namespace": "DeviceControl",
      "name": "BtConnectByPINCode",
      "messageId": "4e4080d6-c440-498a-bb73-ae86c6312806"
    },
    "payload": {
      "pinCode": "1234"
    }
  }
}
```
{% endraw %}

### See also

* [`DeviceControl.ActionExecuted`](#ActionExecuted)
* [`DeviceControl.ActionFailed`](#ActionFailed)
* [`DeviceControl.BtConnect`](#BtConnect)
* [`DeviceControl.BtRequestForPINCode`](#BtRequestForPINCode)
* [`DeviceControl.ReportState`](/CIC/References/Context_Objects.md#ReportState)

## BtDisconnect directive {#BtDisconnect}

Instructs the client to disconnect a Bluetooth speaker.

### Payload fields

None

### Remarks

* This directive is only for Bluetooth speakers.
* The client must frequently report the states of paired Bluetooth devices to CIC using the [`Device.DeviceState`](/CIC/References/Context_Objects.md#DeviceState) object.
* After handling the directive, the client must send the result to CIC, using the [`DeviceControl.ActionExecuted`](#ActionExecuted) or [`DeviceControl.ActionFailed`](#ActionFailed) event.

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

## BtRequestForPINCode event {#BtRequestForPINCode}

Sends the PIN code input request of the Bluetooth speaker to CIC.

### Context fields

{% include "/CIC/References/CICInterface/Context_Objects_List.md" %}

### Payload fields

| Field name       | Data type    | Description                     | Required |
|---------------|---------|-----------------------------|:---------:|
| `deviceName`  | string  | The name of the Bluetooth device to connect. This name is displayed on the PIN code input screen. | Required     |

### Remarks

* Send this event only when the Bluetooth device to connect requests a PIN code. Generally, the PIN code is requested at initial connection.
* After receiving this event, CIC sends a PIN code to the client through the [`DeviceControl.BtConnectByPINCode`](#BtConnectByPINCode) directive.

### Message example

{% raw %}
```json
{
  "context": [
    {{Alerts.AlertsState}},
    {{AudioPlayer.PlayerState}},
    {{Device.DeviceState}},
    {{Device.Display}},
    {{Clova.Location}},
    {{Clova.SavedPlace}},
    {{Speaker.VolumeState}},
    {{SpeechSynthesizer.SpeechState}}
  ],
  "event": {
    "header": {
      "namespace": "DeviceControl",
      "name": "BtRequestForPINCode",
      "messageId": "4e4080d6-c440-498a-bb73-ae86c6312806",
    },
    "payload": {
      "deviceName": "friends device"
    }
  }
}
```
{% endraw %}

### See also

* [`DeviceControl.BtConnect`](#BtConnect)
* [`DeviceControl.BtConnectByPINCode`](#BtConnectByPINCode)
* [`DeviceControl.BtRequestToCancelPinCodeInput`](#BtRequestToCancelPinCodeInput)

## BtRequestToCancelPinCodeInput event {#BtRequestToCancelPinCodeInput}

Sends the cancellation request for the PIN code input from the Bluetooth speaker to CIC.

### Context fields

{% include "/CIC/References/CICInterface/Context_Objects_List.md" %}

### Payload fields

None

### Remarks

* You can cancel the PIN code input request in special circumstances such as no PIN input for a prolonged time or a lost Bluetooth connection.

### Message example

{% raw %}
```json
{
  "context": [
    {{Alerts.AlertsState}},
    {{AudioPlayer.PlayerState}},
    {{Device.DeviceState}},
    {{Device.Display}},
    {{Clova.Location}},
    {{Clova.SavedPlace}},
    {{Speaker.VolumeState}},
    {{SpeechSynthesizer.SpeechState}}
  ],
  "event": {
    "header": {
      "namespace": "DeviceControl",
      "name": "BtRequestToCancelPinCodeInput",
      "messageId": "4e4080d6-c440-498a-bb73-ae86c6312806",
    },
    "payload": {}
  }
}
```
{% endraw %}

### See also

* [`DeviceControl.BtRequestForPINCode`](#BtRequestForPINCode)

## BtStartPairing directive {#BtStartPairing}

Instructs the client to start the Bluetooth pairing mode.

### Payload fields

None

### Remarks

* This directive is only for Bluetooth speakers.
* The client must frequently report the states of paired Bluetooth devices to CIC using the [`Device.DeviceState`](/CIC/References/Context_Objects.md#DeviceState) object.
* After handling the directive, the client must send the result to CIC, using the [`DeviceControl.ActionExecuted`](#ActionExecuted) or [`DeviceControl.ActionFailed`](#ActionFailed) event.

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

Instructs the client to turn off the Bluetooth pairing mode.

### Payload fields

None

### Remarks

* This directive is only for Bluetooth speakers.
* The client must frequently report the states of paired Bluetooth devices to CIC using the [`Device.DeviceState`](/CIC/References/Context_Objects.md#DeviceState) object.
* After handling the directive, the client must send the result to CIC, using the [`DeviceControl.ActionExecuted`](#ActionExecuted) or [`DeviceControl.ActionFailed`](#ActionFailed) event.

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

Instructs the client to turn down the speaker volume or lower the screen brightness by the default unit defined on the client or change the TV channel downward.

### Payload fields

| Field name       | Data type    | Description                     | Included |
|---------------|---------|-----------------------------|:---------:|
| `target`      | string  | The control target.<ul><li><code>"channel"</code>: TV channel</li><li><code>"screenbrightness"</code>: Screen brightness</li><li><code>"volume"</code>: Speaker volume</li></ul> | Always     |

### Remarks

* The default unit by which the volume or brightness is changed is up to the client.
* The client must frequently report the current speaker volume and screen brightness to CIC using the [`Device.DeviceState`](/CIC/References/Context_Objects.md#DeviceState) context object.
* After handling the directive, the client must send the result to CIC, using the [`DeviceControl.ActionExecuted`](#ActionExecuted) or [`DeviceControl.ActionFailed`](#ActionFailed) event.
* Clova normally provides a voice guide ([`SpeechSynthesizer.Speak`](/CIC/References/CICInterface/SpeechSynthesizer.md#Speak) directive) when sending a directive to the client for device control. However, if the control is related to speaker output like the `"volume"` is set in the `target` field, Clova does not provide a voice guide with the [`SpeechSynthesizer.Speak`](/CIC/References/CICInterface/SpeechSynthesizer.md#Speak) directive. This is in consideration of the UX such as for a user listening to music. Instead, you should implement an action to inform the user that the volume has been changed using the lights or a simple sound effect on the client.

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

Instructs the client to report the current state of the client to CIC. Upon receiving this directive, the client must immediately report its current state by sending the [`DeviceControl.ReportState`](#ReportState) event to CIC. After reporting, the client shall report the state at every interval in the `intervalInSeconds` field for the duration in the `durationInSeconds` field.

### Payload fields

| Field name       | Data type    | Description                     | Included |
|---------------|---------|-----------------------------|:---------:|
| `durationInSeconds` | number  | The duration of report. Reports the current state of the device for the specified duration. The unit is in seconds. If this field is undefined, only one report is made to CIC. | Conditional     |
| `intervalInSeconds` | number  | The reporting interval. Reports the current state of the device at the specified interval. The unit is in seconds. This field is valid only when a value exists in the `durationInSeconds` field. | Conditional     |

### Remarks

* The `DeviceControl.ExpectReportState` directive is received when the [`DeviceControl.RequestStateSynchronization`](#RequestStateSynchronization) event is sent to CIC from other clients for synchronization.
* This directive is sent through a [downchannel](/CIC/Guides/Interact_with_CIC.md#CreateConnection), not as a response to an event.

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

Instructs the client to turn up the speaker volume or increase the screen brightness by the default unit defined on the client or change the TV channel upward.

### Payload fields

| Field name       | Data type    | Description                     | Included |
|---------------|---------|-----------------------------|:---------:|
| `target`      | string  | The control target.<ul><li><code>"channel"</code>: TV channel</li><li><code>"screenbrightness"</code>: Screen brightness</li><li><code>"volume"</code>: Speaker volume</li></ul> | Always     |

### Remarks

* The default unit by which the volume or brightness is changed is up to the client.
* The client must frequently report the current speaker volume and screen brightness to CIC using the [`Device.DeviceState`](/CIC/References/Context_Objects.md#DeviceState) context object.
* After handling the directive, the client must send the result to CIC, using the [`DeviceControl.ActionExecuted`](#ActionExecuted) or [`DeviceControl.ActionFailed`](#ActionFailed) event.
* Clova normally provides a voice guide ([`SpeechSynthesizer.Speak`](/CIC/References/CICInterface/SpeechSynthesizer.md#Speak) directive) when sending a directive to the client for device control. However, if the control is related to speaker output like the `"volume"` is set in the `target` field, Clova does not provide a voice guide with the [`SpeechSynthesizer.Speak`](/CIC/References/CICInterface/SpeechSynthesizer.md#Speak) directive. This is in consideration of the UX such as for a user listening to music. Instead, you should implement an action to inform the user that the volume has been changed using the lights or a simple sound effect on the client.

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

Instructs the client to launch a specified app. The app is specified by a custom URL scheme, a relay page URL, or the app name.

### Payload fields

| Field name       | Data type    | Description                     | Included |
|---------------|---------|-----------------------------|:---------:|
| `target`      | string  | The target app to launch. The app can be specified in one of the following ways: <ul><li>Custom URL scheme: A custom URL scheme of the target app. E.g. <code>"{{ book.OrientedServiceWithLowerCase }}searchapp://..."</code></li><li>Relay page URL: A relay page URL that launches the app if the app is already installed. E.g. <code>"http://{{ book.OrientedServiceWithLowerCase }}app.{{ book.OrientedServiceWithLowerCase }}.com/..."</code></li><li>App name: The name of the app recognized from user speech. E.g. <code>"{{ book.OrientedService }}App"</code></li></ul> | Always     |

### Remarks

* If the client cannot or has failed to launch the specified app, send the result to CIC using the [`DeviceControl.ActionFailed`](#ActionFailed) event.

### Message example

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
      "target": "{{ book.OrientedServiceWithLowerCase }}searchapp://..."
    }
  }
}
```

### See also
* [`DeviceControl.ActionFailed`](#ActionFailed)

## OpenScreen directive {#OpenScreen}

Instructs the client to open the settings screen.

### Payload fields

| Field name       | Data type    | Description                     | Included |
|---------------|---------|-----------------------------|:---------:|
| `target`      | string  | The screen to display. Available values are: `"settings"` | Always     |

### Remarks

The client must send the result of handling this directive to CIC using the [`DeviceControl.ActionExecuted`](#ActionExecuted) or [`DeviceControl.ActionFailed`](#ActionFailed) event.

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

Reports to CIC of the current device state.

### Context fields

{% include "/CIC/References/CICInterface/Context_Objects_List.md" %}

### Payload fields

None

### Remarks

* Upon receiving the [`DeviceControl.ExpectReportState`](#ExpectReportState) directive from CIC, the client must report its current state using the `DeviceControl.ReportState` event.
* The state reported through this event is delivered to all the clients registered to the user account, through the [`DeviceControl.SynchronizeState`](#SynchronizeState) directive.
* No directive is returned as a response to this event and the HTTP response is returned as `204 No Content`.

### Message example

{% raw %}

```json
{
  "context": [
    {{Alerts.AlertsState}},
    {{AudioPlayer.PlayerState}},
    {{Device.DeviceState}},
    {{Device.Display}},
    {{Clova.Location}},
    {{Clova.SavedPlace}},
    {{Speaker.VolumeState}},
    {{SpeechSynthesizer.SpeechState}}
  ],
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
* [`DeviceControl.ExpectReportState`](#ExpectReportState)
* [`DeviceControl.SynchronizeState`](#SynchronizeState)

## RequestStateSynchronization event {#RequestStateSynchronization}

Requests for the current state of other client devices registered to the current user account. In return, CIC will send the [`DeviceControl.ExpectReportState`](#ExpectReportState) directive to all the clients registered to the user account.

### Context fields

{% include "/CIC/References/CICInterface/Context_Objects_List.md" %}

### Payload fields

None

### Remarks

* As a response to this event, CIC will send the [`DeviceControl.SynchronizeState`](#SynchronizeState) directive through a [downchannel](/CIC/Guides/Interact_with_CIC.md#CreateConnection).
* No directive is returned as a response to this event and the HTTP response is returned as `204 No Content`.

### Message example

{% raw %}

```json
{
  "context": [
    {{Alerts.AlertsState}},
    {{AudioPlayer.PlayerState}},
    {{Device.DeviceState}},
    {{Device.Display}},
    {{Clova.Location}},
    {{Clova.SavedPlace}},
    {{Speaker.VolumeState}},
    {{SpeechSynthesizer.SpeechState}}
  ],
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

Instructs the client to set the speaker volume level or screen brightness level to the given value or change the TV channel to the given value.

### Payload fields

| Field name       | Data type    | Description                     | Included |
|---------------|---------|-----------------------------|:---------:|
| `target`      | string  | The control target.<ul><li><code>"channel"</code>: TV channel</li><li><code>"screenbrightness"</code>: Screen brightness</li><li><code>"volume"</code>: Speaker volume</li></ul> | Always     |
| `value`       | string  | The value to change to or the TV channel or name.        | Always     |

### Remarks

* The client must frequently report the current speaker volume and screen brightness to CIC using the [`Device.DeviceState`](/CIC/References/Context_Objects.md#DeviceState) context object.
* After handling the directive, the client must send the result to CIC, using the [`DeviceControl.ActionExecuted`](#ActionExecuted) or [`DeviceControl.ActionFailed`](#ActionFailed) event.
* Clova normally provides a voice guide ([`SpeechSynthesizer.Speak`](/CIC/References/CICInterface/SpeechSynthesizer.md#Speak) directive) when sending a directive to the client for device control. However, if the control is related to speaker output like the `"volume"` is set in the `target` field, Clova does not provide a voice guide with the [`SpeechSynthesizer.Speak`](/CIC/References/CICInterface/SpeechSynthesizer.md#Speak) directive. This is in consideration of the UX such as for a user listening to music. Instead, you should implement an action to inform the user that the volume has been changed using the lights or a simple sound effect on the client.

### Message example

{% raw %}

```json
// Change volume
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

Instructs the client to update the states of other client devices registered to the user account. Users can use several clients simultaneously with a single user account. For instance, a client may be an app or Wave, which is an exclusive speaker for Clova. Suppose a client app can control other speaker clients. The app will receive the results of controlling other clients through the `DeviceControl.SynchronizeState` directive and update the states of other clients.

A client may receive this directive in the following cases:

* When CIC receives the [`DeviceControl.ActionExecuted`](#ActionExecuted) event or [`DeviceControl.ActionFailed`](#ActionFailed) event, CIC broadcasts the `DeviceControl.SynchronizeState` directive to all the clients registered to the user account to report the state change of the client device.
* When CIC receives the [`DeviceControl.ReportState`](#ReportState) event, CIC broadcasts the `DeviceControl.SynchronizeState` directive to all the clients registered to the user account to report the state change of the client device.

### Payload fields

| Field name       | Data type    | Description                     | Included |
|---------------|---------|-----------------------------|:---------:|
| `deviceId`    | string  | The ID of the client device with the updated state. | Always     |
| `deviceState` | [Device.DeviceState](/CIC/References/Context_Objects.md#DeviceState) object | The update information on the device state.         | Always     |

### Remarks

The `DeviceControl.SynchronizeState` directive is broadcasted to all the clients registered to the user account through a [downchannel](/CIC/Guides/Interact_with_CIC.md#CreateConnection) and does not contain a [communication ID (`dialogRequestId`)](/CIC/CIC_Overview.md#DialogModel).

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
      "deviceId": "90de78d7-0735-43a8-8bdc-acc3c8bc4a80",
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

Instructs the client to turn off or disable a specified feature or mode. For example, you can use this directive to turn off the Bluetooth of the client device.

### Payload fields

| Field name       | Data type    | Description                     | Included |
|---------------|---------|-----------------------------|:---------:|
| `target`      | string  | The control target.<ul><li><code>"airplane"</code>: Airplane mode</li><li><code>"bluetooth"</code>: Bluetooth</li><li><code>"cellular"</code>: Cellular network</li><li><code>"energysave"</code>: Energy saving mode</li><li><code>"flashlight"</code>: Flashlight</li><li><code>"gps"</code>: GPS</li><li><code>"power"</code>: Power state</li><li><code>"ring"</code>: Ring mode</li><li><code>"silent"</code>: Silent mode</li><li><code>"vibrate"</code>: Vibration mode</li><li><code>"wifi"</code>: Wi-Fi</li></ul> | Always     |

### Remarks

* When turning off or disabling a certain feature or mode, follow the policy of the client device. For example, when disabling sound, the client policy will determine whether or not the client activates vibration or mute mode.
* The client must frequently report the client state to CIC using the [`Device.DeviceState`](/CIC/References/Context_Objects.md#DeviceState) context object.
* After handling the directive, the client must send the result to CIC, using the [`DeviceControl.ActionExecuted`](#ActionExecuted) or [`DeviceControl.ActionFailed`](#ActionFailed) event.

<div class="danger">
  <p><strong>Caution!</strong></p>
  <p>Turn the power off of the client device when the <code>target</code> field is set to <code>"power"</code>.</p>
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

Instructs the client to turn on or enable a specified feature or mode. For example, you can use this directive to turn on the Bluetooth of the client device.

### Payload fields

| Field name       | Data type    | Description                     | Included |
|---------------|---------|-----------------------------|:---------:|
| `target`      | string  | The control target.<ul><li><code>"airplane"</code>: Airplane mode</li><li><code>"bluetooth"</code>: Bluetooth</li><li><code>"cellular"</code>: Cellular network</li><li><code>"energysave"</code>: Energy saving mode</li><li><code>"flashlight"</code>: Flashlight</li><li><code>"gps"</code>: GPS</li><li><code>"power"</code>: Power state</li><li><code>"ring"</code>: Ring mode</li><li><code>"silent"</code>: Silent mode</li><li><code>"vibrate"</code>: Vibration mode</li><li><code>"wifi"</code>: Wi-Fi</li></ul> | Always     |

### Remarks

* The client must frequently report the client state to CIC using the [`Device.DeviceState`](/CIC/References/Context_Objects.md#DeviceState) context object.
* After handling the directive, the client must send the result to CIC, using the [`DeviceControl.ActionExecuted`](#ActionExecuted) or [`DeviceControl.ActionFailed`](#ActionFailed) event.

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
