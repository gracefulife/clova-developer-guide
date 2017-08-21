## Clova Home extension 요청 처리하기 {#HandleClovaHomeExtensionRequest}

사용자는 "거실 전등 켜줘"와 같이 IoT 기기를 제어하도록 Clova에게 요청합니다(HTTPS Request). 클라이언트는 [Discovery 기능](#ProvideDeviceDiscovery)을 통해 확보된 기기 목록과 각 기기별 허용 동작을 보고 사용자의 IoT 기기 제어 요청이 수행 가능한 요청인지 검증합니다. 검증된 사용자 요청은 CEK를 통해 Clova Home extension으로 전달되며 이때, [Clova Home API](/CEK/References/Clova_Home_API.md)를 이용합니다.

"거실 전등 켜줘"와 같은 요청은 다음과 같이 [`TurnOnRequest`](/CEK/References/Clova_Home_API.md#TurnOnRequest) 메시지로 전달됩니다.

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

요청 받은 메시지를 분석하여 IoT 서비스가 제공하는 URI로 사용자의 IoT 기기 제어 요청을 전달하면 됩니다. 이때 함께 전달받은 access token을 사용하여 요청합니다. 필드를 분석하여 사용자의 요청을 처리한 후 [응답 메시지](#ReturnClovaHomeExtensionResponse)를 보내면 됩니다.
