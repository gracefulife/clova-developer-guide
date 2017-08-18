## Shared objects {#SharedObjects}
When sending messages using the Clova Home API, the following shared objects are included in a message body (payload).

| Object name  | Object description  |
|--------------------|---------------------------------------------------|
| [ApplianceObject](#ApplianceObject)  | An object containing information of an IoT appliance  |
| [HeatingModeObject](#HeatingModeObject) | An object containing heating mode information  |
| [SpeedObject](#SpeedObject)  | An object containing speed information  |
| [TemperatureObject](#TemperatureObject) | An object containing temperature information  |
| [TVChannelObject](#TVChannelObject)  | An object containing TV channel information  |
| [VolumeObject](#VolumeObject)  | An object containing volume information  |

### ApplianceObject {#ApplianceObject}
An object that contains information of an IoT appliance. This object is used when returning CEK a list of appliances registered to a user account or when requesting a Clova Home extension to control a specified appliance.

#### Object field
| Field name  | Type  | Field description  | Required |
|---------------|---------|-----------------------------|---------|
| `actions[]`  | string array  | A list of actions supported by the appliance. You must limit the allowed actions to those supported by the appliance. | No  |
| `additionalApplianceDetails` | object  | A field containing additional details of the appliance provided from a manufacturer or IoT service  | No  |
| `applianceId`  | string  | The appliance ID  | Yes  |
| `applianceTypes[]`  | string array  | The appliance type. `applicationType` determines allowed actions you can specify in the `actions` field. For the appliances registered to the IoT service's user account, specify their type as one of the following values.<ul><li>AIRCONDITIONER: Air conditioning or heating system type</li><li>AIRPURIFIER: Air purifier type</li><li>HUMIDIFIER: Humidifier type</li><li>LIGHT: Lighting appliance type</li><li>SETTOPBOX: TV set-top box type</li><li>SMARTPLUG: Plugs that control power supply of an appliance</li><li>SWITCH: Switches that control household power sockets</li><li>THERMOSTAT: Thermostat type</li></ul>  | Yes  |
| `friendlyName`  | string  | The appliance name specified by a user  | No  |
| `friendlyDescription`  | string  | A description of the appliance  | No  |
| `isReachable`  | boolean  | Whether remotely controllable or not <ul><li>true: Remotely controllable</li><li>false: Remotely uncontrollable</li></ul> | No  |
| `manufacturerName`  | string  | The name of the appliance manufacturer  | No  |
| `modelName`  | string  | The name of the appliance model  | No  |
| `version`  | string  | The software version of the manufacturer  | No  |

### Remarks
When your Clova Home extension receives a [`DiscoverAppliancesRequest`](#DiscoverAppliancesRequest) message, you must return a list of appliances by filling in all fields except for `additionalApplianceDetails`. Available values for the `actions` field are determined by the `applianceTypes` field. Available values are as follows for each `applianceTypes` value.

| applianceTypes | Allowed actions  |
|----------------|-----------------------------------------------|
| **AIRCONDITIONER** | <ul><li>DecrementTargetTemperature</li><li>HealthCheck</li><li>IncrementTargetTemperature</li><li>TurnOff</li><li>TurnOn</li></ul> |
| **AIRPURIFIER**  | <ul><li>DecrementFanSpeed</li><li>HealthCheck</li><li>IncrementFanSpeed</li><li>TurnOff</li><li>TurnOn</li></ul>  |
| **HUMIDFIER**  | <ul><li>HealthCheck</li><li>TurnOff</li><li>TurnOn</li></ul> |
| **LIGHT**  | <ul><li>HealthCheck</li><li>TurnOff</li><li>TurnOn</li></ul> |
| **SETTOPBOX**  | <ul><li>DecrementVolume</li><li>HealthCheck</li><li>IncrementVolume</li><li>SetChannel</li><li>TurnOff</li><li>TurnOn</li></ul> |
| **SMARTPLUG**  | <ul><li>HealthCheck</li><li>TurnOff</li><li>TurnOn</li></ul> |
| **SWITCH**  | <ul><li>HealthCheck</li><li>TurnOff</li><li>TurnOn</li></ul> |
| **THERMOSTAT**  | <ul><li>HealthCheck</li><li>SetMode</li><li>TurnOff</li><li>TurnOn</li></ul> |

<div class="note">
<p><strong>Note!</strong></p>
<p>If the actual appliance supports fewer features than those allowed by applianceTypes, you can limit it to use less actions. For example, if your user registered an air purifier (`AIRPURIFIER` type) that does not have a feature to adjust fan speeds, exclude IncrementFanSpeed and DecrementFanSpeed from the allowed actions when returning a DiscoverAppliancesResponse message.</p>
</div>

This table lists the Clova Home APIs related to actions.

| actions  | Related Clova Home API  |
|----------------------------|------------------------------------------|
| **DecrementFanSpeed**  | [`DecrementFanSpeedConfirmation`](#DecrementFanSpeedConfirmation), [`DecrementFanSpeedRequest`](#DecrementFanSpeedRequest) |
| **DecrementTargetTemperature** | [`DecrementTargetTemperatureConfirmation`](#DecrementTargetTemperatureConfirmation), [`DecrementTargetTemperatureRequest`](#DecrementTargetTemperatureRequest) |
| **DecrementVolume**  | [`DecrementVolumeConfirmation`](#DecrementVolumeConfirmation), [`DecrementVolumeRequest`](#DecrementVolumeRequest) |
| **HealthCheck**  | [`HealthCheckRequest`](#HealthCheckRequest), [`HealthCheckResponse`](#HealthCheckResponse) |
| **IncrementFanSpeed**  | [`IncrementFanSpeedConfirmation`](#IncrementFanSpeedConfirmation), [`IncrementFanSpeedRequest`](#IncrementFanSpeedRequest) |
| **IncrementTargetTemperature** | [`IncrementTargetTemperatureConfirmation`](#IncrementTargetTemperatureConfirmation), [`IncrementTargetTemperatureRequest`](#IncrementTargetTemperatureConfirmation) |
| **IncrementVolume**  | [`IncrementVolumeConfirmation`](#IncrementVolumeConfirmation), [`IncrementVolumeRequest`](#IncrementVolumeRequest) |
| **SetChannel**  | [`SetChannelConfirmation`](#SetChannelConfirmation), [`SetChannelRequest`](#SetChannelRequest) |
| **SetMode**  | [`SetModeConfirmation`](#SetModeConfirmation), [`SetModeRequest`](#SetModeRequest) |
| **TurnOff**  | [`TurnOffConfirmation`](#TurnOffConfirmation), [`TurnOffRequest`](#TurnOffRequest) |
| **TurnOn**  | [`TurnOnConfirmation`](#TurnOnConfirmation), [`TurnOnRequest`](#TurnOnRequest) |

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
* [`DiscoverAppliancesResponse`](DiscoverAppliancesResponse)
* [`DiscoverAppliancesRequest`](#DiscoverAppliancesRequest)

### HeatingModeObject {#HeatingModeObject}
An object that contains heating mode information. It displays the name of the heating mode to change to or the heating mode before and after change. It is expressed as strings.

#### Object field
| Field name  | Type  | Field description  | Required |
|---------------|---------|-----------------------------|---------|
| `value`  | string  | A heating mode. <ul><li><strong>"hotwater"</strong>: Hot water mode</li><li><strong>"away"</strong>: Absence mode</li></ul>  | Yes  |

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
* [`SetModeConfirmation`](#SetModeConfirmation)
* [`SetModeRequest`](#SetModeRequest)

### SpeedObject {#SpeedObject}
An object that contains speed information. It displays an expected change in the value of a speed or a target speed before and after change. It is is expressed as integers.

#### Object field
| Field name  | Type  | Field description  | Required |
|---------------|---------|-----------------------------|---------|
| `value`  | number  | Speed value  | Yes  |

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
* [`DecrementFanSpeedConfirmation`](#DecrementFanSpeedConfirmation)
* [`DecrementFanSpeedRequest`](#DecrementFanSpeedRequest)
* [`IncrementFanSpeedConfirmation`](#IncrementFanSpeedConfirmation)
* [`IncrementFanSpeedRequest`](#IncrementFanSpeedRequest)

### TemperatureObject {#TemperatureObject}
An object that contains temperature information. It displays an expected change in the value of a temperature or a target temperature before and after change. It is expressed to one decimal point.

#### Object field
| Field name  | Type  | Field description  | Required |
|---------------|---------|-----------------------------|---------|
| `value`  | number  | Temperature value  | Yes  |

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
* [`DecrementTargetTemperatureConfirmation`](#DecrementTargetTemperatureConfirmation)
* [`DecrementTargetTemperatureRequest`](#DecrementTargetTemperatureRequest)
* [`IncrementTargetTemperatureConfirmation`](#IncrementTargetTemperatureConfirmation)
* [`IncrementTargetTemperatureRequest`](#IncrementTargetTemperatureRequest)

### TVChannelObject {#TVChannelObject}
An object that contains TV channel information. It displays the TV channel to change to or a TV channel before and after change. It is expressed in strings.

#### Object field
| Field name  | Type  | Field description  | Required |
|---------------|---------|-----------------------------|---------|
| `value`  | number  | TV channel number  | Yes  |

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
* [`SetChannelConfirmation`](#SetChannelConfirmation)
* [`SetChannelRequest`](#SetChannelRequest)

### VolumeObject {#VolumeObject}
An object that contains speaker volume information. It displays an expected change in the value of the volume or a volume before and after change. It is expressed as integers.

#### Object field
| Field name  | Type  | Field description  | Required |
|---------------|---------|-----------------------------|---------|
| `value`  | number  | Volume value  | Yes  |

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
* [`DecrementVolumeConfirmation`](#DecrementVolumeConfirmation)
* [`DecrementVolumeRequest`](#DecrementVolumeRequest)
* [`IncrementVolumeConfirmation`](#IncrementVolumeConfirmation)
* [`IncrementVolumeRequest`](#IncrementVolumeRequest)
