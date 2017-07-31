## Device discovery {#ProvideDeviceDiscovery}

When a user enables an IoT service, the client app or the app paired with client device is required to provide a list of IoT devices registered to the user's account. When your Clova Home extension receives a [DiscoverAppliancesRequest](/CEK/References/Clova_Home_API.md#DiscoverAppliancesRequest) message from CEK (HTTPS request), it obtains a list of devices registered to the user account from the IoT service using the access token for the user's account. Then, your Clova Home extension returns a [DiscoverAppliancesResponse](/CEK/References/Clova_Home_API.md#DiscoverAppliancesResponse) message (HTTPS response). See [Clova Home message format](/CEK/References/Clova_Home_Extension_Message_Format.md) for more details on message communicated between CEK and Clova Home extension.

![](/CEK/Resources/Images/CEK_Clova_Home_Extension_Sequence_Diagram.png)

This is an example *[DiscoverAppliancesRequest](/CEK/References/Clova_Home_API.md#DiscoverAppliancesRequest)* message sent to a Clova Home extension.
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

Upon receiving the message, the Clova Home extension finds the user account using the access token and returns the list of devices registered to the user's account using a *[DiscoverAppliancesResponse](/CEK/References/Clova_Home_API.md#DiscoverAppliancesResponse)* message.

This is an example message of *DiscoverAppliancesResponse* sent to CEK from Clova Home extension.

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