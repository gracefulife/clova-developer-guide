## Discovery 기능 제공하기 {#ProvideDeviceDiscovery}

사용자가 IoT 서비스를 사용하도록 설정하면 클라이언트 앱이나 클라이언트 기기와 페어링하는 앱에서 사용자 계정에 등록된 IoT 기기 목록을 제공해야 합니다. Clova Home extension은 CEK로부터 [`DiscoverAppliancesRequest`](/CEK/References/ClovaHomeInterface/Discovery_Interfaces.md#DiscoverAppliancesRequest) 메시지를 받게 됩니다(HTTP Request). Clova Home extension은 전달받은 사용자 계정의 access token을 이용하여 IoT 서비스로부터 사용자 계정에 등록된 기기 목록을 가져와야 하며, 이를 [`DiscoverAppliancesResponse`](/CEK/References/ClovaHomeInterface/Discovery_Interfaces.md#DiscoverAppliancesResponse) 메시지를 사용해서 응답해야 합니다(HTTP Response). CEK와 Clova Home extension 사이에 주고 받는 메시지에 대한 자세한 설명은 [Clova Home extension 메시지](/CEK/References/CEK_API.md#ClovaHomeExtMessage)을 참조합니다.

![](/CEK/Resources/Images/CEK_Clova_Home_Extension_Sequence_Diagram.png)

다음은 Clova Home extension이 전달받는 [`DiscoverAppliancesRequest`](/CEK/References/ClovaHomeInterface/Discovery_Interfaces.md#DiscoverAppliancesRequest) 메시지 예입니다.
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

위 메시지를 받으면 Clova Home extension은 전달받은 access token을 이용하여 사용자 계정을 찾고, 사용자 계정에 등록된 기기 목록을 [`DiscoverAppliancesResponse`](/CEK/References/ClovaHomeInterface/Discovery_Interfaces.md#DiscoverAppliancesResponse) 메시지로 돌려줘야 합니다. 각 기기별로 기기의 식별자 및 이름, 기기의 타입, 사용 가능 여부(Online 여부) 그리고 지원되는 동작(`actions`)과 같은 정보를 포함하고 있습니다.

다음은 Clova Home extension이 `DiscoverAppliancesResponse` 메시지로 CEK에게 응답한 예입니다.

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
        "isIr": false,
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
        "additionalApplianceDetails": {},
        "location": ""
      },
      {
        "applianceId": "device-002",
        "manufacturerName": "device-manufacturer-name",
        "modelName": "스마트 플러그",
        "version": "v1.0",
        "friendlyName": "부엌 플러그",
        "friendlyDescription": "에너지를 절약하는 플러그",
        "isIr": false,
        "isReachable": true,
        "actions": [
          "HealthCheck",
          "TurnOn",
          "TurnOff"
        ],
        "applianceTypes": ["SMARTPLUG"],
        "additionalApplianceDetails": {},
        "location": "LIVING_ROOM"
      }
    ]
  }
}
```
{% endraw %}
