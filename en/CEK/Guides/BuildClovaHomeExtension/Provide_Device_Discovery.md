## Device discovery {#ProvideDeviceDiscovery}

When the user sets up to use an IoT service, the client app or an app paired with the client device must provide the IoT device list registered to the user account. The Clova Home extension receives a [`DiscoverAppliancesRequest`](/CEK/References/ClovaHomeInterface/Discovery_Interfaces.md#DiscoverAppliancesRequest) message from CEK (HTTPS request). Then the Clova Home extension must import the IoT device list registered to the user account from the IoT service using the access token associated to the user account and respond using the [`DiscoverAppliancesResponse`](/CEK/References/ClovaHomeInterface/Discovery_Interfaces.md#DiscoverAppliancesResponse) message (HTTPS response). For more information on the messages exchanged between CEK and Clova Home extensions, see [Clova Home extension message](/CEK/References/CEK_API.md#ClovaHomeExtMessage).

![](/CEK/Resources/Images/CEK_Clova_Home_Extension_Sequence_Diagram.png)

Below is an example of the [`DiscoverAppliancesRequest`](/CEK/References/ClovaHomeInterface/Discovery_Interfaces.md#DiscoverAppliancesRequest) message received by the Clova Home extension.
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

After receiving the above message, the Clova Home extension must identify the user account using the previously obtained access token and return the device list registered in that account using the [`DiscoverAppliancesResponse`](/CEK/References/ClovaHomeInterface/Discovery_Interfaces.md#DiscoverAppliancesResponse) message. The device list includes information such as device identifier, name, type, availability (online/offline), and supported actions (`actions`) for each device.

Below is an example of the Clova Home extension responding to CEK using the `DiscoverAppliancesResponse` message.

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
        "modelName": "Smart lamp",
        "version": "v1.0",
        "friendlyName": "Living room lamp",
        "friendlyDescription": "A lamp that can be controlled using a smartphone",
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
        "modelName": "Smart plug",
        "version": "v1.0",
        "friendlyName": "Kitchen plug",
        "friendlyDescription": "An energy-saving plug",
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
