# Shared objects {#SharedObjects}
The following shared objects are used in the message payload when sending the [Clova Home extension messages](/CEK/References/CEK_API.md#ClovaHomeExtMessage):

| Object name            | Description                                            |
|--------------------|---------------------------------------------------|
| [AirQualityInfoObject](#AirQualityInfoObject)         | The object containing information on air quality.            |
| [ApplianceInfoObject](#ApplianceInfoObject)           | The object containing information on an IoT appliance.        |
| [BatteryInfoObject](#BatteryInfoObject)               | The object containing information on battery.            |
| [BillInfoObject](#BillInfoObject)                     | The object containing information on billing.             |
| [BrightnessInfoObject](#BrightnessInfoObject)         | The object containing information on light or screen brightness. |
| [ColorInfoObject](#ColorInfoObject)                   | The object containing information on the color of lights, screes, or lamps of the target appliance.  |
| [ColorTemperatureInfoObject](#ColorTemperatureInfoObject) | The object containing information on the color temperature of lights, screen, or lamps of the target appliance.  |
| [ConsumptionInfoObject](#ConsumptionInfoObject)       | The object containing information on energy consumption.       |
| [CustomInfoObject](#CustomInfoObject)                 | The object containing information directly entered by the user, such as an arbitrary name, a required unit, or figures. |
| [ExpendableInfoObject](#ExpendableInfoObject)         | The object containing information on usage or remaining lifespan of appliance parts.  |
| [FineDustInfoObject](#FineDustInfoObject)             | The object containing information on fine dust.          |
| [IntensityLevelInfoObject](#IntensityLevelInfoObject) | The object containing information on pressure or water pressure intensity.   |
| [ModeInfoObject](#ModeInfoObject)                     | The object containing information on the operation mode.          |
| [HumidityInfoObject](#HumidityInfoObject)             | The object containing information on humidity.              |
| [PeriodInfoObject](#PeriodInfoObject)                 | The object containing information on the selected period. |
| [PhaseInfoObject](#PhaseInfoObject)                   | The object containing information on the phase of appliance actions.     |
| [ProgressiveTaxBracketInfoObject](#ProgressiveTaxBracketInfoObject)  | The object containing information on progressive tax brackets.  |
| [SpeedInfoObject](#SpeedInfoObject)                   | The object containing information on speed.              |
| [TemperatureInfoObject](#TemperatureInfoObject)       | The object containing information on temperature.          |
| [TimeAmountInfoObject](#TimeAmountInfoObject)         | The object containing information on amount of time, such as elapsed time or remaining time.  |
| [TVChannelNameInfoObject](#TVChannelNameInfoObject)   | The object containing information on a TV channel name.      |
| [TVChannelInfoObject](#TVChannelInfoObject)           | The object containing information on a TV channel.           |
| [UltraFineDustInfoObject](#UltraFineDustInfoObject)   | The object containing information on ultrafine dust.         |
| [VolumeInfoObject](#VolumeInfoObject)                 | The object containing information on volume.          |

## AirQualityInfoObject {#AirQualityInfoObject}
The object containing information on air quality. This is used to indicate the air quality measured by the appliance. It is expressed as a string.

### Object fields
| Field name       | Data type    | Description                     | Required/Included |
|---------------|---------|-----------------------------|:-------------:|
| `index`       | string  | Air quality level. It is limited to the following values.<ul><li><code>"good"</code>: Good</li><li><code>"normal"</code>: Normal</li><li><code>"bad"</code>: Bad</li><li><code>"verybad"</code>: Very bad</li></ul> | Required/Always     |

### Object Example
{% raw %}

```json
// Example: An example used in the GetAirQualityResponse message
{
  "header": {
    "messageId": "33da6561-0149-4532-a30b-e0de8f75c4cf",
    "name": "GetAirQualityResponse",
    "namespace": "ClovaHome",
    "payloadVersion": "1.0"
  },
  "payload": {
    "airQuality": {
        "index": "good"
    }
  }
}
```

{% endraw %}

### See also
* [`GetAirQualityRequest`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#GetAirQualityRequest)
* [`GetAirQualityResponse`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#GetAirQualityResponse)

## ApplianceInfoObject {#ApplianceInfoObject}
ApplianceInfoObject contains the information on IoT appliances. This is used to send a list of appliances registered in the user account to CEK or to request the Clova Home extension to control a specific appliance.

### Object fields
| Field name       | Data type    | Description                     | Required/Included |
|---------------|---------|-----------------------------|:-------------:|
| `actions[]`                  | string array  | List of actions supported by an appliance. The client must restrict the user to controlling the IoT device within the scope of actions supported by the appliance. | Optional/Always    |
| `additionalApplianceDetails` | object        | Additional information provided by the manufacturer or IoT service.                                 | Optional/Conditional    |
| `applianceId`                | string        | Device ID                                                                        | Required/Always    |
| `applianceTypes[]`           | string array  | The appliance type. The `applicationType` determines the value of the `actions` field, which is the action that can be performed an appliance. You must designate the type of appliance registered to the user account of the IoT service as one of the following values: Select the appliance type by referring to the items in the Remarks section.                                                                              | Required/Always    |
| `friendlyName`               | string        | The name of the appliance given by the user.                                                           | Optional/Always    |
| `friendlyDescription`        | string        | The description of the appliance.                                                                  | Optional/Always    |
| `isReachable`                | boolean       | Whether or not remote control is possible <ul><li>true: Remote control is available</li><li>false: Remote control is not available</li></ul> | Optional/Always    |
| `manufacturerName`           | string        | The name of the appliance manufacturer.                                                                  | Optional/Always    |
| `modelName`                  | string        | The name of the appliance model.                                                                   | Optional/Always    |
| `version`                    | string        | The software version of the manufacturer.                                                            | Optional/Always    |
| `location`                   | string        | The location of the appliance installation.                                                                | Optional/Always    |

## Remarks
If the user requests the appliance list using the [`DiscoverAppliancesRequest`](/CEK/References/ClovaHomeInterface/Discovery_Interfaces.md#DiscoverAppliancesRequest) message, the Clova Home extension must fill out all the fields except the `additionalApplianceDetails` field, and deliver the information. Here, the value of the `actions` field is normally determined by the `applianceTypes` field and may have the following values depending on the value of the `applianceTypes` field:

| applianceTypes | Description         | Permitted Actions                                  |
|----------------|-------------|-------------------------------------------------|
| `"AIRCONDITIONER"`  | Type of an air conditioner         | DecrementFanSpeed, DecrementTargetTemperature, GetCurrentTemperature, GetTargetTemperature, HealthCheck, IncrementFanSpeed, IncrementTargetTemperature, SetFanSpeed, SetMode, SetTargetTemperature, TurnOff, TurnOn               |
| `"AIRPURIFIER"`     | Type of an air purifier        | DecrementFanSpeed, GetAirQuality, GetFineDust, GetUltraFineDust, HealthCheck, IncrementFanSpeed, SetFanSpeed, TurnOff, TurnOn    |
| `"AIRSENSOR"`       | Type of an air sensor     | GetAirQuality, GetCurrentTemperature, GetFineDust, GetHumidity, GetUltraFineDust, HealthCheck                                     |
| `"BIDET"`           | Type of a bidet            | Close, GetDeviceState, GetExpendableState, HealthCheck, Open, TurnOff, TurnOn                                                         |
| `"BODYWEIGHTSCALE"` | Type of a weighing scale          | GetDeviceState, HealthCheck                                                                                                             |
| `"CLOTHESCAREMACHINE"` | Type of a clothing care machine    | GetRemainingTime, HealthCheck, TurnOff, TurnOn                                                                                     |
| `"CLOTHESDRYER"`    | Type of a drying machine       | GetDeviceState, HealthCheck, TurnOff, TurnOn                                                                                           |
| `"CLOTHESWASHER"`   | Type of a washing machine       | GetPhase, GetRemainingTime, HealthCheck, TurnOff, TurnOn                                                                           |
| `"DEHUMIDIFIER"`    | Type of a dehumidifier           | GetCurrentTemperature, GetHumidity, HealthCheck, SetFanSpeed, TurnOff, TurnOn                                                    |
| `"DISHWASHER"`      | Type of a dishwasher       | GetPhase, GetRemainingTime, HealthCheck, TurnOff, TurnOn                                                                           |
| `"ELECTRICKETTLE"`  | Type of an electric kettle       | GetCurrentTemperature, HealthCheck, TurnOff, TurnOn                                                                              |
| `"ELECTRICTOOTHBRUSH"` | Type of an electric toothbrush     | GetDeviceState, HealthCheck                                                                                                            |
| `"FAN"`             | Type of a fan           | HealthCheck, SetMode, TurnOff, TurnOn                                                                                            |
| `"HEATER"`          | Type of a heater            | DecrementTargetTemperature, GetCurrentTemperature, HealthCheck, IncrementTargetTemperature, TurnOff, TurnOn                      |
| `"HUMIDIFIER"`      | Type of a humidifier           | GetCurrentTemperature, GetHumidity, HealthCheck, SetFanSpeed, TurnOff, TurnOn                                                    |
| `"KIMCHIREFRIGERATOR"` | Type of a kimchi refrigerator    | GetDeviceState, HealthCheck                                                                                                            |
| `"LIGHT"`           | Type of a smart lighting   | DecrementBrightness, DecrementVolume HealthCheck, IncrementBrightness, IncrementVolume SetBrightness, TurnOff, TurnOn            |
| `"MASSAGECHAIR"`    | Type of a massage chair        | DecrementIntensityLevel, HealthCheck, IncrementIntensityLevel, TurnOff, TurnOn                                                     |
| `"MICROWAVE"`       | Type of a microwave      | GetRemainingTime, HealthCheck, TurnOff, TurnOn                                                                                      |
| `"MOTIONSENSOR"`    | Type of a motion detector    | GetDeviceState, HealthCheck                                                                                                             |
| `"OPENCLOSESENSOR"` | Type of an open/close detector    | GetCloseTime, GetLockState, GetOpenTime, HealthCheck                                                                                   |
| `"OVEN"`            | Type of an oven            | GetDeviceState, HealthCheck                                                                                                             |
| `"POWERSTRIP"`      | Type of a power strip         | GetConsumption, GetEstimateBill, GetProgressiveTaxBracket, HealthCheck, TurnOff, TurnOn                                                                     |
| `"PURIFIER"`        | Type of a purifier          | GetDeviceState, GetExpendableState, HealthCheck, SetMode, SetTargetTemperature                                                     |
| `"RANGE"`           | Type of an electric range          | GetDeviceState, HealthCheck                                                                                                             |
| `"RANGEHOOD"`       | Type of a range hood      | HealthCheck, TurnOff, TurnOn                                                                                                      |
| `"REFRIGERATOR"`    | Type of a refrigerator          | GetDeviceState, HealthCheck, SetFreezerTargetTemperature, SetFridgeTargetTemperature, SetMode                                           |
| `"RICECOOKER"`      | Type of a rice cooker        | GetExpendableState, GetKeepWarmTime, GetPhase, GetRemainingTime, HealthCheck, SetMode, Stop, TurnOff, TurnOn                |
| `"ROBOTVACUUM"`     | Type of a robot vacuum       | Charge, GetBatteryInfo, HealthCheck, TurnOff, TurnOn                                                                             |
| `"SETTOPBOX"`       | Type of a set-top box     | DecrementChannel, DecrementVolume, HealthCheck, IncrementChannel, IncrementVolume, Mute, SetChannel, SetChannelByName, TurnOff, TurnOn, Unmute |
| `"SLEEPINGMONITOR"` | Type of a sleep tracker        | GetDeviceState, HealthCheck, TurnOff, TurnOn                                                                                            |
| `"SMARTBED"`        | Type of a smart bed      | HealthCheck, Lower, Raise, Stop                                                                                                   |
| `"SMARTCHAIR"`      | Type of a smart chair      | GetRightPostureRatio, GetUsageTime, HealthCheck                                                                                       |
| `"SMARTCURTAIN"`    | Type of a smart curtain      | Close, HealthCheck, Open, Stop                                                                                                    |
| `"SMARTHUB"`        | Type of a smart hub      | GetCurrentTemperature, GetHumidity, GetTargetTemperature, HealthCheck, SetMode                                                    |
| `"SMARTMETER"`      | Type of a smart meter      | GetConsumption, GetCurrentBill, GetEstimateBill, GetProgressiveTaxBracket, HealthCheck                                            |
| `"SMARTPLUG"`       | Type of a smart plug     | GetProgressiveTaxBracket, HealthCheck, TurnOff, TurnOn                                                                                                     |
| `"SMARTTV"`         | Type of a smart TV       | DecrementChannel, DecrementVolume, HealthCheck, IncrementChannel, IncrementVolume, Mute, SetChannel, SetChannelByName, TurnOff, TurnOn, Unmute |
| `"SMARTVALVE"`      | Type of a smart valve      | GetLockState, SetLockState                                                                                                        |
| `"SMOKESENSOR"`     | Type of a smoke sensor       | GetDeviceState, HealthCheck                                                                                                             |
| `"SWITCH"`          | Type of a switch to control outlets in homes | HealthCheck, TurnOff, TurnOn                                                                                       |
| `"THERMOSTAT"`      | Type of a thermostat   | DecrementTargetTemperature, GetCurrentTemperature, HealthCheck, IncrementTargetTemperature, SetMode, SetTargetTemperature TurnOff, TurnOn       |
| `"VENTILATOR"`      | Type of a ventilator          | GetDeviceState, HealthCheck, TurnOff, TurnOn                                                                                            |
| `"WATERBOILER"`     | Type of a water boiler          | HealthCheck, SetMode, TurnOff, TurnOn                                                                                             |

<div class="note">
<p><strong>Note!</strong></p>
<p>You can restrict actions to allow fewer actions than are permitted by the applianceTypes depending on the functional limitations of the actual appliance. For example, if there is no function to adjust the fan speed on the air purifier (<code>AIRPURIFIER</code> type), DiscoverAppliancesResponse message must be sent to exclude the IncrementFanSpeed and DecrementFanSpeed fields from the permitted actions. Note that if the user requests an unsupported action, CEK informs the user immediately that the request is not within the permitted range.</p>
</div>

The table below lists the [interfaces](/CEK/References/CEK_API.md#ClovaHomeExtInterface) related to each action:

| Action                    | Related interface                            |
|----------------------------|------------------------------------------|
| Charge                     | [`ChargeConfirmation`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#ChargeConfirmation), [`ChargeRequest`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#ChargeRequest) |
| Close                      | [`CloseConfirmation`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#CloseConfirmation), [`CloseRequest`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#CloseRequest)  |
| DecrementBrightness        | [`DecrementBrightnessConfirmation`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#DecrementBrightnessConfirmation), [`DecrementBrightnessRequest`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#DecrementBrightnessRequest) |
| DecrementChannel           | [`DecrementChannelConfirmation`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#DecrementChannelConfirmation), [`DecrementChannelRequest`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#DecrementChannelRequest) |
| DecrementFanSpeed          | [`DecrementFanSpeedConfirmation`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#DecrementFanSpeedConfirmation), [`DecrementFanSpeedRequest`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#DecrementFanSpeedRequest) |
| DecrementIntensityLevel    | [`DecrementIntensityLevelConfirmation`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#DecrementIntensityLevelConfirmation), [`DecrementIntensityLevelRequest`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#DecrementIntensityLevelRequest)  |
| DecrementTargetTemperature | [`DecrementTargetTemperatureConfirmation`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#DecrementTargetTemperatureConfirmation), [`DecrementTargetTemperatureRequest`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#DecrementTargetTemperatureRequest) |
| DecrementVolume            | [`DecrementVolumeConfirmation`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#DecrementVolumeConfirmation), [`DecrementVolumeRequest`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#DecrementVolumeRequest) |
| GetAirQuality              | [`GetAirQualityRequest`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#GetAirQualityRequest), [`GetAirQualityResponse`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#GetAirQualityResponse) |
| GetBatteryInfo              | [`GetBatteryInfoRequest`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#GetBatteryInfoRequest), [`GetBatteryInfoResponse`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#GetBatteryInfoResponse) |
| GetCloseTime                | [`GetCloseTimeRequest`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#GetCloseTimeRequest), [`GetCloseTimeResponse`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#GetCloseTimeResponse)  |
| GetConsumption              | [`GetConsumptionRequest`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#GetConsumptionRequest), [`GetConsumptionResponse`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#GetConsumptionResponse)  |
| GetCurrentBill              | [`GetCurrentBillRequest`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#GetCurrentBillRequest), [`GetCurrentBillResponse`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#GetCurrentBillResponse)  |
| GetCurrentTemperature       | [`GetCurrentTemperatureRequest`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#GetCurrentTemperatureRequest), [`GetCurrentTemperatureResponse`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#GetCurrentTemperatureResponse) |
| GetDeviceState             | [`GetDeviceStateRequest`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#GetDeviceStateRequest), [`GetDeviceStateResponse`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#GetDeviceStateResponse)  |
| GetEstimateBill            | [`GetEstimateBillRequest`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#GetEstimateBillRequest), [`GetEstimateBillResponse`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#GetEstimateBillResponse)  |
| GetExpendableState         | [`GetExpendableStateRequest`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#GetExpendableStateRequest), [`GetExpendableStateResponse`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#GetExpendableStateResponse)  |
| GetFineDust                | [`GetFineDustRequest`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#GetFineDustRequest), [`GetFineDustResponse`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#GetFineDustResponse) |
| GetHumidity                | [`GetHumidityRequest`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#GetHumidityRequest), [`GetHumidityResponse`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#GetHumidityResponse) |
| GetKeepWarmTime            | [`GetKeepWarmTimeRequest`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#GetKeepWarmTimeRequest), [`GetKeepWarmTimeResponse`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#GetKeepWarmTimeResponse) |
| GetLockState               | [`GetLockStateRequest`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#GetLockStateRequest), [`GetLockStateResponse`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#GetLockStateResponse) |
| GetOpenTime                | [`GetOpenTimeRequest`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#GetOpenTimeRequest), [`GetOpenTimeResponse`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#GetOpenTimeResponse)  |
| GetPhase                   | [`GetPhaseRequest`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#GetPhaseRequest), [`GetPhaseResponse`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#GetPhaseResponse)  |
| GetProgressiveTaxBracket   | [`GetProgressiveTaxBracketRequest`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#GetProgressiveTaxBracketRequest), [`GetProgressiveTaxBracketResponse`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#GetProgressiveTaxBracketResponse) |
| GetRemainingTime           | [`GetRemainingTimeRequest`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#GetRemainingTimeRequest), [`GetRemainingTimeResponse`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#GetRemainingTimeResponse)  |
| GetRightPostureRatio       | [`GetRightPostureRatioRequest`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#GetRightPostureRatioRequest), [`GetRightPostureRatioResponse`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#GetRightPostureRatioResponse)  |
| GetTargetTemperature       | [`GetTargetTemperatureRequest`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#GetTargetTemperatureRequest), [`GetTargetTemperatureResponse`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#GetTargetTemperatureResponse) |
| GetUltraFineDust           | [`GetUltraFineDustRequest`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#GetUltraFineDustRequest), [`GetUltraFineDustResponse`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#GetUltraFineDustResponse) |
| GetUsageTime               | [`GetUsageTimeRequest`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#GetUsageTimeRequest), [`GetUsageTimeResponse`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#GetUsageTimeResponse)  |
| HealthCheck                | [`HealthCheckRequest`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#HealthCheckRequest), [`HealthCheckResponse`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#HealthCheckResponse) |
| IncrementBrightness        | [`IncrementBrightnessConfirmation`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#IncrementBrightnessConfirmation), [`IncrementBrightnessRequest`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#IncrementBrightnessRequest)  |
| IncrementChannel           | [`IncrementChannelConfirmation`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#IncrementChannelConfirmation), [`IncrementChannelRequest`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#IncrementChannelRequest) |
| IncrementFanSpeed          | [`IncrementFanSpeedConfirmation`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#IncrementFanSpeedConfirmation), [`IncrementFanSpeedRequest`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#IncrementFanSpeedRequest) |
| IncrementIntensityLevel    | [`IncrementIntensityLevelConfirmation`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#IncrementIntensityLevelConfirmation), [`IncrementIntensityLevelRequest`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#IncrementIntensityLevelConfirmation)  |
| IncrementTargetTemperature | [`IncrementTargetTemperatureConfirmation`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#IncrementTargetTemperatureConfirmation), [`IncrementTargetTemperatureRequest`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#IncrementTargetTemperatureConfirmation) |
| IncrementVolume            | [`IncrementVolumeConfirmation`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#IncrementVolumeConfirmation), [`IncrementVolumeRequest`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#IncrementVolumeRequest) |
| Lower                      | [`LowerConfirmation`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#LowerConfirmation), [`LowerRequest`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#LowerRequest)  |
| Mute                       | [`MuteConfirmation`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#MuteConfirmation), [`MuteRequest`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#MuteRequest) |
| Open                       | [`OpenConfirmation`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#OpenConfirmation), [`OpenRequest`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#OpenRequest)  |
| Raise                      | [`RaiseConfirmation`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#RaiseConfirmation), [`RaiseRequest`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#RaiseRequest)  |
| SetBrightness              | [`SetBrightnessConfirmation`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#SetBrightnessConfirmation), [`SetBrightnessRequest`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#SetBrightnessRequest)  |
| SetChannel                 | [`SetChannelConfirmation`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#SetChannelConfirmation), [`SetChannelRequest`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#SetChannelRequest) |
| SetChannelByName           | [`SetChannelByNameConfirmation`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#SetChannelByNameConfirmation), [`SetChannelByNameRequest`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#SetChannelByNameRequest) |
| SetColor                   | [`SetColorConfirmation`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#SetColorConfirmation), [`SetColorRequest`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#SetColorRequest)  |
| SetColorTemperature        | [`SetColorTemperatureConfirmation`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#SetColorTemperatureConfirmation), [`SetColorTemperatureRequest`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#SetColorTemperatureRequest)  |
| SetFanSpeed                | [`SetFanSpeedConfirmation`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#SetFanSpeedConfirmation), [`SetFanSpeedRequest`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#SetFanSpeedRequest)  |
| SetFreezerTargetTemperature | [`SetFreezerTargetTemperatureConfirmation`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#SetFreezerTargetTemperatureConfirmation), [`SetFreezerTargetTemperatureRequest`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#SetFreezerTargetTemperatureRequest)  |
| SetFridgeTargetTemperature | [`SetFridgeTargetTemperatureConfirmation`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#SetFridgeTargetTemperatureConfirmation), [`SetFridgeTargetTemperatureRequest`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#SetFridgeTargetTemperatureRequest)  |
| SetLockState               | [`SetLockStateConfirmation`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#SetLockStateConfirmation), [`SetLockStateRequest`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#SetLockStateRequest)  |
| SetMode                    | [`SetModeConfirmation`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#SetModeConfirmation), [`SetModeRequest`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#SetModeRequest) |
| SetTargetTemperature       | [`SetTargetTemperatureConfirmation`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#SetTargetTemperatureConfirmation), [`SetTargetTemperatureRequest`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#SetTargetTemperatureConfirmation)  |
| Stop                       | [`StopConfirmation`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#StopConfirmation), [`StopRequest`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#StopRequest)  |
| TurnOff                    | [`TurnOffConfirmation`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#TurnOffConfirmation), [`TurnOffRequest`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#TurnOffRequest) |
| TurnOn                     | [`TurnOnConfirmation`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#TurnOnConfirmation), [`TurnOnRequest`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#TurnOnRequest) |
| Unmute                     | [`UnmuteConfirmation`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#UnmuteConfirmation), [`UnmuteRequest`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#UnmuteRequest) |

<div class="note">
<p><strong>Note!</strong></p>
<p>You can automatically set the location of the user’s IoT appliances by using the `location` field for each appliance in the <a href="/CEK/References/ClovaHomeInterface/Discovery_Interfaces.html#DiscoverAppliancesResponse"><code>DiscoveryAppAppliancesResponse</code></a> message when sending the list of user registered appliance to CEK.</p>
</div>

The table below shows the location information supported by `location` field. This information is used for analyzing the user utterance or showing the location of the appliance to the user.

{% include "/CEK/References/ClovaHomeInterface/Location.md" %}

### Object Example
{% raw %}

```json
// Example 1: An example used in DiscoverAppliancesResponse message
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
            "HealthCheckt",
            "TurnOn",
            "TurnOff"
        ],
        "applianceTypes": ["LIGHT"],
        "additionalApplianceDetails": {},
        "location": "LIVING_ROOM"
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
          "HealthCheckt",
          "TurnOn",
          "TurnOff"
        ],
        "applianceTypes": ["SMARTPLUG"],
        "additionalApplianceDetails": {},
        "location": ""
      }
    ]
  }
}

// Example 2: An example used in the TurnOnRequest message
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

### See also
* [`DiscoverAppliancesResponse`](/CEK/References/ClovaHomeInterface/Discovery_Interfaces.md#DiscoverAppliancesResponse)
* [`DiscoverAppliancesRequest`](/CEK/References/ClovaHomeInterface/Discovery_Interfaces.md#DiscoverAppliancesRequest)

## BatteryInfoObject {#BatteryInfoObject}
BatteryInfoObject contains information on the appliance battery. This is used to indicate battery information and expressed as an integer (0-100) that represents a percentage.

### Object fields
| Field name       | Data type    | Description                     | Required/Included |
|---------------|---------|-----------------------------|:-------------:|
| `value`       | number  | Remaining battery (%)                 | Required/Always     |

### Object Example
{% raw %}

```json
// Example 1: An example used in the GetBatteryInfoRequest message
{
  "header": {
    "messageId": "6c04fc2d-64dd-41a0-9162-7cb0d4cf7c08",
    "name": "GetBatteryInfoRequest",
    "namespace": "ClovaHome",
    "payloadVersion": "1.0"
  },
  "payload": {
    "accessToken": "92ebcb67fe33",
    "appliance": {
      "applianceId": "device-010"
    }
  }
}

// Example 2: An example used in the GetBatteryInfoResponse message
{
  "header": {
    "messageId": "4ec35000-88ce-4724-b7e4-7f52050558fd",
    "name": "GetBatteryInfoResponse",
    "namespace": "ClovaHome",
    "payloadVersion": "1.0"
  },
  "payload": {
    "batteryInfo": {
      "value": 40
    }
  }
}
```

{% endraw %}

### See also
* [`GetBatteryInfoRequest`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#GetBatteryInfoRequest)
* [`GetBatteryInfoResponse`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#GetBatteryInfoResponse)

## BillInfoObject {#BillInfoObject}
BillInfoObject contains the information on billing derived from the amount of energy consumption measured by the appliance. The billing information is displayed in two components: amount and currency unit.

### Object fields
| Field name       | Data type    | Description                     | Required/Included |
|---------------|---------|-----------------------------|:-------------:|
| `currency`    | string  | Currency unit (<a href="https://en.wikipedia.org/wiki/ISO_4217" target="_blank">ISO 4217</a>)  | Required/Always |
| `value`       | number  | Amount of bill                    | Required/Always   |

### Object Example
{% raw %}

```json
// Example: An example used in the GetCurrentBillResponse message
{
  "header": {
    "messageId": "33da6561-0149-4532-a30b-e0de8f75c4cf",
    "name": "GetCurrentBillResponse",
    "namespace": "ClovaHome",
    "payloadVersion": "1.0"
  },
  "payload": {
    "currentBill": {
        "value": 29900,
        "currency": "KRW"
    },
    "applianceResponseTimestamp": "2017-11-23T20:30:54+09:00"
  }
}
```

{% endraw %}

### See also
* [`GetCurrentBillRequest`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#GetCurrentBillRequest)
* [`GetCurrentBillResponse`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#GetCurrentBillResponse)
* [`GetEstimateBillRequest`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#GetEstimateBillRequest)
* [`GetEstimateBillResponse`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#GetEstimateBillResponse)

## BrightnessInfoObject {#BrightnessInfoObject}
BrightnessInfoObject contains information on light or screen brightness. This is used to indicate the light or screen brightness to change, or the brightness before and after the change. It is expressed as an integer (0-100) that represents a percentage.

### Object fields
| Field name       | Data type    | Description                     | Required/Included |
|---------------|---------|-----------------------------|:-------------:|
| `value`       | number  | Brightness (%)                      | Required/Always     |

### Object Example
{% raw %}

```json
// Example 1: An example used in the IncrementBrightnessRequest message
{
  "header": {
    "messageId": "6c04fc2d-64dd-41a0-9162-7cb0d4cf7c08",
    "name": "IncrementBrightnessRequest",
    "namespace": "ClovaHome",
    "payloadVersion": "1.0"
  },
  "payload": {
    "accessToken": "92ebcb67fe33",
    "appliance": {
      "applianceId": "device-010"
    },
    "deltaBrightness": {
      "value": 40
    }
  }
}

// Example 2: An example used in the IncrementBrightnessConfirmation message
{
  "header": {
    "messageId": "4ec35000-88ce-4724-b7e4-7f52050558fd",
    "name": "DecrementBrightnessConfirmation",
    "namespace": "ClovaHome",
    "payloadVersion": "1.0"
  },
  "payload": {
    "targetBrightness": {
      "value": 40
    },
    "previousState": {
      "targetBrightness": {
        "value": 20
      }
    }
  }
}
```

{% endraw %}

### See also
* [`DecrementBrightnessConfirmation`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#DecrementBrightnessConfirmation)
* [`DecrementBrightnessRequest`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#DecrementBrightnessRequest)
* [`IncrementBrightnessConfirmation`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#IncrementBrightnessConfirmation)
* [`IncrementBrightnessRequest`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#IncrementBrightnessRequest)
* [`SetBrightnessConfirmation`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#SetBrightnessConfirmation)
* [`SetBrightnessRequest`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#SetBrightnessRequest)

## ColorInfoObject {#ColorInfoObject}
ColorInfoObject contains information on the color of lights, the screen, or lamps of the target appliance. This is used to indicate the light or screen color to change, or the color before and after the change. The color information is expressed in the (<a href="https://en.wikipedia.org/wiki/HSL_and_HSV" target="_blank">HSV</a>) model.

### Object fields
| Field name       | Data type    | Description                     | Required/Included |
|---------------|---------|-----------------------------|:-------------:|
| `brightness`  | number  | Value (0-100)                  | Required/Always |
| `hue`         | number  | Hue (0-360)                  | Required/Always |
| `saturation`  | number  | Saturation (0-100)                  | Required/Always |

### Object Example
{% raw %}

```json
// Example: An example used in the SetColorRequest message
{
  "header": {
    "messageId": "a97dff79-5684-4535-8df3-193713c478aa",
    "name": "SetColorRequest",
    "namespace": "ClovaHome",
    "payloadVersion": "1.0"
  },
  "payload": {
    "accessToken": "92ebcb67fe33",
    "appliance": {
      "applianceId": "device-020"
    },
    "color": {
  		"hue": 100,
      "saturation": 100,
      "brightness": 100
  	}
  }
}
```

{% endraw %}

### See also
* [`SetColorConfirmation`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#SetColorConfirmation)
* [`SetColorRequest`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#SetColorRequest)

## ColorTemperatureInfoObject {#ColorTemperatureInfoObject}
ColorTemperatureInfoObject contains information on the color temperature of lights, the screen, or lamps of the target appliance. This is used to indicate the light or screen color temperature to change, or the color temperature before and after the change. It is expressed using the Kelvin (K) scale.

### Object fields
| Field name       | Data type    | Description                     | Required/Included |
|---------------|---------|-----------------------------|:-------------:|
| `value`       | number  | Color temperature (K, Kelvin)             | Required/Always     |

### Object Example
{% raw %}

```json
// Example: An example used in the SetColorTemperatureRequest message
{
  "header": {
    "messageId": "a97dff79-5684-4535-8df3-193713c478aa",
    "name": "SetColorTemperatureRequest",
    "namespace": "ClovaHome",
    "payloadVersion": "1.0"
  },
  "payload": {
    "accessToken": "92ebcb67fe33",
    "appliance": {
      "applianceId": "device-020"
    },
    "colorTemperature": {
      "value": 3600
    }
  }
}
```

{% endraw %}

### See also
* [`SetColorTemperatureConfirmation`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#SetColorTemperatureConfirmation)
* [`SetColorTemperatureRequest`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#SetColorTemperatureRequest)

## ConsumptionInfoObject {#ConsumptionInfoObject}
ConsumptionInfoObject contains information on energy consumption measured by the appliance. The consumption information is displayed in two components: energy consumption amount and unit.

### Object fields
| Field name       | Data type    | Description                     | Required/Included |
|---------------|---------|-----------------------------|:-------------:|
| `unit`        | string  | Energy unit (E.g. electricity: kW)            | Required/Always  |
| `value`       | number  | Energy consumption amount                    | Required/Always   |

### Object Example
{% raw %}

```json
// Example: An example used in the GetCurrentBillResponse message
{
  "header": {
    "messageId": "33da6561-0149-4532-a30b-e0de8f75c4cf",
    "name": "GetCurrentBillResponse",
    "namespace": "ClovaHome",
    "payloadVersion": "1.0"
  },
  "payload": {
    "consumption": {
        "value": 79.7,
        "unit": "kW"
    },
    "applianceResponseTimestamp": "2017-11-23T20:30:54+09:00"
  }
}
```

{% endraw %}

### See also
* [`GetCurrentBillRequest`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#GetCurrentBillRequest)
* [`GetCurrentBillResponse`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#GetCurrentBillResponse)
* [`GetEstimateBillRequest`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#GetEstimateBillRequest)
* [`GetEstimateBillResponse`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#GetEstimateBillResponse)

## CustomInfoObject {#CustomInfoObject}

CustomInfoObject contains information directly entered by the user, such as as arbitrary name, required unit, or figures. This object is used when the [shared objects](#SharedObjects) provided by default cannot express the object information or when providing all information of the appliance using the [`GetDeviceStateResponse`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#GetDeviceStateResponse) message.

### Object fields
| Field name       | Data type    | Description                     | Required/Included |
|---------------|---------|-----------------------------|:-------------:|
| `name`        | string            | The arbitrary name to indicate an appliance state or measurement target. When responding to the user, the state name entered in this field is output as speech. | Required/Always |
| `value`       | number or string | The state value or measurement value.                                                                             | Required/Always |
| `unit`        | string            | The value of the appliance state or the unit information of the measurement. This is omitted if the data type of the `value` field is a string and may have the following units if it is a numeric value.<ul><li><code>"celcius"</code>: Celsius</li><li><code>"percentage"</code>: Percentage</li></ul> | Optional/Conditional |

### Object Example
{% raw %}

```json
// Example: An example used in GetDeviceStateResponse message
{
  "header": {
    "messageId": "33da6561-0149-4532-a30b-e0de8f75c4cf",
    "name": "GetDeviceStateResponse",
    "namespace": "ClovaHome",
    "payloadVersion": "1.0"
  },
  "payload": {
    "states" : [
      {
        "name" : "Temperature of the freezer",
        "value" : -11,
        "unit" : "celsius"
      },
      {
        "name" : "Temperature of the fridge",
        "value" : 2,
        "unit" : "celsius"
      },
      {
        "name" : "Humidity of the fridge",
        "value" : 10,
        "unit" : "percentage"
      },
    ],
    "applianceResponseTimestamp": "2017-11-23T20:31:18+09:00"
  }
}
```

{% endraw %}

### See also
* [`GetDeviceStateRequest`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#GetDeviceStateRequest)
* [`GetDeviceStateResponse`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#GetDeviceStateResponse)

## ExpendableInfoObject {#ExpendableInfoObject}
ExpendableInfoObject contains information on usage or remaining lifespan of device parts. This is used to indicate the usage amount of the appliance parts or their remaining lifespans.

### Object fields
| Field name       | Data type    | Description                     | Required/Included |
|---------------|---------|-----------------------------|:-------------:|
| `name`          | string  | The name of the part.                  | Required/Always |
| `remainingTime` | [TimeAmountInfoObject](#TimeAmountInfoObject)  | The remaining lifespan of the part.    | Optional/Conditional |
| `usage`         | [CustomInfoObject](#CustomInfoObject)          | The usage amount of the part (can be expressed as the number of uses or percentage of usage).      | Optional/Conditional |

### Object Example
{% raw %}

```json
// Example: An example used in the GetExpendableStateResponse message
{
  "header": {
    "messageId": "33da6561-0149-4532-a30b-e0de8f75c4cf",
    "name": "GetExpendableStateResponse",
    "namespace": "ClovaHome",
    "payloadVersion": "1.0"
  },
  "payload": {
    "expendableInfo" : [
      {
        "name": "Packing,"
        "remainingTime" : {
          "month": 1,
          "day": 3
        }
      },
      {
        "name": "Filter 1,"
        "usage": {
          "value" : 80,
          "unit" : "percentage"
        }
      }
    ],
    "applianceResponseTimestamp": "2017-11-23T20:31:18+09:00"
  }
}
```

{% endraw %}

### See also
* [`GetExpendableStateRequest`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#GetExpendableStateRequest)
* [`GetExpendableStateResponse`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#GetExpendableStateResponse)

## FineDustInfoObject {#FineDustInfoObject}
FineDustInfoObject contains information on fine dust. This is used to indicate the fine dust index or level measured by the appliance. It is expressed as a number.

### Object fields
| Field name       | Data type    | Description                     | Required/Included |
|---------------|---------|-----------------------------|:-------------:|
| `value`       | number  | Fine dust index.                  | Optional/Conditional    |
| `index`       | string  | Fine dust level. It is limited to the following values.<ul><li><code>"good"</code>: Good</li><li><code>"normal"</code>: Normal</li><li><code>"bad"</code>: Bad</li><li><code>"verybad"</code>: Very bad</li></ul> | Required/Always     |

### Object Example
{% raw %}

```json
// Example: An example used in the GetFineDustResponse message
{
  "header": {
    "messageId": "33da6561-0149-4532-a30b-e0de8f75c4cf",
    "name": "GetFineDustResponse",
    "namespace": "ClovaHome",
    "payloadVersion": "1.0"
  },
  "payload": {
    "fineDust": {
        "value": 77,
        "index": "normal"
    }
  }
}
```

{% endraw %}

### See also
* [`GetFineDustRequest`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#GetFineDustRequest)
* [`GetFineDustResponse`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#GetFineDustResponse)

## IntensityLevelInfoObject {#IntensityLevelInfoObject}
IntensityLevelInfoObject contains information on pressure or water pressure intensity. This is displayed according to the pressure or water pressure intensities in each appliance.

### Object fields
| Field name       | Data type    | Description                     | Required/Included |
|---------------|---------|-----------------------------|:-------------:|
| `value`       | number  | Intensity of pressure or water pressure.            | Optional/Conditional    |

### Object Example
{% raw %}

```json
// Example: An example used in the IncrementIntensityLevelConfirmation message
{
  "header": {
    "messageId": "be3dde71-84c0-48cf-80d8-440c1ede54d8",
    "name": "IncrementIntensityLevelConfirmation",
    "namespace": "ClovaHome",
    "payloadVersion": "1.0"
  },
  "payload": {
    "intensityLevel": {
      "value": 1
    },
    "previousState": {
      "intensityLevel": {
        "value": 2
      }
    }
  }
}
```

{% endraw %}

### See also

* [`DecrementIntensityLevelConfirmation`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#DecrementIntensityLevelConfirmation)
* [`DecrementIntensityLevelRequest`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#DecrementIntensityLevelRequest)
* [`IncrementIntensityLevelConfirmation`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#IncrementIntensityLevelConfirmation)
* [`IncrementIntensityLevelRequest`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#IncrementIntensityLevelRequest)

## ModeInfoObject {#ModeInfoObject}
ModeInfoObject contains information on the operation mode. This is used to indicate the name of the operation mode to change or the operation mode before and after the change. It is expressed as a string.

### Object fields
| Field name       | Data type    | Description                     | Required/Included |
|---------------|---------|-----------------------------|:-------------:|
| `value`       | string  | [Operation mode](#OperationModes)    | Required/Always     |

### Operation modes {#OperationModes}

<table>
  <thead>
    <tr>
      <th style="width:20%">Appliance type</th><th style="width:80%">Operation mode list and description</th>
    </tr>
  </thead>
  <tdoby>
    <tr>
      <td><code>"AIRCONDITIONER"</code></td>
      <td>
        <ul>
          <li><code>"cool"</code>: Cool mode. A mode mainly used in air conditioners.</li>
          <li><code>"dehumidify"</code>: Dehumidifier mode. A mode mainly used in appliances such as air conditioners or dehumidifiers.</li>
          <li><code>"sleep"</code>: Sleep mode. A mode mainly used in appliances such as smart hubs.</li>
        </ul>
      </td>
    </tr>
    <tr>
      <td><code>"FAN"</code></td>
      <td>
        <ul>
          <li><code>"auto"</code>: Auto mode</li>
          <li><code>"baby"</code>: Baby mode</li>
          <li><code>"sleep"</code>: Sleep mode</li>
      </td>
    </tr>
    <tr>
      <td><code>"LIGHT"</code></td>
      <td>
        <ul>
          <li><code>"concentration"</code>: Concentrating mode</li>
          <li><code>"reading"</code>: Reading mode</li>
          <li><code>"rest"</code>: Resting mode</li>
          <li><code>"sleep"</code>: Sleep mode</li>
          <li><code>"vitality"</code>: Vitality mode</li>
          <li><code>"wakeup"</code>: Wake up mode</li>
        </ul>
      </td>
    </tr>
    <tr>
      <td><code>"PURIFIER"</code></td>
      <td>
        <ul>
          <li><code>"coldwater"</code>: Cold water mode</li>
          <li><code>"general"</code>: General mode</li>
          <li><code>"hotwater"</code>: Hot water mode</li>
          <li><code>"smartchecking"</code>: Smart inspection mode</li>
        </ul>
      </td>
    </tr>
    <tr>
      <td><code>"REFRIGERATOR"</code></td>
      <td>
        <ul>
          <li><code>"filter"</code>: Filter mode</li>
          <li><code>"freeze"</code>: Express freeze mode</li>
          <li><code>"powersaving"</code>: Power saving mode</li>
        </ul>
      </td>
    </tr>
    <tr>
      <td><code>"RICECOOKER"</code></td>
      <td>
        <ul>
          <li><code>"general"</code>: General mode</li>
          <li><code>"keepwarm"</code>: Warm mode</li>
          <li><code>"powersaving"</code>: Power saving mode</li>
          <li><code>"reheating"</code>: Reheating mode</li>
        </ul>
      </td>
    </tr>
    <tr>
      <td><code>"SMARTHUB"</code></td>
      <td>
        <ul>
          <li><code>"away"</code>: Away mode</li>
          <li><code>"hotwater"</code>: Hot water mode</li>
          <li><code>"indoor"</code>: Indoor mode</li>
          <li><code>"sleep"</code>: Sleep mode</li>
        </ul>
      </td>
    </tr>
    <tr>
      <td><code>"THERMOSTAT"</code></td>
      <td>
        <ul>
          <li><code>"away"</code>: Away mode</li>
          <li><code>"hotwater"</code>: Hot water mode</li>
          <li><code>"indoor"</code>: Indoor mode</li>
          <li><code>"sleep"</code>: Sleep mode</li>
        </ul>
      </td>
    </tr>
    <tr>
      <td><code>"WATERBOILER"</code></td>
      <td>
        <ul>
          <li><code>"hotwater"</code>: Hot water supply mode</li>
          <li><code>"reheating"</code>: Reheating mode</li>
        </ul>
      </td>
    </tr>
  </tdoby>
</table>

### Object Example
{% raw %}

```json
// Example 1: An example used in the SetModeRequest message for a thermostat
{
  "header": {
    "messageId": "33da6561-0149-4532-a30b-e0de8f75c4cf",
    "name": "SetModeRequest",
    "namespace": "ClovaHome",
    "payloadVersion": "1.0"
  },
  "payload": {
    "accessToken": "92ebcb67fe33",
    "appliance": {
        "applianceId": "device-006"
    },
    "mode": {
        "value": "hotwater"
    }
  }
}

// Example 2: An example used in the SetModeRequest message - smart hub
{
  "header": {
    "messageId": "b4151a0d-1ec5-4ed0-a39a-1538c356b93b",
    "name": "SetModeRequest",
    "namespace": "ClovaHome",
    "payloadVersion": "1.0"
  },
  "payload": {
    "accessToken": "92ebcb67fe33",
    "appliance": {
        "applianceId": "device-011"
    },
    "mode": {
        "value": "indoor"
    }
  }
}

// Example 3: An example used in the SetModeConfirmation message
{
  "header": {
    "messageId": "b7434bd2-c397-461d-b08d-a4a427455c8f",
    "name": "SetModeConfirmation",
    "namespace": "ClovaHome",
    "payloadVersion": "1.0"
  },
  "payload": {
    "mode": {
      "value": "sleep"
    }
  }
}
```

{% endraw %}

### See also
* [`SetModeConfirmation`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#SetModeConfirmation)
* [`SetModeRequest`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#SetModeRequest)

## HumidityInfoObject {#HumidityInfoObject}
HumidityInfoObject contains information on humidity. This is used to indicate the humidity condition measured by the appliance. It is expressed as a string.

### Object fields
| Field name       | Data type    | Description                     | Required/Included |
|---------------|---------|-----------------------------|:-------------:|
| `value`       | number  | Humidity (%)                      | Required/Always     |

### Object Example
{% raw %}

```json
// Example: An example used in the GetHumidityResponse message
{
  "header": {
    "messageId": "33da6561-0149-4532-a30b-e0de8f75c4cf",
    "name": "GetHumidityResponse",
    "namespace": "ClovaHome",
    "payloadVersion": "1.0"
  },
  "payload": {
    "fineDust": {
        "value": 40
    }
  }
}
```

{% endraw %}

### See also
* [`GetHumidityRequest`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#GetHumidityRequest)
* [`GetHumidityResponse`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#GetHumidityResponse)

## PeriodInfoObject {#PeriodInfoObject}

PeriodInfoObject contains information on periods used for measurements when calculating the amount of consumption or estimating bills.

### Object fields

| Field name       | Data type    | Description                     | Required/Included |
|---------------|---------|-----------------------------|:-------------:|
| `value`       | string  | The information on the period.<ul><li><code>"today"</code>: The period from 00:00am today to the current time.</li><li><code>"yesterday"</code>: The period of the previous day.</li><li><code>"thisWeek"</code>: The period from 00:00am Sunday this week to the current time.</li><li><code>"lastWeek"</code>: The period of the previous week.</li><li><code>"thisMonth"</code>: The period from 00:00am on the first day of this month to the current time.</li><li><code>"lastMonth"</code>: The period of the previous month.</li></ul>        | Required/Always      |

### Object Example
{% raw %}

```json
// Example: An example used in the GetUsageTimeRequest message
{
  "header": {
    "messageId": "59a3f5bc-4c38-4d4c-9b71-3a037bf9f9b0",
    "name": "GetUsageTimeRequest",
    "namespace": "ClovaHome",
    "payloadVersion": "1.0"
  },
  "payload": {
    "accessToken": "92ebcb67fe33",
    "appliance": {
      "applianceId": "device-028"
    },
    "period": {
      "value": "today"
    }
  }
}
```

{% endraw %}

### See also
* [`GetUsageTimeRequest`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#GetUsageTimeRequest)

## PhaseInfoObject {#PhaseInfoObject}

PhaseInfoObject contains information on the phase of device actions. This is used to indicate the current phase of the action or the previous phase of the action.

### Object fields

| Field name       | Data type    | Description                     | Required/Included |
|---------------|---------|-----------------------------|:-------------:|
| `value`       | string  | The string to express the phase of action.        | Required/Always      |

### Object Example
{% raw %}

```json
// Example 1: An example used in the GetPhaseResponse message
{
  "header": {
    "messageId": "b502dd42-b698-4d3b-9ddb-bbdda70f254f",
    "name": "GetPhaseResponse",
    "namespace": "ClovaHome",
    "payloadVersion": "1.0"
  },
  "payload": {
    "phase": {
        "value": "Spin-dry,"
    },
    "applianceResponseTimestamp": "2017-11-23T20:30:19+09:00"
  }
}

// Example 2: An example used in the StopConfirmation message
{
  "header": {
    "messageId": "a4349fd5-7c1c-4fae-9bbd-291749bdd63a",
    "name": "StopConfirmation",
    "namespace": "ClovaHome",
    "payloadVersion": "1.0"
  },
  "payload": {
    "phase": {
      "value": "Wash"
    }
  }
}
```

{% endraw %}

### See also
* [`GetPhaseRequest`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#GetPhaseRequest)
* [`GetPhaseResponse`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#GetPhaseResponse)
* [`StopConfirmation`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#StopConfirmation)
* [`StopRequest`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#StopRequest)

## ProgressiveTaxBracketInfoObject {#ProgressiveTaxBracketInfoObject}
ProgressiveTaxBracketInfoObject contains information on progressive tax brackets.

### Object fields
| Field name       | Data type    | Description                     | Required/Included |
|---------------|---------|-----------------------------|:-------------:|
| `value`       | number  | Progressive tax bracket                    | Required/Always     |

### Object Example
{% raw %}

```json
// Example 1: An example used in the GetProgressiveTaxBracketResponse message
{
  "header": {
    "messageId": "b502dd42-b698-4d3b-9ddb-bbdda70f254f",
    "name": "GetProgressiveTaxBracketResponse",
    "namespace": "ClovaHome",
    "payloadVersion": "1.0"
  },
  "payload": {
    "progressiveTaxBracket": {
      "value": 1
    },
    "applianceResponseTimestamp": "2017-11-23T20:30:19+09:00"
  }
}
```

{% endraw %}

### See also
* [`GetProgressiveTaxBracketRequest`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#GetProgressiveTaxBracketRequest)
* [`GetProgressiveTaxBracketResponse`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#GetProgressiveTaxBracketResponse)

## SpeedInfoObject {#SpeedInfoObject}
SpeedInfoObject contains information on speed. This is used to indicate the speed to change or the desired speed before and after the change. It is expressed as an integer.

### Object fields
| Field name       | Data type    | Description                     | Required/Included |
|---------------|---------|-----------------------------|:-------------:|
| `value`       | number  | Speed value                       | Required/Always     |

### Object Example
{% raw %}

```json
// Example 1: An example used in the IncrementFanSpeedRequest message
{
  "header": {
    "messageId": "6c04fc2d-64dd-41a0-9162-7cb0d4cf7c08",
    "name": "IncrementFanSpeedRequest",
    "namespace": "ClovaHome",
    "payloadVersion": "1.0"
  },
  "payload": {
    "accessToken": "92ebcb67fe33",
    "appliance": {
      "applianceId": "device-004"
    },
    "deltaFanSpeed": {
      "value": 1
    }
  }
}

// Example 2: An example used in the IncrementFanSpeedConfirmation message
{
  "header": {
    "messageId": "4ec35000-88ce-4724-b7e4-7f52050558fd",
    "name": "IncrementFanSpeedConfirmation",
    "namespace": "ClovaHome",
    "payloadVersion": "1.0"
  },
  "payload": {
    "targetFanSpeed": {
      "value": 3
    },
    "previousState": {
      "targetFanSpeed": {
        "value": 2
      }
    }
  }
}
```

{% endraw %}

### See also
* [`DecrementFanSpeedConfirmation`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#DecrementFanSpeedConfirmation)
* [`DecrementFanSpeedRequest`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#DecrementFanSpeedRequest)
* [`IncrementFanSpeedConfirmation`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#IncrementFanSpeedConfirmation)
* [`IncrementFanSpeedRequest`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#IncrementFanSpeedRequest)
* [`SetFanSpeedConfirmation`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#SetFanSpeedConfirmation)
* [`SetFanSpeedRequest`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#SetFanSpeedRequest)

## TimeInfoObject {#TimeInfoObject}
TimeInfoObject contains information on amount of time, such as elapsed time or remaining time. You must use the appropriate fields of the object for the situation, because the remaining time can be expressed in various ways. For example, the same amount of time can be expressed differently, such as 1 day and 1 hour or 25 hours.

### Object fields
| Field name       | Data type    | Description                     | Required/Included |
|---------------|---------|-----------------------------|:-------------:|
| `year`        | number  | 1 year unit                      | Optional/Conditional     |
| `month`       | number  | 1 month unit                    | Optional/Conditional     |
| `day`         | number  | 1 day unit                      | Optional/Conditional     |
| `hour`        | number  | 1 hour unit                     | Optional/Conditional     |
| `minute`      | number  | 1 minute unit                      | Optional/Conditional     |
| `second`      | number  | 1 second unit                      | Optional/Conditional     |

### Object Example
{% raw %}

```json
// Example: An example used in the GetKeepWarmTimeResponse message
{
  "header": {
    "messageId": "b502dd42-b698-4d3b-9ddb-bbdda70f254f",
    "name": "GetKeepWarmTimeResponse",
    "namespace": "ClovaHome",
    "payloadVersion": "1.0"
  },
  "payload": {
    "keepWarmTime": {
      "hour": 12
    },
    "applianceResponseTimestamp": "2017-11-23T20:30:19+09:00"
  }
}
```

{% endraw %}

### See also
* [`GetKeepWarmTimeRequest`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#GetKeepWarmTimeRequest)
* [`GetKeepWarmTimeResponse`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#GetKeepWarmTimeResponse)
* [`GetRemainingTimeRequest`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#GetRemainingTimeRequest)
* [`GetRemainingTimeResponse`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#GetRemainingTimeResponse)
* [`GetUsageTimeRequest`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#GetUsageTimeRequest)
* [`GetUsageTimeResponse`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#GetUsageTimeResponse)

## TemperatureInfoObject {#TemperatureInfoObject}
TemperatureInfoObject contains information on temperature. This is used to indicate the amount of temperature to change, the temperature before and after the change, or the currently set desired temperature. It is expressed up to one decimal place.

### Object fields
| Field name       | Data type    | Description                     | Required/Included |
|---------------|---------|-----------------------------|:-------------:|
| `value`       | number  | Temperature value                       | Required/Always     |

### Object Example
{% raw %}

```json
// Example 1: An example used in the IncrementTargetTemperatureRequest message
{
  "header": {
    "messageId": "6c04fc2d-64dd-41a0-9162-7cb0d4cf7c08",
    "name": "IncrementTargetTemperatureRequest",
    "namespace": "ClovaHome",
    "payloadVersion": "1.0"
  },
  "payload": {
    "accessToken": "92ebcb67fe33",
    "appliance": {
      "applianceId": "device-001"
    },
    "deltaTemperature": {
      "value": 1
    }
  }
}

// Example 2: An example used in the IncrementTargetTemperatureConfirmation message
{
  "header": {
    "messageId": "4ec35000-88ce-4724-b7e4-7f52050558fd",
    "name": "IncrementTargetTemperatureConfirmation",
    "namespace": "ClovaHome",
    "payloadVersion": "1.0"
  },
  "payload": {
    "targetTemperature": {
      "value": 25
    },
    "previousState": {
      "targetTemperature": {
        "value": 21
      }
    }
  }
}
```

{% endraw %}

### See also
* [`DecrementTargetTemperatureConfirmation`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#DecrementTargetTemperatureConfirmation)
* [`DecrementTargetTemperatureRequest`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#DecrementTargetTemperatureRequest)
* [`IncrementTargetTemperatureConfirmation`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#IncrementTargetTemperatureConfirmation)
* [`IncrementTargetTemperatureRequest`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#IncrementTargetTemperatureRequest)
* [`GetCurrentTargetTemperatureRequest`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#GetCurrentTargetTemperatureRequest)
* [`GetCurrentTargetTemperatureResponse`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#GetCurrentTargetTemperatureResponse)
* [`GetTargetTemperatureRequest`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#GetTargetTemperatureRequest)
* [`GetTargetTemperatureResponse`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#GetTargetTemperatureResponse)
* [`SetFreezerTargetTemperatureConfirmation`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#SetFreezerTargetTemperatureConfirmation)
* [`SetFreezerTargetTemperatureRequest`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#SetFreezerTargetTemperatureRequest)
* [`SetFridgeTargetTemperatureConfirmation`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#SetFridgeTargetTemperatureConfirmation)
* [`SetFridgeTargetTemperatureRequest`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#SetFridgeTargetTemperatureRequest)
* [`SetTargetTemperatureConfirmation`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#SetTargetTemperatureConfirmation)
* [`SetTargetTemperatureRequest`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#SetTargetTemperatureRequest)

## TVChannelNameInfoObject {#TVChannelNameInfoObject}
TVChannelNameInfoObject contains information on a TV channel name. This is used to indicate the name of TV channel to change or the TV channel before and after the change. It is expressed as a string.

### Object fields
| Field name       | Data type    | Description                     | Required/Included |
|---------------|---------|-----------------------------|:-------------:|
| `value`       | string  | Name of a TV channel                  | Required/Always     |

### Object Example
{% raw %}

```json
// Example 1: An example used in the SetChannelByNameRequest message
{
  "header": {
    "messageId": "6c04fc2d-64dd-41a0-9162-7cb0d4cf7c08",
    "name": "SetChannelByNameRequest",
    "namespace": "ClovaHome",
    "payloadVersion": "1.0"
  },
  "payload": {
    "accessToken": "92ebcb67fe33",
    "appliance": {
      "applianceId": "device-006"
    },
    "channel": {
      "value": "sbs"
    }
  }
}

// Example 2: An example used in the SetChannelByNameConfirmation message
{
  "header": {
    "messageId": "4ec35000-88ce-4724-b7e4-7f52050558fd",
    "name": "SetChannelByNameConfirmation",
    "namespace": "ClovaHome",
    "payloadVersion": "1.0"
  },
  "payload": {
  	"channelName": {
  		"value": "sbs"
  	}
  }
}
```

{% endraw %}

### See also
* [`SetChannelByNameConfirmation`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#SetChannelByNameConfirmation)
* [`SetChannelByNameRequest`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#SetChannelByNameRequest)

## TVChannelInfoObject {#TVChannelInfoObject}
TVChannelInfoObject contains information on a TV channel number. This is used to indicate the channel number of TV channel to change or the TV channel before and after the change. It is expressed as a number.

### Object fields
| Field name       | Data type    | Description                     | Required/Included |
|---------------|---------|-----------------------------|:-------------:|
| `value`       | number  | TV channel number                  | Required/Always     |

### Object Example
{% raw %}

```json
// Example 1: An example used in the SetChannelRequest message
{
  "header": {
    "messageId": "33da6561-0149-4532-a30b-e0de8f75c4cf",
    "name": "SetChannelRequest",
    "namespace": "ClovaHome",
    "payloadVersion": "1.0"
  },
  "payload": {
    "accessToken": "92ebcb67fe33",
    "appliance": {
        "applianceId": "device-007"
    },
    "channel": {
        "value": 13
    }
  }
}

// Example 2: An example used in the SetChannelConfirmation message
{
  "header": {
    "messageId": "4ec35000-88ce-4724-b7e4-7f52050558fd",
    "name": "SetChannelConfirmation",
    "namespace": "ClovaHome",
    "payloadVersion": "1.0"
  },
  "payload": {
    "channel": {
      "value": 13
    }
  }
}
```

{% endraw %}

### See also
* [`DecrementChannelConfirmation`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#DecrementChannelConfirmation)
* [`DecrementChannelRequest`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#DecrementChannelRequest)
* [`IncrementChannelConfirmation`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#IncrementChannelConfirmation)
* [`IncrementChannelRequest`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#IncrementChannelRequest)
* [`SetChannelConfirmation`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#SetChannelConfirmation)
* [`SetChannelRequest`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#SetChannelRequest)

## VolumeInfoObject {#VolumeInfoObject}
VolumeInfoObject contains information on the speaker volume. This is used to indicate the new volume to change or the volume before and after the change. It is expressed as an integer.

### Object fields
| Field name       | Data type    | Description                     | Required/Included |
|---------------|---------|-----------------------------|:-------------:|
| `value`       | number  | Value of the volume                       | Required/Always     |

### Object Example
{% raw %}

```json
// Example 1: An example used in the IncrementVolumeRequest message
{
  "header": {
    "messageId": "6c04fc2d-64dd-41a0-9162-7cb0d4cf7c08",
    "name": "IncrementVolumeRequest",
    "namespace": "ClovaHome",
    "payloadVersion": "1.0"
  },
  "payload": {
    "accessToken": "92ebcb67fe33",
    "appliance": {
      "applianceId": "device-005"
    },
    "deltaVolume": {
      "value": 10
    }
  }
}

// Example 2: An example used in the IncrementVolumeConfirmation message
{
  "header": {
    "messageId": "4ec35000-88ce-4724-b7e4-7f52050558fd",
    "name": "IncrementVolumeConfirmation",
    "namespace": "ClovaHome",
    "payloadVersion": "1.0"
  },
  "payload": {
    "targetVolume": {
      "value": 20
    },
    "previousState": {
      "targetVolume": {
        "value": 10
      }
    }
  }
}
```

{% endraw %}

### See also
* [`DecrementVolumeConfirmation`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#DecrementVolumeConfirmation)
* [`DecrementVolumeRequest`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#DecrementVolumeRequest)
* [`IncrementVolumeConfirmation`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#IncrementVolumeConfirmation)
* [`IncrementVolumeRequest`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#IncrementVolumeRequest)

## UltraFineDustInfoObject {#UltraFineDustInfoObject}
UltraFineDustInfoObject contains information on ultrafine dust. This is used to indicate the ultrafine dust index or the level measured by the appliance. It is expressed as a number.

### Object fields
| Field name       | Data type    | Description                     | Required/Included |
|---------------|---------|-----------------------------|:-------------:|
| `value`       | number  | Ultrafine dust index.                | Optional/Conditional    |
| `index`       | number  | Ultrafine dust level. It is limited to the following values.<ul><li><code>"good"</code>: Good</li><li><code>"normal"</code>: Normal</li><li><code>"bad"</code>: Bad</li><li><code>"verybad"</code>: Very bad</li></ul> | Required/Always     |

### Object Example
{% raw %}

```json
// Example: An example used in the GetUltraFineDustResponse message
{
  "header": {
    "messageId": "33da6561-0149-4532-a30b-e0de8f75c4cf",
    "name": "GetUltraFineDustResponse",
    "namespace": "ClovaHome",
    "payloadVersion": "1.0"
  },
  "payload": {
    "ultraFineDust": {
        "value": 44,
        "index": "good"
    }
  }
}
```

{% endraw %}

### See also
* [`GetUltraFineDustRequest`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#GetUltraFineDustRequest)
* [`GetUltraFineDustResponse`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#GetUltraFineDustResponse)
