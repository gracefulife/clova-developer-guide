## Shared objects {#SharedObjects}
When you send [Clova Home extension messages](/CEK/References/CEK_API.md#ClovaHomeExtMessage), the following shared objects are included in a message body (payload).

| Object name            | Object description                                            |
|--------------------|---------------------------------------------------|
| [AirQualityObject](#AirQualityObject)       | An object containing an air quality            |
| [ApplianceObject](#ApplianceObject)         | An object containing details of an IoT appliance        |
| [BatteryInfoObject](#BatteryInfoObject)       | An object containing details of a battery            |
| [BrightnessObject](#BrightnessObject)       | An object containing details of brightness        |
| [FineDustObject](#FineDustObject)           | An object containing data on fine dust concentrations level      |
| [HeatingModeObject](#HeatingModeObject)     | An object containing a heating mode          |
| [HumidityObject](#HumidityObject)           | An object containing humidity              |
| [SpeedObject](#SpeedObject)                 | An object containing a speed              |
| [TemperatureObject](#TemperatureObject)     | An object containing a temperature.          |
| [TVChannelNameObject](#TVChannelNameObject) | An object containing detail of the name of TV channel      |
| [TVChannelObject](#TVChannelObject)         | An object containing a TV channel           |
| [UltraFineDustObject](#UltraFineDustObject) | An object containing data on ultra fine dust concentrations level     |
| [VolumeObject](#VolumeObject)               | An object containing a volume          |

### AirQualityObject {#AirQualityObject}
An object containing an air quality. It is applied to show the air quality measured by the appliance. It is expressed in string.

#### Object field
| Field name       | Type    | Field description                     | Required |
|---------------|---------|-----------------------------|---------|
| `index`       | string  | Air quality index                    | Yes     |

#### Object Example
{% raw %}

```json
// Example : GetAirQualityResponse message
{
  "header": {
    "messageId": "33da6561-0149-4532-a30b-e0de8f75c4cf",
    "name": "GetAirQualityResponse",
    "namespace": "ClovaHome",
    "payloadVersion": "1.0"
  },
  "payload": {
    "airQuality": {
        "index": "보통"
    }
  }
}
```

{% endraw %}

#### See also
* [`GetAirQualityRequest`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#GetAirQualityRequest)
* [`GetAirQualityResponse`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#GetAirQualityResponse)

### ApplianceObject {#ApplianceObject}
An object containing details of an IoT appliance. This object is used when returning CEK a list of appliances registered on a user account or when requesting a Clova Home extension to control a specified appliance.

#### Object field
| Field name       | Type    | Field description                     | Required |
|---------------|---------|-----------------------------|---------|
| `actions[]`                  | string array  | A list of actions supported by the appliance. You must limit the allowed actions to those supported by the appliance. | No    |
| `additionalApplianceDetails` | object        | A field containing additional details of the appliance provided from the manufacturer or IoT service                                 | No    |
| `applianceId`                | string        | The appliance ID                                                                        | Yes    |
| `applianceTypes[]`           | string array  | The appliance type. `applicationType` determines allowed actions you can specify in the `actions` field. Specify the type as one of the following values for the appliances registered on the user's IoT service account.<ul><li>AIRCONDITIONER: Air conditioning or heating system type</li><li>AIRPURIFIER: Air purifier type</li><li>HUMIDIFIER: Humidifier type</li><li>LIGHT: Lighting appliance type</li><li>SETTOPBOX: TV set-top box type</li><li>SMARTPLUG: Plugs that control power supply of an appliance</li><li>SWITCH: Switches that control household power sockets</li><li>THERMOSTAT: Thermostat type</li></ul>          | Yes    |
| `friendlyName`               | string        | The appliance name specified by the user                                                           | No    |
| `friendlyDescription`        | string        | A description of the appliance                                                                  | No    |
| `isReachable`                | boolean       | Whether remotely controllable or not <ul><li>true: Remotely controllable</li><li>false: Remotely uncontrollable</li></ul> | No    |
| `manufacturerName`           | string        | The name of the appliance manufacturer                                                                  | No    |
| `modelName`                  | string        | The name of the appliance model                                                                   | No    |
| `version`                    | string        | The version of the manufacturer software                                                            | No    |
| `location`                   | string        | The place where the appliance is installed                                                                 | No    |

### Remarks
When your Clova Home extension receives a [`DiscoverAppliancesRequest`](/CEK/References/ClovaHomeInterface/Discovery_Interfaces.md#DiscoverAppliancesRequest) message, you must return a list of appliances by filling in all fields except for `additionalApplianceDetails`. Allowed `actions` are determined by `applianceTypes`. Available values for each `applianceTypes` are as follows.

| applianceTypes | Allowed actions                                |
|----------------|-----------------------------------------------|
| `AIRCONDITIONER` | DecrementTargetTemperature, GetTargetTemperature, HealthCheck, IncrementTargetTemperature, SetTargetTemperature, TurnOff, TurnOn               |
| `AIRPURIFIER`    | DecrementFanSpeed, GetAirQuality, GetFineDust, GetUltraFineDust, HealthCheck, IncrementFanSpeed, SetFanSpeed, TurnOff, TurnOn                  |
| `AIRSENSOR`      | GetAirQuality, GetFineDust, GetHumidity, GetUltraFineDust, GetTargetTemperature, HealthCheck                                                   |
| `DEHUMIDIFIER`   | GetHumidity, HealthCheck, SetFanSpeed, TurnOff, TurnOn                                                                                         |
| `HUMIDFIER`      | GetHumidity, HealthCheck, TurnOff, TurnOn                                                                                                      |
| `LIGHT`          | DecrementBrightness, HealthCheck, IncrementBrightness, SetBrightness, TurnOff, TurnOn                                                          |
| `ROBOTVACUUM`    | Charge, GetBatteryInfo, HealthCheck, TurnOff, TurnOn                                                                                           |
| `SETTOPBOX`      | DecrementChannel, DecrementVolume, HealthCheck, IncrementChannel, IncrementVolume, Mute, SetChannel, SetChannelByName, TurnOff, TurnOn, Unmute |
| `SMARTHUB`       | GetHumidity, GetTargetTemperature, HealthCheck, SetMode                                                                                        |
| `SMARTPLUG`      | HealthCheck, TurnOff, TurnOn                                                                                                                   |
| `SMARTTV`        | DecrementChannel, DecrementVolume, HealthCheck, IncrementChannel, IncrementVolume, Mute, SetChannel, SetChannelByName, TurnOff, TurnOn, Unmute |
| `SMARTVALVE`     | GetLockState, SetLockState                                                 |
| `SWITCH`         | HealthCheck, TurnOff, TurnOn                                                                                                                   |
| `THERMOSTAT`     | HealthCheck, SetMode, TurnOff, TurnOn                                                                                                          |

<div class="note">
<p><strong>Note!</strong></p>
<p>If an actual appliance supports fewer features than those allowed by applianceTypes, you can limit it to use less actions. For example, if your user registered an air purifier (<code>AIRPURIFIER</code> type) that does not have a feature to adjust fan speeds, exclude IncrementFanSpeed and DecrementFanSpeed from the allowed actions when returning DiscoverAppliancesResponse messages.</p>
</div>

This table lists the [interfaces](/CEK/References/CEK_API.md#ClovaHomeExtInterface) related to each actions.

| actions                    | Related interfaces                            |
|----------------------------|------------------------------------------|
| `Charge`                     | [`ChargeConfirmation`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#ChargeConfirmation), [`ChargeRequest`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#ChargeRequest) |
| `DecrementBrightness`        | [`DecrementBrightnessConfirmation`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#DecrementBrightnessConfirmation), [`DecrementBrightnessRequest`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#DecrementBrightnessRequest) |
| `DecrementChannel`           | [`DecrementChannelConfirmation`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#DecrementChannelConfirmation), [`DecrementChannelRequest`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#DecrementChannelRequest) |
| `DecrementFanSpeed`          | [`DecrementFanSpeedConfirmation`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#DecrementFanSpeedConfirmation), [`DecrementFanSpeedRequest`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#DecrementFanSpeedRequest) |
| `DecrementTargetTemperature` | [`DecrementTargetTemperatureConfirmation`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#DecrementTargetTemperatureConfirmation), [`DecrementTargetTemperatureRequest`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#DecrementTargetTemperatureRequest) |
| `DecrementVolume`            | [`DecrementVolumeConfirmation`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#DecrementVolumeConfirmation), [`DecrementVolumeRequest`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#DecrementVolumeRequest) |
| `GetAirQuality`              | [`GetAirQualityRequest`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#GetAirQualityRequest), [`GetAirQualityResponse`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#GetAirQualityResponse) |
| `GetBatteryInfo`              | [`GetBatteryInfoRequest`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#GetBatteryInfoRequest), [`GetBatteryInfoResponse`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#GetBatteryInfoResponse) |
| `GetFineDust`                | [`GetFineDustRequest`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#GetFineDustRequest), [`GetFineDustResponse`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#GetFineDustResponse) |
| `GetHumidity`                | [`GetHumidityRequest`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#GetHumidityRequest), [`GetHumidityResponse`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#GetHumidityResponse) |
| `GetLockState`               | [`GetLockStateRequest`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#GetLockStateRequest), [`GetLockStateResponse`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#GetLockStateResponse) |
| `GetTargetTemperature`       | [`GetTargetTemperatureRequest`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#GetTargetTemperatureRequest), [`GetTargetTemperatureResponse`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#GetTargetTemperatureResponse) |
| `GetUltraFineDust`           | [`GetUltraFineDustRequest`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#GetUltraFineDustRequest), [`GetUltraFineDustResponse`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#GetUltraFineDustResponse) |
| `HealthCheck`                | [`HealthCheckRequest`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#HealthCheckRequest), [`HealthCheckResponse`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#HealthCheckResponse) |
| `IncrementBrightness`        | [`IncrementBrightnessConfirmation`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#IncrementBrightnessConfirmation), [`IncrementBrightnessRequest`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#IncrementBrightnessRequest)  |
| `IncrementChannel`           | [`IncrementChannelConfirmation`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#IncrementChannelConfirmation), [`IncrementChannelRequest`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#IncrementChannelRequest) |
| `IncrementFanSpeed`          | [`IncrementFanSpeedConfirmation`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#IncrementFanSpeedConfirmation), [`IncrementFanSpeedRequest`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#IncrementFanSpeedRequest) |
| `IncrementTargetTemperature` | [`IncrementTargetTemperatureConfirmation`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#IncrementTargetTemperatureConfirmation), [`IncrementTargetTemperatureRequest`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#IncrementTargetTemperatureConfirmation) |
| `IncrementVolume`            | [`IncrementVolumeConfirmation`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#IncrementVolumeConfirmation), [`IncrementVolumeRequest`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#IncrementVolumeRequest) |
| `Mute`                       | [`MuteConfirmation`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#MuteConfirmation), [`MuteRequest`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#MuteRequest) |
| `SetBrightness`              | [`SetBrightnessConfirmation`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#SetBrightnessConfirmation), [`SetBrightnessRequest`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#SetBrightnessRequest)  |
| `SetChannel`                 | [`SetChannelConfirmation`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#SetChannelConfirmation), [`SetChannelRequest`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#SetChannelRequest) |
| `SetChannelByName`           | [`SetChannelByNameConfirmation`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#SetChannelByNameConfirmation), [`SetChannelByNameRequest`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#SetChannelByNameRequest) |
| `SetMode`                    | [`SetModeConfirmation`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#SetModeConfirmation), [`SetModeRequest`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#SetModeRequest) |
| `SetFanSpeed`                | [`SetFanSpeedConfirmation`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#SetFanSpeedConfirmation), [`SetFanSpeedRequest`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#SetFanSpeedRequest)  |
| `SetLockState`               | [`SetLockStateConfirmation`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#SetLockStateConfirmation), [`SetLockStateRequest`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#SetLockStateRequest)  |
| `SetTargetTemperature`       | [`SetTargetTemperatureConfirmation`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#SetTargetTemperatureConfirmation), [`SetTargetTemperatureRequest`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#SetTargetTemperatureConfirmation)  |
| `TurnOff`                    | [`TurnOffConfirmation`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#TurnOffConfirmation), [`TurnOffRequest`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#TurnOffRequest) |
| `TurnOn`                     | [`TurnOnConfirmation`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#TurnOnConfirmation), [`TurnOnRequest`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#TurnOnRequest) |
| `Unmute`                     | [`UnmuteConfirmation`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#UnmuteConfirmation), [`UnmuteRequest`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#UnmuteRequest) |

<div class="note">
<p><strong>Note!</strong></p>
<p>When passing a list of IoT appliances registered on a user via [`DiscoveryAppAppliancesResponse`](/CEK/References/ClovaHomeInterface/Discovery_Interfaces.md#DiscoverAppliancesResponse) message, return the location of each appliance using `location` field to CEK. If then, user’s IoT appliance location setting will be done automatically.</p>
</div>

The following table shows location details supported from `location` field. The details are used to analyze user's speech or to reveal the appliance to the user.

| `location` field value |    Location details       |
|------------------|------------------|
| `ATTIC`                     | Attic   |
| `BALCONY`                   | Balcony  |
| `BALCONY_IN_LIVING_ROOM`    | Balcony in living room  |
| `BALCONY_IN_MAIN_ROOM`      | Balcony in master bedroom  |
| `BALCONY_KITCHEN`           | Balcony in kitchen  |
| `BATH_ROOM`                 | Bathroom  |
| `BATH_ROOM_IN_LIVING_ROOM`  | Bathroom in living room |
| `BATH_ROOM_IN_MAIN_ROOM`    | Bathroom in master bedroom |
| `BED_ROOM`                  | Bedroom |
| `BIG_BATH_ROOM`             | Bathroom  |
| `BIG_CHILD_ROOM`            | Older child's room  |
| `BIG_ROOM`                  | Large room  |
| `BOILER_ROOM`               | Boiler room |
| `DINING_ROOM`               | Dining room|
| `DRESS_ROOM`                | Dress room |
| `ENTERANCE`                 | Entrance |
| `FAMILY_ROOM`               | Family room  |
| `FATHER_ROOM`               | Father's room |
| `FIFTH_ROOM`                | Fifth room  |
| `FIRST_ROOM`                | First room |
| `FOURTH_ROOM`               | Fourth room |
| `HALLWAY`                   | Hallway |
| `KITCHEN`                   | Kitchen |
| `LIBRARY`                   | Library |
| `LIVING_ROOM`               | Living room|
| `MAIN_GATE`                 | Main gate |
| `MAIN_ROOM`                 | Master bedroom |
| `MOTHER_ROOM`               | Mother's room |
| `MY_ROOM`                   | My room  |
| `PARENTS_ROOM`              | Parents' room  |
| `PLAY_ROOM`                 | Play room  |
| `POWDER_ROOM`               | Powder room |
| `ROOM`                      | Room  |
| `SECOND_ROOM`               | Second room |
| `SMALL_CHILD_ROOM`          | Younger child's room |
| `SMALL_LIVING_ROOM`         | Small living room  |
| `SMALL_ROOM`                | Small room |
| `SMALL_KITCHEN`             | Small kitchen  |
| `SMALL_BATH_ROOM`           | Toilet |
| `STAIRS`                    | Stairs |
| `THIRD_ROOM`                | Third room |
| `UPSTAIRS_ROOM`             | Upstairs room|
| `UTILITY_ROOM`              | Utility room |
| `WAREHOUSE`                 | Warehouse |
| `YARD`                      | Yard |

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
        "additionalApplianceDetails": {},
        "location": "LIVING_ROOM"
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
        "additionalApplianceDetails": {},
        "location": ""
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

### BrightnessObject {#BrightnessObject}
An object containing details of brightness. It is used to define brightness of a light or the brightness before or after any change. The value is expressed as an integer (0~100), meaning a percentage.

#### Object field
| Field name       | Type    | Field description                     | Required |
|---------------|---------|-----------------------------|---------|
| `value`       | number  | brightness (%)                      | Yes     |

#### Object Example
{% raw %}

```json
// Example 1: IncrementBrightnessRequest message
{
  "header": {
    "messageId": "6c04fc2d-64dd-41a0-9162-7cb0d4cf7c08",
    "name": "IncrementBrightnessRequest",
    "namespace": "ClovaHome",
    "payloadVersion": "1.0"
  },
  "payload": {
    "accessToken": "92ebcb67fe33",
    "appliance": {
      "applianceId": "device-010"
    },
    "deltaBrightness": {
      "value": 40
    }
  }
}

// Example 2 : IncrementBrightnessConfirmation message
{
  "header": {
    "messageId": "4ec35000-88ce-4724-b7e4-7f52050558fd",
    "name": "DecrementBrightnessConfirmation",
    "namespace": "ClovaHome",
    "payloadVersion": "1.0"
  },
  "payload": {
    "targetBrightness": {
      "value": 40
    },
    "previousState": {
      "targetBrightness": {
        "value": 20
      }
    }
  }
}
```

{% endraw %}

#### See also
* [`DecrementBrightnessConfirmation`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#DecrementBrightnessConfirmation)
* [`DecrementBrightnessRequest`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#DecrementBrightnessRequest)
* [`IncrementBrightnessConfirmation`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#IncrementBrightnessConfirmation)
* [`IncrementBrightnessRequest`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#IncrementBrightnessRequest)
* [`SetBrightnessConfirmation`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#SetBrightnessConfirmation)
* [`SetBrightnessRequest`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#SetBrightnessRequest)

### BatteryInfoObject {#BatteryInfoObject}
An object containing battery info of the appliance. It is applied when the battery info is requested. The value is expressed as an integer (0~100), meaning a percentage.

#### Object field
| Field name       | Type    | Field description                     | Required |
|---------------|---------|-----------------------------|---------|
| `value`       | number  | remaining battery (%)                      | Yes     |

#### Object Example
{% raw %}

```json
// Example 1 : GetBatteryInfoRequest message
{
  "header": {
    "messageId": "6c04fc2d-64dd-41a0-9162-7cb0d4cf7c08",
    "name": "GetBatteryInfoRequest",
    "namespace": "ClovaHome",
    "payloadVersion": "1.0"
  },
  "payload": {
    "accessToken": "92ebcb67fe33",
    "appliance": {
      "applianceId": "device-010"
    }
  }
}

// Example 2 : GetBatteryInfoResponse message
{
  "header": {
    "messageId": "4ec35000-88ce-4724-b7e4-7f52050558fd",
    "name": "GetBatteryInfoResponse",
    "namespace": "ClovaHome",
    "payloadVersion": "1.0"
  },
  "payload": {
    "batteryInfo": {
      "value": 40
    }
  }
}
```

{% endraw %}

#### See also
* [`GetBatteryInfoRequest`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#GetBatteryInfoRequest)
* [`GetBatteryInfoResponse`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#GetBatteryInfoResponse)

### FineDustObject {#FineDustObject}
An object containing data on fine dust. It is used to define the fine dust concentration level measured by the appliance. The value is expressed as a number.

#### Object field
| Field name       | Type    | Field description                     | Required |
|---------------|---------|-----------------------------|---------|
| `value`       | number  | Fine dust index                  | Yes     |
| `index`       | string  | Fine dust concentration level                  | Yes     |

#### Object Example
{% raw %}

```json
// Example : GetFineDustResponse message
{
  "header": {
    "messageId": "33da6561-0149-4532-a30b-e0de8f75c4cf",
    "name": "GetFineDustResponse",
    "namespace": "ClovaHome",
    "payloadVersion": "1.0"
  },
  "payload": {
    "fineDust": {
        "value": 77,
        "index": "보통"
    }
  }
}
```

{% endraw %}

#### See also
* [`GetFineDustRequest`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#GetFineDustRequest)
* [`GetFineDustResponse`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#GetFineDustResponse)

### HeatingModeObject {#HeatingModeObject}
An object containing a heating mode. It is used to define the name of the heating mode to change to or the heating mode before and after change. The value is expressed as a string.

#### Object field
| Field name       | Type    | Field description                     | Required |
|---------------|---------|-----------------------------|---------|
| `value`       | string  | A heating mode. <ul><li><code>"hotwater"</code>: Hot water mode</li><li><code>"away"</code>: Absence mode</li></ul>   | Yes     |

#### Object Example
{% raw %}

```json
// Example 1 : SetModeRequest message
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

// Example 2 : SetModeConfirmation message
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

### HumidityObject {#HumidityObject}
An object containing data humidity. It is used to define the humidity condition measured by the appliance. The value is expressed as a string.

#### Object field
| Field name       | Type    | Field description                     | Required |
|---------------|---------|-----------------------------|---------|
| `value`       | number  | humidity (%)                      | Yes     |

#### Object Example
{% raw %}

```json
// Example : GetHumidityResponse message
{
  "header": {
    "messageId": "33da6561-0149-4532-a30b-e0de8f75c4cf",
    "name": "GetHumidityResponse",
    "namespace": "ClovaHome",
    "payloadVersion": "1.0"
  },
  "payload": {
    "fineDust": {
        "value": 40
    }
  }
}
```

{% endraw %}

#### See also
* [`GetHumidityRequest`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#GetHumidityRequest)
* [`GetHumidityResponse`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#GetHumidityResponse)

### SpeedObject {#SpeedObject}
An object containing a speed. It is used to define an expected change in the value of a speed or a target speed before and after change. The value is expressed as an integer.

#### Object field
| Field name       | Type    | Field description                     | Required |
|---------------|---------|-----------------------------|---------|
| `value`       | number  | A speed value                       | Yes     |

#### Object Example
{% raw %}

```json
// Example 1 : IncrementFanSpeedRequest message
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

// Example 2 : IncrementFanSpeedConfirmation message
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
* [`SetFanSpeedConfirmation`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#SetFanSpeedConfirmation)
* [`SetFanSpeedRequest`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#SetFanSpeedRequest)

### TemperatureObject {#TemperatureObject}
An object containing a temperature. It is used to define an expected change in the value of a temperature or a target temperature before and after change or a setup target temperature. The value is expressed as the number of the first decimal point.

#### Object field
| Field name       | Type    | Field description                     | Required |
|---------------|---------|-----------------------------|---------|
| `value`       | number  | A temperature value                       | Yes     |

#### Object Example
{% raw %}

```json
// Example 1 : IncrementTargetTemperatureRequest message
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

// Example 2 : IncrementTargetTemperatureConfirmation message
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
* [`GetTargetTemperatureRequest`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#GetTargetTemperatureRequest)
* [`GetTargetTemperatureResponse`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#GetTargetTemperatureResponse)
* [`SetTargetTemperatureConfirmation`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#SetTargetTemperatureConfirmation)
* [`SetTargetTemperatureRequest`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#SetTargetTemperatureRequest)

### TVChannelNameObject {#TVChannelNameObject}
An object containing a name of TV channel. It is used to define a TV channel or a name of TV channel before and after change. The value is expressed as a string.

#### Object field
| Field name       | Type    | Field description                     | Required |
|---------------|---------|-----------------------------|---------|
| `value`       | string  | a name of TV channel                   | Yes     |

#### Object Example
{% raw %}

```json
// Example 1 : SetChannelByNameRequest message
{
  "header": {
    "messageId": "6c04fc2d-64dd-41a0-9162-7cb0d4cf7c08",
    "name": "SetChannelByNameRequest",
    "namespace": "ClovaHome",
    "payloadVersion": "1.0"
  },
  "payload": {
    "accessToken": "92ebcb67fe33",
    "appliance": {
      "applianceId": "device-006"
    },
    "channel": {
      "value": "sbs"
    }
  }
}

// Example 2 : SetChannelByNameConfirmation message
{
  "header": {
    "messageId": "4ec35000-88ce-4724-b7e4-7f52050558fd",
    "name": "SetChannelByNameConfirmation",
    "namespace": "ClovaHome",
    "payloadVersion": "1.0"
  },
  "payload": {
  	"channelName": {
  		"value": "sbs"
  	}
  }
}
```

{% endraw %}

#### See also
* [`SetChannelByNameConfirmation`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#SetChannelByNameConfirmation)
* [`SetChannelByNameRequest`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#SetChannelByNameRequest)

### TVChannelObject {#TVChannelObject}
An object containing a number of TV channel. It is used to define a TV channel or a number of TV channel before and after change. The value is expressed as a number.

#### Object field
| Field name       | Type    | Field description                     | Required |
|---------------|---------|-----------------------------|---------|
| `value`       | number  | A TV channel number                  | Yes     |

#### Object Example
{% raw %}

```json
// Example 1 : SetChannelRequest message
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

// Example 2 : SetChannelConfirmation message
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
* [`DecrementChannelConfirmation`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#DecrementChannelConfirmation)
* [`DecrementChannelRequest`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#DecrementChannelRequest)
* [`IncrementChannelConfirmation`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#IncrementChannelConfirmation)
* [`IncrementChannelRequest`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#IncrementChannelRequest)
* [`SetChannelConfirmation`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#SetChannelConfirmation)
* [`SetChannelRequest`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#SetChannelRequest)

### VolumeObject {#VolumeObject}
An object containing a speaker volume. It is used to define an expected change in the value of a volume or a volume before and after change. The value is expressed as an integer.

#### Object field
| Field name       | Type    | Field description                     | Required |
|---------------|---------|-----------------------------|---------|
| `value`       | number  | A volume value                       | Yes     |

#### Object Example
{% raw %}

```json
// Example 1 : IncrementVolumeRequest message
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

// Example 2 : IncrementVolumeConfirmation message
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

### UltraFineDustObject {#UltraFineDustObject}
An object containing data on ultra fine dust. It is used to define the ultra fine dust concentration level measured by the appliance. The value is expressed as a number.

#### Object field
| Field name       | Type    | Field description                     | Required |
|---------------|---------|-----------------------------|---------|
| `value`       | number  | Ultra fine dust index                  | Yes     |
| `index`       | number  | Ultra fine dust concentration level                  | Yes     |

#### Object Example
{% raw %}

```json
// Example : GetUltraFineDustResponse message
{
  "header": {
    "messageId": "33da6561-0149-4532-a30b-e0de8f75c4cf",
    "name": "GetUltraFineDustResponse",
    "namespace": "ClovaHome",
    "payloadVersion": "1.0"
  },
  "payload": {
    "fineDust": {
        "value": 44,
        "index": "좋음"
    }
  }
}
```

{% endraw %}

#### See also
* [`GetUltraFineDustRequest`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#GetUltraFineDustRequest)
* [`GetUltraFineDustResponse`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#GetUltraFineDustResponse)
