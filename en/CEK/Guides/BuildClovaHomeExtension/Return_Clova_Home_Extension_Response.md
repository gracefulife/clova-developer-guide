## Returning Clova Home extension response {#ReturnClovaHomeExtensionResponse}

You must have your Clova Home extension return processing results back to CEK (HTTPS response). Responses from a Clova Home extension have the following characteristics.

* When the request is about obtaining information on appliance states, the information is obtained from the IoT service, which means the information may not reflect actual current states.
* When the request is about controlling an appliance, your extension does not return its final state after necessary change has been made. Instead, the returned response just verifies that the user's request has been successfully forwarded to the IoT service.
* When the request has been processed properly, you must respond to the [Clova Home extension request](#HandleClovaHomeExtensionRequest) using an appropriate [interface](/CEK/References/CEK_API.md#ClovaHomeExtInterface).

When [`TurnOnRequest`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#TurnOnRequest) (request to control an appliance such as "Turn on the light") is forwarded to an IoT service and the IoT service responds that the request has been processed properly, you must return the result back to CEK with a [`TurnOnConfirmation`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#TurnOnConfirmation) message.

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

If any error occurs while processing user requests, you must return an appropriate error message to CEK using the [Error API](/CEK/References/ClovaHomeInterface/Error_Interfaces.md). Clova processes errors accordingly based on the API it has received.

This is an example of when a `TargetOfflineError` message is returned due to a connection problem with an appliance.

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
<p>Responses must use HTTP 200 OK even when they return an error message.</p>
</div>
