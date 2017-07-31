## Control API {#ControlAPI}

This API is used for requests and responses related to obtaining information of IoT appliances or controlling IoT appliances.

| Message name         | Message type  | Message description                                   |
|------------------|-----------|---------------------------------------------|
| [DecrementTargetTemperatureRequest](#DecrementTargetTemperatureRequest)     | Request | Requests Clova Home extension to decrease temperature by a specified value on the target appliance.      |
| [DecrementTargetTemperatureConfirmation](#DecrementTargetTemperatureConfirmation) | Response | Returns the result of setting the target appliance to decrease temperature in response to the [DecrementTargetTemperatureRequest](#DecrementTargetTemperatureRequest) message sent from CEK. |
| [GetLockStateRequest](#GetLockStateRequest)                                 | Request  | Requests Clova Home extension to provide the current lock state of the target appliance.            |
| [GetLockStateResponse](#GetLockStateResponse)                               | Response | Returns the current lock state of the target appliance in response to the [GetLockStateRequest](#GetLockStateRequest) message sent from CEK. |
| [GetTargetTemperatureRequest](#GetTargetTemperatureRequest)                 | Request  | Requests Clova Home extension to provide the current target temperature set on the target appliance.            |
| [GetTargetTemperatureResponse](#GetTargetTemperatureResponse)               | Response | Returns the current target temperature set on the target appliance in response to the [GetTargetTemperatureRequest](#GetTargetTemperatureRequest) message sent from CEK. |
| [HealthCheckRequest](#HealthCheckRequest)                                   | Request  Clova sends health check request to Clova Home extension periodically to check connectivity with user appliance. |
| [HealthCheckResponse](#HealthCheckResponse)                                 | Response | Returns a list of appliance IDs that are currently reachable in response to the [HealthCheckRequest](#HealthCheckRequest) message sent from CEK. |
| [IncrementTargetTemperatureRequest](#IncrementTargetTemperatureRequest)     | Request  | Requests Clova Home extension to increase temperature by a specified value on the target appliance.     |
| [IncrementTargetTemperatureConfirmation](#IncrementTargetTemperatureConfirmation) | Response | Returns the result of setting the target appliance to increase temperature in response to the [IncrementTargetTemperatureRequest](#IncrementTargetTemperatureRequest) message sent from CEK. |
| [SetLockStateRequest](#SetLockStateRequest)                                 | Request  | Requests Clova Home extension to lock or unlock the target appliance.                 |
| [SetLockStateConfirmation](#SetLockStateConfirmation)                       | Response | Returns the result of setting the target appliance to lock or unlock in response to the [SetLockStateRequest](#SetLockStateRequest) message sent from CEK. |
| [TurnOffRequest](#TurnOffRequest)                                           | Request  | Requests Clova Home extension to turn off the target appliance.                        |
| [TurnOffConfirmation](#TurnOffConfirmation)                                 | Response | Returns the result of setting the target appliance to turn off in response to the [TurnOffRequest](#TurnOffRequest) message sent from CEK. |
| [TurnOnRequest](#TurnOnRequest)                                             | Request  | Requests Clova Home extension to turn on the target appliance.                        |
| [TurnOnConfirmation](#TurnOnConfirmation)                                   | Response | Returns the result of setting the target appliance to turn on in response to the [TurnOnRequest](#TurnOnRequest) message sent from CEK. |

### DecrementTargetTemperatureRequest {#DecrementTargetTemperatureRequest}
Requests Clova Home extension to decrease temperature by a specified value on the target appliance. It is usually used to controls appliances such as an air conditioner. Use a *[DecrementTargetTemperatureConfirmation](#DecrementTargetTemperatureConfirmation)* message to respond to this request.

#### Payload field

| Field name       | Type    | Field description                     | Required |
|---------------|---------|-----------------------------|---------|
| accessToken      | string                                  | Access token for the user account of IoT service. CEK forwards the access token obtained from the authorization server of 3rd party service. See [Linking user account](/CEK/Guides/LinkUserAccount.md) for more details.                          | Yes    |
| appliance        | [ApplianceObject](#ApplianceObject)     | Object containing information of the target appliance. applianceId is a required field. | Yes    |
| deltaTemperature | [TemperatureObject](#TemperatureObject) | Object containing the expected change in temperature.                              | Yes    |

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
* [DecrementTargetTemperatureConfirmation](#DecrementTargetTemperatureConfirmation)

### DecrementTargetTemperatureConfirmation {#DecrementTargetTemperatureConfirmation}
Returns the result of setting the target appliance to decrease temperature in response to the [DecrementTargetTemperatureRequest](#DecrementTargetTemperatureRequest) message sent from CEK.

#### Payload field

| Field name       | Type    | Field description                     | Required |
|---------------|---------|-----------------------------|---------|
| accessToken       | string                                  | Access token for the user account of IoT service. CEK forwards the access token obtained from the authorization server of 3rd party service. See [Linking user account](/CEK/Guides/LinkUserAccount.md) for more details.                          | Yes    |
| appliance         | [ApplianceObject](#ApplianceObject)     | Object containing information of the target appliance. applianceId is a required field. | Yes    |
| targetTemperature | [TemperatureObject](#TemperatureObject) | Object containing the current target temperature                            | Yes    |
| previousState     | object                                  | Object containing previous state of the appliance                           | Yes    |
| previousState.targetTemperature | [TemperatureObject](#TemperatureObject) | Object containing previous target temperature              | Yes    |

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
* [DecrementTargetTemperatureRequest](#DecrementTargetTemperatureRequest)

### GetLockStateRequest {#GetLockStateRequest}
Requests Clova Home extension to provide the current lock state of the target appliance. It is usually used to check state of appliances such as a door lock. Use a *[GetLockStateResponse](#GetLockStateResponse)* message to respond to this request.

#### Payload field

| Field name       | Type    | Field description                     | Required |
|---------------|---------|-----------------------------|---------|
| accessToken      | string                              | Access token for the user account of IoT service. CEK forwards the access token obtained from the authorization server of 3rd party service. See [Linking user account](/CEK/Guides/LinkUserAccount.md) for more details.                          | Yes    |
| appliance        | [ApplianceObject](#ApplianceObject) | Object containing information of the target appliance. applianceId is a required field. | Yes    |

#### Message example

{% raw %}
```json
{
  "header": {
    "messageId": "33da6561-0149-4532-a30b-e0de8f75c4cf",
    "name": "GetLockStateRequest",
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
* [GetLockStateResponse](#GetLockStateResponse)

### GetLockStateResponse {#GetLockStateResponse}
Returns the current lock state of a target appliance in response to a [GetLockStateRequest](#GetLockStateRequest) message sent from CEK.

#### Payload field

| Field name       | Type    | Field description                     | Required |
|---------------|---------|-----------------------------|---------|
| lockState                    | string  | Current lock state of the appliance. Available values are: <ul><li>"LOCKED"</li><li>"UNLOCKED"</li></ul>             | Yes    |
| applicanceResponseTimestamp  | string  | Time when lock state of the appliance was checked (Timestamp, [ISO 8061](https://en.wikipedia.org/wiki/ISO_8601))  | Yes    |

#### Message example

{% raw %}
```json
{
  "header":{
    "messageId":"19b29d5e-04b3-4524-a538-35ae77ea2618",
    "name":"GetLockStateResponse",
    "namespace":"ClovaHome",
    "payloadVersion":"1.0"
  },
  "payload":{
    "lockState":"LOCKED",
    "applianceResponseTimestamp":"2017-05-29T23:20:50.52Z"
  }
}
```
{% endraw %}

#### See also
* [GetLockStateRequest](#GetLockStateRequest)

### GetTargetTemperatureRequest {#GetTargetTemperatureRequest}
Requests Clova Home extension to provide the current target temperature set on the appliance. It is usually used to check state of appliances such as an air conditioner. Use a *[GetTargetTemperatureResponse](#GetTargetTemperatureResponse)* message to respond to this request.

#### Payload field

| Field name       | Type    | Field description                     | Required |
|---------------|---------|-----------------------------|---------|
| accessToken      | string                              | Access token for the user account of IoT service. CEK forwards the access token obtained from the authorization server of 3rd party service. See [Linking user account](/CEK/Guides/LinkUserAccount.md) for more details.                          | Yes    |
| appliance        | [ApplianceObject](#ApplianceObject) | Object containing information of the target appliance. applianceId is a required field. | Yes    |

#### Message example

{% raw %}
```json
{
  "header": {
    "messageId": "33da6561-0149-4532-a30b-e0de8f75c4cf",
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

#### See also
* [GetTargetTemperatureResponse](#GetTargetTemperatureResponse)

### GetTargetTemperatureResponse {#GetTargetTemperatureResponse}
Returns the current target temperature set on a target appliance in response to the [GetTargetTemperatureRequest](#GetTargetTemperatureRequest) message sent from CEK.

#### Payload field

| Field name       | Type    | Field description                     | Required |
|---------------|---------|-----------------------------|---------|
| targetTemperature            | [TemperatureObject](#TemperatureObject)  | Object containing the current target temperature                                  | Yes    |
| applicanceResponseTimestamp  | string  | Time when the target temperature on the appliance was checked (Timestamp, [ISO 8061](https://en.wikipedia.org/wiki/ISO_8601))  | Yes    |

#### Message example

{% raw %}
```json
{
  "header":{
    "messageId":"19b29d5e-04b3-4524-a538-35ae77ea2618",
    "name":"GetTargetTemperatureResponse",
    "namespace":"ClovaHome",
    "payloadVersion":"1.0"
  },
  "payload":{
    "targetTemperature": {
      "value": 24.0
    },
    "applianceResponseTimestamp":"2017-05-29T23:20:50.52Z"
  }
}
```
{% endraw %}

#### See also
* [GetTargetTemperatureRequest](#GetTargetTemperatureRequest)

### HealthCheckRequest {#HealthCheckRequest}
Clova sends this message to Clova Home extension periodically to check the connectivity with user appliance. Use a *[HealthCheckResponse](#HealthCheckResponse)* message to respond to this request.

#### Payload field

| Field name       | Type    | Field description                     | Required |
|---------------|---------|-----------------------------|---------|
| accessToken   | string  | Access token for Clova Home extension | Yes    |

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
    "accessToken": "92ebcb67fe33"
  }
}
```
{% endraw %}

#### See also
* [HealthCheckResponse](#HealthCheckResponse)

### HealthCheckResponse {#HealthCheckResponse}
Returns a list of appliance IDs that are currently reachable in response to the [HealthCheckRequest](#HealthCheckRequest) message sent from CEK.

#### Payload field

| Field name       | Type    | Field description                     | Required |
|---------------|---------|-----------------------------|---------|
| reachableAppliances[] | string array  | Array containing a list of appliance IDs that are currently reachable | Yes    |

#### Message example

{% raw %}
```json
{
  "header":{
    "messageId":"19b29d5e-04b3-4524-a538-35ae77ea2618",
    "name":"HealthCheckResponse",
    "namespace":"ClovaHome",
    "payloadVersion":"1.0"
  },
  "payload":{
    "reachableAppliances": [
        "devicd-001",
        "devicd-002"
    ]
  }
}
```
{% endraw %}

#### See also
* [GetLockStateRequest](#GetLockStateRequest)

### IncrementTargetTemperatureRequest {#IncrementTargetTemperatureRequest}
Requests Clova Home extension to increase temperature by a specified value on the target appliance. It is usually used to control appliances such as an air conditioner. Use a *[IncrementTargetTemperatureConfirmation](#IncrementTargetTemperatureConfirmation)* message to respond to this request.

#### Payload field

| Field name       | Type    | Field description                     | Required |
|---------------|---------|-----------------------------|---------|
| accessToken      | string                                  | Access token for the user account of IoT service. CEK forwards the access token obtained from the authorization server of 3rd party service. See [Linking user account](/CEK/Guides/LinkUserAccount.md) for more details.                          | Yes    |
| appliance        | [ApplianceObject](#ApplianceObject)     | Object containing information of the target appliance. applianceId is a required field. | Yes    |
| deltaTemperature | [TemperatureObject](#TemperatureObject) | Object containing the expected change in temperature.                              | Yes    |

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
* [IncrementTargetTemperatureConfirmation](#IncrementTargetTemperatureConfirmation)

### IncrementTargetTemperatureConfirmation {#IncrementTargetTemperatureConfirmation}
Returns the result of setting the temperature to increase on the target appliance in response to the [IncrementTargetTemperatureRequest](#IncrementTargetTemperatureRequest) message sent from CEK.

#### Payload field

| Field name       | Type    | Field description                     | Required |
|---------------|---------|-----------------------------|---------|
| accessToken      | string                                   | Access token for Clova Home extension                               | Yes    |
| appliance        | [ApplianceObject](#ApplianceObject)      | Object containing information of the target appliance. applianceId is a required field.    | Yes    |
| targetTemperature | [TemperatureObject](#TemperatureObject) | Object containing the current target temperature                               | Yes    |
| previousState     | object                                  | Object containing previous state of the appliance                              | Yes    |
| previousState.targetTemperature | [TemperatureObject](#TemperatureObject) | Object containing previous target temperature                 | Yes    |

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
* [IncrementTargetTemperatureRequest](#IncrementTargetTemperatureRequest)

### SetLockStateRequest {#SetLockStateRequest}
Requests Clova Home extension to lock or unlock the target appliance. It is usually used to control appliances such as a door lock. Use a *[SetLockStateConfirmation](#SetLockStateConfirmation)* message to respond to this request.

#### Payload field

| Field name       | Type    | Field description                     | Required |
|---------------|---------|-----------------------------|---------|
| accessToken      | string                                  | Access token for the user account of IoT service. CEK forwards the access token obtained from the authorization server of 3rd party service. See [Linking user account](/CEK/Guides/LinkUserAccount.md) for more details.                          | Yes    |
| appliance        | [ApplianceObject](#ApplianceObject)     | Object containing information of the target appliance. applianceId is a required field. | Yes    |
| lockState        | string                                  | Current lock state of the appliance. Available values are: <ul><li>"LOCKED"</li><li>"UNLOCKED"</li></ul> | Yes    |

#### Message example

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
      "applianceId": "device-001"
    },
    "lockState": "LOCKED"
  }
}
```
{% endraw %}

#### See also
* [SetLockStateConfirmation](#SetLockStateConfirmation)

### SetLockStateConfirmation {#SetLockStateConfirmation}
Returns the result of setting to lock or unlock the target appliance in response to the [SetLockStateRequest](#SetLockStateRequest) message sent from CEK.

#### Payload field

| Field name       | Type    | Field description                     | Required |
|---------------|---------|-----------------------------|---------|
| lockState     | string  | Current lock state of the appliance. Available values are: <ul><li>"LOCKED"</li><li>"UNLOCKED"</li></ul> | Yes    |

#### Message example

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

#### See also
* [SetLockStateRequest](#SetLockStateRequest)

### TurnOffRequest {#TurnOffRequest}
Requests Clova Home extension to turn off the target appliance. Use a *[TurnOffConfirmation](#TurnOffConfirmation)* message to respond to this request.

#### Payload field

| Field name       | Type    | Field description                     | Required |
|---------------|---------|-----------------------------|---------|
| accessToken      | string                                  | Access token for the user account of IoT service. CEK forwards the access token obtained from the authorization server of 3rd party service. See [Linking user account](/CEK/Guides/LinkUserAccount.md) for more details.                          | Yes    |
| appliance        | [ApplianceObject](#ApplianceObject)     | Object containing information of the target appliance. applianceId is a required field. | Yes    |

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
* [TurnOffConfirmation](#TurnOffConfirmation)

### TurnOffConfirmation {#TurnOffConfirmation}
Returns the result of setting the target appliance turn off in response to the [TurnOffRequest](#TurnOffRequest) message sent from CEK.

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
* [TurnOffRequest](#TurnOffRequest)

### TurnOnRequest {#TurnOnRequest}
Requests Clova Home extension to turn on the target appliance. Use a *[TurnOnConfirmation](#TurnOnConfirmation)* message to respond to this request.

#### Payload field

| Field name       | Type    | Field description                     | Required |
|---------------|---------|-----------------------------|---------|
| accessToken      | string                                  | Access token for the user account of IoT service. CEK forwards the access token obtained from the authorization server of 3rd party service. See [Linking user account](/CEK/Guides/LinkUserAccount.md) for more details.                          | Yes    |
| appliance        | [ApplianceObject](#ApplianceObject)     | Object containing information of the target appliance. applianceId is a required field. | Yes    |

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
* [TurnOnConfirmation](#TurnOnConfirmation)


### TurnOnConfirmation {#TurnOnConfirmation}
Returns the result of setting the target appliance to turn on in response to the [TurnOnRequest](#TurnOnRequest) message sent from CEK.

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
* [TurnOnRequest](#TurnOnRequest)