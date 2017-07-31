## Shared objects {#SharedObjects}
Clova Home API를 이용하여 메시지를 보낼 때 메시지 본문(payload)에 다음과 같은 객체(shared objects)가 사용됩니다.

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
| additionalApplianceDetails | object        | 제조사나 IoT 서비스의 추가 정보를 받기 위해 예약해둔 필드                                  | 선택    |
| applianceId                | string        | 기기 ID                                                                        | 필수    |
| applianceTypes[]           | string array  | 기기 타입. 다음과 같은 값을 가집니다.<ul><li>LIGHT : 조명 기기 타입</li><li>SMARTLOCK : 도어락 타입</li><li>SWITCH : 가정 내 콘센트 전원을 제어하는 스위치</li><li>SMARTPLUG : 기기 전원을 제어하는 플러그</li></ul>          | 필수    |
| friendlyName               | string        | 사용자가 붙여준 기기의 이름                                                           | 선택    |
| friendlyDescription        | string        | 기기에 대한 설명                                                                  | 선택    |
| isReachable                | boolean       | 원격 제어 가능 여부 <ul><li>true: 원격 제어 가능</li><li>false: 원격 제어 불가</li></ul> | 선택    |
| manufacturerName           | string        | 기기 제조사 이름                                                                  | 선택    |
| modelName                  | string        | 기기 모델 이름                                                                   | 선택    |
| version                    | string        | 제조사의 소프트웨어 버전                                                            | 선택    |

### Remarks
*[DiscoverAppliancesRequest](#DiscoverAppliancesRequest)* 메시지를 통해 사용자 기기 목록을 요청하면 Clova Home extension은 *additionalApplianceDetails* 필드를 제외한 모든 필드의 정보를 채워서 전달해야 합니다.

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
        "manufacturerName": "device-manufacturer-name",
        "modelName": "스마트 전등",
        "version": "v1.0",
        "friendlyName": "거실 전등",
        "friendlyDescription": "스마트폰으로 제어할 수 있는 전등",
        "isReachable": true,
          "actions": [
            "TurnOn",
            "TurnOff"
        ],
        "applianceTypes": ["LIGHT"],
        "additionalApplianceDetails": {
        }
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
          "TurnOn",
          "TurnOff"
        ],
        "applianceTypes": ["SMARTPLUG"],
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
온도 정보를 담고 있는 객체입니다. 변경할 온도의 크기나 변경 전후의 희망 온도를 나타낼 때 사용되며 소수점 첫째 자리까지 표현합니다.

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
* [GetTargetTemperatureResponse](#GetTargetTemperatureResponse)
* [IncrementTargetTemperatureRequest](#IncrementTargetTemperatureRequest)
* [IncrementTargetTemperatureConfirmation](#IncrementTargetTemperatureConfirmation)
