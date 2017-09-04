# Discovery API

사용자 계정에 등록된 IoT 기기 목록을 확인할 때 사용되는 API입니다.

| 메시지 이름         | 메시지 타입  | 메시지 설명                                   |
|------------------|-----------|---------------------------------------------|
| [`DiscoverAppliancesRequest`](#DiscoverAppliancesRequest)                     | Request  | 사용자가 등록한 IoT 기기 목록을 Clova Home extension에게 요청합니다.             |
| [`DiscoverAppliancesResponse`](#DiscoverAppliancesResponse)                   | Response | [`DiscoverAppliancesRequest`](#DiscoverAppliancesRequest) 메시지에 대한 응답으로 사용자가 등록한 IoT 기기 목록을 CEK에게 전달합니다. |

## DiscoverAppliancesRequest {#DiscoverAppliancesRequest}
사용자가 등록한 기기 목록을 Clova Home extension에게 요청합니다. 이 요청에 대한 응답으로 [`DiscoverAppliancesResponse`](#DiscoverAppliancesResponse) 메시지를 사용해야 합니다.

### Payload field

| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|---------|
| `accessToken`   | string  | Clova Home extension의 access token  | 필수     |

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
* [`DiscoverAppliancesResponse`](#DiscoverAppliancesResponse)

## DiscoverAppliancesResponse {#DiscoverAppliancesResponse}
사용자가 등록한 기기 목록을 CEK에게 전달합니다. 이 메시지는 [`DiscoverAppliancesRequest`](#DiscoverAppliancesRequest) 메시지에 대한 응답으로 사용됩니다.

### Payload field

| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|---------|
| `discoveredAppliances[]`  | [ApplianceObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#ApplianceObject) array  | 사용자 계정에 등록된 기기 목록을 표현하는 객체 배열          | 필수    |

### Remarks
IoT 서비스를 제공할 때 각 사용자 계정에 등록된 기기 목록을 제공해야 합니다.

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
          "TurnOn",
          "TurnOff"
        ],
        "applianceTypes": ["SMARTPLUG"],
        "additionalApplianceDetails": {}
      }
    ]
  }
}
```
{% endraw %}

### See also
* [`DiscoverAppliancesRequest`](#DiscoverAppliancesRequest)
