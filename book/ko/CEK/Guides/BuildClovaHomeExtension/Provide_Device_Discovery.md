## Discovery 기능 제공하기 {#ProvideDeviceDiscovery}

사용자가 IoT 서비스를 사용하도록 설정하면 클라이언트 앱이나 클라이언트 기기와 페어링하는 앱에서 사용자 계정에 등록된 IoT 기기 목록을 제공해야 합니다. Clova Home extension은 CEK로부터 [DiscoverAppliancesRequest](/CEK/References/Clova_Home_API.md#DiscoverAppliancesRequest) 메시지를 받게 됩니다(HTTPS Request). Clova Home extension은 전달받은 사용자 계정의 access token을 이용하여 IoT 서비스로부터 사용자 계정에 등록된 기기 목록을 가져와야 하며, 이를 [DiscoverAppliancesResponse](/CEK/References/Clova_Home_API.md#DiscoverAppliancesResponse) 메시지를 사용해서 응답해야 합니다(HTTPS Response). CEK와 Clova Home extension 사이에 주고 받는 메시지에 대한 자세한 설명은 [Clova Home 메시지 포맷](/CEK/References/Clova_Home_Extension_Message_Format.md)을 참조합니다.

![](/CEK/Resources/Images/CEK_Clova_Home_Extension_Sequence_Diagram.png)

다음은 Clova Home extension이 전달받는 *[DiscoverAppliancesRequest](/CEK/References/Clova_Home_API.md#DiscoverAppliancesRequest)* 메시지 예입니다.
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

위 메시지를 받으면 Clova Home extension은 전달받은 access token을 이용하여 사용자 계정을 찾고, 사용자 계정에 등록된 기기 목록을 *[DiscoverAppliancesResponse](/CEK/References/Clova_Home_API.md#DiscoverAppliancesResponse)* 메시지로 돌려줘야 합니다.

다음은 Clova Home extension이 *DiscoverAppliancesResponse* 메시지로 CEK에게 응답한 예입니다.

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
```
{% endraw %}
