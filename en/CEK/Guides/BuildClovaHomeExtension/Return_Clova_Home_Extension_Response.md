## Returning Clova Home extension responses {#ReturnClovaHomeExtensionResponse}

A Clova Home extension developer must design the code to return the processed result to CEK (HTTPS response). Responses from the Clova home extension have the following characteristics:

* When the device state information is requested, the response may be different from the actual, up-to-date state of the device because the information is obtained from the IoT service.
* When device control is requested, the response does not return the final state of the device but only whether the user request was delivered successfully to the IoT service.
* When the request is processed successfully, the response must use an appropriate [interface](/CEK/References/CEK_API.md#ClovaHomeExtInterface) for the [Clova Home extension request](#HandleClovaHomeExtensionRequest) as shown below.

When a control request such as "Turn on the light" ([`TurnOnRequest`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#TurnOnRequest)) is sent to the IoT service and the service responds that the request has been processed properly, the extension must send the result to CEK using the [`TurnOnConfirmation`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#TurnOnConfirmation) message as shown below.

{% raw %}
```json
{
  "header": {
    "messageId": "4ec35000-88ce-4724-b7e4-7f52050558fd",
    "name": "TurnOnConfirmation",
    "namespace": "ClovaHome",
    "payloadVersion": "1.0"
  },
  "payload": {}
}
```
{% endraw %}

If an error occurs while performing the user request, the extension must send the error to CEK using the [Error API](/CEK/References/ClovaHomeInterface/Error_Interfaces.md). Clova performs error handling according to the received API.

Below is an example of sending a `TargetOfflineError` error message due to failing to connect to the device.

{% raw %}
```json
{
  "header": {
    "messageId": "fef949b7-eb94-4bda-a417-2cfb604194c3",
    "namespace": "ClovaHome",
    "name": "TargetOfflineError",
    "payloadVersion": "1.0"
  },
  "payload": {
  }
}
```
{% endraw %}


<div class="note">
<p><strong>Note!</strong></p>
<p>You must use the HTTP 200 OK response even when sending an error message.</p>
</div>
