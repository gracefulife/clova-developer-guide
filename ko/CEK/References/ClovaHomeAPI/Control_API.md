## Control API {#ControlAPI}

IoT 기기 정보 확인 및 기기 제어와 관련된 요청 및 응답을 수행할 때 사용되는 API입니다.

| 메시지 이름         | 메시지 타입  | 메시지 설명                                   |
|------------------|-----------|---------------------------------------------|
| [`DecrementFanSpeedConfirmation`](#IncrementFanSpeedConfirmation)             | Response | [`DecrementFanSpeedRequest`](#DecrementFanSpeedRequest) 메시지에 대한 응답으로 대상 기기가 팬 속도를 설정한 결과를 CEK에게 전달합니다. |
| [`DecrementFanSpeedRequest`](#IncrementFanSpeedRequest)                       | Response | 대상 기기가 지정한 값만큼 팬 속도를 낮추도록 Clova Home extension에게 요청합니다. |
| [`DecrementTargetTemperatureConfirmation`](#DecrementTargetTemperatureConfirmation) | Response | [`DecrementTargetTemperatureRequest`](#DecrementTargetTemperatureRequest) 메시지에 대한 응답으로 대상 기기가 온도를 낮추도록 설정한 결과를 CEK에게 전달합니다. |
| [`DecrementTargetTemperatureRequest`](#DecrementTargetTemperatureRequest)     | Request | 대상 기기가 지정한 값만큼 온도를 낮추도록 Clova Home extension에게 요청합니다.      |
| [`DecrementVolumeConfirmation`](#DecrementVolumeConfirmation)                     | Response | [`DecrementVolumeRequest`](#DecrementVolumeRequest) 메시지에 대한 응답으로 대상 기기가 스피커 볼륨 크기를 설정한 결과를 CEK에게 전달합니다. |
| [`DecrementVolumeRequest`](#DecrementVolumeRequest)                           | Response | 대상 기기가 지정한 값만큼 볼륨 크기를 낮추도록 Clova home extension에게 요청합니다. |
| [`HealthCheckRequest`](#HealthCheckRequest)                                   | Request  | 지정한 기기의 상태를 파악할 때 사용되며, 대상 기기의 상태 정보를 Clova Home extension에게 요청합니다. |
| [`HealthCheckResponse`](#HealthCheckResponse)                                 | Response | [`HealthCheckRequest`](#HealthCheckRequest) 메시지에 대한 응답으로 지정한 기기의 상태 정보를 CEK에게 전달합니다. |
| [`IncrementFanSpeedConfirmation`](#IncrementFanSpeedConfirmation)             | Response | [`IncrementFanSpeedRequest`](#IncrementFanSpeedRequest) 메시지에 대한 응답으로 대상 기기가 팬의 속도를 높이도록 설정한 결과를 CEK에게 전달합니다. |
| [`IncrementFanSpeedRequest`](#IncrementFanSpeedRequest)                       | Response | 대상 기기가 지정한 값만큼 팬 속도를 높이도록 Clova Home extension에게 요청합니다. |
| [`IncrementTargetTemperatureConfirmation`](#IncrementTargetTemperatureConfirmation) | Response | [`IncrementTargetTemperatureRequest`](#IncrementTargetTemperatureRequest) 메시지에 대한 응답으로 대상 기기가 온도를 높이도록 설정한 결과를 CEK에게 전달합니다. |
| [`IncrementTargetTemperatureRequest`](#IncrementTargetTemperatureRequest)     | Request  | 대상 기기가 지정한 값만큼 온도를 높이도록 Clova Home extension에게 요청합니다.     |
| [`IncrementVolumeConfirmation`](#IncrementVolumeConfirmation)                     | Response | [`IncrementVolumeRequest`](#IncrementVolumeRequest) 메시지에 대한 응답으로 대상 기기가 스피커 볼륨을 높이도록 설정한 결과를 CEK에게 전달합니다. |
| [`IncrementVolumeRequest`](#IncrementVolumeRequest)                           | Response | 대상 기기가 지정한 값만큼 볼륨 크기를 높이도록 Clova Home extension에게 요청합니다. |
| [`SetChannelConfirmation`](#SetModeConfirmation)                              | Request  | [`SetChannelRequest`](#SetChannelRequest) 메시지에 대한 응답으로 TV 채널을 변경하도록 설정한 결과를 CEK에게 전달합니다. |
| [`SetChannelRequest`](#SetModeRequest)                                        | Request  | 대상 기기가 지정한 채널로 TV 채널을 변경하도록 Clova Home extension에게 요청합니다. |
| [`SetModeConfirmation`](#SetModeConfirmation)                                 | Request  | [`SetModeRequest`](#SetModeRequest) 메시지에 대한 응답으로 난방 모드를 변경하도록 설정한 결과를 CEK에게 전달합니다. |
| [`SetModeRequest`](#SetModeRequest)                                           | Request  | 대상 기기가 지정한 모드로 난방 모드를 변경하도록 Clova Home extension에게 요청합니다. |
| [`TurnOffConfirmation`](#TurnOffConfirmation)                                 | Response | [`TurnOffRequest`](#TurnOffRequest) 메시지에 대한 응답으로 대상 기기를 끄도록 설정한 결과를 CEK에게 전달합니다. |
| [`TurnOffRequest`](#TurnOffRequest)                                           | Request  | 대상 기기를 끄도록 Clova Home extension에게 요청합니다.                        |
| [`TurnOnConfirmation`](#TurnOnConfirmation)                                   | Response | [`TurnOnRequest`](#TurnOnRequest) 메시지에 대한 응답으로 대상 기기를 켜도록 설정한 결과를 CEK에게 전달합니다. |
| [`TurnOnRequest`](#TurnOnRequest)                                             | Request  | 대상 기기를 켜도록 Clova Home extension에게 요청합니다.                        |

### DecrementFanSpeedConfirmation {#DecrementFanSpeedConfirmation}
[`DecrementFanSpeedRequest`](#DecrementFanSpeedRequest) 메시지에 대한 응답으로 대상 기기가 팬 속도를 설정한 결과를 CEK에게 전달합니다.

#### Payload field

| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|---------|
| `targetFanSpeed`       | [SpeedObject](#SpeedObject)             | 현재 속도 정보를 담고 있는 객체                                | 필수    |
| `previousState`     | object                                  | 기기의 이전 상황 정보를 담고 있는 객체                           | 필수    |
| `previousState.targetFanSpeed` | [SpeedObject](#SpeedObject)     | 이전 속도 정보를 담고 있는 객체                                | 필수    |

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
주로 공기청정기와 같은 기기를 제어할 때 사용되며, 대상 기기가 지정한 수준만큼 팬의 속도를 낮추도록 Clova Home extension에게 요청합니다. 이 요청에 대한 응답으로 [`DecrementFanSpeedConfirmation`](#DecrementFanSpeedConfirmation) 메시지를 사용해야 합니다.

#### Payload field

| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|---------|
| `accessToken`      | string                                  | IoT 서비스의 사용자 계정의 access token. CEK는 외부 서비스의 인증 서버로부터 획득한 사용자 계정의 access token을 전달합니다. 자세한 설명은 [사용자 계정 연결하기](/CEK/Guides/LinkUserAccount.md)를 참조합니다.                          | 필수    |
| `appliance`        | [ApplianceObject](#ApplianceObject)     | 대상 기기 정보를 담고 있는 객체. `applianceId` 필드는 필수입니다.     | 필수    |
| `deltaFanSpeed`       | [SpeedObject](#SpeedObject)             | 변경할 속도 정보를 담고 있는 객체.                              | 필수    |

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
[`DecrementTargetTemperatureRequest`](#DecrementTargetTemperatureRequest) 메시지에 대한 응답으로 대상 기기가 온도를 낮추도록 설정한 결과를 CEK에게 전달합니다.

#### Payload field

| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|---------|
| `targetTemperature` | [TemperatureObject](#TemperatureObject) | 현재 희망 온도 정보를 담고 있는 객체                            | 필수    |
| `previousState`     | object                                  | 기기의 이전 상황 정보를 담고 있는 객체                           | 필수    |
| `previousState.targetTemperature` | [TemperatureObject](#TemperatureObject) | 이전 희망 온도 정보를 담고 있는 객체              | 필수    |

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
주로 에어컨과 같은 기기를 제어할 때 사용되며, 대상 기기가 지정한 값만큼 온도를 낮추도록 Clova Home extension에게 요청합니다. 이 요청에 대한 응답으로 [`DecrementTargetTemperatureConfirmation`](#DecrementTargetTemperatureConfirmation) 메시지를 사용해야 합니다.

#### Payload field

| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|---------|
| `accessToken`      | string                                  | IoT 서비스의 사용자 계정의 access token. CEK는 외부 서비스의 인증 서버로부터 획득한 사용자 계정의 access token을 전달합니다. 자세한 설명은 [사용자 계정 연결하기](/CEK/Guides/LinkUserAccount.md)를 참조합니다.                          | 필수    |
| `appliance`        | [ApplianceObject](#ApplianceObject)     | 대상 기기 정보를 담고 있는 객체. `applianceId` 필드는 필수입니다. | 필수    |
| `deltaTemperature` | [TemperatureObject](#TemperatureObject) | 변경할 온도 정보를 담고 있는 객체.                              | 필수    |

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
[`DecrementVolumeRequest`](#DecrementVolumeRequest) 메시지에 대한 응답으로 대상 기기가 스피커 볼륨 크기를 설정한 결과를 CEK에게 전달합니다.

#### Payload field

| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|---------|
| `targetVolume`      | [VolumeObject](#SpeedObject)            | 현재 볼륨 정보를 담고 있는 객체                             | 필수    |
| `previousState`     | object                                  | 기기의 이전 상황 정보를 담고 있는 객체                        | 필수    |
| `previousState.targetVolume` | [VolumeObject](#SpeedObject)    | 이전 볼륨 정보를 담고 있는 객체                             | 필수    |

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
주로 TV 셋톱 박스와 같은 기기를 제어할 때 사용되며, 대상 기기가 지정한 수준만큼 스피커 볼륨을 낮추도록 Clova Home extension에게 요청합니다. 이 요청에 대한 응답으로 [`DecrementVolumeConfirmation`](#DecrementVolumeConfirmation) 메시지를 사용해야 합니다.

#### Payload field

| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|---------|
| `accessToken`      | string                                  | IoT 서비스의 사용자 계정의 access token. CEK는 외부 서비스의 인증 서버로부터 획득한 사용자 계정의 access token을 전달합니다. 자세한 설명은 [사용자 계정 연결하기](/CEK/Guides/LinkUserAccount.md)를 참조합니다.                          | 필수    |
| `appliance`        | [ApplianceObject](#ApplianceObject)     | 대상 기기 정보를 담고 있는 객체. `applianceId` 필드는 필수입니다.     | 필수    |
| `deltaVolume`       | [VolumeObject](#VolumeObject)             | 변경할 볼륨 정보를 담고 있는 객체.                           | 필수    |

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
지정한 기기의 상태를 파악할 때 사용되며, 대상 기기의 상태 정보를 Clova Home extension에게 요청합니다. 이 요청에 대한 응답으로 [`HealthCheckResponse`](#HealthCheckResponse) 메시지를 사용해야 합니다.

#### Payload field

| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|---------|
| `accessToken`   | string  | Clova Home extension의 access token | 필수    |
| `appliance`     | [ApplianceObject](#ApplianceObject)     | 대상 기기 정보를 담고 있는 객체. `applianceId` 필드는 필수입니다.     | 필수    |

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
[`HealthCheckRequest`](#HealthCheckRequest) 메시지에 대한 응답으로 지정된 기기의 상태를 CEK에게 전달합니다.

#### Payload field

| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|---------|
| `isReachable` | boolean | 네트워크를 통해 대상 기기에 접근 가능하지를 나타내는 값. <ul><li><strong>true</strong> : 접근 가능(online)</li><li><strong>false</strong> : 접근 불가(offline)</li></ul> | 필수    |
| `isTurnOn`    | boolean | 대상 기기의 동작 상태를 나타내는 값. <ul><li><strong>true</strong> : 대기 상태(idle)</li><li><strong>false</strong> : 동작 상태(working)</li></ul>                  | 필수    |

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
[`IncrementFanSpeedRequest`](#IncrementFanSpeedRequest) 메시지에 대한 응답으로 대상 기기가 팬의 속도를 높이도록 설정한 결과를 CEK에게 전달합니다.

#### Payload field

| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|---------|
| `targetFanSpeed`            | [SpeedObject](#SpeedObject) | 현재 팬의 속도 정보를 담고 있는 객체                  | 필수    |
| `previousState`          | object                      | 기기의 이전 상황 정보를 담고 있는 객체                 | 필수    |
| `previousState.FanSpeed` | [SpeedObject](#SpeedObject) | 이전 팬의 속도 정보를 담고 있는 객체                  | 필수    |

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
주로 공기청정기와 같은 기기를 제어할 때 사용되며, 대상 기기가 지정한 값만큼 팬의 속도를 높이도록 Clova Home extension에게 요청합니다. 이 요청에 대한 응답으로 [`IncrementFanSpeedConfirmation`](#IncrementFanSpeedConfirmation) 메시지를 사용해야 합니다.

#### Payload field

| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|---------|
| `accessToken`      | string                                  | IoT 서비스의 사용자 계정의 access token. CEK는 외부 서비스의 인증 서버로부터 획득한 사용자 계정의 access token을 전달합니다. 자세한 설명은 [사용자 계정 연결하기](/CEK/Guides/LinkUserAccount.md)를 참조합니다.                          | 필수    |
| `appliance`        | [ApplianceObject](#ApplianceObject)     | 대상 기기 정보를 담고 있는 객체. `applianceId` 필드는 필수입니다. | 필수    |
| `deltaFanSpeed` | [SpeedObject](#SpeedObject) | 변경할 속도 정보를 담고 있는 객체.                              | 필수    |

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
[`IncrementTargetTemperatureRequest`](#IncrementTargetTemperatureRequest) 메시지에 대한 응답으로 대상 기기가 온도를 높이도록 설정한 결과를 CEK에게 전달합니다.

#### Payload field

| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|---------|
| `targetTemperature` | [TemperatureObject](#TemperatureObject) | 현재 희망 온도 정보를 담고 있는 객체                               | 필수    |
| `previousState`     | object                                  | 기기의 이전 상황 정보를 담고 있는 객체                              | 필수    |
| `previousState.targetTemperature` | [TemperatureObject](#TemperatureObject) | 이전 희망 온도 정보를 담고 있는 객체                 | 필수    |

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
주로 에어컨과 같은 기기를 제어할 때 사용되며, 대상 기기가 지정한 값만큼 온도를 높이도록 Clova Home extension에게 요청합니다. 이 요청에 대한 응답으로 [`IncrementTargetTemperatureConfirmation`](#IncrementTargetTemperatureConfirmation) 메시지를 사용해야 합니다.

#### Payload field

| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|---------|
| `accessToken`      | string | IoT 서비스의 사용자 계정의 access token. CEK는 외부 서비스의 인증 서버로부터 획득한 사용자 계정의 access token을 전달합니다. 자세한 설명은 [사용자 계정 연결하기](/CEK/Guides/LinkUserAccount.md)를 참조합니다. | 필수    |
| `appliance`        | [ApplianceObject](#ApplianceObject)     | 대상 기기 정보를 담고 있는 객체. `applianceId` 필드는 필수입니다. | 필수    |
| `deltaTemperature` | [TemperatureObject](#TemperatureObject) | 변경할 온도 정보를 담고 있는 객체.                              | 필수    |

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
[`IncrementVolumeRequest`](#IncrementVolumeRequest) 메시지에 대한 응답으로 대상 기기가 스피커 볼륨을 높이도록 설정한 결과를 CEK에게 전달합니다.

#### Payload field

| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|---------|
| `targetVolume` | [VolumeObject](#VolumeObject)               | 현재 볼륨 정보를 담고 있는 객체                               | 필수    |
| `previousState`     | object                                 | 기기의 이전 상황 정보를 담고 있는 객체                              | 필수    |
| `previousState.targetVolume` | [VolumeObject](#VolumeObject) | 이전 볼륨 정보를 담고 있는 객체                 | 필수    |

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
주로 TV 셋톱 박스와 같은 기기를 제어할 때 사용되며, 대상 기기가 지정한 값만큼 스피커 볼륨을 높이도록 Clova Home extension에게 요청합니다. 이 요청에 대한 응답으로 [`IncrementVolumeConfirmation`](#IncrementVolumeConfirmation) 메시지를 사용해야 합니다.

#### Payload field

| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|---------|
| `accessToken`      | string                                  | IoT 서비스의 사용자 계정의 access token. CEK는 외부 서비스의 인증 서버로부터 획득한 사용자 계정의 access token을 전달합니다. 자세한 설명은 [사용자 계정 연결하기](/CEK/Guides/LinkUserAccount.md)를 참조합니다.                          | 필수    |
| `appliance`        | [ApplianceObject](#ApplianceObject)     | 대상 기기 정보를 담고 있는 객체. `applianceId` 필드는 필수입니다. | 필수    |
| `deltaVolume` | [VolumeObject](#VolumeObject)                | 변경할 온도 정보를 담고 있는 객체.                              | 필수    |

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
[`SetChannelRequest`](#SetChannelRequest) 메시지에 대한 응답으로 TV 채널을 변경하도록 설정한 결과를 CEK에게 전달합니다.

#### Payload field

| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|---------|
| `channel`     | [TVChannelObject](#TVChannelObject)  | 대상 기기에 설정된 TV 채널 정보를 담고 있는 객체.      | 필수    |

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
주로 TV 셋톱 박스와 같은 기기를 제어할 때 사용되며, 채널을 지정한 값으로 변경하도록 Clova Home extension에게 요청합니다. 이 요청에 대한 응답으로 [`SetChannelConfirmation`](#SetChannelConfirmation) 메시지를 사용해야 합니다.

#### Payload field

| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|---------|
| `accessToken`   | string | IoT 서비스의 사용자 계정의 access token. CEK는 외부 서비스의 인증 서버로부터 획득한 사용자 계정의 access token을 전달합니다. 자세한 설명은 [사용자 계정 연결하기](/CEK/Guides/LinkUserAccount.md)를 참조합니다.                          | 필수    |
| `appliance`     | [ApplianceObject](#ApplianceObject) | 대상 기기 정보를 담고 있는 객체. `applianceId` 필드는 필수입니다. | 필수    |
| `channel`       | [TVChannelObject](#TVChannelObject) | 대상 기기에 설정할 TV 채널 정보를 담고 있는 객체.                | 필수    |

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
[`SetModeRequest`](#SetModeRequest) 메시지에 대한 응답으로 난방 모드를 변경하도록 설정한 결과를 CEK에게 전달합니다.

#### Payload field

| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|---------|
| `mode`        | [HeatingModeObject](#HeatingModeObject)  | 대상 기기에 설정된 난방 모드 정보를 담고 있는 객체.      | 필수    |

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
주로 난방 조절 장치와 같은 기기를 제어할 때 사용되며, 난방 모드를 지정한 값으로 변경하도록 Clova Home extension에게 요청합니다. 이 요청에 대한 응답으로 [`SetModeConfirmation`](#SetModeConfirmation) 메시지를 사용해야 합니다.

#### Payload field

| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|---------|
| `accessToken` | string  | IoT 서비스의 사용자 계정의 access token. CEK는 외부 서비스의 인증 서버로부터 획득한 사용자 계정의 access token을 전달합니다. 자세한 설명은 [사용자 계정 연결하기](/CEK/Guides/LinkUserAccount.md)를 참조합니다. | 필수    |
| `appliance`   | [ApplianceObject](#ApplianceObject)     | 대상 기기 정보를 담고 있는 객체. `applianceId` 필드는 필수입니다. | 필수    |
| `mode`        | [HeatingModeObject](#HeatingModeObject) | 대상 기기에 설정할 난방 모드 정보를 담고 있는 객체                         | 필수    |

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
* [`TurnOffRequest`](#TurnOffRequest)

### TurnOffRequest {#`TurnOffRequest`}
대상 기기를 끄도록 Clova Home extension에게 요청합니다. 이 요청에 대한 응답으로 [`TurnOffConfirmation`](#TurnOffConfirmation) 메시지를 사용해야 합니다.

#### Payload field

| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|---------|
| `accessToken`      | string                                  | IoT 서비스의 사용자 계정의 access token. CEK는 외부 서비스의 인증 서버로부터 획득한 사용자 계정의 access token을 전달합니다. 자세한 설명은 [사용자 계정 연결하기](/CEK/Guides/LinkUserAccount.md)를 참조합니다.                          | 필수    |
| `appliance`        | [ApplianceObject](#ApplianceObject)     | 대상 기기 정보를 담고 있는 객체. `applianceId` 필드는 필수입니다. | 필수    |

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
[`TurnOnRequest`](#TurnOnRequest) 메시지에 대한 응답으로 대상 기기를 켜도록 설정한 결과를 CEK에게 전달합니다.

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
* [`TurnOnRequest`](#TurnOnRequest)

### TurnOnRequest {#TurnOnRequest}
대상 기기를 켜도록 Clova Home extension에게 요청합니다. 이 요청에 대한 응답으로 [`TurnOnConfirmation`](#TurnOnConfirmation) 메시지를 사용해야 합니다.

#### Payload field

| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|---------|
| `accessToken`      | string                                  | IoT 서비스의 사용자 계정의 access token. CEK는 외부 서비스의 인증 서버로부터 획득한 사용자 계정의 access token을 전달합니다. 자세한 설명은 [사용자 계정 연결하기](/CEK/Guides/LinkUserAccount.md)를 참조합니다.                          | 필수    |
| `appliance`        | [ApplianceObject](#ApplianceObject)     | 대상 기기 정보를 담고 있는 객체. `applianceId` 필드는 필수입니다. | 필수    |

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
