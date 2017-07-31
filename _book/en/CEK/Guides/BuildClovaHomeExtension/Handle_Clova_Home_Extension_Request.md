## Handling Clova Home extension request {#HandleClovaHomeExtensionRequest}

A user can request Clova to control his or her IoT device by saying, for example, "Turn on the living room light" (HTTPS request). When a user makes such a request related to controlling IoT devices, verification is performed whether the request can be carried out by looking at the list of available devices and their allowed actions obtained through [Device discovery](#ProvideDeviceDiscovery). Following the verification, the request is sent to your Clova Home extension through CEK using [Clova Home API](/CEK/References/Clova_Home_API.md).

Requests such as "Turn on the living room light" is sent using a *[TurnOnRequest](/CEK/References/Clova_Home_API.md#TurnOnRequest)* message as follows.

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

The received message is analyzed and the request is sent to the URI of the IoT service. At which point, the previously obtained access token is passed together. Then, you analyze the fields, process the user request, and return a [Response message](#ReturnClovaHomeExtensionResponse).
