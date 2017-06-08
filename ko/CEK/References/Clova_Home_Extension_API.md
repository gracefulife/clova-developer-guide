# Clova Home extension API

IoT 기기를 제어할 때 사용하는 API이며, 메시지 헤더(header)의 값으로 *ClovaHome*를 가집니다. Clova Home extension은 이 API를 사용하여 제어할 수 있는 기기 목록을 제공하거나 사용자가 등록한 IoT 기기를 제어해야 합니다.

| 메시지 이름         | 메시지 타입  | 메시지 설명                                   |
|------------------|-----------|---------------------------------------------|
| [DecrementTargetTemperatureRequest](#DecrementTargetTemperatureRequest)     | Request | 대상 기기에게 지정한 값만큼 온도를 낮추도록 Clova Home extension에게 요청합니다.      |
| [DecrementTargetTemperatureConfirmation](#DecrementTargetTemperatureConfirmation) | Response | [DecrementTargetTemperatureRequest](#DecrementTargetTemperatureRequest) 메시지에 대한 응답으로 대상 기기가 온도를 낮추도록 설정한 결과를 CEK에게 전달합니다. |
| [DiscoverAppliancesRequest](#DiscoverAppliancesRequest)                     | Request  | 사용자가 등록한 IoT 기기 목록을 Clova Home extension에게 요청합니다.             |
| [DiscoverAppliancesResponse](#DiscoverAppliancesResponse)                   | Response | [DiscoverAppliancesRequest](#DiscoverAppliancesRequest) 메시지에 대한 응답으로 사용자가 등록한 IoT 기기 목록을 CEK에게 전달합니다. |
| [DriverInternalError](#DriverInternalError)                                 | Error Response | 내부적인 오류가 발생하면 CEK에게 이 메지지를 응답으로 보냅니다.             |
| [GetLockStateRequest](#GetLockStateRequest)                                 | Request  | 대상 기기의 현재 잠금 상태 정보를 Clova Home extension에게 요청합니다.            |
| [GetLockStateResponse](#GetLockStateResponse)                               | Response | [GetLockStateRequest](#GetLockStateRequest) 메시지에 대한 응답으로 대상 기기의 현재 잠금 상태를 CEK에게 전달합니다. |
| [GetTargetTemperatureRequest](#GetTargetTemperatureRequest)                 | Request  | 대상 기기에 설정된 희망 온도 값을 Clova Home extension에게 요청합니다.            |
| [GetTargetTemperatureResponse](#GetTargetTemperatureResponse)               | Response | [GetTargetTemperatureRequest](#GetTargetTemperatureRequest) 메시지에 대한 응답으로 대상 기기에 설정된 희망 온도 값을 CEK에게 전달합니다. |
| [HealthCheckRequest](#HealthCheckRequest)                                   | Request  | Clova가 사용자 기기의 연결 여부를 파악하기 위해 이 메시지를 주기적으로 Clova Home extension에게 보냅니다. |
| [HealthCheckResponse](#HealthCheckResponse)                                 | Response | [HealthCheckRequest](#HealthCheckRequest) 메시지에 대한 응답으로 현재 접근 가능한 사용자 기기의 ID 목록을 CEK에게 전달합니다. |
| [IncrementTargetTemperatureRequest](#IncrementTargetTemperatureRequest)     | Request  | 대상 기기에게 지정한 값만큼 온도를 높이도록 Clova Home extension에게 요청합니다.     |
| [IncrementTargetTemperatureConfirmation](#IncrementTargetTemperatureConfirmation) | Response | [IncrementTargetTemperatureRequest](#IncrementTargetTemperatureRequest) 메시지에 대한 응답으로 대상 기기가 온도를 높이도록 설정한 결과를 CEK에게 전달합니다. |
| [SetLockStateRequest](#SetLockStateRequest)                                 | Request  | 대상 기기를 잠그거나 열도록 Clova Home extension에게 요청합니다.                 |
| [SetLockStateConfirmation](#SetLockStateConfirmation)                       | Response | [SetLockStateRequest](#SetLockStateRequest) 메시지에 대한 응답으로 대상 기기가 잠기거나 열리도록 설정한 결과를 CEK에게 전달합니다. |
| [TargetOfflineError](#TargetOfflineError)                                   | Error Response | 대상 기기에 접속할 수 없으면(offline) CEK에게 이 메시지를 응답으로 보냅니다. |
| [TurnOffRequest](#TurnOffRequest)                                           | Request  | 대상 기기를 끄도록 Clova Home extension에게 요청합니다.                        |
| [TurnOffConfirmation](#TurnOffConfirmation)                                 | Response | [TurnOffRequest](#TurnOffRequest) 메시지에 대한 응답으로 대상 기기를 끄도록 설정한 결과를 CEK에게 전달합니다. |
| [TurnOnRequest](#TurnOnRequest)                                             | Request  | 대상 기기를 켜도록 Clova Home extension에게 요청합니다.                        |
| [TurnOnConfirmation](#TurnOnConfirmation)                                   | Response | [TurnOnRequest](#TurnOnRequest) 메시지에 대한 응답으로 대상 기기를 켜도록 설정한 결과를 CEK에게 전달합니다. |

## DecrementTargetTemperatureRequest {#DecrementTargetTemperatureRequest}
주로 에어컨과 같은 기기를 제어할 때 사용되며, 대상 기기에게 지정한 값만큼 온도를 낮추도록 Clova Home extension에게 요청합니다. 이 요청에 대한 응답으로 *[DecrementTargetTemperatureConfirmation](#DecrementTargetTemperatureConfirmation)* 메시지를 사용해야 합니다.

### Payload field

| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|---------|
| accessToken      | string                                  | Clova Home extension 접근 토큰                            | 필수    |
| appliance        | [ApplianceObject](#ApplianceObject)     | 대상 기기 정보를 담고 있는 객체. applianceId 필드를 필수로 가집니다. | 필수    |
| deltaTemperature | [TemperatureObject](#TemperatureObject) | 변경할 온도 정보를 담고 있는 객체.                              | 필수    |

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
* [DecrementTargetTemperatureConfirmation](#DecrementTargetTemperatureConfirmation)

## DecrementTargetTemperatureConfirmation {#DecrementTargetTemperatureConfirmation})
[DecrementTargetTemperatureRequest](#DecrementTargetTemperatureRequest) 메시지에 대한 응답으로 대상 기기가 온도를 낮추도록 설정한 결과를 CEK에게 전달합니다.

### Payload field

| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|---------|
| accessToken       | string                                  | Clova Home extension 접근 토큰                            | 필수    |
| appliance         | [ApplianceObject](#ApplianceObject)     | 대상 기기 정보를 담고 있는 객체. applianceId 필드를 필수로 가집니다. | 필수    |
| targetTemperature | [TemperatureObject](#TemperatureObject) | 현재 희망 온도 정보를 담고 있는 객체                            | 필수    |
| previousState     | object                                  | 기기의 이전 상황 정보를 담고 있는 객체                           | 필수    |
| previousState.targetTemperature | [TemperatureObject](#TemperatureObject) | 이전 희망 온도 정보를 담고 있는 객체              | 필수    |

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
* [DecrementTargetTemperatureRequest](#DecrementTargetTemperatureRequest)

## DiscoverAppliancesRequest {#DiscoverAppliancesRequest}
사용자가 등록한 기기 목록을 Clova Home extension에게 요청합니다. 이 요청에 대한 응답으로 *[ClovaHome.DiscoverAppliancesResponse](DiscoverAppliancesResponse)* 메시지를 사용해야 합니다.

### Payload field

| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|---------|
| accessToken   | string  | Clova Home extension 접근 토큰  | 필수     |

### Message example

{% raw %}
```json
{
    "header": {
        "messageId": "8ddd7f05-7703-4cb4-a6dd-93c209c6647b",
        "name": "DiscoverAppliancesRequest",
        "namespace": "ClovaHome",
        "payloadVersion": "1.0"
    },
    "payload": {
        "accessToken": "92ebcb67fe33"
    }
}
```
{% endraw %}

### See also
* [ClovaHome.DiscoverAppliancesResponse](DiscoverAppliancesResponse)

## DiscoverAppliancesResponse {#DiscoverAppliancesResponse}
사용자가 등록한 기기 목록을 CEK에게 전달합니다. 이 메시지는 *[ClovaHome.DiscoverAppliancesRequest](DiscoverAppliancesRequest)* 메시지에 대한 응답으로 사용됩니다.

### Payload field

| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|---------|
| discoveredAppliances[]  | [ApplianceObject](#ApplianceObject) array  | 사용자 계정에 등록된 기기 목록을 표현하는 객체 배열          | 필수    |

### Remarks
IoT 서비스를 제공할 때 각 사용자가 등록한 기기의 제공할 수 있어야 합니다.

### Message example

{% raw %}
```json
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
        "manufacturerName": "LG U+",
        "modelName": "U+ 스마트 조명",
        "version": "v1.0",
        "friendlyName": "거실 전등",
        "friendlyDescription": "스마트폰으로 제어 가능한 스마트 조명",
        "isReachable": true,
          "actions": [
            "TurnOn",
          "TurnOff"
        ],
        "additionalApplianceDetails": {
        }
      },
      {
        "applianceId": "device-002",
        "manufacturerName": "LG U+",
        "modelName": "U+ 스마트 플러그",
        "version": "v1.0",
        "friendlyName": "안방 TV 플러그",
        "friendlyDescription": "전기절약해주는 똑똑한 플러그",
        "isReachable": true,
        "actions": [
          "TurnOn",
          "TurnOff"
        ],
        "additionalApplianceDetails": {
        }
      }
    ]
  }
}
```
{% endraw %}

### See also
* [ClovaHome.DiscoverAppliancesRequest](DiscoverAppliancesRequest)

## DriverInternalError {#DriverInternalError}
내부적인 오류가 발생하면 CEK에게 이 메지지를 응답으로 보냅니다. CEK가 이 메시지를 전달받으면 미리 준비된 오류 메시지를 클라이언트에 전달합니다.

### Payload field

없음

### Remarks
* 오류 메시지도 정상적인 HTTP 응답(200 OK)으로 CEK에게 메시지를 전달해야 합니다.
* 오류 메시지의 이름으로 상황을 판단하기 때문에 별도의 본문(payload)가 필요하지 않습니다.

### Message example

{% raw %}
```json
{
  "header": {
    "messageId": "fef949b7-eb94-4bda-a417-2cfb604194c3",
    "namespace": "ClovaHome",
    "name": "DriverInternalError",
    "payloadVersion": "1.0"
  },
  "payload": {
  }
}
```
{% endraw %}

### See also
* [TargetOfflineError](#TargetOfflineError)

## GetLockStateRequest {#GetLockStateRequest}
주로 도어록과 같은 기기의 상태를 확인할 때 사용되며, 대상 기기의 현재 잠금 상태 정보를 Clova Home extension에게 요청합니다. 이 요청에 대한 응답으로 *[GetLockStateResponse](#GetLockStateResponse)* 메시지를 사용해야 합니다.

### Payload field

| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|---------|
| accessToken      | string                              | Clova Home extension 접근 토큰                            | 필수    |
| appliance        | [ApplianceObject](#ApplianceObject) | 대상 기기 정보를 담고 있는 객체. applianceId 필드를 필수로 가집니다. | 필수    |

### Message example

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
      "applianceId": "device-1"
    }
  }
}
```
{% endraw %}

### See also
* [GetLockStateResponse](#GetLockStateResponse)

## GetLockStateResponse {#GetLockStateResponse}
[GetLockStateRequest](#GetLockStateRequest) 메시지에 대한 응답으로 대상 기기의 현재 잠금 상태를 CEK에게 전달합니다.

### Payload field

| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|---------|
| lockState                    | string  | 기기의 잠금 상태. 다음과 같은 값을 가집니다. <ul><li>LOCKED</li><li>UNLOCKED</li></ul>             | 필수    |
| applicanceResponseTimestamp  | string  | 기기의 잠금 상태를 확인한 시간 (Timestamp, [ISO 8061](https://en.wikipedia.org/wiki/ISO_8601))  | 필수    |

### Message example

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

### See also
* [GetLockStateRequest](#GetLockStateRequest)

## GetTargetTemperatureRequest {#GetTargetTemperatureRequest}
주로 에어컨과 같은 기기의 상태를 확인할 때 사용되며, 대상 기기에 설정된 희망 온도 값을 Clova Home extension에게 요청합니다. 이 요청에 대한 응답으로 *[GetTargetTemperatureResponse](#GetTargetTemperatureResponse)* 메시지를 사용해야 합니다.

### Payload field

| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|---------|
| accessToken      | string                              | Clova Home extension 접근 토큰                            | 필수    |
| appliance        | [ApplianceObject](#ApplianceObject) | 대상 기기 정보를 담고 있는 객체. applianceId 필드를 필수로 가집니다. | 필수    |

### Message example

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
      "applianceId": "device-1"
    }
  }
}
```
{% endraw %}

### See also
* [GetTargetTemperatureResponse](#GetTargetTemperatureResponse)

## GetTargetTemperatureResponse {#GetTargetTemperatureResponse}
[GetTargetTemperatureRequest](#GetTargetTemperatureRequest) 메시지에 대한 응답으로 대상 기기에 설정된 희망 온도 값을 CEK에게 전달합니다.

### Payload field

| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|---------|
| targetTemperature | [TemperatureObject](#TemperatureObject)  | 현재 설정된 희망 온도 정보를 담고 있는 객체                                  | 필수    |
| applicanceResponseTimestamp  | string  | 기기의 희망 온도를 확인한 시간 (Timestamp, [ISO 8061](https://en.wikipedia.org/wiki/ISO_8601))  | 필수    |

### Message example

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

### See also
* [GetTargetTemperatureRequest](#GetTargetTemperatureRequest)

# HealthCheckRequest {#HealthCheckRequest}
Clova가 사용자 기기의 연결 여부를 파악하기 위해 이 메시지를 주기적으로 Clova Home extension에게 보냅니다. 이 요청에 대한 응답으로 *[HealthCheckResponse](#HealthCheckResponse)* 메시지를 사용해야 합니다.

### Payload field

| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|---------|
| accessToken   | string  | Clova Home extension 접근 토큰 | 필수    |

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
    "accessToken": "92ebcb67fe33"
  }
}
```
{% endraw %}

### See also
* [HealthCheckResponse](#HealthCheckResponse)

## HealthCheckResponse {#HealthCheckResponse}
[HealthCheckRequest](#HealthCheckRequest) 메시지에 대한 응답으로 현재 접근 가능한 사용자 기기의 ID 목록을 CEK에게 전달합니다.

### Payload field

| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|---------|
| reachableAppliances | string array  | 현재 접근 가능한 사용자 기기의 ID 목록을 가지는 배열 | 필수    |

### Message example

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

### See also
* [GetLockStateRequest](#GetLockStateRequest)

## IncrementTargetTemperatureRequest {#IncrementTargetTemperatureRequest}
주로 에어컨과 같은 기기를 제어할 때 사용되며, 대상 기기에게 지정한 값만큼 온도를 높이도록 Clova Home extension에게 요청합니다. 이 요청에 대한 응답으로 *[IncrementTargetTemperatureConfirmation](#IncrementTargetTemperatureConfirmation)* 메시지를 사용해야 합니다.

### Payload field

| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|---------|
| accessToken      | string                                  | Clova Home extension 접근 토큰                            | 필수    |
| appliance        | [ApplianceObject](#ApplianceObject)     | 대상 기기 정보를 담고 있는 객체. applianceId 필드를 필수로 가집니다. | 필수    |
| deltaTemperature | [TemperatureObject](#TemperatureObject) | 변경할 온도 정보를 담고 있는 객체.                              | 필수    |

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
* [IncrementTargetTemperatureConfirmation](#IncrementTargetTemperatureConfirmation)

## IncrementTargetTemperatureConfirmation {#IncrementTargetTemperatureConfirmation}
[IncrementTargetTemperatureRequest](#IncrementTargetTemperatureRequest) 메시지에 대한 응답으로 대상 기기가 온도를 높이도록 설정한 결과를 CEK에게 전달합니다.

### Payload field

| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|---------|
| accessToken      | string                                   | Clova Home extension 접근 토큰                               | 필수    |
| appliance        | [ApplianceObject](#ApplianceObject)      | 대상 기기 정보를 담고 있는 객체. applianceId 필드를 필수로 가집니다.    | 필수    |
| targetTemperature | [TemperatureObject](#TemperatureObject) | 현재 희망 온도 정보를 담고 있는 객체                               | 필수    |
| previousState     | object                                  | 기기의 이전 상황 정보를 담고 있는 객체                              | 필수    |
| previousState.targetTemperature | [TemperatureObject](#TemperatureObject) | 이전 희망 온도 정보를 담고 있는 객체                 | 필수    |

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
* [IncrementTargetTemperatureRequest](#IncrementTargetTemperatureRequest)

## SetLockStateRequest {#SetLockStateRequest}
주어 도어록과 같은 기기를 제어할 때 사용되며, 대상 기기를 잠그거나 열도록 Clova Home extension에게 요청합니다. 이 요청에 대한 응답으로 *[SetLockStateConfirmation](#SetLockStateConfirmation)* 메시지를 사용해야 합니다.

### Payload field

| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|---------|
| accessToken      | string                                  | Clova Home extension 접근 토큰                            | 필수    |
| appliance        | [ApplianceObject](#ApplianceObject)     | 대상 기기 정보를 담고 있는 객체. applianceId 필드를 필수로 가집니다. | 필수    |
| lockState        | string                                  | 설정할 기기의 잠금 상태. 다음과 같은 값을 가집니다. <ul><li>LOCKED</li><li>UNLOCKED</li></ul> | 필수    |

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
      "applianceId": "device-001"
    },
    "lockState": "LOCKED"
  }
}
```
{% endraw %}

### See also
* [SetLockStateConfirmation](#SetLockStateConfirmation)

## SetLockStateConfirmation {#SetLockStateConfirmation}
[SetLockStateRequest](#SetLockStateRequest) 메시지에 대한 응답으로 대상 기기가 잠기거나 열리도록 설정한 결과를 CEK에게 전달합니다.

### Payload field

| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|---------|
| lockState     | string  | 기기의 잠금 상태. 다음과 같은 값을 가집니다. <ul><li>LOCKED</li><li>UNLOCKED</li></ul> | 필수    |

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
* [SetLockStateRequest](#SetLockStateRequest)

## TargetOfflineError{#TargetOfflineError}
대상 기기에 접속할 수 없으면(offline) CEK에게 이 메시지를 응답으로 보냅니다. CEK가 이 메시지를 전달받으면 미리 준비된 오류 메시지를 클라이언트에 전달합니다.

### Payload field

없음

### Remarks
* 오류 메시지도 정상적인 HTTP 응답(200 OK)으로 CEK에게 메시지를 전달해야 합니다.
* 오류 메시지의 이름으로 상황을 판단하기 때문에 별도의 본문(payload)가 필요하지 않습니다.

### Message example

{% raw %}
```json
{
  "header": {
    "messageId": "fef949b7-eb94-4bda-a417-2cfb604194c3",
    "namespace": "ClovaHome",
    "name": "TargetOfflineError",
    "payloadVersion": "1.0"
  },
  "payload": {
  }
}
```
{% endraw %}

### See also
* [DriverInternalError](#DriverInternalError)

## TurnOffRequest {#TurnOffRequest}
대상 기기를 끄도록 Clova Home extension에게 요청합니다. 이 요청에 대한 응답으로 *[TurnOffConfirmation](#TurnOffConfirmation)* 메시지를 사용해야 합니다.

### Payload field

| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|---------|
| accessToken      | string                                  | Clova Home extension 접근 토큰                            | 필수    |
| appliance        | [ApplianceObject](#ApplianceObject)     | 대상 기기 정보를 담고 있는 객체. applianceId 필드를 필수로 가집니다. | 필수    |

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
* [TurnOffConfirmation](#TurnOffConfirmation)

## TurnOffConfirmation {#TurnOffConfirmation}
[TurnOffRequest](#TurnOffRequest) 메시지에 대한 응답으로 대상 기기를 끄도록 설정한 결과를 CEK에게 전달합니다.

### Payload field
없음

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
* [TurnOffRequest](#TurnOffRequest)

## TurnOnRequest {#TurnOnRequest}
대상 기기를 켜도록 Clova Home extension에게 요청합니다. 이 요청에 대한 응답으로 *[TurnOnConfirmation](#TurnOnConfirmation)* 메시지를 사용해야 합니다.

### Payload field

| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|---------|
| accessToken      | string                                  | Clova Home extension 접근 토큰                            | 필수    |
| appliance        | [ApplianceObject](#ApplianceObject)     | 대상 기기 정보를 담고 있는 객체. applianceId 필드를 필수로 가집니다. | 필수    |

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
* [TurnOnConfirmation](#TurnOnConfirmation)


## TurnOnConfirmation {#TurnOnConfirmation}
[TurnOnRequest](#TurnOnRequest) 메시지에 대한 응답으로 대상 기기를 켜도록 설정한 결과를 CEK에게 전달합니다.

### Payload field
없음

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
* [TurnOnRequest](#TurnOnRequest)



## Shared objects
Clova Home Extension API를 이용하여 이벤트 메시지나 지시 메시지를 보낼 때 메시지 본문(payload)에 다음과 같은 객체(shared objects)를 공유하여 사용합니다.

| 객체 이름            | 객체 설명                                            |
|--------------------|---------------------------------------------------|
| [ApplianceObject](#ApplianceObject)     | IoT 기기의 정보가 담긴 객체            |
| [TemperatureObject](#TemperatureObject) | 온도 정보를 담고 있는 객체             |

### ApplianceObject {#ApplianceObject}
IoT 기기의 정보를 담고 있는 객체입니다. 사용자 계정에 등록된 기기 목록을 CEK에게 전달하거나 특정 기기를 대상으로 지정하여 Clova Home extension에 기기 제어를 요청할 때 이 객체를 사용합니다.

#### Object field
| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|---------|
| actions[]                  | string array  | 기기가 지원하는 동작 목록. 사용자는 기기가 지원하는 제어 동작을 요청할 수 있습니다.               | 선택    |
| additionalApplianceDetails | obejct        | 제조사나 IoT 서비스의 추가 정보를 받기 위해 예약해둔 필드                                  | 선택    |
| applianceId                | string        | 기기 ID                                                                        | 필수    |
| friendlyName               | string        | 사용자가 붙이 기기의 이름                                                           | 선택    |
| friendlyDescription        | string        | 기기에 대한 설명                                                                  | 선택    |
| isReachable                | boolean       | 원격 제어 가능 여부 <ul><li>true: 원격 제어 가능</li><li>false: 원격 제어 불가</li></ul> | 선택    |
| manufacturerName           | string        | 기기 제조사 이름                                                                  | 선택    |
| modelName                  | string        | 기기 모델 이름                                                                   | 선택    |
| version                    | string        | 제조사의 소프트웨어 버전                                                            | 선택    |

### Remarks
*[DiscoverAppliancesRequest](#DiscoverAppliancesRequest)* 메시지를 통해 사용자 기기 목록을 요청하면 Clova Home extension은 *additionalApplianceDetails* 필드를 제외한 모든 필드의 정보를 채워서 전달해야 한다.

#### Object Example
{% raw %}
```json
// 예제 1: DiscoverAppliancesResponse 메시지에서 사용된 예
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
        "manufacturerName": "LG U+",
        "modelName": "U+ 스마트 조명",
        "version": "v1.0",
        "friendlyName": "거실 전등",
        "friendlyDescription": "스마트폰으로 제어 가능한 스마트 조명",
        "isReachable": true,
          "actions": [
            "TurnOn",
          "TurnOff"
        ],
        "additionalApplianceDetails": {
        }
      },
      {
        "applianceId": "device-002",
        "manufacturerName": "LG U+",
        "modelName": "U+ 스마트 플러그",
        "version": "v1.0",
        "friendlyName": "안방 TV 플러그",
        "friendlyDescription": "전기절약해주는 똑똑한 플러그",
        "isReachable": true,
        "actions": [
          "TurnOn",
          "TurnOff"
        ],
        "additionalApplianceDetails": {
        }
      }
    ]
  }
}

// 예제 2: TurnOnRequest 메시지에서 사용된 예
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
* [ClovaHome.DiscoverAppliancesResponse](DiscoverAppliancesResponse)
* [DecrementTargetTemperatureRequest](#DecrementTargetTemperatureRequest)
* [DiscoverAppliancesRequest](#DiscoverAppliancesRequest)
* [GetLockStateRequest](#GetLockStateRequest)
* [GetTargetTemperatureRequest](#GetTargetTemperatureRequest)
* [IncrementTargetTemperatureRequest](#IncrementTargetTemperatureRequest)
* [SetLockStateRequest](#SetLockStateRequest)
* [TurnOffRequest](#TurnOffRequest)
* [TurnOnRequest](#TurnOnRequest)

### TemperatureObject {#TemperatureObject}
온도 정보를 담고 있는 객체입니다. 변경할 온도의 크기나 변경 전후의 희망 온도를 나타낼 때 사용되며 소수점 첫째자리까지 표현합니다.

#### Object field
| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|---------|
| value         | number  | 온도 값.                      | 필수     |

#### Object Example
{% raw %}
```json
// 예제 1: IncrementTargetTemperatureRequest 메시지에서 사용된 예
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

// 예제 2: IncrementTargetTemperatureConfirmation 메시지에서 사용된 예
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
* [DecrementTargetTemperatureRequest](#DecrementTargetTemperatureRequest)
* [DecrementTargetTemperatureConfirmation](#DecrementTargetTemperatureConfirmation)
* [GetTargetTemperatureRequest](#GetTargetTemperatureRequest)
* [GetTargetTemperatureRequest](#GetTargetTemperatureResponse)
* [IncrementTargetTemperatureRequest](#IncrementTargetTemperatureRequest)
* [IncrementTargetTemperatureRequest](#IncrementTargetTemperatureConfirmation)
