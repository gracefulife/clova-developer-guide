# Control

IoT 기기 정보 확인 및 기기 제어와 관련된 요청 및 응답을 수행할 때 사용되는 인터페이스입니다.

| 메시지 이름         | 메시지 타입  | 메시지 설명                                   |
|------------------|-----------|---------------------------------------------|
| [`ChargeConfirmation`](#ChargeConfirmation)                                   | Response | [`ChargeRequest`](#ChargeRequest) 메시지에 대한 응답으로 대상 기기가 스스로 충전하도록 요청한 후 처리된 결과를 CEK에게 전달합니다. |
| [`ChargeRequest`](#ChargeRequest)                                             | Request  | 대상 기기가 스스로를 충전하도록 Clova Home extension에게 요청합니다. |
| [`CloseConfirmation`](#CloseConfirmation)                                     | Response | [`CloseRequest`](#CloseRequest) 메시지에 대한 응답으로 스마트 커튼이 일광 차단하거나, 비데의 뚜껑을 닫도록 요청한 후 처리된 결과를 CEK에게 전달합니다. |
| [`CloseRequest`](#CloseRequest)                                               | Request  | 스마트 커튼이나 비데 등의 제품을 제어할 때 사용되며, 스마트 커튼이 일광 차단하거나, 비데의 뚜껑을 닫도록 Clova Home extension에게 요청합니다.  |
| [`DecrementBrightnessConfirmation`](#DecrementBrightnessConfirmation)         | Response | [`DecrementBrightnessRequest`](#DecrementBrightnessRequest) 메시지에 대한 응답으로 대상 기기가 조명 밝기를 낮추도록 요청한 후 처리된 결과를 CEK에게 전달합니다. |
| [`DecrementBrightnessRequest`](#DecrementBrightnessRequest)                   | Request  | 대상 기기가 지정한 수준만큼 조명의 밝기를 낮추도록 Clova Home extension에게 요청합니다. |
| [`DecrementChannelConfirmation`](#DecrementChannelConfirmation)               | Response | [`DecrementChannelRequest`](#DecrementChannelRequest) 메시지에 대한 응답으로 대상 기기가 TV 채널을 낮추도록 요청한 후 처리된 결과를 CEK에게 전달합니다. |
| [`DecrementChannelRequest`](#DecrementChannelRequest)                         | Request  | 대상 기기가 지정한 수준만큼 TV 채널을 낮추도록 Clova Home extension에게 요청합니다. |
| [`DecrementFanSpeedConfirmation`](#DecrementFanSpeedConfirmation)             | Response | [`DecrementFanSpeedRequest`](#DecrementFanSpeedRequest) 메시지에 대한 응답으로 대상 기기가 팬 속도를 낮추도록 요청한 후 처리된 결과를 CEK에게 전달합니다. |
| [`DecrementFanSpeedRequest`](#DecrementFanSpeedRequest)                       | Request  | 대상 기기가 지정한 값만큼 팬 속도를 낮추도록 Clova Home extension에게 요청합니다. |
| [`DecrementIntensityLevelConfirmation`](#DecrementIntensityLevelConfirmation) | Response | [`DecrementIntensityLevelRequest`](#DecrementIntensityLevelRequest) 메시지에 대한 응답으로 대상 기기가 압력이나 수압 등의 세기를 낮추도록 요청한 후 처리된 결과를 CEK에게 전달합니다.  |
| [`DecrementIntensityLevelRequest`](#DecrementIntensityLevelRequest)           | Request  | 주로 에어컨이나 온도 조절 장치와 같은 기기를 제어할 때 사용되며, 대상 기기가 지정한 값만큼 압력이나 수압의 세기를 낮추도록 Clova Home extension에게 요청합니다.  |
| [`DecrementTargetTemperatureConfirmation`](#DecrementTargetTemperatureConfirmation) | Response | [`DecrementTargetTemperatureRequest`](#DecrementTargetTemperatureRequest) 메시지에 대한 응답으로 대상 기기가 온도를 낮추도록 요청한 후 처리된 결과를 CEK에게 전달합니다. |
| [`DecrementTargetTemperatureRequest`](#DecrementTargetTemperatureRequest)     | Request  | 대상 기기가 지정한 값만큼 온도를 낮추도록 Clova Home extension에게 요청합니다.      |
| [`DecrementVolumeConfirmation`](#DecrementVolumeConfirmation)                 | Response | [`DecrementVolumeRequest`](#DecrementVolumeRequest) 메시지에 대한 응답으로 대상 기기가 스피커 볼륨 크기를 낮추도록 요청한 후 처리된 결과를 CEK에게 전달합니다. |
| [`DecrementVolumeRequest`](#DecrementVolumeRequest)                           | Request  | 대상 기기가 지정한 값만큼 볼륨 크기를 낮추도록 Clova home extension에게 요청합니다. |
| [`GetAirQualityRequest`](#GetAirQualityRequest)                               | Request  | 대상 기기가 측정한 공기질 정보를 Clova Home extension에게 요청합니다. |
| [`GetAirQualityResponse`](#GetAirQualityResponse)                             | Response | [`GetAirQualityRequest`](#GetAirQualityRequest) 메시지에 대한 응답으로 대상 기기가 측정한 공기질 정보를 CEK에게 전달합니다. |
| [`GetAsleepDurationRequest`](#GetAsleepDurationRequest)                       | Request  | 주로 수면 센서에서 측정된 정보를 확인할 때 사용되며, 대상 기기가 측정한 사용자의 수면 시간을 Clova Home extension에게 요청합니다.  |
| [`GetAsleepDurationResponse`](#GetAsleepDurationResponse)                     | Response | [`GetAsleepDurationRequest`](#GetAsleepDurationRequest) 메시지에 대한 응답으로 대상 기기가 측정한 사용자의 수면 시간을 CEK에게 전달합니다.  |
| [`GetAwakeDurationRequest`](#GetAwakeDurationRequest)                         | Request  | 주로 수면 센서에서 측정된 정보를 확인할 때 사용되며, 대상 기기가 측정한 사용자의 취침 후 비수면 시간, 즉 사용자가 취침을 시작한 순간부터 수면에 진입한 순간까지의 시간을 Clova Home extension에게 요청합니다.  |
| [`GetAwakeDurationResponse`](#GetAwakeDurationResponse)                       | Response | [`GetAwakeDurationRequest`](#GetAwakeDurationRequest) 메시지에 대한 응답으로 대상 기기가 측정한 사용자의 취침 후 비수면 시간, 즉 사용자가 취침을 시작한 순간부터 수면에 진입한 순간까지의 시간을 CEK에게 전달합니다.  |
| [`GetBatteryInfoRequest`](#GetBatteryInfoRequest)                             | Request  | 대상 기기의 배터리 정보를 Clova Home extension에게 요청합니다. |
| [`GetBatteryInfoResponse`](#GetBatteryInfoResponse)                           | Response | [`GetBatteryInfoRequest`](#GetBatteryInfoRequest) 메시지에 대한 응답으로 대상 기기의 배터리 정보를 CEK에게 전달합니다. |
| [`GetCleaningCycleRequest`](#GetCleaningCycleRequest)                                                   | Request  | 기기의 세척 주기를 확인할 때 사용되며, 대상 기기의 다음 세척 주기까지 남은 시간에 대한 정보를 Clova Home extension에게 요청합니다.  |
| [`GetCleaningCycleResponse`](#GetCleaningCycleResponse)                                                  | Response | [`GetCleaningCycleRequest`](#GetCleaningCycleRequest) 메시지에 대한 응답으로 대상 기기의 다음 세척 주기까지 남은 시간을 CEK에게 전달합니다.  |
| [`GetCloseTimeRequest`](#GetCloseTimeRequest)                                 | Request  | 주로 열림 감지 센서가 감지한 내용 중 감지 대상이 마지막으로 닫혔던 시점의 시간 정보를 Clova Home extension에게 요청합니다. |
| [`GetCloseTimeResponse`](#GetCloseTimeResponse)                               | Response | [`GetCloseTimeRequest`](#GetCloseTimeRequest) 메시지에 대한 응답으로 대상 기기가 감지한 내용 중 감지 대상이 마지막으로 닫혔던 시점의 시간 정보를 CEK에게 전달합니다.  |
| [`GetConsumptionRequest`](#GetConsumptionRequest)                             | Request  | 주로 스마트 플러그나 스마트 멀티탭과 같은 기기에서 현재까지 측정된 에너지 또는 자원을 확인할 때 사용되며, 대상 기기가 측정한 에너지 또는 자원 정보를 Clova Home extension에게 요청합니다.  |
| [`GetConsumptionResponse`](#GetConsumptionResponse)                           | Response | [`GetConsumptionRequest`](#GetConsumptionRequest) 메시지에 대한 응답으로 대상 기기가 현재까지 측정한 에너지 또는 자원 정보를 CEK에게 전달합니다.  |
| [`GetCurrentBillRequest`](#GetCurrentBillRequest)                             | Request  | 주로 스마트 플러그나 스마트 멀티탭과 같은 기기에서 측정된 현재까지의 사용량의 기반으로 요금을 확인할 때 사용되며, 대상 기기가 측정한 요금 정보를 Clova Home extension에게 요청합니다.  |
| [`GetCurrentBillResponse`](#GetCurrentBillResponse)                           | Response | [`GetCurrentBillRequest`](#GetCurrentBillRequest) 메시지에 대한 응답으로 대상 기기가 현재까지 측정한 요금 정보를 CEK에게 전달합니다.   |
| [`GetCurrentTemperatureRequest`](#GetCurrentTemperatureRequest)               | Request  | 대상 기기가 측정한 현재 온도 정보를 Clova Home extension에게 요청합니다. |
| [`GetCurrentTemperatureResponse`](#GetCurrentTemperatureResponse)             | Response | [`GetCurrentTemperatureRequest`](#GetCurrentTemperatureRequest) 메시지에 대한 응답으로 대상 기기가 측정한 현재 온도 정보를 CEK에게 전달합니다. |
| [`GetDeviceStateRequest`](#GetDeviceStateRequest)                             | Request  | 대상 기기가 제공하는 모든 상태 정보를 확인할 때 사용됩니다.  |
| [`GetDeviceStateResponse`](#GetDeviceStateResponse)                           | Response | [`GetDeviceStateRequest`](#GetDeviceStateRequest) 메시지에 대한 응답으로 대상 기기가 제공하는 모든 상태 정보를 CEK에게 전달합니다.  |
| [`GetEstimateBillRequest`](#GetEstimateBillRequest)                           | Request  | 주로 스마트 플러그나 스마트 멀티탭과 같은 기기에서 측정된 사용량의 기반으로 예상 요금을 확인할 때 사용되며, 대상 기기가 예측한 요금 정보를 Clova Home extension에게 요청합니다.  |
| [`GetEstimateBillResponse`](#GetEstimateBillResponse)                         | Response | [`GetEstimateBillRequest`](#GetEstimateBillRequest) 메시지에 대한 응답으로 대상 기기가 예측한 요금 정보를 CEK에게 전달합니다.  |
| [`GetExpendableStateRequest`](#GetExpendableStateRequest)                     | Request  | 기기의 필터나 소모품의 사용량이나 남은 수명을 확인할 때 사용되며, 대상 기기가 보유하고 있는 소모품의 사용량이나 수명 정보를 Clova extension에게 요청합니다.  |
| [`GetExpendableStateResponse`](#GetExpendableStateResponse)                   | Response | [`GetExpendableStateRequest`](#GetExpendableStateRequest) 메시지에 대한 응답으로 대상 기기가 제공하는 모든 소모품의 사용량이나 수명 정보를 CEK에게 전달합니다. |
| [`GetFineDustRequest`](#GetFineDustRequest)                                   | Request  | 대상 기기가 측정한 미세 먼지(PM10) 정보를 Clova Home extension에게 요청합니다. |
| [`GetFineDustResponse`](#GetFineDustResponse)                                 | Response | [`GetFineDustRequest`](#GetFineDustRequest) 메시지에 대한 응답으로 대상 기기가 측정한 미세 먼지(PM10) 정보를 CEK에게 전달합니다. |
| [`GetHumidityRequest`](#GetHumidityRequest)                                   | Request  | 대상 기기가 측정한 습도 정보를 Clova Home extension에게 요청합니다. |
| [`GetHumidityResponse`](#GetHumidityResponse)                                 | Response | [`GetHumidityRequest`](#GetHumidityRequest) 메시지에 대한 응답으로 대상 기기가 측정한 습도 정보를 CEK에게 전달합니다. |
| [`GetKeepWarmTimeRequest`](#GetKeepWarmTimeRequest)                           | Request  | 밥솥과 같은 기기에서 음식의 보온에 사용된 시간을 확인할 때 사용되며, 대상 기기가 보온 모드를 유지한 시간 정보를 Clova Home extension에게 요청합니다.  |
| [`GetKeepWarmTimeResponse`](#GetKeepWarmTimeResponse)                         | Response | [`GetKeepWarmTimeRequest`](#GetKeepWarmTimeRequest) 메시지에 대한 응답으로 대상 기기가 보온 모드를 유지한 시간 정보를 CEK에게 전달합니다.  |
| [`GetLockStateRequest`](#GetLockStateRequest)                                 | Request  | 주로 스마트 밸브와 같은 기기의 상태를 확인할 때 사용되며, 대상 기기가 가진 잠금 장치의 현재 잠금 상태 정보를 Clova Home extension에게 요청합니다.  |
| [`GetLockStateResponse`](#GetLockStateResponse)                               | Response | [`GetLockStateRequest`](#GetLockStateRequest) 메시지에 대한 응답으로 대상 기기가 가진 잠금 장치의 현재 잠금 상태를 CEK에게 전달합니다.  |
| [`GetOpenStateRequest`](#GetOpenStateRequest)                                 | Request  | 주로 열림 감지 센서가 감지한 내용 중 감지 대상의 현재 상태 정보(열림 또는 닫힘)를 Clova Home extension에게 요청합니다.  |
| [`GetOpenStateResponse`](#GetOpenStateResponse)                               | Response | [`GetOpenStateRequest`](#GetOpenStateRequest) 메시지에 대한 응답으로 주로 감지 대상의 현재 상태 정보(열림 또는 닫힘)를 CEK에게 전달합니다.  |
| [`GetOpenTimeRequest`](#GetOpenTimeRequest)                                   | Request  | 주로 열림 감지 센서가 감지한 내용 중 감지 대상이 마지막으로 열렸던 시점의 시간 정보를 Clova Home extension에게 요청합니다.   |
| [`GetOpenTimeResponse`](#GetOpenTimeResponse)                                 | Response | [`GetOpenTimeRequest`](#GetOpenTimeRequest) 메시지에 대한 응답으로 대상 기기가 감지한 내용 중 감지 대상이 마지막으로 열렸던 시점의 시간 정보를 CEK에게 전달합니다.  |
| [`GetPhaseRequest`](#GetPhaseRequest)                                         | Request  | 주로 밥솥이나 세탁기와 같이 동작 단계가 있는 기기에서 현재 동작 단계 정보를 확인할 때 사용되며, 대상 기기의 현재 동작 단계 정보를 Clova Home extension에게 요청합니다.  |
| [`GetPhaseResponse`](#GetPhaseResponse)                                       | Response | [`GetPhaseRequest`](#GetPhaseRequest) 메시지에 대한 응답으로 대상 기기의 현재 동작 단계 정보를 CEK에게 전달합니다.  |
| [`GetProgressiveTaxBracketRequest`](#GetProgressiveTaxBracketRequest)         | Request  | 주로 전기 계량기나 스마트 플러그와 같은 기기에서 누진세 단계를 확인할 때 사용되며, 대상 기기가 판단한 누진세 단계 정보를 Clova Home extension에게 요청합니다.  |
| [`GetProgressiveTaxBracketResponse`](#GetProgressiveTaxBracketResponse)         | Response | [`GetProgressiveTaxBracketRequest`](#GetProgressiveTaxBracketRequest) 메시지에 대한 응답으로 대상 기기가 판단한 누진세 단계 정보를 CEK에게 전달합니다. |
| [`GetRemainingTimeRequest`](#GetRemainingTimeRequest)                         | Request  | 주로 밥솥이나 세탁기와 같은 기기에서 동작 종료까지 남은 시간을 확인할 때 사용되며, 대상 기기의 동작 종료까지 남은 시간에 대한 정보를 Clova Home extension에게 요청합니다.  |
| [`GetRemainingTimeResponse`](#GetRemainingTimeResponse)                       | Response | [`GetRemainingTimeRequest`](#GetRemainingTimeRequest) 메시지에 대한 응답으로 대상 기기가 동작 종료하기까지 남은 시간을 CEK에게 전달합니다. |
| [`GetRightPostureRatioRequest`](#GetRightPostureRatioRequest)                 | Request  | 사용자가 바른 자세로 대상 기기를 사용한 비율이 얼마인지 확인할 때 사용하며, 사용자가 대상 기기를 사용할 때 특정 기간이나 현재까지 바른 자세를 유지한 비율 정보를 Clova Home extension에게 요청합니다.  |
| [`GetRightPostureRatioResponse`](#GetRightPostureRatioResponse)               | Response | [`GetRightPostureRatioRequest`](#GetRightPostureRatioRequest) 메시지에 대한 응답으로 사용자가 대상 기기를 바른 자세로 사용한 비율 정보를 CEK에게 전달합니다.  |
| [`GetCurrentSittingStateRequest`](#GetCurrentSittingStateRequest)             | Request  | 스마트 의자와 같은 기기에서 사용자의 사용 상태를 확인할 때 사용되며, 대상 기기가 사용자 착석 여부를 감지한 정보와 최근 사용자가 사용한 시간 정보를 Clova Home extension에게 요청합니다.  |
| [`GetCurrentSittingStateResponse`](#GetCurrentSittingStateResponse)           | Response | [`GetCurrentSittingStateRequest`](#GetCurrentSittingStateRequest) 메시지에 대한 응답으로 대상 기기가 사용자 착석 여부를 감지한 정보와 최근 사용자가 사용한 시간 정보를 CEK에게 전달합니다.  |
| [`GetSleepScoreRequest`](#GetSleepScoreRequest)                               | Request  | 수면 센서와 같은 기기에서 사용자 수면 점수 정보를 확인할 때 사용되며, 대상 기기가 평가한 사용자의 수면 점수를 Clova Home extension에게 요청합니다.  |
| [`GetSleepScoreResponse`](#GetSleepScoreResponse)                             | Response | [`GetSleepScoreRequest`](#GetSleepScoreRequest) 메시지에 대한 응답으로 대상 기기가 평가한 사용자의 수면 점수를 CEK에게 전달합니다.  |
| [`GetSleepStartTimeRequest`](#GetSleepStartTimeRequest)                       | Request  | 수면 센서와 같은 기기에서 사용자 수면 점수 정보를 확인할 때 사용되며, 대상 기기가 측정한 사용자의 수면 시작 시간을 Clova Home extension에게 요청합니다.  |
| [`GetSleepStartTimeResponse`](#GetSleepStartTimeRequest)                      | Response | [`GetSleepStartTimeRequest`](#GetSleepStartTimeRequest) 메시지에 대한 응답으로 대상 기기가 측정한 사용자의 수면 시작 시간을 CEK에게 전달합니다.  |
| [`GetTargetTemperatureRequest`](#GetTargetTemperatureRequest)                 | Request  | 대상 기기가 설정한 희망 온도 정보를 Clova Home extension에게 요청합니다. |
| [`GetTargetTemperatureResponse`](#GetTargetTemperatureResponse)               | Response | [`GetTargetTemperatureRequest`](#GetTargetTemperatureRequest) 메시지에 대한 응답으로 대상 기기가 설정한 희망 온도 정보를 CEK에게 전달합니다. |
| [`GetUltraFineDustRequest`](#GetUltraFineDustRequest)                         | Request  | 대상 기기가 측정한 초미세 먼지(PM2.5) 정보를 Clova Home extension에게 요청합니다. |
| [`GetUltraFineDustResponse`](#GetUltraFineDustResponse)                       | Response | [`GetUltraFineDustRequest`](#GetUltraFineDustRequest) 메시지에 대한 응답으로 대상 기기가 측정한 초미세 먼지(PM2.5) 정보를 CEK에게 전달합니다. |
| [`GetUsageTimeRequest`](#GetUsageTimeRequest)                                 | Request | 사용자가 대상 기기를 얼마나 사용했는지 확인할 때 사용하며, 대상 기기가 특정 기간이나 현재까지 누적 사용된 시간 정보를 Clova Home extension에게 요청합니다.  |
| [`GetUsageTimeResponse`](#GetUsageTimeResponse)                               | Response | [`GetUsageTimeRequest`](#GetUsageTimeRequest) 메시지에 대한 응답으로 대상 기기가 사용된 시간 정보를 CEK에게 전달합니다.  |
| [`HealthCheckRequest`](#HealthCheckRequest)                                   | Request  | 지정한 기기의 상태를 파악할 때 사용되며, 대상 기기의 상태 정보를 Clova Home extension에게 요청합니다. |
| [`HealthCheckResponse`](#HealthCheckResponse)                                 | Response | [`HealthCheckRequest`](#HealthCheckRequest) 메시지에 대한 응답으로 지정한 기기의 상태 정보를 CEK에게 전달합니다. |
| [`IncrementBrightnessConfirmation`](#IncrementBrightnessConfirmation)         | Response | [`IncrementBrightnessRequest`](#IncrementBrightnessRequest) 메시지에 대한 응답으로 대상 기기가 조명 밝기를 높이도록 요청한 후 처리된 결과를 CEK에게 전달합니다. |
| [`IncrementBrightnessRequest`](#IncrementBrightnessRequest)                   | Request  | 대상 기기가 지정한 수준만큼 조명의 밝기를 높이도록 Clova Home extension에게 요청합니다. |
| [`IncrementChannelConfirmation`](#IncrementChannelConfirmation)               | Response | [`IncrementChannelRequest`](#IncrementChannelRequest) 메시지에 대한 응답으로 대상 기기가 TV 채널을 높이도록 요청한 후 처리된 결과를 CEK에게 전달합니다. |
| [`IncrementChannelRequest`](#IncrementChannelRequest)                         | Request  | 대상 기기가 지정한 수준만큼 TV 채널을 높이도록 Clova Home extension에게 요청합니다. |
| [`IncrementFanSpeedConfirmation`](#IncrementFanSpeedConfirmation)             | Response | [`IncrementFanSpeedRequest`](#IncrementFanSpeedRequest) 메시지에 대한 응답으로 대상 기기가 팬의 속도를 높이도록 요청한 후 처리된 결과를 CEK에게 전달합니다. |
| [`IncrementFanSpeedRequest`](#IncrementFanSpeedRequest)                       | Request | 대상 기기가 지정한 값만큼 팬 속도를 높이도록 Clova Home extension에게 요청합니다. |
| [`IncrementIntensityLevelConfirmation`](#IncrementIntensityLevelConfirmation) | Response | [`DecrementIntensityLevelRequest`](#DecrementIntensityLevelRequest) 메시지에 대한 응답으로 대상 기기가 압력이나 수압 등의 세기를 높이도록 요청한 후 처리된 결과를 CEK에게 전달합니다.  |
| [`IncrementIntensityLevelRequest`](#IncrementIntensityLevelRequest)           | Request  | 대상 기기가 지정한 값만큼 압력이나 수압의 세기를 높이도록 Clova Home extension에게 요청합니다. |
| [`IncrementTargetTemperatureConfirmation`](#IncrementTargetTemperatureConfirmation) | Response | [`IncrementTargetTemperatureRequest`](#IncrementTargetTemperatureRequest) 메시지에 대한 응답으로 대상 기기가 온도를 높이도록 요청한 후 처리된 결과를 CEK에게 전달합니다. |
| [`IncrementTargetTemperatureRequest`](#IncrementTargetTemperatureRequest)     | Request  | 대상 기기가 지정한 값만큼 온도를 높이도록 Clova Home extension에게 요청합니다.     |
| [`IncrementVolumeConfirmation`](#IncrementVolumeConfirmation)                 | Response | [`IncrementVolumeRequest`](#IncrementVolumeRequest) 메시지에 대한 응답으로 대상 기기가 스피커 볼륨을 높이도록 요청한 후 처리된 결과를 CEK에게 전달합니다. |
| [`IncrementVolumeRequest`](#IncrementVolumeRequest)                           | Request | 대상 기기가 지정한 값만큼 볼륨 크기를 높이도록 Clova Home extension에게 요청합니다. |
| [`LowerConfirmation`](#LowerConfirmation)                                     | Response | [`LowerRequest`](#LowerRequest) 메시지에 대한 응답으로 대상 기기의 높낮이를 낮추도록 요청한 후 처리된 결과를 CEK에게 전달합니다.  |
| [`LowerRequest`](#LowerRequest)                                               | Request  | 주로 커튼이나 블라인드, 침대 같은 기기를 제어할 때 사용되며, 대상 기기의 높낮이를 내리도록 Clova Home extension에게 요청합니다.  |
| [`MuteConfirmation`](#MuteConfirmation)                                       | Response | [`MuteRequest`](#MuteRequest) 메시지에 대한 응답으로 대상 기기의 소리를 끄도록 설정(음소거)한 결과를 CEK에게 전달합니다. |
| [`MuteRequest`](#MuteRequest)                                                 | Request  | 대상 기기의 소리를 끄도록(음소거) Clova Home extension에게 요청합니다. |
| [`OpenConfirmation`](#OpenConfirmation)                                       | Response | [`OpenRequest`](#OpenRequest) 메시지에 대한 응답으로 스마트 커튼이 일광 차단을 해제하거나, 비데의 뚜껑을 열도록 요청한 후 처리된 결과를 CEK에게 전달합니다. |
| [`OpenRequest`](#OpenRequest)                                                 | Request  | 스마트 커튼이나 비데 등의 제품을 제어할 때 사용되며, 스마트 커튼이 일광 차단을 해제하거나, 비데의 뚜껑을 열도록 Clova Home extension에게 요청합니다.  |
| [`RaiseConfirmation`](#RaiseConfirmation)                                     | Response | [`RaiseRequest`](#RaiseRequest) 메시지에 대한 응답으로 대상 기기의 높낮이를 높이도록 요청한 후 처리된 결과를 CEK에게 전달합니다.  |
| [`RaiseRequest`](#RaiseRequest)                                               | Request  | 주로 커튼이나 블라인드, 침대 같은 기기를 제어할 때 사용되며, 대상 기기의 높낮이를 높이도록 Clova Home extension에게 요청합니다.  |
| [`ReleaseModeConfirmation`](#ReleaseModeConfirmation)                         | Response | [`ReleaseModeRequest`](#ReleaseModeRequest) 메시지에 대한 응답으로 현재 기기의 운전 모드(operation mode)를 해제하도록 요청한 후 처리된 결과를 CEK에게 전달합니다.  |
| [`ReleaseModeRequest`](#ReleaseModeRequest)                                   | Request  | 현재 기기에 설정된 운전 모드(operation mode)를 해제할 때 사용되며, 기기의 운전 모드를 해제하여 이전 운전 모드나 기본 운전 모드로 돌아가도록 Clova Home extension에게 요청합니다.  |
| [`SetBrightnessConfirmation`](#SetBrightnessConfirmation)                     | Response | [`SetBrightnessRequest`](#SetBrightnessRequest) 메시지에 대한 응답으로 조명 밝기를 변경하도록 요청한 후 처리된 결과를 CEK에게 전달합니다. |
| [`SetBrightnessRequest`](#SetBrightnessRequest)                               | Request  | 대상 기기가 조명 밝기를 지정한 값으로 변경하도록 Clova Home extension에게 요청합니다. |
| [`SetChannelByNameConfirmation`](#SetChannelByNameConfirmation)               | Response | [`SetChannelByNameRequest`](#SetChannelByNameRequest) 메시지에 대한 응답으로 채널 이름으로 TV 채널을 변경하도록 요청한 후 처리된 결과를 CEK에게 전달합니다. |
| [`SetChannelByNameRequest`](#SetChannelByNameRequest)                         | Request  | 대상 기기가 지정한 채널 이름으로 채널을 변경하도록 Clova Home extension에게 요청합니다. |
| [`SetChannelConfirmation`](#SetChannelConfirmation)                           | Response | [`SetChannelRequest`](#SetChannelRequest) 메시지에 대한 응답으로 채널 번호로 TV 채널을 변경하도록 요청한 후 처리된 결과를 CEK에게 전달합니다. |
| [`SetChannelRequest`](#SetChannelRequest)                                     | Request  | 대상 기기가 지정한 채널 번호로 TV 채널을 변경하도록 Clova Home extension에게 요청합니다. |
| [`SetColorConfirmation`](#SetColorConfirmation)                               | Response | [`SetColorRequest`](#SetColorRequest) 메시지에 대한 응답으로 대상기기의 조명이나 화면, 전등의 색을 변경하도록 요청한 후 처리된 결과를 CEK에게 전달합니다. |
| [`SetColorRequest`](#SetColorRequest)                                         | Request  | 주로 스마트 전등과 같은 기기를 제어할 때 사용되며, 대상 기기의 조명이나 화면, 전등의 색을 변경하도록 Clova Home extension에게 요청합니다.  |
| [`SetColorTemperatureConfirmation`](#SetColorTemperatureConfirmation)         | Response | [`SetColorTemperatureRequest`](#SetColorTemperatureRequest) 메시지에 대한 응답으로 대상기기의 조명이나 화면, 전등의 색온도를 변경하도록 요청한 후 처리된 결과를 CEK에게 전달합니다.  |
| [`SetColorTemperatureRequest`](#SetColorTemperatureRequest)                   | Request  | 주로 스마트 전등과 같은 기기를 제어할 때 사용되며, 대상 기기의 조명이나 화면, 전등의 색온도를 변경하도록 Clova Home extension에게 요청합니다.  |
| [`SetFanSpeedConfirmation`](#SetFanSpeedConfirmation)                         | Response | [`SetFanSpeedRequest`](#SetFanSpeedRequest) 메시지에 대한 응답으로 팬 속도를 변경하도록 요청한 후 처리된 결과를 CEK에게 전달합니다. |
| [`SetFanSpeedRequest`](#SetFanSpeedRequest)                                   | Request  | 대상 기기가 지정한 값으로 팬 속도를 변경하도록 Clova Home extension에게 요청합니다. |
| [`SetFreezerTargetTemperatureConfirmation`](#SetFreezerTargetTemperatureConfirmation)  | Response  |  [`SetFreezerTargetTemperatureRequest`](#SetFreezerTargetTemperatureRequest) 메시지에 대한 응답으로 냉동실의 희망 온도를 변경하도록 요청한 후 처리된 결과를 CEK에게 전달합니다. |
| [`SetFreezerTargetTemperatureRequest`](#SetFreezerTargetTemperatureRequest)   | Request  | 냉장고 같은 기기를 제어할 때 사용되며, 냉장고의 냉동고 희망 온도를 지정한 값으로 변경하도록 Clova Home extension에게 요청합니다.  |
| [`SetFridgeTargetTemperatureConfirmation`](#SetFridgeTargetTemperatureConfirmation) | Response | [`SetFridgeTargetTemperatureRequest`](#SetFridgeTargetTemperatureRequest) 메시지에 대한 응답으로 냉장실의 희망 온도를 변경하도록 요청한 후 처리된 결과를 CEK에게 전달합니다.  |
| [`SetFridgeTargetTemperatureRequest`](#SetFridgeTargetTemperatureRequest)     | Request  | 냉장고 같은 기기를 제어할 때 사용되며, 냉장고의 냉장실 희망 온도를 지정한 값으로 변경하도록 Clova Home extension에게 요청합니다.  |
| [`SetLockStateConfirmation`](#SetLockStateConfirmation)                       | Response | [`SetLockStateRequest`](#SetLockStateRequest) 메시지에 대한 응답으로 대상 기기가 잠기거나 열리도록 요청한 후 처리된 결과를 CEK에게 전달합니다.  |
| [`SetLockStateRequest`](#SetLockStateRequest)                                 | Request  | 대상 기기를 잠그거나 열도록 Clova Home extension에게 요청합니다.  |
| [`SetModeConfirmation`](#SetModeConfirmation)                                 | Response | [`SetModeRequest`](#SetModeRequest) 메시지에 대한 응답으로 운전 모드(operation mode)를 변경하도록 요청한 후 처리된 결과를 CEK에게 전달합니다. |
| [`SetModeRequest`](#SetModeRequest)                                           | Request  | 대상 기기가 지정한 모드로 운전 모드(operation mode)를 변경하도록 Clova Home extension에게 요청합니다. |
| [`SetTargetTemperatureConfirmation`](#SetTargetTemperatureConfirmation)       | Response | [`SetTargetTemperatureRequest`](#SetTargetTemperatureRequest) 메시지에 대한 응답으로 희망 온도를 변경하도록 요청한 후 처리된 결과를 CEK에게 전달합니다. |
| [`SetTargetTemperatureRequest`](#SetTargetTemperatureRequest)                 | Request  | 대상 기기가 희망 온도를 지정한 값으로 변경하도록 Clova Home extension에게 요청합니다. |
| [`StopConfirmation`](#StopConfirmation)                                       | Response | [`StopRequest`](#StopRequest) 메시지에 대한 응답으로 대상 기기에게 동작 중지를 요청한 결과를 CEK에게 전달합니다.  |
| [`StopRequest`](#StopRequest)                                                 | Request  | 기기의 현재 동작을 중지하도록 Clova Home extension에게 요청합니다.  |
| [`TurnOffConfirmation`](#TurnOffConfirmation)                                 | Response | [`TurnOffRequest`](#TurnOffRequest) 메시지에 대한 응답으로 대상 기기를 끄도록 요청한 후 처리된 결과를 CEK에게 전달합니다. |
| [`TurnOffRequest`](#TurnOffRequest)                                           | Request  | 대상 기기를 끄도록 Clova Home extension에게 요청합니다.                        |
| [`TurnOnConfirmation`](#TurnOnConfirmation)                                   | Response | [`TurnOnRequest`](#TurnOnRequest) 메시지에 대한 응답으로 대상 기기를 켜도록 요청한 후 처리된 결과를 CEK에게 전달합니다. |
| [`TurnOnRequest`](#TurnOnRequest)                                             | Request  | 대상 기기를 켜도록 Clova Home extension에게 요청합니다.                        |
| [`UnmuteConfirmation`](#UnmuteConfirmation)                                   | Response | [`UnmuteRequest`](#UnmuteRequest) 메시지에 대한 응답으로 대상 기기의 소리를 켜도록 설정(음소거 해제)한 결과를 CEK에게 전달합니다. |
| [`UnmuteRequest`](#UnmuteRequest)                                             | Request  | 대상 기기의 소리를 켜도록(음소거 해제) Clova Home extension에게 요청합니다. |

## ChargeConfirmation {#ChargeConfirmation}
[`ChargeRequest`](#ChargeRequest) 메시지에 대한 응답으로 대상 기기가 스스로 충전하도록 요청한 후 처리된 결과를 CEK에게 전달합니다.

### Payload fields

없음

### Message example

{% raw %}

```json
{
  "header": {
    "messageId": "4ec35000-88ce-4724-b7e4-7f52050558fd",
    "name": "ChargeConfirmation",
    "namespace": "ClovaHome",
    "payloadVersion": "1.0"
  },
  "payload": {}
}
```

{% endraw %}

### See also
* [`ChargeRequest`](#ChargeRequest)

## ChargeRequest {#ChargeRequest}
주로 로봇 청소기를 제어할 때 사용되며, 대상 기기가 스스로를 충전하도록 Clova Home extension에게 요청합니다. 이 요청에 대한 응답으로 [`ChargeConfirmation`](#ChargeConfirmation) 메시지를 사용해야 합니다.

### Payload fields

| 필드 이름       | 자료형    | 필드 설명                     | 포함 여부 |
|---------------|---------|-----------------------------|:---------:|
| `accessToken`      | string                                  | IoT 서비스의 사용자 계정의 access token. CEK는 외부 서비스의 인증 서버로부터 획득한 사용자 계정의 access token을 전달합니다. 자세한 설명은 [사용자 계정 연결하기](/CEK/Guides/Link_User_Account.md)를 참조합니다.                          | 항상    |
| `appliance`        | [ApplianceInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#ApplianceInfoObject)     | 대상 기기 정보를 담고 있는 객체. `applianceId` 필드는 필수입니다.     | 항상    |

### Message example

{% raw %}

```json
{
  "header": {
    "messageId": "6c04fc2d-64dd-41a0-9162-7cb0d4cf7c08",
    "name": "ChargeRequest",
    "namespace": "ClovaHome",
    "payloadVersion": "1.0"
  },
  "payload": {
    "accessToken": "92ebcb67fe33",
    "appliance": {
      "applianceId": "device-009"
    }
  }
}
```

{% endraw %}

### See also
* [`ChargeConfirmation`](#ChargeConfirmation)

## CloseConfirmation {#CloseConfirmation}
[`CloseRequest`](#CloseRequest) 메시지에 대한 응답으로 스마트 커튼이 일광 차단하거나, 비데의 뚜껑을 닫도록 요청한 후 처리된 결과를 CEK에게 전달합니다.

### Payload fields

없음

### Message example

{% raw %}

```json
{
  "header": {
    "messageId": "a4349fd5-7c1c-4fae-9bbd-291749bdd63a",
    "name": "CloseConfirmation",
    "namespace": "ClovaHome",
    "payloadVersion": "1.0"
  },
  "payload": {}
}
```

{% endraw %}

### See also
* [`CloseRequest`](#CloseRequest)

## CloseRequest {#CloseRequest}
스마트 커튼이나 비데 등의 제품을 제어할 때 사용되며, 스마트 커튼이 일광 차단하거나, 비데의 뚜껑을 닫도록 Clova Home extension에게 요청합니다. 이 요청에 대한 응답으로 [`CloseConfirmation`](#CloseConfirmation) 메시지를 사용해야 합니다.

### Payload fields

| 필드 이름       | 자료형    | 필드 설명                     | 포함 여부 |
|---------------|---------|-----------------------------|:---------:|
| `accessToken`      | string                                  | IoT 서비스의 사용자 계정의 access token. CEK는 외부 서비스의 인증 서버로부터 획득한 사용자 계정의 access token을 전달합니다. 자세한 설명은 [사용자 계정 연결하기](/CEK/Guides/Link_User_Account.md)를 참조합니다.                          | 항상    |
| `appliance`        | [ApplianceInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#ApplianceInfoObject)     | 대상 기기 정보를 담고 있는 객체. `applianceId` 필드는 필수입니다.     | 항상    |

### Message example

{% raw %}

```json
{
  "header": {
    "messageId": "8030275d-0e71-463d-b1d8-3e761e5389ad",
    "name": "CloseRequest",
    "namespace": "ClovaHome",
    "payloadVersion": "1.0"
  },
  "payload": {
    "accessToken": "92ebcb67fe33",
    "appliance": {
      "applianceId": "device-012"
    }
  }
}
```

{% endraw %}

### See also
* [`CloseConfirmation`](#CloseConfirmation)

## DecrementBrightnessConfirmation {#DecrementBrightnessConfirmation}
[`DecrementBrightnessRequest`](#DecrementBrightnessRequest) 메시지에 대한 응답으로 대상 기기가 조명 밝기를 낮추도록 요청한 후 처리된 결과를 CEK에게 전달합니다.

### Payload fields

| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|:---------:|
| `brightness`               | [BrightnessInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#BrightnessInfoObject) | 현재 밝기 정보를 담고 있는 객체                                | 선택    |
| `previousState`            | object | 기기의 이전 상황 정보를 담고 있는 객체                           | 선택    |
| `previousState.brightness` | [BrightnessInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#BrightnessInfoObject) | 이전 밝기 정보를 담고 있는 객체                                | 선택    |

### Remarks

대상 기기에서 payload에 입력할 정보를 얻어올 수 없으면 값을 입력하지 않아도 됩니다. 이 경우 사용자에게 구체적인 정보 없이 기기 제어 요청이 정상 처리되었음을 알려줍니다.

### Message example

{% raw %}

```json
{
  "header": {
    "messageId": "4ec35000-88ce-4724-b7e4-7f52050558fd",
    "name": "DecrementBrightnessConfirmation",
    "namespace": "ClovaHome",
    "payloadVersion": "1.0"
  },
  "payload": {
    "brightness": {
      "value": 20
    },
    "previousState": {
      "brightness": {
        "value": 40
      }
    }
  }
}
```

{% endraw %}

### See also
* [`DecrementBrightnessRequest`](#DecrementBrightnessRequest)

## DecrementBrightnessRequest {#DecrementBrightnessRequest}
주로 조명 기기를 제어할 때 사용되며, 대상 기기가 지정한 수준만큼 조명의 밝기를 낮추도록 Clova Home extension에게 요청합니다. 이 요청에 대한 응답으로 [`DecrementBrightnessConfirmation`](#DecrementBrightnessConfirmation) 메시지를 사용해야 합니다.

### Payload fields

| 필드 이름       | 자료형    | 필드 설명                     | 포함 여부 |
|---------------|---------|-----------------------------|:---------:|
| `accessToken`      | string                                  | IoT 서비스의 사용자 계정의 access token. CEK는 외부 서비스의 인증 서버로부터 획득한 사용자 계정의 access token을 전달합니다. 자세한 설명은 [사용자 계정 연결하기](/CEK/Guides/Link_User_Account.md)를 참조합니다.                          | 항상    |
| `appliance`        | [ApplianceInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#ApplianceInfoObject)     | 대상 기기 정보를 담고 있는 객체. `applianceId` 필드는 필수입니다.     | 항상    |
| `deltaBrightness`       | [BrightnessInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#BrightnessInfoObject)             | 변경할 밝기의 크기 정보를 담고 있는 객체                              | 항상    |

### Message example

{% raw %}

```json
{
  "header": {
    "messageId": "6c04fc2d-64dd-41a0-9162-7cb0d4cf7c08",
    "name": "DecrementBrightnessRequest",
    "namespace": "ClovaHome",
    "payloadVersion": "1.0"
  },
  "payload": {
    "accessToken": "92ebcb67fe33",
    "appliance": {
      "applianceId": "device-010"
    },
    "deltaBrightness": {
      "value": 20
    }
  }
}
```

{% endraw %}

### See also
* [`DecrementBrightnessConfirmation`](#DecrementBrightnessConfirmation)

## DecrementChannelConfirmation {#DecrementChannelConfirmation}
[`DecrementChannelRequest`](#DecrementChannelRequest) 메시지에 대한 응답으로 대상 기기가 TV 채널을 낮추도록 요청한 후 처리된 결과를 CEK에게 전달합니다.

### Payload fields

| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|:---------:|
| `channel`               | [TVChannelInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#TVChannelInfoObject) | 현재 TV 채널 정보를 담고 있는 객체                                | 선택    |
| `subChannel`            | [TVChannelInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#TVChannelInfoObject) | 현재 TV 채널의 서브 채널 정보를 가지는 객체                         | 선택    |
| `previousState`            | object | 기기의 이전 상황 정보를 담고 있는 객체                           | 선택    |
| `previousState.channel`    | [TVChannelInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#TVChannelInfoObject) | 이전 TV 채널 정보를 담고 있는 객체                                | 선택    |
| `previousState.subChannel` | [TVChannelInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#TVChannelInfoObject) | 이전 TV 채널의 서브 채널 정보를 가지는 객체                         | 선택    |

### Remarks

대상 기기에서 payload에 입력할 정보를 얻어올 수 없으면 값을 입력하지 않아도 됩니다. 이 경우 사용자에게 구체적인 정보 없이 기기 제어 요청이 정상 처리되었음을 알려줍니다.

### Message example

{% raw %}

```json
{
  "header": {
    "messageId": "4ec35000-88ce-4724-b7e4-7f52050558fd",
    "name": "DecrementChannelConfirmation",
    "namespace": "ClovaHome",
    "payloadVersion": "1.0"
  },
  "payload": {
    "channel": {
      "value": 12
    },
    "subChannel": {
      "value": 1
    },
    "previousState": {
      "channel": {
        "value": 13
      },
      "subChannel": {
        "value": 1
      }
    }
  }
}
```
{% endraw %}

### See also
* [`DecrementChannelRequest`](#DecrementChannelRequest)

## DecrementChannelRequest {#DecrementChannelRequest}
주로 TV나 셋톱박스를 제어할 때 사용되며, 대상 기기가 지정한 수준만큼 TV 채널을 낮추도록 Clova Home extension에게 요청합니다. 이 요청에 대한 응답으로 [`DecrementChannelConfirmation`](#DecrementChannelConfirmation) 메시지를 사용해야 합니다.

### Payload fields

| 필드 이름       | 자료형    | 필드 설명                     | 포함 여부 |
|---------------|---------|-----------------------------|:---------:|
| `accessToken`      | string                                  | IoT 서비스의 사용자 계정의 access token. CEK는 외부 서비스의 인증 서버로부터 획득한 사용자 계정의 access token을 전달합니다. 자세한 설명은 [사용자 계정 연결하기](/CEK/Guides/Link_User_Account.md)를 참조합니다.                          | 항상    |
| `appliance`        | [ApplianceInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#ApplianceInfoObject)     | 대상 기기 정보를 담고 있는 객체. `applianceId` 필드는 필수입니다.     | 항상    |
| `deltaChannel`       | [TVChannelInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#TVChannelInfoObject)             | 변경할 TV 채널의 크기 정보를 담고 있는 객체                              | 항상    |

### Message example

{% raw %}

```json
{
  "header": {
    "messageId": "6c04fc2d-64dd-41a0-9162-7cb0d4cf7c08",
    "name": "DecrementChannelRequest",
    "namespace": "ClovaHome",
    "payloadVersion": "1.0"
  },
  "payload": {
    "accessToken": "92ebcb67fe33",
    "appliance": {
      "applianceId": "device-011"
    },
    "deltaChannel": {
      "value": 1
    }
  }
}
```

{% endraw %}

### See also
* [`DecrementChannelConfirmation`](#DecrementChannelConfirmation)

## DecrementFanSpeedConfirmation {#DecrementFanSpeedConfirmation}
[`DecrementFanSpeedRequest`](#DecrementFanSpeedRequest) 메시지에 대한 응답으로 대상 기기가 팬 속도를 낮추도록 요청한 후 처리된 결과를 CEK에게 전달합니다.

### Payload fields

| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|:---------:|
| `fanSpeed`       | [SpeedInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#SpeedInfoObject)             | 현재 팬의 속도 정보를 담고 있는 객체. 팬의 속도는 풍속을 의미하며 팬 속도를 다음과 같은 값으로 제한합니다.<ul><li><code>1</code>: 약한 바람(1단)</li><li><code>2</code>: 중간 바람(2단)</li><li><code>3</code>: 강한 바람(3단)</li></ul> | 선택    |
| `previousState`     | object                                  | 기기의 이전 상황 정보를 담고 있는 객체                           | 선택    |
| `previousState.fanSpeed` | [SpeedInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#SpeedInfoObject)     | 이전 팬의 속도 정보를 담고 있는 객체. 팬의 속도는 풍속을 의미하며 팬 속도를 다음과 같은 값으로 제한합니다.<ul><li><code>1</code>: 약한 바람(1단)</li><li><code>2</code>: 중간 바람(2단)</li><li><code>3</code>: 강한 바람(3단)</li></ul> | 선택    |

### Remarks

대상 기기에서 payload에 입력할 정보를 얻어올 수 없으면 값을 입력하지 않아도 됩니다. 이 경우 사용자에게 구체적인 정보 없이 기기 제어 요청이 정상 처리되었음을 알려줍니다.

### Message example

{% raw %}

```json
{
  "header": {
    "messageId": "4ec35000-88ce-4724-b7e4-7f52050558fd",
    "name": "DecrementFanSpeedConfirmation",
    "namespace": "ClovaHome",
    "payloadVersion": "1.0"
  },
  "payload": {
    "fanSpeed": {
      "value": 2
    },
    "previousState": {
      "fanSpeed": {
        "value": 3
      }
    }
  }
}
```

{% endraw %}

### See also
* [`DecrementFanSpeedRequest`](#DecrementFanSpeedRequest)

## DecrementFanSpeedRequest {#DecrementFanSpeedRequest}
주로 공기청정기와 같은 기기를 제어할 때 사용되며, 대상 기기가 지정한 수준만큼 팬의 속도를 낮추도록 Clova Home extension에게 요청합니다. 이 요청에 대한 응답으로 [`DecrementFanSpeedConfirmation`](#DecrementFanSpeedConfirmation) 메시지를 사용해야 합니다.

### Payload fields

| 필드 이름       | 자료형    | 필드 설명                     | 포함 여부 |
|---------------|---------|-----------------------------|:---------:|
| `accessToken`      | string                                  | IoT 서비스의 사용자 계정의 access token. CEK는 외부 서비스의 인증 서버로부터 획득한 사용자 계정의 access token을 전달합니다. 자세한 설명은 [사용자 계정 연결하기](/CEK/Guides/Link_User_Account.md)를 참조합니다.                          | 항상    |
| `appliance`        | [ApplianceInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#ApplianceInfoObject)     | 대상 기기 정보를 담고 있는 객체. `applianceId` 필드는 필수입니다.     | 항상    |
| `deltaFanSpeed`       | [SpeedInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#SpeedInfoObject)             | 변경할 팬 속도의 크기 정보를 담고 있는 객체. 팬의 속도는 풍속을 의미하며 팬 속도를 다음과 같은 값으로 제한합니다.<ul><li><code>1</code>: 약한 바람(1단)</li><li><code>2</code>: 중간 바람(2단)</li><li><code>3</code>: 강한 바람(3단)</li></ul> | 항상    |

### Message example

{% raw %}

```json
{
  "header": {
    "messageId": "6c04fc2d-64dd-41a0-9162-7cb0d4cf7c08",
    "name": "DecrementFanSpeedRequest",
    "namespace": "ClovaHome",
    "payloadVersion": "1.0"
  },
  "payload": {
    "accessToken": "92ebcb67fe33",
    "appliance": {
      "applianceId": "device-004"
    },
    "deltaFanSpeed": {
      "value": 2
    }
  }
}
```

{% endraw %}

### See also
* [`DecrementFanSpeedConfirmation`](#DecrementFanSpeedConfirmation)

## DecrementIntensityLevelConfirmation {#DecrementIntensityLevelConfirmation}
[`DecrementIntensityLevelRequest`](#DecrementIntensityLevelRequest) 메시지에 대한 응답으로 대상 기기가 압력이나 수압 등의 세기를 낮추도록 요청한 후 처리된 결과를 CEK에게 전달합니다.

### Payload fields

| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|:---------:|
| `intensityLevel` | [IntensityLevelInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#IntensityLevelInfoObject) | 현재 압력/수압 등의 세기 정보를 담고 있는 객체                  | 선택    |
| `previousState`  | object                                  | 기기의 이전 상황 정보를 담고 있는 객체                           | 선택    |
| `previousState.intensityLevel` | [IntensityLevelInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#IntensityLevelInfoObject) | 이전 압력/수압 등의 세기 정보를 담고 있는 객체    | 선택    |

### Remarks

대상 기기에서 payload에 입력할 정보를 얻어올 수 없으면 값을 입력하지 않아도 됩니다. 이 경우 사용자에게 구체적인 정보 없이 기기 제어 요청이 정상 처리되었음을 알려줍니다.

### Message example

{% raw %}

```json
{
  "header": {
    "messageId": "be3dde71-84c0-48cf-80d8-440c1ede54d8",
    "name": "DecrementIntensityLevelConfirmation",
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
* [`DecrementIntensityLevelRequest`](#DecrementIntensityLevelRequest)

## DecrementIntensityLevelRequest {#DecrementIntensityLevelRequest}
주로 에어컨이나 온도 조절 장치와 같은 기기를 제어할 때 사용되며, 대상 기기가 지정한 값만큼 압력이나 수압의 세기를 낮추도록 Clova Home extension에게 요청합니다. 이 요청에 대한 응답으로 [`DecrementIntensityLevelConfirmation`](#DecrementIntensityLevelConfirmation) 메시지를 사용해야 합니다.

### Payload fields

| 필드 이름       | 자료형    | 필드 설명                     | 포함 여부 |
|---------------|---------|-----------------------------|:---------:|
| `accessToken`      | string                                  | IoT 서비스의 사용자 계정의 access token. CEK는 외부 서비스의 인증 서버로부터 획득한 사용자 계정의 access token을 전달합니다. 자세한 설명은 [사용자 계정 연결하기](/CEK/Guides/Link_User_Account.md)를 참조합니다.                          | 항상    |
| `appliance`        | [ApplianceInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#ApplianceInfoObject)     | 대상 기기 정보를 담고 있는 객체. `applianceId` 필드는 필수입니다. | 항상    |
| `deltaIntensity`   | [IntensityLevelInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#TemperatureInfoObject) | 변경할 세기의 정보를 담고 있는 객체                            | 항상    |

### Message example

{% raw %}

```json
{
  "header": {
    "messageId": "6c04fc2d-64dd-41a0-9162-7cb0d4cf7c08",
    "name": "DecrementIntensityLevelRequest",
    "namespace": "ClovaHome",
    "payloadVersion": "1.0"
  },
  "payload": {
    "accessToken": "92ebcb67fe33",
    "appliance": {
      "applianceId": "device-015"
    },
    "deltaTemperature": {
      "value": 1
    }
  }
}
```

{% endraw %}

### See also
* [`DecrementIntensityLevelConfirmation`](#DecrementIntensityLevelConfirmation)

## DecrementTargetTemperatureConfirmation {#DecrementTargetTemperatureConfirmation}
[`DecrementTargetTemperatureRequest`](#DecrementTargetTemperatureRequest) 메시지에 대한 응답으로 대상 기기가 온도를 낮추도록 요청한 후 처리된 결과를 CEK에게 전달합니다.

### Payload fields

| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|:---------:|
| `previousState`     | object                                  | 기기의 이전 상황 정보를 담고 있는 객체                           | 선택    |
| `previousState.targetTemperature` | [TemperatureInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#TemperatureInfoObject) | 이전 희망 온도 정보를 담고 있는 객체              | 선택    |
| `targetTemperature` | [TemperatureInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#TemperatureInfoObject) | 대상 기기에 설정되었거나 extension이 대상 기기에게 설정하도록 요청한 희망 온도 정보를 담고 있는 객체                            | 선택    |

### Remarks

대상 기기에서 payload에 입력할 정보를 얻어올 수 없으면 값을 입력하지 않아도 됩니다. 이 경우 사용자에게 구체적인 정보 없이 기기 제어 요청이 정상 처리되었음을 알려줍니다.

### Message example

{% raw %}

```json
{
  "header": {
    "messageId": "4ec35000-88ce-4724-b7e4-7f52050558fd",
    "name": "DecrementTargetTemperatureConfirmation",
    "namespace": "ClovaHome",
    "payloadVersion": "1.0"
  },
  "payload": {
    "targetTemperature": {
      "value": 23
    },
    "previousState": {
      "targetTemperature": {
        "value": 25
      }
    }
  }
}
```

{% endraw %}

### See also
* [`DecrementTargetTemperatureRequest`](#DecrementTargetTemperatureRequest)

## DecrementTargetTemperatureRequest {#DecrementTargetTemperatureRequest}
주로 에어컨이나 온도 조절 장치와 같은 기기를 제어할 때 사용되며, 대상 기기가 지정한 값만큼 온도를 낮추도록 Clova Home extension에게 요청합니다. 이 요청에 대한 응답으로 [`DecrementTargetTemperatureConfirmation`](#DecrementTargetTemperatureConfirmation) 메시지를 사용해야 합니다.

### Payload fields

| 필드 이름       | 자료형    | 필드 설명                     | 포함 여부 |
|---------------|---------|-----------------------------|:---------:|
| `accessToken`      | string                                  | IoT 서비스의 사용자 계정의 access token. CEK는 외부 서비스의 인증 서버로부터 획득한 사용자 계정의 access token을 전달합니다. 자세한 설명은 [사용자 계정 연결하기](/CEK/Guides/Link_User_Account.md)를 참조합니다.                          | 항상    |
| `appliance`        | [ApplianceInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#ApplianceInfoObject)     | 대상 기기 정보를 담고 있는 객체. `applianceId` 필드는 필수입니다. | 항상    |
| `deltaTemperature` | [TemperatureInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#TemperatureInfoObject) | 변경할 온도의 크기 정보를 담고 있는 객체                              | 항상    |

### Message example

{% raw %}

```json
{
  "header": {
    "messageId": "6c04fc2d-64dd-41a0-9162-7cb0d4cf7c08",
    "name": "DecrementTargetTemperatureRequest",
    "namespace": "ClovaHome",
    "payloadVersion": "1.0"
  },
  "payload": {
    "accessToken": "92ebcb67fe33",
    "appliance": {
      "applianceId": "device-001"
    },
    "deltaTemperature": {
      "value": 2
    }
  }
}
```

{% endraw %}

### See also
* [`DecrementTargetTemperatureConfirmation`](#DecrementTargetTemperatureConfirmation)

## DecrementVolumeConfirmation {#DecrementVolumeConfirmation}
[`DecrementVolumeRequest`](#DecrementVolumeRequest) 메시지에 대한 응답으로 대상 기기가 스피커 볼륨 크기를 낮추도록 요청한 후 처리된 결과를 CEK에게 전달합니다.

### Payload fields

| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|:---------:|
| `previousState`     | object                                  | 기기의 이전 상황 정보를 담고 있는 객체                        | 선택    |
| `previousState.targetVolume` | [VolumeInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#SpeedInfoObject)    | 이전 볼륨 정보를 담고 있는 객체                             | 선택    |
| `targetVolume`      | [VolumeInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#SpeedInfoObject)            | 대상 기기에 설정되었거나 extension이 대상 기기에게 설정하도록 요청한 볼륨 정보를 담고 있는 객체                             | 선택    |

### Remarks

대상 기기에서 payload에 입력할 정보를 얻어올 수 없으면 값을 입력하지 않아도 됩니다. 이 경우 사용자에게 구체적인 정보 없이 기기 제어 요청이 정상 처리되었음을 알려줍니다.

### Message example

{% raw %}

```json
{
  "header": {
    "messageId": "4ec35000-88ce-4724-b7e4-7f52050558fd",
    "name": "DecrementVolumeConfirmation",
    "namespace": "ClovaHome",
    "payloadVersion": "1.0"
  },
  "payload": {
    "targetVolume": {
      "value": 10
    },
    "previousState": {
      "targetVolume": {
        "value": 20
      }
    }
  }
}
```

{% endraw %}

### See also
* [`DecrementVolumeRequest`](#DecrementVolumeRequest)

## DecrementVolumeRequest {#DecrementVolumeRequest}
주로 TV 셋톱 박스와 같은 기기를 제어할 때 사용되며, 대상 기기가 지정한 수준만큼 스피커 볼륨을 낮추도록 Clova Home extension에게 요청합니다. 이 요청에 대한 응답으로 [`DecrementVolumeConfirmation`](#DecrementVolumeConfirmation) 메시지를 사용해야 합니다.

### Payload fields

| 필드 이름       | 자료형    | 필드 설명                     | 포함 여부 |
|---------------|---------|-----------------------------|:---------:|
| `accessToken`      | string                                  | IoT 서비스의 사용자 계정의 access token. CEK는 외부 서비스의 인증 서버로부터 획득한 사용자 계정의 access token을 전달합니다. 자세한 설명은 [사용자 계정 연결하기](/CEK/Guides/Link_User_Account.md)를 참조합니다.                          | 항상    |
| `appliance`        | [ApplianceInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#ApplianceInfoObject)     | 대상 기기 정보를 담고 있는 객체. `applianceId` 필드는 필수입니다.     | 항상    |
| `deltaVolume`       | [VolumeInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#VolumeInfoObject)             | 변경할 볼륨의 크기 정보를 담고 있는 객체                           | 항상    |

### Message example

{% raw %}

```json
{
  "header": {
    "messageId": "6c04fc2d-64dd-41a0-9162-7cb0d4cf7c08",
    "name": "DecrementVolumeRequest",
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
```

{% endraw %}

### See also
* [`DecrementVolumeConfirmation`](#DecrementVolumeConfirmation)

## GetAirQualityRequest {#GetAirQualityRequest}
주로 공기청정기와 같은 기기에서 측정된 공기질 정보를 확인할 때 사용되며, 대상 기기가 측정한 공기질 정보를 Clova Home extension에게 요청합니다. 이 요청에 대한 응답으로 [`GetAirQualityResponse`](#GetAirQualityResponse) 메시지를 사용해야 합니다.

| 필드 이름       | 자료형    | 필드 설명                     | 포함 여부 |
|---------------|---------|-----------------------------|:---------:|
| `accessToken`      | string                                  | IoT 서비스의 사용자 계정의 access token. CEK는 외부 서비스의 인증 서버로부터 획득한 사용자 계정의 access token을 전달합니다. 자세한 설명은 [사용자 계정 연결하기](/CEK/Guides/Link_User_Account.md)를 참조합니다.                          | 항상    |
| `appliance`        | [ApplianceInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#ApplianceInfoObject)     | 대상 기기 정보를 담고 있는 객체. `applianceId` 필드는 필수입니다.     | 항상    |

### Message example

{% raw %}

```json
{
  "header": {
    "messageId": "6c04fc2d-64dd-41a0-9162-7cb0d4cf7c08",
    "name": "GetAirQualityRequest",
    "namespace": "ClovaHome",
    "payloadVersion": "1.0"
  },
  "payload": {
    "accessToken": "92ebcb67fe33",
    "appliance": {
      "applianceId": "device-011"
    }
  }
}
```

{% endraw %}

### See also
* [`GetAirQualityResponse`](#GetAirQualityResponse)

## GetAirQualityResponse {#GetAirQualityResponse}
[`GetAirQualityRequest`](#GetAirQualityRequest) 메시지에 대한 응답으로 대상 기기가 측정한 공기질 정보를 CEK에게 전달합니다.

| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|:---------:|
| `airQuality`                 | [AirQualityInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#AirQualityInfoObject) | 현재 기기가 측정한 공기질 정보를 담고 있는 객체   | 필수    |
| `applianceResponseTimestamp` | string | 기기에서 요청한 정보를 확인한 시간(Timestamp, <a href="https://en.wikipedia.org/wiki/ISO_8601" target="_blank">ISO 8601</a>)     | 선택    |

### Message example

{% raw %}

```json
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
    },
    "applianceResponseTimestamp": "2017-11-23T20:30:04+09:00"
  }
}
```

{% endraw %}

### See also
* [`GetAirQualityRequest`](#GetAirQualityRequest)

## GetAsleepDurationRequest {#GetAsleepDurationRequest}
주로 수면 센서에서 측정된 정보를 확인할 때 사용되며, 대상 기기가 측정한 사용자의 수면 시간을 Clova Home extension에게 요청합니다. 이 요청에 대한 응답으로 [`GetAsleepDurationResponse`](#GetAsleepDurationResponse) 메시지를 사용해야 합니다.

| 필드 이름       | 자료형    | 필드 설명                     | 포함 여부 |
|---------------|---------|-----------------------------|:---------:|
| `accessToken`      | string                                  | IoT 서비스의 사용자 계정의 access token. CEK는 외부 서비스의 인증 서버로부터 획득한 사용자 계정의 access token을 전달합니다. 자세한 설명은 [사용자 계정 연결하기](/CEK/Guides/Link_User_Account.md)를 참조합니다.                          | 항상    |
| `appliance`        | [ApplianceInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#ApplianceInfoObject)     | 대상 기기 정보를 담고 있는 객체. `applianceId` 필드는 필수입니다.     | 항상    |
| `period`           | [PeriodInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#PeriodInfoObject)           | 기간 정보를 담고 있는 객체                                      | 조건부  |

### Message example

{% raw %}

```json
{
  "header": {
    "messageId": "6c04fc2d-64dd-41a0-9162-7cb0d4cf7c08",
    "name": "GetAsleepDurationRequest",
    "namespace": "ClovaHome",
    "payloadVersion": "1.0"
  },
  "payload": {
    "accessToken": "92ebcb67fe33",
    "appliance": {
      "applianceId": "device-032"
    },
    "period": {
      "start": "2018-03-28T00:00:00+09:00",
      "end": "2018-03-28T23:59:59+09:00"
    }
  }
}
```

{% endraw %}

### See also
* [`GetAsleepDurationResponse`](#GetAsleepDurationResponse)

## GetAsleepDurationResponse {#GetAsleepDurationResponse}
[`GetAsleepDurationRequest`](#GetAsleepDurationRequest) 메시지에 대한 응답으로 대상 기기가 측정한 사용자의 수면 시간을 CEK에게 전달합니다.

| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|:---------:|
| `applianceResponseTimestamp`  | string | 기기에서 요청한 정보를 확인한 시간(Timestamp, <a href="https://en.wikipedia.org/wiki/ISO_8601" target="_blank">ISO 8601</a>)     | 선택    |
| `asleepDuration`                    | string | 수면 시간의 평균(Duration, <a href="https://en.wikipedia.org/wiki/ISO_8601#Durations" target="_blank">ISO 8601</a>)   | 필수    |

### Message example

{% raw %}

```json
{
  "header": {
    "messageId": "33da6561-0149-4532-a30b-e0de8f75c4cf",
    "name": "GetAsleepDurationResponse",
    "namespace": "ClovaHome",
    "payloadVersion": "1.0"
  },
  "payload": {
    "asleepDuration": "PT8H40M",
    "applianceResponseTimestamp": "2018-03-29T16:22:22+09:00"
  }
}
```

{% endraw %}

### See also
* [`GetAsleepDurationRequest`](#GetAsleepDurationRequest)

## GetAwakeDurationRequest {#GetAwakeDurationRequest}
주로 수면 센서에서 측정된 정보를 확인할 때 사용되며, 대상 기기가 측정한 사용자의 취침 후 비수면 시간, 즉 사용자가 취침을 시작한 순간부터 수면에 진입한 순간까지의 시간을 Clova Home extension에게 요청합니다. 이 요청에 대한 응답으로 [`GetAwakeDurationResponse`](#GetAwakeDurationResponse) 메시지를 사용해야 합니다.

| 필드 이름       | 자료형    | 필드 설명                     | 포함 여부 |
|---------------|---------|-----------------------------|:---------:|
| `accessToken`      | string                                  | IoT 서비스의 사용자 계정의 access token. CEK는 외부 서비스의 인증 서버로부터 획득한 사용자 계정의 access token을 전달합니다. 자세한 설명은 [사용자 계정 연결하기](/CEK/Guides/Link_User_Account.md)를 참조합니다.                          | 항상    |
| `appliance`        | [ApplianceInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#ApplianceInfoObject)     | 대상 기기 정보를 담고 있는 객체. `applianceId` 필드는 필수입니다.     | 항상    |
| `period`           | [PeriodInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#PeriodInfoObject)           | 기간 정보를 담고 있는 객체                                      | 조건부  |

### Message example

{% raw %}

```json
{
  "header": {
    "messageId": "6c04fc2d-64dd-41a0-9162-7cb0d4cf7c08",
    "name": "GetAwakeDurationRequest",
    "namespace": "ClovaHome",
    "payloadVersion": "1.0"
  },
  "payload": {
    "accessToken": "92ebcb67fe33",
    "appliance": {
      "applianceId": "device-032"
    },
    "period": {
      "start": "2018-03-28T00:00:00+09:00",
      "end": "2018-03-28T23:59:59+09:00"
    }
  }
}
```

{% endraw %}

### See also
* [`GetAwakeDurationResponse`](#GetAwakeDurationResponse)

## GetAwakeDurationResponse {#GetAwakeDurationResponse}
[`GetAwakeDurationRequest`](#GetAwakeDurationRequest) 메시지에 대한 응답으로 대상 기기가 측정한 사용자의 취침 후 비수면 시간, 즉 사용자가 취침을 시작한 순간부터 수면에 진입한 순간까지의 시간을 CEK에게 전달합니다.

| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|:---------:|
| `applianceResponseTimestamp`  | string | 기기에서 요청한 정보를 확인한 시간(Timestamp, <a href="https://en.wikipedia.org/wiki/ISO_8601" target="_blank">ISO 8601</a>)     | 선택    |
| `awakeDuration`                    | string | 취침 후 비수면 시간의 평균(Duration, <a href="https://en.wikipedia.org/wiki/ISO_8601#Durations" target="_blank">ISO 8601</a>)   | 필수    |

### Message example

{% raw %}

```json
{
  "header": {
    "messageId": "33da6561-0149-4532-a30b-e0de8f75c4cf",
    "name": "GetAwakeDurationResponse",
    "namespace": "ClovaHome",
    "payloadVersion": "1.0"
  },
  "payload": {
    "awakeDuration": "PT0H20M",
    "applianceResponseTimestamp": "2018-03-29T16:22:22+00:00"
  }
}
```

{% endraw %}

### See also
* [`GetAwakeDurationRequest`](#GetAwakeDurationRequest)

## GetBatteryInfoRequest {#GetBatteryInfoRequest}
주로 로봇청소기와 같이 무선 동작하는 기기의 내장 배터리 정보를 확인할 때 사용되며, 대상 기기의 현재 배터리 정보를 Clova Home extension에게 요청합니다. 이 요청에 대한 응답으로 [`GetBatteryInfoResponse`](#GetBatteryInfoResponse) 메시지를 사용해야 합니다.

| 필드 이름       | 자료형    | 필드 설명                     | 포함 여부 |
|---------------|---------|-----------------------------|:---------:|
| `accessToken`      | string                                  | IoT 서비스의 사용자 계정의 access token. CEK는 외부 서비스의 인증 서버로부터 획득한 사용자 계정의 access token을 전달합니다. 자세한 설명은 [사용자 계정 연결하기](/CEK/Guides/Link_User_Account.md)를 참조합니다.                          | 항상    |
| `appliance`        | [ApplianceInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#ApplianceInfoObject)     | 대상 기기 정보를 담고 있는 객체. `applianceId` 필드는 필수입니다.     | 항상    |

### Message example

{% raw %}

```json
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
      "applianceId": "device-011"
    }
  }
}
```

{% endraw %}

### See also
* [`GetBatteryInfoResponse`](#GetBatteryInfoResponse)

## GetBatteryInfoResponse {#GetBatteryInfoResponse}
[`GetBatteryInfoRequest`](#GetBatteryInfoRequest) 메시지에 대한 응답으로 대상 기기의 배터리 정보를 CEK에게 전달합니다.

| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|:---------:|
| `applianceResponseTimestamp` | string | 기기에서 요청한 정보를 확인한 시간(Timestamp, <a href="https://en.wikipedia.org/wiki/ISO_8601" target="_blank">ISO 8601</a>)     | 선택    |
| `batteryInfo`                 | [BatteryInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#BatteryInfoObject) | 현재 기기의 배터리 정보를 담고 있는 객체   | 필수    |

### Message example

{% raw %}

```json
{
  "header": {
    "messageId": "33da6561-0149-4532-a30b-e0de8f75c4cf",
    "name": "GetBatteryInfoResponse",
    "namespace": "ClovaHome",
    "payloadVersion": "1.0"
  },
  "payload": {
    "batteryInfo": {
        "value": 50
    },
    "applianceResponseTimestamp": "2017-11-23T20:30:19+09:00"
  }
}
```

{% endraw %}

### See also
* [`GetBatteryInfoRequest`](#GetBatteryInfoRequest)

## GetBatteryInfoRequest {#GetBatteryInfoRequest}
주로 로봇청소기와 같이 무선 동작하는 기기의 내장 배터리 정보를 확인할 때 사용되며, 대상 기기의 현재 배터리 정보를 Clova Home extension에게 요청합니다. 이 요청에 대한 응답으로 [`GetBatteryInfoResponse`](#GetBatteryInfoResponse) 메시지를 사용해야 합니다.

| 필드 이름       | 자료형    | 필드 설명                     | 포함 여부 |
|---------------|---------|-----------------------------|:---------:|
| `accessToken`      | string                                  | IoT 서비스의 사용자 계정의 access token. CEK는 외부 서비스의 인증 서버로부터 획득한 사용자 계정의 access token을 전달합니다. 자세한 설명은 [사용자 계정 연결하기](/CEK/Guides/Link_User_Account.md)를 참조합니다.                          | 항상    |
| `appliance`        | [ApplianceInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#ApplianceInfoObject)     | 대상 기기 정보를 담고 있는 객체. `applianceId` 필드는 필수입니다.     | 항상    |

### Message example

{% raw %}

```json
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
      "applianceId": "device-011"
    }
  }
}
```

{% endraw %}

### See also
* [`GetBatteryInfoResponse`](#GetBatteryInfoResponse)

## GetBatteryInfoResponse {#GetBatteryInfoResponse}
[`GetBatteryInfoRequest`](#GetBatteryInfoRequest) 메시지에 대한 응답으로 대상 기기의 배터리 정보를 CEK에게 전달합니다.

| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|:---------:|
| `applianceResponseTimestamp` | string | 기기에서 요청한 정보를 확인한 시간(Timestamp, <a href="https://en.wikipedia.org/wiki/ISO_8601" target="_blank">ISO 8601</a>)     | 선택    |
| `batteryInfo`                 | [BatteryInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#BatteryInfoObject) | 현재 기기의 배터리 정보를 담고 있는 객체   | 필수    |

### Message example

{% raw %}

```json
{
  "header": {
    "messageId": "33da6561-0149-4532-a30b-e0de8f75c4cf",
    "name": "GetBatteryInfoResponse",
    "namespace": "ClovaHome",
    "payloadVersion": "1.0"
  },
  "payload": {
    "batteryInfo": {
        "value": 50
    },
    "applianceResponseTimestamp": "2017-11-23T20:30:19+09:00"
  }
}
```

{% endraw %}

### See also
* [`GetBatteryInfoRequest`](#GetBatteryInfoRequest)

## GetCleaningCycleRequest {#GetCleaningCycleRequest}
기기의 세척 주기를 확인할 때 사용되며, 대상 기기의 다음 세척 주기까지 남은 시간에 대한 정보를 Clova Home extension에게 요청합니다. 이 요청에 대한 응답으로 [`GetCleaningCycleResponse`](#GetCleaningCycleResponse) 메시지를 사용해야 합니다.

| 필드 이름       | 자료형    | 필드 설명                     | 포함 여부 |
|---------------|---------|-----------------------------|:---------:|
| `accessToken`      | string                                  | IoT 서비스의 사용자 계정의 access token. CEK는 외부 서비스의 인증 서버로부터 획득한 사용자 계정의 access token을 전달합니다. 자세한 설명은 [사용자 계정 연결하기](/CEK/Guides/Link_User_Account.md)를 참조합니다.                          | 항상    |
| `appliance`        | [ApplianceInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#ApplianceInfoObject)     | 대상 기기 정보를 담고 있는 객체. `applianceId` 필드는 필수입니다.     | 항상    |

### Message example

{% raw %}

```json
{
  "header": {
    "messageId": "9a1a7237-f1c0-44f8-b4db-2a2abb1f0e1c",
    "name": "GetCleaningCycleRequest",
    "namespace": "ClovaHome",
    "payloadVersion": "1.0"
  },
  "payload": {
    "accessToken": "92ebcb67fe33",
    "appliance": {
      "applianceId": "device-045"
    }
  }
}
```

{% endraw %}

### See also
* [`GetCleaningCycleResponse`](#GetCleaningCycleResponse)

## GetCleaningCycleResponse {#GetCleaningCycleResponse}

[`GetCleaningCycleRequest`](#GetCleaningCycleRequest) 메시지에 대한 응답으로 대상 기기의 다음 세척 주기까지 남은 시간을 CEK에게 전달합니다.

| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|:---------:|
| `applianceResponseTimestamp` | string | 기기에서 요청한 정보를 확인한 시간(Timestamp, <a href="https://en.wikipedia.org/wiki/ISO_8601" target="_blank">ISO 8601</a>)     | 선택    |
| `remainingTime`              | string | 세척 필요 시점까지 남은 시간(Duration, <a href="https://en.wikipedia.org/wiki/ISO_8601#Durations" target="_blank">ISO 8601</a>)    | 필수    |

### Message example

{% raw %}

```json
{
  "header": {
    "messageId": "b502dd42-b698-4d3b-9ddb-bbdda70f254f",
    "name": "GetCleaningCycleResponse",
    "namespace": "ClovaHome",
    "payloadVersion": "1.0"
  },
  "payload": {
    "remainingTime": "PT8H40M",
    "applianceResponseTimestamp": "2017-11-23T20:30:19+09:00"
  }
}
```

{% endraw %}

### See also
* [`GetCleaningCycleRequest`](#GetGetCleaningCycleRequest)

## GetCloseTimeRequest {#GetCloseTimeRequest}
주로 열림 감지 센서가 감지한 내용 중 감지 대상이 마지막으로 닫혔던 시점의 시간 정보를 Clova Home extension에게 요청합니다. 이 요청에 대한 응답으로 [`GetCloseTimeResponse`](#GetCloseTimeResponse) 메시지를 사용해야 합니다.

| 필드 이름       | 자료형    | 필드 설명                     | 포함 여부 |
|---------------|---------|-----------------------------|:---------:|
| `accessToken`      | string                                  | IoT 서비스의 사용자 계정의 access token. CEK는 외부 서비스의 인증 서버로부터 획득한 사용자 계정의 access token을 전달합니다. 자세한 설명은 [사용자 계정 연결하기](/CEK/Guides/Link_User_Account.md)를 참조합니다.                          | 항상    |
| `appliance`        | [ApplianceInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#ApplianceInfoObject)     | 대상 기기 정보를 담고 있는 객체. `applianceId` 필드는 필수입니다.     | 항상    |

### Message example

{% raw %}

```json
{
  "header": {
    "messageId": "59a3f5bc-4c38-4d4c-9b71-3a037bf9f9b0",
    "name": "GetCloseTimeRequest",
    "namespace": "ClovaHome",
    "payloadVersion": "1.0"
  },
  "payload": {
    "accessToken": "92ebcb67fe33",
    "appliance": {
      "applianceId": "device-025"
    }
  }
}
```

{% endraw %}

### See also
* [`GetCloseTimeResponse`](#GetCloseTimeResponse)

## GetCloseTimeResponse {#GetCloseTimeResponse}

[`GetCloseTimeRequest`](#GetCloseTimeRequest) 메시지에 대한 응답으로 대상 기기가 감지한 내용 중 감지 대상이 마지막으로 닫혔던 시점의 시간 정보를 CEK에게 전달합니다.

| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|:---------:|
| `applianceResponseTimestamp` | string | 기기에서 요청한 정보를 확인한 시간(Timestamp, <a href="https://en.wikipedia.org/wiki/ISO_8601" target="_blank">ISO 8601</a>)     | 선택    |
| `closeTimestamp`             | string | 감지 대상이 마지막으로 닫혔던 시간(Timestamp, <a href="https://en.wikipedia.org/wiki/ISO_8601" target="_blank">ISO 8601</a>)     | 필수    |

### Message example

{% raw %}

```json
{
  "header": {
    "messageId": "b502dd42-b698-4d3b-9ddb-bbdda70f254f",
    "name": "GetCloseTimeResponse",
    "namespace": "ClovaHome",
    "payloadVersion": "1.0"
  },
  "payload": {
    "closeTimestamp": "2018-03-13T23:17:50+09:00",
    "applianceResponseTimestamp": "2017-11-23T20:30:19+09:00"
  }
}
```

{% endraw %}

### See also
* [`GetCloseTimeRequest`](#GetCloseTimeRequest)

## GetConsumptionRequest {#GetConsumptionRequest}
주로 스마트 플러그나 스마트 멀티탭과 같은 기기에서 현재까지 측정된 에너지 또는 자원을 확인할 때 사용되며, 대상 기기가 측정한 에너지 또는 자원 정보를 Clova Home extension에게 요청합니다. 이 요청에 대한 응답으로 [`GetConsumptionResponse`](#GetConsumptionResponse) 메시지를 사용해야 합니다.

| 필드 이름       | 자료형    | 필드 설명                     | 포함 여부 |
|---------------|---------|-----------------------------|:---------:|
| `accessToken`      | string                                  | IoT 서비스의 사용자 계정의 access token. CEK는 외부 서비스의 인증 서버로부터 획득한 사용자 계정의 access token을 전달합니다. 자세한 설명은 [사용자 계정 연결하기](/CEK/Guides/Link_User_Account.md)를 참조합니다.                          | 항상    |
| `appliance`        | [ApplianceInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#ApplianceInfoObject)     | 대상 기기 정보를 담고 있는 객체. `applianceId` 필드는 항상 포함됩니다.     | 항상    |

### Message example

{% raw %}

```json
{
  "header": {
    "messageId": "2d8b8c3b-5905-4355-b4bb-fa359c46c308",
    "name": "GetConsumptionRequest",
    "namespace": "ClovaHome",
    "payloadVersion": "1.0"
  },
  "payload": {
    "accessToken": "92ebcb67fe33",
    "appliance": {
      "applianceId": "device-019"
    }
  }
}
```

{% endraw %}

### See also
* [`GetConsumptionResponse`](#GetConsumptionResponse)

## GetConsumptionResponse {#GetConsumptionResponse}
[`GetConsumptionRequest`](#GetConsumptionRequest) 메시지에 대한 응답으로 대상 기기가 현재까지 측정한 에너지 또는 자원 정보를 CEK에게 전달합니다.

| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|:---------:|
| `applianceResponseTimestamp` | string | 기기에서 요청한 정보를 확인한 시간(Timestamp, <a href="https://en.wikipedia.org/wiki/ISO_8601" target="_blank">ISO 8601</a>)     | 선택    |
| `consumption[]`              | [ConsumptionInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#ConsumptionInfoObject) array | 기기가 현재까지 측정한 에너지 또는 자원 정보를 담고 있는 객체   | 필수    |

### Message example

{% raw %}

```json
{
  "header": {
    "messageId": "33da6561-0149-4532-a30b-e0de8f75c4cf",
    "name": "GetConsumptionResponse",
    "namespace": "ClovaHome",
    "payloadVersion": "1.0"
  },
  "payload": {
    "consumption": [
      {
        "name": "전기사용량",
        "value": 79.7,
        "unit": "kW"
      }
    ],
    "applianceResponseTimestamp": "2017-11-23T20:30:54+09:00"
  }
}
```

{% endraw %}

### See also
* [GetConsumptionRequest](#GetConsumptionRequest)

## GetCurrentBillRequest {#GetCurrentBillRequest}
주로 스마트 플러그나 스마트 멀티탭과 같은 기기에서 측정된 현재까지의 사용량의 기반으로 요금을 확인할 때 사용되며, 대상 기기가 측정한 요금 정보를 Clova Home extension에게 요청합니다. 이 요청에 대한 응답으로 [`GetCurrentBillResponse`](#GetCurrentBillResponse) 메시지를 사용해야 합니다.

| 필드 이름       | 자료형    | 필드 설명                     | 포함 여부 |
|---------------|---------|-----------------------------|:---------:|
| `accessToken`      | string                                  | IoT 서비스의 사용자 계정의 access token. CEK는 외부 서비스의 인증 서버로부터 획득한 사용자 계정의 access token을 전달합니다. 자세한 설명은 [사용자 계정 연결하기](/CEK/Guides/Link_User_Account.md)를 참조합니다.                          | 항상    |
| `appliance`        | [ApplianceInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#ApplianceInfoObject)     | 대상 기기 정보를 담고 있는 객체. `applianceId` 필드는 항상 포함됩니다.     | 항상    |

### Message example

{% raw %}

```json
{
  "header": {
    "messageId": "2d8b8c3b-5905-4355-b4bb-fa359c46c308",
    "name": "GetCurrentBillRequest",
    "namespace": "ClovaHome",
    "payloadVersion": "1.0"
  },
  "payload": {
    "accessToken": "92ebcb67fe33",
    "appliance": {
      "applianceId": "device-019"
    }
  }
}
```

{% endraw %}

### See also
* [`GetCurrentBillResponse`](#GetCurrentBillResponse)

## GetCurrentBillResponse {#GetCurrentBillResponse}
[`GetCurrentBillRequest`](#GetCurrentBillRequest) 메시지에 대한 응답으로 대상 기기가 현재까지 측정한 요금 정보를 CEK에게 전달합니다.

| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|:---------:|
| `applianceResponseTimestamp` | string | 기기에서 요청한 정보를 확인한 시간(Timestamp, <a href="https://en.wikipedia.org/wiki/ISO_8601" target="_blank">ISO 8601</a>)     | 선택    |
| `currentBill`                 | [BillInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#BillInfoObject) | 기기가 현재까지 측정한 요금 정보를 담고 있는 객체   | 필수    |

### Message example

{% raw %}

```json
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
* [GetCurrentBillRequest](#GetCurrentBillRequest)

## GetCurrentTemperatureRequest {#GetCurrentTemperatureRequest}
주로 에어컨이나 온도 조절 장치와 같은 기기에서 측정된 현재 온도를 확인할 때 사용되며, 대상 기기가 측정한 현재 온도 정보를 Clova Home extension에게 요청합니다. 이 요청에 대한 응답으로 [`GetCurrentTemperatureResponse`](#GetCurrentTemperatureResponse) 메시지를 사용해야 합니다.

| 필드 이름       | 자료형    | 필드 설명                     | 포함 여부 |
|---------------|---------|-----------------------------|:---------:|
| `accessToken`      | string                                  | IoT 서비스의 사용자 계정의 access token. CEK는 외부 서비스의 인증 서버로부터 획득한 사용자 계정의 access token을 전달합니다. 자세한 설명은 [사용자 계정 연결하기](/CEK/Guides/Link_User_Account.md)를 참조합니다.                          | 항상    |
| `appliance`        | [ApplianceInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#ApplianceInfoObject)     | 대상 기기 정보를 담고 있는 객체. `applianceId` 필드는 필수입니다.     | 항상    |

### Message example

{% raw %}

```json
{
  "header": {
    "messageId": "3085a017-919f-4708-8748-fb68af10faba",
    "name": "GetCurrentTemperatureRequest",
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
* [`GetCurrentTemperatureResponse`](#GetCurrentTemperatureResponse)
* [`GetTargetTemperatureRequest`](#GetTargetTemperatureRequest)

## GetCurrentTemperatureResponse {#GetCurrentTemperatureResponse}
[`GetCurrentTemperatureRequest`](#GetCurrentTemperatureRequest) 메시지에 대한 응답으로 대상 기기가 측정한 현재 온도 정보를 CEK에게 전달합니다.

| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|:---------:|
| `applianceResponseTimestamp` | string | 기기에서 요청한 정보를 확인한 시간(Timestamp, <a href="https://en.wikipedia.org/wiki/ISO_8601" target="_blank">ISO 8601</a>)     | 선택    |
| `currentTemperature`          | [TemperatureInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#TemperatureInfoObject) | 대상 기기가 측정한 현재 온도 정보를 담고 있는 객체  | 필수    |

### Message example

{% raw %}

```json
{
  "header": {
    "messageId": "7eef3a17-675d-4bbd-bd8a-f379855d05ca",
    "name": "GetCurrentTemperatureResponse",
    "namespace": "ClovaHome",
    "payloadVersion": "1.0"
  },
  "payload": {
    "currentTemperature": {
        "value": 22
    },
    "applianceResponseTimestamp": "2017-11-23T20:30:32+09:00"
  }
}
```

{% endraw %}

### See also
* [`GetCurrentTemperatureRequest`](#GetCurrentTemperatureRequest)
* [`GetTargetTemperatureResponse`](#GetTargetTemperatureResponse)

## GetDeviceStateRequest {#GetDeviceStateRequest}

대상 기기가 제공하는 모든 상태 정보와 측정 정보를 확인할 때 사용됩니다. 예를 들면, 공기 청정기로부터 공기질, 습도, 미세 먼지, 초미세 먼지 정보를 각각 [`GetAirQualityRequest`](#GetAirQualityRequest), [`GetHumidityRequest`](#GetHumidityRequest), [`GetFineDustRequest`](#GetFineDustRequest), [`GetUltraFineDustRequest`](#GetUltraFineDustRequest) 메시지를 이용하여 확인할 수도 있지만 `GetDeviceStateRequest` 메시지를 이용하여 해당 정보를 한번에 확인할 수도 있습니다. 일부 측정 정보는 기간 정보가 필요한데 이경우 `period` 필드를 통해 정보가 전달됩니다. 이 요청에 대한 응답으로 [`GetDeviceStateResponse`](#GetDeviceStateResponse) 메시지를 사용해야 합니다.

| 필드 이름       | 자료형    | 필드 설명                     | 포함 여부 |
|---------------|---------|-----------------------------|:---------:|
| `accessToken`      | string                                  | IoT 서비스의 사용자 계정의 access token. CEK는 외부 서비스의 인증 서버로부터 획득한 사용자 계정의 access token을 전달합니다. 자세한 설명은 [사용자 계정 연결하기](/CEK/Guides/Link_User_Account.md)를 참조합니다.                          | 항상    |
| `appliance`        | [ApplianceInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#ApplianceInfoObject)     | 대상 기기 정보를 담고 있는 객체. `applianceId` 필드는 항상 포함됩니다.     | 항상    |
| `period`           | [PeriodInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#PeriodInfoObject)           | 기간 정보를 담고 있는 객체                                         | 조건부   |

### Message example

{% raw %}

```json
{
  "header": {
    "messageId": "6c04fc2d-64dd-41a0-9162-7cb0d4cf7c08",
    "name": "GetDeviceStateRequest",
    "namespace": "ClovaHome",
    "payloadVersion": "1.0"
  },
  "payload": {
    "accessToken": "92ebcb67fe33",
    "appliance": {
      "applianceId": "device-012"
    },
    "period": {
      "start": "2018-03-28T00:00:00+09:00",
      "end": "2018-03-28T23:59:59+09:00"
    }
  }
}
```

{% endraw %}

### See also
* [`GetDeviceStateResponse`](#GetDeviceStateResponse)

## GetDeviceStateResponse {#GetDeviceStateResponse}
[`GetDeviceStateRequest`](#GetDeviceStateRequest) 메시지에 대한 응답으로 대상 기기가 제공하는 모든 상태 정보를 CEK에게 전달합니다.

| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|:---------:|
| `applianceResponseTimestamp` | string | 기기에서 요청한 정보를 확인한 시간(Timestamp, <a href="https://en.wikipedia.org/wiki/ISO_8601" target="_blank">ISO 8601</a>)     | 선택    |
| `states[]`                   | [CustomInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#CustomInfoObject) array  | 기기가 제공하는 모든 상태 정보를 담고 있는 객체                    | 필수  |

### Message example

{% raw %}

```json
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
        "name" : "냉동실온도",
        "value" : -11,
        "unit" : "celsius"
      },
      {
        "name" : "냉장실온도",
        "value" : 2,
        "unit" : "celsius"
      },
      {
        "name" : "냉장실습도",
        "value" : 10,
        "unit" : "percentage"
      }
    ],
    "applianceResponseTimestamp": "2017-11-23T20:31:18+09:00"
  }
}
```

{% endraw %}

### See also
* [`GetDeviceStateRequest`](#GetDeviceStateRequest)

## GetEstimateBillRequest {#GetEstimateBillRequest}
주로 스마트 플러그나 스마트 멀티탭과 같은 기기에서 측정된 사용량의 기반으로 예상 요금을 확인할 때 사용되며, 대상 기기가 예측한 요금 정보를 Clova Home extension에게 요청합니다. 이 요청에 대한 응답으로 [`GetEstimateBillResponse`](#GetEstimateBillResponse) 메시지를 사용해야 합니다.

| 필드 이름       | 자료형    | 필드 설명                     | 포함 여부 |
|---------------|---------|-----------------------------|:---------:|
| `accessToken`      | string                                  | IoT 서비스의 사용자 계정의 access token. CEK는 외부 서비스의 인증 서버로부터 획득한 사용자 계정의 access token을 전달합니다. 자세한 설명은 [사용자 계정 연결하기](/CEK/Guides/Link_User_Account.md)를 참조합니다.                          | 항상    |
| `appliance`        | [ApplianceInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#ApplianceInfoObject)     | 대상 기기 정보를 담고 있는 객체. `applianceId` 필드는 항상 포함됩니다.     | 항상    |

### Message example

{% raw %}

```json
{
  "header": {
    "messageId": "eadd9f02-6bf9-47b1-b07e-12f5e39fd37e",
    "name": "GetEstimateBillRequest",
    "namespace": "ClovaHome",
    "payloadVersion": "1.0"
  },
  "payload": {
    "accessToken": "92ebcb67fe33",
    "appliance": {
      "applianceId": "device-019"
    }
  }
}
```

{% endraw %}

### See also
* [`GetEstimateBillResponse`](#GetEstimateBillResponse)

## GetEstimateBillResponse {#GetEstimateBillResponse}
[`GetEstimateBillRequest`](#GetEstimateBillRequest) 메시지에 대한 응답으로 대상 기기가 예측한 요금 정보를 CEK에게 전달합니다.

| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|:---------:|
| `applianceResponseTimestamp` | string | 기기에서 요청한 정보를 확인한 시간(Timestamp, <a href="https://en.wikipedia.org/wiki/ISO_8601" target="_blank">ISO 8601</a>)     | 선택    |
| `estimateBill`                 | [BillInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#BillInfoObject) | 기기가 예측한 요금 정보를 담고 있는 객체   | 필수    |

### Message example

{% raw %}

```json
{
  "header": {
    "messageId": "34e79706-f626-4c76-8bfb-3f4661d4aa74",
    "name": "GetEstimateBillResponse",
    "namespace": "ClovaHome",
    "payloadVersion": "1.0"
  },
  "payload": {
    "estimateBill": {
        "value": 60000,
        "currency": "KRW"
    },
    "applianceResponseTimestamp": "2017-11-23T20:30:54+09:00"
  }
}
```

{% endraw %}

### See also
* [GetEstimateBillRequest](#GetEstimateBillRequest)

## GetExpendableStateRequest {#GetExpendableStateRequest}

기기의 필터나 소모품의 사용량이나 남은 수명을 확인할 때 사용되며, 대상 기기가 보유하고 있는 소모품의 사용량이나 수명 정보를 Clova extension에게 요청합니다. 이 요청에 대한 응답으로 [`GetExpendableStateResponse`](#GetExpendableStateResponse) 메시지를 사용해야 합니다.

| 필드 이름       | 자료형    | 필드 설명                     | 포함 여부 |
|---------------|---------|-----------------------------|:---------:|
| `accessToken`      | string                                  | IoT 서비스의 사용자 계정의 access token. CEK는 외부 서비스의 인증 서버로부터 획득한 사용자 계정의 access token을 전달합니다. 자세한 설명은 [사용자 계정 연결하기](/CEK/Guides/Link_User_Account.md)를 참조합니다.                          | 항상    |
| `appliance`        | [ApplianceInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#ApplianceInfoObject)     | 대상 기기 정보를 담고 있는 객체. `applianceId` 필드는 항상 포함됩니다.     | 항상    |

### Message example

{% raw %}

```json
{
  "header": {
    "messageId": "6c04fc2d-64dd-41a0-9162-7cb0d4cf7c08",
    "name": "GetExpendableStateRequest",
    "namespace": "ClovaHome",
    "payloadVersion": "1.0"
  },
  "payload": {
    "accessToken": "92ebcb67fe33",
    "appliance": {
      "applianceId": "device-030"
    }
  }
}
```

{% endraw %}

### See also
* [`GetExpendableStateResponse`](#GetExpendableStateResponse)

## GetExpendableStateResponse {#GetExpendableStateResponse}
[`GetExpendableStateRequest`](#GetExpendableStateRequest) 메시지에 대한 응답으로 대상 기기가 제공하는 모든 소모품의 사용량이나 수명 정보를 CEK에게 전달합니다.

| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|:---------:|
| `applianceResponseTimestamp` | string | 기기에서 요청한 정보를 확인한 시간(Timestamp, <a href="https://en.wikipedia.org/wiki/ISO_8601" target="_blank">ISO 8601</a>)     | 선택    |
| `expendableInfo[]`           | [ExpendableInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#ExpendableInfoObject) array  | 기기 소모품의 사용량이나 수명 정보를 담고 있는 객체                    | 필수  |

### Message example

{% raw %}

```json
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
        "name" : "패킹",
        "remainingTime": "P0001-04-10"
      },
      {
        "name" : "1번 필터",
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
* [`GetExpendableStateRequest`](#GetExpendableStateRequest)

## GetFineDustRequest {#GetFineDustRequest}
주로 공기청정기와 같은 기기에서 측정된 미세 먼지(PM10) 정보를 확인할 때 사용되며, 대상 기기가 측정한 미세 먼지 정보를 Clova Home extension에게 요청합니다. 이 요청에 대한 응답으로 [`GetFineDustResponse`](#GetFineDustResponse) 메시지를 사용해야 합니다.

| 필드 이름       | 자료형    | 필드 설명                     | 포함 여부 |
|---------------|---------|-----------------------------|:---------:|
| `accessToken`      | string                                  | IoT 서비스의 사용자 계정의 access token. CEK는 외부 서비스의 인증 서버로부터 획득한 사용자 계정의 access token을 전달합니다. 자세한 설명은 [사용자 계정 연결하기](/CEK/Guides/Link_User_Account.md)를 참조합니다.                          | 항상    |
| `appliance`        | [ApplianceInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#ApplianceInfoObject)     | 대상 기기 정보를 담고 있는 객체. `applianceId` 필드는 항상 포함됩니다.     | 항상    |

### Message example

{% raw %}

```json
{
  "header": {
    "messageId": "6c04fc2d-64dd-41a0-9162-7cb0d4cf7c08",
    "name": "GetFineDustRequest",
    "namespace": "ClovaHome",
    "payloadVersion": "1.0"
  },
  "payload": {
    "accessToken": "92ebcb67fe33",
    "appliance": {
      "applianceId": "device-011"
    }
  }
}
```

{% endraw %}

### See also
* [`GetFineDustResponse`](#GetFineDustResponse)

## GetFineDustResponse {#GetFineDustResponse}
[`GetFineDustRequest`](#GetFineDustRequest) 메시지에 대한 응답으로 대상 기기가 측정한 미세 먼지(PM10) 정보를 CEK에게 전달합니다.

| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|:---------:|
| `applianceResponseTimestamp` | string | 기기에서 요청한 정보를 확인한 시간(Timestamp, <a href="https://en.wikipedia.org/wiki/ISO_8601" target="_blank">ISO 8601</a>)     | 선택    |
| `fineDust`                 | [FineDustInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#FineDustInfoObject) | 현재 기기가 측정한 미세 먼지 정보를 담고 있는 객체   | 필수    |

### Message example

{% raw %}

```json
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
    },
    "applianceResponseTimestamp": "2017-11-23T20:30:44+09:00"
  }
}
```

{% endraw %}

### See also
* [`GetFineDustRequest`](#GetFineDustRequest)

## GetHumidityRequest {#GetHumidityRequest}
주로 가습기와 같은 기기에서 측정된 습도 정보를 확인할 때 사용되며, 대상 기기가 측정한 습도 정보를 Clova Home extension에게 요청합니다. 이 요청에 대한 응답으로 [`GetHumidityResponse`](#GetHumidityResponse) 메시지를 사용해야 합니다.

| 필드 이름       | 자료형    | 필드 설명                     | 포함 여부 |
|---------------|---------|-----------------------------|:---------:|
| `accessToken`      | string                                  | IoT 서비스의 사용자 계정의 access token. CEK는 외부 서비스의 인증 서버로부터 획득한 사용자 계정의 access token을 전달합니다. 자세한 설명은 [사용자 계정 연결하기](/CEK/Guides/Link_User_Account.md)를 참조합니다.                          | 항상    |
| `appliance`        | [ApplianceInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#ApplianceInfoObject)     | 대상 기기 정보를 담고 있는 객체. `applianceId` 필드는 항상 포함됩니다.     | 항상    |

### Message example

{% raw %}

```json
{
  "header": {
    "messageId": "6c04fc2d-64dd-41a0-9162-7cb0d4cf7c08",
    "name": "GetHumidityRequest",
    "namespace": "ClovaHome",
    "payloadVersion": "1.0"
  },
  "payload": {
    "accessToken": "92ebcb67fe33",
    "appliance": {
      "applianceId": "device-012"
    }
  }
}
```

{% endraw %}

### See also
* [`GetHumidityResponse`](#GetHumidityResponse)

## GetHumidityResponse {#GetHumidityResponse}
[`GetHumidityRequest`](#GetHumidityRequest) 메시지에 대한 응답으로 대상 기기가 측정한 습도 정보를 CEK에게 전달합니다.

| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|:---------:|
| `applianceResponseTimestamp` | string | 기기에서 요청한 정보를 확인한 시간(Timestamp, <a href="https://en.wikipedia.org/wiki/ISO_8601" target="_blank">ISO 8601</a>)     | 선택    |
| `humidity`                 | [HumidityInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#HumidityInfoObject) | 현재 기기가 측정한 습도 정보를 담고 있는 객체   | 필수    |

### Message example

{% raw %}

```json
{
  "header": {
    "messageId": "33da6561-0149-4532-a30b-e0de8f75c4cf",
    "name": "GetHumidityResponse",
    "namespace": "ClovaHome",
    "payloadVersion": "1.0"
  },
  "payload": {
    "humidity": {
        "value": 40
    },
    "applianceResponseTimestamp": "2017-11-23T20:30:54+09:00"
  }
}
```

{% endraw %}

### See also
* [GetHumidityRequest](#GetHumidityRequest)

## GetKeepWarmTimeRequest {#GetKeepWarmTimeRequest}
밥솥과 같은 기기에서 음식의 보온에 사용된 시간을 확인할 때 사용되며, 대상 기기가 보온 모드를 유지한 시간 정보를 Clova Home extension에게 요청합니다. 이 요청에 대한 응답으로 [`GetKeepWarmTimeResponse`](#GetKeepWarmTimeResponse) 메시지를 사용해야 합니다.

| 필드 이름       | 자료형    | 필드 설명                     | 포함 여부 |
|---------------|---------|-----------------------------|:---------:|
| `accessToken`      | string                                  | IoT 서비스의 사용자 계정의 access token. CEK는 외부 서비스의 인증 서버로부터 획득한 사용자 계정의 access token을 전달합니다. 자세한 설명은 [사용자 계정 연결하기](/CEK/Guides/Link_User_Account.md)를 참조합니다.                          | 항상    |
| `appliance`        | [ApplianceInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#ApplianceInfoObject)     | 대상 기기 정보를 담고 있는 객체. `applianceId` 필드는 필수입니다.     | 항상    |

### Message example

{% raw %}

```json
{
  "header": {
    "messageId": "59a3f5bc-4c38-4d4c-9b71-3a037bf9f9b0",
    "name": "GetKeepWarmTimeRequest",
    "namespace": "ClovaHome",
    "payloadVersion": "1.0"
  },
  "payload": {
    "accessToken": "92ebcb67fe33",
    "appliance": {
      "applianceId": "device-029"
    }
  }
}
```

{% endraw %}

### See also
* [`GetKeepWarmTimeResponse`](#GetKeepWarmTimeResponse)

## GetKeepWarmTimeResponse {#GetKeepWarmTimeResponse}

[`GetKeepWarmTimeRequest`](#GetKeepWarmTimeRequest) 메시지에 대한 응답으로 대상 기기가 보온 모드를 유지한 시간 정보를 CEK에게 전달합니다.

| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|:---------:|
| `applianceResponseTimestamp` | string | 기기에서 요청한 정보를 확인한 시간(Timestamp, <a href="https://en.wikipedia.org/wiki/ISO_8601" target="_blank">ISO 8601</a>)        | 선택    |
| `keepWarmTime`               | string | 보온 모드를 유지한 시간(Duration, <a href="https://en.wikipedia.org/wiki/ISO_8601#Durations" target="_blank">ISO 8601</a>)       | 필수    |

### Message example

{% raw %}

```json
{
  "header": {
    "messageId": "b502dd42-b698-4d3b-9ddb-bbdda70f254f",
    "name": "GetKeepWarmTimeResponse",
    "namespace": "ClovaHome",
    "payloadVersion": "1.0"
  },
  "payload": {
    "keepWarmTime": "PT5H00M",
    "applianceResponseTimestamp": "2017-11-23T20:30:19+09:00"
  }
}
```

{% endraw %}

### See also
* [`GetKeepWarmTimeRequest`](#GetKeepWarmTimeRequest)

## GetLockStateRequest {#GetLockStateRequest}
주로 스마트 밸브와 같은 기기의 상태를 확인할 때 사용되며, 대상 기기가 가진 잠금 장치의 현재 잠금 상태 정보를 Clova Home extension에게 요청합니다. 이 요청에 대한 응답으로 [`GetLockStateResponse`](#GetLockStateResponse) 메시지를 사용해야 합니다.

| 필드 이름       | 자료형    | 필드 설명                     | 포함 여부 |
|---------------|---------|-----------------------------|:---------:|
| `accessToken`      | string                                  | IoT 서비스의 사용자 계정의 access token. CEK는 외부 서비스의 인증 서버로부터 획득한 사용자 계정의 access token을 전달합니다. 자세한 설명은 [사용자 계정 연결하기](/CEK/Guides/Link_User_Account.md)를 참조합니다.                          | 항상    |
| `appliance`        | [ApplianceInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#ApplianceInfoObject)     | 대상 기기 정보를 담고 있는 객체. `applianceId` 필드는 항상 포함됩니다.     | 항상    |

### Message example

{% raw %}

```json
{
  "header": {
    "messageId": "6c04fc2d-64dd-41a0-9162-7cb0d4cf7c08",
    "name": "GetLockStateRequest",
    "namespace": "ClovaHome",
    "payloadVersion": "1.0"
  },
  "payload": {
    "accessToken": "92ebcb67fe33",
    "appliance": {
      "applianceId": "device-012"
    }
  }
}
```

{% endraw %}

### See also
* [`GetLockStateResponse`](#GetLockStateResponse)

## GetLockStateResponse {#GetLockStateResponse}
[`GetLockStateRequest`](#GetLockStateRequest) 메시지에 대한 응답으로 대상 기기가 가진 잠금 장치의 현재 잠금 상태를 CEK에게 전달합니다.

| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|:---------:|
| `applianceResponseTimestamp` | string | 기기에서 요청한 정보를 확인한 시간(Timestamp, <a href="https://en.wikipedia.org/wiki/ISO_8601" target="_blank">ISO 8601</a>)     | 선택    |
| `lockState`                  | string | 기기 잠금 장치의 잠금 상태. 다음과 같은 값을 가집니다. <ul><li><code>"LOCKED"</code>: 잠금 장치가 잠긴 상태</li><li><code>"UNLOCKED"</code>: 잠금 장치가 잠기지 않은 상태</li></ul> | 필수    |


### Message example

{% raw %}

```json
{
  "header": {
    "messageId": "33da6561-0149-4532-a30b-e0de8f75c4cf",
    "name": "GetLockStateResponse",
    "namespace": "ClovaHome",
    "payloadVersion": "1.0"
  },
  "payload": {
    "lockState": "LOCKED",
    "applianceResponseTimestamp": "2017-11-23T20:31:08+09:00"
  }
}
```

{% endraw %}

### See also
* [`GetLockStateRequest`](#GetLockStateRequest)

## GetOpenStateRequest {#GetOpenStateRequest}
주로 열림 감지 센서가 감지한 내용 중 감지 대상의 현재 상태 정보(열림 또는 닫힘)를 Clova Home extension에게 요청합니다. 이 요청에 대한 응답으로 [`GetOpenStateResponse`](#GetOpenStateResponse) 메시지를 사용해야 합니다.

| 필드 이름       | 자료형    | 필드 설명                     | 포함 여부 |
|---------------|---------|-----------------------------|:---------:|
| `accessToken`      | string                                  | IoT 서비스의 사용자 계정의 access token. CEK는 외부 서비스의 인증 서버로부터 획득한 사용자 계정의 access token을 전달합니다. 자세한 설명은 [사용자 계정 연결하기](/CEK/Guides/Link_User_Account.md)를 참조합니다.                          | 항상    |
| `appliance`        | [ApplianceInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#ApplianceInfoObject)     | 대상 기기 정보를 담고 있는 객체. `applianceId` 필드는 항상 포함됩니다.     | 항상    |

### Message example

{% raw %}

```json
{
  "header": {
    "messageId": "6c04fc2d-64dd-41a0-9162-7cb0d4cf7c08",
    "name": "GetOpenStateRequest",
    "namespace": "ClovaHome",
    "payloadVersion": "1.0"
  },
  "payload": {
    "accessToken": "92ebcb67fe33",
    "appliance": {
      "applianceId": "device-012"
    }
  }
}
```

{% endraw %}

### See also
* [`GetOpenStateResponse`](#GetOpenStateResponse)

## GetOpenStateResponse {#GetOpenStateResponse}
[`GetOpenStateRequest`](#GetOpenStateRequest) 메시지에 대한 응답으로 주로 감지 대상의 현재 상태 정보(열림 또는 닫힘)를 CEK에게 전달합니다.

| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|:---------:|
| `applianceResponseTimestamp` | string | 기기에서 요청한 정보를 확인한 시간(Timestamp, <a href="https://en.wikipedia.org/wiki/ISO_8601" target="_blank">ISO 8601</a>)     | 선택    |
| `openState`                  | string | 커버나 문, 창문 따위를 감지한 상태 정보.<ul><li><code>"CLOSED"</code>: 커버나 문, 창문 따위가 닫힌 상태</li><li><code>"OPENED"</code>: 커버나 문, 창문 따위가 열린 상태</li></ul> | 필수    |


### Message example

{% raw %}

```json
{
  "header": {
    "messageId": "33da6561-0149-4532-a30b-e0de8f75c4cf",
    "name": "GetOpenStateResponse",
    "namespace": "ClovaHome",
    "payloadVersion": "1.0"
  },
  "payload": {
    "OpenState": "LOCKED",
    "applianceResponseTimestamp": "2017-11-23T20:31:08+09:00"
  }
}
```

{% endraw %}

### See also
* [`GetOpenStateRequest`](#GetOpenStateRequest)

## GetOpenTimeRequest {#GetOpenTimeRequest}
주로 열림 감지 센서가 감지한 내용 중 감지 대상이 마지막으로 열렸던 시점의 시간 정보를 Clova Home extension에게 요청합니다. 이 요청에 대한 응답으로 [`GetOpenTimeResponse`](#GetOpenTimeResponse) 메시지를 사용해야 합니다.

| 필드 이름       | 자료형    | 필드 설명                     | 포함 여부 |
|---------------|---------|-----------------------------|:---------:|
| `accessToken`      | string                                  | IoT 서비스의 사용자 계정의 access token. CEK는 외부 서비스의 인증 서버로부터 획득한 사용자 계정의 access token을 전달합니다. 자세한 설명은 [사용자 계정 연결하기](/CEK/Guides/Link_User_Account.md)를 참조합니다.                          | 항상    |
| `appliance`        | [ApplianceInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#ApplianceInfoObject)     | 대상 기기 정보를 담고 있는 객체. `applianceId` 필드는 필수입니다.     | 항상    |

### Message example

{% raw %}

```json
{
  "header": {
    "messageId": "59a3f5bc-4c38-4d4c-9b71-3a037bf9f9b0",
    "name": "GetOpenTimeRequest",
    "namespace": "ClovaHome",
    "payloadVersion": "1.0"
  },
  "payload": {
    "accessToken": "92ebcb67fe33",
    "appliance": {
      "applianceId": "device-025"
    }
  }
}
```

{% endraw %}

### See also
* [`GetOpenTimeResponse`](#GetOpenTimeResponse)

## GetOpenTimeResponse {#GetOpenTimeResponse}

[`GetOpenTimeRequest`](#GetOpenTimeRequest) 메시지에 대한 응답으로 대상 기기가 감지한 내용 중 감지 대상이 마지막으로 열렸던 시점의 시간 정보를 CEK에게 전달합니다.

| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|:---------:|
| `applianceResponseTimestamp` | string | 기기에서 요청한 정보를 확인한 시간(Timestamp, <a href="https://en.wikipedia.org/wiki/ISO_8601" target="_blank">ISO 8601</a>)     | 선택    |
| `openTimestamp`              | string | 감지 대상이 마지막으로 열렸던 시간(Timestamp, <a href="https://en.wikipedia.org/wiki/ISO_8601" target="_blank">ISO 8601</a>)     | 필수    |

### Message example

{% raw %}

```json
{
  "header": {
    "messageId": "b502dd42-b698-4d3b-9ddb-bbdda70f254f",
    "name": "GetOpenTimeResponse",
    "namespace": "ClovaHome",
    "payloadVersion": "1.0"
  },
  "payload": {
    "openTimestamp": "2018-03-13T23:20:15+09:00",
    "applianceResponseTimestamp": "2017-11-23T20:30:19+09:00"
  }
}
```

{% endraw %}

### See also
* [`GetOpenTimeRequest`](#GetOpenTimeRequest)

## GetPhaseRequest {#GetPhaseRequest}
주로 밥솥이나 세탁기와 같이 동작 단계가 있는 기기에서 현재 동작 단계 정보를 확인할 때 사용되며, 대상 기기의 현재 동작 단계 정보를 Clova Home extension에게 요청합니다. 이 요청에 대한 응답으로 [`GetPhaseResponse`](#GetPhaseResponse) 메시지를 사용해야 합니다.

| 필드 이름       | 자료형    | 필드 설명                     | 포함 여부 |
|---------------|---------|-----------------------------|:---------:|
| `accessToken`      | string                                  | IoT 서비스의 사용자 계정의 access token. CEK는 외부 서비스의 인증 서버로부터 획득한 사용자 계정의 access token을 전달합니다. 자세한 설명은 [사용자 계정 연결하기](/CEK/Guides/Link_User_Account.md)를 참조합니다.                          | 항상    |
| `appliance`        | [ApplianceInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#ApplianceInfoObject)     | 대상 기기 정보를 담고 있는 객체. `applianceId` 필드는 필수입니다.     | 항상    |

### Message example

{% raw %}

```json
{
  "header": {
    "messageId": "0e25429d-b7c2-4588-aa85-3c46168e8776",
    "name": "GetPhaseRequest",
    "namespace": "ClovaHome",
    "payloadVersion": "1.0"
  },
  "payload": {
    "accessToken": "92ebcb67fe33",
    "appliance": {
      "applianceId": "device-017"
    }
  }
}
```

{% endraw %}

### See also
* [`GetPhaseResponse`](#GetPhaseResponse)

## GetPhaseResponse {#GetPhaseResponse}
[`GetPhaseRequest`](#GetPhaseRequest) 메시지에 대한 응답으로 대상 기기의 현재 동작 단계 정보를 CEK에게 전달합니다.

| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|:---------:|
| `applianceResponseTimestamp` | string | 기기에서 요청한 정보를 확인한 시간(Timestamp, <a href="https://en.wikipedia.org/wiki/ISO_8601" target="_blank">ISO 8601</a>)     | 선택    |
| `phase`                 | [PhaseInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#PhaseInfoObject) | 기기의 현재 동작 단계 정보를 담고 있는 객체   | 필수    |

### Message example

{% raw %}

```json
{
  "header": {
    "messageId": "b502dd42-b698-4d3b-9ddb-bbdda70f254f",
    "name": "GetPhaseResponse",
    "namespace": "ClovaHome",
    "payloadVersion": "1.0"
  },
  "payload": {
    "phase": {
        "value": "wash",
    },
    "applianceResponseTimestamp": "2017-11-23T20:30:19+09:00"
  }
}
```

{% endraw %}

### See also
* [`GetPhaseRequest`](#GetPhaseRequest)

## GetProgressiveTaxBracketRequest {#GetProgressiveTaxBracketRequest}
주로 전기 계량기나 스마트 플러그와 같은 기기에서 누진세 단계를 확인할 때 사용되며, 대상 기기가 판단한 누진세 단계 정보를 Clova Home extension에게 요청합니다. 이 요청에 대한 응답으로 [`GetProgressiveTaxBracketResponse`](#GetProgressiveTaxBracketResponse) 메시지를 사용해야 합니다.

| 필드 이름       | 자료형    | 필드 설명                     | 포함 여부 |
|---------------|---------|-----------------------------|:---------:|
| `accessToken`      | string                                  | IoT 서비스의 사용자 계정의 access token. CEK는 외부 서비스의 인증 서버로부터 획득한 사용자 계정의 access token을 전달합니다. 자세한 설명은 [사용자 계정 연결하기](/CEK/Guides/Link_User_Account.md)를 참조합니다.                          | 항상    |
| `appliance`        | [ApplianceInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#ApplianceInfoObject)     | 대상 기기 정보를 담고 있는 객체. `applianceId` 필드는 필수입니다.     | 항상    |

### Message example

{% raw %}

```json
{
  "header": {
    "messageId": "59a3f5bc-4c38-4d4c-9b71-3a037bf9f9b0",
    "name": "GetProgressiveTaxBracketRequest",
    "namespace": "ClovaHome",
    "payloadVersion": "1.0"
  },
  "payload": {
    "accessToken": "92ebcb67fe33",
    "appliance": {
      "applianceId": "device-017"
    }
  }
}
```

{% endraw %}

### See also
* [`GetProgressiveTaxBracketResponse`](#GetProgressiveTaxBracketResponse)

## GetProgressiveTaxBracketResponse {#GetProgressiveTaxBracketResponse}

[`GetProgressiveTaxBracketRequest`](#GetProgressiveTaxBracketRequest) 메시지에 대한 응답으로 대상 기기가 판단한 누진세 단계 정보를 CEK에게 전달합니다.

| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|:---------:|
| `applianceResponseTimestamp` | string | 기기에서 요청한 정보를 확인한 시간(Timestamp, <a href="https://en.wikipedia.org/wiki/ISO_8601" target="_blank">ISO 8601</a>)     | 선택    |
| `progressiveTaxBracket`      | [ProgressiveTaxBracketInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#ProgressiveTaxBracketInfoObject) | 누진세 단계 정보를 가지는 객체  | 필수    |

### Message example

{% raw %}

```json
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
* [`GetProgressiveTaxBracketRequest`](#GetProgressiveTaxBracketRequest)

## GetRemainingTimeRequest {#GetRemainingTimeRequest}
주로 밥솥이나 세탁기와 같은 기기에서 동작 종료까지 남은 시간을 확인할 때 사용되며, 대상 기기의 동작 종료까지 남은 시간에 대한 정보를 Clova Home extension에게 요청합니다. 이 요청에 대한 응답으로 [`GetRemainingTimeResponse`](#GetRemainingTimeResponse) 메시지를 사용해야 합니다.

| 필드 이름       | 자료형    | 필드 설명                     | 포함 여부 |
|---------------|---------|-----------------------------|:---------:|
| `accessToken`      | string                                  | IoT 서비스의 사용자 계정의 access token. CEK는 외부 서비스의 인증 서버로부터 획득한 사용자 계정의 access token을 전달합니다. 자세한 설명은 [사용자 계정 연결하기](/CEK/Guides/Link_User_Account.md)를 참조합니다.                          | 항상    |
| `appliance`        | [ApplianceInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#ApplianceInfoObject)     | 대상 기기 정보를 담고 있는 객체. `applianceId` 필드는 필수입니다.     | 항상    |

### Message example

{% raw %}

```json
{
  "header": {
    "messageId": "59a3f5bc-4c38-4d4c-9b71-3a037bf9f9b0",
    "name": "GetRemainingTimeRequest",
    "namespace": "ClovaHome",
    "payloadVersion": "1.0"
  },
  "payload": {
    "accessToken": "92ebcb67fe33",
    "appliance": {
      "applianceId": "device-017"
    }
  }
}
```

{% endraw %}

### See also
* [`GetRemainingTimeResponse`](#GetRemainingTimeResponse)

## GetRemainingTimeResponse {#GetRemainingTimeResponse}

[`GetRemainingTimeRequest`](#GetRemainingTimeRequest) 메시지에 대한 응답으로 대상 기기가 동작 종료하기까지 남은 시간을 CEK에게 전달합니다.

| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|:---------:|
| `applianceResponseTimestamp` | string | 기기에서 요청한 정보를 확인한 시간(Timestamp, <a href="https://en.wikipedia.org/wiki/ISO_8601" target="_blank">ISO 8601</a>)     | 선택    |
| `remainingTime`              | string | 동작 종료까지 남은 시간(Duration, <a href="https://en.wikipedia.org/wiki/ISO_8601#Durations" target="_blank">ISO 8601</a>)    | 필수    |

### Message example

{% raw %}

```json
{
  "header": {
    "messageId": "b502dd42-b698-4d3b-9ddb-bbdda70f254f",
    "name": "GetRemainingTimeResponse",
    "namespace": "ClovaHome",
    "payloadVersion": "1.0"
  },
  "payload": {
    "remainingTime": "PT8H40M",
    "applianceResponseTimestamp": "2017-11-23T20:30:19+09:00"
  }
}
```

{% endraw %}

### See also
* [`GetRemainingTimeRequest`](#GetRemainingTimeRequest)

## GetRightPostureRatioRequest {#GetRightPostureRatioRequest}
사용자가 바른 자세로 대상 기기를 사용한 비율이 얼마인지 확인할 때 사용하며, 사용자가 대상 기기를 사용할 때 특정 기간이나 현재까지 바른 자세를 유지한 비율 정보를 Clova Home extension에게 요청합니다. 이 요청에 대한 응답으로 [`GetRightPostureRatioResponse`](#GetRightPostureRatioResponse) 메시지를 사용해야 합니다.

| 필드 이름       | 자료형    | 필드 설명                     | 포함 여부 |
|---------------|---------|-----------------------------|:---------:|
| `accessToken`      | string                                  | IoT 서비스의 사용자 계정의 access token. CEK는 외부 서비스의 인증 서버로부터 획득한 사용자 계정의 access token을 전달합니다. 자세한 설명은 [사용자 계정 연결하기](/CEK/Guides/Link_User_Account.md)를 참조합니다.                          | 항상    |
| `appliance`        | [ApplianceInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#ApplianceInfoObject)     | 대상 기기 정보를 담고 있는 객체. `applianceId` 필드는 필수입니다.     | 항상    |
| `period`           | [PeriodInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#PeriodInfoObject)           | 기간 정보를 담고 있는 객체                                     | 항상   |

### Message example

{% raw %}

```json
{
  "header": {
    "messageId": "59a3f5bc-4c38-4d4c-9b71-3a037bf9f9b0",
    "name": "GetRightPostureRatioRequest",
    "namespace": "ClovaHome",
    "payloadVersion": "1.0"
  },
  "payload": {
    "accessToken": "92ebcb67fe33",
    "appliance": {
      "applianceId": "device-028"
    },
    "period": {
      "start": "2018-03-28T00:00:00+09:00",
      "end": "2018-03-28T23:59:59+09:00"
    }
  }
}
```

{% endraw %}

### See also
* [`GetRightPostureRatioResponse`](#GetRightPostureRatioResponse)

## GetRightPostureRatioResponse {#GetRightPostureRatioResponse}

[`GetRightPostureRatioRequest`](#GetRightPostureRatioRequest) 메시지에 대한 응답으로 사용자가 대상 기기를 바른 자세로 사용한 비율 정보를 CEK에게 전달합니다.

| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|:---------:|
| `applianceResponseTimestamp` | string | 기기에서 요청한 정보를 확인한 시간(Timestamp, <a href="https://en.wikipedia.org/wiki/ISO_8601" target="_blank">ISO 8601</a>)     | 선택    |
| `rightPostureRatio`          | [RatioInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#RatioInfoObject) | 사용자가 대상 기기르 바른 자세로 사용한 비율 정보를 가지는 객체   | 필수    |

### Message example

{% raw %}

```json
{
  "header": {
    "messageId": "b502dd42-b698-4d3b-9ddb-bbdda70f254f",
    "name": "GetRightPostureRatioResponse",
    "namespace": "ClovaHome",
    "payloadVersion": "1.0"
  },
  "payload": {
    "rightPostureRatio": {
      "value": 80
    },
    "applianceResponseTimestamp": "2017-11-23T20:30:19+09:00"
  }
}
```

{% endraw %}

### See also
* [`GetRightPostureRatioRequest`](#GetRightPostureRatioRequest)

## GetCurrentSittingStateRequest {#GetCurrentSittingStateRequest}
스마트 의자와 같은 기기에서 사용자의 사용 상태를 확인할 때 사용되며, 대상 기기가 사용자 착석 여부를 감지한 정보와 최근 사용자가 사용한 시간 정보를 Clova Home extension에게 요청합니다. 이 요청에 대한 응답으로 [`GetCurrentSittingStateResponse`](#GetCurrentSittingStateResponse) 메시지를 사용해야 합니다.

| 필드 이름       | 자료형    | 필드 설명                     | 포함 여부 |
|---------------|---------|-----------------------------|:---------:|
| `accessToken`      | string                                  | IoT 서비스의 사용자 계정의 access token. CEK는 외부 서비스의 인증 서버로부터 획득한 사용자 계정의 access token을 전달합니다. 자세한 설명은 [사용자 계정 연결하기](/CEK/Guides/Link_User_Account.md)를 참조합니다.                          | 항상    |
| `appliance`        | [ApplianceInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#ApplianceInfoObject)     | 대상 기기 정보를 담고 있는 객체. `applianceId` 필드는 항상 포함됩니다.     | 항상    |

### Message example

{% raw %}

```json
{
  "header": {
    "messageId": "6c04fc2d-64dd-41a0-9162-7cb0d4cf7c08",
    "name": "GetCurrentSittingStateRequest",
    "namespace": "ClovaHome",
    "payloadVersion": "1.0"
  },
  "payload": {
    "accessToken": "92ebcb67fe33",
    "appliance": {
      "applianceId": "device-032"
    }
  }
}
```

{% endraw %}

### See also
* [`GetCurrentSittingStateResponse`](#GetCurrentSittingStateResponse)

## GetCurrentSittingStateResponse {#GetCurrentSittingStateResponse}
[`GetCurrentSittingStateRequest`](#GetCurrentSittingStateRequest) 메시지에 대한 응답으로 대상 기기가 사용자 착석 여부를 감지한 정보와 최근 사용자가 사용한 시간 정보를 CEK에게 전달합니다.

| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|:---------:|
| `applianceResponseTimestamp` | string  | 기기에서 요청한 정보를 확인한 시간(Timestamp, <a href="https://en.wikipedia.org/wiki/ISO_8601" target="_blank">ISO 8601</a>)     | 선택    |
| `sittingState`               | [SittingStateInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#SittingStateInfoObject) |  스마트 의자와 같은 기기에 대한 사용자의 착석 정보가 담긴 객체              | 필수    |
| `recentlySittingPeriod`      | [PeriodInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#PeriodInfoObject) | 최근 사용 시간 정보를 담고 있는 객체              | 선택    |

### Message example

{% raw %}

```json
{
  "header": {
    "messageId": "33da6561-0149-4532-a30b-e0de8f75c4cf",
    "name": "GetCurrentSittingStateResponse",
    "namespace": "ClovaHome",
    "payloadVersion": "1.0"
  },
  "payload": {
    "sittingState": {
      "value": true
    },
    "recentlySittingPeriod": {
      "start": "2018-03-28T00:10:00+09:00",
      "end": "2018-03-28T23:59:59+09:00"
    },
    "applianceResponseTimestamp": "2018-03-29T14:32:13+09:00"
  }
}
```

{% endraw %}

### See also
* [`GetCurrentSittingStateRequest`](#GetCurrentSittingStateRequest)

## GetSleepScoreRequest {#GetSleepScoreRequest}
수면 센서와 같은 기기에서 사용자 수면 점수 정보를 확인할 때 사용되며, 대상 기기가 평가한 사용자의 수면 점수를 Clova Home extension에게 요청합니다. 이 요청에 대한 응답으로 [`GetSleepScoreResponse`](#GetSleepScoreResponse) 메시지를 사용해야 합니다.

| 필드 이름       | 자료형    | 필드 설명                     | 포함 여부 |
|---------------|---------|-----------------------------|:---------:|
| `accessToken`      | string                                  | IoT 서비스의 사용자 계정의 access token. CEK는 외부 서비스의 인증 서버로부터 획득한 사용자 계정의 access token을 전달합니다. 자세한 설명은 [사용자 계정 연결하기](/CEK/Guides/Link_User_Account.md)를 참조합니다.                          | 항상    |
| `appliance`        | [ApplianceInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#ApplianceInfoObject)     | 대상 기기 정보를 담고 있는 객체. `applianceId` 필드는 항상 포함됩니다.     | 항상    |
| `period`           | [PeriodInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#PeriodInfoObject)           | 기간 정보를 담고 있는 객체                                          | 조건부  |

### Message example

{% raw %}

```json
{
  "header": {
    "messageId": "6c04fc2d-64dd-41a0-9162-7cb0d4cf7c08",
    "name": "GetSleepScoreRequest",
    "namespace": "ClovaHome",
    "payloadVersion": "1.0"
  },
  "payload": {
    "accessToken": "92ebcb67fe33",
    "appliance": {
      "applianceId": "device-032"
    },
    "period": {
      "start": "2018-03-28T00:00:00+09:00",
      "end": "2018-03-28T23:59:59+09:00"
    }
  }
}
```

{% endraw %}

### See also
* [`GetSleepScoreResponse`](#GetSleepScoreResponse)

## GetSleepScoreResponse {#GetSleepScoreResponse}
[`GetSleepScoreRequest`](#GetSleepScoreRequest) 메시지에 대한 응답으로 대상 기기가 평가한 사용자의 수면 점수를 CEK에게 전달합니다.

| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|:---------:|
| `applianceResponseTimestamp` | string  | 기기에서 요청한 정보를 확인한 시간(Timestamp, <a href="https://en.wikipedia.org/wiki/ISO_8601" target="_blank">ISO 8601</a>)     | 선택    |
| `sleepScore`                 | [SleepScoreInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#SleepScoreInfoObject)  | 수면 점수 정보가 담긴 객체                                                       | 필수    |

### Message example

{% raw %}

```json
{
  "header": {
    "messageId": "33da6561-0149-4532-a30b-e0de8f75c4cf",
    "name": "GetSleepScoreResponse",
    "namespace": "ClovaHome",
    "payloadVersion": "1.0"
  },
  "payload": {
    "sleepScore": {
      "value": 80
    },
    "applianceResponseTimestamp": "2018-03-29T14:32:13+09:00"
  }
}
```

{% endraw %}

### See also
* [`GetSleepScoreRequest`](#GetSleepScoreRequest)

## GetSleepStartTimeRequest {#GetSleepStartTimeRequest}
수면 센서와 같은 기기에서 사용자 수면 점수 정보를 확인할 때 사용되며, 대상 기기가 측정한 사용자의 수면 시작 시간을 Clova Home extension에게 요청합니다. 이 요청에 대한 응답으로 [`GetSleepStartTimeResponse`](#GetSleepStartTimeResponse) 메시지를 사용해야 합니다.

| 필드 이름       | 자료형    | 필드 설명                     | 포함 여부 |
|---------------|---------|-----------------------------|:---------:|
| `accessToken`      | string                                  | IoT 서비스의 사용자 계정의 access token. CEK는 외부 서비스의 인증 서버로부터 획득한 사용자 계정의 access token을 전달합니다. 자세한 설명은 [사용자 계정 연결하기](/CEK/Guides/Link_User_Account.md)를 참조합니다.                          | 항상    |
| `appliance`        | [ApplianceInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#ApplianceInfoObject)     | 대상 기기 정보를 담고 있는 객체. `applianceId` 필드는 항상 포함됩니다.     | 항상    |
| `period`           | [PeriodInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#PeriodInfoObject)           | 기간 정보를 담고 있는 객체                                          | 조건부  |

### Message example

{% raw %}

```json
{
  "header": {
    "messageId": "6c04fc2d-64dd-41a0-9162-7cb0d4cf7c08",
    "name": "GetSleepStartTimeRequest",
    "namespace": "ClovaHome",
    "payloadVersion": "1.0"
  },
  "payload": {
    "accessToken": "92ebcb67fe33",
    "appliance": {
      "applianceId": "device-032"
    },
    "period": {
      "start": "2018-03-28T00:00:00+09:00",
      "end": "2018-03-28T23:59:59+09:00"
    }
  }
}
```

{% endraw %}

### See also
* [`GetSleepStartTimeResponse`](#GetSleepStartTimeResponse)

## GetSleepStartTimeResponse {#GetSleepStartTimeResponse}
[`GetSleepStartTimeRequest`](#GetSleepStartTimeRequest) 메시지에 대한 응답으로 대상 기기가 측정한 사용자의 수면 시작 시간을 CEK에게 전달합니다.

| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|:---------:|
| `applianceResponseTimestamp` | string  | 기기에서 요청한 정보를 확인한 시간(Timestamp, <a href="https://en.wikipedia.org/wiki/ISO_8601" target="_blank">ISO 8601</a>)     | 선택    |
| `startTimestampList[]`       | string  | 날짜 순서대로 수면 시작 시간을 저장하고 있는 배열                                      | 필수    |

### Message example

{% raw %}

```json
{
  "header": {
    "messageId": "33da6561-0149-4532-a30b-e0de8f75c4cf",
    "name": "GetSleepStartTimeResponse",
    "namespace": "ClovaHome",
    "payloadVersion": "1.0"
  },
  "payload": {
    "startTimestampList": [
      "2018-03-22T20:44:43+09:00",
      "2018-03-23T22:12:12+09:00",
      "2018-03-24T21:11:55+09:00"
    ],
    "applianceResponseTimestamp": "2018-03-29T14:32:13+09:00"
  }
}
```

{% endraw %}

### See also
* [`GetSleepStartTimeRequest`](#GetSleepStartTimeRequest)

## GetTargetTemperatureRequest {#GetTargetTemperatureRequest}
주로 에어컨이나 온도 조절 장치와 같은 기기에서 설정된 희망 온도를 확인할 때 사용되며, 대상 기기가 설정한 희망 온도 정보를 Clova Home extension에게 요청합니다. 이 요청에 대한 응답으로 [`GetTargetTemperatureResponse`](#GetTargetTemperatureResponse) 메시지를 사용해야 합니다.

| 필드 이름       | 자료형    | 필드 설명                     | 포함 여부 |
|---------------|---------|-----------------------------|:---------:|
| `accessToken`      | string                                  | IoT 서비스의 사용자 계정의 access token. CEK는 외부 서비스의 인증 서버로부터 획득한 사용자 계정의 access token을 전달합니다. 자세한 설명은 [사용자 계정 연결하기](/CEK/Guides/Link_User_Account.md)를 참조합니다.                          | 항상    |
| `appliance`        | [ApplianceInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#ApplianceInfoObject)     | 대상 기기 정보를 담고 있는 객체. `applianceId` 필드는 항상 포함됩니다.     | 항상    |

### Message example

{% raw %}

```json
{
  "header": {
    "messageId": "6c04fc2d-64dd-41a0-9162-7cb0d4cf7c08",
    "name": "GetTargetTemperatureRequest",
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
* [`GetTargetTemperatureResponse`](#GetTargetTemperatureResponse)

## GetTargetTemperatureResponse {#GetTargetTemperatureResponse}
[`GetTargetTemperatureRequest`](#GetTargetTemperatureRequest) 메시지에 대한 응답으로 대상 기기가 설정한 희망 온도 정보를 CEK에게 전달합니다.

| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|:---------:|
| `applianceResponseTimestamp` | string | 기기에서 요청한 정보를 확인한 시간(Timestamp, <a href="https://en.wikipedia.org/wiki/ISO_8601" target="_blank">ISO 8601</a>)     | 선택    |
| `targetTemperature`          | [TemperatureInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#TemperatureInfoObject) | 대상 기기에 설정되었거나 extension이 대상 기기에게 설정하도록 요청한 희망 온도 정보를 담고 있는 객체  | 필수    |

### Message example

{% raw %}

```json
{
  "header": {
    "messageId": "33da6561-0149-4532-a30b-e0de8f75c4cf",
    "name": "GetTargetTemperatureResponse",
    "namespace": "ClovaHome",
    "payloadVersion": "1.0"
  },
  "payload": {
    "targetTemperature": {
        "value": 24
    },
    "applianceResponseTimestamp": "2017-11-23T20:31:18+09:00"
  }
}
```

{% endraw %}

### See also
* [`GetTargetTemperatureRequest`](#GetTargetTemperatureRequest)

## GetUltraFineDustRequest {#GetUltraFineDustRequest}
주로 공기청정기와 같은 기기에서 측정된 초미세 먼지(PM2.5) 정보를 확인할 때 사용되며, 대상 기기가 측정한 초미세 먼지 정보를 Clova Home extension에게 요청합니다. 이 요청에 대한 응답으로 [`GetUltraFineDustResponse`](#GetUltraFineDustResponse) 메시지를 사용해야 합니다.

| 필드 이름       | 자료형    | 필드 설명                     | 포함 여부 |
|---------------|---------|-----------------------------|:---------:|
| `accessToken`      | string                                  | IoT 서비스의 사용자 계정의 access token. CEK는 외부 서비스의 인증 서버로부터 획득한 사용자 계정의 access token을 전달합니다. 자세한 설명은 [사용자 계정 연결하기](/CEK/Guides/Link_User_Account.md)를 참조합니다.                          | 항상    |
| `appliance`        | [ApplianceInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#ApplianceInfoObject)     | 대상 기기 정보를 담고 있는 객체. `applianceId` 필드는 항상 포함됩니다.     | 항상    |

### Message example

{% raw %}

```json
{
  "header": {
    "messageId": "6c04fc2d-64dd-41a0-9162-7cb0d4cf7c08",
    "name": "GetUltraFineDustRequest",
    "namespace": "ClovaHome",
    "payloadVersion": "1.0"
  },
  "payload": {
    "accessToken": "92ebcb67fe33",
    "appliance": {
      "applianceId": "device-011"
    }
  }
}
```

{% endraw %}

### See also
* [`GetUltraFineDustResponse`](#GetUltraFineDustResponse)

## GetUltraFineDustResponse {#GetUltraFineDustResponse}
[`GetUltraFineDustRequest`](#GetUltraFineDustRequest) 메시지에 대한 응답으로 대상 기기가 측정한 초미세 먼지(PM2.5) 정보를 CEK에게 전달합니다.

| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|:---------:|
| `applianceResponseTimestamp` | string | 기기에서 요청한 정보를 확인한 시간(Timestamp, <a href="https://en.wikipedia.org/wiki/ISO_8601" target="_blank">ISO 8601</a>)     | 선택    |
| `ultraFineDust`                 | [UltraFineDustInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#UltraFineDustInfoObject) | 현재 기기가 측정한 초미세 먼지 정보를 담고 있는 객체   | 필수    |

### Message example

{% raw %}

```json
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
    },
    "applianceResponseTimestamp": "2017-11-23T20:26:48+09:00"
  }
}
```

{% endraw %}

### See also
* [`GetUltraFineDustRequest`](#GetUltraFineDustRequest)

## GetUsageTimeRequest {#GetUsageTimeRequest}
사용자가 대상 기기를 얼마나 사용했는지 확인할 때 사용하며, 대상 기기가 특정 기간이나 현재까지 누적 사용된 시간 정보를 Clova Home extension에게 요청합니다. 이 요청에 대한 응답으로 [`GetUsageTimeResponse`](#GetUsageTimeResponse) 메시지를 사용해야 합니다.

| 필드 이름       | 자료형    | 필드 설명                     | 포함 여부 |
|---------------|---------|-----------------------------|:---------:|
| `accessToken`      | string                                  | IoT 서비스의 사용자 계정의 access token. CEK는 외부 서비스의 인증 서버로부터 획득한 사용자 계정의 access token을 전달합니다. 자세한 설명은 [사용자 계정 연결하기](/CEK/Guides/Link_User_Account.md)를 참조합니다.                          | 항상    |
| `appliance`        | [ApplianceInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#ApplianceInfoObject)     | 대상 기기 정보를 담고 있는 객체. `applianceId` 필드는 필수입니다.     | 항상    |
| `period`           | [PeriodInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#PeriodInfoObject)           | 기간 정보를 담고 있는 객체                                     | 항상   |

### Message example

{% raw %}

```json
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
      "start": "2018-03-28T00:00:00+09:00",
      "end": "2018-03-28T23:59:59+09:00"
    }
  }
}
```

{% endraw %}

### See also
* [`GetUsageTimeResponse`](#GetUsageTimeResponse)

## GetUsageTimeResponse {#GetUsageTimeResponse}

[`GetUsageTimeRequest`](#GetUsageTimeRequest) 메시지에 대한 응답으로 대상 기기가 사용된 시간 정보를 CEK에게 전달합니다.

| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|:---------:|
| `applianceResponseTimestamp` | string | 기기에서 요청한 정보를 확인한 시간(Timestamp, <a href="https://en.wikipedia.org/wiki/ISO_8601" target="_blank">ISO 8601</a>)     | 선택    |
| `usageTime`                  | string | 사용 시간(Duration, <a href="https://en.wikipedia.org/wiki/ISO_8601#Durations" target="_blank">ISO 8601</a>)               | 필수    |

### Message example

{% raw %}

```json
{
  "header": {
    "messageId": "b502dd42-b698-4d3b-9ddb-bbdda70f254f",
    "name": "GetUsageTimeResponse",
    "namespace": "ClovaHome",
    "payloadVersion": "1.0"
  },
  "payload": {
    "usageTime": "P12DT8H40M",
    "applianceResponseTimestamp": "2017-11-23T20:30:19+09:00"
  }
}
```

{% endraw %}

### See also
* [`GetUsageTimeRequest`](#GetUsageTimeRequest)

## HealthCheckRequest {#HealthCheckRequest}
지정한 기기의 상태를 파악할 때 사용되며, 대상 기기의 상태 정보를 Clova Home extension에게 요청합니다. 이 요청에 대한 응답으로 [`HealthCheckResponse`](#HealthCheckResponse) 메시지를 사용해야 합니다.

### Payload fields

| 필드 이름       | 자료형    | 필드 설명                     | 포함 여부 |
|---------------|---------|-----------------------------|:---------:|
| `accessToken`   | string  | Clova Home extension의 access token | 항상    |
| `appliance`     | [ApplianceInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#ApplianceInfoObject)     | 대상 기기 정보를 담고 있는 객체. `applianceId` 필드는 항상 포합됩니다.     | 항상    |

### Message example

{% raw %}

```json
{
  "header": {
    "messageId": "33da6561-0149-4532-a30b-e0de8f75c4cf",
    "name": "HealthCheckRequest",
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
* [`HealthCheckResponse`](#HealthCheckResponse)

## HealthCheckResponse {#HealthCheckResponse}
[`HealthCheckRequest`](#HealthCheckRequest) 메시지에 대한 응답으로 지정된 기기의 상태를 CEK에게 전달합니다.

### Payload fields

| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|:---------:|
| `isReachable` | boolean | 네트워크를 통해 대상 기기에 접근 가능한지 나타내는 값. <ul><li><code>true</code>: 접근 가능(online)</li><li><code>false</code>: 접근 불가(offline)</li></ul> | 필수    |
| `isTurnOn`    | boolean | 대상 기기의 동작 상태를 나타내는 값. <ul><li><code>true</code>: 대기 상태(idle)</li><li><code>false</code>: 동작 상태(working)</li></ul>                  | 필수    |

### Message example

{% raw %}

```json
{
  "header": {
    "messageId": "33da6561-0149-4532-a30b-e0de8f75c4cf",
    "name": "HealthCheckResponse",
    "namespace": "ClovaHome",
    "payloadVersion": "1.0"
  },
  "payload": {
    "isReachable": true,
    "isTurnOn": false
  }
}
```

{% endraw %}

### See also
* [`HealthCheckRequest`](#HealthCheckRequest)

## IncrementBrightnessConfirmation {#IncrementBrightnessConfirmation}
[`IncrementBrightnessRequest`](#IncrementBrightnessRequest) 메시지에 대한 응답으로 대상 기기가 조명 밝기를 높이도록 요청한 후 처리된 결과를 CEK에게 전달합니다.

### Payload fields

| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|:---------:|
| `brightness`               | [BrightnessInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#BrightnessInfoObject) | 현재 밝기 정보를 담고 있는 객체                                | 선택    |
| `previousState`            | object | 기기의 이전 상황 정보를 담고 있는 객체                           | 선택    |
| `previousState.brightness` | [BrightnessInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#BrightnessInfoObject) | 이전 밝기 정보를 담고 있는 객체                                | 선택    |

### Remarks

대상 기기에서 payload에 입력할 정보를 얻어올 수 없으면 값을 입력하지 않아도 됩니다. 이 경우 사용자에게 구체적인 정보 없이 기기 제어 요청이 정상 처리되었음을 알려줍니다.

### Message example

{% raw %}

```json
{
  "header": {
    "messageId": "4ec35000-88ce-4724-b7e4-7f52050558fd",
    "name": "IncrementBrightnessConfirmation",
    "namespace": "ClovaHome",
    "payloadVersion": "1.0"
  },
  "payload": {
    "brightness": {
      "value": 40
    },
    "previousState": {
      "brightness": {
        "value": 20
      }
    }
  }
}
```

{% endraw %}

### See also
* [`IncrementBrightnessRequest`](#IncrementBrightnessRequest)

## IncrementBrightnessRequest {#IncrementBrightnessRequest}
주로 조명 기기를 제어할 때 사용되며, 대상 기기가 지정한 수준만큼 조명의 밝기를 높이도록 Clova Home extension에게 요청합니다. 이 요청에 대한 응답으로 [`IncrementBrightnessConfirmation`](#IncrementBrightnessConfirmation) 메시지를 사용해야 합니다.

### Payload fields

| 필드 이름       | 자료형    | 필드 설명                     | 포함 여부 |
|---------------|---------|-----------------------------|:---------:|
| `accessToken`      | string                                  | IoT 서비스의 사용자 계정의 access token. CEK는 외부 서비스의 인증 서버로부터 획득한 사용자 계정의 access token을 전달합니다. 자세한 설명은 [사용자 계정 연결하기](/CEK/Guides/Link_User_Account.md)를 참조합니다.                          | 항상    |
| `appliance`        | [ApplianceInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#ApplianceInfoObject)     | 대상 기기 정보를 담고 있는 객체. `applianceId` 필드는 항상 포함니다.     | 항상    |
| `deltaBrightness`       | [BrightnessInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#BrightnessInfoObject)             | 변경할 밝기의 크기 정보를 담고 있는 객체                              | 항상    |

### Message example

{% raw %}

```json
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
      "value": 20
    }
  }
}
```

{% endraw %}

### See also
* [`IncrementBrightnessConfirmation`](#IncrementBrightnessConfirmation)

## IncrementChannelConfirmation {#IncrementChannelConfirmation}
[`IncrementChannelRequest`](#IncrementChannelRequest) 메시지에 대한 응답으로 대상 기기가 TV 채널을 높이도록 요청한 후 처리된 결과를 CEK에게 전달합니다.

### Payload fields

| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|:---------:|
| `channel`               | [TVChannelInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#TVChannelInfoObject) | 현재 TV 채널 정보를 담고 있는 객체                                | 선택    |
| `subChannel`            | [TVChannelInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#TVChannelInfoObject) | 현재 TV 채널의 서브 채널 정보를 가지는 객체                         | 선택    |
| `previousState`            | object | 기기의 이전 상황 정보를 담고 있는 객체                           | 선택    |
| `previousState.channel`    | [TVChannelInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#TVChannelInfoObject) | 이전 TV 채널 정보를 담고 있는 객체                                | 선택    |
| `previousState.subChannel` | [TVChannelInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#TVChannelInfoObject) | 이전 TV 채널의 서브 채널 정보를 가지는 객체                         | 선택    |

### Remarks

대상 기기에서 payload에 입력할 정보를 얻어올 수 없으면 값을 입력하지 않아도 됩니다. 이 경우 사용자에게 구체적인 정보 없이 기기 제어 요청이 정상 처리되었음을 알려줍니다.

### Message example

{% raw %}

```json
{
  "header": {
    "messageId": "4ec35000-88ce-4724-b7e4-7f52050558fd",
    "name": "IncrementChannelConfirmation",
    "namespace": "ClovaHome",
    "payloadVersion": "1.0"
  },
  "payload": {
    "channel": {
      "value": 14
    },
    "subChannel": {
      "value": 1
    }
    "previousState": {
      "channel": {
        "value": 15
      },
      "subChannel": {
        "value": 1
      }
    }
  }
}
```

{% endraw %}

### See also
* [`IncrementChannelRequest`](#IncrementChannelRequest)

## IncrementChannelRequest {#IncrementChannelRequest}
주로 TV나 셋톱박스를 제어할 때 사용되며, 대상 기기가 지정한 수준만큼 TV 채널을 높이도록 Clova Home extension에게 요청합니다. 이 요청에 대한 응답으로 [`IncrementChannelConfirmation`](#IncrementChannelConfirmation) 메시지를 사용해야 합니다.

### Payload fields

| 필드 이름       | 자료형    | 필드 설명                     | 포함 여부 |
|---------------|---------|-----------------------------|:---------:|
| `accessToken`      | string                                  | IoT 서비스의 사용자 계정의 access token. CEK는 외부 서비스의 인증 서버로부터 획득한 사용자 계정의 access token을 전달합니다. 자세한 설명은 [사용자 계정 연결하기](/CEK/Guides/Link_User_Account.md)를 참조합니다.                          | 항상    |
| `appliance`        | [ApplianceInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#ApplianceInfoObject)     | 대상 기기 정보를 담고 있는 객체. `applianceId` 필드는 필수입니다.     | 항상    |
| `deltaChannel`       | [TVChannelInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#TVChannelInfoObject)             | 변경할 TV 채널의 크기 정보를 담고 있는 객체                              | 항상    |

### Message example

{% raw %}

```json
{
  "header": {
    "messageId": "6c04fc2d-64dd-41a0-9162-7cb0d4cf7c08",
    "name": "IncrementChannelRequest",
    "namespace": "ClovaHome",
    "payloadVersion": "1.0"
  },
  "payload": {
    "accessToken": "92ebcb67fe33",
    "appliance": {
      "applianceId": "device-011"
    },
    "deltaChannel": {
      "value": 1
    }
  }
}
```

{% endraw %}

### See also
* [`IncrementChannelConfirmation`](#IncrementChannelConfirmation)

## IncrementFanSpeedConfirmation {#IncrementFanSpeedConfirmation}
[`IncrementFanSpeedRequest`](#IncrementFanSpeedRequest) 메시지에 대한 응답으로 대상 기기가 팬의 속도를 높이도록 요청한 후 처리된 결과를 CEK에게 전달합니다.

### Payload fields

| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|:---------:|
| `fanSpeed`            | [SpeedInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#SpeedInfoObject) | 현재 팬의 속도 정보를 담고 있는 객체. 팬의 속도는 풍속을 의미하며 팬 속도를 다음과 같은 값으로 제한합니다.<ul><li><code>1</code>: 약한 바람(1단)</li><li><code>2</code>: 중간 바람(2단)</li><li><code>3</code>: 강한 바람(3단)</li></ul> | 선택    |
| `previousState`          | object                      | 기기의 이전 상황 정보를 담고 있는 객체                 | 선택    |
| `previousState.FanSpeed` | [SpeedInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#SpeedInfoObject) | 이전 팬의 속도 정보를 담고 있는 객체. 팬의 속도는 풍속을 의미하며 팬 속도를 다음과 같은 값으로 제한합니다.<ul><li><code>1</code>: 약한 바람(1단)</li><li><code>2</code>: 중간 바람(2단)</li><li><code>3</code>: 강한 바람(3단)</li></ul> | 선택    |

### Remarks

대상 기기에서 payload에 입력할 정보를 얻어올 수 없으면 값을 입력하지 않아도 됩니다. 이 경우 사용자에게 구체적인 정보 없이 기기 제어 요청이 정상 처리되었음을 알려줍니다.

### Message example

{% raw %}

```json
{
  "header": {
    "messageId": "4ec35000-88ce-4724-b7e4-7f52050558fd",
    "name": "IncrementFanSpeedConfirmation",
    "namespace": "ClovaHome",
    "payloadVersion": "1.0"
  },
  "payload": {
    "fanSpeed": {
      "value": 3
    },
    "previousState": {
      "fanSpeed": {
        "value": 2
      }
    }
  }
}
```

{% endraw %}

### See also
* [`IncrementFanSpeedRequest`](#IncrementFanSpeedRequest)

## IncrementFanSpeedRequest {#IncrementFanSpeedRequest}
주로 공기청정기와 같은 기기를 제어할 때 사용되며, 대상 기기가 지정한 값만큼 팬의 속도를 높이도록 Clova Home extension에게 요청합니다. 이 요청에 대한 응답으로 [`IncrementFanSpeedConfirmation`](#IncrementFanSpeedConfirmation) 메시지를 사용해야 합니다.

### Payload fields

| 필드 이름       | 자료형    | 필드 설명                     | 포함 여부 |
|---------------|---------|-----------------------------|:---------:|
| `accessToken`      | string                                  | IoT 서비스의 사용자 계정의 access token. CEK는 외부 서비스의 인증 서버로부터 획득한 사용자 계정의 access token을 전달합니다. 자세한 설명은 [사용자 계정 연결하기](/CEK/Guides/Link_User_Account.md)를 참조합니다.                          | 항상    |
| `appliance`        | [ApplianceInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#ApplianceInfoObject)     | 대상 기기 정보를 담고 있는 객체. `applianceId` 필드는 필수입니다. | 항상    |
| `deltaFanSpeed` | [SpeedInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#SpeedInfoObject) | 변경할 속도의 크기 정보를 담고 있는 객체. 팬의 속도는 풍속을 의미하며 팬 속도를 다음과 같은 값으로 제한합니다.<ul><li><code>1</code>: 약한 바람(1단)</li><li><code>2</code>: 중간 바람(2단)</li><li><code>3</code>: 강한 바람(3단)</li></ul>  | 항상    |

### Message example

{% raw %}

```json
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
```

{% endraw %}

### See also
* [`IncrementFanSpeedConfirmation`](#IncrementFanSpeedConfirmation)

## IncrementIntensityLevelConfirmation {#IncrementIntensityLevelConfirmation}
[`DecrementIntensityLevelRequest`](#DecrementIntensityLevelRequest) 메시지에 대한 응답으로 대상 기기가 압력이나 수압 등의 세기를 높이도록 요청한 후 처리된 결과를 CEK에게 전달합니다.

### Payload fields

| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|:---------:|
| `intensityLevel` | [IntensityLevelInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#IntensityLevelInfoObject) | 현재 압력/수압 등의 세기 정보를 담고 있는 객체                  | 선택    |
| `previousState`  | object                                  | 기기의 이전 상황 정보를 담고 있는 객체                           | 선택    |
| `previousState.intensityLevel` | [IntensityLevelInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#IntensityLevelInfoObject) | 이전 압력/수압 등의 세기 정보를 담고 있는 객체    | 선택    |

### Remarks

대상 기기에서 payload에 입력할 정보를 얻어올 수 없으면 값을 입력하지 않아도 됩니다. 이 경우 사용자에게 구체적인 정보 없이 기기 제어 요청이 정상 처리되었음을 알려줍니다.

### Message example

{% raw %}

```json
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
* [`IncrementIntensityLevelRequest`](#IncrementIntensityLevelRequest)

## IncrementIntensityLevelRequest {#IncrementIntensityLevelRequest}
대상 기기가 지정한 값만큼 압력이나 수압의 세기를 높이도록 Clova Home extension에게 요청합니다. 이 요청에 대한 응답으로 [`IncrementIntensityLevelConfirmation`](#IncrementIntensityLevelConfirmation) 메시지를 사용해야 합니다.

### Payload fields

| 필드 이름       | 자료형    | 필드 설명                     | 포함 여부 |
|---------------|---------|-----------------------------|:---------:|
| `accessToken`      | string                                  | IoT 서비스의 사용자 계정의 access token. CEK는 외부 서비스의 인증 서버로부터 획득한 사용자 계정의 access token을 전달합니다. 자세한 설명은 [사용자 계정 연결하기](/CEK/Guides/Link_User_Account.md)를 참조합니다.                          | 항상    |
| `appliance`        | [ApplianceInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#ApplianceInfoObject)     | 대상 기기 정보를 담고 있는 객체. `applianceId` 필드는 필수입니다. | 항상    |
| `deltaIntensity`   | [IntensityLevelInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#IntensityLevelInfoObject) | 변경할 압력이나 수압의 세기 정보를 담고 있는 객체           | 항상    |

### Message example

{% raw %}

```json
{
  "header": {
    "messageId": "6c04fc2d-64dd-41a0-9162-7cb0d4cf7c08",
    "name": "IncrementIntensityLevelRequest",
    "namespace": "ClovaHome",
    "payloadVersion": "1.0"
  },
  "payload": {
    "accessToken": "92ebcb67fe33",
    "appliance": {
      "applianceId": "device-015"
    },
    "deltaTemperature": {
      "value": 1
    }
  }
}
```

{% endraw %}

### See also
* [`IncrementIntensityLevelConfirmation`](#IncrementIntensityLevelConfirmation)

## IncrementTargetTemperatureConfirmation {#IncrementTargetTemperatureConfirmation}
[`IncrementTargetTemperatureRequest`](#IncrementTargetTemperatureRequest) 메시지에 대한 응답으로 대상 기기가 온도를 높이도록 요청한 후 처리된 결과를 CEK에게 전달합니다.

### Payload fields

| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|:---------:|
| `previousState`     | object                                  | 기기의 이전 상황 정보를 담고 있는 객체                              | 선택    |
| `previousState.targetTemperature` | [TemperatureInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#TemperatureInfoObject) | 이전 희망 온도 정보를 담고 있는 객체                 | 선택    |
| `targetTemperature` | [TemperatureInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#TemperatureInfoObject) | 대상 기기에 설정되었거나 extension이 대상 기기에게 설정하도록 요청한 희망 온도 정보를 담고 있는 객체                               | 선택    |

### Remarks

대상 기기에서 payload에 입력할 정보를 얻어올 수 없으면 값을 입력하지 않아도 됩니다. 이 경우 사용자에게 구체적인 정보 없이 기기 제어 요청이 정상 처리되었음을 알려줍니다.

### Message example

{% raw %}

```json
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
        "value": 22
      }
    }
  }
}
```

{% endraw %}

### See also
* [`IncrementTargetTemperatureRequest`](#IncrementTargetTemperatureRequest)

## IncrementTargetTemperatureRequest {#IncrementTargetTemperatureRequest}
주로 에어컨이나 온도 조절 장치와 같은 기기를 제어할 때 사용되며, 대상 기기가 지정한 값만큼 온도를 높이도록 Clova Home extension에게 요청합니다. 이 요청에 대한 응답으로 [`IncrementTargetTemperatureConfirmation`](#IncrementTargetTemperatureConfirmation) 메시지를 사용해야 합니다.

### Payload fields

| 필드 이름       | 자료형    | 필드 설명                     | 포함 여부 |
|---------------|---------|-----------------------------|:---------:|
| `accessToken`      | string | IoT 서비스의 사용자 계정의 access token. CEK는 외부 서비스의 인증 서버로부터 획득한 사용자 계정의 access token을 전달합니다. 자세한 설명은 [사용자 계정 연결하기](/CEK/Guides/Link_User_Account.md)를 참조합니다. | 항상    |
| `appliance`        | [ApplianceInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#ApplianceInfoObject)     | 대상 기기 정보를 담고 있는 객체. `applianceId` 필드는 필수입니다. | 항상    |
| `deltaTemperature` | [TemperatureInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#TemperatureInfoObject) | 변경할 온도의 크기 정보를 담고 있는 객체                              | 항상    |

### Message example

{% raw %}

```json
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
      "value": 3
    }
  }
}
```

{% endraw %}

### See also
* [`IncrementTargetTemperatureConfirmation`](#IncrementTargetTemperatureConfirmation)

## IncrementVolumeConfirmation {#IncrementVolumeConfirmation}
[`IncrementVolumeRequest`](#IncrementVolumeRequest) 메시지에 대한 응답으로 대상 기기가 스피커 볼륨을 높이도록 요청한 후 처리된 결과를 CEK에게 전달합니다.

### Payload fields

| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|:---------:|
| `previousState`     | object                                 | 기기의 이전 상황 정보를 담고 있는 객체                              | 선택    |
| `previousState.targetVolume` | [VolumeInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#VolumeInfoObject) | 이전 볼륨 정보를 담고 있는 객체                 | 선택    |
| `targetVolume` | [VolumeInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#VolumeInfoObject)               | 대상 기기에 설정되었거나 extension이 대상 기기에게 설정하도록 요청한 볼륨 정보를 담고 있는 객체                 | 선택    |

### Message example

{% raw %}

```json
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
* [`IncrementVolumeRequest`](#IncrementVolumeRequest)

## IncrementVolumeRequest {#IncrementVolumeRequest}
주로 TV 셋톱 박스와 같은 기기를 제어할 때 사용되며, 대상 기기가 지정한 값만큼 스피커 볼륨을 높이도록 Clova Home extension에게 요청합니다. 이 요청에 대한 응답으로 [`IncrementVolumeConfirmation`](#IncrementVolumeConfirmation) 메시지를 사용해야 합니다.

### Payload fields

| 필드 이름       | 자료형    | 필드 설명                     | 포함 여부 |
|---------------|---------|-----------------------------|:---------:|
| `accessToken`      | string                                  | IoT 서비스의 사용자 계정의 access token. CEK는 외부 서비스의 인증 서버로부터 획득한 사용자 계정의 access token을 전달합니다. 자세한 설명은 [사용자 계정 연결하기](/CEK/Guides/Link_User_Account.md)를 참조합니다.                          | 항상    |
| `appliance`        | [ApplianceInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#ApplianceInfoObject)     | 대상 기기 정보를 담고 있는 객체. `applianceId` 필드는 필수입니다. | 항상    |
| `deltaVolume` | [VolumeInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#VolumeInfoObject)                | 변경할 볼륨의 크기 정보를 담고 있는 객체                              | 항상    |

### Message example

{% raw %}

```json
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
```

{% endraw %}

### See also
* [`IncrementVolumeConfirmation`](#IncrementVolumeConfirmation)

## LowerConfirmation {#LowerConfirmation}
[`LowerRequest`](#LowerRequest) 메시지에 대한 응답으로 대상 기기의 높낮이를 낮추도록 요청한 후 처리된 결과를 CEK에게 전달합니다.

### Payload fields

없음

### Message example

{% raw %}

```json
{
  "header": {
    "messageId": "4ec35000-88ce-4724-b7e4-7f52050558fd",
    "name": "LowerConfirmation",
    "namespace": "ClovaHome",
    "payloadVersion": "1.0"
  },
  "payload": {}
}
```

{% endraw %}

### See also
* [`LowerRequest`](#LowerRequest)

## LowerRequest {#LowerRequest}
스마트 침대 같은 기기를 제어할 때 사용되며, 대상 기기의 높낮이를 내리도록 Clova Home extension에게 요청합니다. 이 요청에 대한 응답으로 [`LowerConfirmation`](#LowerConfirmation) 메시지를 사용해야 합니다.

### Payload fields

| 필드 이름       | 자료형    | 필드 설명                     | 포함 여부 |
|---------------|---------|-----------------------------|:---------:|
| `accessToken`      | string                                  | IoT 서비스의 사용자 계정의 access token. CEK는 외부 서비스의 인증 서버로부터 획득한 사용자 계정의 access token을 전달합니다. 자세한 설명은 [사용자 계정 연결하기](/CEK/Guides/Link_User_Account.md)를 참조합니다.                          | 항상    |
| `appliance`        | [ApplianceInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#ApplianceInfoObject)     | 대상 기기 정보를 담고 있는 객체. `applianceId` 필드는 필수입니다.     | 항상    |

### Remarks
기기의 높낮이를 조정할 때 이동될 수 있는 최대 위치까지 이동됩니다. 높낮이 조정 중에 기기를 멈추려면 [StopRequest](#StopRequest) 메시지를 받아야 합니다.

### Message example

{% raw %}

```json
{
  "header": {
    "messageId": "253f1f01-c157-411d-8c3f-96ea6173fcc6",
    "name": "LowerRequest",
    "namespace": "ClovaHome",
    "payloadVersion": "1.0"
  },
  "payload": {
    "accessToken": "92ebcb67fe33",
    "appliance": {
      "applianceId": "device-014"
    }
  }
}
```

{% endraw %}

### See also
* [`RaiseRequest`](#RaiseRequest)
* [`LowerConfirmation`](#LowerConfirmation)

## MuteConfirmation {#MuteConfirmation}
[`MuteRequest`](#MuteRequest) 메시지에 대한 응답으로 대상 기기의 소리를 끄도록 설정(음소거)한 결과를 CEK에게 전달합니다.

### Payload fields
없음

### Message example

{% raw %}

```json
{
  "header": {
    "messageId": "4ec35000-88ce-4724-b7e4-7f52050558fd",
    "name": "MuteConfirmation",
    "namespace": "ClovaHome",
    "payloadVersion": "1.0"
  },
  "payload": {}
}
```

{% endraw %}

### See also
* [`MuteRequest`](#MuteRequest)

## MuteRequest {#MuteRequest}
주로 TV나 셋톱박스와 같은 기기를 제어할 때 사용되며, 대상 기기의 소리를 끄도록(음소거) Clova Home extension에게 요청합니다. 이 요청에 대한 응답으로 [`MuteConfirmation`](#MuteConfirmation) 메시지를 사용해야 합니다.

### Payload fields

| 필드 이름       | 자료형    | 필드 설명                     | 포함 여부 |
|---------------|---------|-----------------------------|:---------:|
| `accessToken`      | string                                  | IoT 서비스의 사용자 계정의 access token. CEK는 외부 서비스의 인증 서버로부터 획득한 사용자 계정의 access token을 전달합니다. 자세한 설명은 [사용자 계정 연결하기](/CEK/Guides/Link_User_Account.md)를 참조합니다.                          | 항상    |
| `appliance`        | [ApplianceInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#ApplianceInfoObject)     | 대상 기기 정보를 담고 있는 객체. `applianceId` 필드는 필수입니다. | 항상    |

### Message example

{% raw %}

```json
{
  "header": {
    "messageId": "6c04fc2d-64dd-41a0-9162-7cb0d4cf7c08",
    "name": "MuteRequest",
    "namespace": "ClovaHome",
    "payloadVersion": "1.0"
  },
  "payload": {
    "accessToken": "92ebcb67fe33",
    "appliance": {
      "applianceId": "device-005"
    }
  }
}
```

{% endraw %}

### See also
* [`MuteConfirmation`](#MuteConfirmation)

## OpenConfirmation {#OpenConfirmation}
[`OpenRequest`](#OpenRequest) 메시지에 대한 응답으로 스마트 커튼이 일광 차단을 해제하거나, 비데의 뚜껑을 열도록 요청한 후 처리된 결과를 CEK에게 전달합니다.

### Payload fields

없음

### Message example

{% raw %}

```json
{
  "header": {
    "messageId": "a4349fd5-7c1c-4fae-9bbd-291749bdd63a",
    "name": "OpenConfirmation",
    "namespace": "ClovaHome",
    "payloadVersion": "1.0"
  },
  "payload": {}
}
```

{% endraw %}

### See also
* [`OpenRequest`](#OpenRequest)

## OpenRequest {#OpenRequest}
스마트 커튼이나 비데 등의 제품을 제어할 때 사용되며, 스마트 커튼이 일광 차단을 해제하거나, 비데의 뚜껑을 열도록 Clova Home extension에게 요청합니다. 이 요청에 대한 응답으로 [`OpenConfirmation`](#OpenConfirmation) 메시지를 사용해야 합니다.

### Payload fields

| 필드 이름       | 자료형    | 필드 설명                     | 포함 여부 |
|---------------|---------|-----------------------------|:---------:|
| `accessToken`      | string                                  | IoT 서비스의 사용자 계정의 access token. CEK는 외부 서비스의 인증 서버로부터 획득한 사용자 계정의 access token을 전달합니다. 자세한 설명은 [사용자 계정 연결하기](/CEK/Guides/Link_User_Account.md)를 참조합니다.                          | 항상    |
| `appliance`        | [ApplianceInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#ApplianceInfoObject)     | 대상 기기 정보를 담고 있는 객체. `applianceId` 필드는 필수입니다.     | 항상    |

### Message example

{% raw %}

```json
{
  "header": {
    "messageId": "8030275d-0e71-463d-b1d8-3e761e5389ad",
    "name": "OpenRequest",
    "namespace": "ClovaHome",
    "payloadVersion": "1.0"
  },
  "payload": {
    "accessToken": "92ebcb67fe33",
    "appliance": {
      "applianceId": "device-012"
    }
  }
}
```

{% endraw %}

### See also
* [`OpenConfirmation`](#OpenConfirmation)

## RaiseConfirmation {#RaiseConfirmation}
[`RaiseRequest`](#RaiseRequest) 메시지에 대한 응답으로 대상 기기의 높낮이를 높이도록 요청한 후 처리된 결과를 CEK에게 전달합니다.

### Payload fields

없음

### Message example

{% raw %}

```json
{
  "header": {
    "messageId": "4ec35000-88ce-4724-b7e4-7f52050558fd",
    "name": "RaiseConfirmation",
    "namespace": "ClovaHome",
    "payloadVersion": "1.0"
  },
  "payload": {}
}
```

{% endraw %}

### See also
* [`RaiseRequest`](#RaiseRequest)

## RaiseRequest {#RaiseRequest}
스마트 침대 같은 기기를 제어할 때 사용되며, 대상 기기의 높낮이를 높이도록 Clova Home extension에게 요청합니다. 이 요청에 대한 응답으로 [`RaiseConfirmation`](#RaiseConfirmation) 메시지를 사용해야 합니다.

### Payload fields

| 필드 이름       | 자료형    | 필드 설명                     | 포함 여부 |
|---------------|---------|-----------------------------|:---------:|
| `accessToken`      | string                                  | IoT 서비스의 사용자 계정의 access token. CEK는 외부 서비스의 인증 서버로부터 획득한 사용자 계정의 access token을 전달합니다. 자세한 설명은 [사용자 계정 연결하기](/CEK/Guides/Link_User_Account.md)를 참조합니다.                          | 항상    |
| `appliance`        | [ApplianceInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#ApplianceInfoObject)     | 대상 기기 정보를 담고 있는 객체. `applianceId` 필드는 필수입니다.     | 항상    |

### Remarks
기기의 높낮이를 조정할 때 이동될 수 있는 최대 위치까지 이동됩니다. 높낮이 조정 중에 기기를 멈추려면 [StopRequest](#StopRequest) 메시지를 받아야 합니다.

### Message example

{% raw %}

```json
{
  "header": {
    "messageId": "253f1f01-c157-411d-8c3f-96ea6173fcc6",
    "name": "RaiseRequest",
    "namespace": "ClovaHome",
    "payloadVersion": "1.0"
  },
  "payload": {
    "accessToken": "92ebcb67fe33",
    "appliance": {
      "applianceId": "device-014"
    }
  }
}
```

{% endraw %}

### See also

* [`LowerRequest`](#LowerRequest)
* [`RaiseConfirmation`](#RaiseConfirmation)

## ReleaseModeConfirmation {#ReleaseModeConfirmation}
[`ReleaseModeRequest`](#ReleaseModeRequest) 메시지에 대한 응답으로 현재 기기의 운전 모드(operation mode)를 해제하도록 요청한 후 처리된 결과를 CEK에게 전달합니다.

### Payload fields

| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|:---------:|
| `mode`          | [ModeInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#ModeInfoObject)  | 운전 모드 해제 요청에 의해 대상 기기에 설정되었거나 extension이 대상 기기에게 되돌아가도록 요청한 운전 모드 정보를 담고 있는 객체      | 선택    |
| `previousState` | [ModeInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#ModeInfoObject)  | 운전 모드 해제 요청 전에 대상 기기에 설정되어 있던 운전 모드 정보를 담고 있는 객체      | 선택    |

### Remarks

대상 기기에서 payload에 입력할 정보를 얻어올 수 없으면 값을 입력하지 않아도 됩니다. 이 경우 사용자에게 구체적인 정보 없이 기기 제어 요청이 정상 처리되었음을 알려줍니다.

### Message example

{% raw %}

```json
{
  "header": {
    "messageId": "4ec35000-88ce-4724-b7e4-7f52050558fd",
    "name": "ReleaseModeConfirmation",
    "namespace": "ClovaHome",
    "payloadVersion": "1.0"
  },
  "payload": {
    "previousState": {
      "mode": {
        "value": "sleep"
      }
    },
    "mode": {
      "value": "wakeup"
    }
  }
}
```

{% endraw %}

### See also
* [`ReleaseModeRequest`](#ReleaseModeRequest)

## ReleaseModeRequest {#ReleaseModeRequest}
현재 기기에 설정된 운전 모드(operation mode)를 해제할 때 사용되며, 기기의 운전 모드를 해제하여 이전 운전 모드나 기본 운전 모드로 돌아가도록 Clova Home extension에게 요청합니다. 이 요청에 대한 응답으로 [`ReleaseModeConfirmation`](#ReleaseModeConfirmation) 메시지를 사용해야 합니다.

### Payload fields

| 필드 이름       | 자료형    | 필드 설명                     | 포함 여부 |
|---------------|---------|-----------------------------|:---------:|
| `accessToken` | string  | IoT 서비스의 사용자 계정의 access token. CEK는 외부 서비스의 인증 서버로부터 획득한 사용자 계정의 access token을 전달합니다. 자세한 설명은 [사용자 계정 연결하기](/CEK/Guides/Link_User_Account.md)를 참조합니다. | 항상    |
| `appliance`   | [ApplianceInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#ApplianceInfoObject)     | 대상 기기 정보를 담고 있는 객체. `applianceId` 필드는 필수입니다. | 항상    |
| `mode`        | [ModeInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#ModeInfoObject) | 대상 기기에서 해제할 운전 모드 정보를 담고 있는 객체                         | 항상    |

### Message example

{% raw %}

```json
{
  "header": {
    "messageId": "33da6561-0149-4532-a30b-e0de8f75c4cf",
    "name": "ReleaseModeRequest",
    "namespace": "ClovaHome",
    "payloadVersion": "1.0"
  },
  "payload": {
    "accessToken": "92ebcb67fe33",
    "appliance": {
        "applianceId": "device-006"
    },
    "mode": "sleep"
  }
}
```

{% endraw %}

### See also
* [`ReleaseModeConfirmation`](#ReleaseModeConfirmation)

## SetBrightnessConfirmation {#SetBrightnessConfirmation}
[`SetBrightnessRequest`](#SetBrightnessRequest) 메시지에 대한 응답으로 조명 밝기를 변경하도록 요청한 후 처리된 결과를 CEK에게 전달합니다.

### Payload fields

| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|:---------:|
| `brightness`               | [BrightnessInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#BrightnessInfoObject) | 대상 기기에 설정되었거나 extension이 대상 기기에게 설정하도록 요청한 밝기 정보를 담고 있는 객체                                | 선택    |

### Remarks

대상 기기에서 payload에 입력할 정보를 얻어올 수 없으면 값을 입력하지 않아도 됩니다. 이 경우 사용자에게 구체적인 정보 없이 기기 제어 요청이 정상 처리되었음을 알려줍니다.

### Message example

{% raw %}

```json
{
  "header": {
    "messageId": "4ec35000-88ce-4724-b7e4-7f52050558fd",
    "name": "SetBrightnessConfirmation",
    "namespace": "ClovaHome",
    "payloadVersion": "1.0"
  },
  "payload": {
    "brightness": {
      "value": 80
    }
  }
}
```

{% endraw %}

### See also
* [`SetBrightnessRequest`](#SetBrightnessRequest)

## SetBrightnessRequest {#SetBrightnessRequest}
주로 조명 기기를 제어할 때 사용되며, 대상 기기가 조명 밝기를 지정한 값으로 변경하도록 Clova Home extension에게 요청합니다. 이 요청에 대한 응답으로 [`SetBrightnessConfirmation`](#SetBrightnessConfirmation) 메시지를 사용해야 합니다.

### Payload fields

| 필드 이름       | 자료형    | 필드 설명                     | 포함 여부 |
|---------------|---------|-----------------------------|:---------:|
| `accessToken`   | string | IoT 서비스의 사용자 계정의 access token. CEK는 외부 서비스의 인증 서버로부터 획득한 사용자 계정의 access token을 전달합니다. 자세한 설명은 [사용자 계정 연결하기](/CEK/Guides/Link_User_Account.md)를 참조합니다.                          | 항상    |
| `appliance`     | [ApplianceInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#ApplianceInfoObject) | 대상 기기 정보를 담고 있는 객체. `applianceId` 필드는 필수입니다. | 항상    |
| `brightness`       | [BrightnessInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#BrightnessInfoObject) | 대상 기기에 설정할 조명 밝기 정보를 담고 있는 객체                | 항상    |

### Message example

{% raw %}

```json
{
  "header": {
    "messageId": "6c04fc2d-64dd-41a0-9162-7cb0d4cf7c08",
    "name": "SetBrightnessRequest",
    "namespace": "ClovaHome",
    "payloadVersion": "1.0"
  },
  "payload": {
    "accessToken": "92ebcb67fe33",
    "appliance": {
      "applianceId": "device-006"
    },
    "brightness": {
      "value": 80
    }
  }
}
```

{% endraw %}

### See also
* [`SetBrightnessConfirmation`](#SetBrightnessConfirmation)

## SetChannelByNameConfirmation {#SetChannelByNameConfirmation}
[`SetChannelByNameRequest`](#SetChannelByNameRequest) 메시지에 대한 응답으로 채널 이름으로 TV 채널을 변경하도록 요청한 후 처리된 결과를 CEK에게 전달합니다.

### Payload fields

| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|:---------:|
| `channelName`               | [TVChannelNameInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#TVChannelNameInfoObject) | 대상 기기에 설정되었거나 extension이 대상 기기에게 설정하도록 요청한 TV 채널의 이름 정보를 담고 있는 객체                                | 선택    |

### Remarks

대상 기기에서 payload에 입력할 정보를 얻어올 수 없으면 값을 입력하지 않아도 됩니다. 이 경우 사용자에게 구체적인 정보 없이 기기 제어 요청이 정상 처리되었음을 알려줍니다.

### Message example

{% raw %}

```json
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
* [`SetChannelByNameRequest`](#SetChannelByNameRequest)

## SetChannelByNameRequest {#SetChannelByNameRequest}
주로 TV 셋톱 박스와 같은 기기를 제어할 때 사용되며, 대상 기기가 지정한 채널 이름으로 채널을 변경하도록 Clova Home extension에게 요청합니다. 이 요청에 대한 응답으로 [`SetChannelByNameConfirmation`](#SetChannelByNameConfirmation) 메시지를 사용해야 합니다.

### Payload fields

| 필드 이름       | 자료형    | 필드 설명                     | 포함 여부 |
|---------------|---------|-----------------------------|:---------:|
| `accessToken`   | string | IoT 서비스의 사용자 계정의 access token. CEK는 외부 서비스의 인증 서버로부터 획득한 사용자 계정의 access token을 전달합니다. 자세한 설명은 [사용자 계정 연결하기](/CEK/Guides/Link_User_Account.md)를 참조합니다.                          | 항상    |
| `appliance`     | [ApplianceInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#ApplianceInfoObject) | 대상 기기 정보를 담고 있는 객체. `applianceId` 필드는 필수입니다. | 항상    |
| `channelName`       | [TVChannelNameInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#TVChannelNameInfoObject) | 대상 기기에 설정할 TV 채널의 이름 정보를 담고 있는 객체                | 항상    |

### Message example

{% raw %}

```json
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
```

{% endraw %}

### See also
* [`SetChannelByNameConfirmation`](#SetChannelByNameConfirmation)

## SetChannelConfirmation {#SetChannelConfirmation}
[`SetChannelRequest`](#SetChannelRequest) 메시지에 대한 응답으로 채널 번호로 TV 채널을 변경하도록 요청한 후 처리된 결과를 CEK에게 전달합니다.

### Payload fields

| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|:---------:|
| `channel`     | [TVChannelInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#TVChannelInfoObject)  | 대상 기기에 설정되었거나 extension이 대상 기기에게 설정하도록 요청한 TV 채널 정보를 담고 있는 객체      | 선택    |
| `subChannel`  | [TVChannelInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#TVChannelInfoObject)  | 대상 기기에 설정되었거나 extension이 대상 기기에게 설정하도록 요청한 TV 채널의 서브 채널 정보를 가지는 객체 | 선택    |

### Remarks

대상 기기에서 payload에 입력할 정보를 얻어올 수 없으면 값을 입력하지 않아도 됩니다. 이 경우 사용자에게 구체적인 정보 없이 기기 제어 요청이 정상 처리되었음을 알려줍니다.

### Message example

{% raw %}

```json
{
  "header": {
    "messageId": "4ec35000-88ce-4724-b7e4-7f52050558fd",
    "name": "SetChannelConfirmation",
    "namespace": "ClovaHome",
    "payloadVersion": "1.0"
  },
  "payload": {
    "channel": {
      "value":15
    },
    "subChannel": {
      "value": 1
    }
  }
}
```

{% endraw %}

### See also
* [`SetChannelRequest`](#SetChannelRequest)

## SetChannelRequest {#SetChannelRequest}
주로 TV 셋톱 박스와 같은 기기를 제어할 때 사용되며, 대상 기기가 지정한 채널 번호로 채널을 변경하도록 Clova Home extension에게 요청합니다. 이 요청에 대한 응답으로 [`SetChannelConfirmation`](#SetChannelConfirmation) 메시지를 사용해야 합니다.

### Payload fields

| 필드 이름       | 자료형    | 필드 설명                     | 포함 여부 |
|---------------|---------|-----------------------------|:---------:|
| `accessToken`   | string | IoT 서비스의 사용자 계정의 access token. CEK는 외부 서비스의 인증 서버로부터 획득한 사용자 계정의 access token을 전달합니다. 자세한 설명은 [사용자 계정 연결하기](/CEK/Guides/Link_User_Account.md)를 참조합니다.                          | 항상    |
| `appliance`     | [ApplianceInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#ApplianceInfoObject) | 대상 기기 정보를 담고 있는 객체. `applianceId` 필드는 필수입니다. | 항상    |
| `channel`       | [TVChannelInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#TVChannelInfoObject) | 대상 기기에 설정할 TV 채널 정보를 담고 있는 객체                | 항상    |
| `subChannel`    | [TVChannelInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#TVChannelInfoObject) | 대상 기기에 설정할 TV 채널의 서브 채널 정보를 가지는 객체         | 조건부   |

### Message example

{% raw %}

```json
{
  "header": {
    "messageId": "6c04fc2d-64dd-41a0-9162-7cb0d4cf7c08",
    "name": "SetChannelRequest",
    "namespace": "ClovaHome",
    "payloadVersion": "1.0"
  },
  "payload": {
    "accessToken": "92ebcb67fe33",
    "appliance": {
      "applianceId": "device-006"
    },
    "channel": {
      "value": 15
    },
    "subChannel": {
      "value": 1
    }
  }
}
```

{% endraw %}

### See also
* [`SetChannelConfirmation`](#SetChannelConfirmation)

## SetColorConfirmation {#SetColorConfirmation}
[`SetColorRequest`](#SetColorRequest) 메시지에 대한 응답으로 대상기기의 조명이나 화면, 전등의 색을 변경하도록 요청한 후 처리된 결과를 CEK에게 전달합니다.

### Payload fields

| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|:---------:|
| `color`   | [ColorInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#ColorInfoObject) | 대상 기기에 설정되었거나 extension이 대상 기기에게 설정하도록 요청한 조명이나 화면, 전등의 색 정보를 담고 있는 객체                                | 선택    |

### Remarks

대상 기기에서 payload에 입력할 정보를 얻어올 수 없으면 값을 입력하지 않아도 됩니다. 이 경우 사용자에게 구체적인 정보 없이 기기 제어 요청이 정상 처리되었음을 알려줍니다.

### Message example

{% raw %}

```json
{
  "header": {
    "messageId": "0e380076-59f1-4417-9d30-895be4b34cea",
    "name": "SetColorConfirmation",
    "namespace": "ClovaHome",
    "payloadVersion": "1.0"
  },
  "payload": {
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
* [`SetColorRequest`](#SetColorRequest)

## SetColorRequest {#SetColorRequest}
주로 스마트 전등과 같은 기기를 제어할 때 사용되며, 대상 기기의 조명이나 화면, 전등의 색을 변경하도록 Clova Home extension에게 요청합니다. 이 요청에 대한 응답으로 [`SetColorConfirmation`](#SetColorConfirmation) 메시지를 사용해야 합니다.

### Payload fields

| 필드 이름       | 자료형    | 필드 설명                     | 포함 여부 |
|---------------|---------|-----------------------------|:---------:|
| `accessToken`   | string | IoT 서비스의 사용자 계정의 access token. CEK는 외부 서비스의 인증 서버로부터 획득한 사용자 계정의 access token을 전달합니다. 자세한 설명은 [사용자 계정 연결하기](/CEK/Guides/Link_User_Account.md)를 참조합니다.                          | 항상    |
| `appliance`     | [ApplianceInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#ApplianceInfoObject) | 대상 기기 정보를 담고 있는 객체. `applianceId` 필드는 필수입니다. | 항상    |
| `color`         | [ColorInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#ColorInfoObject) | 대상 기기의 조명이나 화면, 전등에 설정할 색 정보를 담고 있는 객체            | 항상    |

### Message example

{% raw %}

```json
{
  "header": {
    "messageId": "a130f6de-d2ac-45d5-86b7-936a841a3c63",
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
* [`SetColorConfirmation`](#SetColorConfirmation)

## SetColorTemperatureConfirmation {#SetColorTemperatureConfirmation}
[`SetColorTemperatureRequest`](#SetColorTemperatureRequest) 메시지에 대한 응답으로 대상기기의 조명이나 화면, 전등의 색온도를 변경하도록 요청한 후 처리된 결과를 CEK에게 전달합니다.

### Payload fields

| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|:---------:|
| `colorTemperature`   | [ColorTemperatureInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#ColorTemperatureInfoObject) | 대상 기기에 설정되었거나 extension이 대상 기기에게 설정하도록 요청한 조명이나 화면, 전등의 색온도 정보를 담고 있는 객체                                | 선택    |

### Remarks

대상 기기에서 payload에 입력할 정보를 얻어올 수 없으면 값을 입력하지 않아도 됩니다. 이 경우 사용자에게 구체적인 정보 없이 기기 제어 요청이 정상 처리되었음을 알려줍니다.

### Message example

{% raw %}

```json
{
  "header": {
    "messageId": "4ec35000-88ce-4724-b7e4-7f52050558fd",
    "name": "SetColorTemperatureConfirmation",
    "namespace": "ClovaHome",
    "payloadVersion": "1.0"
  },
  "payload": {
  	"colorTemperature": {
  		"value": 3600
  	}
  }
}
```

{% endraw %}

### See also
* [`SetColorTemperatureRequest`](#SetColorTemperatureRequest)

## SetColorTemperatureRequest {#SetColorTemperatureRequest}
주로 스마트 전등과 같은 기기를 제어할 때 사용되며, 대상 기기의 조명이나 화면, 전등의 색온도를 변경하도록 Clova Home extension에게 요청합니다. 이 요청에 대한 응답으로 [`SetColorTemperatureConfirmation`](#SetColorTemperatureConfirmation) 메시지를 사용해야 합니다.

### Payload fields

| 필드 이름       | 자료형    | 필드 설명                     | 포함 여부 |
|---------------|---------|-----------------------------|:---------:|
| `accessToken`   | string | IoT 서비스의 사용자 계정의 access token. CEK는 외부 서비스의 인증 서버로부터 획득한 사용자 계정의 access token을 전달합니다. 자세한 설명은 [사용자 계정 연결하기](/CEK/Guides/Link_User_Account.md)를 참조합니다.                          | 항상    |
| `appliance`     | [ApplianceInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#ApplianceInfoObject) | 대상 기기 정보를 담고 있는 객체. `applianceId` 필드는 필수입니다. | 항상    |
| `colorTemperature` | [ColorTemperatureInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#ColorTemperatureInfoObject) | 대상 기기의 조명이나 화면, 전등에 설정할 색온도 정보를 담고 있는 객체                | 항상    |

### Message example

{% raw %}

```json
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
* [`SetColorTemperatureConfirmation`](#SetColorTemperatureConfirmation)

## SetFanSpeedConfirmation {#SetFanSpeedConfirmation}
[`SetFanSpeedRequest`](#SetFanSpeedRequest) 메시지에 대한 응답으로 팬 속도를 변경하도록 요청한 후 처리된 결과를 CEK에게 전달합니다.

### Payload fields

| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|:---------:|
| `fanSpeed`               | [SpeedInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#SpeedInfoObject) | 대상 기기에 설정되었거나 extension이 대상 기기에게 설정하도록 요청한 팬의 속도 정보를 담고 있는 객체. 팬의 속도는 풍속을 의미하며 팬 속도를 다음과 같은 값으로 제한합니다.<ul><li><code>1</code>: 약한 바람(1단)</li><li><code>2</code>: 중간 바람(2단)</li><li><code>3</code>: 강한 바람(3단)</li></ul>   | 선택    |

### Remarks

대상 기기에서 payload에 입력할 정보를 얻어올 수 없으면 값을 입력하지 않아도 됩니다. 이 경우 사용자에게 구체적인 정보 없이 기기 제어 요청이 정상 처리되었음을 알려줍니다.

### Message example

{% raw %}

```json
{
  "header": {
    "messageId": "4ec35000-88ce-4724-b7e4-7f52050558fd",
    "name": "SetFanSpeedConfirmation",
    "namespace": "ClovaHome",
    "payloadVersion": "1.0"
  },
  "payload": {
    "fanSpeed": {
      "value": 2
    }
  }
}
```

{% endraw %}

### See also
* [`SetFanSpeedRequest`](#SetFanSpeedRequest)

## SetFanSpeedRequest {#SetFanSpeedRequest}
주로 공기청정기와 같은 기기를 제어할 때 사용되며, 대상 기기가 지정한 값으로 팬 속도를 변경하도록 Clova Home extension에게 요청합니다. 이 요청에 대한 응답으로 [`SetFanSpeedConfirmation`](#SetFanSpeedConfirmation) 메시지를 사용해야 합니다.

### Payload fields

| 필드 이름       | 자료형    | 필드 설명                     | 포함 여부 |
|---------------|---------|-----------------------------|:---------:|
| `accessToken`   | string | IoT 서비스의 사용자 계정의 access token. CEK는 외부 서비스의 인증 서버로부터 획득한 사용자 계정의 access token을 전달합니다. 자세한 설명은 [사용자 계정 연결하기](/CEK/Guides/Link_User_Account.md)를 참조합니다.                          | 항상    |
| `appliance`     | [ApplianceInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#ApplianceInfoObject) | 대상 기기 정보를 담고 있는 객체. `applianceId` 필드는 필수입니다. | 항상    |
| `fanSpeed`       | [SpeedInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#SpeedInfoObject) | 대상 기기에 설정할 팬의 속도 정보를 담고 있는 객체. 팬의 속도는 풍속을 의미하며 팬 속도를 다음과 같은 값으로 제한합니다.<ul><li><code>1</code>: 약한 바람(1단)</li><li><code>2</code>: 중간 바람(2단)</li><li><code>3</code>: 강한 바람(3단)</li></ul>     | 항상    |

### Message example

{% raw %}

```json
{
  "header": {
    "messageId": "6c04fc2d-64dd-41a0-9162-7cb0d4cf7c08",
    "name": "SetFanSpeedRequest",
    "namespace": "ClovaHome",
    "payloadVersion": "1.0"
  },
  "payload": {
    "accessToken": "92ebcb67fe33",
    "appliance": {
      "applianceId": "device-004"
    },
    "fanSpeed": {
      "value": 2
    }
  }
}
```

{% endraw %}

### See also
* [`SetFanSpeedConfirmation`](#SetFanSpeedConfirmation)

## SetFreezerTargetTemperatureConfirmation {#SetFreezerTargetTemperatureConfirmation}
[`SetFreezerTargetTemperatureRequest`](#SetFreezerTargetTemperatureRequest) 메시지에 대한 응답으로 냉동실의 희망 온도를 변경하도록 요청한 후 처리된 결과를 CEK에게 전달합니다.

### Payload fields

| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|:---------:|
| `targetTemperature`               | [TemperatureInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#TemperatureInfoObject) | 대상 기기에 설정되었거나 extension이 대상 기기에게 설정하도록 요청한 희망 온도 정보를 담고 있는 객체                                | 선택    |

### Remarks

대상 기기에서 payload에 입력할 정보를 얻어올 수 없으면 값을 입력하지 않아도 됩니다. 이 경우 사용자에게 구체적인 정보 없이 기기 제어 요청이 정상 처리되었음을 알려줍니다.

### Message example

{% raw %}

```json
{
  "header": {
    "messageId": "4ec35000-88ce-4724-b7e4-7f52050558fd",
    "name": "SetFreezerTargetTemperatureConfirmation",
    "namespace": "ClovaHome",
    "payloadVersion": "1.0"
  },
  "payload": {
    "targetTemperature": {
      "value": 22
    }
  }
}
```

{% endraw %}

### See also
* [`SetFreezerTargetTemperatureRequest`](#SetFreezerTargetTemperatureRequest)

## SetFreezerTargetTemperatureRequest {#SetFreezerTargetTemperatureRequest}
냉장고 같은 기기를 제어할 때 사용되며, 냉장고의 냉동고 희망 온도를 지정한 값으로 변경하도록 Clova Home extension에게 요청합니다. 이 요청에 대한 응답으로 [`SetFreezerTargetTemperatureConfirmation`](#SetFreezerTargetTemperatureConfirmation) 메시지를 사용해야 합니다.

### Payload fields

| 필드 이름       | 자료형    | 필드 설명                     | 포함 여부 |
|---------------|---------|-----------------------------|:---------:|
| `accessToken`   | string | IoT 서비스의 사용자 계정의 access token. CEK는 외부 서비스의 인증 서버로부터 획득한 사용자 계정의 access token을 전달합니다. 자세한 설명은 [사용자 계정 연결하기](/CEK/Guides/Link_User_Account.md)를 참조합니다.                          | 항상    |
| `appliance`     | [ApplianceInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#ApplianceInfoObject) | 대상 기기 정보를 담고 있는 객체. `applianceId` 필드는 필수입니다.        | 항상    |
| `targetTemperature`       | [TemperatureInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#TemperatureInfoObject) | 대상 기기에 설정해야 할 희망 온도 정보를 담고 있는 객체     | 항상    |

### Message example

{% raw %}

```json
{
  "header": {
    "messageId": "6c04fc2d-64dd-41a0-9162-7cb0d4cf7c08",
    "name": "SetFreezerTargetTemperatureRequest",
    "namespace": "ClovaHome",
    "payloadVersion": "1.0"
  },
  "payload": {
    "accessToken": "92ebcb67fe33",
    "appliance": {
      "applianceId": "device-021"
    },
    "targetTemperature": {
      "value": 22
    }
  }
}
```

{% endraw %}

### See also
* [`SetFreezerTargetTemperatureConfirmation`](#SetFreezerTargetTemperatureConfirmation)

## SetFridgeTargetTemperatureConfirmation {#SetFridgeTargetTemperatureConfirmation}
[`SetFridgeTargetTemperatureRequest`](#SetFridgeTargetTemperatureRequest) 메시지에 대한 응답으로 냉장실의 희망 온도를 변경하도록 요청한 후 처리된 결과를 CEK에게 전달합니다.

### Payload fields

| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|:---------:|
| `targetTemperature`               | [TemperatureInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#TemperatureInfoObject) | 대상 기기에 설정되었거나 extension이 대상 기기에게 설정하도록 요청한 희망 온도 정보를 담고 있는 객체                                | 선택    |

### Remarks

대상 기기에서 payload에 입력할 정보를 얻어올 수 없으면 값을 입력하지 않아도 됩니다. 이 경우 사용자에게 구체적인 정보 없이 기기 제어 요청이 정상 처리되었음을 알려줍니다.

### Message example

{% raw %}

```json
{
  "header": {
    "messageId": "4ec35000-88ce-4724-b7e4-7f52050558fd",
    "name": "SetFridgeTargetTemperatureConfirmation",
    "namespace": "ClovaHome",
    "payloadVersion": "1.0"
  },
  "payload": {
    "targetTemperature": {
      "value": 22
    }
  }
}
```

{% endraw %}

### See also
* [`SetFridgeTargetTemperatureRequest`](#SetFridgeTargetTemperatureRequest)

## SetFridgeTargetTemperatureRequest {#SetFridgeTargetTemperatureRequest}
냉장고 같은 기기를 제어할 때 사용되며, 냉장고의 냉장실 희망 온도를 지정한 값으로 변경하도록 Clova Home extension에게 요청합니다. 이 요청에 대한 응답으로 [`SetFridgeTargetTemperatureConfirmation`](#SetFridgeTargetTemperatureConfirmation) 메시지를 사용해야 합니다.

### Payload fields

| 필드 이름       | 자료형    | 필드 설명                     | 포함 여부 |
|---------------|---------|-----------------------------|:---------:|
| `accessToken`   | string | IoT 서비스의 사용자 계정의 access token. CEK는 외부 서비스의 인증 서버로부터 획득한 사용자 계정의 access token을 전달합니다. 자세한 설명은 [사용자 계정 연결하기](/CEK/Guides/Link_User_Account.md)를 참조합니다.                          | 항상    |
| `appliance`     | [ApplianceInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#ApplianceInfoObject) | 대상 기기 정보를 담고 있는 객체. `applianceId` 필드는 필수입니다.        | 항상    |
| `targetTemperature`       | [TemperatureInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#TemperatureInfoObject) | 대상 기기에 설정해야 할 희망 온도 정보를 담고 있는 객체     | 항상    |

### Message example

{% raw %}

```json
{
  "header": {
    "messageId": "6c04fc2d-64dd-41a0-9162-7cb0d4cf7c08",
    "name": "SetFridgeTargetTemperatureRequest",
    "namespace": "ClovaHome",
    "payloadVersion": "1.0"
  },
  "payload": {
    "accessToken": "92ebcb67fe33",
    "appliance": {
      "applianceId": "device-021"
    },
    "targetTemperature": {
      "value": 22
    }
  }
}
```

{% endraw %}

### See also
* [`SetFridgeTargetTemperatureConfirmation`](#SetFridgeTargetTemperatureConfirmation)

## SetLockStateConfirmation {#SetLockStateConfirmation}
[`SetLockStateRequest`](#SetLockStateRequest) 메시지에 대한 응답으로 대상 기기가 잠기거나 열리도록 요청한 후 처리된 결과를 CEK에게 전달합니다.

### Payload fields

| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|:---------:|
| `lockState`   | string  | 대상 기기에 설정되었거나 extension이 대상 기기에게 설정하도록 요청한 기기의 잠금 상태. 다음과 같은 값을 가집니다. <ul><li><code>"LOCKED"</code></li><li><code>"UNLOCKED"</code></li></ul> | 필수    |


### Message example

{% raw %}

```json
{
  "header": {
    "messageId": "4ec35000-88ce-4724-b7e4-7f52050558fd",
    "name": "SetLockStateConfirmation",
    "namespace": "ClovaHome",
    "payloadVersion": "1.0"
  },
  "payload": {
    "lockState": "LOCKED"
  }
}
```

{% endraw %}

### See also
* [`SetLockStateRequest`](#SetLockStateRequest)

## SetLockStateRequest {#SetLockStateRequest}
주로 스마트 밸브와 같은 기기를 제어할 때 사용되며, 대상 기기를 잠그거나 열도록 Clova Home extension에게 요청합니다. 이 요청에 대한 응답으로 [`SetLockStateConfirmation`](#SetLockStateConfirmation) 메시지를 사용해야 합니다.

### Payload fields

| 필드 이름       | 자료형    | 필드 설명                     | 포함 여부 |
|---------------|---------|-----------------------------|:---------:|
| `accessToken`   | string | IoT 서비스의 사용자 계정의 access token. CEK는 외부 서비스의 인증 서버로부터 획득한 사용자 계정의 access token을 전달합니다. 자세한 설명은 [사용자 계정 연결하기](/CEK/Guides/Link_User_Account.md)를 참조합니다.                          | 항상    |
| `appliance`     | [ApplianceInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#ApplianceInfoObject) | 대상 기기 정보를 담고 있는 객체. `applianceId` 필드는 필수입니다. | 항상    |
| `lockState`       | string | 설정할 기기의 잠금 상태. 다음과 같은 값을 가집니다. <ul><li><code>"LOCKED"</code></li><li><code>"UNLOCKED"</code></li></ul> | 항상    |

### Message example

{% raw %}

```json
{
  "header": {
    "messageId": "6c04fc2d-64dd-41a0-9162-7cb0d4cf7c08",
    "name": "SetLockStateRequest",
    "namespace": "ClovaHome",
    "payloadVersion": "1.0"
  },
  "payload": {
    "accessToken": "92ebcb67fe33",
    "appliance": {
      "applianceId": "device-012"
    },
    "lockState": "LOCKED"
  }
}
```

{% endraw %}

### See also
* [`SetLockStateConfirmation`](#SetLockStateConfirmation)

## SetModeConfirmation {#SetModeConfirmation}
[`SetModeRequest`](#SetModeRequest) 메시지에 대한 응답으로 운전 모드(operation mode)를 변경하도록 요청한 후 처리된 결과를 CEK에게 전달합니다.

### Payload fields

| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|:---------:|
| `mode`        | [ModeInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#ModeInfoObject)  | 대상 기기에 설정되었거나 extension이 대상 기기에게 설정하도록 요청한 운전 모드 정보를 담고 있는 객체      | 선택    |

### Remarks

대상 기기에서 payload에 입력할 정보를 얻어올 수 없으면 값을 입력하지 않아도 됩니다. 이 경우 사용자에게 구체적인 정보 없이 기기 제어 요청이 정상 처리되었음을 알려줍니다.

### Message example

{% raw %}

```json
{
  "header": {
    "messageId": "4ec35000-88ce-4724-b7e4-7f52050558fd",
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
* [`SetModeRequest`](#SetModeRequest)

## SetModeRequest {#SetModeRequest}
기기의 운전 모드(operation mode)를 제어할 때 사용되며, 기기의 운전 모드를 지정한 값으로 변경하도록 Clova Home extension에게 요청합니다. 이 요청에 대한 응답으로 [`SetModeConfirmation`](#SetModeConfirmation) 메시지를 사용해야 합니다.

### Payload fields

| 필드 이름       | 자료형    | 필드 설명                     | 포함 여부 |
|---------------|---------|-----------------------------|:---------:|
| `accessToken` | string  | IoT 서비스의 사용자 계정의 access token. CEK는 외부 서비스의 인증 서버로부터 획득한 사용자 계정의 access token을 전달합니다. 자세한 설명은 [사용자 계정 연결하기](/CEK/Guides/Link_User_Account.md)를 참조합니다. | 항상    |
| `appliance`   | [ApplianceInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#ApplianceInfoObject)     | 대상 기기 정보를 담고 있는 객체. `applianceId` 필드는 필수입니다. | 항상    |
| `mode`        | [ModeInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#ModeInfoObject) | 대상 기기에 설정할 운전 모드 정보를 담고 있는 객체                         | 항상    |

### Message example

{% raw %}

```json
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
```

{% endraw %}

### See also
* [`SetModeConfirmation`](#SetModeConfirmation)

## SetTargetTemperatureConfirmation {#SetTargetTemperatureConfirmation}
[`SetTargetTemperatureRequest`](#SetTargetTemperatureRequest) 메시지에 대한 응답으로 희망 온도를 변경하도록 요청한 후 처리된 결과를 CEK에게 전달합니다.

### Payload fields

| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|:---------:|
| `targetTemperature`               | [TemperatureInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#TemperatureInfoObject) | 대상 기기에 설정되었거나 extension이 대상 기기에게 설정하도록 요청한 희망 온도 정보를 담고 있는 객체                                | 선택    |

### Remarks

대상 기기에서 payload에 입력할 정보를 얻어올 수 없으면 값을 입력하지 않아도 됩니다. 이 경우 사용자에게 구체적인 정보 없이 기기 제어 요청이 정상 처리되었음을 알려줍니다.

### Message example

{% raw %}

```json
{
  "header": {
    "messageId": "4ec35000-88ce-4724-b7e4-7f52050558fd",
    "name": "SetTargetTemperatureConfirmation",
    "namespace": "ClovaHome",
    "payloadVersion": "1.0"
  },
  "payload": {
    "targetTemperature": {
      "value": 22
    }
  }
}
```

{% endraw %}

### See also
* [`SetTargetTemperatureRequest`](#SetTargetTemperatureRequest)

## SetTargetTemperatureRequest {#SetTargetTemperatureRequest}
주로 에어컨이나 온도 조절 장치와 같은 기기를 제어할 때 사용되며, 대상 기기가 희망 온도를 지정한 값으로 변경하도록 Clova Home extension에게 요청합니다. 이 요청에 대한 응답으로 [`SetTargetTemperatureConfirmation`](#SetTargetTemperatureConfirmation) 메시지를 사용해야 합니다.

### Payload fields

| 필드 이름       | 자료형    | 필드 설명                     | 포함 여부 |
|---------------|---------|-----------------------------|:---------:|
| `accessToken`   | string | IoT 서비스의 사용자 계정의 access token. CEK는 외부 서비스의 인증 서버로부터 획득한 사용자 계정의 access token을 전달합니다. 자세한 설명은 [사용자 계정 연결하기](/CEK/Guides/Link_User_Account.md)를 참조합니다.                          | 항상    |
| `appliance`     | [ApplianceInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#ApplianceInfoObject) | 대상 기기 정보를 담고 있는 객체. `applianceId` 필드는 필수입니다. | 항상    |
| `targetTemperature`       | [TemperatureInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#TemperatureInfoObject) | 대상 기기에 설정해야 할 희망 온도 정보를 담고 있는 객체                | 항상    |

### Message example

{% raw %}

```json
{
  "header": {
    "messageId": "6c04fc2d-64dd-41a0-9162-7cb0d4cf7c08",
    "name": "SetTargetTemperatureRequest",
    "namespace": "ClovaHome",
    "payloadVersion": "1.0"
  },
  "payload": {
    "accessToken": "92ebcb67fe33",
    "appliance": {
      "applianceId": "device-001"
    },
    "targetTemperature": {
      "value": 22
    }
  }
}
```

{% endraw %}

### See also
* [`SetTargetTemperatureConfirmation`](#SetTargetTemperatureConfirmation)

## StopConfirmation {#StopConfirmation}
[`StopRequest`](#StopRequest) 메시지에 대한 응답으로 대상 기기에게 동작 중지를 요청한 결과를 CEK에게 전달합니다.

### Payload fields

| 필드 이름       | 자료형    | 필드 설명                     | 필수 |
|---------------|---------|-----------------------------|:---------:|
| `phase`       | [PhaseInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#PhaseInfoObject) | 기기가 정지하기 직전에 수행하던 동작 단계의 정보를 담고 있는 객체   | 선택  |

### Message example

{% raw %}

```json
{
  "header": {
    "messageId": "a4349fd5-7c1c-4fae-9bbd-291749bdd63a",
    "name": "StopConfirmation",
    "namespace": "ClovaHome",
    "payloadVersion": "1.0"
  },
  "payload": {
    "phase": {
      "value": "세탁"
    }
  }
}
```

{% endraw %}

### See also
* [`StopRequest`](#StopRequest)

## StopRequest {#StopRequest}
기기의 현재 동작을 중지하도록 Clova Home extension에게 요청합니다. 이 요청에 대한 응답으로 [`StopConfirmation`](#StopConfirmation) 메시지를 사용해야 합니다.

### Payload fields

| 필드 이름       | 자료형    | 필드 설명                     | 포함 여부 |
|---------------|---------|-----------------------------|:---------:|
| `accessToken`      | string                                  | IoT 서비스의 사용자 계정의 access token. CEK는 외부 서비스의 인증 서버로부터 획득한 사용자 계정의 access token을 전달합니다. 자세한 설명은 [사용자 계정 연결하기](/CEK/Guides/Link_User_Account.md)를 참조합니다.                          | 항상    |
| `appliance`        | [ApplianceInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#ApplianceInfoObject)     | 대상 기기 정보를 담고 있는 객체. `applianceId` 필드는 필수입니다.     | 항상    |

### Message example

{% raw %}

```json
{
  "header": {
    "messageId": "8030275d-0e71-463d-b1d8-3e761e5389ad",
    "name": "StopRequest",
    "namespace": "ClovaHome",
    "payloadVersion": "1.0"
  },
  "payload": {
    "accessToken": "92ebcb67fe33",
    "appliance": {
      "applianceId": "device-016"
    }
  }
}
```

{% endraw %}

### See also
* [`StopConfirmation`](#StopConfirmation)

## TurnOffConfirmation {#TurnOffConfirmation}
[`TurnOffRequest`](#TurnOffRequest) 메시지에 대한 응답으로 대상 기기를 끄도록 요청한 후 처리된 결과를 CEK에게 전달합니다.

### Payload fields
없음

### Message example

{% raw %}

```json
{
  "header": {
    "messageId": "4ec35000-88ce-4724-b7e4-7f52050558fd",
    "name": "TurnOffConfirmation",
    "namespace": "ClovaHome",
    "payloadVersion": "1.0"
  },
  "payload": {}
}
```

{% endraw %}

### See also
* [`TurnOffRequest`](#TurnOffRequest)

## TurnOffRequest {#TurnOffRequest}
대상 기기를 끄도록 Clova Home extension에게 요청합니다. 이 요청에 대한 응답으로 [`TurnOffConfirmation`](#TurnOffConfirmation) 메시지를 사용해야 합니다.

### Payload fields

| 필드 이름       | 자료형    | 필드 설명                     | 포함 여부 |
|---------------|---------|-----------------------------|:---------:|
| `accessToken`      | string                                  | IoT 서비스의 사용자 계정의 access token. CEK는 외부 서비스의 인증 서버로부터 획득한 사용자 계정의 access token을 전달합니다. 자세한 설명은 [사용자 계정 연결하기](/CEK/Guides/Link_User_Account.md)를 참조합니다.                          | 항상    |
| `appliance`        | [ApplianceInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#ApplianceInfoObject)     | 대상 기기 정보를 담고 있는 객체. `applianceId` 필드는 필수입니다. | 항상    |

### Message example

{% raw %}

```json
{
  "header": {
    "messageId": "6c04fc2d-64dd-41a0-9162-7cb0d4cf7c08",
    "name": "TurnOffRequest",
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
* [`TurnOffConfirmation`](#TurnOffConfirmation)

## TurnOnConfirmation {#TurnOnConfirmation}
[`TurnOnRequest`](#TurnOnRequest) 메시지에 대한 응답으로 대상 기기를 켜도록 요청한 후 처리된 결과를 CEK에게 전달합니다.

### Payload fields
없음

### Message example

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

### See also
* [`TurnOnRequest`](#TurnOnRequest)

## TurnOnRequest {#TurnOnRequest}
대상 기기를 켜도록 Clova Home extension에게 요청합니다. 이 요청에 대한 응답으로 [`TurnOnConfirmation`](#TurnOnConfirmation) 메시지를 사용해야 합니다.

### Payload fields

| 필드 이름       | 자료형    | 필드 설명                     | 포함 여부 |
|---------------|---------|-----------------------------|:---------:|
| `accessToken`      | string                                  | IoT 서비스의 사용자 계정의 access token. CEK는 외부 서비스의 인증 서버로부터 획득한 사용자 계정의 access token을 전달합니다. 자세한 설명은 [사용자 계정 연결하기](/CEK/Guides/Link_User_Account.md)를 참조합니다.                          | 항상    |
| `appliance`        | [ApplianceInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#ApplianceInfoObject)     | 대상 기기 정보를 담고 있는 객체. `applianceId` 필드는 필수입니다. | 항상    |

### Message example

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

### See also
* [`TurnOnConfirmation`](#TurnOnConfirmation)

## UnmuteConfirmation {#UnmuteConfirmation}
[`UnmuteRequest`](#UnmuteRequest) 메시지에 대한 응답으로 대상 기기의 소리를 켜도록 설정(음소거 해제)한 결과를 CEK에게 전달합니다.

### Payload fields
없음

### Message example

{% raw %}

```json
{
  "header": {
    "messageId": "4ec35000-88ce-4724-b7e4-7f52050558fd",
    "name": "UnmuteConfirmation",
    "namespace": "ClovaHome",
    "payloadVersion": "1.0"
  },
  "payload": {}
}
```

{% endraw %}

### See also
* [`UnmuteRequest`](#UnmuteRequest)

## UnmuteRequest {#UnmuteRequest}
주로 TV나 셋톱박스와 같은 기기를 제어할 때 사용되며, 대상 기기의 소리를 켜도록(음소거 해제) Clova Home extension에게 요청합니다. 이 요청에 대한 응답으로 [`UnmuteConfirmation`](#UnmuteConfirmation) 메시지를 사용해야 합니다.

### Payload fields

| 필드 이름       | 자료형    | 필드 설명                     | 포함 여부 |
|---------------|---------|-----------------------------|:---------:|
| `accessToken`      | string                                  | IoT 서비스의 사용자 계정의 access token. CEK는 외부 서비스의 인증 서버로부터 획득한 사용자 계정의 access token을 전달합니다. 자세한 설명은 [사용자 계정 연결하기](/CEK/Guides/Link_User_Account.md)를 참조합니다.                          | 항상    |
| `appliance`        | [ApplianceInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#ApplianceInfoObject)     | 대상 기기 정보를 담고 있는 객체. `applianceId` 필드는 필수입니다. | 항상    |

### Message example

{% raw %}

```json
{
  "header": {
    "messageId": "6c04fc2d-64dd-41a0-9162-7cb0d4cf7c08",
    "name": "UnmuteRequest",
    "namespace": "ClovaHome",
    "payloadVersion": "1.0"
  },
  "payload": {
    "accessToken": "92ebcb67fe33",
    "appliance": {
      "applianceId": "device-005"
    }
  }
}
```

{% endraw %}

### See also
* [`UnmuteConfirmation`](#UnmuteConfirmation)
