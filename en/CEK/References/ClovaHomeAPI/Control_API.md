## Control API {#ControlAPI}

Processes requests and responses related to obtaining information of IoT appliances or controlling IoT appliances.

| Message name  | Message type  | Message description  |
|------------------|-----------|---------------------------------------------|
| [`DecrementFanSpeedConfirmation`](#DecrementFanSpeedConfirmation)  | Response | Returns CEK the result of setting the target appliance to reduce the fan speed, in response to a [`DecrementFanSpeedRequest`](#DecrementFanSpeedRequest) message. |
| [`DecrementFanSpeedRequest`](#DecrementFanSpeedRequest)  | Response | Requests your Clova Home extension to set the target appliance to reduce the fan speed by a specified value. |
| [`DecrementTargetTemperatureConfirmation`](#DecrementTargetTemperatureConfirmation) | Response | Returns CEK the result of setting the target appliance to reduce the temperature, in response to a [`DecrementTargetTemperatureRequest`](#DecrementTargetTemperatureRequest) message. |
| [`DecrementTargetTemperatureRequest`](#DecrementTargetTemperatureRequest)  | Request | Requests your Clova Home extension to set the target appliance to reduce the temperature by a specified value.  |
| [`DecrementVolumeConfirmation`](#DecrementVolumeConfirmation)  | Response | Returns CEK the result of setting the target appliance to turn down the speaker volume, in response to a [`DecrementVolumeRequest`](#DecrementVolumeRequest) message. |
| [`DecrementVolumeRequest`](#DecrementVolumeRequest)  | Response | Requests your Clova Home extension to set the target appliance to turn down the speaker volume by a specified value. |
| [`HealthCheckRequest`](#HealthCheckRequest)  | Request  | Requests your Clova Home extension to check the state of the target appliance. |
| [`HealthCheckResponse`](#HealthCheckResponse)  | Response | Returns CEK the state of the target appliance, in response to a [`HealthCheckRequest`](#HealthCheckRequest) message. |
| [`IncrementFanSpeedConfirmation`](#IncrementFanSpeedConfirmation)  | Response | Returns CEK the result of setting the target appliance to raise the fan speed, in response to a[`IncrementFanSpeedRequest`](#IncrementFanSpeedRequest) message. |
| [`IncrementFanSpeedRequest`](#IncrementFanSpeedRequest)  | Response | Requests your Clova Home extension to set the target appliance to raise the fan speed by a specified value. |
| [`IncrementTargetTemperatureConfirmation`](#IncrementTargetTemperatureConfirmation) | Response | Returns CEK the result of setting the target appliance to raise the temperature, in response to a [`IncrementTargetTemperatureRequest`](#IncrementTargetTemperatureRequest) message. |
| [`IncrementTargetTemperatureRequest`](#IncrementTargetTemperatureRequest)  | Request  | Requests your Clova Home extension to set the target appliance to raise the temperature by a specified value.  |
| [`IncrementVolumeConfirmation`](#IncrementVolumeConfirmation)  | Response | Returns CEK the result of setting the target appliance to turn up the speaker volume, in response to a [`IncrementVolumeRequest`](#IncrementVolumeRequest) message. |
| [`IncrementVolumeRequest`](#IncrementVolumeRequest)  | Response | Requests your Clova Home extension to set the target appliance to turn up the speaker volume by a specified value. |
| [`SetChannelConfirmation`](#SetChannelConfirmation)  | Request  | Returns CEK the result of setting the target appliance to change the TV channel, in response to a [`SetChannelRequest`](#SetChannelRequest) message. |
| [`SetChannelRequest`](#SetChannelRequest)  | Request  | Requests your Clova Home extension to set the target appliance to change to a specified TV channel. |
| [`SetModeConfirmation`](#SetModeConfirmation)  | Request  | Returns CEK the result of setting the heating system to change the mode, in response to a [`SetModeRequest`](#SetModeRequest) message. |
| [`SetModeRequest`](#SetModeRequest)  | Request  | Requests your Clova Home extension to set the target appliace to change to a specified heating mode. |
| [`TurnOffConfirmation`](#TurnOffConfirmation)  | Response | Returns CEK the result of setting the target appliance to turn off, in response to a [`TurnOffRequest`](#TurnOffRequest) message. |
| [`TurnOffRequest`](#TurnOffRequest)  | Request  | Requests your Clova Home extension to turn off the target appliance.  |
| [`TurnOnConfirmation`](#TurnOnConfirmation)  | Response | Returns CEK the result of setting the target appliance to turn on, in response to a [`TurnOnRequest`](#TurnOnRequest) message. |
| [`TurnOnRequest`](#TurnOnRequest)  | Request  | Requests your Clova Home extension to turn on the target appliance.  |

### DecrementFanSpeedConfirmation {#DecrementFanSpeedConfirmation}
Returns CEK the result of setting the target appliance to reduce the fan speed, in response to a [`DecrementFanSpeedRequest`](#DecrementFanSpeedRequest) message.

#### Payload field

| Field name  | Type  | Field description  | Required |
|---------------|---------|-----------------------------|---------|
| `targetFanSpeed`  | [SpeedObject](#SpeedObject)  | An object containing the current speed  | Yes  |
| `previousState`  | object  | An object containing the previous state of the appliance  | Yes  |
| `previousState.targetFanSpeed` | [SpeedObject](#SpeedObject)  | An object containing the previous speed  | Yes  |

#### Message example

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
    "targetFanSpeed": {
      "value": 2
    },
    "previousState": {
      "targetFanSpeed": {
        "value": 4
      }
    }
  }
}
```
{% endraw %}

#### See also
* [`DecrementFanSpeedRequest`](#DecrementFanSpeedRequest)

### DecrementFanSpeedRequest {#DecrementFanSpeedRequest}
Requests your Clova Home extension to set the target appliance to reduce the fan speed by a specified value. It is usually used to control appliances such as an air purifier. To respond to this request, use a [`DecrementFanSpeedConfirmation`](#DecrementFanSpeedConfirmation) message.

#### Payload field

| Field name  | Type  | Field description  | Required |
|---------------|---------|-----------------------------|---------|
| `accessToken`  | string  | The access token for the user's IoT service account. CEK forwards the access token by obtaining it from the authorization server of the 3rd party service. See [Linking user account](/CEK/Guides/LinkUserAccount.md) for more details.  | Yes  |
| `appliance`  | [ApplianceObject](#ApplianceObject)  | An object containing information of the target appliance. `applianceId` is a required field.  | Yes  |
| `deltaFanSpeed`  | [SpeedObject](#SpeedObject)  | An object containing the expected change in the value of the speed.  | Yes  |

#### Message example

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

#### See also
* [`DecrementFanSpeedConfirmation`](#DecrementFanSpeedConfirmation)

### DecrementTargetTemperatureConfirmation {#DecrementTargetTemperatureConfirmation}
Returns CEK the result of setting the target appliance to reduce the temperature, in response to a [`DecrementTargetTemperatureRequest`](#DecrementTargetTemperatureRequest) message.

#### Payload field

| Field name  | Type  | Field description  | Required |
|---------------|---------|-----------------------------|---------|
| `targetTemperature` | [TemperatureObject](#TemperatureObject) | An object containing the current target temperature  | Yes  |
| `previousState`  | object  | An object containing the previous state of the appliance  | Yes  |
| `previousState.targetTemperature` | [TemperatureObject](#TemperatureObject) | An object containing the previous target temperature  | Yes  |

#### Message example

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

#### See also
* [`DecrementTargetTemperatureRequest`](#DecrementTargetTemperatureRequest)

### DecrementTargetTemperatureRequest {#DecrementTargetTemperatureRequest}
Requests Clova Home extension to set the target appliance to reduce the temperature by a specified value. It is usually used to control appliances such as an air conditioner. To respond to this request, use a [`DecrementTargetTemperatureConfirmation`](#DecrementTargetTemperatureConfirmation) message.

#### Payload field

| Field name  | Type  | Field description  | Required |
|---------------|---------|-----------------------------|---------|
| `accessToken`  | string  | The access token for the user's IoT service account. CEK forwards the access token by obtaining it from the authorization server of the 3rd party service. See [Linking user account](/CEK/Guides/LinkUserAccount.md) for more details.  | Yes  |
| `appliance`  | [ApplianceObject](#ApplianceObject)  | An object containing information of the target appliance. `applianceId` is a required field. | Yes  |
| `deltaTemperature` | [TemperatureObject](#TemperatureObject) | An object containing the expected change in the value of the temperature.  | Yes  |

#### Message example

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

#### See also
* [`DecrementTargetTemperatureConfirmation`](#DecrementTargetTemperatureConfirmation)

### DecrementVolumeConfirmation {#DecrementVolumeConfirmation}
Returns CEK the result of setting the target appliance to turn down the speaker volume, in response to a [`DecrementVolumeRequest`](#DecrementVolumeRequest) message.

#### Payload field

| Field name  | Type  | Field description  | Required |
|---------------|---------|-----------------------------|---------|
| `targetVolume`  | [VolumeObject](#SpeedObject)  | An object containing the current volume  | Yes  |
| `previousState`  | object  | An object containing the previous state of the appliance  | Yes  |
| `previousState.targetVolume` | [VolumeObject](#SpeedObject)  | An object containing the previous volume  | Yes  |

#### Message example

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

#### See also
* [`DecrementVolumeRequest`](#DecrementVolumeRequest)

### DecrementVolumeRequest {#DecrementVolumeRequest}
Requests your Clova Home extension to set the target appliance to turn down the speaker volume. It is usually used to control appliances such as a TV set-top box. To respond to this request, use a [`DecrementVolumeConfirmation`](#DecrementVolumeConfirmation) message.

#### Payload field

| Field name  | Type  | Field description  | Required |
|---------------|---------|-----------------------------|---------|
| `accessToken`  | string  | The access token for user's IoT service account. CEK forwards the access token by obtaining it from the authorization server of the 3rd party service. See [Linking user account](/CEK/Guides/LinkUserAccount.md) for more details.  | Yes  |
| `appliance`  | [ApplianceObject](#ApplianceObject)  | An object containing information of the target appliance. `applianceId` is a required field.  | Yes  |
| `deltaVolume`  | [VolumeObject](#VolumeObject)  | An object containing the expected change in the value of the volume.  | Yes  |

#### Message example

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

#### See also
* [`DecrementVolumeConfirmation`](#DecrementVolumeConfirmation)

### HealthCheckRequest {#HealthCheckRequest}
Requests your Clova Home extension to check the state of the target appliance. To respond to this request, use a [`HealthCheckResponse`](#HealthCheckResponse) message.

#### Payload field

| Field name  | Type  | Field description  | Required |
|---------------|---------|-----------------------------|---------|
| `accessToken`  | string  | The access token for the Clova Home extension | Yes  |
| `appliance`  | [ApplianceObject](#ApplianceObject)  | An object containing information of the target appliance. `applianceId` is a required field.  | Yes  |

#### Message example

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

#### See also
* [`HealthCheckResponse`](#HealthCheckResponse)

### HealthCheckResponse {#HealthCheckResponse}
Returns CEK the state of the target appliance, in response to a [`HealthCheckRequest`](#HealthCheckRequest) message.

#### Payload field

| Field name  | Type  | Field description  | Required |
|---------------|---------|-----------------------------|---------|
| `isReachable` | boolean | A value that indicates whether the target appliance is reachable through network. <ul><li><strong>true</strong>: Reachable (online)</li><li><strong>false</strong>: Not reachable (offline)</li></ul> | Yes  |
| `isTurnOn`  | boolean | A value that indicates the working state of the target appliance. <ul><li><strong>true</strong>: Idle</li><li><strong>false</strong>: Working</li></ul>  | Yes  |

#### Message example

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

#### See also
* [`HealthCheckRequest`](#HealthCheckRequest)

### IncrementFanSpeedConfirmation {#IncrementFanSpeedConfirmation}
Returns CEK the result of setting the target appliance to raise the fan speed, in response to a [`IncrementFanSpeedRequest`](#IncrementFanSpeedRequest) message.

#### Payload field

| Field name  | Type  | Field description  | Required |
|---------------|---------|-----------------------------|---------|
| `targetFanSpeed`  | [SpeedObject](#SpeedObject) | An object containing the current fan speed  | Yes  |
| `previousState`  | object  | An object containing the previous state of the appliance  | Yes  |
| `previousState.FanSpeed` | [SpeedObject](#SpeedObject) | An object containing the previous fan speed  | Yes  |

#### Message example

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
* [`IncrementFanSpeedRequest`](#IncrementFanSpeedRequest)

### IncrementFanSpeedRequest {#IncrementFanSpeedRequest}
Requests your Clova Home extension to set the target appliance to raise the fan speed by a specified value. It is usually used to control appliances such as an air purifier. To respond to this request, use a [`IncrementFanSpeedConfirmation`](#IncrementFanSpeedConfirmation) message.

#### Payload field

| Field name  | Type  | Field description  | Required |
|---------------|---------|-----------------------------|---------|
| `accessToken`  | string  | The access token for the user's IoT service account. CEK forwards the access token by obtaining it from the authorization server of the 3rd party service. See [Linking user account](/CEK/Guides/LinkUserAccount.md) for more details.  | Yes  |
| `appliance`  | [ApplianceObject](#ApplianceObject)  | An object containing information of the target appliance. `applianceId` is a required field. | Yes  |
| `deltaFanSpeed` | [SpeedObject](#SpeedObject) | An object containing the expected change in the value of the speed.  | Yes  |

#### Message example

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

#### See also
* [`IncrementFanSpeedConfirmation`](#IncrementFanSpeedConfirmation)

### IncrementTargetTemperatureConfirmation {#IncrementTargetTemperatureConfirmation}
Returns CEK the result of setting the target appliance to raise the temperature, in response to a [`IncrementTargetTemperatureRequest`](#IncrementTargetTemperatureRequest) message.

#### Payload field

| Field name  | Type  | Field description  | Required |
|---------------|---------|-----------------------------|---------|
| `targetTemperature` | [TemperatureObject](#TemperatureObject) | An object containing the current target temperature  | Yes  |
| `previousState`  | object  | An object containing the previous state of the appliance  | Yes  |
| `previousState.targetTemperature` | [TemperatureObject](#TemperatureObject) | An object containing the previous target temperature  | Yes  |

#### Message example

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

#### See also
* [`IncrementTargetTemperatureRequest`](#IncrementTargetTemperatureRequest)

### IncrementTargetTemperatureRequest {#IncrementTargetTemperatureRequest}
Requests your Clova Home extension to set the target appliance to raise the temperature by a specified value. It is usually used to control appliances such as an air conditioner. To respond to this request, use an [`IncrementTargetTemperatureConfirmation`](#IncrementTargetTemperatureConfirmation) message.

#### Payload field

| Field name  | Type  | Field description  | Required |
|---------------|---------|-----------------------------|---------|
| `accessToken`  | string | The access token for the user's IoT service account. CEK forwards the access token by obtaining it from the authorization server of the 3rd party service. See [Linking user account](/CEK/Guides/LinkUserAccount.md) for more details. | Yes  |
| `appliance`  | [ApplianceObject](#ApplianceObject)  | An object containing information of the target appliance. `applianceId` is a required field. | Yes  |
| `deltaTemperature` | [TemperatureObject](#TemperatureObject) | An object containing the expected change in the value of the temperature.  | Yes  |

#### Message example

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

#### See also
* [`IncrementTargetTemperatureConfirmation`](#IncrementTargetTemperatureConfirmation)

### IncrementVolumeConfirmation {#IncrementVolumeConfirmation}
Returns CEK the result of setting the target appliance to turn up the speaker volume, in response to an [`IncrementVolumeRequest`](#IncrementVolumeRequest) message.

#### Payload field

| Field name  | Type  | Field description  | Required |
|---------------|---------|-----------------------------|---------|
| `targetVolume` | [VolumeObject](#VolumeObject)  | An object containing the current volume  | Yes  |
| `previousState`  | object  | An object containing the previous state of the appliance  | Yes  |
| `previousState.targetVolume` | [VolumeObject](#VolumeObject) | An object containing the previous volume  | Yes  |

#### Message example

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

#### See also
* [`IncrementVolumeRequest`](#IncrementVolumeRequest)

### IncrementVolumeRequest {#IncrementVolumeRequest}
Requests your Clova Home extension to set the target appliance to turn up the speaker volume by a specified value. It is usually used to control appliances such as a TV set-top box. To respond to this request, use an [`IncrementVolumeConfirmation`](#IncrementVolumeConfirmation) message.

#### Payload field

| Field name  | Type  | Field description  | Required |
|---------------|---------|-----------------------------|---------|
| `accessToken`  | string  | The access token for the user's IoT service account. CEK forwards the access token by obtaining it from the authorization server of the 3rd party service. See [Linking user account](/CEK/Guides/LinkUserAccount.md) for more details.  | Yes  |
| `appliance`  | [ApplianceObject](#ApplianceObject)  | An object containing information of the target appliance. `applianceId` is a required field. | Yes  |
| `deltaVolume` | [VolumeObject](#VolumeObject)  | An object containing the expected change in the value of the temperature.  | Yes  |

#### Message example

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

#### See also
* [`IncrementVolumeConfirmation`](#IncrementVolumeConfirmation)

### SetChannelConfirmation {#SetChannelConfirmation}
Returns CEK the result of setting the target appliance to change the TV channel, in response to a [`SetChannelRequest`](#SetChannelRequest) message.

#### Payload field

| Field name  | Type  | Field description  | Required |
|---------------|---------|-----------------------------|---------|
| `channel`  | [TVChannelObject](#TVChannelObject)  | An object containing the TV channel set on the target appliance.  | Yes  |

#### Message example

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

#### See also
* [`SetChannelRequest`](#SetChannelRequest)

### SetChannelRequest {#SetChannelRequest}
Requests your Clova Home extension to set the target appliance to change to a specified channel. It is usually used to control appliances such as a TV set-top box. To respond to this request, use a [`SetChannelConfirmation`](#SetChannelConfirmation) message.

#### Payload field

| Field name  | Type  | Field description  | Required |
|---------------|---------|-----------------------------|---------|
| `accessToken`  | string | The access token for the user's IoT service account. CEK forwards the access token by obtaining it from the authorization server of the 3rd party service. See [Linking user account](/CEK/Guides/LinkUserAccount.md) for more details.  | Yes  |
| `appliance`  | [ApplianceObject](#ApplianceObject) | An object containing information of the target appliance. `applianceId` is a required field. | Yes  |
| `channel`  | [TVChannelObject](#TVChannelObject) | An object containing the TV channel to set on the target appliance.  | Yes  |

#### Message example

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

#### See also
* [`SetChannelConfirmation`](#SetChannelConfirmation)

### SetModeConfirmation {#SetModeConfirmation}
Returns CEK the result of setting the target appliance to change the heating mode, in response to a [`SetModeRequest`](#SetModeRequest) message.

#### Payload field

| Field name  | Type  | Field description  | Required |
|---------------|---------|-----------------------------|---------|
| `mode`  | [HeatingModeObject](#HeatingModeObject)  | An object containing the heating mode set on the target appliance.  | Yes  |

#### Message example

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

#### See also
* [`SetModeRequest`](#SetModeRequest)

### SetModeRequest {#SetModeRequest}
Requests your Clova Home extension to change the heating mode to a specified value. It is usually used to control appliances such as a heating system. To respond to this request, use a [`SetModeConfirmation`](#SetModeConfirmation) message.

#### Payload field

| Field name  | Type  | Field description  | Required |
|---------------|---------|-----------------------------|---------|
| `accessToken`| string  | The access token for the user's IoT service account. CEK forwards the access token by obtaining it from the authorization server of the 3rd party service. See [Linking user account](/CEK/Guides/LinkUserAccount.md) for more details. | Yes  |
| `appliance`  | [ApplianceObject](#ApplianceObject)  | An object containing information of the target appliance. `applianceId` is a required field. | Yes  |
| `mode`  | [HeatingModeObject](#HeatingModeObject) | An object containing the heating mode to set on the target appliance  | Yes  |

#### Message example

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

#### See also
* [`SetModeConfirmation`](#SetModeConfirmation)

### TurnOffConfirmation {#TurnOffConfirmation}
Returns CEK the result of setting the target appliance to turn off, in response to a [TurnOffRequest](#TurnOffRequest) message.

#### Payload field
None

#### Message example

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

#### See also
* [`TurnOffRequest`](#TurnOffRequest)

### TurnOffRequest {#`TurnOffRequest`}
Requests your Clova Home extension to turn off the target appliance. To respond to this request, use a [`TurnOffConfirmation`](#TurnOffConfirmation) message.

#### Payload field

| Field name  | Type  | Field description  | Required |
|---------------|---------|-----------------------------|---------|
| `accessToken`  | string  | The access token for the user's IoT service account. CEK forwards the access token by obtaining it from the authorization server of the 3rd party service. See [Linking user account](/CEK/Guides/LinkUserAccount.md) for more details.  | Yes  |
| `appliance`  | [ApplianceObject](#ApplianceObject)  | An object containing information of the target appliance. `applianceId` is a required field. | Yes  |

#### Message example

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

#### See also
* [`TurnOffConfirmation`](#TurnOffConfirmation)

### TurnOnConfirmation {#TurnOnConfirmation}
Returns CEK the result of setting the target appliance to turn on, in response to a [`TurnOnRequest`](#TurnOnRequest) message.

#### Payload field
None

#### Message example

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

#### See also
* [`TurnOnRequest`](#TurnOnRequest)

### TurnOnRequest {#TurnOnRequest}
Requests your Clova Home extension to turn on the target appliance. To respond to this request, use a [`TurnOnConfirmation`](#TurnOnConfirmation) message.

#### Payload field

| Field name  | Type  | Field description  | Required |
|---------------|---------|-----------------------------|---------|
| `accessToken`  | string  | The access token for the user's IoT service account. CEK forwards the access token by obtaining it from the authorization server of the 3rd party service. See [Linking user account](/CEK/Guides/LinkUserAccount.md) for more details.  | Yes  |
| `appliance`  | [ApplianceObject](#ApplianceObject)  | An object containing information of the target appliance. `applianceId` is a required field. | Yes  |

#### Message example

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

#### See also
* [`TurnOnConfirmation`](#TurnOnConfirmation)
