# DeviceControl

The DeviceControl namespace provides interfaces for controlling client devices or reporting to CIC the result of changing client device settings.

Users may request to manipulating their client devices. If the user's request is on controlling the client device, the client will receive a directive of this namespace, `DeviceControl`. The client has to perform the task instructed by the directive and then send the result to CIC.

The DeviceControl namespace provides the following events and directives.

| Message name         | Message type  | Message description                                   |
|------------------|-----------|---------------------------------------------|
| [`ActionExecuted`](#ActionExecuted)       | Event     | A message to notify CIC that the client has successfully changed the specified settings.           |
| [`ActionFailed`](#ActionFailed)           | Event     | A message to notify CIC that the client cannot or has failed to change the specified settings. |
| [`BtConnect`](#BtConnect)                 | Directive | Instructs a client to connect a Bluetooth speaker.                               |
| [`BtDisconnect`](#BtDisconnect)           | Directive | Instructs a client to disconnect a Bluetooth speaker.                               |
| [`BtStartPairing`](#BtStartPairing)       | Directive | Instructs a client to start the Bluetooth pairing mode.                                   |
| [`BtStopPairing`](#BtStopPairing)         | Directive | Instructs a client to terminate the Bluetooth pairing mode.                                   |
| [`Decrease`](#Decrease)                   | Directive | Instructs a client to turn down speaker volume or decrease screen brightness by a default unit.                     |
| [`ExpectReportState`](#ExpectReportState)  | Directive | Instructs a client to report the current state of the client device to CIC.                             |
| [`Increase`](#Increase)                   | Directive | Instructs a client to turn up speaker volume or increase screen brightness by a default unit.                     |
| [`LaunchApp`](#LaunchApp)                 | Directive | Instructs a client to launch the specified app.                                             |
| [`OpenScreen`](#OpenScreen)               | Directive | Instructs a client to open the settings screen.                                              |
| [`ReportState`](#ReportState)             | Event     | A message to notify CIC the current state of the appliance to CIC.                |
| [`RequestStateSynchronization`](#RequestStateSynchronization) | Event   | A message to notify CIC to acquire current state of other client's devices registered on the user's account.  |
| [`SetValue`](#SetValue)                   | Directive | Instructs a client to set speaker volume or screen brightness to a specified value.                    |
| [`SynchronizeState`](#SynchronizeState)     | Directive | Instructs a client to update states of other client's devices registered on the user account.         |
| [`TurnOff`](#TurnOff)                     | Directive | Instructs a client to turn off or disable a specified feature or mode.                           |
| [`TurnOn`](#TurnOn)                       | Directive | Instructs a client to turn on or enable a specified feature or mode.                                   |

<div class="note">
  <p><strong>Note!</strong></p>
  <p>The DeviceControl API is yet to be implemented. This specification is provided only for the defining process and is subject to change.</p>
</div>

## ActionExecuted event {#ActionExecuted}

A message for reporting to CIC that the client has taken an action on the specified feature or mode.

### Context fields

None

### Payload fields

| Field name       | Type    | Description                     | Required |
|---------------|:---------:|-----------------------------|:---------:|
| `target`      | string  | The feature or mode that the client has taken an action on:<ul><li><code>"airplane"</code>: Airplane mode</li><li><code>"app"</code>: App</li><li><code>"bluetooth"</code>: Bluetooth</li><li><code>"cellular"</code>: Cellular network</li><li><code>"channel"</code>: TV channel</li><li><code>"flashlight"</code>: Flashlight</li><li><code>"gps"</code>: GPS</li><li><code>"powersave"</code>: Power saving mode</li><li><code>"screenbrightness"</code>: Screen brightness</li><li><code>"soundmode"</code>: Sound mode</li><li><code>"volume"</code>: Speaker volume</li><li><code>"wifi"</code>: WiFi</li></ul> | Required |
| `command`     | string  | The successful action taken by the client.  <ul><li>BtConnect</li><li>BtDisconnect</li><li>BtStartPairing</li><li>BtStopPairing</li><li>Decrease</li><li>Increase</li><li>OpenScreen</li><li>SetValue</li><li>TurnOn</li><li>TurnOff</li></ul> | Required |

### Remarks

When CIC receives this event, CIC sends the [`SynchronizeState`](#SynchronizeState) directive to all the clients registered to the current user's account to notify the state change of the client device.

### Message example

{% raw %}

```json
{
  "context": [],
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

A message for reporting to CIC that the client cannot or has failed to take an action on the specified feature or mode.

### Context fields

None

### Payload fields

| Field name       | Type    | Description                     | Required |
|---------------|:---------:|-----------------------------|:---------:|
| `target`      | string  | The feature or mode the client cannot or has failed to take an action on:<ul><li><code>"airplane"</code>: Airplane mode</li><li><code>"app"</code>: App</li><li><code>"bluetooth"</code>: Bluetooth</li><li><code>"cellular"</code>: Cellular network</li><li><code>"channel"</code>: TV channel</li><li><code>"flashlight"</code>: Flashlight</li><li><code>"gps"</code>: GPS</li><li><code>"powersave"</code>: Power saving mode</li><li><code>"screenbrightness"</code>: Screen brightness</li><li><code>"soundmode"</code>: Sound mode</li><li><code>"volume"</code>: Speaker volume</li><li><code>"wifi"</code>: WiFi</li></ul>| Required     |
| `command`     | string  | The action the client cannot perform or has failed. <ul><li>BtConnect</li><li>BtDisconnect</li><li>BtStartPairing</li><li>BtStopPairing</li><li>Decrease</li><li>Increase</li><li>LaunchApp</li><li>OpenScreen</li><li>SetValue</li><li>TurnOn</li><li>TurnOff</li></ul> | Required   |

### Remarks

* Upon receiving this event, CIC sends the [`SynchronizeState`](#SynchronizeState) directive to all the clients registered to the user's account to notify the state change of the client's device.
* If the client has failed to launch an app after for the [`LaunchApp`](#LaunchApp) directive, set the `target` field to `"app"`.

### Message example

{% raw %}

```json
{
  "context": [],
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

Instructs a client to connect to one of the paired Bluetooth speakers to send the sound out. If the client is paired with more than one device, the client shall connect to the one based on its pre-defined policy. For example, a client may have a policy to attempt connecting in the order of the latest to oldest connections .

### Payload fields

None

### Remarks

* This directive is only for Bluetooth speakers for sending sound out.
* The client must frequently report the states of paired Bluetooth devices to CIC frequently, using the [`Device.DeviceState`](/CIC/References/Context_Objects.md#DeviceState) object.
* The client must send the result of processing this directive to CIC, using the [`DeviceControl.ActionExecuted`](#ActionExecuted) or [`DeviceControl.ActionFailed`](#ActionFailed) event.

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

Instructs a client to disconnect a Bluetooth speaker for sending sound out.

### Payload fields

None

### Remarks

* This directive is only for Bluetooth speakers for sending sound out.
* The client must frequently report the states of paired Bluetooth devices to CIC frequently, using the [`Device.DeviceState`](/CIC/References/Context_Objects.md#DeviceState) object.
* The client must send the result of processing this directive to CIC, using the [`DeviceControl.ActionExecuted`](#ActionExecuted) or [`DeviceControl.ActionFailed`](#ActionFailed) event.

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

Instructs a client to start the Bluetooth pairing mode.

### Payload fields

None

### Remarks

* This directive is only for Bluetooth speakers for sending sound out.
* The client must frequently report the states of paired Bluetooth devices to CIC frequently, using the [`Device.DeviceState`](/CIC/References/Context_Objects.md#DeviceState) object.
* The client must send the result of processing this directive to CIC, using the [`DeviceControl.ActionExecuted`](#ActionExecuted) or [`DeviceControl.ActionFailed`](#ActionFailed) event.

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

Instructs a client to turn off the Bluetooth pairing mode.

### Payload fields

None

### Remarks

* This directive is only for Bluetooth speakers for sending sound out.
* The client must frequently report the states of paired Bluetooth devices to CIC frequently, using the [`Device.DeviceState`](/CIC/References/Context_Objects.md#DeviceState) object.
* The client must send the result of processing this directive to CIC, using the [`DeviceControl.ActionExecuted`](#ActionExecuted) or [`DeviceControl.ActionFailed`](#ActionFailed) event.

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

Instructs a client to turn down the client's speaker volume or make the client screen darker by the default unit defined on the client, or change the TV channel down.

### Payload fields

| Field name       | Type    | Description                     | Provided |
|---------------|:---------:|-----------------------------|:---------:|
| `target`      | string  | The settings to change:<ul><li><code>"channel"</code>: TV channel</li><li><code>"screenbrightness"</code>: Screen brightness</li><li><code>"volume"</code>: Speaker volume</li></ul> | Always |

### Remarks

* The default unit by which the volume or brightness is changed is up to the client.
* The client must frequently inform the CIC of the current speaker volume level and screen brightness level, using the [`Device.DeviceState`](/CIC/References/Context_Objects.md#DeviceState) context object.
* The client must send the result of processing this directive to CIC, using the [`DeviceControl.ActionExecuted`](#ActionExecuted) event or the [`DeviceControl.ActionFailed`](#ActionFailed) event.

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

Instructs a client to report the current state of the client to CIC. When receiving this directive, the client shall immediately report the current state to CIC using the [`DeviceControl.ReportState`](#ReportState) event. After reporting, the client shall report the state at every `intervalInSeconds` for `durationInSeconds`.

### Payload fields

| Field name       | Type    | Description                     | Provided |
|---------------|:---------:|-----------------------------|:---------:|
| `durationInSeconds` | number  | The period during which the client shall repeat reporting its state to CIC. The unit is second. If this field is undefined, report to CIC only once. | Conditional |
| `intervalInSeconds` | number  | The reporting cycle. At every interval defined by this field, report the current client state to CIC. The unit is second. This field is valid only if the `durationInSeconds` field is defined. If `durationInSeconds` is undefined, so is this field. | Conditional |

### Remarks

* The `DeviceControl.ExpectReportState` directive is received when the [`DeviceControl.RequestStateSynchronization`](#RequestStateSynchronization) event is sent to CIC from other clients for synchronization.
* This directive is sent through [downchannel](/CIC/Guides/Interact_with_CIC.md#CreateConnection), not as a response to an event.

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

Instructs a client to turn up the client's speaker volume or make the client screen brighter by the default unit defined on the client, or change the TV channel up.

### Payload fields

| Field name       | Type    | Description                     | Provided |
|---------------|:---------:|-----------------------------|:---------:|
| `target`      | string  | The settings to change: <ul><li><code>"channel"</code>: TV channel</li><li><code>"screenbrightness"</code>: Screen brightness</li><li><code>"volume"</code>: Speaker volume</li></ul> | Always |

### Remarks

* The default unit by which the volume or brightness is changed is up to the client.
* The client must frequently inform the CIC of the current speaker volume level and screen brightness level, using the [`Device.DeviceState`](/CIC/References/Context_Objects.md#DeviceState) context object.
* The client must send the result of processing this directive to CIC, using the [`DeviceControl.ActionExecuted`](#ActionExecuted) event or the [`DeviceControl.ActionFailed`](#ActionFailed) event.

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

Instructs a client to launch the specified app. The app is specified by a custom URL scheme or a relay page URL or the app name.

### Payload fields

| Field name       | Type    | Description                     | Provided |
|---------------|:---------:|-----------------------------|:---------:|
| `target`      | string  | Specifies the app to launch. The app can be specified in one of the following ways: <ul><li>Custom URL scheme: A custom URL scheme of the target app. e.g. <code>"naversearchapp://..."</code></li><li>Relay page URL: A relay page URL that launches the app if the app is already installed. e.g. <code>"http://naverapp.naver.com/..."</code></li><li>App name: The name of the app recognized from user's speech. e.g. <code>"NAVER App"</code></li></ul> | Always |

### Remarks

* If the client cannot or has failed to launch the specified app, send the result to CIC using the [`DeviceControl.ActionFailed`](#ActionFailed) event.

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

Instructs a client to open the setting screen.

### Payload fields

| Field name       | Type    | Description                     | Provided |
|---------------|:---------:|-----------------------------|:---------:|
| `target`      | string  | The screen to display. Available values are: <ul><li><code>"settings"</code></li></ul> | Always |

### Remarks

The client must send the result of processing this directive to CIC, using the [`DeviceControl.ActionExecuted`](#ActionExecuted) event or [`DeviceControl.ActionFailed`](#ActionFailed) event.

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

A message for reporting to CIC the current state of the client to CIC.

### Context fields

To deliver the current state of the client device, send the following [Context information(Context)](/CIC/References/Context_Objects.md) with this event.

* [`Device.DeviceState`](/CIC/References/Context_Objects.md#DeviceState)

### Payload fields

None

### Remarks

* Send this event to report the current client state, when you receive the [`DeviceControl.ExpectReportState`](#ExpectReportState) directive from CIC.
* The state reported through this event will be delivered to all the clients registered to the current user's account, through the [`DeviceControl.SynchronizeState`](#SynchronizeState) directive.

### Message example

{% raw %}

```json
{
  "context": [
      {{Device.DeviceState}}
    ],
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

* [`Device.DeviceState`](/CIC/References/Context_Objects.md#DeviceState)
* [`DeviceControl.ExpectReportState`](#ExpectReportState)
* [`DeviceControl.SynchronizeState`](#SynchronizeState)

## RequestStateSynchronization event {#RequestStateSynchronization}

A message for reporting to CIC to acquire the current state of other client devices registered to the current user's account. In return, CIC will send the [`DeviceControl.ExpectReportState`](#ExpectReportState) directive to all the clients registered to the current user's account.

### Context fields

None

### Payload fields

None

### Remarks

As a response to this event, CIC will send the [`DeviceControl.SynchronizeState`](#SynchronizeState) directive through a [downchannel](/CIC/Guides/Interact_with_CIC.md#CreateConnection).

### Message example

{% raw %}

```json
{
  "context": [],
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

Instructs a client to set the speaker volume level or screen brightness level to the given value, or change the TV channel to the given value.

### Payload fields

| Field name       | Type    | Description                     | Provided |
|---------------|:---------:|-----------------------------|:---------:|
| `target`      | string  | The settings to change:<ul><li><code>"channel"</code>: TV channel</li><li><code>"screenbrightness"</code>: Screen brightness</li><li><code>"volume"</code>: Speaker volume</li></ul> | Always |
| `value`       | string  | The level or TV channel to change to.       | Always |

### Remarks

* The client must frequently inform the CIC of the current speaker volume level and screen brightness level, using the [`Device.DeviceState`](/CIC/References/Context_Objects.md#DeviceState) context object.
* The client must send the result of processing this directive to CIC, using the [`DeviceControl.ActionExecuted`](#ActionExecuted) event or the [`DeviceControl.ActionFailed`](#ActionFailed) event.

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

Instructs a client to update the states of other client devices registered to the current user's account. Users can use several clients simultaneously with a single user account. For instance, a client may be an app or Wave, an exclusive speaker for Clova. Suppose a client app can control other speaker clients. The app will receive the results of controlling other clients through the `DeviceControl.SynchronizeState` directive, and update other clients' states.

A client may receive this directive in the following cases:

* When CIC receives the [`DeviceControl.ActionExecuted`](#ActionExecuted) event or [`DeviceControl.ActionFailed`](#ActionFailed) event: CIC broadcasts the `DeviceControl.SynchronizeState` directive to all the clients registered to the current user's account to notify the state change of the client device.
* When CIC receives the [`DeviceControl.ReportState`](#ReportState) event: CIC broadcasts the `DeviceControl.SynchronizeState` directive to all the clients registered to the current user's account to notify the state change of the client device.

### Payload fields

| Field name       | Type    | Description                     | Provided |
|---------------|:---------:|-----------------------------|:---------:|
| `deviceId`    | string  | The ID of the client device with an updated state. | Always |
| `deviceState` | [Device.DeviceState](/CIC/References/Context_Objects.md#DeviceState) object | Contains the updated state of the device.    | Always |

### Remarks

The `DeviceControl.SynchronizeState` directive is broadcasted to all the clients registered to a user's account through a [downchannel](/CIC/Guides/Interact_with_CIC.md#CreateConnection) and does not contain a [communication ID (`dialogRequestId`)](/CIC/CIC_Overview.md#DialogModel).

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
      "deviceId": "2cd9a306-a7d4-45be-943a-0f4e4a70812b",
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

Instructs a client to turn off or disable the specified feature or mode on the client, such as Bluetooth.

### Payload fields

| Field name       | Type    | Description                     | Provided |
|---------------|:---------:|-----------------------------|:---------:|
| `target`      | string  | The feature or mode to turn off:<ul><li><code>"airplane"</code>: Airplane mode</li><li><code>"bluetooth"</code>: Bluetooth</li><li><code>"cellular"</code>: Mobile communication</li><li><code>"energysave"</code>: Energy saving mode</li><li><code>"flashlight"</code>: Flashlight</li><li><code>"gps"</code>: GPS</li><li><code>"power"</code>: Power state</li><li><code>"ring"</code>: Ring mode</li><li><code>"silent"</code>: Silent mode</li><li><code>"vibrate"</code>: Vibration mode</li><li><code>"wifi"</code>: Wireless LAN</li></ul> | Always |

### Remarks

* When turning off or disabling a certain feature or mode, follow the policy of the client device. For example, when disabling sound, the client policy will determine whether the client activates vibration mode or mutes.
* The client must frequently report the client state to CIC, using the [`Device.DeviceState`](/CIC/References/Context_Objects.md#DeviceState) context object.
* The client must send the result of processing this directive to CIC, using the [`DeviceControl.ActionExecuted`](#ActionExecuted) event or the [`DeviceControl.ActionFailed`](#ActionFailed) event.

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

Instructs a client to turn on or enable the specified feature or mode on the client, such as Bluetooth.

### Payload fields

| Field name       | Type    | Description                     | Provided |
|---------------|:---------:|-----------------------------|:---------:|
| `target`      | string  | The feature or mode to turn on:<ul><li><code>"airplane"</code>: Airplane mode</li><li><code>"bluetooth"</code>: Bluetooth</li><li><code>"cellular"</code>: Mobile communication</li><li><code>"energysave"</code>: Energy saving mode</li><li><code>"flashlight"</code>: Flashlight</li><li><code>"gps"</code>: GPS</li><li><code>"power"</code>: Power state</li><li><code>"ring"</code>: Ring mode</li><li><code>"silent"</code>: Silent mode</li><li><code>"vibrate"</code>: Vibration mode</li><li><code>"wifi"</code>: Wireless LAN</li></ul> | Always     |

### Remarks

* The client must frequently report the client state to CIC, using the [`Device.DeviceState`](/CIC/References/Context_Objects.md#DeviceState) context object.
* The client must send the result of processing this directive to CIC, using the [`DeviceControl.ActionExecuted`](#ActionExecuted) event or the [`DeviceControl.ActionFailed`](#ActionFailed) event.

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
