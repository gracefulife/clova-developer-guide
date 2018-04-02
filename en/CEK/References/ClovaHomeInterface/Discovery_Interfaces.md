# Discovery

The discovery interfaces are used to check a list of IoT devices registered to a user account.

| Message name         | Type  | Description                                   |
|------------------|-----------|---------------------------------------------|
| [`DiscoverAppliancesRequest`](#DiscoverAppliancesRequest)   | Request  | Requests the list of IoT devices registered by the user to the Clova Home extension.             |
| [`DiscoverAppliancesResponse`](#DiscoverAppliancesResponse) | Response | Sends the list of IoT devices registered by the user to CEK as response to the [`DiscoverAppliancesRequest`](#DiscoverAppliancesRequest) message. |

## DiscoverAppliancesRequest {#DiscoverAppliancesRequest}
Request the list of IoT devices registered by the user to the Clova Home extension. The extension must use the [`DiscoverAppliancesResponse`](#DiscoverAppliancesResponse) message as response to this request.

### Payload fields

| Field name       | Data type    | Description                     | Included |
|---------------|---------|-----------------------------|:---------:|
| `accessToken`   | string  | Access token of the Clova Home extension  | Always     |

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
Sends the list of IoT devices registered by the user to CEK. This message is used as a response to the [`DiscoverAppliancesRequest`](#DiscoverAppliancesRequest) message.

### Payload fields

| Field name       | Data type    | Description                     | Required |
|---------------|---------|-----------------------------|:---------:|
| `discoveredAppliances[]`  | [ApplianceInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#ApplianceInfoObject) array  | An object array that expresses the appliance list registered to the user account.          | Required    |

### Remarks
You must provide the list of appliances registered in each user account when you provide the IoT service.

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
        "modelName": "Smart lamp,"
        "version": "v1.0",
        "friendlyName": "Living room lamp,"
        "friendlyDescription": "A lamp that can be controlled using a smartphone,"
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
        "additionalApplianceDetails": {}
      },
      {
        "applianceId": "device-002",
        "manufacturerName": "device-manufacturer-name",
        "modelName": "Smart plug,"
        "version": "v1.0",
        "friendlyName": "Kitchen plug,"
        "friendlyDescription": "An energy-saving plug,"
        "isReachable": true,
        "actions": [
          "HealthCheck",
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
