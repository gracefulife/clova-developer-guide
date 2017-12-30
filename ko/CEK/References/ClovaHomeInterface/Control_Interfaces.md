# Control

IoT 기기 정보 확인 및 기기 제어와 관련된 요청 및 응답을 수행할 때 사용되는 인터페이스입니다.

| 메시지 이름         | 메시지 타입  | 메시지 설명                                   |
|------------------|-----------|---------------------------------------------|
| [`ChargeConfirmation`](#ChargeConfirmation)                                   | Response | [`ChargeRequest`](#ChargeRequest) 메시지에 대한 응답으로 대상 기기가 스스로 충전하도록 설정한 결과를 CEK에게 전달합니다. |
| [`ChargeRequest`](#ChargeRequest)                                             | Request  | 대상 기기가 스스로를 충전하도록 Clova Home extension에게 요청합니다. |
| [`DecrementBrightnessConfirmation`](#DecrementBrightnessConfirmation)         | Response | [`DecrementBrightnessRequest`](#DecrementBrightnessRequest) 메시지에 대한 응답으로 대상 기기가 조명 밝기를 낮추도록 설정한 결과를 CEK에게 전달합니다. |
| [`DecrementBrightnessRequest`](#DecrementBrightnessRequest)                   | Request  | 대상 기기가 지정한 수준만큼 조명의 밝기를 낮추도록 Clova Home extension에게 요청합니다. |
| [`DecrementChannelConfirmation`](#DecrementChannelConfirmation)               | Response | [`DecrementChannelRequest`](#DecrementChannelRequest) 메시지에 대한 응답으로 대상 기기가 TV 채널을 낮추도록 설정한 결과를 CEK에게 전달합니다. |
| [`DecrementChannelRequest`](#DecrementChannelRequest)                         | Request  | 대상 기기가 지정한 수준만큼 TV 채널을 낮추도록 Clova Home extension에게 요청합니다. |
| [`DecrementFanSpeedConfirmation`](#DecrementFanSpeedConfirmation)             | Response | [`DecrementFanSpeedRequest`](#DecrementFanSpeedRequest) 메시지에 대한 응답으로 대상 기기가 팬 속도를 낮추도록 설정한 결과를 CEK에게 전달합니다. |
| [`DecrementFanSpeedRequest`](#DecrementFanSpeedRequest)                       | Request  | 대상 기기가 지정한 값만큼 팬 속도를 낮추도록 Clova Home extension에게 요청합니다. |
| [`DecrementTargetTemperatureConfirmation`](#DecrementTargetTemperatureConfirmation) | Response | [`DecrementTargetTemperatureRequest`](#DecrementTargetTemperatureRequest) 메시지에 대한 응답으로 대상 기기가 온도를 낮추도록 설정한 결과를 CEK에게 전달합니다. |
| [`DecrementTargetTemperatureRequest`](#DecrementTargetTemperatureRequest)     | Request  | 대상 기기가 지정한 값만큼 온도를 낮추도록 Clova Home extension에게 요청합니다.      |
| [`DecrementVolumeConfirmation`](#DecrementVolumeConfirmation)                 | Response | [`DecrementVolumeRequest`](#DecrementVolumeRequest) 메시지에 대한 응답으로 대상 기기가 스피커 볼륨 크기를 낮추도록 설정한 결과를 CEK에게 전달합니다. |
| [`DecrementVolumeRequest`](#DecrementVolumeRequest)                           | Request  | 대상 기기가 지정한 값만큼 볼륨 크기를 낮추도록 Clova home extension에게 요청합니다. |
| [`GetAirQualityRequest`](#GetAirQualityRequest)                               | Request  | 대상 기기가 측정한 공기질 정보를 Clova Home extension에게 요청합니다. |
| [`GetAirQualityResponse`](#GetAirQualityResponse)                             | Response | [`GetAirQualityRequest`](#GetAirQualityRequest) 메시지에 대한 응답으로 대상 기기가 측정한 공기질 정보를 CEK에게 전달합니다. |
| [`GetBatteryInfoRequest`](#GetBatteryInfoRequest)                             | Request  | 대상 기기의 배터리 정보를 Clova Home extension에게 요청합니다. |
| [`GetBatteryInfoResponse`](#GetBatteryInfoResponse)                           | Response | [`GetBatteryInfoRequest`](#GetBatteryInfoRequest) 메시지에 대한 응답으로 대상 기기의 배터리 정보를 CEK에게 전달합니다. |
| [`GetCurrentTemperatureRequest`](#GetCurrentTemperatureRequest)               | Request  | 대상 기기가 측정한 현재 온도 정보를 Clova Home extension에게 요청합니다. |
| [`GetCurrentTemperatureResponse`](#GetCurrentTemperatureResponse)             | Response | [`GetCurrentTemperatureRequest`](#GetCurrentTemperatureRequest) 메시지에 대한 응답으로 대상 기기가 측정한 현재 온도 정보를 CEK에게 전달합니다. |
| [`GetFineDustRequest`](#GetFineDustRequest)                                   | Request  | 대상 기기가 측정한 미세 먼지(PM10) 정보를 Clova Home extension에게 요청합니다. |
| [`GetFineDustResponse`](#GetFineDustResponse)                                 | Response | [`GetFineDustRequest`](#GetFineDustRequest) 메시지에 대한 응답으로 대상 기기가 측정한 미세 먼지(PM10) 정보를 CEK에게 전달합니다. |
| [`GetHumidityRequest`](#GetHumidityRequest)                                   | Request  | 대상 기기가 측정한 습도 정보를 Clova Home extension에게 요청합니다. |
| [`GetHumidityResponse`](#GetHumidityResponse)                                 | Response | [`GetHumidityRequest`](#GetHumidityRequest) 메시지에 대한 응답으로 대상 기기가 측정한 습도 정보를 CEK에게 전달합니다. |
| [`GetLockStateRequest`](#GetLockStateRequest)                                 | Request  | 대상 기기의 현재 잠금 상태 정보를 Clova Home extension에게 요청합니다.   |
| [`GetLockStateResponse`](#GetLockStateResponse)                               | Response | [`GetLockStateRequest`](#GetLockStateRequest) 메시지에 대한 응답으로 대상 기기의 현재 잠금 상태를 CEK에게 전달합니다. |
| [`GetTargetTemperatureRequest`](#GetTargetTemperatureRequest)                 | Request  | 대상 기기가 설정한 희망 온도 정보를 Clova Home extension에게 요청합니다. |
| [`GetTargetTemperatureResponse`](#GetTargetTemperatureResponse)               | Response | [`GetTargetTemperatureRequest`](#GetTargetTemperatureRequest) 메시지에 대한 응답으로 대상 기기가 설정한 희망 온도 정보를 CEK에게 전달합니다. |
| [`GetUltraFineDustRequest`](#GetUltraFineDustRequest)                         | Request  | 대상 기기가 측정한 초미세 먼지(PM2.5) 정보를 Clova Home extension에게 요청합니다. |
| [`GetUltraFineDustResponse`](#GetUltraFineDustResponse)                       | Response | [`GetUltraFineDustRequest`](#GetUltraFineDustRequest) 메시지에 대한 응답으로 대상 기기가 측정한 초미세 먼지(PM2.5) 정보를 CEK에게 전달합니다. |
| [`HealthCheckRequest`](#HealthCheckRequest)                                   | Request  | 지정한 기기의 상태를 파악할 때 사용되며, 대상 기기의 상태 정보를 Clova Home extension에게 요청합니다. |
| [`HealthCheckResponse`](#HealthCheckResponse)                                 | Response | [`HealthCheckRequest`](#HealthCheckRequest) 메시지에 대한 응답으로 지정한 기기의 상태 정보를 CEK에게 전달합니다. |
| [`IncrementBrightnessConfirmation`](#IncrementBrightnessConfirmation)         | Response | [`IncrementBrightnessRequest`](#IncrementBrightnessRequest) 메시지에 대한 응답으로 대상 기기가 조명 밝기를 높이도록 설정한 결과를 CEK에게 전달합니다. |
| [`IncrementBrightnessRequest`](#IncrementBrightnessRequest)                   | Request  | 대상 기기가 지정한 수준만큼 조명의 밝기를 높이도록 Clova Home extension에게 요청합니다. |
| [`IncrementChannelConfirmation`](#IncrementChannelConfirmation)               | Response | [`IncrementChannelRequest`](#IncrementChannelRequest) 메시지에 대한 응답으로 대상 기기가 TV 채널을 높이도록 설정한 결과를 CEK에게 전달합니다. |
| [`IncrementChannelRequest`](#IncrementChannelRequest)                         | Request  | 대상 기기가 지정한 수준만큼 TV 채널을 높이도록 Clova Home extension에게 요청합니다. |
| [`IncrementFanSpeedConfirmation`](#IncrementFanSpeedConfirmation)             | Response | [`IncrementFanSpeedRequest`](#IncrementFanSpeedRequest) 메시지에 대한 응답으로 대상 기기가 팬의 속도를 높이도록 설정한 결과를 CEK에게 전달합니다. |
| [`IncrementFanSpeedRequest`](#IncrementFanSpeedRequest)                       | Request | 대상 기기가 지정한 값만큼 팬 속도를 높이도록 Clova Home extension에게 요청합니다. |
| [`IncrementTargetTemperatureConfirmation`](#IncrementTargetTemperatureConfirmation) | Response | [`IncrementTargetTemperatureRequest`](#IncrementTargetTemperatureRequest) 메시지에 대한 응답으로 대상 기기가 온도를 높이도록 설정한 결과를 CEK에게 전달합니다. |
| [`IncrementTargetTemperatureRequest`](#IncrementTargetTemperatureRequest)     | Request  | 대상 기기가 지정한 값만큼 온도를 높이도록 Clova Home extension에게 요청합니다.     |
| [`IncrementVolumeConfirmation`](#IncrementVolumeConfirmation)                 | Response | [`IncrementVolumeRequest`](#IncrementVolumeRequest) 메시지에 대한 응답으로 대상 기기가 스피커 볼륨을 높이도록 설정한 결과를 CEK에게 전달합니다. |
| [`IncrementVolumeRequest`](#IncrementVolumeRequest)                           | Request | 대상 기기가 지정한 값만큼 볼륨 크기를 높이도록 Clova Home extension에게 요청합니다. |
| [`MuteConfirmation`](#MuteConfirmation)                                       | Response | [`MuteRequest`](#MuteRequest) 메시지에 대한 응답으로 대상 기기의 소리를 끄도록 설정(음소거)한 결과를 CEK에게 전달합니다. |
| [`MuteRequest`](#MuteRequest)                                                 | Request  | 대상 기기의 소리를 끄도록(음소거) Clova Home extension에게 요청합니다. |
| [`SetBrightnessConfirmation`](#SetBrightnessConfirmation)                     | Response | [`SetBrightnessRequest`](#SetBrightnessRequest) 메시지에 대한 응답으로 조명 밝기를 변경하도록 설정한 결과를 CEK에게 전달합니다. |
| [`SetBrightnessRequest`](#SetBrightnessRequest)                               | Request  | 대상 기기가 조명 밝기를 지정한 값으로 변경하도록 Clova Home extension에게 요청합니다. |
| [`SetChannelByNameConfirmation`](#SetChannelByNameConfirmation)               | Response | [`SetChannelByNameRequest`](#SetChannelByNameRequest) 메시지에 대한 응답으로 채널 이름으로 TV 채널을 변경하도록 설정한 결과를 CEK에게 전달합니다. |
| [`SetChannelByNameRequest`](#SetChannelByNameRequest)                         | Request  | 대상 기기가 지정한 채널 이름으로 채널을 변경하도록 Clova Home extension에게 요청합니다. |
| [`SetChannelConfirmation`](#SetChannelConfirmation)                           | Response | [`SetChannelRequest`](#SetChannelRequest) 메시지에 대한 응답으로 채널 번호로 TV 채널을 변경하도록 설정한 결과를 CEK에게 전달합니다. |
| [`SetChannelRequest`](#SetChannelRequest)                                     | Request  | 대상 기기가 지정한 채널 번호로 TV 채널을 변경하도록 Clova Home extension에게 요청합니다. |
| [`SetFanSpeedConfirmation`](#SetFanSpeedConfirmation)                         | Response | [`SetFanSpeedRequest`](#SetFanSpeedRequest) 메시지에 대한 응답으로 팬 속도를 변경하도록 설정한 결과를 CEK에게 전달합니다. |
| [`SetFanSpeedRequest`](#SetFanSpeedRequest)                                   | Request  | 대상 기기가 지정한 값으로 팬 속도를 변경하도록 Clova Home extension에게 요청합니다. |
| [`SetLockStateConfirmation`](#SetLockStateConfirmation)                       | Response | [`SetLockStateRequest`](#SetLockStateRequest) 메시지에 대한 응답으로 대상 기기가 잠기거나 열리도록 설정한 결과를 CEK에게 전달합니다.  |
| [`SetLockStateRequest`](#SetLockStateRequest)                                 | Request  | 대상 기기를 잠그거나 열도록 Clova Home extension에게 요청합니다.  |
| [`SetModeConfirmation`](#SetModeConfirmation)                                 | Response | [`SetModeRequest`](#SetModeRequest) 메시지에 대한 응답으로 운전 모드(operation mode)를 변경하도록 설정한 결과를 CEK에게 전달합니다. |
| [`SetModeRequest`](#SetModeRequest)                                           | Request  | 대상 기기가 지정한 모드로 운전 모드(operation mode)를 변경하도록 Clova Home extension에게 요청합니다. |
| [`SetTargetTemperatureConfirmation`](#SetTargetTemperatureConfirmation)       | Response | [`SetTargetTemperatureRequest`](#SetTargetTemperatureRequest) 메시지에 대한 응답으로 희망 온도를 변경하도록 설정한 결과를 CEK에게 전달합니다. |
| [`SetTargetTemperatureRequest`](#SetTargetTemperatureRequest)                 | Request  | 대상 기기가 희망 온도를 지정한 값으로 변경하도록 Clova Home extension에게 요청합니다. |
| [`TurnOffConfirmation`](#TurnOffConfirmation)                                 | Response | [`TurnOffRequest`](#TurnOffRequest) 메시지에 대한 응답으로 대상 기기를 끄도록 설정한 결과를 CEK에게 전달합니다. |
| [`TurnOffRequest`](#TurnOffRequest)                                           | Request  | 대상 기기를 끄도록 Clova Home extension에게 요청합니다.                        |
| [`TurnOnConfirmation`](#TurnOnConfirmation)                                   | Response | [`TurnOnRequest`](#TurnOnRequest) 메시지에 대한 응답으로 대상 기기를 켜도록 설정한 결과를 CEK에게 전달합니다. |
| [`TurnOnRequest`](#TurnOnRequest)                                             | Request  | 대상 기기를 켜도록 Clova Home extension에게 요청합니다.                        |
| [`UnmuteConfirmation`](#UnmuteConfirmation)                                   | Response | [`UnmuteRequest`](#UnmuteRequest) 메시지에 대한 응답으로 대상 기기의 소리를 켜도록 설정(음소거 해제)한 결과를 CEK에게 전달합니다. |
| [`UnmuteRequest`](#UnmuteRequest)                                             | Request  | 대상 기기의 소리를 켜도록(음소거 해제) Clova Home extension에게 요청합니다. |

## ChargeConfirmation {#ChargeConfirmation}
[`ChargeRequest`](#ChargeRequest) 메시지에 대한 응답으로 대상 기기가 스스로 충전하도록 설정한 결과를 CEK에게 전달합니다.

### Payload fields

없음

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
주로 로봇 청소기를 제어할 때 사용되며, 대상 기기가 스스로를 충전하도록 Clova Home extension에게 요청합니다. 이 요청에 대한 응답으로 [`ChargeConfirmation`](#ChargeConfirmation) 메시지를 사용해야 합니다.

### Payload fields

| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|---------|
| `accessToken`      | string                                  | IoT 서비스의 사용자 계정의 access token. CEK는 외부 서비스의 인증 서버로부터 획득한 사용자 계정의 access token을 전달합니다. 자세한 설명은 [사용자 계정 연결하기](/CEK/Guides/LinkUserAccount.md)를 참조합니다.                          | 필수    |
| `appliance`        | [ApplianceInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#ApplianceInfoObject)     | 대상 기기 정보를 담고 있는 객체. `applianceId` 필드는 필수입니다.     | 필수    |

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
[`DecrementBrightnessRequest`](#DecrementBrightnessRequest) 메시지에 대한 응답으로 대상 기기가 조명 밝기를 낮추도록 설정한 결과를 CEK에게 전달합니다.

### Payload fields

| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|---------|
| `brightness`               | [BrightnessInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#BrightnessInfoObject) | 현재 밝기 정보를 담고 있는 객체                                | 선택    |
| `previousState`            | object | 기기의 이전 상황 정보를 담고 있는 객체                           | 선택    |
| `previousState.brightness` | [BrightnessInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#BrightnessInfoObject) | 이전 밝기 정보를 담고 있는 객체                                | 선택    |

### Remarks

대상 기기에서 payload에 입력할 정보를 얻어올 수 없으면 값을 입력하지 않아도 됩니다. 이 경우 사용자에게 구체적인 정보 없이 기기 제어 요청이 정상 처리되었음을 알려줍니다.

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
주로 조명 기기를 제어할 때 사용되며, 대상 기기가 지정한 수준만큼 조명의 밝기를 낮추도록 Clova Home extension에게 요청합니다. 이 요청에 대한 응답으로 [`DecrementBrightnessConfirmation`](#DecrementBrightnessConfirmation) 메시지를 사용해야 합니다.

### Payload fields

| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|---------|
| `accessToken`      | string                                  | IoT 서비스의 사용자 계정의 access token. CEK는 외부 서비스의 인증 서버로부터 획득한 사용자 계정의 access token을 전달합니다. 자세한 설명은 [사용자 계정 연결하기](/CEK/Guides/LinkUserAccount.md)를 참조합니다.                          | 필수    |
| `appliance`        | [ApplianceInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#ApplianceInfoObject)     | 대상 기기 정보를 담고 있는 객체. `applianceId` 필드는 필수입니다.     | 필수    |
| `deltaBrightness`       | [BrightnessInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#BrightnessInfoObject)             | 변경할 밝기의 크기 정보를 담고 있는 객체                              | 필수    |

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
[`DecrementChannelRequest`](#DecrementChannelRequest) 메시지에 대한 응답으로 대상 기기가 TV 채널을 낮추도록 설정한 결과를 CEK에게 전달합니다.

### Payload fields

| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|---------|
| `channel`               | [TVChannelInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#TVChannelInfoObject) | 현재 TV 채널 정보를 담고 있는 객체                                | 선택    |
| `previousState`            | object | 기기의 이전 상황 정보를 담고 있는 객체                           | 선택    |
| `previousState.channel` | [TVChannelInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#TVChannelInfoObject) | 이전 TV 채널 정보를 담고 있는 객체                                | 선택    |

### Remarks

대상 기기에서 payload에 입력할 정보를 얻어올 수 없으면 값을 입력하지 않아도 됩니다. 이 경우 사용자에게 구체적인 정보 없이 기기 제어 요청이 정상 처리되었음을 알려줍니다.

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
    "channel": {
      "value": 12
    },
    "previousState": {
      "channel": {
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
주로 TV나 셋톱박스를 제어할 때 사용되며, 대상 기기가 지정한 수준만큼 TV 채널을 낮추도록 Clova Home extension에게 요청합니다. 이 요청에 대한 응답으로 [`DecrementChannelConfirmation`](#DecrementChannelConfirmation) 메시지를 사용해야 합니다.

### Payload fields

| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|---------|
| `accessToken`      | string                                  | IoT 서비스의 사용자 계정의 access token. CEK는 외부 서비스의 인증 서버로부터 획득한 사용자 계정의 access token을 전달합니다. 자세한 설명은 [사용자 계정 연결하기](/CEK/Guides/LinkUserAccount.md)를 참조합니다.                          | 필수    |
| `appliance`        | [ApplianceInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#ApplianceInfoObject)     | 대상 기기 정보를 담고 있는 객체. `applianceId` 필드는 필수입니다.     | 필수    |
| `deltaChannel`       | [TVChannelInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#TVChannelInfoObject)             | 변경할 TV 채널의 크기 정보를 담고 있는 객체                              | 필수    |

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
[`DecrementFanSpeedRequest`](#DecrementFanSpeedRequest) 메시지에 대한 응답으로 대상 기기가 팬 속도를 낮추도록 설정한 결과를 CEK에게 전달합니다.

### Payload fields

| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|---------|
| `fanSpeed`       | [SpeedInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#SpeedInfoObject)             | 현재 팬의 속도 정보를 담고 있는 객체. 팬의 속도는 풍속을 의미하며 팬 속도를 다음과 같은 값으로 제한합니다.<ul><li><code>1</code>: 약한 바람(1단)</li><li><code>2</code>: 중간 바람(2단)</li><li><code>3</code>: 강한 바람(3단)</li></ul> | 선택    |
| `previousState`     | object                                  | 기기의 이전 상황 정보를 담고 있는 객체                           | 선택    |
| `previousState.fanSpeed` | [SpeedInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#SpeedInfoObject)     | 이전 팬의 속도 정보를 담고 있는 객체. 팬의 속도는 풍속을 의미하며 팬 속도를 다음과 같은 값으로 제한합니다.<ul><li><code>1</code>: 약한 바람(1단)</li><li><code>2</code>: 중간 바람(2단)</li><li><code>3</code>: 강한 바람(3단)</li></ul> | 선택    |

### Remarks

대상 기기에서 payload에 입력할 정보를 얻어올 수 없으면 값을 입력하지 않아도 됩니다. 이 경우 사용자에게 구체적인 정보 없이 기기 제어 요청이 정상 처리되었음을 알려줍니다.

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
        "value": 3
      }
    }
  }
}
```

{% endraw %}

### See also
* [`DecrementFanSpeedRequest`](#DecrementFanSpeedRequest)

## DecrementFanSpeedRequest {#DecrementFanSpeedRequest}
주로 공기청정기와 같은 기기를 제어할 때 사용되며, 대상 기기가 지정한 수준만큼 팬의 속도를 낮추도록 Clova Home extension에게 요청합니다. 이 요청에 대한 응답으로 [`DecrementFanSpeedConfirmation`](#DecrementFanSpeedConfirmation) 메시지를 사용해야 합니다.

### Payload fields

| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|---------|
| `accessToken`      | string                                  | IoT 서비스의 사용자 계정의 access token. CEK는 외부 서비스의 인증 서버로부터 획득한 사용자 계정의 access token을 전달합니다. 자세한 설명은 [사용자 계정 연결하기](/CEK/Guides/LinkUserAccount.md)를 참조합니다.                          | 필수    |
| `appliance`        | [ApplianceInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#ApplianceInfoObject)     | 대상 기기 정보를 담고 있는 객체. `applianceId` 필드는 필수입니다.     | 필수    |
| `deltaFanSpeed`       | [SpeedInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#SpeedInfoObject)             | 변경할 팬 속도의 크기 정보를 담고 있는 객체. 팬의 속도는 풍속을 의미하며 팬 속도를 다음과 같은 값으로 제한합니다.<ul><li><code>1</code>: 약한 바람(1단)</li><li><code>2</code>: 중간 바람(2단)</li><li><code>3</code>: 강한 바람(3단)</li></ul> | 필수    |

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
[`DecrementTargetTemperatureRequest`](#DecrementTargetTemperatureRequest) 메시지에 대한 응답으로 대상 기기가 온도를 낮추도록 설정한 결과를 CEK에게 전달합니다.

### Payload fields

| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|---------|
| `targetTemperature` | [TemperatureInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#TemperatureInfoObject) | 현재 희망 온도 정보를 담고 있는 객체                            | 선택    |
| `previousState`     | object                                  | 기기의 이전 상황 정보를 담고 있는 객체                           | 선택    |
| `previousState.targetTemperature` | [TemperatureInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#TemperatureInfoObject) | 이전 희망 온도 정보를 담고 있는 객체              | 선택    |

### Remarks

대상 기기에서 payload에 입력할 정보를 얻어올 수 없으면 값을 입력하지 않아도 됩니다. 이 경우 사용자에게 구체적인 정보 없이 기기 제어 요청이 정상 처리되었음을 알려줍니다.

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
      "value": 23
    },
    "previousState": {
      "targetTemperature": {
        "value": 25
      }
    }
  }
}
```

{% endraw %}

### See also
* [`DecrementTargetTemperatureRequest`](#DecrementTargetTemperatureRequest)

## DecrementTargetTemperatureRequest {#DecrementTargetTemperatureRequest}
주로 에어컨이나 온도 조절 장치와 같은 기기를 제어할 때 사용되며, 대상 기기가 지정한 값만큼 온도를 낮추도록 Clova Home extension에게 요청합니다. 이 요청에 대한 응답으로 [`DecrementTargetTemperatureConfirmation`](#DecrementTargetTemperatureConfirmation) 메시지를 사용해야 합니다.

### Payload fields

| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|---------|
| `accessToken`      | string                                  | IoT 서비스의 사용자 계정의 access token. CEK는 외부 서비스의 인증 서버로부터 획득한 사용자 계정의 access token을 전달합니다. 자세한 설명은 [사용자 계정 연결하기](/CEK/Guides/LinkUserAccount.md)를 참조합니다.                          | 필수    |
| `appliance`        | [ApplianceInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#ApplianceInfoObject)     | 대상 기기 정보를 담고 있는 객체. `applianceId` 필드는 필수입니다. | 필수    |
| `deltaTemperature` | [TemperatureInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#TemperatureInfoObject) | 변경할 온도의 크기 정보를 담고 있는 객체                              | 필수    |

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
      "value": 2
    }
  }
}
```

{% endraw %}

### See also
* [`DecrementTargetTemperatureConfirmation`](#DecrementTargetTemperatureConfirmation)

## DecrementVolumeConfirmation {#DecrementVolumeConfirmation}
[`DecrementVolumeRequest`](#DecrementVolumeRequest) 메시지에 대한 응답으로 대상 기기가 스피커 볼륨 크기를 낮추도록 설정한 결과를 CEK에게 전달합니다.

### Payload fields

| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|---------|
| `targetVolume`      | [VolumeInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#SpeedInfoObject)            | 현재 볼륨 정보를 담고 있는 객체                             | 선택    |
| `previousState`     | object                                  | 기기의 이전 상황 정보를 담고 있는 객체                        | 선택    |
| `previousState.targetVolume` | [VolumeInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#SpeedInfoObject)    | 이전 볼륨 정보를 담고 있는 객체                             | 선택    |

### Remarks

대상 기기에서 payload에 입력할 정보를 얻어올 수 없으면 값을 입력하지 않아도 됩니다. 이 경우 사용자에게 구체적인 정보 없이 기기 제어 요청이 정상 처리되었음을 알려줍니다.

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
주로 TV 셋톱 박스와 같은 기기를 제어할 때 사용되며, 대상 기기가 지정한 수준만큼 스피커 볼륨을 낮추도록 Clova Home extension에게 요청합니다. 이 요청에 대한 응답으로 [`DecrementVolumeConfirmation`](#DecrementVolumeConfirmation) 메시지를 사용해야 합니다.

### Payload fields

| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|---------|
| `accessToken`      | string                                  | IoT 서비스의 사용자 계정의 access token. CEK는 외부 서비스의 인증 서버로부터 획득한 사용자 계정의 access token을 전달합니다. 자세한 설명은 [사용자 계정 연결하기](/CEK/Guides/LinkUserAccount.md)를 참조합니다.                          | 필수    |
| `appliance`        | [ApplianceInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#ApplianceInfoObject)     | 대상 기기 정보를 담고 있는 객체. `applianceId` 필드는 필수입니다.     | 필수    |
| `deltaVolume`       | [VolumeInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#VolumeInfoObject)             | 변경할 볼륨의 크기 정보를 담고 있는 객체                           | 필수    |

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
주로 공기청정기와 같은 기기에서 측정된 공기질 정보를 확인할 때 사용되며, 대상 기기가 측정한 공기질 정보를 Clova Home extension에게 요청합니다. 이 요청에 대한 응답으로 [`GetAirQualityResponse`](#GetAirQualityResponse) 메시지를 사용해야 합니다.

| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|---------|
| `accessToken`      | string                                  | IoT 서비스의 사용자 계정의 access token. CEK는 외부 서비스의 인증 서버로부터 획득한 사용자 계정의 access token을 전달합니다. 자세한 설명은 [사용자 계정 연결하기](/CEK/Guides/LinkUserAccount.md)를 참조합니다.                          | 필수    |
| `appliance`        | [ApplianceInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#ApplianceInfoObject)     | 대상 기기 정보를 담고 있는 객체. `applianceId` 필드는 필수입니다.     | 필수    |

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
[`GetAirQualityRequest`](#GetAirQualityRequest) 메시지에 대한 응답으로 대상 기기가 측정한 공기질 정보를 CEK에게 전달합니다.

| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|---------|
| `airQuality`                 | [AirQualityInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#AirQualityInfoObject) | 현재 기기가 측정한 공기질 정보를 담고 있는 객체   | 필수    |
| `applianceResponseTimestamp` | string | 기기에서 요청한 정보를 확인한 시간(Timestamp, [ISO 8601](https://en.wikipedia.org/wiki/ISO_8601))     | 선택    |

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
        "index": "good"
    },
    "applianceResponseTimestamp": "2017-11-23T20:30:04+09:00"
  }
}
```

{% endraw %}

### See also
* [`GetAirQualityRequest`](#GetAirQualityRequest)

## GetBatteryInfoRequest {#GetBatteryInfoRequest}
주로 로봇청소기와 같이 무선 동작하는 기기의 내장 배터리 정보를 확인할 때 사용되며, 대상 기기의 현재 배터리 정보를 Clova Home extension에게 요청합니다. 이 요청에 대한 응답으로 [`GetBatteryInfoResponse`](#GetBatteryInfoResponse) 메시지를 사용해야 합니다.

| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|---------|
| `accessToken`      | string                                  | IoT 서비스의 사용자 계정의 access token. CEK는 외부 서비스의 인증 서버로부터 획득한 사용자 계정의 access token을 전달합니다. 자세한 설명은 [사용자 계정 연결하기](/CEK/Guides/LinkUserAccount.md)를 참조합니다.                          | 필수    |
| `appliance`        | [ApplianceInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#ApplianceInfoObject)     | 대상 기기 정보를 담고 있는 객체. `applianceId` 필드는 필수입니다.     | 필수    |

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
[`GetBatteryInfoRequest`](#GetBatteryInfoRequest) 메시지에 대한 응답으로 대상 기기의 배터리 정보를 CEK에게 전달합니다.

| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|---------|
| `batteryInfo`                 | [BatteryInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#BatteryInfoObject) | 현재 기기의 배터리 정보를 담고 있는 객체   | 필수    |
| `applianceResponseTimestamp` | string | 기기에서 요청한 정보를 확인한 시간(Timestamp, [ISO 8601](https://en.wikipedia.org/wiki/ISO_8601))     | 선택    |

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
    },
    "applianceResponseTimestamp": "2017-11-23T20:30:19+09:00"
  }
}
```

{% endraw %}

### See also
* [`GetBatteryInfoRequest`](#GetBatteryInfoRequest)

## GetCurrentTemperatureRequest {#GetCurrentTemperatureRequest}
주로 에어컨이나 온도 조절 장치와 같은 기기에서 측정된 현재 온도를 확인할 때 사용되며, 대상 기기가 측정한 현재 온도 정보를 Clova Home extension에게 요청합니다. 이 요청에 대한 응답으로 [`GetCurrentTemperatureResponse`](#GetCurrentTemperatureResponse) 메시지를 사용해야 합니다.

| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|---------|
| `accessToken`      | string                                  | IoT 서비스의 사용자 계정의 access token. CEK는 외부 서비스의 인증 서버로부터 획득한 사용자 계정의 access token을 전달합니다. 자세한 설명은 [사용자 계정 연결하기](/CEK/Guides/LinkUserAccount.md)를 참조합니다.                          | 필수    |
| `appliance`        | [ApplianceInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#ApplianceInfoObject)     | 대상 기기 정보를 담고 있는 객체. `applianceId` 필드는 필수입니다.     | 필수    |

### Message example

{% raw %}

```json
{
  "header": {
    "messageId": "3085a017-919f-4708-8748-fb68af10faba",
    "name": "GetCurrentTemperatureRequest",
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
* [`GetCurrentTemperatureResponse`](#GetCurrentTemperatureResponse)
* [`GetTargetTemperatureRequest`](#GetTargetTemperatureRequest)

## GetCurrentTemperatureResponse {#GetCurrentTemperatureResponse}
[`GetCurrentTemperatureRequest`](#GetCurrentTemperatureRequest) 메시지에 대한 응답으로 대상 기기가 측정한 현재 온도 정보를 CEK에게 전달합니다.

| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|---------|
| `currentTemperature`          | [TemperatureInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#TemperatureInfoObject) | 대상 기기가 측정한 현재 온도 정보를 담고 있는 객체  | 필수    |
| `applianceResponseTimestamp` | string | 기기에서 요청한 정보를 확인한 시간(Timestamp, [ISO 8601](https://en.wikipedia.org/wiki/ISO_8601))     | 선택    |

### Message example

{% raw %}

```json
{
  "header": {
    "messageId": "7eef3a17-675d-4bbd-bd8a-f379855d05ca",
    "name": "GetCurrentTemperatureResponse",
    "namespace": "ClovaHome",
    "payloadVersion": "1.0"
  },
  "payload": {
    "currentTemperature": {
        "value": 22
    },
    "applianceResponseTimestamp": "2017-11-23T20:30:32+09:00"
  }
}
```

{% endraw %}

### See also
* [`GetCurrentTemperatureRequest`](#GetCurrentTemperatureRequest)
* [`GetTargetTemperatureResponse`](#GetTargetTemperatureResponse)

## GetFineDustRequest {#GetFineDustRequest}
주로 공기청정기와 같은 기기에서 측정된 미세 먼지(PM10) 정보를 확인할 때 사용되며, 대상 기기가 측정한 미세 먼지 정보를 Clova Home extension에게 요청합니다. 이 요청에 대한 응답으로 [`GetFineDustResponse`](#GetFineDustResponse) 메시지를 사용해야 합니다.

| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|---------|
| `accessToken`      | string                                  | IoT 서비스의 사용자 계정의 access token. CEK는 외부 서비스의 인증 서버로부터 획득한 사용자 계정의 access token을 전달합니다. 자세한 설명은 [사용자 계정 연결하기](/CEK/Guides/LinkUserAccount.md)를 참조합니다.                          | 필수    |
| `appliance`        | [ApplianceInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#ApplianceInfoObject)     | 대상 기기 정보를 담고 있는 객체. `applianceId` 필드는 필수입니다.     | 필수    |

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
[`GetFineDustRequest`](#GetFineDustRequest) 메시지에 대한 응답으로 대상 기기가 측정한 미세 먼지(PM10) 정보를 CEK에게 전달합니다.

| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|---------|
| `fineDust`                 | [FineDustInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#FineDustInfoObject) | 현재 기기가 측정한 미세 먼지 정보를 담고 있는 객체   | 필수    |
| `applianceResponseTimestamp` | string | 기기에서 요청한 정보를 확인한 시간(Timestamp, [ISO 8601](https://en.wikipedia.org/wiki/ISO_8601))     | 선택    |

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
      "value": 77,
      "index": "normal"
    },
    "applianceResponseTimestamp": "2017-11-23T20:30:44+09:00"
  }
}
```

{% endraw %}

### See also
* [`GetFineDustRequest`](#GetFineDustRequest)

## GetHumidityRequest {#GetHumidityRequest}
주로 가습기와 같은 기기에서 측정된 습도 정보를 확인할 때 사용되며, 대상 기기가 측정한 습도 정보를 Clova Home extension에게 요청합니다. 이 요청에 대한 응답으로 [`GetHumidityResponse`](#GetHumidityResponse) 메시지를 사용해야 합니다.

| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|---------|
| `accessToken`      | string                                  | IoT 서비스의 사용자 계정의 access token. CEK는 외부 서비스의 인증 서버로부터 획득한 사용자 계정의 access token을 전달합니다. 자세한 설명은 [사용자 계정 연결하기](/CEK/Guides/LinkUserAccount.md)를 참조합니다.                          | 필수    |
| `appliance`        | [ApplianceInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#ApplianceInfoObject)     | 대상 기기 정보를 담고 있는 객체. `applianceId` 필드는 필수입니다.     | 필수    |

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
[`GetHumidityRequest`](#GetHumidityRequest) 메시지에 대한 응답으로 대상 기기가 측정한 습도 정보를 CEK에게 전달합니다.

| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|---------|
| `humidity`                 | [HumidityInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#HumidityInfoObject) | 현재 기기가 측정한 습도 정보를 담고 있는 객체   | 필수    |
| `applianceResponseTimestamp` | string | 기기에서 요청한 정보를 확인한 시간(Timestamp, [ISO 8601](https://en.wikipedia.org/wiki/ISO_8601))     | 선택    |

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
    },
    "applianceResponseTimestamp": "2017-11-23T20:30:54+09:00"
  }
}
```

{% endraw %}

### See also
* [GetHumidityRequest](#GetHumidityRequest)

## GetLockStateRequest {#GetLockStateRequest}
주로 스마트 밸브와 같은 기기의 상태를 확인할 때 사용되며, 대상 기기의 현재 잠금 상태 정보를 Clova Home extension에게 요청합니다. 이 요청에 대한 응답으로 [`GetLockStateResponse`](#GetLockStateResponse) 메시지를 사용해야 합니다.

| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|---------|
| `accessToken`      | string                                  | IoT 서비스의 사용자 계정의 access token. CEK는 외부 서비스의 인증 서버로부터 획득한 사용자 계정의 access token을 전달합니다. 자세한 설명은 [사용자 계정 연결하기](/CEK/Guides/LinkUserAccount.md)를 참조합니다.                          | 필수    |
| `appliance`        | [ApplianceInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#ApplianceInfoObject)     | 대상 기기 정보를 담고 있는 객체. `applianceId` 필드는 필수입니다.     | 필수    |

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
[`GetLockStateRequest`](#GetLockStateRequest) 메시지에 대한 응답으로 대상 기기의 현재 잠금 상태를 CEK에게 전달합니다.

| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|---------|
| `lockState`   | string | 기기의 잠금 상태. 다음과 같은 값을 가집니다. <ul><li><code>"LOCKED"</code></li><li><code>"UNLOCKED"</code></li></ul> | 필수    |
| `applianceResponseTimestamp` | string | 기기에서 요청한 정보를 확인한 시간(Timestamp, [ISO 8601](https://en.wikipedia.org/wiki/ISO_8601))     | 선택    |

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
  },
  "applianceResponseTimestamp": "2017-11-23T20:31:08+09:00"
}
```

{% endraw %}

### See also
* [`GetLockStateRequest`](#GetLockStateRequest)

## GetTargetTemperatureRequest {#GetTargetTemperatureRequest}
주로 에어컨이나 온도 조절 장치와 같은 기기에서 설정된 희망 온도를 확인할 때 사용되며, 대상 기기가 설정한 희망 온도 정보를 Clova Home extension에게 요청합니다. 이 요청에 대한 응답으로 [`GetTargetTemperatureResponse`](#GetTargetTemperatureResponse) 메시지를 사용해야 합니다.

| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|---------|
| `accessToken`      | string                                  | IoT 서비스의 사용자 계정의 access token. CEK는 외부 서비스의 인증 서버로부터 획득한 사용자 계정의 access token을 전달합니다. 자세한 설명은 [사용자 계정 연결하기](/CEK/Guides/LinkUserAccount.md)를 참조합니다.                          | 필수    |
| `appliance`        | [ApplianceInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#ApplianceInfoObject)     | 대상 기기 정보를 담고 있는 객체. `applianceId` 필드는 필수입니다.     | 필수    |

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
[`GetTargetTemperatureRequest`](#GetTargetTemperatureRequest) 메시지에 대한 응답으로 대상 기기가 설정한 희망 온도 정보를 CEK에게 전달합니다.

| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|---------|
| `targetTemperature`          | [TemperatureInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#TemperatureInfoObject) | 대상 기기에 설정된 희망 온도 정보를 담고 있는 객체  | 필수    |
| `applianceResponseTimestamp` | string | 기기에서 요청한 정보를 확인한 시간(Timestamp, [ISO 8601](https://en.wikipedia.org/wiki/ISO_8601))     | 선택    |

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
        "value": 24
    },
    "applianceResponseTimestamp": "2017-11-23T20:31:18+09:00"
  }
}
```

{% endraw %}

### See also
* [`GetTargetTemperatureRequest`](#GetTargetTemperatureRequest)

## GetUltraFineDustRequest {#GetUltraFineDustRequest}
주로 공기청정기와 같은 기기에서 측정된 초미세 먼지(PM2.5) 정보를 확인할 때 사용되며, 대상 기기가 측정한 초미세 먼지 정보를 Clova Home extension에게 요청합니다. 이 요청에 대한 응답으로 [`GetUltraFineDustResponse`](#GetUltraFineDustResponse) 메시지를 사용해야 합니다.

| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|---------|
| `accessToken`      | string                                  | IoT 서비스의 사용자 계정의 access token. CEK는 외부 서비스의 인증 서버로부터 획득한 사용자 계정의 access token을 전달합니다. 자세한 설명은 [사용자 계정 연결하기](/CEK/Guides/LinkUserAccount.md)를 참조합니다.                          | 필수    |
| `appliance`        | [ApplianceInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#ApplianceInfoObject)     | 대상 기기 정보를 담고 있는 객체. `applianceId` 필드는 필수입니다.     | 필수    |

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
[`GetUltraFineDustRequest`](#GetUltraFineDustRequest) 메시지에 대한 응답으로 대상 기기가 측정한 초미세 먼지(PM2.5) 정보를 CEK에게 전달합니다.

| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|---------|
| `ultraFineDust`                 | [UltraFineDustInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#UltraFineDustInfoObject) | 현재 기기가 측정한 초미세 먼지 정보를 담고 있는 객체   | 필수    |
| `applianceResponseTimestamp` | string | 기기에서 요청한 정보를 확인한 시간(Timestamp, [ISO 8601](https://en.wikipedia.org/wiki/ISO_8601))     | 선택    |

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
    "ultraFineDust": {
      "value": 44,
      "index": "good"
    },
    "applianceResponseTimestamp": "2017-11-23T20:26:48+09:00"
  }
}
```

{% endraw %}

### See also
* [`GetUltraFineDustRequest`](#GetUltraFineDustRequest)

## HealthCheckRequest {#HealthCheckRequest}
지정한 기기의 상태를 파악할 때 사용되며, 대상 기기의 상태 정보를 Clova Home extension에게 요청합니다. 이 요청에 대한 응답으로 [`HealthCheckResponse`](#HealthCheckResponse) 메시지를 사용해야 합니다.

### Payload fields

| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|---------|
| `accessToken`   | string  | Clova Home extension의 access token | 필수    |
| `appliance`     | [ApplianceInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#ApplianceInfoObject)     | 대상 기기 정보를 담고 있는 객체. `applianceId` 필드는 필수입니다.     | 필수    |

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
[`HealthCheckRequest`](#HealthCheckRequest) 메시지에 대한 응답으로 지정된 기기의 상태를 CEK에게 전달합니다.

### Payload fields

| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|---------|
| `isReachable` | boolean | 네트워크를 통해 대상 기기에 접근 가능한지 나타내는 값. <ul><li><code>true</code>: 접근 가능(online)</li><li><code>false</code>: 접근 불가(offline)</li></ul> | 필수    |
| `isTurnOn`    | boolean | 대상 기기의 동작 상태를 나타내는 값. <ul><li><code>true</code>: 대기 상태(idle)</li><li><code>false</code>: 동작 상태(working)</li></ul>                  | 필수    |

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
[`IncrementBrightnessRequest`](#IncrementBrightnessRequest) 메시지에 대한 응답으로 대상 기기가 조명 밝기를 높이도록 설정한 결과를 CEK에게 전달합니다.

### Payload fields

| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|---------|
| `brightness`               | [BrightnessInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#BrightnessInfoObject) | 현재 밝기 정보를 담고 있는 객체                                | 선택    |
| `previousState`            | object | 기기의 이전 상황 정보를 담고 있는 객체                           | 필수    |
| `previousState.brightness` | [BrightnessInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#BrightnessInfoObject) | 이전 밝기 정보를 담고 있는 객체                                | 선택    |

### Remarks

대상 기기에서 payload에 입력할 정보를 얻어올 수 없으면 값을 입력하지 않아도 됩니다. 이 경우 사용자에게 구체적인 정보 없이 기기 제어 요청이 정상 처리되었음을 알려줍니다.

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
주로 조명 기기를 제어할 때 사용되며, 대상 기기가 지정한 수준만큼 조명의 밝기를 높이도록 Clova Home extension에게 요청합니다. 이 요청에 대한 응답으로 [`IncrementBrightnessConfirmation`](#IncrementBrightnessConfirmation) 메시지를 사용해야 합니다.

### Payload fields

| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|---------|
| `accessToken`      | string                                  | IoT 서비스의 사용자 계정의 access token. CEK는 외부 서비스의 인증 서버로부터 획득한 사용자 계정의 access token을 전달합니다. 자세한 설명은 [사용자 계정 연결하기](/CEK/Guides/LinkUserAccount.md)를 참조합니다.                          | 필수    |
| `appliance`        | [ApplianceInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#ApplianceInfoObject)     | 대상 기기 정보를 담고 있는 객체. `applianceId` 필드는 필수입니다.     | 필수    |
| `deltaBrightness`       | [BrightnessInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#BrightnessInfoObject)             | 변경할 밝기의 크기 정보를 담고 있는 객체                              | 필수    |

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
[`IncrementChannelRequest`](#IncrementChannelRequest) 메시지에 대한 응답으로 대상 기기가 TV 채널을 높이도록 설정한 결과를 CEK에게 전달합니다.

### Payload fields

| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|---------|
| `channel`               | [TVChannelInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#TVChannelInfoObject) | 현재 TV 채널 정보를 담고 있는 객체                                | 선택    |
| `previousState`            | object | 기기의 이전 상황 정보를 담고 있는 객체                           | 선택    |
| `previousState.channel` | [TVChannelInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#TVChannelInfoObject) | 이전 TV 채널 정보를 담고 있는 객체                                | 선택    |

### Remarks

대상 기기에서 payload에 입력할 정보를 얻어올 수 없으면 값을 입력하지 않아도 됩니다. 이 경우 사용자에게 구체적인 정보 없이 기기 제어 요청이 정상 처리되었음을 알려줍니다.

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
    "channel": {
      "value": 14
    },
    "previousState": {
      "channel": {
        "value": 15
      }
    }
  }
}
```

{% endraw %}

### See also
* [`IncrementChannelRequest`](#IncrementChannelRequest)

## IncrementChannelRequest {#IncrementChannelRequest}
주로 TV나 셋톱박스를 제어할 때 사용되며, 대상 기기가 지정한 수준만큼 TV 채널을 높이도록 Clova Home extension에게 요청합니다. 이 요청에 대한 응답으로 [`IncrementChannelConfirmation`](#IncrementChannelConfirmation) 메시지를 사용해야 합니다.

### Payload fields

| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|---------|
| `accessToken`      | string                                  | IoT 서비스의 사용자 계정의 access token. CEK는 외부 서비스의 인증 서버로부터 획득한 사용자 계정의 access token을 전달합니다. 자세한 설명은 [사용자 계정 연결하기](/CEK/Guides/LinkUserAccount.md)를 참조합니다.                          | 필수    |
| `appliance`        | [ApplianceInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#ApplianceInfoObject)     | 대상 기기 정보를 담고 있는 객체. `applianceId` 필드는 필수입니다.     | 필수    |
| `deltaChannel`       | [TVChannelInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#TVChannelInfoObject)             | 변경할 TV 채널의 크기 정보를 담고 있는 객체                              | 필수    |

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
[`IncrementFanSpeedRequest`](#IncrementFanSpeedRequest) 메시지에 대한 응답으로 대상 기기가 팬의 속도를 높이도록 설정한 결과를 CEK에게 전달합니다.

### Payload fields

| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|---------|
| `fanSpeed`            | [SpeedInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#SpeedInfoObject) | 현재 팬의 속도 정보를 담고 있는 객체. 팬의 속도는 풍속을 의미하며 팬 속도를 다음과 같은 값으로 제한합니다.<ul><li><code>1</code>: 약한 바람(1단)</li><li><code>2</code>: 중간 바람(2단)</li><li><code>3</code>: 강한 바람(3단)</li></ul> | 선택    |
| `previousState`          | object                      | 기기의 이전 상황 정보를 담고 있는 객체                 | 선택    |
| `previousState.FanSpeed` | [SpeedInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#SpeedInfoObject) | 이전 팬의 속도 정보를 담고 있는 객체. 팬의 속도는 풍속을 의미하며 팬 속도를 다음과 같은 값으로 제한합니다.<ul><li><code>1</code>: 약한 바람(1단)</li><li><code>2</code>: 중간 바람(2단)</li><li><code>3</code>: 강한 바람(3단)</li></ul> | 선택    |

### Remarks

대상 기기에서 payload에 입력할 정보를 얻어올 수 없으면 값을 입력하지 않아도 됩니다. 이 경우 사용자에게 구체적인 정보 없이 기기 제어 요청이 정상 처리되었음을 알려줍니다.

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
주로 공기청정기와 같은 기기를 제어할 때 사용되며, 대상 기기가 지정한 값만큼 팬의 속도를 높이도록 Clova Home extension에게 요청합니다. 이 요청에 대한 응답으로 [`IncrementFanSpeedConfirmation`](#IncrementFanSpeedConfirmation) 메시지를 사용해야 합니다.

### Payload fields

| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|---------|
| `accessToken`      | string                                  | IoT 서비스의 사용자 계정의 access token. CEK는 외부 서비스의 인증 서버로부터 획득한 사용자 계정의 access token을 전달합니다. 자세한 설명은 [사용자 계정 연결하기](/CEK/Guides/LinkUserAccount.md)를 참조합니다.                          | 필수    |
| `appliance`        | [ApplianceInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#ApplianceInfoObject)     | 대상 기기 정보를 담고 있는 객체. `applianceId` 필드는 필수입니다. | 필수    |
| `deltaFanSpeed` | [SpeedInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#SpeedInfoObject) | 변경할 속도의 크기 정보를 담고 있는 객체. 팬의 속도는 풍속을 의미하며 팬 속도를 다음과 같은 값으로 제한합니다.<ul><li><code>1</code>: 약한 바람(1단)</li><li><code>2</code>: 중간 바람(2단)</li><li><code>3</code>: 강한 바람(3단)</li></ul>  | 필수    |

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
[`IncrementTargetTemperatureRequest`](#IncrementTargetTemperatureRequest) 메시지에 대한 응답으로 대상 기기가 온도를 높이도록 설정한 결과를 CEK에게 전달합니다.

### Payload fields

| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|---------|
| `targetTemperature` | [TemperatureInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#TemperatureInfoObject) | 현재 희망 온도 정보를 담고 있는 객체                               | 선택    |
| `previousState`     | object                                  | 기기의 이전 상황 정보를 담고 있는 객체                              | 선택    |
| `previousState.targetTemperature` | [TemperatureInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#TemperatureInfoObject) | 이전 희망 온도 정보를 담고 있는 객체                 | 선택    |

### Remarks

대상 기기에서 payload에 입력할 정보를 얻어올 수 없으면 값을 입력하지 않아도 됩니다. 이 경우 사용자에게 구체적인 정보 없이 기기 제어 요청이 정상 처리되었음을 알려줍니다.

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
      "value": 25
    },
    "previousState": {
      "targetTemperature": {
        "value": 22
      }
    }
  }
}
```

{% endraw %}

### See also
* [`IncrementTargetTemperatureRequest`](#IncrementTargetTemperatureRequest)

## IncrementTargetTemperatureRequest {#IncrementTargetTemperatureRequest}
주로 에어컨이나 온도 조절 장치와 같은 기기를 제어할 때 사용되며, 대상 기기가 지정한 값만큼 온도를 높이도록 Clova Home extension에게 요청합니다. 이 요청에 대한 응답으로 [`IncrementTargetTemperatureConfirmation`](#IncrementTargetTemperatureConfirmation) 메시지를 사용해야 합니다.

### Payload fields

| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|---------|
| `accessToken`      | string | IoT 서비스의 사용자 계정의 access token. CEK는 외부 서비스의 인증 서버로부터 획득한 사용자 계정의 access token을 전달합니다. 자세한 설명은 [사용자 계정 연결하기](/CEK/Guides/LinkUserAccount.md)를 참조합니다. | 필수    |
| `appliance`        | [ApplianceInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#ApplianceInfoObject)     | 대상 기기 정보를 담고 있는 객체. `applianceId` 필드는 필수입니다. | 필수    |
| `deltaTemperature` | [TemperatureInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#TemperatureInfoObject) | 변경할 온도의 크기 정보를 담고 있는 객체                              | 필수    |

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
      "value": 3
    }
  }
}
```

{% endraw %}

### See also
* [`IncrementTargetTemperatureConfirmation`](#IncrementTargetTemperatureConfirmation)

## IncrementVolumeConfirmation {#IncrementVolumeConfirmation}
[`IncrementVolumeRequest`](#IncrementVolumeRequest) 메시지에 대한 응답으로 대상 기기가 스피커 볼륨을 높이도록 설정한 결과를 CEK에게 전달합니다.

### Payload fields

| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|---------|
| `targetVolume` | [VolumeInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#VolumeInfoObject)               | 현재 볼륨 정보를 담고 있는 객체                               | 선택    |
| `previousState`     | object                                 | 기기의 이전 상황 정보를 담고 있는 객체                              | 선택    |
| `previousState.targetVolume` | [VolumeInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#VolumeInfoObject) | 이전 볼륨 정보를 담고 있는 객체                 | 선택    |

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
주로 TV 셋톱 박스와 같은 기기를 제어할 때 사용되며, 대상 기기가 지정한 값만큼 스피커 볼륨을 높이도록 Clova Home extension에게 요청합니다. 이 요청에 대한 응답으로 [`IncrementVolumeConfirmation`](#IncrementVolumeConfirmation) 메시지를 사용해야 합니다.

### Payload fields

| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|---------|
| `accessToken`      | string                                  | IoT 서비스의 사용자 계정의 access token. CEK는 외부 서비스의 인증 서버로부터 획득한 사용자 계정의 access token을 전달합니다. 자세한 설명은 [사용자 계정 연결하기](/CEK/Guides/LinkUserAccount.md)를 참조합니다.                          | 필수    |
| `appliance`        | [ApplianceInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#ApplianceInfoObject)     | 대상 기기 정보를 담고 있는 객체. `applianceId` 필드는 필수입니다. | 필수    |
| `deltaVolume` | [VolumeInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#VolumeInfoObject)                | 변경할 볼륨의 크기 정보를 담고 있는 객체                              | 필수    |

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
[`MuteRequest`](#MuteRequest) 메시지에 대한 응답으로 대상 기기의 소리를 끄도록 설정(음소거)한 결과를 CEK에게 전달합니다.

### Payload fields
없음

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
주로 TV나 셋톱박스와 같은 기기를 제어할 때 사용되며, 대상 기기의 소리를 끄도록(음소거) Clova Home extension에게 요청합니다. 이 요청에 대한 응답으로 [`MuteConfirmation`](#MuteConfirmation) 메시지를 사용해야 합니다.

### Payload fields

| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|---------|
| `accessToken`      | string                                  | IoT 서비스의 사용자 계정의 access token. CEK는 외부 서비스의 인증 서버로부터 획득한 사용자 계정의 access token을 전달합니다. 자세한 설명은 [사용자 계정 연결하기](/CEK/Guides/LinkUserAccount.md)를 참조합니다.                          | 필수    |
| `appliance`        | [ApplianceInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#ApplianceInfoObject)     | 대상 기기 정보를 담고 있는 객체. `applianceId` 필드는 필수입니다. | 필수    |

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
[`SetBrightnessRequest`](#SetBrightnessRequest) 메시지에 대한 응답으로 조명 밝기를 변경하도록 설정한 결과를 CEK에게 전달합니다.

### Payload fields

| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|---------|
| `brightness`               | [BrightnessInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#BrightnessInfoObject) | 현재 밝기 정보를 담고 있는 객체                                | 선택    |

### Remarks

대상 기기에서 payload에 입력할 정보를 얻어올 수 없으면 값을 입력하지 않아도 됩니다. 이 경우 사용자에게 구체적인 정보 없이 기기 제어 요청이 정상 처리되었음을 알려줍니다.

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
주로 조명 기기를 제어할 때 사용되며, 대상 기기가 조명 밝기를 지정한 값으로 변경하도록 Clova Home extension에게 요청합니다. 이 요청에 대한 응답으로 [`SetBrightnessConfirmation`](#SetBrightnessConfirmation) 메시지를 사용해야 합니다.

### Payload fields

| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|---------|
| `accessToken`   | string | IoT 서비스의 사용자 계정의 access token. CEK는 외부 서비스의 인증 서버로부터 획득한 사용자 계정의 access token을 전달합니다. 자세한 설명은 [사용자 계정 연결하기](/CEK/Guides/LinkUserAccount.md)를 참조합니다.                          | 필수    |
| `appliance`     | [ApplianceInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#ApplianceInfoObject) | 대상 기기 정보를 담고 있는 객체. `applianceId` 필드는 필수입니다. | 필수    |
| `brightness`       | [BrightnessInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#BrightnessInfoObject) | 대상 기기에 설정할 조명 밝기 정보를 담고 있는 객체                | 필수    |

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
[`SetChannelByNameRequest`](#SetChannelByNameRequest) 메시지에 대한 응답으로 채널 이름으로 TV 채널을 변경하도록 설정한 결과를 CEK에게 전달합니다.

### Payload fields

| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|---------|
| `channelName`               | [TVChannelNameInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#TVChannelNameInfoObject) | 현재 TV 채널의 이름 정보를 담고 있는 객체                                | 선택    |

### Remarks

대상 기기에서 payload에 입력할 정보를 얻어올 수 없으면 값을 입력하지 않아도 됩니다. 이 경우 사용자에게 구체적인 정보 없이 기기 제어 요청이 정상 처리되었음을 알려줍니다.

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
주로 TV 셋톱 박스와 같은 기기를 제어할 때 사용되며, 대상 기기가 지정한 채널 이름으로 채널을 변경하도록 Clova Home extension에게 요청합니다. 이 요청에 대한 응답으로 [`SetChannelByNameConfirmation`](#SetChannelByNameConfirmation) 메시지를 사용해야 합니다.

### Payload fields

| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|---------|
| `accessToken`   | string | IoT 서비스의 사용자 계정의 access token. CEK는 외부 서비스의 인증 서버로부터 획득한 사용자 계정의 access token을 전달합니다. 자세한 설명은 [사용자 계정 연결하기](/CEK/Guides/LinkUserAccount.md)를 참조합니다.                          | 필수    |
| `appliance`     | [ApplianceInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#ApplianceInfoObject) | 대상 기기 정보를 담고 있는 객체. `applianceId` 필드는 필수입니다. | 필수    |
| `channelName`       | [TVChannelNameInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#TVChannelNameInfoObject) | 대상 기기에 설정할 TV 채널의 이름 정보를 담고 있는 객체                | 필수    |

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
[`SetChannelRequest`](#SetChannelRequest) 메시지에 대한 응답으로 채널 번호로 TV 채널을 변경하도록 설정한 결과를 CEK에게 전달합니다.

### Payload fields

| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|---------|
| `channel`     | [TVChannelInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#TVChannelInfoObject)  | 대상 기기에 설정된 TV 채널 정보를 담고 있는 객체      | 선택    |

### Remarks

대상 기기에서 payload에 입력할 정보를 얻어올 수 없으면 값을 입력하지 않아도 됩니다. 이 경우 사용자에게 구체적인 정보 없이 기기 제어 요청이 정상 처리되었음을 알려줍니다.

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
주로 TV 셋톱 박스와 같은 기기를 제어할 때 사용되며, 대상 기기가 지정한 채널 번호로 채널을 변경하도록 Clova Home extension에게 요청합니다. 이 요청에 대한 응답으로 [`SetChannelConfirmation`](#SetChannelConfirmation) 메시지를 사용해야 합니다.

### Payload fields

| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|---------|
| `accessToken`   | string | IoT 서비스의 사용자 계정의 access token. CEK는 외부 서비스의 인증 서버로부터 획득한 사용자 계정의 access token을 전달합니다. 자세한 설명은 [사용자 계정 연결하기](/CEK/Guides/LinkUserAccount.md)를 참조합니다.                          | 필수    |
| `appliance`     | [ApplianceInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#ApplianceInfoObject) | 대상 기기 정보를 담고 있는 객체. `applianceId` 필드는 필수입니다. | 필수    |
| `channel`       | [TVChannelInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#TVChannelInfoObject) | 대상 기기에 설정할 TV 채널 정보를 담고 있는 객체                | 필수    |

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
[`SetFanSpeedRequest`](#SetFanSpeedRequest) 메시지에 대한 응답으로 팬 속도를 변경하도록 설정한 결과를 CEK에게 전달합니다.

### Payload fields

| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|---------|
| `fanSpeed`               | [SpeedInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#SpeedInfoObject) | 현재 팬의 속도 정보를 담고 있는 객체. 팬의 속도는 풍속을 의미하며 팬 속도를 다음과 같은 값으로 제한합니다.<ul><li><code>1</code>: 약한 바람(1단)</li><li><code>2</code>: 중간 바람(2단)</li><li><code>3</code>: 강한 바람(3단)</li></ul>   | 선택    |

### Remarks

대상 기기에서 payload에 입력할 정보를 얻어올 수 없으면 값을 입력하지 않아도 됩니다. 이 경우 사용자에게 구체적인 정보 없이 기기 제어 요청이 정상 처리되었음을 알려줍니다.

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
주로 공기청정기와 같은 기기를 제어할 때 사용되며, 대상 기기가 지정한 값으로 팬 속도를 변경하도록 Clova Home extension에게 요청합니다. 이 요청에 대한 응답으로 [`SetFanSpeedConfirmation`](#SetFanSpeedConfirmation) 메시지를 사용해야 합니다.

### Payload fields

| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|---------|
| `accessToken`   | string | IoT 서비스의 사용자 계정의 access token. CEK는 외부 서비스의 인증 서버로부터 획득한 사용자 계정의 access token을 전달합니다. 자세한 설명은 [사용자 계정 연결하기](/CEK/Guides/LinkUserAccount.md)를 참조합니다.                          | 필수    |
| `appliance`     | [ApplianceInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#ApplianceInfoObject) | 대상 기기 정보를 담고 있는 객체. `applianceId` 필드는 필수입니다. | 필수    |
| `fanSpeed`       | [SpeedInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#SpeedInfoObject) | 대상 기기에 설정할 팬의 속도 정보를 담고 있는 객체. 팬의 속도는 풍속을 의미하며 팬 속도를 다음과 같은 값으로 제한합니다.<ul><li><code>1</code>: 약한 바람(1단)</li><li><code>2</code>: 중간 바람(2단)</li><li><code>3</code>: 강한 바람(3단)</li></ul>     | 필수    |

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
[`SetLockStateRequest`](#SetLockStateRequest) 메시지에 대한 응답으로 대상 기기가 잠기거나 열리도록 설정한 결과를 CEK에게 전달합니다.

### Payload fields

| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|---------|
| `lockState`   | string  | 기기의 잠금 상태. 다음과 같은 값을 가집니다. <ul><li><code>"LOCKED"</code></li><li><code>"UNLOCKED"</code></li></ul> | 필수    |


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
주로 스마트 밸브와 같은 기기를 제어할 때 사용되며, 대상 기기를 잠그거나 열도록 Clova Home extension에게 요청합니다. 이 요청에 대한 응답으로 [`SetLockStateConfirmation`](#SetLockStateConfirmation) 메시지를 사용해야 합니다.

### Payload fields

| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|---------|
| `accessToken`   | string | IoT 서비스의 사용자 계정의 access token. CEK는 외부 서비스의 인증 서버로부터 획득한 사용자 계정의 access token을 전달합니다. 자세한 설명은 [사용자 계정 연결하기](/CEK/Guides/LinkUserAccount.md)를 참조합니다.                          | 필수    |
| `appliance`     | [ApplianceInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#ApplianceInfoObject) | 대상 기기 정보를 담고 있는 객체. `applianceId` 필드는 필수입니다. | 필수    |
| `lockState`       | string | 설정할 기기의 잠금 상태. 다음과 같은 값을 가집니다. <ul><li><code>"LOCKED"</code></li><li><code>"UNLOCKED"</code></li></ul> | 필수    |

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
[`SetModeRequest`](#SetModeRequest) 메시지에 대한 응답으로 운전 모드(operation mode)를 변경하도록 설정한 결과를 CEK에게 전달합니다.

### Payload fields

| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|---------|
| `mode`        | [ModeInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#ModeInfoObject)  | 대상 기기에 설정된 운전 모드 정보를 담고 있는 객체      | 선택    |

### Remarks

대상 기기에서 payload에 입력할 정보를 얻어올 수 없으면 값을 입력하지 않아도 됩니다. 이 경우 사용자에게 구체적인 정보 없이 기기 제어 요청이 정상 처리되었음을 알려줍니다.

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
      "value": "sleep"
    }
  }
}
```

{% endraw %}

### See also
* [`SetModeRequest`](#SetModeRequest)

## SetModeRequest {#SetModeRequest}
기기의 운전 모드(operation mode)를 제어할 때 사용되며, 기기의 운전 모드를 지정한 값으로 변경하도록 Clova Home extension에게 요청합니다. 이 요청에 대한 응답으로 [`SetModeConfirmation`](#SetModeConfirmation) 메시지를 사용해야 합니다.

### Payload fields

| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|---------|
| `accessToken` | string  | IoT 서비스의 사용자 계정의 access token. CEK는 외부 서비스의 인증 서버로부터 획득한 사용자 계정의 access token을 전달합니다. 자세한 설명은 [사용자 계정 연결하기](/CEK/Guides/LinkUserAccount.md)를 참조합니다. | 필수    |
| `appliance`   | [ApplianceInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#ApplianceInfoObject)     | 대상 기기 정보를 담고 있는 객체. `applianceId` 필드는 필수입니다. | 필수    |
| `mode`        | [ModeInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#ModeInfoObject) | 대상 기기에 설정할 운전 모드 정보를 담고 있는 객체                         | 필수    |

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
[`SetTargetTemperatureRequest`](#SetTargetTemperatureRequest) 메시지에 대한 응답으로 희망 온도를 변경하도록 설정한 결과를 CEK에게 전달합니다.

### Payload fields

| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|---------|
| `targetTemperature`               | [TemperatureInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#TemperatureInfoObject) | 현재 희망 온도 정보를 담고 있는 객체                                | 선택    |

### Remarks

대상 기기에서 payload에 입력할 정보를 얻어올 수 없으면 값을 입력하지 않아도 됩니다. 이 경우 사용자에게 구체적인 정보 없이 기기 제어 요청이 정상 처리되었음을 알려줍니다.

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
      "value": 22
    }
  }
}
```

{% endraw %}

### See also
* [`SetTargetTemperatureRequest`](#SetTargetTemperatureRequest)

## SetTargetTemperatureRequest {#SetTargetTemperatureRequest}
주로 에어컨이나 온도 조절 장치와 같은 기기를 제어할 때 사용되며, 대상 기기가 희망 온도를 지정한 값으로 변경하도록 Clova Home extension에게 요청합니다. 이 요청에 대한 응답으로 [`SetTargetTemperatureConfirmation`](#SetTargetTemperatureConfirmation) 메시지를 사용해야 합니다.

### Payload fields

| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|---------|
| `accessToken`   | string | IoT 서비스의 사용자 계정의 access token. CEK는 외부 서비스의 인증 서버로부터 획득한 사용자 계정의 access token을 전달합니다. 자세한 설명은 [사용자 계정 연결하기](/CEK/Guides/LinkUserAccount.md)를 참조합니다.                          | 필수    |
| `appliance`     | [ApplianceInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#ApplianceInfoObject) | 대상 기기 정보를 담고 있는 객체. `applianceId` 필드는 필수입니다. | 필수    |
| `targetTemperature`       | [TemperatureInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#TemperatureInfoObject) | 대상 기기에 설정할 희망 온도 정보를 담고 있는 객체                | 필수    |

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
      "value": 22
    }
  }
}
```

{% endraw %}

### See also
* [`SetTargetTemperatureConfirmation`](#SetTargetTemperatureConfirmation)

## TurnOffConfirmation {#TurnOffConfirmation}
[`TurnOffRequest`](#TurnOffRequest) 메시지에 대한 응답으로 대상 기기를 끄도록 설정한 결과를 CEK에게 전달합니다.

### Payload fields
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
* [`TurnOffRequest`](#TurnOffRequest)

## TurnOffRequest {#TurnOffRequest}
대상 기기를 끄도록 Clova Home extension에게 요청합니다. 이 요청에 대한 응답으로 [`TurnOffConfirmation`](#TurnOffConfirmation) 메시지를 사용해야 합니다.

### Payload fields

| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|---------|
| `accessToken`      | string                                  | IoT 서비스의 사용자 계정의 access token. CEK는 외부 서비스의 인증 서버로부터 획득한 사용자 계정의 access token을 전달합니다. 자세한 설명은 [사용자 계정 연결하기](/CEK/Guides/LinkUserAccount.md)를 참조합니다.                          | 필수    |
| `appliance`        | [ApplianceInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#ApplianceInfoObject)     | 대상 기기 정보를 담고 있는 객체. `applianceId` 필드는 필수입니다. | 필수    |

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
[`TurnOnRequest`](#TurnOnRequest) 메시지에 대한 응답으로 대상 기기를 켜도록 설정한 결과를 CEK에게 전달합니다.

### Payload fields
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
* [`TurnOnRequest`](#TurnOnRequest)

## TurnOnRequest {#TurnOnRequest}
대상 기기를 켜도록 Clova Home extension에게 요청합니다. 이 요청에 대한 응답으로 [`TurnOnConfirmation`](#TurnOnConfirmation) 메시지를 사용해야 합니다.

### Payload fields

| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|---------|
| `accessToken`      | string                                  | IoT 서비스의 사용자 계정의 access token. CEK는 외부 서비스의 인증 서버로부터 획득한 사용자 계정의 access token을 전달합니다. 자세한 설명은 [사용자 계정 연결하기](/CEK/Guides/LinkUserAccount.md)를 참조합니다.                          | 필수    |
| `appliance`        | [ApplianceInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#ApplianceInfoObject)     | 대상 기기 정보를 담고 있는 객체. `applianceId` 필드는 필수입니다. | 필수    |

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
[`UnmuteRequest`](#UnmuteRequest) 메시지에 대한 응답으로 대상 기기의 소리를 켜도록 설정(음소거 해제)한 결과를 CEK에게 전달합니다.

### Payload fields
없음

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
주로 TV나 셋톱박스와 같은 기기를 제어할 때 사용되며, 대상 기기의 소리를 켜도록(음소거 해제) Clova Home extension에게 요청합니다. 이 요청에 대한 응답으로 [`UnmuteConfirmation`](#UnmuteConfirmation) 메시지를 사용해야 합니다.

### Payload fields

| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|---------|
| `accessToken`      | string                                  | IoT 서비스의 사용자 계정의 access token. CEK는 외부 서비스의 인증 서버로부터 획득한 사용자 계정의 access token을 전달합니다. 자세한 설명은 [사용자 계정 연결하기](/CEK/Guides/LinkUserAccount.md)를 참조합니다.                          | 필수    |
| `appliance`        | [ApplianceInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#ApplianceInfoObject)     | 대상 기기 정보를 담고 있는 객체. `applianceId` 필드는 필수입니다. | 필수    |

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
