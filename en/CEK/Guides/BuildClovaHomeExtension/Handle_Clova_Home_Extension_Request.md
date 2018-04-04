## Handling a Clova Home extension request {#HandleClovaHomeExtensionRequest}

Users can make requests (HTTPS request) to Clova in order to control an IoT device, with commands such as "Turn on the light." The client uses the [device discovery](#ProvideDeviceDiscovery) function to check the list of available devices and the permitted actions per device, and verify whether the control request can be carried out. Once verified, the user request is delivered to the Clova Home extension via CEK using the [Clova Home extension message](/CEK/References/CEK_API.md#ClovaHomeExtMessage).

Requests, such as "Turn on the light" is sent using the [`TurnOnRequest`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#TurnOnRequest) message as shown below.

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

The extension can then analyze the received message to send the control request for the IoT device using the URI provided by the IoT service. Make sure to send the control request with the previously obtained access token.
