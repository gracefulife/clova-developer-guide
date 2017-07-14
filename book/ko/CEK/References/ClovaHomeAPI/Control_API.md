## Control API {#ControlAPI}

IoT 기기 정보 확인 및 기기 제어와 관련된 요청 및 응답을 수행할 때 사용되는 API입니다.

| 메시지 이름         | 메시지 타입  | 메시지 설명                                   |
|------------------|-----------|---------------------------------------------|
| [DecrementTargetTemperatureRequest](#DecrementTargetTemperatureRequest)     | Request | 대상 기기가 지정한 값만큼 온도를 낮추도록 Clova Home extension에게 요청합니다.      |
| [DecrementTargetTemperatureConfirmation](#DecrementTargetTemperatureConfirmation) | Response | [DecrementTargetTemperatureRequest](#DecrementTargetTemperatureRequest) 메시지에 대한 응답으로 대상 기기가 온도를 낮추도록 설정한 결과를 CEK에게 전달합니다. |
| [GetLockStateRequest](#GetLockStateRequest)                                 | Request  | 대상 기기의 현재 잠금 상태 정보를 Clova Home extension에게 요청합니다.            |
| [GetLockStateResponse](#GetLockStateResponse)                               | Response | [GetLockStateRequest](#GetLockStateRequest) 메시지에 대한 응답으로 대상 기기의 현재 잠금 상태를 CEK에게 전달합니다. |
| [GetTargetTemperatureRequest](#GetTargetTemperatureRequest)                 | Request  | 대상 기기에 설정된 희망 온도 값을 Clova Home extension에게 요청합니다.            |
| [GetTargetTemperatureResponse](#GetTargetTemperatureResponse)               | Response | [GetTargetTemperatureRequest](#GetTargetTemperatureRequest) 메시지에 대한 응답으로 대상 기기에 설정된 희망 온도 값을 CEK에게 전달합니다. |
| [HealthCheckRequest](#HealthCheckRequest)                                   | Request  | Clova가 사용자 기기의 연결 여부를 파악하기 위해 이 메시지를 주기적으로 Clova Home extension에게 보냅니다. |
| [HealthCheckResponse](#HealthCheckResponse)                                 | Response | [HealthCheckRequest](#HealthCheckRequest) 메시지에 대한 응답으로 현재 접근 가능한 사용자 기기의 ID 목록을 CEK에게 전달합니다. |
| [IncrementTargetTemperatureRequest](#IncrementTargetTemperatureRequest)     | Request  | 대상 기기가 지정한 값만큼 온도를 높이도록 Clova Home extension에게 요청합니다.     |
| [IncrementTargetTemperatureConfirmation](#IncrementTargetTemperatureConfirmation) | Response | [IncrementTargetTemperatureRequest](#IncrementTargetTemperatureRequest) 메시지에 대한 응답으로 대상 기기가 온도를 높이도록 설정한 결과를 CEK에게 전달합니다. |
| [SetLockStateRequest](#SetLockStateRequest)                                 | Request  | 대상 기기를 잠그거나 열도록 Clova Home extension에게 요청합니다.                 |
| [SetLockStateConfirmation](#SetLockStateConfirmation)                       | Response | [SetLockStateRequest](#SetLockStateRequest) 메시지에 대한 응답으로 대상 기기가 잠기거나 열리도록 설정한 결과를 CEK에게 전달합니다. |
| [TurnOffRequest](#TurnOffRequest)                                           | Request  | 대상 기기를 끄도록 Clova Home extension에게 요청합니다.                        |
| [TurnOffConfirmation](#TurnOffConfirmation)                                 | Response | [TurnOffRequest](#TurnOffRequest) 메시지에 대한 응답으로 대상 기기를 끄도록 설정한 결과를 CEK에게 전달합니다. |
| [TurnOnRequest](#TurnOnRequest)                                             | Request  | 대상 기기를 켜도록 Clova Home extension에게 요청합니다.                        |
| [TurnOnConfirmation](#TurnOnConfirmation)                                   | Response | [TurnOnRequest](#TurnOnRequest) 메시지에 대한 응답으로 대상 기기를 켜도록 설정한 결과를 CEK에게 전달합니다. |

### DecrementTargetTemperatureRequest {#DecrementTargetTemperatureRequest}
주로 에어컨과 같은 기기를 제어할 때 사용되며, 대상 기기가 지정한 값만큼 온도를 낮추도록 Clova Home extension에게 요청합니다. 이 요청에 대한 응답으로 *[DecrementTargetTemperatureConfirmation](#DecrementTargetTemperatureConfirmation)* 메시지를 사용해야 합니다.

#### Payload field

| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|---------|
| accessToken      | string                                  | IoT 서비스의 사용자 계정의 access token. CEK는 외부 서비스의 인증 서버로부터 획득한 사용자 계정의 access token을 전달합니다. 자세한 설명은 [사용자 계정 연결하기](/CEK/Guides/LinkUserAccount.md)를 참조합니다.                          | 필수    |
| appliance        | [ApplianceObject](#ApplianceObject)     | 대상 기기 정보를 담고 있는 객체. applianceId 필드는 필수입니다. | 필수    |
| deltaTemperature | [TemperatureObject](#TemperatureObject) | 변경할 온도 정보를 담고 있는 객체.                              | 필수    |

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
[DecrementTargetTemperatureRequest](#DecrementTargetTemperatureRequest) 메시지에 대한 응답으로 대상 기기가 온도를 낮추도록 설정한 결과를 CEK에게 전달합니다.

#### Payload field

| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|---------|
| accessToken       | string                                  | IoT 서비스의 사용자 계정의 access token. CEK는 외부 서비스의 인증 서버로부터 획득한 사용자 계정의 access token을 전달합니다. 자세한 설명은 [사용자 계정 연결하기](/CEK/Guides/LinkUserAccount.md)를 참조합니다.                          | 필수    |
| appliance         | [ApplianceObject](#ApplianceObject)     | 대상 기기 정보를 담고 있는 객체. applianceId 필드는 필수입니다. | 필수    |
| targetTemperature | [TemperatureObject](#TemperatureObject) | 현재 희망 온도 정보를 담고 있는 객체                            | 필수    |
| previousState     | object                                  | 기기의 이전 상황 정보를 담고 있는 객체                           | 필수    |
| previousState.targetTemperature | [TemperatureObject](#TemperatureObject) | 이전 희망 온도 정보를 담고 있는 객체              | 필수    |

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
주로 도어록과 같은 기기의 상태를 확인할 때 사용되며, 대상 기기의 현재 잠금 상태 정보를 Clova Home extension에게 요청합니다. 이 요청에 대한 응답으로 *[GetLockStateResponse](#GetLockStateResponse)* 메시지를 사용해야 합니다.

#### Payload field

| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|---------|
| accessToken      | string                              | IoT 서비스의 사용자 계정의 access token. CEK는 외부 서비스의 인증 서버로부터 획득한 사용자 계정의 access token을 전달합니다. 자세한 설명은 [사용자 계정 연결하기](/CEK/Guides/LinkUserAccount.md)를 참조합니다.                          | 필수    |
| appliance        | [ApplianceObject](#ApplianceObject) | 대상 기기 정보를 담고 있는 객체. applianceId 필드는 필수입니다. | 필수    |

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
[GetLockStateRequest](#GetLockStateRequest) 메시지에 대한 응답으로 대상 기기의 현재 잠금 상태를 CEK에게 전달합니다.

#### Payload field

| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|---------|
| lockState                    | string  | 기기의 잠금 상태. 다음과 같은 값을 가집니다. <ul><li>"LOCKED"</li><li>"UNLOCKED"</li></ul>             | 필수    |
| applicanceResponseTimestamp  | string  | 기기의 잠금 상태를 확인한 시간 (Timestamp, [ISO 8061](https://en.wikipedia.org/wiki/ISO_8601))  | 필수    |

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
주로 에어컨과 같은 기기의 상태를 확인할 때 사용되며, 대상 기기에 설정된 희망 온도 값을 Clova Home extension에게 요청합니다. 이 요청에 대한 응답으로 *[GetTargetTemperatureResponse](#GetTargetTemperatureResponse)* 메시지를 사용해야 합니다.

#### Payload field

| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|---------|
| accessToken      | string                              | IoT 서비스의 사용자 계정의 access token. CEK는 외부 서비스의 인증 서버로부터 획득한 사용자 계정의 access token을 전달합니다. 자세한 설명은 [사용자 계정 연결하기](/CEK/Guides/LinkUserAccount.md)를 참조합니다.                          | 필수    |
| appliance        | [ApplianceObject](#ApplianceObject) | 대상 기기 정보를 담고 있는 객체. applianceId 필드는 필수입니다. | 필수    |

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
[GetTargetTemperatureRequest](#GetTargetTemperatureRequest) 메시지에 대한 응답으로 대상 기기에 설정된 희망 온도 값을 CEK에게 전달합니다.

#### Payload field

| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|---------|
| targetTemperature            | [TemperatureObject](#TemperatureObject)  | 현재 설정된 희망 온도 정보를 담고 있는 객체                                  | 필수    |
| applicanceResponseTimestamp  | string  | 기기의 희망 온도를 확인한 시간 (Timestamp, [ISO 8061](https://en.wikipedia.org/wiki/ISO_8601))  | 필수    |

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
Clova가 사용자 기기의 연결 여부를 파악하기 위해 이 메시지를 주기적으로 Clova Home extension에게 보냅니다. 이 요청에 대한 응답으로 *[HealthCheckResponse](#HealthCheckResponse)* 메시지를 사용해야 합니다.

#### Payload field

| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|---------|
| accessToken   | string  | Clova Home extension의 access token | 필수    |

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
[HealthCheckRequest](#HealthCheckRequest) 메시지에 대한 응답으로 현재 접근 가능한 사용자 기기의 ID 목록을 CEK에게 전달합니다.

#### Payload field

| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|---------|
| reachableAppliances[] | string array  | 현재 접근 가능한 사용자 기기의 ID 목록을 가지는 배열 | 필수    |

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
주로 에어컨과 같은 기기를 제어할 때 사용되며, 대상 기기가 지정한 값만큼 온도를 높이도록 Clova Home extension에게 요청합니다. 이 요청에 대한 응답으로 *[IncrementTargetTemperatureConfirmation](#IncrementTargetTemperatureConfirmation)* 메시지를 사용해야 합니다.

#### Payload field

| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|---------|
| accessToken      | string                                  | IoT 서비스의 사용자 계정의 access token. CEK는 외부 서비스의 인증 서버로부터 획득한 사용자 계정의 access token을 전달합니다. 자세한 설명은 [사용자 계정 연결하기](/CEK/Guides/LinkUserAccount.md)를 참조합니다.                          | 필수    |
| appliance        | [ApplianceObject](#ApplianceObject)     | 대상 기기 정보를 담고 있는 객체. applianceId 필드는 필수입니다. | 필수    |
| deltaTemperature | [TemperatureObject](#TemperatureObject) | 변경할 온도 정보를 담고 있는 객체.                              | 필수    |

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
[IncrementTargetTemperatureRequest](#IncrementTargetTemperatureRequest) 메시지에 대한 응답으로 대상 기기가 온도를 높이도록 설정한 결과를 CEK에게 전달합니다.

#### Payload field

| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|---------|
| accessToken      | string                                   | Clova Home extension의 access token                               | 필수    |
| appliance        | [ApplianceObject](#ApplianceObject)      | 대상 기기 정보를 담고 있는 객체. applianceId 필드는 필수입니다.    | 필수    |
| targetTemperature | [TemperatureObject](#TemperatureObject) | 현재 희망 온도 정보를 담고 있는 객체                               | 필수    |
| previousState     | object                                  | 기기의 이전 상황 정보를 담고 있는 객체                              | 필수    |
| previousState.targetTemperature | [TemperatureObject](#TemperatureObject) | 이전 희망 온도 정보를 담고 있는 객체                 | 필수    |

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
주로 도어록과 같은 기기를 제어할 때 사용되며, 대상 기기를 잠그거나 열도록 Clova Home extension에게 요청합니다. 이 요청에 대한 응답으로 *[SetLockStateConfirmation](#SetLockStateConfirmation)* 메시지를 사용해야 합니다.

#### Payload field

| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|---------|
| accessToken      | string                                  | IoT 서비스의 사용자 계정의 access token. CEK는 외부 서비스의 인증 서버로부터 획득한 사용자 계정의 access token을 전달합니다. 자세한 설명은 [사용자 계정 연결하기](/CEK/Guides/LinkUserAccount.md)를 참조합니다.                          | 필수    |
| appliance        | [ApplianceObject](#ApplianceObject)     | 대상 기기 정보를 담고 있는 객체. applianceId 필드는 필수입니다. | 필수    |
| lockState        | string                                  | 설정할 기기의 잠금 상태. 다음과 같은 값을 가집니다. <ul><li>"LOCKED"</li><li>"UNLOCKED"</li></ul> | 필수    |

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
[SetLockStateRequest](#SetLockStateRequest) 메시지에 대한 응답으로 대상 기기가 잠기거나 열리도록 설정한 결과를 CEK에게 전달합니다.

#### Payload field

| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|---------|
| lockState     | string  | 기기의 잠금 상태. 다음과 같은 값을 가집니다. <ul><li>"LOCKED"</li><li>"UNLOCKED"</li></ul> | 필수    |

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
대상 기기를 끄도록 Clova Home extension에게 요청합니다. 이 요청에 대한 응답으로 *[TurnOffConfirmation](#TurnOffConfirmation)* 메시지를 사용해야 합니다.

#### Payload field

| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|---------|
| accessToken      | string                                  | IoT 서비스의 사용자 계정의 access token. CEK는 외부 서비스의 인증 서버로부터 획득한 사용자 계정의 access token을 전달합니다. 자세한 설명은 [사용자 계정 연결하기](/CEK/Guides/LinkUserAccount.md)를 참조합니다.                          | 필수    |
| appliance        | [ApplianceObject](#ApplianceObject)     | 대상 기기 정보를 담고 있는 객체. applianceId 필드는 필수입니다. | 필수    |

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
[TurnOffRequest](#TurnOffRequest) 메시지에 대한 응답으로 대상 기기를 끄도록 설정한 결과를 CEK에게 전달합니다.

#### Payload field
없음

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
대상 기기를 켜도록 Clova Home extension에게 요청합니다. 이 요청에 대한 응답으로 *[TurnOnConfirmation](#TurnOnConfirmation)* 메시지를 사용해야 합니다.

#### Payload field

| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|---------|
| accessToken      | string                                  | IoT 서비스의 사용자 계정의 access token. CEK는 외부 서비스의 인증 서버로부터 획득한 사용자 계정의 access token을 전달합니다. 자세한 설명은 [사용자 계정 연결하기](/CEK/Guides/LinkUserAccount.md)를 참조합니다.                          | 필수    |
| appliance        | [ApplianceObject](#ApplianceObject)     | 대상 기기 정보를 담고 있는 객체. applianceId 필드는 필수입니다. | 필수    |

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
[TurnOnRequest](#TurnOnRequest) 메시지에 대한 응답으로 대상 기기를 켜도록 설정한 결과를 CEK에게 전달합니다.

#### Payload field
없음

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
