# Control API

Processes requests and responses related to obtaining information of IoT appliances or controlling IoT appliances.

| Message name         | Message type  | Message description                                   |
|------------------|-----------|---------------------------------------------|
| [`ChargeConfirmation`](#ChargeConfirmation)                                   | Response | Returns the result of setting the target appliance to start self-charge in response to a [`ChargeRequest`](#ChargeRequest) message. |
| [`ChargeRequest`](#ChargeRequest)                                             | Request  | Requests your Clova Home extension to self-charge the target appliance. |
| [`DecrementBrightnessConfirmation`](#DecrementBrightnessConfirmation)         | Response | Returns CEK the result of setting the target appliance to turn down the brightness in response to a [`DecrementBrightnessRequest`](#DecrementBrightnessRequest) message. |
| [`DecrementBrightnessRequest`](#DecrementBrightnessRequest)                   | Request  | Requests your Clova Home extension to set the target appliance to turn down the brightness by a specified level. |
| [`DecrementChannelConfirmation`](#DecrementChannelConfirmation)               | Response | Returns CEK the result of setting the target appliance to reduce the number of TV channels in response to a [`DecrementChannelRequest`](#DecrementChannelRequest) message. |
| [`DecrementChannelRequest`](#DecrementChannelRequest)                         | Request  | Requests your Clova Home extension to set the target appliance to reduce the number of TV channel by a specified level. |
| [`DecrementFanSpeedConfirmation`](#DecrementFanSpeedConfirmation)             | Request | Returns CEK the result of setting the target appliance to reduce the fan speed, in response to a [`DecrementFanSpeedRequest`](#DecrementFanSpeedRequest) message. |
| [`DecrementFanSpeedRequest`](#DecrementFanSpeedRequest)                       | Request  | Requests your Clova Home extension to set the target appliance to reduce the fan speed by a specified value. |
| [`DecrementTargetTemperatureConfirmation`](#DecrementTargetTemperatureConfirmation) | Response | Returns CEK the result of setting the target appliance to reduce the temperature, in response to a [`DecrementTargetTemperatureRequest`](#DecrementTargetTemperatureRequest) message. |
| [`DecrementTargetTemperatureRequest`](#DecrementTargetTemperatureRequest)     | Request  Requests your Clova Home extension to set the target appliance to reduce the temperature by a specified value.      |
| [`DecrementVolumeConfirmation`](#DecrementVolumeConfirmation)                 | Response | Returns CEK the result of setting the target appliance to turn down the speaker volume, in response to a [`DecrementVolumeRequest`](#DecrementVolumeRequest) message. |
| [`DecrementVolumeRequest`](#DecrementVolumeRequest)                           | Request  Requests your Clova Home extension to set the target appliance to turn down the speaker volume by a specified value. |
| [`GetAirQualityRequest`](#GetAirQualityRequest)                               | Request  | Requests your Clova Home extension to pass the air quality info measured by the target appliance. |
| [`GetAirQualityResponse`](#GetAirQualityResponse)                             | Response | Returns CEK the air quality info measured by the target appliance in response to a [`GetAirQualityRequest`](#GetAirQualityRequest) message. |
| [`GetBatteryInfoRequest`](#GetBatteryInfoRequest)                             | Request  | Requests your Clova Home extension to pass the battery info of the target appliance. |
| [`GetBatteryInfoResponse`](#GetBatteryInfoResponse)                           | Response | Returns CEK the battery info of the target appliance as response to a [`GetBatteryInfoRequest`](#GetBatteryInfoRequest) message. |
| [`GetFineDustRequest`](#GetFineDustRequest)                                   | Request  | Requests your Clova Home extension to pass the fine dust (PM10) info measured by the target appliance. |
| [`GetFineDustResponse`](#GetFineDustResponse)                                 | Response | Returns CEK the fine dust (PM10) info measured by the target appliance as response to a [`GetFineDustRequest`](#GetFineDustRequest) message. |
| [`GetHumidityRequest`](#GetHumidityRequest)                                   | Request  | Requests your Clova Home extension to pass the humidity info measured by the target appliance. |
| [`GetHumidityResponse`](#GetHumidityResponse)                                 | Response | Returns CEK the humidity info measured by the target appliance in response to a [`GetHumidityRequest`](#GetHumidityRequest) message. |
| [`GetLockStateRequest`](#GetLockStateRequest)                                 | Request  | Requests your Clova Home extension to pass the lock state of the target appliance.   |
| [`GetLockStateResponse`](#GetLockStateResponse)                               | Response | Returns CEK the lock state of the appliance in response to a [`GetLockStateRequest`](#GetLockStateRequest) message. |
| [`GetTargetTemperatureRequest`](#GetTargetTemperatureRequest)                 | Request  | Requests your Clova Home extension to pass the target temperature set on the target appliance. |
| [`GetTargetTemperatureResponse`](#GetTargetTemperatureResponse)               | Response | Returns the current target temperature set on the target appliance in response to the [GetTargetTemperatureRequest](#GetTargetTemperatureRequest) message sent from CEK. |
| [`GetUltraFineDustRequest`](#GetUltraFineDustRequest)                         | Request  | Requests your Clova Home extension to pass the ultra fine dust (PM2.5) info measured by the target appliance. |
| [`GetUltraFineDustResponse`](#GetUltraFineDustResponse)                       | Response | Returns CEK the ultra fine dust (PM2.5) info measured by the target appliance as response to a [`GetUltraFineDustRequest`](#GetUltraFineDustRequest) message. |
| [`HealthCheckRequest`](#HealthCheckRequest)                                   | Request  | Requests your Clova Home extension to check and report the state of the target appliance. |
| [`HealthCheckResponse`](#HealthCheckResponse)                                 | Response | Returns CEK the state of the target appliance, in response to a [`HealthCheckRequest`](#HealthCheckRequest) message. |
| [`IncrementBrightnessConfirmation`](#IncrementBrightnessConfirmation)         | Response | Returns CEK the result of setting the target appliance to turn up the brightness in response to a [`IncrementBrightnessRequest`](#IncrementBrightnessRequest) message. |
| [`IncrementBrightnessRequest`](#IncrementBrightnessRequest)                   | Request  | Requests your Clova Home extension to set the target appliance to turn up the brightness by a specified level. |
| [`IncrementChannelConfirmation`](#IncrementChannelConfirmation)               | Response | Returns CEK the result of setting the target appliance to increase the number of TV channel in response to a [`IncrementChannelRequest`](#IncrementChannelRequest) message. |
| [`IncrementChannelRequest`](#IncrementChannelRequest)                         | Request  | Requests your Clova Home extension to set the target appliance to increase the number of TV channel by a specified level. |
| [`IncrementFanSpeedConfirmation`](#IncrementFanSpeedConfirmation)             | Response | Returns CEK the result of setting the target appliance to raise the fan speed, in response to an [`IncrementFanSpeedRequest`](#IncrementFanSpeedRequest) message. |
| [`IncrementFanSpeedRequest`](#IncrementFanSpeedRequest)                       | Request | Requests your Clova Home extension to set the target appliance to raise the fan speed by a specified value. |
| [`IncrementTargetTemperatureConfirmation`](#IncrementTargetTemperatureConfirmation) | Response | Returns CEK the result of setting the target appliance to raise the temperature, in response to an [`IncrementTargetTemperatureRequest`](#IncrementTargetTemperatureRequest) message. |
| [`IncrementTargetTemperatureRequest`](#IncrementTargetTemperatureRequest)     | Request  | Requests your Clova Home extension to set the target appliance to raise the temperature by a specified value.     |
| [`IncrementVolumeConfirmation`](#IncrementVolumeConfirmation)                 | Response | Returns CEK the result of setting the target appliance to turn up the speaker volume, in response to an [`IncrementVolumeRequest`](#IncrementVolumeRequest) message. |
| [`IncrementVolumeRequest`](#IncrementVolumeRequest)                           | Request | Requests your Clova Home extension to set the target appliance to raise the volume by a specified value. |
| [`MuteConfirmation`](#MuteConfirmation)                                       | Response | Returns CEK the result of setting the target appliance to turn off the sound (to mute), in response to a [`MuteRequest`](#MuteRequest) message. |
| [`MuteRequest`](#MuteRequest)                                                 | Request  | Requests your Clova Home extension to turn off the sound (to mute) of the target appliance. |
| [`SetBrightnessConfirmation`](#SetBrightnessConfirmation)                     | Response | Returns CEK the result of setting the target appliance to adjust the brightness in response to a [`SetBrightnessRequest`](#ISetBrightnessRequest) message. |
| [`SetBrightnessRequest`](#SetBrightnessRequest)                               | Request  | Requests your Clova Home extension to set the target appliance to adjust the brightness by a specified level. |
| [`SetChannelByNameConfirmation`](#SetChannelByNameConfirmation)               | Response | Returns CEK the result of setting the target appliance to change the TV channel by the channel name in response to a [`SetChannelByNameRequest`](#SetChannelByNameRequest) message. |
| [`SetChannelByNameRequest`](#SetChannelByNameRequest)                         | Request  | Requests your Clova Home extension to set the target appliance to change the TV channel to a specified channel name. |
| [`SetChannelConfirmation`](#SetChannelConfirmation)                           | Response | Returns CEK the result of setting the target appliance to change the TV channel by channel number in response to a [`SetChannelRequest`](#SetChannelRequest) message. |
| [`SetChannelRequest`](#SetChannelRequest)                                     | Request  | Requests your Clova Home extension to set the target appliance to change the TV channel to a specified channel number. |
| [`SetFanSpeedConfirmation`](#SetFanSpeedConfirmation)                         | Response | Returns CEK the result of setting the target appliance to adjust the fan speed in response to a [`SetFanSpeedRequest`](#SetFanSpeedRequest) message. |
| [`SetFanSpeedRequest`](#SetFanSpeedRequest)                                   | Request  | Requests your Clova Home extension to set the target appliance to adjust the fan speed by a specified level. |
| [`SetLockStateConfirmation`](#SetLockStateConfirmation)                       | Response | Returns the result of setting the target appliance to lock or unlock in response to the [`SetLockStateRequest`](#SetLockStateRequest) message sent from CEK.  |
| [`SetLockStateRequest`](#SetLockStateRequest)                                 | Request  | Requests your Clova Home extension to lock or unlock the target appliance.  |
| [`SetModeConfirmation`](#SetModeConfirmation)                                 | Response | Returns CEK the result of setting the target appliance to change the heating mode, in response to a [`SetModeRequest`](#SetModeRequest) message. |
| [`SetModeRequest`](#SetModeRequest)                                           | Request  | Requests your Clova Home extension to set the target appliance to change the heating mode to a specified mode. |
| [`SetTargetTemperatureConfirmation`](#SetTargetTemperatureConfirmation)       | Response | Returns CEK the result of setting the target appliance to change the target temperature in response to a [`SetTargetTemperatureRequest`](#SetTargetTemperatureRequest) message. |
| [`SetTargetTemperatureRequest`](#SetTargetTemperatureRequest)                 | Request  | Requests your Clova Home extension to set the target appliance to change the target temperature by a specified level. |
| [`TurnOffConfirmation`](#TurnOffConfirmation)                                 | Response | Returns CEK the result of setting the target appliance to turn off, in response to a [`TurnOffRequest`](#TurnOffRequest) message. |
| [`TurnOffRequest`](#TurnOffRequest)                                           | Request  | Requests your Clova Home extension to turn off the target appliance.                        |
| [`TurnOnConfirmation`](#TurnOnConfirmation)                                   | Response | Returns the result of setting the target appliance to turn on in response to a [`TurnOnRequest`](#TurnOnRequest) message. |
| [`TurnOnRequest`](#TurnOnRequest)                                             | Request  | Requests your Clova Home extension to turn on the target appliance.                        |
| [`UnmuteConfirmation`](#UnmuteConfirmation)                                   | Response | Returns CEK the result of setting the target appliance to turn on the sound (to unmute) in response to a [`UnmuteRequest`](#UnmuteRequest) message. |
| [`UnmuteRequest`](#UnmuteRequest)                                             | Request  | Requests your Clova Home extension to turn on the sound (to unmute) of the target appliance. |

## ChargeConfirmation {#ChargeConfirmation}
Returns CEK the result of setting the target appliance to start self-charging in response to a [`ChargeRequest`](#ChargeRequest) message.

### Payload field

None

### Message example

{% raw %}

```json
{
  "header": {
    "messageId": "4ec35000-88ce-4724-b7e4-7f52050558fd",
    "name": "ChargeConfirmation",
    "namespace": "ClovaHome",
    "payloadVersion": "1.0"
  },
  "payload": {}
}
```

{% endraw %}

### See also
* [`ChargeRequest`](#ChargeRequest)

## ChargeRequest {#ChargeRequest}
Requests your Clova Home extension to self-charge the target appliance. It is usually used to control appliances such as a robot vacuum cleaner. To respond to this request, use a [`ChargeConfirmation`](#ChargeConfirmation) message.

### Payload field

| Field name       | Type    | Field description                     | Required |
|---------------|---------|-----------------------------|---------|
| `accessToken`      | string                                  | The access token for the user's IoT service account. CEK forwards the access token by obtaining it from the authorization server of the 3rd party service. See [Linking user account](/CEK/Guides/LInk_User_Account.md) for more details.                          | Yes    |
| `appliance`        | [ApplianceInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#ApplianceInfoObject)     | An object containing details of the target appliance. `applianceId` is a required field.     | Yes    |

### Message example

{% raw %}

```json
{
  "header": {
    "messageId": "6c04fc2d-64dd-41a0-9162-7cb0d4cf7c08",
    "name": "ChargeRequest",
    "namespace": "ClovaHome",
    "payloadVersion": "1.0"
  },
  "payload": {
    "accessToken": "92ebcb67fe33",
    "appliance": {
      "applianceId": "device-009"
    }
  }
}
```

{% endraw %}

### See also
* [`ChargeConfirmation`](#ChargeConfirmation)

## DecrementBrightnessConfirmation {#DecrementBrightnessConfirmation}
Returns CEK the result of setting the target appliance to turn down the brightness in response to a [`DecrementBrightnessRequest`](#DecrementBrightnessRequest) message.

### Payload field

| Field name       | Type    | Field description                     | Required |
|---------------|---------|-----------------------------|---------|
| `brightness`               | [BrightnessInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#BrightnessInfoObject) | An object containing the current brightness detail                                | Yes    |
| `previousState`            | object | An object containing the previous state of the appliance                           | Yes    |
| `previousState.brightness` | [BrightnessInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#BrightnessInfoObject) | An object containing the previous brightness detail                                | Yes    |

### Message example

{% raw %}

```json
{
  "header": {
    "messageId": "4ec35000-88ce-4724-b7e4-7f52050558fd",
    "name": "DecrementBrightnessConfirmation",
    "namespace": "ClovaHome",
    "payloadVersion": "1.0"
  },
  "payload": {
    "brightness": {
      "value": 20
    },
    "previousState": {
      "brightness": {
        "value": 40
      }
    }
  }
}
```

{% endraw %}

### See also
* [`DecrementBrightnessRequest`](#DecrementBrightnessRequest)

## DecrementBrightnessRequest {#DecrementBrightnessRequest}
Requests your Clova Home extension to set the target appliance to turn down the brightness by a specified level. It is usually used to control appliances such as a lighting appliance. To respond to this request, use a [`DecrementBrightnessConfirmation`](#DecrementBrightnessConfirmation) message.

### Payload field

| Field name       | Type    | Field description                     | Required |
|---------------|---------|-----------------------------|---------|
| `accessToken`      | string                                  | The access token for the user's IoT service account. CEK forwards the access token by obtaining it from the authorization server of the 3rd party service. See [Linking user account](/CEK/Guides/LInk_User_Account.md) for more details.                          | Yes    |
| `appliance`        | [ApplianceInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#ApplianceInfoObject)     | An object containing details of the target appliance. `applianceId` is a required field.     | Yes    |
| `deltaBrightness`       | [BrightnessInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#BrightnessInfoObject)             | An object containing the expected change in the value of the brightness.                              | Yes    |

### Message example

{% raw %}

```json
{
  "header": {
    "messageId": "6c04fc2d-64dd-41a0-9162-7cb0d4cf7c08",
    "name": "DecrementBrightnessRequest",
    "namespace": "ClovaHome",
    "payloadVersion": "1.0"
  },
  "payload": {
    "accessToken": "92ebcb67fe33",
    "appliance": {
      "applianceId": "device-010"
    },
    "deltaBrightness": {
      "value": 20
    }
  }
}
```

{% endraw %}

### See also
* [`DecrementBrightnessConfirmation`](#DecrementBrightnessConfirmation)

## DecrementChannelConfirmation {#DecrementChannelConfirmation}
Returns CEK the result of setting the target appliance to reduce the number of TV channel in response to a [`DecrementChannelRequest`](#DecrementChannelRequest) message.

### Payload field

| Field name       | Type    | Field description                     | Required |
|---------------|---------|-----------------------------|---------|
| `channel`               | [TVChannelInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#TVChannelInfoObject) | An object containing the current TV channel detail                                | Yes    |
| `previousState`            | object | An object containing the previous state of the appliance                           | Yes    |
| `previousState.channel` | [TVChannelInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#TVChannelInfoObject) | An object containing the previous TV channel detail                                | Yes    |

### Message example

{% raw %}

```json
{
  "header": {
    "messageId": "4ec35000-88ce-4724-b7e4-7f52050558fd",
    "name": "DecrementChannelConfirmation",
    "namespace": "ClovaHome",
    "payloadVersion": "1.0"
  },
  "payload": {
    "brightness": {
      "value": 12
    },
    "previousState": {
      "brightness": {
        "value": 13
      }
    }
  }
}
```

{% endraw %}

### See also
* [`DecrementChannelRequest`](#DecrementChannelRequest)

## DecrementChannelRequest {#DecrementChannelRequest}
Requests your Clova Home extension to set the target appliance to reduce the number of TV channel by a specified level. It is usually used to control appliances such as a TV or a set-top box. To respond to this request, use a [`DecrementChannelConfirmation`](#DecrementChannelConfirmation) message.

### Payload field

| Field name       | Type    | Field description                     | Required |
|---------------|---------|-----------------------------|---------|
| `accessToken`      | string                                  | The access token for the user's IoT service account. CEK forwards the access token by obtaining it from the authorization server of the 3rd party service. See [Linking user account](/CEK/Guides/LInk_User_Account.md) for more details.                          | Yes    |
| `appliance`        | [ApplianceInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#ApplianceInfoObject)     | An object containing details of the target appliance. `applianceId` is a required field.     | Yes    |
| `deltaChannel`       | [TVChannelInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#TVChannelInfoObject)             | An object containing the expected change in the value of the TV channel.                              | Yes    |

### Message example

{% raw %}

```json
{
  "header": {
    "messageId": "6c04fc2d-64dd-41a0-9162-7cb0d4cf7c08",
    "name": "DecrementChannelRequest",
    "namespace": "ClovaHome",
    "payloadVersion": "1.0"
  },
  "payload": {
    "accessToken": "92ebcb67fe33",
    "appliance": {
      "applianceId": "device-011"
    },
    "deltaChannel": {
      "value": 1
    }
  }
}
```

{% endraw %}

### See also
* [`DecrementChannelConfirmation`](#DecrementChannelConfirmation)

## DecrementFanSpeedConfirmation {#DecrementFanSpeedConfirmation}
Returns CEK the result of setting the target appliance to reduce the fan speed, in response to a [`DecrementFanSpeedRequest`](#DecrementFanSpeedRequest) message.

### Payload field

| Field name       | Type    | Field description                     | Required |
|---------------|---------|-----------------------------|---------|
| `fanSpeed`       | [SpeedInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#SpeedInfoObject)             | An object containing the current fan speed                                | Yes    |
| `previousState`     | object                                  | An object containing the previous state of the appliance                           | Yes    |
| `previousState.fanSpeed` | [SpeedInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#SpeedInfoObject)     | An object containing the previous fan speed                                | Yes    |

### Message example

{% raw %}

```json
{
  "header": {
    "messageId": "4ec35000-88ce-4724-b7e4-7f52050558fd",
    "name": "DecrementFanSpeedConfirmation",
    "namespace": "ClovaHome",
    "payloadVersion": "1.0"
  },
  "payload": {
    "fanSpeed": {
      "value": 2
    },
    "previousState": {
      "fanSpeed": {
        "value": 4
      }
    }
  }
}
```

{% endraw %}

### See also
* [`DecrementFanSpeedRequest`](#DecrementFanSpeedRequest)

## DecrementFanSpeedRequest {#DecrementFanSpeedRequest}
Requests your Clova Home extension to set the target appliance to reduce the fan speed by a specified value. It is usually used to control appliances such as an air purifier. To respond to this request, use a [`DecrementFanSpeedConfirmation`](#DecrementFanSpeedConfirmation) message.

### Payload field

| Field name       | Type    | Field description                     | Required |
|---------------|---------|-----------------------------|---------|
| `accessToken`      | string                                  | The access token for the user's IoT service account. CEK forwards the access token by obtaining it from the authorization server of the 3rd party service. See [Linking user account](/CEK/Guides/LInk_User_Account.md) for more details.                          | Yes    |
| `appliance`        | [ApplianceInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#ApplianceInfoObject)     | An object containing details of the target appliance. `applianceId` is a required field.     | Yes    |
| `deltaFanSpeed`       | [SpeedInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#SpeedInfoObject)             | An object containing the expected change in the value of the fan speed.                              | Yes    |

### Message example

{% raw %}

```json
{
  "header": {
    "messageId": "6c04fc2d-64dd-41a0-9162-7cb0d4cf7c08",
    "name": "DecrementFanSpeedRequest",
    "namespace": "ClovaHome",
    "payloadVersion": "1.0"
  },
  "payload": {
    "accessToken": "92ebcb67fe33",
    "appliance": {
      "applianceId": "device-004"
    },
    "deltaFanSpeed": {
      "value": 2
    }
  }
}
```

{% endraw %}

### See also
* [`DecrementFanSpeedConfirmation`](#DecrementFanSpeedConfirmation)

## DecrementTargetTemperatureConfirmation {#DecrementTargetTemperatureConfirmation}
Returns CEK the result of setting the target appliance to reduce the temperature, in response to a [`DecrementTargetTemperatureRequest`](#DecrementTargetTemperatureRequest) message.

### Payload field

| Field name       | Type    | Field description                     | Required |
|---------------|---------|-----------------------------|---------|
| `targetTemperature` | [TemperatureInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#TemperatureInfoObject) | An object containing the current target temperature                            | Yes    |
| `previousState`     | object                                  | An object containing the previous state of the appliance                           | Yes    |
| `previousState.targetTemperature` | [TemperatureInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#TemperatureInfoObject) | An object containing the previous target temperature              | Yes    |

### Message example

{% raw %}

```json
{
  "header": {
    "messageId": "4ec35000-88ce-4724-b7e4-7f52050558fd",
    "name": "DecrementTargetTemperatureConfirmation",
    "namespace": "ClovaHome",
    "payloadVersion": "1.0"
  },
  "payload": {
    "targetTemperature": {
      "value": 23.0
    },
    "previousState": {
      "targetTemperature": {
        "value": 25.0
      }
    }
  }
}
```

{% endraw %}

### See also
* [`DecrementTargetTemperatureRequest`](#DecrementTargetTemperatureRequest)

## DecrementTargetTemperatureRequest {#DecrementTargetTemperatureRequest}
Requests your Clova Home extension to set the target appliance to reduce the temperature by a specified value. It is usually used to control appliances such as an air conditioner or a temperature controller. To respond to this request, use a [`DecrementTargetTemperatureConfirmation`](#DecrementTargetTemperatureConfirmation) message.

### Payload field

| Field name       | Type    | Field description                     | Required |
|---------------|---------|-----------------------------|---------|
| `accessToken`      | string                                  | The access token for the user's IoT service account. CEK forwards the access token by obtaining it from the authorization server of the 3rd party service. See [Linking user account](/CEK/Guides/LInk_User_Account.md) for more details.                          | Yes    |
| `appliance`        | [ApplianceInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#ApplianceInfoObject)     | An object containing details of the target appliance. `applianceId` is a required field. | Yes    |
| `deltaTemperature` | [TemperatureInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#TemperatureInfoObject) | An object containing the expected change in the value of the temperature.                              | Yes    |

### Message example

{% raw %}

```json
{
  "header": {
    "messageId": "6c04fc2d-64dd-41a0-9162-7cb0d4cf7c08",
    "name": "DecrementTargetTemperatureRequest",
    "namespace": "ClovaHome",
    "payloadVersion": "1.0"
  },
  "payload": {
    "accessToken": "92ebcb67fe33",
    "appliance": {
      "applianceId": "device-001"
    },
    "deltaTemperature": {
      "value": 2.0
    }
  }
}
```

{% endraw %}

### See also
* [`DecrementTargetTemperatureConfirmation`](#DecrementTargetTemperatureConfirmation)

## DecrementVolumeConfirmation {#DecrementVolumeConfirmation}
Returns CEK the result of setting the target appliance to turn down the speaker volume, in response to a [`DecrementVolumeRequest`](#DecrementVolumeRequest) message.

### Payload field

| Field name       | Type    | Field description                     | Required |
|---------------|---------|-----------------------------|---------|
| `targetVolume`      | [VolumeInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#SpeedInfoObject)            | An object containing the current volume                             | Yes    |
| `previousState`     | object                                  | An object containing the previous state of the appliance                        | Yes    |
| `previousState.targetVolume` | [VolumeInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#SpeedInfoObject)    | An object containing the previous volume                             | Yes    |

### Message example

{% raw %}

```json
{
  "header": {
    "messageId": "4ec35000-88ce-4724-b7e4-7f52050558fd",
    "name": "DecrementVolumeConfirmation",
    "namespace": "ClovaHome",
    "payloadVersion": "1.0"
  },
  "payload": {
    "targetVolume": {
      "value": 10
    },
    "previousState": {
      "targetVolume": {
        "value": 20
      }
    }
  }
}
```

{% endraw %}

### See also
* [`DecrementVolumeRequest`](#DecrementVolumeRequest)

## DecrementVolumeRequest {#DecrementVolumeRequest}
Requests your Clova Home extension to set the target appliance to turn down the speaker volume by a specified value. It is usually used to control appliances such as a TV set-top box. To respond to this request, use a [`DecrementVolumeConfirmation`](#DecrementVolumeConfirmation) message.

### Payload field

| Field name       | Type    | Field description                     | Required |
|---------------|---------|-----------------------------|---------|
| `accessToken`      | string                                  | The access token for the user's IoT service account. CEK forwards the access token by obtaining it from the authorization server of the 3rd party service. See [Linking user account](/CEK/Guides/LInk_User_Account.md) for more details.                          | Yes    |
| `appliance`        | [ApplianceInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#ApplianceInfoObject)     | An object containing details of the target appliance. `applianceId` is a required field.     | Yes    |
| `deltaVolume`       | [VolumeInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#VolumeInfoObject)             | An object containing the expected change in the value of the volume.                           | Yes    |

### Message example

{% raw %}

```json
{
  "header": {
    "messageId": "6c04fc2d-64dd-41a0-9162-7cb0d4cf7c08",
    "name": "DecrementVolumeRequest",
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
```

{% endraw %}

### See also
* [`DecrementVolumeConfirmation`](#DecrementVolumeConfirmation)

## GetAirQualityRequest {#GetAirQualityRequest}
Requests your Clova Home extension to set the target appliance to pass the air quality info measured by the target appliance. It is usually used to control appliances such as an air purifier. To respond to this request, use a [`GetAirQualityResponse`](#GetAirQualityResponse) message.

| Field name       | Type    | Field description                     | Required |
|---------------|---------|-----------------------------|---------|
| `accessToken`      | string                                  | The access token for the user's IoT service account. CEK forwards the access token by obtaining it from the authorization server of the 3rd party service. See [Linking user account](/CEK/Guides/LInk_User_Account.md) for more details.                          | Yes    |
| `appliance`        | [ApplianceInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#ApplianceInfoObject)     | An object containing details of the target appliance. `applianceId` is a required field.     | Yes    |

### Message example

{% raw %}

```json
{
  "header": {
    "messageId": "6c04fc2d-64dd-41a0-9162-7cb0d4cf7c08",
    "name": "GetAirQualityRequest",
    "namespace": "ClovaHome",
    "payloadVersion": "1.0"
  },
  "payload": {
    "accessToken": "92ebcb67fe33",
    "appliance": {
      "applianceId": "device-011"
    }
  }
}
```

{% endraw %}

### See also
* [`GetAirQualityResponse`](#GetAirQualityResponse)

## GetAirQualityResponse {#GetAirQualityResponse}
Returns CEK the air quality info measured by the target appliance in response to a [`GetAirQualityRequest`](#GetAirQualityRequest) message.

| Field name       | Type    | Field description                     | Required |
|---------------|---------|-----------------------------|---------|
| `airQuality`                 | [AirQualityInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#AirQualityInfoObject) | An object containing details of the current air quality measured by the target appliance.   | Yes    |
| `applianceResponseTimestamp` | string | Time when the requests made from the appliance was checked(Timestamp, [ISO 8061](https://en.wikipedia.org/wiki/ISO_8601))     | Yes    |

### Message example

{% raw %}

```json
{
  "header": {
    "messageId": "33da6561-0149-4532-a30b-e0de8f75c4cf",
    "name": "GetAirQualityResponse",
    "namespace": "ClovaHome",
    "payloadVersion": "1.0"
  },
  "payload": {
    "airQuality": {
        "index": "normal"
    }
  }
}
```

{% endraw %}

### See also
* [`GetAirQualityRequest`](#GetAirQualityRequest)

## GetBatteryInfoRequest {#GetBatteryInfoRequest}
Requests your Clova Home extension to pass the current battery info of the target appliance. It is usually used to check internal battery info of wireless devices such as a robot vacuum cleaner. To respond to this request, use a [`GetBatteryInfoResponse`](#GetBatteryInfoResponse) message.

| Field name       | Type    | Field description                     | Required |
|---------------|---------|-----------------------------|---------|
| `accessToken`      | string                                  | The access token for the user's IoT service account. CEK forwards the access token by obtaining it from the authorization server of the 3rd party service. See [Linking user account](/CEK/Guides/LInk_User_Account.md) for more details.                          | Yes    |
| `appliance`        | [ApplianceInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#ApplianceInfoObject)     | An object containing details of the target appliance. `applianceId` is a required field.     | Yes    |

### Message example

{% raw %}

```json
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
      "applianceId": "device-011"
    }
  }
}
```

{% endraw %}

### See also
* [`GetBatteryInfoResponse`](#GetBatteryInfoResponse)

## GetBatteryInfoResponse {#GetBatteryInfoResponse}
Returns CEK the battery info of the target appliance as response to a [`GetBatteryInfoRequest`](#GetBatteryInfoRequest) message.

| Field name       | Type    | Field description                     | Required |
|---------------|---------|-----------------------------|---------|
| `batteryInfo`                 | [BrightnessObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#BatteryInfoObject) | An object containing the current battery info.   | Yes    |
| `applianceResponseTimestamp` | string | Time when the requests made from the appliance was checked(Timestamp, [ISO 8061](https://en.wikipedia.org/wiki/ISO_8601))     | Yes    |

### Message example

{% raw %}

```json
{
  "header": {
    "messageId": "33da6561-0149-4532-a30b-e0de8f75c4cf",
    "name": "GetBatteryInfoResponse",
    "namespace": "ClovaHome",
    "payloadVersion": "1.0"
  },
  "payload": {
    "batteryInfo": {
        "value": 50
    }
  }
}
```

{% endraw %}

### See also
* [`GetBatteryInfoRequest`](#GetBatteryInfoRequest)

## GetFineDustRequest {#GetFineDustRequest}
Requests your Clova Home extension to pass the fine dust info (PM10) measured by the target appliance. It is usually used to check fine dust info (PM10) from appliances such as an air purifier. To respond to this request, use a [`GetFineDustResponse`](#GetFineDustResponse) message.

| Field name       | Type    | Field description                     | Required |
|---------------|---------|-----------------------------|---------|
| `accessToken`      | string                                  | The access token for the user's IoT service account. CEK forwards the access token by obtaining it from the authorization server of the 3rd party service. See [Linking user account](/CEK/Guides/LInk_User_Account.md) for more details.                          | Yes    |
| `appliance`        | [ApplianceInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#ApplianceInfoObject)     | An object containing details of the target appliance. `applianceId` is a required field.     | Yes    |

### Message example

{% raw %}

```json
{
  "header": {
    "messageId": "6c04fc2d-64dd-41a0-9162-7cb0d4cf7c08",
    "name": "GetFineDustRequest",
    "namespace": "ClovaHome",
    "payloadVersion": "1.0"
  },
  "payload": {
    "accessToken": "92ebcb67fe33",
    "appliance": {
      "applianceId": "device-011"
    }
  }
}
```

{% endraw %}

### See also
* [`GetFineDustResponse`](#GetFineDustResponse)

## GetFineDustResponse {#GetFineDustResponse}
Returns CEK the fine dust (PM10) info measured by the target appliance as response to a [`GetFineDustRequest`](#GetFineDustRequest) message.

| Field name       | Type    | Field description                     | Required |
|---------------|---------|-----------------------------|---------|
| `fineDust`                 | [FineDustInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#FineDustInfoObject) | An object containing details of the current fine dust info measured by the target appliance.   | Yes    |
| `applianceResponseTimestamp` | string | Time when the requests made from the appliance was checked(Timestamp, [ISO 8061](https://en.wikipedia.org/wiki/ISO_8601))     | Yes    |

### Message example

{% raw %}

```json
{
  "header": {
    "messageId": "33da6561-0149-4532-a30b-e0de8f75c4cf",
    "name": "GetFineDustResponse",
    "namespace": "ClovaHome",
    "payloadVersion": "1.0"
  },
  "payload": {
    "fineDust": {
        "value": 77
    }
  }
}
```

{% endraw %}

### See also
* [`GetFineDustRequest`](#GetFineDustRequest)

## GetHumidityRequest {#GetHumidityRequest}
Requests your Clova Home extension to set the target appliance to pass the humidity info measured by the target appliance. It is usually used to check humidity info from appliances such as a humidifier. To respond to this request, use a [`GetHumidityResponse`](#GetHumidityResponse) message.

| Field name       | Type    | Field description                     | Required |
|---------------|---------|-----------------------------|---------|
| `accessToken`      | string                                  | The access token for the user's IoT service account. CEK forwards the access token by obtaining it from the authorization server of the 3rd party service. See [Linking user account](/CEK/Guides/LInk_User_Account.md) for more details.                          | Yes    |
| `appliance`        | [ApplianceInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#ApplianceInfoObject)     | An object containing details of the target appliance. `applianceId` is a required field.     | Yes    |

### Message example

{% raw %}

```json
{
  "header": {
    "messageId": "6c04fc2d-64dd-41a0-9162-7cb0d4cf7c08",
    "name": "GetHumidityRequest",
    "namespace": "ClovaHome",
    "payloadVersion": "1.0"
  },
  "payload": {
    "accessToken": "92ebcb67fe33",
    "appliance": {
      "applianceId": "device-012"
    }
  }
}
```

{% endraw %}

### See also
* [`GetHumidityResponse`](#GetHumidityResponse)

## GetHumidityResponse {#GetHumidityResponse}
Returns CEK the humidity info measured by the target appliance in response to a [`GetHumidityRequest`](#GetHumidityRequest) message.

| Field name       | Type    | Field description                     | Required |
|---------------|---------|-----------------------------|---------|
| `humidity`                 | [HumidityInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#HumidityInfoObject) | An object containing details of the current humidity measured by the target appliance.   | Yes    |
| `applianceResponseTimestamp` | string | Time when the requests made from the appliance was checked(Timestamp, [ISO 8061](https://en.wikipedia.org/wiki/ISO_8601))     | Yes    |

### Message example

{% raw %}

```json
{
  "header": {
    "messageId": "33da6561-0149-4532-a30b-e0de8f75c4cf",
    "name": "GetHumidityResponse",
    "namespace": "ClovaHome",
    "payloadVersion": "1.0"
  },
  "payload": {
    "humidity": {
        "value": 40
    }
  }
}
```

{% endraw %}

### See also
* [GetHumidityRequest](#GetHumidityRequest)

## GetLockStateRequest {#GetLockStateRequest}
Requests Clova Home extension to provide the current lock state of the target appliance. It is usually used to check state of appliances such as a smart valve. To respond to this request, use a [`GetLockStateResponse`](#GetLockStateResponse) message.

| Field name       | Type    | Field description                     | Required |
|---------------|---------|-----------------------------|---------|
| `accessToken`      | string                                  | The access token for the user's IoT service account. CEK forwards the access token by obtaining it from the authorization server of the 3rd party service. See [Linking user account](/CEK/Guides/LInk_User_Account.md) for more details.                          | Yes    |
| `appliance`        | [ApplianceInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#ApplianceInfoObject)     | An object containing details of the target appliance. `applianceId` is a required field.     | Yes    |

### Message example

{% raw %}

```json
{
  "header": {
    "messageId": "6c04fc2d-64dd-41a0-9162-7cb0d4cf7c08",
    "name": "GetLockStateRequest",
    "namespace": "ClovaHome",
    "payloadVersion": "1.0"
  },
  "payload": {
    "accessToken": "92ebcb67fe33",
    "appliance": {
      "applianceId": "device-012"
    }
  }
}
```

{% endraw %}

### See also
* [`GetLockStateResponse`](#GetLockStateResponse)

## GetLockStateResponse {#GetLockStateResponse}
Returns CEK the lock state of the appliance in response to a [`GetLockStateRequest`](#GetLockStateRequest) message.

| Field name       | Type    | Field description                     | Required |
|---------------|---------|-----------------------------|---------|
| `lockState`   | string | Lock state of the appliance. Available values are: <ul><li><code>"LOCKED"</code></li><li><code>"UNLOCKED"</code></li></ul> | Yes    |
| `applianceResponseTimestamp` | string | Time when the requests made from the appliance was checked(Timestamp, [ISO 8061](https://en.wikipedia.org/wiki/ISO_8601))     | Yes    |

### Message example

{% raw %}

```json
{
  "header": {
    "messageId": "33da6561-0149-4532-a30b-e0de8f75c4cf",
    "name": "GetLockStateResponse",
    "namespace": "ClovaHome",
    "payloadVersion": "1.0"
  },
  "payload": {
    "airQuality": "LOCKED"
  }
}
```

{% endraw %}

### See also
* [`GetLockStateRequest`](#GetLockStateRequest)

## GetTargetTemperatureRequest {#GetTargetTemperatureRequest}
Requests your Clova Home extension to pass the target temperature set by the target appliance. It is usually used to check the target temperature from appliances such as an air conditioner or a temperature controller. To respond to this request, use a [`GetTargetTemperatureResponse`](#GetTargetTemperatureResponse) message.

| Field name       | Type    | Field description                     | Required |
|---------------|---------|-----------------------------|---------|
| `accessToken`      | string                                  | The access token for the user's IoT service account. CEK forwards the access token by obtaining it from the authorization server of the 3rd party service. See [Linking user account](/CEK/Guides/LInk_User_Account.md) for more details.                          | Yes    |
| `appliance`        | [ApplianceInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#ApplianceInfoObject)     | An object containing details of the target appliance. `applianceId` is a required field.     | Yes    |

### Message example

{% raw %}

```json
{
  "header": {
    "messageId": "6c04fc2d-64dd-41a0-9162-7cb0d4cf7c08",
    "name": "GetTargetTemperatureRequest",
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

### See also
* [`GetTargetTemperatureResponse`](#GetTargetTemperatureResponse)

## GetTargetTemperatureResponse {#GetTargetTemperatureResponse}
Returns CEK the result of setting the target temperature on the target appliance in response to an [`GetTargetTemperatureRequest`](#GetTargetTemperatureRequest) message.

| Field name       | Type    | Field description                     | Required |
|---------------|---------|-----------------------------|---------|
| `targetTemperature`          | [TemperatureInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#TemperatureInfoObject) | An object containing the target temperature set on the target appliance   | Yes    |
| `applianceResponseTimestamp` | string | Time when the requests made from the appliance was checked(Timestamp, [ISO 8061](https://en.wikipedia.org/wiki/ISO_8601))     | Yes    |

### Message example

{% raw %}

```json
{
  "header": {
    "messageId": "33da6561-0149-4532-a30b-e0de8f75c4cf",
    "name": "GetTargetTemperatureResponse",
    "namespace": "ClovaHome",
    "payloadVersion": "1.0"
  },
  "payload": {
    "targetTemperature": {
        "value": 24.0
    }
  }
}
```

{% endraw %}

### See also
* [`GetTargetTemperatureRequest`](#GetTargetTemperatureRequest)

## GetUltraFineDustRequest {#GetUltraFineDustRequest}
Requests your Clova Home extension to pass the ultra fine dust info (PM2.5) measured by the target appliance. It is usually used to check the ultra fine dust info (PM2.5) from appliances such as an air purifier. To respond to this request, use a [`GetUltraFineDustResponse`](#GetUltraFineDustResponse) message.

| Field name       | Type    | Field description                     | Required |
|---------------|---------|-----------------------------|---------|
| `accessToken`      | string                                  | The access token for the user's IoT service account. CEK forwards the access token by obtaining it from the authorization server of the 3rd party service. See [Linking user account](/CEK/Guides/LInk_User_Account.md) for more details.                          | Yes    |
| `appliance`        | [ApplianceInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#ApplianceInfoObject)     | An object containing details of the target appliance. `applianceId` is a required field.     | Yes    |

### Message example

{% raw %}

```json
{
  "header": {
    "messageId": "6c04fc2d-64dd-41a0-9162-7cb0d4cf7c08",
    "name": "GetUltraFineDustRequest",
    "namespace": "ClovaHome",
    "payloadVersion": "1.0"
  },
  "payload": {
    "accessToken": "92ebcb67fe33",
    "appliance": {
      "applianceId": "device-011"
    }
  }
}
```

{% endraw %}

### See also
* [`GetUltraFineDustResponse`](#GetUltraFineDustResponse)

## GetUltraFineDustResponse {#GetUltraFineDustResponse}
Returns CEK the ultra fine dust (PM2.5) info measured by the target appliance as response to a [`GetUltraFineDustRequest`](#GetUltraFineDustRequest) message.

| Field name       | Type    | Field description                     | Required |
|---------------|---------|-----------------------------|---------|
| `fineDust`                 | [UltraFineDustInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#UltraFineDustInfoObject) | An object containing details of the current ultra fine dust info measured by the target appliance.   | Yes    |
| `applianceResponseTimestamp` | string | Time when the requests made from the appliance was checked(Timestamp, [ISO 8061](https://en.wikipedia.org/wiki/ISO_8601))     | Yes    |

### Message example

{% raw %}

```json
{
  "header": {
    "messageId": "33da6561-0149-4532-a30b-e0de8f75c4cf",
    "name": "GetUltraFineDustResponse",
    "namespace": "ClovaHome",
    "payloadVersion": "1.0"
  },
  "payload": {
    "fineDust": {
        "value": 44
    }
  }
}
```

{% endraw %}

### See also
* [`GetUltraFineDustRequest`](#GetUltraFineDustRequest)

## HealthCheckRequest {#HealthCheckRequest}
Requests your Clova Home extension to check and report the state of the target appliance. To respond to this request, use a [`HealthCheckResponse`](#HealthCheckResponse) message.

### Payload field

| Field name       | Type    | Field description                     | Required |
|---------------|---------|-----------------------------|---------|
| `accessToken`   | string  | The access token for the Clova Home extension | Yes    |
| `appliance`     | [ApplianceInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#ApplianceInfoObject)     | An object containing details of the target appliance. `applianceId` is a required field.     | Yes    |

### Message example

{% raw %}

```json
{
  "header": {
    "messageId": "33da6561-0149-4532-a30b-e0de8f75c4cf",
    "name": "HealthCheckRequest",
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

### See also
* [`HealthCheckResponse`](#HealthCheckResponse)

## HealthCheckResponse {#HealthCheckResponse}
Returns CEK the state of the target appliance, in response to a [`HealthCheckRequest`](#HealthCheckRequest) message.

### Payload field

| Field name       | Type    | Field description                     | Required |
|---------------|---------|-----------------------------|---------|
| `isReachable` | boolean | A value that indicates whether the target appliance is reachable over a network. <ul><li><code>true</code>: Reachable (online)</li><li><code>false</code>: Not reachable (offline)</li></ul> | Yes    |
| `isTurnOn`    | boolean | A value that indicates the working state of the target appliance. <ul><li><code>true</code>: Idle</li><li><code>false</code>: Working</li></ul>                  | Yes    |

### Message example

{% raw %}

```json
{
  "header": {
    "messageId": "33da6561-0149-4532-a30b-e0de8f75c4cf",
    "name": "HealthCheckResponse",
    "namespace": "ClovaHome",
    "payloadVersion": "1.0"
  },
  "payload": {
    "isReachable": true,
    "isTurnOn": false
  }
}
```

{% endraw %}

### See also
* [`HealthCheckRequest`](#HealthCheckRequest)

## IncrementBrightnessConfirmation {#IncrementBrightnessConfirmation}
Returns CEK the result of setting the target appliance to turn up the brightness in response to a [`IncrementBrightnessRequest`](#IncrementBrightnessRequest) message.

### Payload field

| Field name       | Type    | Field description                     | Required |
|---------------|---------|-----------------------------|---------|
| `brightness`               | [BrightnessInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#BrightnessInfoObject) | An object containing the current brightness detail                                | Yes    |
| `previousState`            | object | An object containing the previous state of the appliance                           | Yes    |
| `previousState.brightness` | [BrightnessInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#BrightnessInfoObject) | An object containing the previous brightness detail                                | Yes    |

### Message example

{% raw %}

```json
{
  "header": {
    "messageId": "4ec35000-88ce-4724-b7e4-7f52050558fd",
    "name": "IncrementBrightnessConfirmation",
    "namespace": "ClovaHome",
    "payloadVersion": "1.0"
  },
  "payload": {
    "brightness": {
      "value": 40
    },
    "previousState": {
      "brightness": {
        "value": 20
      }
    }
  }
}
```

{% endraw %}

### See also
* [`IncrementBrightnessRequest`](#IncrementBrightnessRequest)

## IncrementBrightnessRequest {#IncrementBrightnessRequest}
Requests your Clova Home extension to set the target appliance to turn up the brightness by a specified level. It is usually used to control appliances such as a lighting appliance. To respond to this request, use a [`IncrementBrightnessConfirmation`](#IncrementBrightnessConfirmation) message.

### Payload field

| Field name       | Type    | Field description                     | Required |
|---------------|---------|-----------------------------|---------|
| `accessToken`      | string                                  | The access token for the user's IoT service account. CEK forwards the access token by obtaining it from the authorization server of the 3rd party service. See [Linking user account](/CEK/Guides/LInk_User_Account.md) for more details.                          | Yes    |
| `appliance`        | [ApplianceInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#ApplianceInfoObject)     | An object containing details of the target appliance. `applianceId` is a required field.     | Yes    |
| `deltaBrightness`       | [BrightnessInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#BrightnessInfoObject)             | An object containing the expected change in the value of the brightness.                              | Yes    |

### Message example

{% raw %}

```json
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
      "value": 20
    }
  }
}
```

{% endraw %}

### See also
* [`IncrementBrightnessConfirmation`](#IncrementBrightnessConfirmation)

## IncrementChannelConfirmation {#IncrementChannelConfirmation}
Returns CEK the result of setting the target appliance to increase the number of TV channels in response to a [`IncrementChannelRequest`](#IncrementChannelRequest) message.

### Payload field

| Field name       | Type    | Field description                     | Required |
|---------------|---------|-----------------------------|---------|
| `channel`               | [TVChannelInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#TVChannelInfoObject) | An object containing the current TV channel detail                                | Yes    |
| `previousState`            | object | An object containing the previous state of the appliance                           | Yes    |
| `previousState.channel` | [TVChannelInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#TVChannelInfoObject) | An object containing the previous TV channel detail                                | Yes    |

### Message example

{% raw %}

```json
{
  "header": {
    "messageId": "4ec35000-88ce-4724-b7e4-7f52050558fd",
    "name": "IncrementChannelConfirmation",
    "namespace": "ClovaHome",
    "payloadVersion": "1.0"
  },
  "payload": {
    "brightness": {
      "value": 14
    },
    "previousState": {
      "brightness": {
        "value": 13
      }
    }
  }
}
```

{% endraw %}

### See also
* [`IncrementChannelRequest`](#IncrementChannelRequest)

## IncrementChannelRequest {#IncrementChannelRequest}
Requests your Clova Home extension to set the target appliance to increase the number of TV channel by a specified level. It is usually used to control appliances such as a TV or a set-top box. To respond to this request, use a [`IncrementChannelConfirmation`](#IncrementChannelConfirmation) message.

### Payload field

| Field name       | Type    | Field description                     | Required |
|---------------|---------|-----------------------------|---------|
| `accessToken`      | string                                  | The access token for the user's IoT service account. CEK forwards the access token by obtaining it from the authorization server of the 3rd party service. See [Linking user account](/CEK/Guides/LInk_User_Account.md) for more details.                          | Yes    |
| `appliance`        | [ApplianceInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#ApplianceInfoObject)     | An object containing details of the target appliance. `applianceId` is a required field.     | Yes    |
| `deltaChannel`       | [TVChannelInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#TVChannelInfoObject)             | An object containing the expected change in the value of the TV channel.                              | Yes    |

### Message example

{% raw %}

```json
{
  "header": {
    "messageId": "6c04fc2d-64dd-41a0-9162-7cb0d4cf7c08",
    "name": "IncrementChannelRequest",
    "namespace": "ClovaHome",
    "payloadVersion": "1.0"
  },
  "payload": {
    "accessToken": "92ebcb67fe33",
    "appliance": {
      "applianceId": "device-011"
    },
    "deltaChannel": {
      "value": 1
    }
  }
}
```

{% endraw %}

### See also
* [`IncrementChannelConfirmation`](#IncrementChannelConfirmation)

## IncrementFanSpeedConfirmation {#IncrementFanSpeedConfirmation}
Returns CEK the result of setting the target appliance to raise the fan speed, in response to an [`IncrementFanSpeedRequest`](#IncrementFanSpeedRequest) message.

### Payload field

| Field name       | Type    | Field description                     | Required |
|---------------|---------|-----------------------------|---------|
| `fanSpeed`            | [SpeedInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#SpeedInfoObject) | An object containing the current fan speed                  | Yes    |
| `previousState`          | object                      | An object containing the previous state of the appliance                 | Yes    |
| `previousState.FanSpeed` | [SpeedInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#SpeedInfoObject) | An object containing the previous fan speed                  | Yes    |

### Message example

{% raw %}

```json
{
  "header": {
    "messageId": "4ec35000-88ce-4724-b7e4-7f52050558fd",
    "name": "IncrementFanSpeedConfirmation",
    "namespace": "ClovaHome",
    "payloadVersion": "1.0"
  },
  "payload": {
    "fanSpeed": {
      "value": 3
    },
    "previousState": {
      "fanSpeed": {
        "value": 2
      }
    }
  }
}
```

{% endraw %}

### See also
* [`IncrementFanSpeedRequest`](#IncrementFanSpeedRequest)

## IncrementFanSpeedRequest {#IncrementFanSpeedRequest}
Requests your Clova Home extension to set the target appliance to raise the fan speed by a specified value. It is usually used to control appliances such as an air purifier. To respond to this request, use an [`IncrementFanSpeedConfirmation`](#IncrementFanSpeedConfirmation) message.

### Payload field

| Field name       | Type    | Field description                     | Required |
|---------------|---------|-----------------------------|---------|
| `accessToken`      | string                                  | The access token for the user's IoT service account. CEK forwards the access token by obtaining it from the authorization server of the 3rd party service. See [Linking user account](/CEK/Guides/LInk_User_Account.md) for more details.                          | Yes    |
| `appliance`        | [ApplianceInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#ApplianceInfoObject)     | An object containing details of the target appliance. `applianceId` is a required field. | Yes    |
| `deltaFanSpeed` | [SpeedInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#SpeedInfoObject) | An object containing the expected change in the value of the speed.                              | Yes    |

### Message example

{% raw %}

```json
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
```

{% endraw %}

### See also
* [`IncrementFanSpeedConfirmation`](#IncrementFanSpeedConfirmation)

## IncrementTargetTemperatureConfirmation {#IncrementTargetTemperatureConfirmation}
Returns CEK the result of setting the target appliance to raise the temperature, in response to an [`IncrementTargetTemperatureRequest`](#IncrementTargetTemperatureRequest) message.

### Payload field

| Field name       | Type    | Field description                     | Required |
|---------------|---------|-----------------------------|---------|
| `targetTemperature` | [TemperatureInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#TemperatureInfoObject) | An object containing the current target temperature                               | Yes    |
| `previousState`     | object                                  | An object containing the previous state of the appliance                              | Yes    |
| `previousState.targetTemperature` | [TemperatureInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#TemperatureInfoObject) | An object containing the previous target temperature                 | Yes    |

### Message example

{% raw %}

```json
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
        "value": 22.0
      }
    }
  }
}
```

{% endraw %}

### See also
* [`IncrementTargetTemperatureRequest`](#IncrementTargetTemperatureRequest)

## IncrementTargetTemperatureRequest {#IncrementTargetTemperatureRequest}
Requests your Clova Home extension to set the target appliance to increase the temperature by a specified value. It is usually used to control appliances such as an air conditioner or a temperature controller. To respond to this request, use an [`IncrementTargetTemperatureConfirmation`](#IncrementTargetTemperatureConfirmation) message.

### Payload field

| Field name       | Type    | Field description                     | Required |
|---------------|---------|-----------------------------|---------|
| `accessToken`      | string | The access token for the user's IoT service account. CEK forwards the access token by obtaining it from the authorization server of the 3rd party service. See [Linking user account](/CEK/Guides/LInk_User_Account.md) for more details. | Yes    |
| `appliance`        | [ApplianceInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#ApplianceInfoObject)     | An object containing details of the target appliance. `applianceId` is a required field. | Yes    |
| `deltaTemperature` | [TemperatureInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#TemperatureInfoObject) | An object containing the expected change in the value of the temperature.                              | Yes    |

### Message example

{% raw %}

```json
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
      "value": 3.0
    }
  }
}
```

{% endraw %}

### See also
* [`IncrementTargetTemperatureConfirmation`](#IncrementTargetTemperatureConfirmation)

## IncrementVolumeConfirmation {#IncrementVolumeConfirmation}
Returns CEK the result of setting the target appliance to turn up the speaker volume, in response to an [`IncrementVolumeRequest`](#IncrementVolumeResponse) message.

### Payload field

| Field name       | Type    | Field description                     | Required |
|---------------|---------|-----------------------------|---------|
| `targetVolume` | [VolumeInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#VolumeInfoObject)               | An object containing the current volume                               | Yes    |
| `previousState`     | object                                 | An object containing the previous state of the appliance                              | Yes    |
| `previousState.targetVolume` | [VolumeInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#VolumeInfoObject) | An object containing the previous volume                 | Yes    |

### Message example

{% raw %}

```json
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

### See also
* [`IncrementVolumeRequest`](#IncrementVolumeRequest)

## IncrementVolumeRequest {#IncrementVolumeRequest}
Requests your Clova Home extension to set the target appliance to turn up the speaker volume by a specified value. It is usually used to control appliances such as a TV set-top box. To respond to this request, use an [`IncrementVolumeConfirmation`](#IncrementVolumeConfirmation) message.

### Payload field

| Field name       | Type    | Field description                     | Required |
|---------------|---------|-----------------------------|---------|
| `accessToken`      | string                                  | The access token for the user's IoT service account. CEK forwards the access token by obtaining it from the authorization server of the 3rd party service. See [Linking user account](/CEK/Guides/LInk_User_Account.md) for more details.                          | Yes    |
| `appliance`        | [ApplianceInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#ApplianceInfoObject)     | An object containing details of the target appliance. `applianceId` is a required field. | Yes    |
| `deltaVolume` | [VolumeInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#VolumeInfoObject)                | An object containing the expected change in the value of the volume.                              | Yes    |

### Message example

{% raw %}

```json
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
```

{% endraw %}

### See also
* [`IncrementVolumeConfirmation`](#IncrementVolumeConfirmation)

## MuteConfirmation {#MuteConfirmation}
Returns CEK the result of setting the target appliance to turn off the sound (to mute) in response to a [`MuteRequest`](#MuteRequest) message.

### Payload field
None

### Message example

{% raw %}

```json
{
  "header": {
    "messageId": "4ec35000-88ce-4724-b7e4-7f52050558fd",
    "name": "MuteConfirmation",
    "namespace": "ClovaHome",
    "payloadVersion": "1.0"
  },
  "payload": {}
}
```

{% endraw %}

### See also
* [`MuteRequest`](#MuteRequest)

## MuteRequest {#MuteRequest}
Requests your Clova Home extension to turn off the sound (to mute) of the target appliance. It is usually used to control appliances such as a TV or a set-top box. To respond to this request, use a [`MuteConfirmation`](#MuteConfirmation) message.

### Payload field

| Field name       | Type    | Field description                     | Required |
|---------------|---------|-----------------------------|---------|
| `accessToken`      | string                                  | The access token for the user's IoT service account. CEK forwards the access token by obtaining it from the authorization server of the 3rd party service. See [Linking user account](/CEK/Guides/LInk_User_Account.md) for more details.                          | Yes    |
| `appliance`        | [ApplianceInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#ApplianceInfoObject)     | An object containing details of the target appliance. `applianceId` is a required field. | Yes    |

### Message example

{% raw %}

```json
{
  "header": {
    "messageId": "6c04fc2d-64dd-41a0-9162-7cb0d4cf7c08",
    "name": "MuteRequest",
    "namespace": "ClovaHome",
    "payloadVersion": "1.0"
  },
  "payload": {
    "accessToken": "92ebcb67fe33",
    "appliance": {
      "applianceId": "device-005"
    }
  }
}
```

{% endraw %}

### See also
* [`MuteConfirmation`](#MuteConfirmation)

## SetBrightnessConfirmation {#SetBrightnessConfirmation}
Returns CEK the result of setting the target appliance to adjust the brightness in response to a [`SetBrightnessRequest`](#ISetBrightnessRequest) message.

### Payload field

| Field name       | Type    | Field description                     | Required |
|---------------|---------|-----------------------------|---------|
| `brightness`               | [BrightnessInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#BrightnessInfoObject) | An object containing the current brightness detail                                | Yes    |

### Message example

{% raw %}

```json
{
  "header": {
    "messageId": "4ec35000-88ce-4724-b7e4-7f52050558fd",
    "name": "SetBrightnessConfirmation",
    "namespace": "ClovaHome",
    "payloadVersion": "1.0"
  },
  "payload": {
    "brightness": {
      "value": 80
    }
  }
}
```

{% endraw %}

### See also
* [`SetBrightnessRequest`](#SetBrightnessRequest)

## SetBrightnessRequest {#SetBrightnessRequest}
Requests your Clova Home extension to set the target appliance to adjust the brightness by a specified level. It is usually used to control appliances such as a lighting appliance. To respond to this request, use a [`SetBrightnessConfirmation`](#SetBrightnessConfirmation) message.

### Payload field

| Field name       | Type    | Field description                     | Required |
|---------------|---------|-----------------------------|---------|
| `accessToken`   | string | The access token for the user's IoT service account. CEK forwards the access token by obtaining it from the authorization server of the 3rd party service. See [Linking user account](/CEK/Guides/LInk_User_Account.md) for more details.                          | Yes    |
| `appliance`     | [ApplianceInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#ApplianceInfoObject) | An object containing details of the target appliance. `applianceId` is a required field. | Yes    |
| `brightness`       | [BrightnessInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#BrightnessInfoObject) | An object containing the brightness to set on the target appliance                | Yes    |

### Message example

{% raw %}

```json
{
  "header": {
    "messageId": "6c04fc2d-64dd-41a0-9162-7cb0d4cf7c08",
    "name": "SetBrightnessRequest",
    "namespace": "ClovaHome",
    "payloadVersion": "1.0"
  },
  "payload": {
    "accessToken": "92ebcb67fe33",
    "appliance": {
      "applianceId": "device-006"
    },
    "brightness": {
      "value": 80
    }
  }
}
```

{% endraw %}

### See also
* [`SetBrightnessConfirmation`](#SetBrightnessConfirmation)

## SetChannelByNameConfirmation {#SetChannelByNameConfirmation}
Returns CEK the result of setting the target appliance to change the TV channel by the channel name in response to a [`SetChannelByNameRequest`](#SetChannelByNameRequest) message.

### Payload field

| Field name       | Type    | Field description                     | Required |
|---------------|---------|-----------------------------|---------|
| `channelName`               | [TVChannelNameInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#TVChannelInfoObject) | An object containing a name of the current TV channel                                | Yes    |

### Message example

{% raw %}

```json
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

### See also
* [`SetChannelByNameRequest`](#SetChannelByNameRequest)

## SetChannelByNameRequest {#SetChannelByNameRequest}
Requests your Clova Home extension to set the target appliance to change the channel to a specified channel name. It is usually used to control appliances such as a TV set-top box. To respond to this request, use a [`SetChannelByNameConfirmation`](#SetChannelByNameConfirmation) message.

### Payload field

| Field name       | Type    | Field description                     | Required |
|---------------|---------|-----------------------------|---------|
| `accessToken`   | string | The access token for the user's IoT service account. CEK forwards the access token by obtaining it from the authorization server of the 3rd party service. See [Linking user account](/CEK/Guides/LInk_User_Account.md) for more details.                          | Yes    |
| `appliance`     | [ApplianceInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#ApplianceInfoObject) | An object containing details of the target appliance. `applianceId` is a required field. | Yes    |
| `channelName`       | [TVChannelNameInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#TVChannelInfoObject) | An object containing the name of the current TV channel to be set on the target appliance.                | Yes    |

### Message example

{% raw %}

```json
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
```

{% endraw %}

### See also
* [`SetChannelByNameConfirmation`](#SetChannelByNameConfirmation)

## SetChannelConfirmation {#SetChannelConfirmation}
Returns CEK the result of setting the target appliance to change the TV channel by channel number in response to a [`SetChannelRequest`](#SetChannelRequest) message.

### Payload field

| Field name       | Type    | Field description                     | Required |
|---------------|---------|-----------------------------|---------|
| `channel`     | [TVChannelInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#TVChannelInfoObject)  | An object containing the TV channel set on the target appliance.      | Yes    |

### Message example

{% raw %}

```json
{
  "header": {
    "messageId": "4ec35000-88ce-4724-b7e4-7f52050558fd",
    "name": "SetChannelConfirmation",
    "namespace": "ClovaHome",
    "payloadVersion": "1.0"
  },
  "payload": {
    "channel": {
      "value":15
    }
  }
}
```

{% endraw %}

### See also
* [`SetChannelRequest`](#SetChannelRequest)

## SetChannelRequest {#SetChannelRequest}
Requests your Clova Home extension to set the target appliance to change the channel to a specified channel number. It is usually used to control appliances such as a TV set-top box. To respond to this request, use a [`SetChannelConfirmation`](#SetChannelConfirmation) message.

### Payload field

| Field name       | Type    | Field description                     | Required |
|---------------|---------|-----------------------------|---------|
| `accessToken`   | string | The access token for the user's IoT service account. CEK forwards the access token by obtaining it from the authorization server of the 3rd party service. See [Linking user account](/CEK/Guides/LInk_User_Account.md) for more details.                          | Yes    |
| `appliance`     | [ApplianceInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#ApplianceInfoObject) | An object containing details of the target appliance. `applianceId` is a required field. | Yes    |
| `channel`       | [TVChannelInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#TVChannelInfoObject) | An object containing the current TV channel to be set on the target appliance.                | Yes    |

### Message example

{% raw %}

```json
{
  "header": {
    "messageId": "6c04fc2d-64dd-41a0-9162-7cb0d4cf7c08",
    "name": "SetChannelRequest",
    "namespace": "ClovaHome",
    "payloadVersion": "1.0"
  },
  "payload": {
    "accessToken": "92ebcb67fe33",
    "appliance": {
      "applianceId": "device-006"
    },
    "channel": {
      "value": 15
    }
  }
}
```

{% endraw %}

### See also
* [`SetChannelConfirmation`](#SetChannelConfirmation)

## SetFanSpeedConfirmation {#SetFanSpeedConfirmation}
Returns CEK the result of setting the target appliance to adjust the fan speed in response to a [`SetFanSpeedRequest`](#SetFanSpeedRequest) message.

### Payload field

| Field name       | Type    | Field description                     | Required |
|---------------|---------|-----------------------------|---------|
| `fanSpeed`               | [SpeedInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#SpeedInfoObject) | An object containing the current fan speed                                | Yes    |


### Message example

{% raw %}

```json
{
  "header": {
    "messageId": "4ec35000-88ce-4724-b7e4-7f52050558fd",
    "name": "SetFanSpeedConfirmation",
    "namespace": "ClovaHome",
    "payloadVersion": "1.0"
  },
  "payload": {
    "fanSpeed": {
      "value": 2
    }
  }
}
```

{% endraw %}

### See also
* [`SetFanSpeedRequest`](#SetFanSpeedRequest)

## SetFanSpeedRequest {#SetFanSpeedRequest}
Requests your Clova Home extension to set the target appliance to change the fan speed to a specified value. It is usually used to control appliances such as an air purifier. To respond to this request, use an [`SetFanSpeedConfirmation`](#SetFanSpeedConfirmation) message.

### Payload field

| Field name       | Type    | Field description                     | Required |
|---------------|---------|-----------------------------|---------|
| `accessToken`   | string | The access token for the user's IoT service account. CEK forwards the access token by obtaining it from the authorization server of the 3rd party service. See [Linking user account](/CEK/Guides/LInk_User_Account.md) for more details.                          | Yes    |
| `appliance`     | [ApplianceInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#ApplianceInfoObject) | An object containing details of the target appliance. `applianceId` is a required field. | Yes    |
| `fanSpeed`       | [SpeedInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#SpeedInfoObject) | An object containing the current fan speed to be set on the target appliance.                | Yes    |

### Message example

{% raw %}

```json
{
  "header": {
    "messageId": "6c04fc2d-64dd-41a0-9162-7cb0d4cf7c08",
    "name": "SetFanSpeedRequest",
    "namespace": "ClovaHome",
    "payloadVersion": "1.0"
  },
  "payload": {
    "accessToken": "92ebcb67fe33",
    "appliance": {
      "applianceId": "device-004"
    },
    "fanSpeed": {
      "value": 2
    }
  }
}
```

{% endraw %}

### See also
* [`SetFanSpeedConfirmation`](#SetFanSpeedConfirmation)

## SetLockStateConfirmation {#SetLockStateConfirmation}
Returns the result of setting the target appliance to lock or unlock in response to the [`SetLockStateRequest`](#SetLockStateRequest) message sent from CEK.

### Payload field

| Field name       | Type    | Field description                     | Required |
|---------------|---------|-----------------------------|---------|
| `lockState`   | string  |Lock state of the appliance. Available values are: <ul><li><code>"LOCKED"</code></li><li><code>"UNLOCKED"</code></li></ul> | Yes    |


### Message example

{% raw %}

```json
{
  "header": {
    "messageId": "4ec35000-88ce-4724-b7e4-7f52050558fd",
    "name": "SetLockStateConfirmation",
    "namespace": "ClovaHome",
    "payloadVersion": "1.0"
  },
  "payload": {
    "lockState": "LOCKED"
  }
}
```

{% endraw %}

### See also
* [`SetLockStateRequest`](#SetLockStateRequest)

## SetLockStateRequest {#SetLockStateRequest}
Requests Clova Home extension to lock or unlock the target appliance. It is usually used to control appliances such as a smart valve. To respond to this request, use a [`SetLockStateConfirmation`](#SetLockStateConfirmation) message.

### Payload field

| Field name       | Type    | Field description                     | Required |
|---------------|---------|-----------------------------|---------|
| `accessToken`   | string | The access token for the user's IoT service account. CEK forwards the access token by obtaining it from the authorization server of the 3rd party service. See [Linking user account](/CEK/Guides/LInk_User_Account.md) for more details.                          | Yes    |
| `appliance`     | [ApplianceInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#ApplianceInfoObject) | An object containing details of the target appliance. `applianceId` is a required field. | Yes    |
| `lockState`       Lock state of the appliance. Available values are: <ul><li><code>"LOCKED"</code></li><li><code>"UNLOCKED"</code></li></ul> | Yes    |

### Message example

{% raw %}

```json
{
  "header": {
    "messageId": "6c04fc2d-64dd-41a0-9162-7cb0d4cf7c08",
    "name": "SetLockStateRequest",
    "namespace": "ClovaHome",
    "payloadVersion": "1.0"
  },
  "payload": {
    "accessToken": "92ebcb67fe33",
    "appliance": {
      "applianceId": "device-012"
    },
    "lockState": "LOCKED"
  }
}
```

{% endraw %}

### See also
* [`SetLockStateConfirmation`](#SetLockStateConfirmation)

## SetModeConfirmation {#SetModeConfirmation}
Returns CEK the result of setting the target appliance to change the heating mode, in response to a [`SetModeRequest`](#SetModeRequest) message.

### Payload field

| Field name       | Type    | Field description                     | Required |
|---------------|---------|-----------------------------|---------|
| `mode`        | [HeatingModeInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#HeatingModeInfoObject)  | An object containing the heating mode set on the target appliance.      | Yes    |

### Message example

{% raw %}

```json
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

### See also
* [`SetModeRequest`](#SetModeRequest)

## SetModeRequest {#SetModeRequest}
Requests your Clova Home extension to change the heating mode to a specified value. It is usually used to control appliances such as a heating system. To respond to this request, use a [`SetModeConfirmation`](#SetModeConfirmation) message.

### Payload field

| Field name       | Type    | Field description                     | Required |
|---------------|---------|-----------------------------|---------|
| `accessToken` | string  | The access token for the user's IoT service account. CEK forwards the access token by obtaining it from the authorization server of the 3rd party service. See [Linking user account](/CEK/Guides/LInk_User_Account.md) for more details. | Yes    |
| `appliance`   | [ApplianceInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#ApplianceInfoObject)     | An object containing details of the target appliance. `applianceId` is a required field. | Yes    |
| `mode`        | [HeatingModeInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#HeatingModeInfoObject) | An object containing the heating mode to set on the target appliance                         | Yes    |

### Message example

{% raw %}

```json
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
```

{% endraw %}

### See also
* [`SetModeConfirmation`](#SetModeConfirmation)

## SetTargetTemperatureConfirmation {#SetTargetTemperatureConfirmation}
Returns CEK the result of setting the target appliance to change the target temperature in response to a [`SetTargetTemperatureRequest`](#SetTargetTemperatureRequest) message.

### Payload field

| Field name       | Type    | Field description                     | Required |
|---------------|---------|-----------------------------|---------|
| `targetTemperature`               | [TemperatureInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#TemperatureInfoObject) | An object containing the current target temperature                                | Yes    |

### Message example

{% raw %}

```json
{
  "header": {
    "messageId": "4ec35000-88ce-4724-b7e4-7f52050558fd",
    "name": "SetTargetTemperatureConfirmation",
    "namespace": "ClovaHome",
    "payloadVersion": "1.0"
  },
  "payload": {
    "targetTemperature": {
      "value": 22.0
    }
  }
}
```

{% endraw %}

### See also
* [`SetTargetTemperatureRequest`](#SetTargetTemperatureRequest)

## SetTargetTemperatureRequest {#SetTargetTemperatureRequest}
Requests your Clova Home extension to set the target appliance to change the temperature to a specified value. It is usually used to control appliances such as an air conditioner or a temperature controller. To respond to this request, use an [`SetTargetTemperatureConfirmation`](#SetTargetTemperatureConfirmation) message.

### Payload field

| Field name       | Type    | Field description                     | Required |
|---------------|---------|-----------------------------|---------|
| `accessToken`   | string | The access token for the user's IoT service account. CEK forwards the access token by obtaining it from the authorization server of the 3rd party service. See [Linking user account](/CEK/Guides/LInk_User_Account.md) for more details.                          | Yes    |
| `appliance`     | [ApplianceInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#ApplianceInfoObject) | An object containing details of the target appliance. `applianceId` is a required field. | Yes    |
| `targetTemperature`       | [TemperatureInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#TemperatureInfoObject) | An object containing the target temperature that is to be set on the target appliance.                | Yes    |

### Message example

{% raw %}

```json
{
  "header": {
    "messageId": "6c04fc2d-64dd-41a0-9162-7cb0d4cf7c08",
    "name": "SetTargetTemperatureRequest",
    "namespace": "ClovaHome",
    "payloadVersion": "1.0"
  },
  "payload": {
    "accessToken": "92ebcb67fe33",
    "appliance": {
      "applianceId": "device-001"
    },
    "targetTemperature": {
      "value": 22.0
    }
  }
}
```

{% endraw %}

### See also
* [`SetTargetTemperatureConfirmation`](#SetTargetTemperatureConfirmation)

## TurnOffConfirmation {#TurnOffConfirmation}
Returns CEK the result of setting the target appliance to turn off in response to a [`TurnOffRequest`](#TurnOffRequest) message.

### Payload field
None

### Message example

{% raw %}

```json
{
  "header": {
    "messageId": "4ec35000-88ce-4724-b7e4-7f52050558fd",
    "name": "TurnOffConfirmation",
    "namespace": "ClovaHome",
    "payloadVersion": "1.0"
  },
  "payload": {}
}
```

{% endraw %}

### See also
* [`TurnOffRequest`](#TurnOffRequest)

## TurnOffRequest {#TurnOffRequest}
Requests your Clova Home extension to turn off the target appliance. To respond to this request, use a [`TurnOffConfirmation`](#TurnOffConfirmation) message.

### Payload field

| Field name       | Type    | Field description                     | Required |
|---------------|---------|-----------------------------|---------|
| `accessToken`      | string                                  | The access token for the user's IoT service account. CEK forwards the access token by obtaining it from the authorization server of the 3rd party service. See [Linking user account](/CEK/Guides/LInk_User_Account.md) for more details.                          | Yes    |
| `appliance`        | [ApplianceInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#ApplianceInfoObject)     | An object containing details of the target appliance. `applianceId` is a required field. | Yes    |

### Message example

{% raw %}

```json
{
  "header": {
    "messageId": "6c04fc2d-64dd-41a0-9162-7cb0d4cf7c08",
    "name": "TurnOffRequest",
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

### See also
* [`TurnOffConfirmation`](#TurnOffConfirmation)

## TurnOnConfirmation {#TurnOnConfirmation}
Returns CEK the result of setting the target appliance to turn on, in response to a [`TurnOnRequest`](#TurnOnRequest) message.

### Payload field
None

### Message example

{% raw %}

```json
{
  "header": {
    "messageId": "4ec35000-88ce-4724-b7e4-7f52050558fd",
    "name": "TurnOnConfirmation",
    "namespace": "ClovaHome",
    "payloadVersion": "1.0"
  },
  "payload": {}
}
```

{% endraw %}

### See also
* [`TurnOnRequest`](#TurnOnRequest)

## TurnOnRequest {#TurnOnRequest}
Requests your Clova Home extension to turn on the target appliance. To respond to this request, use a [`TurnOnConfirmation`](#TurnOnConfirmation) message.

### Payload field

| Field name       | Type    | Field description                     | Required |
|---------------|---------|-----------------------------|---------|
| `accessToken`      | string                                  | The access token for the user's IoT service account. CEK forwards the access token by obtaining it from the authorization server of the 3rd party service. See [Linking user account](/CEK/Guides/LInk_User_Account.md) for more details.                          | Yes    |
| `appliance`        | [ApplianceInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#ApplianceInfoObject)     | An object containing details of the target appliance. `applianceId` is a required field. | Yes    |

### Message example

{% raw %}

```json
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

### See also
* [`TurnOnConfirmation`](#TurnOnConfirmation)

## UnmuteConfirmation {#UnmuteConfirmation}
Returns CEK the result of setting the target appliance to turn on the sound (to unmute) in response to a [`UnmuteRequest`](#UnmuteRequest) message.

### Payload field
None

### Message example

{% raw %}

```json
{
  "header": {
    "messageId": "4ec35000-88ce-4724-b7e4-7f52050558fd",
    "name": "UnmuteConfirmation",
    "namespace": "ClovaHome",
    "payloadVersion": "1.0"
  },
  "payload": {}
}
```

{% endraw %}

### See also
* [`UnmuteRequest`](#UnmuteRequest)

## UnmuteRequest {#UnmuteRequest}
Requests your Clova Home extension to turn on the sound (to unmute) of the target appliance. It is usually used to control appliances such as a TV or a set-top box. To respond to this request, use a [`UnmuteConfirmation`](#UnmuteConfirmation) message.

### Payload field

| Field name       | Type    | Field description                     | Required |
|---------------|---------|-----------------------------|---------|
| `accessToken`      | string                                  | The access token for the user's IoT service account. CEK forwards the access token by obtaining it from the authorization server of the 3rd party service. See [Linking user account](/CEK/Guides/LInk_User_Account.md) for more details.                          | Yes    |
| `appliance`        | [ApplianceInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#ApplianceInfoObject)     | An object containing details of the target appliance. `applianceId` is a required field. | Yes    |

### Message example

{% raw %}

```json
{
  "header": {
    "messageId": "6c04fc2d-64dd-41a0-9162-7cb0d4cf7c08",
    "name": "UnmuteRequest",
    "namespace": "ClovaHome",
    "payloadVersion": "1.0"
  },
  "payload": {
    "accessToken": "92ebcb67fe33",
    "appliance": {
      "applianceId": "device-005"
    }
  }
}
```

{% endraw %}

### See also
* [`UnmuteConfirmation`](#UnmuteConfirmation)
