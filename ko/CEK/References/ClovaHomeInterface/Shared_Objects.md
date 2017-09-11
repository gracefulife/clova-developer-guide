## Shared objects {#SharedObjects}
[Clova Home extension 메시지](/CEK/References/CEK_API.md#ClovaHomeExtMessage)를 보낼 때 메시지 본문(payload)에 다음과 같은 공유 객체(shared objects)가 사용됩니다.

| 객체 이름            | 객체 설명                                            |
|--------------------|---------------------------------------------------|
| [ApplianceObject](#ApplianceObject)     | IoT 기기의 정보가 담긴 객체        |
| [HeatingModeObject](#HeatingModeObject) | 난방 모드 정보가 담긴 객체          |
| [SpeedObject](#SpeedObject)             | 속도 정보가 담긴 객체              |
| [TemperatureObject](#TemperatureObject) | 온도 정보를 담고 있는 객체          |
| [TVChannelObject](#TVChannelObject)     | TV 채널 정보가 담긴 객체           |
| [VolumeObject](#VolumeObject)           | 볼륨 정보를 담고 있는 객체          |

### ApplianceObject {#ApplianceObject}
IoT 기기의 정보를 담고 있는 객체입니다. 사용자 계정에 등록된 기기 목록을 CEK에게 전달하거나 특정 기기를 대상으로 지정하여 Clova Home extension에 기기 제어를 요청할 때 이 객체를 사용합니다.

#### Object field
| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|---------|
| `actions[]`                  | string array  | 기기가 지원하는 동작 목록. 클라이언트는 기기가 지원하는 동작 내에서 사용자가 IoT 기기를 제어하도록 제한해야 합니다. | 선택    |
| `additionalApplianceDetails` | object        | 제조사나 IoT 서비스에서 제공하는 추가 정보를 담고 있는 필드                                 | 선택    |
| `applianceId`                | string        | 기기 ID                                                                        | 필수    |
| `applianceTypes[]`           | string array  | 기기 타입. `applicationType`에 따라 해당 기기가 수행할 수 있는 동작인 `actions` 필드의 값이 달라집니다. IoT 서비스에서 사용자 계정에 등록된 기기의 타입을 다음 값 중 하나로 지정해야 합니다.<ul><li>AIRCONDITIONER : 냉난방기 타입</li><li>AIRPURIFIER : 공기청정기 타입</li><li>HUMIDIFIER : 가습기 타입</li><li>LIGHT : 조명 기기 타입</li><li>SETTOPBOX : TV 셋톱 박스 타입</li><li>SMARTPLUG : 기기 전원을 제어하는 플러그</li><li>SWITCH : 가정 내 콘센트 전원을 제어하는 스위치</li><li>THERMOSTAT : 온도 조절 기기 타입</li></ul>          | 필수    |
| `friendlyName`               | string        | 사용자가 붙여준 기기의 이름                                                           | 선택    |
| `friendlyDescription`        | string        | 기기에 대한 설명                                                                  | 선택    |
| `isReachable`                | boolean       | 원격 제어 가능 여부 <ul><li>true: 원격 제어 가능</li><li>false: 원격 제어 불가</li></ul> | 선택    |
| `manufacturerName`           | string        | 기기 제조사 이름                                                                  | 선택    |
| `modelName`                  | string        | 기기 모델 이름                                                                   | 선택    |
| `version`                    | string        | 제조사의 소프트웨어 버전                                                            | 선택    |

### Remarks
[`DiscoverAppliancesRequest`](/CEK/References/ClovaHomeInterface/Discovery_Interfaces.md#DiscoverAppliancesRequest) 메시지를 통해 사용자 기기 목록을 요청하면 Clova Home extension은 `additionalApplianceDetails` 필드를 제외한 모든 필드의 정보를 채워서 전달해야 합니다. 이때, `actions` 필드의 값은 보통 `applianceTypes` 필드에 의해 결정되며, `applianceTypes` 필드 값에 따라 다음과 같은 값을 가질 수 있습니다.

| applianceTypes | 허용되는 actions                                |
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
<p>실제 기기의 기능 제약에 따라 기기의 applianceTypes가 허용하는 actions보다 적은 actions을 사용하도록 제한할 수 있다. 예를 들면, 사용자가 등록한 공기청정기(`AIRPURIFIER` 타입)에 팬 속도를 조절할 수 있는 기능이 없을 경우 해당 기기에 허용되는 actions에서 IncrementFanSpeed와 DecrementFanSpeed를 제외하고 DiscoverAppliancesResponse 메시지를 보내야 합니다.</p>
</div>

다음 표는 각 actions 항목과 관련이 있는 [인터페이스](/CEK/References/CEK_API.md#ClovaHomeExtInterface)를 나열하고 있습니다.

| actions                    | 관련된 인터페이스                            |
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
* [`DiscoverAppliancesResponse`](/CEK/References/ClovaHomeInterface/Discovery_Interfaces.md#DiscoverAppliancesResponse)
* [`DiscoverAppliancesRequest`](/CEK/References/ClovaHomeInterface/Discovery_Interfaces.md#DiscoverAppliancesRequest)

### HeatingModeObject {#HeatingModeObject}
난방 모드 정보를 담고 있는 객체입니다. 변경할 난방 모드의 이름이나 변경 전후의 난방 모드를 나타낼 때 사용되며 문자열로 표현됩니다.

#### Object field
| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|---------|
| `value`       | string  | 난방 모드. <ul><li><code>"hotwater"</code> : 온수 모드</li><li><code>"away"</code> : 외출 모드</li></ul>   | 필수     |

#### Object Example
{% raw %}
```json
// 예제 1: SetModeRequest 메시지에서 사용된 예
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

// 예제 2: SetModeConfirmation 메시지에서 사용된 예
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
속도 정보를 담고 있는 객체입니다. 변경할 속도의 크기나 변경 전후의 희망 속도를 나타낼 때 사용되며 정수로 표현됩니다.

#### Object field
| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|---------|
| `value`       | number  | 속도 값                       | 필수     |

#### Object Example
{% raw %}
```json
// 예제 1: IncrementFanSpeedRequest 메시지에서 사용된 예
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

// 예제 2: IncrementFanSpeedConfirmation 메시지에서 사용된 예
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
온도 정보를 담고 있는 객체입니다. 변경할 온도의 크기나 변경 전후의 희망 온도를 나타낼 때 사용되며 소수점 첫째 자리 숫자로 표현됩니다.

#### Object field
| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|---------|
| `value`       | number  | 온도 값                       | 필수     |

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
* [`DecrementTargetTemperatureConfirmation`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#DecrementTargetTemperatureConfirmation)
* [`DecrementTargetTemperatureRequest`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#DecrementTargetTemperatureRequest)
* [`IncrementTargetTemperatureConfirmation`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#IncrementTargetTemperatureConfirmation)
* [`IncrementTargetTemperatureRequest`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#IncrementTargetTemperatureRequest)

### TVChannelObject {#TVChannelObject}
TV 채널 정보를 담고 있는 객체입니다. 변경할 TV 채널의 이름이나 변경 전후의 TV 채널을 나타낼 때 사용되며 문자열로 표현됩니다.

#### Object field
| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|---------|
| `value`       | number  | TV 채널 번호                  | 필수     |

#### Object Example
{% raw %}
```json
// 예제 1: SetChannelRequest 메시지에서 사용된 예
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

// 예제 2: SetChannelConfirmation 메시지에서 사용된 예
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
스피커의 볼륨 정보를 담고 있는 객체입니다. 변경할 볼륨의 크기나 변경 전후의 볼륨 정보를 나타낼 때 사용되며 정수로 표현됩니다.

#### Object field
| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|---------|
| `value`       | number  | 볼륨 값                       | 필수     |

#### Object Example
{% raw %}
```json
// 예제 1: IncrementVolumeRequest 메시지에서 사용된 예
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

// 예제 2: IncrementVolumeConfirmation 메시지에서 사용된 예
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
