## Returning Clova Home extension response {#ReturnClovaHomeExtensionResponse}

Your Clova Home extension must return processing results back to CEK (HTTPS response). Responses from Clova Home extension have the following characteristics.

* When the request is about obtaining information of appliance state, the information is obtained from the IoT service, which means the information may not reflect actual current state.
* When the request is about controlling an appliance, your extension does not return final state of the appliance after necessary change has been made. Instead, the returned response only verifies that the user's request has been successfully forwarded to the IoT service.
* When the request is processed properly, you must respond to the [Clova Home extension request](#HandleClovaHomeExtensionRequest) by returning a message using the appropriate [Clova Home API](/CEK/References/Clova_Home_API.md).

| Clova Home extension request API | Clova Home extension response API |
|------------------------------|------------------------------|
| DecrementTargetTemperatureRequest | DecrementTargetTemperatureConfirmation |
| DiscoverAppliancesRequest         | DiscoverAppliancesResponse             |
| GetLockStateRequest               | GetLockStateResponse                   |
| GetTargetTemperatureRequest       | GetTargetTemperatureResponse           |
| HealthCheckRequest                | HealthCheckResponse                    |
| IncrementTargetTemperatureRequest | IncrementTargetTemperatureConfirmation |
| SetLockStateRequest               | SetLockStateConfirmation               |
| TurnOffRequest                    | TurnOffConfirmation                    |
| TurnOnRequest                     | TurnOnConfirmation                     |


When the request about controlling an appliance such as "Turn on the living room light" is forwarded to the IoT service and the IoT service responds that the request has been properly processed, you must return the result back to CEK using a *[TurnOnRequest](/CEK/References/Clova_Home_API.md)* message.

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

When a user asks for appliance state (*GetTargetTemperatureRequest*) by saying, for example, "Tell me the current target temperature", you must return state information to CEK using a *[GetTargetTemperatureResponse](#GetTargetTemperatureResponse)* message as follows.

{% raw %}
```json
{
  "header":{
    "messageId":"19b29d5e-04b3-4524-a538-35ae77ea2618",
    "name":"GetTargetTemperatureResponse",
    "namespace":"ClovaHome",
    "payloadVersion":"1.0"
  },
  "payload":{
    "targetTemperature": {
      "value": 24.0
    },
    "applianceResponseTimestamp":"2017-05-29T23:20:50.52Z"
  }
}
```
{% endraw %}

If there is a problem with connecting to a particular IoT appliance or if any internal error occurs, you must return an appropriate error message to CEK using the following APIs. Clova handles errors accordingly depending on the API it receives.

* [DriverInternalError](#DriverInternalError)
* [TargetOfflineError](#TargetOfflineError)

<div class="note">
<p><strong>Note!</strong></p>
<p>More error messages will be added going forward.</p>
</div>

This is an example of a *TargetOfflineError* message returned when there is a connection problem with an appliance.

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
<p>Use HTTP 200 OK even when you send an error response.</p>
</div>