## Providing device discovery {#ProvideDeviceDiscovery}

When a user enables an IoT service, the client app or the app paired with the client device must provide a list of IoT appliances registered on the user's account. When your Clova Home extension receives a [`DiscoverAppliancesRequest`](/CEK/References/ClovaHomeInterface/Discovery_Interfaces.md#DiscoverAppliancesRequest) message from CEK (HTTPS request), it obtains a list of appliances registered on the user's account from the IoT service using an access token for the account. Then, your Clova Home extension returns a [`DiscoverAppliancesResponse`](/CEK/References/ClovaHomeInterface/Discovery_Interfaces.md#DiscoverAppliancesResponse) message (HTTPS response). See [Clova Home extension message](/CEK/References/CEK_API.md#ClovaHomeExtMessage) for more details on messages sent and received between CEK and a Clova Home extension.

![](/CEK/Resources/Images/CEK_Clova_Home_Extension_Sequence_Diagram.png)

This is an example of a [`DiscoverAppliancesRequest`](/CEK/References/ClovaHomeInterface/Discovery_Interfaces.md#DiscoverAppliancesRequest) message sent to a Clova Home extension.
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

When the Clova Home extension receives this message, it finds the user account for the access token and returns the list of appliances registered on the user's account, using a [`DiscoverAppliancesResponse`](/CEK/References/ClovaHomeInterface/Discovery_Interfaces.md#DiscoverAppliancesResponse) message. The message contains details of each appliance, such as appliance identifiers, appliance names, appliance availability (whether online or not), and supported actions (`actions`).

This is an example of a `DiscoverAppliancesResponse` message which a Clova Home extension returns to CEK.

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
