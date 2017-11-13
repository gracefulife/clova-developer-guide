## Handling Clova Home extension request {#HandleClovaHomeExtensionRequest}

Users can make a verbal request to Clova to control their IoT appliances, such as "Turn on the light" (HTTPS request). When users make such requests to their IoT appliance, the client checks the list of available appliances and their allowed actions obtained through [device discovery](#ProvideDeviceDiscovery) and verifies whether it can carry out the request. The verified request is then sent to your Clova Home extension through CEK, using [Clova Home extension messages](/CEK/References/CEK_API.md#ClovaHomeExtMessage).

Requests such as "Turn on the light" is sent with a [`TurnOnRequest`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#TurnOnRequest) message as follows.

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

The received message is analyzed and the request is sent to the URI of the IoT service. At which point, the previously obtained access token is passed together. Then, you analyze the fields, process the user request, and return a [response message](#ReturnClovaHomeExtensionResponse).