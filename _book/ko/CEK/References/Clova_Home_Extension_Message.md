## Clova Home extension 메시지 {#ClovaHomeExtMessage}
Clova Home extension 메시지는 IoT 기기를 제어하는 extension이 CEK와 정보를 주고 받을 때 전용으로 사용하는 메시지 스펙입니다. 여기에서는 Clova Home extension 메시지의 [메시지 포맷](#ClovaHomeExtMessageFormat)과 [인터페이스](#ClovaHomeExtInterface)에 대해 설명합니다.

### 메시지 포맷 {#ClovaHomeExtMessageFormat}

Clova Home extension 메시지는 `header` 필드와 `payload` 필드로 구성되어 있으며, 이는 요청 메시지와 응답 메시지 모두 동일합니다. 이 중에서 `payload` 필드는 사용된 [인터페이스](#ClovaHomeExtInterface)에 따라 그 구성이 달라질 수 있습니다. 여기에서는 Clova Home extension 메시지의 공통된 포맷에 대해 설명합니다.

<div class="note">
  <p><strong>Note!</strong></p>
  <p>Clova Home extension 메시지는 요청 메시지와 응답 메시지로 구분됩니다. CEK가 extension으로 보내는 요청 메시지는 `XxxxRequest`와 같은 이름을 가지며, extension이 CEK로 보내는 응답 메시지는 `XxxxConfirmation`이나 `XxxxResponse` 형태의 이름을 가집니다. 또한, 오류 상황에도 정상적인 HTTPS 응답(200 OK)을 보내야 하며, 이때 `XxxxError`와 같은 이름의 응답 메시지를 보내야 합니다.</p>
</div>

#### Message structure
{% raw %}
```json
{
  "header": {
    "messageId": {{string}},
    "namespace": {{string}},
    "name": {{string}},
    "payloadVersion": {{string}}
  },
  "payload": {{object}}
}
```
{% endraw %}


#### Message fields
| 필드 이름       | 자료형    | 필드 설명                     | 필수/포함 여부 |
|---------------|---------|-----------------------------|:-------------:|
| `header`                 | object | 메시지의 헤더                                                                                            | 필수/항상     |
| `header.messageId`       | string | 메시지 ID(UUID). 개별 메시지를 구분하기 위해 Clova에서 생성한 식별자입니다.                                         | 필수/항상     |
| `header.name`            | string | 메시지의 API 이름                                                                                        | 필수/항상     |
| `header.namespace`       | string | 이 필드는 `"ClovaHome"`으로 고정됩니다.                                                                     | 필수/항상     |
| `header.payloadVersion`  | string | `header.name`에 명시된 Clova Home extension 메시지의 버전. 이 버전에 따라 `payload` 필드의 구성이 달라질 수 있습니다.  | 필수/항상     |
| `payload`                | object | `header.name`에 지정된 [인터페이스](#ClovaHomeExtInterface)에 따라 payload 객체의 구성과 필드 값이 달라집니다.       | 필수/항상     |

#### Message example
{% raw %}
```json
예제 1: DiscoverAppliancesRequest - 요청 메시지
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

예제 2: DiscoverAppliancesResponse - 응답 메시지
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
            "DecrementBrightness",
            "HealthCheck",
            "IncrementBrightness",
            "SetBrightness",
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
          "HealthCheck",
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

예제 3: IncrementTargetTemperatureConfirmation - 응답 메시지
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

예제 4: TargetOffLineError - 오류 응답 메시지
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

#### See also
* [Clova Home extension 만들기](/CEK/Guides/Build_Clova_Home_Extension.md)
* [인터페이스](#ClovaHomeExtInterface)

### 인터페이스 {#ClovaHomeExtInterface}
Clova Home extension 메시지의 인터페이스는 다음과 같이 분류됩니다.

* 인터페이스
  * [Discovery 인터페이스](/CEK/References/ClovaHomeInterface/Discovery_Interfaces.md)
  * [Control 인터페이스](/CEK/References/ClovaHomeInterface/Control_Interfaces.md)
  * [Error 인터페이스](/CEK/References/ClovaHomeInterface/Error_Interfaces.md)

* 공유 객체
  * [공유 객체](/CEK/References/ClovaHomeInterface/Shared_Objects.md)
