## Shared objects {#SharedObjects}
When you send [Clova Home extension messages](/CEK/References/CEK_API.md#ClovaHomeExtMessage), the following shared objects are included in a message body (payload).

| Object name            | Object description                                            |
|--------------------|---------------------------------------------------|
| [ApplianceObject](#ApplianceObject)     | An object containing details of an IoT appliance        |
| [HeatingModeObject](#HeatingModeObject) | An object containing a heating mode          |
| [SpeedObject](#SpeedObject)             | An object containing a speed              |
| [TemperatureObject](#TemperatureObject) | An object containing a temperature          |
| [TVChannelObject](#TVChannelObject)     | An object containing a TV channel           |
| [VolumeObject](#VolumeObject)           | An object containing a volume          |

### ApplianceObject {#ApplianceObject}
An object containing details of an IoT appliance. This object is used when returning CEK a list of appliances registered to a user account or when requesting a Clova Home extension to control a specified appliance.

#### Object field
| Field name       | Type    | Field description                     | Required |
|---------------|---------|-----------------------------|---------|
| `actions[]`                  | string array  | A list of actions supported by the appliance. You must limit the allowed actions to those supported by the appliance. | No    |
| `additionalApplianceDetails` | object        | A field containing additional details of the appliance provided from the manufacturer or IoT service                                 | No    |
| `applianceId`                | string        | The appliance ID                                                                        | Yes    |
| `applianceTypes[]`           | string array  | The appliance type. `applicationType` determines allowed actions you can specify in the `actions` field. Specify the type as one of the following values for the appliances registered to the user's IoT service account.<ul><li>AIRCONDITIONER: Air conditioning or heating system type</li><li>AIRPURIFIER: Air purifier type</li><li>HUMIDIFIER: Humidifier type</li><li>LIGHT: Lighting appliance type</li><li>SETTOPBOX: TV set-top box type</li><li>SMARTPLUG: Plugs that control power supply of an appliance</li><li>SWITCH: Switches that control household power sockets</li><li>THERMOSTAT: Thermostat type</li></ul>          | Yes    |
| `friendlyName`               | string        | The appliance name specified by the user                                                           | No    |
| `friendlyDescription`        | string        | A description of the appliance                                                                  | No    |
| `isReachable`                | boolean       | Whether remotely controllable or not <ul><li>true: Remotely controllable</li><li>false: Remotely uncontrollable</li></ul> | No    |
| `manufacturerName`           | string        | The name of the appliance manufacturer                                                                  | No    |
| `modelName`                  | string        | The name of the appliance model                                                                   | No    |
| `version`                    | string        | The version of the manufacturer software                                                            | No    |

### Remarks
When your Clova Home extension receives a [`DiscoverAppliancesRequest`](/CEK/References/ClovaHomeInterface/Discovery_Interfaces.md#DiscoverAppliancesRequest) message, you must return a list of appliances by filling in all fields except for `additionalApplianceDetails`. Allowed `actions` are determined by `applianceTypes`. Available values for each `applianceTypes` are as follows.

| applianceTypes | Allowed actions                                |
|----------------|-----------------------------------------------|
| `AIRCONDITIONER` | <ul><li>DecrementTargetTemperature</li><li>HealthCheck</li><li>IncrementTargetTemperature</li><li>TurnOff</li><li>TurnOn</li></ul> |
| `AIRPURIFIER`    | <ul><li>DecrementFanSpeed</li><li>HealthCheck</li><li>IncrementFanSpeed</li><li>TurnOff</li><li>TurnOn</li></ul>                   |
| `HUMIDFIER`      | <ul><li>HealthCheck</li><li>TurnOff</li><li>TurnOn</li></ul> |
| `LIGHT`          | <ul><li>HealthCheck</li><li>TurnOff</li><li>TurnOn</li></ul> |
| `SETTOPBOX`      | <ul><li>DecrementVolume</li><li>HealthCheck</li><li>IncrementVolume</li><li>SetChannel</li><li>TurnOff</li><li>TurnOn</li></ul> |
| `SMARTPLUG`      | <ul><li>HealthCheck</li><li>TurnOff</li><li>TurnOn</li></ul> |
| `SWITCH`         | <ul><li>HealthCheck</li><li>TurnOff</li><li>TurnOn</li></ul> |
| `THERMOSTAT`     | <ul><li>HealthCheck</li><li>SetMode</li><li>TurnOff</li><li>TurnOn</li></ul> |

<div class="note">
<p><strong>Note!</strong></p>
<p>If an actual appliance supports fewer features than those allowed by applianceTypes, you can limit it to use less actions. For example, if your user registered an air purifier (`AIRPURIFIER` type) that does not have a feature to adjust fan speeds, exclude IncrementFanSpeed and DecrementFanSpeed from the allowed actions when returning DiscoverAppliancesResponse messages.</p>
</div>

This table lists the [interfaces](/CEK/References/CEK_API.md#ClovaHomeExtInterface) related to each actions.

| actions                    | Related interfaces                            |
|----------------------------|------------------------------------------|
| `DecrementFanSpeed`          | [`DecrementFanSpeedConfirmation`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#DecrementFanSpeedConfirmation), [`DecrementFanSpeedRequest`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#DecrementFanSpeedRequest) |
| `DecrementTargetTemperature` | [`DecrementTargetTemperatureConfirmation`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#DecrementTargetTemperatureConfirmation), [`DecrementTargetTemperatureRequest`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#DecrementTargetTemperatureRequest) |
| `DecrementVolume`            | [`DecrementVolumeConfirmation`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#DecrementVolumeConfirmation), [`DecrementVolumeRequest`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#DecrementVolumeRequest) |
| `HealthCheck`                | [`HealthCheckRequest`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#HealthCheckRequest), [`HealthCheckResponse`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#HealthCheckResponse) |
| `IncrementFanSpeed`          | [`IncrementFanSpeedConfirmation`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#IncrementFanSpeedConfirmation), [`IncrementFanSpeedRequest`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#IncrementFanSpeedRequest) |
| `IncrementTargetTemperature` | [`IncrementTargetTemperatureConfirmation`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#IncrementTargetTemperatureConfirmation), [`IncrementTargetTemperatureRequest`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#IncrementTargetTemperatureConfirmation) |
| `IncrementVolume`            | [`IncrementVolumeConfirmation`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#IncrementVolumeConfirmation), [`IncrementVolumeRequest`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#IncrementVolumeRequest) |
| `SetChannel`                 | [`SetChannelConfirmation`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#SetChannelConfirmation), [`SetChannelRequest`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#SetChannelRequest) |
| `SetMode`                    | [`SetModeConfirmation`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#SetModeConfirmation), [`SetModeRequest`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#SetModeRequest) |
| `TurnOff`                    | [`TurnOffConfirmation`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#TurnOffConfirmation), [`TurnOffRequest`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#TurnOffRequest) |
| `TurnOn`                     | [`TurnOnConfirmation`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#TurnOnConfirmation), [`TurnOnRequest`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#TurnOnRequest) |

#### Object Example
{% raw %}
```json
// Example 1: DiscoverAppliancesResponse message
{
  "header": {
    "messageId": "99f9d8ff-9366-4cab-a90c-b4c7eca0abbe",
    "name": "DiscoverAppliancesResponse",
    "namespace": "ClovaHome",
    "payloadVersion": "1.0"
  },
  "payload": {
    "discoveredAppliances": [
      {
        "applianceId": "device-001",
        "manufacturerName": "device-manufacturer-name",
        "modelName": "스마트 전등",
        "version": "v1.0",
        "friendlyName": "거실 전등",
        "friendlyDescription": "스마트폰으로 제어할 수 있는 전등",
        "isReachable": true,
          "actions": [
            "HealthCheckt",
            "TurnOn",
            "TurnOff"
        ],
        "applianceTypes": ["LIGHT"],
        "additionalApplianceDetails": {}
      },
      {
        "applianceId": "device-002",
        "manufacturerName": "device-manufacturer-name",
        "modelName": "스마트 플러그",
        "version": "v1.0",
        "friendlyName": "부엌 플러그",
        "friendlyDescription": "에너지를 절약하는 플러그",
        "isReachable": true,
        "actions": [
          "HealthCheckt",
          "TurnOn",
          "TurnOff"
        ],
        "applianceTypes": ["SMARTPLUG"],
        "additionalApplianceDetails": {}
      }
    ]
  }
}

// Example 2: TurnOnRequest message
{
  "header": {
    "messageId": "6c04fc2d-64dd-41a0-9162-7cb0d4cf7c08",
    "name": "TurnOnRequest",
    "namespace": "ClovaHome",
    "payloadVersion": "1.0"
  },
  "payload": {
    "accessToken": "92ebcb67fe33",
    "appliance": {
      "applianceId": "device-001"
    }
  }
}
```
{% endraw %}

#### See also
* [`DiscoverAppliancesResponse`](/CEK/References/ClovaHomeInterface/Discovery_Interfaces.md#DiscoverAppliancesResponse)
* [`DiscoverAppliancesRequest`](/CEK/References/ClovaHomeInterface/Discovery_Interfaces.md#DiscoverAppliancesRequest)

### HeatingModeObject {#HeatingModeObject}
An object containing a heating mode. It displays the name of the heating mode to change to or the heating mode before and after change. The value is expressed as a string.

#### Object field
| Field name       | Type    | Field description                     | Required |
|---------------|---------|-----------------------------|---------|
| `value`       | string  | A heating mode. <ul><li><code>"hotwater"</code>: Hot water mode</li><li><code>"away"</code>: Absence mode</li></ul>   | Yes     |

#### Object Example
{% raw %}
```json
// Example 1: SetModeRequest message
{
  "header": {
    "messageId": "33da6561-0149-4532-a30b-e0de8f75c4cf",
    "name": "SetModeRequest",
    "namespace": "ClovaHome",
    "payloadVersion": "1.0"
  },
  "payload": {
    "accessToken": "92ebcb67fe33",
    "appliance": {
        "applianceId": "device-006"
    },
    "mode": {
        "value": "hotwater"
    }
  }
}

// Example 2: SetModeConfirmation message
{
  "header": {
    "messageId": "4ec35000-88ce-4724-b7e4-7f52050558fd",
    "name": "SetModeConfirmation",
    "namespace": "ClovaHome",
    "payloadVersion": "1.0"
  },
  "payload": {
    "mode": {
      "value": "hotwater"
    }
  }
}
```
{% endraw %}

#### See also
* [`SetModeConfirmation`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#SetModeConfirmation)
* [`SetModeRequest`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#SetModeRequest)

### SpeedObject {#SpeedObject}
An object containing a speed. It displays an expected change in the value of a speed or a target speed before and after change. The value is expressed as an integer.

#### Object field
| Field name       | Type    | Field description                     | Required |
|---------------|---------|-----------------------------|---------|
| `value`       | number  | A speed value                       | Yes     |

#### Object Example
{% raw %}
```json
// Example 1: IncrementFanSpeedRequest message
{
  "header": {
    "messageId": "6c04fc2d-64dd-41a0-9162-7cb0d4cf7c08",
    "name": "IncrementFanSpeedRequest",
    "namespace": "ClovaHome",
    "payloadVersion": "1.0"
  },
  "payload": {
    "accessToken": "92ebcb67fe33",
    "appliance": {
      "applianceId": "device-004"
    },
    "deltaFanSpeed": {
      "value": 1
    }
  }
}

// Example 2: IncrementFanSpeedConfirmation message
{
  "header": {
    "messageId": "4ec35000-88ce-4724-b7e4-7f52050558fd",
    "name": "IncrementFanSpeedConfirmation",
    "namespace": "ClovaHome",
    "payloadVersion": "1.0"
  },
  "payload": {
    "targetFanSpeed": {
      "value": 3
    },
    "previousState": {
      "targetFanSpeed": {
        "value": 2
      }
    }
  }
}
```
{% endraw %}

#### See also
* [`DecrementFanSpeedConfirmation`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#DecrementFanSpeedConfirmation)
* [`DecrementFanSpeedRequest`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#DecrementFanSpeedRequest)
* [`IncrementFanSpeedConfirmation`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#IncrementFanSpeedConfirmation)
* [`IncrementFanSpeedRequest`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#IncrementFanSpeedRequest)

### TemperatureObject {#TemperatureObject}
An object containing a temperature. It displays an expected change in the value of a temperature or a target temperature before and after change. The value is expressed as the number of the first decimal point.

#### Object field
| Field name       | Type    | Field description                     | Required |
|---------------|---------|-----------------------------|---------|
| `value`       | number  | A temperature value                       | Yes     |

#### Object Example
{% raw %}
```json
// Example 1: IncrementTargetTemperatureRequest message
{
  "header": {
    "messageId": "6c04fc2d-64dd-41a0-9162-7cb0d4cf7c08",
    "name": "IncrementTargetTemperatureRequest",
    "namespace": "ClovaHome",
    "payloadVersion": "1.0"
  },
  "payload": {
    "accessToken": "92ebcb67fe33",
    "appliance": {
      "applianceId": "device-001"
    },
    "deltaTemperature": {
      "value": 1.0
    }
  }
}

// Example 2: IncrementTargetTemperatureConfirmation message
{
  "header": {
    "messageId": "4ec35000-88ce-4724-b7e4-7f52050558fd",
    "name": "IncrementTargetTemperatureConfirmation",
    "namespace": "ClovaHome",
    "payloadVersion": "1.0"
  },
  "payload": {
    "targetTemperature": {
      "value": 25.0
    },
    "previousState": {
      "targetTemperature": {
        "value": 21.0
      }
    }
  }
}
```
{% endraw %}

#### See also
* [`DecrementTargetTemperatureConfirmation`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#DecrementTargetTemperatureConfirmation)
* [`DecrementTargetTemperatureRequest`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#DecrementTargetTemperatureRequest)
* [`IncrementTargetTemperatureConfirmation`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#IncrementTargetTemperatureConfirmation)
* [`IncrementTargetTemperatureRequest`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#IncrementTargetTemperatureRequest)

### TVChannelObject {#TVChannelObject}
An object containing a TV channel. It displays a TV channel to change to or a TV channel before and after change. The value is expressed as a string.

#### Object field
| Field name       | Type    | Field description                     | Required |
|---------------|---------|-----------------------------|---------|
| `value`       | number  | A TV channel number                  | Yes     |

#### Object Example
{% raw %}
```json
// Example 1: SetChannelRequest message
{
  "header": {
    "messageId": "33da6561-0149-4532-a30b-e0de8f75c4cf",
    "name": "SetChannelRequest",
    "namespace": "ClovaHome",
    "payloadVersion": "1.0"
  },
  "payload": {
    "accessToken": "92ebcb67fe33",
    "appliance": {
        "applianceId": "device-007"
    },
    "channel": {
        "value": 13
    }
  }
}

// Example 2: SetChannelConfirmation message
{
  "header": {
    "messageId": "4ec35000-88ce-4724-b7e4-7f52050558fd",
    "name": "SetChannelConfirmation",
    "namespace": "ClovaHome",
    "payloadVersion": "1.0"
  },
  "payload": {
    "channel": {
      "value": 13
    }
  }
}
```
{% endraw %}

#### See also
* [`SetChannelConfirmation`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#SetChannelConfirmation)
* [`SetChannelRequest`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#SetChannelRequest)

### VolumeObject {#VolumeObject}
An object containing a speaker volume. It displays an expected change in the value of a volume or a volume before and after change. The value is expressed as an integer.

#### Object field
| Field name       | Type    | Field description                     | Required |
|---------------|---------|-----------------------------|---------|
| `value`       | number  | A volume value                       | Yes     |

#### Object Example
{% raw %}
```json
// Example 1: IncrementVolumeRequest message
{
  "header": {
    "messageId": "6c04fc2d-64dd-41a0-9162-7cb0d4cf7c08",
    "name": "IncrementVolumeRequest",
    "namespace": "ClovaHome",
    "payloadVersion": "1.0"
  },
  "payload": {
    "accessToken": "92ebcb67fe33",
    "appliance": {
      "applianceId": "device-005"
    },
    "deltaVolume": {
      "value": 10
    }
  }
}

// Example 2: IncrementVolumeConfirmation message
{
  "header": {
    "messageId": "4ec35000-88ce-4724-b7e4-7f52050558fd",
    "name": "IncrementVolumeConfirmation",
    "namespace": "ClovaHome",
    "payloadVersion": "1.0"
  },
  "payload": {
    "targetVolume": {
      "value": 20
    },
    "previousState": {
      "targetVolume": {
        "value": 10
      }
    }
  }
}
```
{% endraw %}

#### See also
* [`DecrementVolumeConfirmation`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#DecrementVolumeConfirmation)
* [`DecrementVolumeRequest`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#DecrementVolumeRequest)
* [`IncrementVolumeConfirmation`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#IncrementVolumeConfirmation)
* [`IncrementVolumeRequest`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#IncrementVolumeRequest)
