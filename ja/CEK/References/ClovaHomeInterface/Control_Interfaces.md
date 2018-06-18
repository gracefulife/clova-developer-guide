# Control

IoTデバイスの情報の確認、デバイス操作のリクエストおよびレスポンスの際に使用されるインターフェースです。

| メッセージ         | タイプ  | 説明                                   |
|------------------|-----------|---------------------------------------------|
| [`ChargeConfirmation`](#ChargeConfirmation)                                   | Response | [`ChargeRequest`](#ChargeRequest)メッセージに対するレスポンスです。デバイスの充電を開始するように設定した結果をCEKに返します。 |
| [`ChargeRequest`](#ChargeRequest)                                             | Request  | デバイスの充電を開始するようClova Home Extensionにリクエストします。 |
| [`CloseConfirmation`](#CloseConfirmation)                                     | Response | [`CloseRequest`](#CloseRequest)メッセージに対するレスポンスです。スマートカーテンや温水洗浄便座の蓋を閉めるように設定した結果をCEKに返します。 |
| [`CloseRequest`](#CloseRequest)                                               | Request  | スマートカーテンや温水洗浄便座などのデバイスを制御する際に使用します。スマートカーテンや温水洗浄便座の蓋を閉めるようClova Home Extensionにリクエストします。  |
| [`DecrementBrightnessConfirmation`](#DecrementBrightnessConfirmation)         | Response | [`DecrementBrightnessRequest`](#DecrementBrightnessRequest)メッセージに対するレスポンスです。照明の輝度を下げるように設定した結果をCEKに返します。 |
| [`DecrementBrightnessRequest`](#DecrementBrightnessRequest)                   | Request  | 照明の輝度を指定された値に下げるようClova Home Extensionにリクエストします。 |
| [`DecrementChannelConfirmation`](#DecrementChannelConfirmation)               | Response | [`DecrementChannelRequest`](#DecrementChannelRequest)メッセージに対するレスポンスです。テレビのチャンネルを下げるように設定した結果をCEKに返します。 |
| [`DecrementChannelRequest`](#DecrementChannelRequest)                         | Request  | テレビのチャンネルを指定された値に下げるようClova Home Extensionにリクエストします。 |
| [`DecrementFanSpeedConfirmation`](#DecrementFanSpeedConfirmation)             | Response | [`DecrementFanSpeedRequest`](#DecrementFanSpeedRequest)メッセージに対するレスポンスです。ファンの速度を下げるように設定した結果をCEKに返します。 |
| [`DecrementFanSpeedRequest`](#DecrementFanSpeedRequest)                       | Request  | ファンの速度を指定された値に下げるようClova Home Extensionにリクエストします。 |
| [`DecrementIntensityLevelConfirmation`](#DecrementIntensityLevelConfirmation) | Response | [`DecrementIntensityLevelRequest`](#DecrementIntensityLevelRequest)メッセージに対するレスポンスです。圧力や水圧などの強度を下げるように設定した結果をCEKに返します。  |
| [`DecrementIntensityLevelRequest`](#DecrementIntensityLevelRequest)           | Request  | 主にエアコンやサーモスタットのようなデバイスの制御に使用します。圧力や水圧の強度を指定された値に下げるようClova Home Extensionにリクエストします。  |
| [`DecrementTargetTemperatureConfirmation`](#DecrementTargetTemperatureConfirmation) | Response | [`DecrementTargetTemperatureRequest`](#DecrementTargetTemperatureRequest)メッセージに対するレスポンスです。温度を下げるように設定した結果をCEKに返します。 |
| [`DecrementTargetTemperatureRequest`](#DecrementTargetTemperatureRequest)     | Request  | 設定温度を指定された値に下げるようClova Home Extensionにリクエストします。      |
| [`DecrementVolumeConfirmation`](#DecrementVolumeConfirmation)                 | Response | [`DecrementVolumeRequest`](#DecrementVolumeRequest)メッセージに対するレスポンスです。スピーカーの音量を下げるように設定した結果をCEKに返します。 |
| [`DecrementVolumeRequest`](#DecrementVolumeRequest)                           | Request  | スピーカーの音量を下げるようClova Home Extensionにリクエストします。 |
| [`GetAirQualityRequest`](#GetAirQualityRequest)                               | Request  | デバイスで測定された空気質情報をClova Home Extensionにリクエストします。 |
| [`GetAirQualityResponse`](#GetAirQualityResponse)                             | Response | [`GetAirQualityRequest`](#GetAirQualityRequest)メッセージに対するレスポンスです。デバイスで測定された空気質情報をCEKに返します。 |
| [`GetAsleepDurationRequest`](#GetAsleepDurationRequest)                       | Request  | 主に睡眠センサーで測定された情報を確認する際に使用します。デバイスで測定されたユーザーの睡眠時間をClova Home Extensionにリクエストします。  |
| [`GetAsleepDurationResponse`](#GetAsleepDurationResponse)                     | Response | [`GetAsleepDurationRequest`](#GetAsleepDurationRequest)メッセージに対するレスポンスです。デバイスで測定されたユーザーの睡眠時間をCEKに返します。  |
| [`GetAwakeDurationRequest`](#GetAwakeDurationRequest)                         | Request  | 主に睡眠センサーで測定された情報を確認する際に使用します。デバイスで測定されたユーザーの入眠潜時、つまりユーザーが就寝してから睡眠状態に入るまでの時間をClova Home Extensionにリクエストします。  |
| [`GetAwakeDurationResponse`](#GetAwakeDurationResponse)                       | Response | [`GetAwakeDurationRequest`](#GetAwakeDurationRequest)メッセージに対するレスポンスです。デバイスで測定されたユーザーの入眠潜時、つまりユーザーが就寝してから睡眠状態に入るまでの時間をCEKに返します。  |
| [`GetBatteryInfoRequest`](#GetBatteryInfoRequest)                             | Request  | デバイスの電池の情報をClova Home Extensionにリクエストします。 |
| [`GetBatteryInfoResponse`](#GetBatteryInfoResponse)                           | Response | [`GetBatteryInfoRequest`](#GetBatteryInfoRequest)メッセージに対するレスポンスです。デバイスの電池の情報をCEKに返します。 |
| [`GetCleaningCycleRequest`](#GetCleaningCycleRequest)                                                   | Request  | デバイスをクリーニングする周期を確認する際に使用します。デバイスの次のクリーニング周期までの残り時間をClova Home extensionにリクエストします。  |
| [`GetCleaningCycleResponse`](#GetCleaningCycleResponse)                                                  | Response | [`GetCleaningCycleRequest`](#GetCleaningCycleRequest)メッセージに対するレスポンスです。デバイスの次のクリーニング周期までの残り時間をCEKに返します。  |
| [`GetCloseTimeRequest`](#GetCloseTimeRequest)                                 | Request  | 開閉センサーで検知された開閉状況のうち、検知対象が最後に閉まったときの日時情報をClova Home Extensionにリクエストします。 |
| [`GetCloseTimeResponse`](#GetCloseTimeResponse)                               | Response | [`GetCloseTimeRequest`](#GetCloseTimeRequest)メッセージに対するレスポンスです。開閉センサーの検知対象が最後に閉まったときの日時情報をCEKに返します。  |
| [`GetConsumptionRequest`](#GetConsumptionRequest)                             | Request  | 主にスマートプラグやスマートテーブルタップのようなデバイスで測定された、現在までのエネルギーまたはリソースを確認する際に使用します。測定されたエネルギーまたはリソースの情報をClova Home Extensionにリクエストします。  |
| [`GetConsumptionResponse`](#GetConsumptionResponse)                           | Response | [`GetConsumptionRequest`](#GetConsumptionRequest)メッセージに対するレスポンスです。現在まで測定されたエネルギーまたはリソースの情報をCEKに返します。  |
| [`GetCurrentBillRequest`](#GetCurrentBillRequest)                             | Request  | 主にスマートプラグやスマートテーブルタップのようなデバイスで測定された、現在までのエネルギー使用量に基づいた利用料金を確認する際に使用します。測定された料金情報をClova Home Extensionにリクエストします。  |
| [`GetCurrentBillResponse`](#GetCurrentBillResponse)                           | Response | [`GetCurrentBillRequest`](#GetCurrentBillRequest)メッセージに対するレスポンスです。現在まで測定された料金情報をCEKに返します。   |
| [`GetCurrentTemperatureRequest`](#GetCurrentTemperatureRequest)               | Request  | 現在の温度をClova Home Extensionにリクエストします。 |
| [`GetCurrentTemperatureResponse`](#GetCurrentTemperatureResponse)             | Response | [`GetCurrentTemperatureRequest`](#GetCurrentTemperatureRequest)メッセージに対するレスポンスです。デバイスで測定された現在の温度をCEKに返します。 |
| [`GetDeviceStateRequest`](#GetDeviceStateRequest)                             | Request  | デバイスが提供するすべてのステータス情報を確認する際に使用します。  |
| [`GetDeviceStateResponse`](#GetDeviceStateResponse)                           | Response | [`GetDeviceStateRequest`](#GetDeviceStateRequest)メッセージに対するレスポンスです。デバイスが提供するすべてのステータス情報をCEKに返します。  |
| [`GetEstimateBillRequest`](#GetEstimateBillRequest)                           | Request  | 主にスマートプラグやスマートテーブルタップのようなデバイスで測定されたエネルギー使用量に基づいて、利用料金を推定する際に使用します。推定された料金情報をClova Home Extensionにリクエストします。  |
| [`GetEstimateBillResponse`](#GetEstimateBillResponse)                         | Response | [`GetEstimateBillRequest`](#GetEstimateBillRequest)メッセージに対するレスポンスです。推定された料金情報をCEKに返します。  |
| [`GetExpendableStateRequest`](#GetExpendableStateRequest)                     | Request  | フィルターなど、デバイスの消耗品の使用量や残り寿命を確認する際に使用します。デバイスが持つ消耗品の使用量や寿命情報をリクエストします。  |
| [`GetExpendableStateResponse`](#GetExpendableStateResponse)                   | Response | [`GetExpendableStateRequest`](#GetExpendableStateRequest)メッセージに対するレスポンスです。デバイスが提供するすべての消耗品の使用量や寿命情報をCEKに返します。 |
| [`GetFineDustRequest`](#GetFineDustRequest)                                   | Request  | デバイスで測定された微細粉塵(PM10)の情報をClova Home Extensionにリクエストします。 |
| [`GetFineDustResponse`](#GetFineDustResponse)                                 | Response | [`GetFineDustRequest`](#GetFineDustRequest)メッセージに対するレスポンスです。デバイスで測定された微細粉塵(PM10)の情報をCEKに返します。 |
| [`GetHumidityRequest`](#GetHumidityRequest)                                   | Request  | デバイスで測定された湿度をClova Home Extensionにリクエストします。 |
| [`GetHumidityResponse`](#GetHumidityResponse)                                 | Response | [`GetHumidityRequest`](#GetHumidityRequest)メッセージに対するレスポンスです。デバイスで測定された湿度をCEKに返します。 |
| [`GetKeepWarmTimeRequest`](#GetKeepWarmTimeRequest)                           | Request  | 炊飯器のようなデバイスで、食べ物が保温された時間を確認する際に使用します。デバイスで保温モードが維持された時間の情報をClova Home Extensionにリクエストします。  |
| [`GetKeepWarmTimeResponse`](#GetKeepWarmTimeResponse)                         | Response | [`GetKeepWarmTimeRequest`](#GetKeepWarmTimeRequest)メッセージに対するレスポンスです。保温モードが維持された時間の情報をCEKに返します。  |
| [`GetLockStateRequest`](#GetLockStateRequest)                                 | Request  | 主にスマートバルブなどのデバイスの状態を確認する際に使用します。デバイスが持っているロック装置の現在のロック状態をClova Home Extensionにリクエストします。  |
| [`GetLockStateResponse`](#GetLockStateResponse)                               | Response | [`GetLockStateRequest`](#GetLockStateRequest)メッセージに対するレスポンスです。デバイスが持っているロック装置の現在のロック状態をCEKに返します。  |
| [`GetOpenStateRequest`](#GetOpenStateRequest)                                 | Request  | 主に開閉センサーで検知された開閉状況のうち、検知対象の現在の状態(開いている/閉まっている)をClova Home Extensionにリクエストします。  |
| [`GetOpenStateResponse`](#GetOpenStateResponse)                               | Response | [`GetOpenStateRequest`](#GetOpenStateRequest)メッセージに対するレスポンスです。主に検知対象の現在の状態(開いている/閉まっている)をCEKに返します。  |
| [`GetOpenTimeRequest`](#GetOpenTimeRequest)                                   | Request  | 主に開閉センサーで検知された開閉状況のうち、検知対象が最後に開いたときの日時情報をClova Home Extensionにリクエストします。   |
| [`GetOpenTimeResponse`](#GetOpenTimeResponse)                                 | Response | [`GetOpenTimeRequest`](#GetOpenTimeRequest)メッセージに対するレスポンスです。開閉センサーの検知対象が最後に開いたときの日時情報をCEKに返します。  |
| [`GetPhaseRequest`](#GetPhaseRequest)                                         | Request  | 主に炊飯器や洗濯機など、動作に段階があるデバイスで、現在の動作段階を確認する際に使用します。デバイスの現在の動作段階をClova Home Extensionにリクエストします。  |
| [`GetPhaseResponse`](#GetPhaseResponse)                                       | Response | [`GetPhaseRequest`](#GetPhaseRequest)メッセージに対するレスポンスです。デバイスの現在の動作段階をCEKに返します。  |
| [`GetProgressiveTaxBracketRequest`](#GetProgressiveTaxBracketRequest)         | Request  | 主に電力量計やスマートプラグなどのデバイスで、累進税の段階を確認する際に使用します。判断された累進税の段階をClova Home Extensionにリクエストします。  |
| [`GetProgressiveTaxBracketResponse`](#GetProgressiveTaxBracketResponse)         | Response | [`GetProgressiveTaxBracketRequest`](#GetProgressiveTaxBracketRequest)メッセージに対するレスポンスです。デバイスで判断された累進税の段階情報をCEKに返します。 |
| [`GetRemainingTimeRequest`](#GetRemainingTimeRequest)                         | Request  | 主に炊飯器や洗濯機のようなデバイスで、動作終了までの残り時間を確認する際に使用します。デバイスの動作終了までの残り時間をClova Home Extensionにリクエストします。  |
| [`GetRemainingTimeResponse`](#GetRemainingTimeResponse)                       | Response | [`GetRemainingTimeRequest`](#GetRemainingTimeRequest)メッセージに対するレスポンスです。デバイスの動作終了までの残り時間をCEKに返します。 |
| [`GetRightPostureRatioRequest`](#GetRightPostureRatioRequest)                 | Request  | ユーザーが正しい姿勢でデバイスを使用した割合を確認する際に使用します。ユーザーがデバイスを使用する際、特定の期間または現在まで正しい姿勢を保った割合の情報をClova Home Extensionにリクエストします。  |
| [`GetRightPostureRatioResponse`](#GetRightPostureRatioResponse)               | Response | [`GetRightPostureRatioRequest`](#GetRightPostureRatioRequest)メッセージに対するレスポンスです。ユーザーが正しい姿勢でデバイスを使用した割合をCEKに返します。  |
| [`GetCurrentSittingStateRequest`](#GetCurrentSittingStateRequest)             | Request  | スマートチェアなどのデバイスで、ユーザーの使用状況を確認する際に使用します。デバイスで検知されたユーザーの着席情報と、直近でユーザーがデバイスを使用した時間の情報をClova Home Extensionにリクエストします。  |
| [`GetCurrentSittingStateResponse`](#GetCurrentSittingStateResponse)           | Response | [`GetCurrentSittingStateRequest`](#GetCurrentSittingStateRequest)メッセージに対するレスポンスです。デバイスで検知されたユーザーの着席情報と、直近でユーザーがデバイスを使用した時間の情報をCEKに返します。  |
| [`GetSleepScoreRequest`](#GetSleepScoreRequest)                               | Request  | 睡眠センサーのようなデバイスで、ユーザーの睡眠スコアの情報を確認する際に使用します。デバイスで評価されたユーザーの睡眠スコアをClova Home Extensionにリクエストします。  |
| [`GetSleepScoreResponse`](#GetSleepScoreResponse)                             | Response | [`GetSleepScoreRequest`](#GetSleepScoreRequest)メッセージに対するレスポンスです。デバイスで評価されたユーザーの睡眠スコアをCEKに返します。  |
| [`GetSleepStartTimeRequest`](#GetSleepStartTimeRequest)                       | Request  | 睡眠センサーのようなデバイスで、ユーザーの睡眠スコアの情報を確認する際に使用します。デバイスで測定されたユーザーの睡眠開始時間をClova Home Extensionにリクエストします。  |
| [`GetSleepStartTimeResponse`](#GetSleepStartTimeRequest)                      | Response | [`GetSleepStartTimeRequest`](#GetSleepStartTimeRequest)メッセージに対するレスポンスです。デバイスで測定されたユーザーの睡眠開始時間をCEKに返します。  |
| [`GetTargetTemperatureRequest`](#GetTargetTemperatureRequest)                 | Request  | デバイスの設定温度をClova Home Extensionにリクエストします。 |
| [`GetTargetTemperatureResponse`](#GetTargetTemperatureResponse)               | Response | [`GetTargetTemperatureRequest`](#GetTargetTemperatureRequest)メッセージに対するレスポンスです。デバイスの設定温度をCEKに返します。 |
| [`GetUltraFineDustRequest`](#GetUltraFineDustRequest)                         | Request  | デバイスで測定された超微細粉塵(PM2.5)の情報をClova Home Extensionにリクエストします。 |
| [`GetUltraFineDustResponse`](#GetUltraFineDustResponse)                       | Response | [`GetUltraFineDustRequest`](#GetUltraFineDustRequest)メッセージに対するレスポンスです。デバイスで測定された超微細粉塵(PM2.5)の情報をCEKに返します。 |
| [`GetUsageTimeRequest`](#GetUsageTimeRequest)                                 | Request | デバイスの使用時間を確認する際に使用します。特定の期間または現在までの累積使用時間をClova Home Extensionにリクエストします。  |
| [`GetUsageTimeResponse`](#GetUsageTimeResponse)                               | Response | [`GetUsageTimeRequest`](#GetUsageTimeRequest)メッセージに対するレスポンスです。デバイスの累積使用時間をCEKに返します。  |
| [`HealthCheckRequest`](#HealthCheckRequest)                                   | Request  | デバイスのステータスを把握する際に使用します。デバイスのステータス情報をClova Home Extensionにリクエストします。 |
| [`HealthCheckResponse`](#HealthCheckResponse)                                 | Response | [`HealthCheckRequest`](#HealthCheckRequest)メッセージに対するレスポンスです。デバイスのステータス情報をCEKに返します。 |
| [`IncrementBrightnessConfirmation`](#IncrementBrightnessConfirmation)         | Response | [`IncrementBrightnessRequest`](#IncrementBrightnessRequest)メッセージに対するレスポンスです。照明の輝度を上げるように設定した結果をCEKに返します。 |
| [`IncrementBrightnessRequest`](#IncrementBrightnessRequest)                   | Request  | 照明の輝度を指定された値に上げるようClova Home Extensionにリクエストします。 |
| [`IncrementChannelConfirmation`](#IncrementChannelConfirmation)               | Response | [`IncrementChannelRequest`](#IncrementChannelRequest)メッセージに対するレスポンスです。テレビのチャンネルを上げるように設定した結果をCEKに返します。 |
| [`IncrementChannelRequest`](#IncrementChannelRequest)                         | Request  | テレビのチャンネルを指定された値に上げるようClova Home Extensionにリクエストします。 |
| [`IncrementFanSpeedConfirmation`](#IncrementFanSpeedConfirmation)             | Response | [`IncrementFanSpeedRequest`](#IncrementFanSpeedRequest)メッセージに対するレスポンスです。ファンの速度を上げるように設定した結果をCEKに返します。 |
| [`IncrementFanSpeedRequest`](#IncrementFanSpeedRequest)                       | Request | ファンの速度を指定された値に上げるようClova Home Extensionにリクエストします。 |
| [`IncrementIntensityLevelConfirmation`](#IncrementIntensityLevelConfirmation) | Response | [`DecrementIntensityLevelRequest`](#DecrementIntensityLevelRequest)メッセージに対するレスポンスです。圧力や水圧などの強度を上げるように設定した結果をCEKに返します。  |
| [`IncrementIntensityLevelRequest`](#IncrementIntensityLevelRequest)           | Request  | 圧力や水圧などの強度を指定された値に上げるようClova Home Extensionにリクエストします。 |
| [`IncrementTargetTemperatureConfirmation`](#IncrementTargetTemperatureConfirmation) | Response | [`IncrementTargetTemperatureRequest`](#IncrementTargetTemperatureRequest)メッセージに対するレスポンスです。温度を上げるように設定した結果をCEKに返します。 |
| [`IncrementTargetTemperatureRequest`](#IncrementTargetTemperatureRequest)     | Request  | 温度を指定された値に上げるようClova Home Extensionにリクエストします。     |
| [`IncrementVolumeConfirmation`](#IncrementVolumeConfirmation)                 | Response | [`IncrementVolumeRequest`](#IncrementVolumeRequest)メッセージに対するレスポンスです。スピーカーの音量を上げるように設定した結果をCEKに返します。 |
| [`IncrementVolumeRequest`](#IncrementVolumeRequest)                           | Request | スピーカーの音量を指定された値に上げるようClova Home Extensionにリクエストします。 |
| [`LowerConfirmation`](#LowerConfirmation)                                     | Response | [`LowerRequest`](#LowerRequest)メッセージに対するレスポンスです。デバイスの高さを下げるように設定した結果をCEKに返します。  |
| [`LowerRequest`](#LowerRequest)                                               | Request  | 主にカーテンやブラインド、ベッドなどのデバイスを制御する際に使用します。デバイスの高さを下げるようClova Home Extensionにリクエストします。  |
| [`MuteConfirmation`](#MuteConfirmation)                                       | Response | [`MuteRequest`](#MuteRequest)メッセージに対するレスポンスです。デバイスの音をミュートにするように設定した結果をCEKに返します。 |
| [`MuteRequest`](#MuteRequest)                                                 | Request  | デバイスの音をミュートにするようClova Home Extensionにリクエストします。 |
| [`OpenConfirmation`](#OpenConfirmation)                                       | Response | [`OpenRequest`](#OpenRequest)メッセージに対するレスポンスです。スマートカーテンや温水洗浄便座の蓋を開けるように設定した結果をCEKに返します。 |
| [`OpenRequest`](#OpenRequest)                                                 | Request  | スマートカーテンや温水洗浄便座などのデバイスを制御する際に使用します。スマートカーテンや温水洗浄便座の蓋を開けるようClova Home Extensionにリクエストします。  |
| [`RaiseConfirmation`](#RaiseConfirmation)                                     | Response | [`RaiseRequest`](#RaiseRequest)メッセージに対するレスポンスです。デバイスの高さを上げるように設定した結果をCEKに返します。  |
| [`RaiseRequest`](#RaiseRequest)                                               | Request  | 主にカーテンやブラインド、ベッドなどのデバイスを制御する際に使用します。デバイスの高さを上げるようClova Home Extensionにリクエストします。  |
| [`ReleaseModeConfirmation`](#ReleaseModeConfirmation)                         | Response | [`ReleaseModeRequest`](#ReleaseModeRequest)メッセージに対するレスポンスです。デバイスの現在の運転モード(operation mode)を解除するように設定した結果をCEKに返します。  |
| [`ReleaseModeRequest`](#ReleaseModeRequest)                                   | Request  | 現在、デバイスに設定されている運転モード(operation mode)を解除する際に使用します。デバイスの運転モードを解除し、前の運転モードまたはデフォルトの運転モードに戻るようにClova Home Extensionにリクエストします。  |
| [`SetBrightnessConfirmation`](#SetBrightnessConfirmation)                     | Response | [`SetBrightnessRequest`](#SetBrightnessRequest)メッセージに対するレスポンスです。照明の輝度を変更するように設定した結果をCEKに返します。 |
| [`SetBrightnessRequest`](#SetBrightnessRequest)                               | Request  | 照明の輝度を指定された値に変更するようClova Home Extensionにリクエストします。 |
| [`SetChannelByNameConfirmation`](#SetChannelByNameConfirmation)               | Response | [`SetChannelByNameRequest`](#SetChannelByNameRequest)メッセージに対するレスポンスです。指定されたチャンネル名にテレビのチャンネルを変更するように設定した結果をCEKに返します。 |
| [`SetChannelByNameRequest`](#SetChannelByNameRequest)                         | Request  | 指定されたチャンネル名にチャンネルを変更するようClova Home Extensionにリクエストします。 |
| [`SetChannelConfirmation`](#SetChannelConfirmation)                           | Response | [`SetChannelRequest`](#SetChannelRequest)メッセージに対するレスポンスです。指定されたチャンネル番号にテレビのチャンネルを変更するように設定した結果をCEKに返します。 |
| [`SetChannelRequest`](#SetChannelRequest)                                     | Request  | 指定されたチャンネル番号にテレビのチャンネルを変更するようClova Home Extensionにリクエストします。 |
| [`SetColorConfirmation`](#SetColorConfirmation)                               | Response | [`SetColorRequest`](#SetColorRequest)メッセージに対するレスポンスです。照明や画面、電球の色を変更するように設定した結果をCEKに返します。 |
| [`SetColorRequest`](#SetColorRequest)                                         | Request  | 主にスマート照明などのデバイスを制御する際に使用します。照明や画面、電球の色を変更するようClova Home Extensionにリクエストします。  |
| [`SetColorTemperatureConfirmation`](#SetColorTemperatureConfirmation)         | Response | [`SetColorTemperatureRequest`](#SetColorTemperatureRequest)メッセージに対するレスポンスです。照明や画面、電球の色温度を変更するように設定した結果をCEKに返します。  |
| [`SetColorTemperatureRequest`](#SetColorTemperatureRequest)                   | Request  | 主にスマート照明などのデバイスを制御する際に使用します。照明や画面、電球の色温度を変更するようClova Home extensionにリクエストします。  |
| [`SetFanSpeedConfirmation`](#SetFanSpeedConfirmation)                         | Response | [`SetFanSpeedRequest`](#SetFanSpeedRequest)メッセージに対するレスポンスです。ファンの速度を変更するように設定した結果をCEKに返します。 |
| [`SetFanSpeedRequest`](#SetFanSpeedRequest)                                   | Request  | ファンの速度を指定された値に変更するようClova Home extensionにリクエストします。 |
| [`SetFreezerTargetTemperatureConfirmation`](#SetFreezerTargetTemperatureConfirmation)  | Response  |  [`SetFreezerTargetTemperatureRequest`](#SetFreezerTargetTemperatureRequest)メッセージに対するレスポンスです。冷凍室の設定温度を変更するように設定した結果をCEKに返します。 |
| [`SetFreezerTargetTemperatureRequest`](#SetFreezerTargetTemperatureRequest)   | Request  | 冷蔵庫などのデバイスを制御する際に使用します。冷凍庫の設定温度を指定された値に変更するようClova Home extensionにリクエストします。  |
| [`SetFridgeTargetTemperatureConfirmation`](#SetFridgeTargetTemperatureConfirmation) | Response | [`SetFridgeTargetTemperatureRequest`](#SetFridgeTargetTemperatureRequest)メッセージに対するレスポンスです。冷蔵室の設定温度を変更するように設定した結果をCEKに返します。  |
| [`SetFridgeTargetTemperatureRequest`](#SetFridgeTargetTemperatureRequest)     | Request  | 冷蔵庫などのデバイスを制御する際に使用します。冷蔵室の設定温度を指定された値に変更するようClova Home extensionにリクエストします。  |
| [`SetLockStateConfirmation`](#SetLockStateConfirmation)                       | Response | [`SetLockStateRequest`](#SetLockStateRequest)メッセージに対するレスポンスです。デバイスの開閉を設定した結果をCEKに返します。  |
| [`SetLockStateRequest`](#SetLockStateRequest)                                 | Request  | デバイスの開閉をClova Home extensionにリクエストします。  |
| [`SetModeConfirmation`](#SetModeConfirmation)                                 | Response | [`SetModeRequest`](#SetModeRequest)メッセージに対するレスポンスです。運転モード(operation mode)を変更するように設定した結果をCEKに返します。 |
| [`SetModeRequest`](#SetModeRequest)                                           | Request  | デバイスの運転モードを指定されたモードに変更するようClova Home extensionにリクエストします。 |
| [`SetTargetTemperatureConfirmation`](#SetTargetTemperatureConfirmation)       | Response | [`SetTargetTemperatureRequest`](#SetTargetTemperatureRequest)メッセージに対するレスポンスです。設定温度変更のリクエストを処理した結果をCEKに返します。 |
| [`SetTargetTemperatureRequest`](#SetTargetTemperatureRequest)                 | Request  | 設定温度を指定された値に変更するようClova Home extensionにリクエストします。 |
| [`StopConfirmation`](#StopConfirmation)                                       | Response | [`StopRequest`](#StopRequest)メッセージに対するレスポンスです。動作中止のリクエストを処理した結果をCEKに返します。  |
| [`StopRequest`](#StopRequest)                                                 | Request  | デバイスの現在の動作を中止するようClova Home extensionにリクエストします。  |
| [`TurnOffConfirmation`](#TurnOffConfirmation)                                 | Response | [`TurnOffRequest`](#TurnOffRequest)メッセージに対するレスポンスです。デバイスの電源をオフにするように設定した結果をCEKに返します。 |
| [`TurnOffRequest`](#TurnOffRequest)                                           | Request  | デバイスの電源をオフにするようClova Home extensionにリクエストします。                        |
| [`TurnOnConfirmation`](#TurnOnConfirmation)                                   | Response | [`TurnOnRequest`](#TurnOnRequest)メッセージに対するレスポンスです。デバイスの電源をオンにするように設定した結果をCEKに返します。 |
| [`TurnOnRequest`](#TurnOnRequest)                                             | Request  | デバイスの電源をオンにするようClova Home extensionにリクエストします。                        |
| [`UnmuteConfirmation`](#UnmuteConfirmation)                                   | Response | [`UnmuteRequest`](#UnmuteRequest)メッセージに対するレスポンスです。デバイスのミュートを解除するように設定した結果をCEKに返します。 |
| [`UnmuteRequest`](#UnmuteRequest)                                             | Request  | デバイスのミュートを解除するようClova Home extensionにリクエストします。 |

## ChargeConfirmation {#ChargeConfirmation}
[`ChargeRequest`](#ChargeRequest)メッセージに対するレスポンスです。デバイスの充電を開始するように設定した結果をCEKに返します。

### Payload fields

なし

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

### 次の項目も参照してください。
* [`ChargeRequest`](#ChargeRequest)

## ChargeRequest {#ChargeRequest}
主にロボット掃除機を制御する際に使用します。デバイスの充電を開始するようClova Home Extensionにリクエストします。このリクエストに対するレスポンスとして、[`ChargeConfirmation`](#ChargeConfirmation)メッセージを使用する必要があります。

### Payload fields

| フィールド名       | データ型    | フィールドの説明                     | 任意 |
|---------------|---------|-----------------------------|:---------:|
| `accessToken`      | string                                  | IoTサービスのユーザーアカウントのアクセストークン。CEKは、外部サービスの認可サーバーから取得したユーザーアカウントのアクセストークンを渡します。詳細については、[ユーザーアカウントをリンクする](/CEK/Guides/Link_User_Account.md)を参照してください。                          | 常時    |
| `appliance`        | [ApplianceInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#ApplianceInfoObject)     | エンドポイントの情報を持つオブジェクト。`applianceId`フィールドは必須です。     | 常時    |

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

### 次の項目も参照してください。
* [`ChargeConfirmation`](#ChargeConfirmation)

## CloseConfirmation {#CloseConfirmation}
[`CloseRequest`](#CloseRequest)メッセージに対するレスポンスです。スマートカーテンや温水洗浄便座の蓋を閉めるように設定した結果をCEKに返します。

### Payload fields

なし

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

### 次の項目も参照してください。
* [`CloseRequest`](#CloseRequest)

## CloseRequest {#CloseRequest}
スマートカーテンや温水洗浄便座などのデバイスを制御する際に使用します。スマートカーテンや温水洗浄便座の蓋を閉めるようClova Home Extensionにリクエストします。このリクエストに対するレスポンスとして、[`CloseConfirmation`](#CloseConfirmation)メッセージを使用する必要があります。

### Payload fields

| フィールド名       | データ型    | フィールドの説明                     | 任意 |
|---------------|---------|-----------------------------|:---------:|
| `accessToken`      | string                                  | IoTサービスのユーザーアカウントのアクセストークン。CEKは、外部サービスの認可サーバーから取得したユーザーアカウントのアクセストークンを渡します。詳細については、[ユーザーアカウントをリンクする](/CEK/Guides/Link_User_Account.md)を参照してください。                          | 常時    |
| `appliance`        | [ApplianceInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#ApplianceInfoObject)     | エンドポイントの情報を持つオブジェクト。`applianceId`フィールドは必須です。     | 常時    |

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

### 次の項目も参照してください。
* [`CloseConfirmation`](#CloseConfirmation)

## DecrementBrightnessConfirmation {#DecrementBrightnessConfirmation}
[`DecrementBrightnessRequest`](#DecrementBrightnessRequest)メッセージに対するレスポンスです。照明の輝度を下げるように設定した結果をCEKに返します。

### Payload fields

| フィールド名       | データ型    | フィールドの説明                     | 必須/選択 |
|---------------|---------|-----------------------------|:---------:|
| `brightness`               | [BrightnessInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#BrightnessInfoObject) | 現在の輝度情報を持つオブジェクト                                | 選択    |
| `previousState`            | object | エンドポイントの前の状況情報を持つオブジェクト                           | 選択    |
| `previousState.brightness` | [BrightnessInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#BrightnessInfoObject) | 前の輝度情報を持つオブジェクト                                | 選択    |

### 備考

エンドポイントからペイロードに入力する情報を取得できない場合、値を省略できます。その場合、ユーザーには具体的な情報なしに、リクエストが正常に処理されたことを通知します。

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

### 次の項目も参照してください。
* [`DecrementBrightnessRequest`](#DecrementBrightnessRequest)

## DecrementBrightnessRequest {#DecrementBrightnessRequest}
主に照明などのデバイスを制御する際に使用します。照明の輝度を指定された値に下げるようClova Home Extensionにリクエストします。このリクエストに対するレスポンスとして、[`DecrementBrightnessConfirmation`](#DecrementBrightnessConfirmation)メッセージを使用する必要があります。

### Payload fields

| フィールド名       | データ型    | フィールドの説明                     | 任意 |
|---------------|---------|-----------------------------|:---------:|
| `accessToken`      | string                                  | IoTサービスのユーザーアカウントのアクセストークン。CEKは、外部サービスの認可サーバーから取得したユーザーアカウントのアクセストークンを渡します。詳細については、[ユーザーアカウントをリンクする](/CEK/Guides/Link_User_Account.md)を参照してください。                          | 常時    |
| `appliance`        | [ApplianceInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#ApplianceInfoObject)     | エンドポイントの情報を持つオブジェクト。`applianceId`フィールドは必須です。     | 常時    |
| `deltaBrightness`       | [BrightnessInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#BrightnessInfoObject)             | 変更する輝度情報を持つオブジェクト                              | 常時    |

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

### 次の項目も参照してください。
* [`DecrementBrightnessConfirmation`](#DecrementBrightnessConfirmation)

## DecrementChannelConfirmation {#DecrementChannelConfirmation}
[`DecrementChannelRequest`](#DecrementChannelRequest)メッセージに対するレスポンスです。テレビのチャンネルを下げるように設定した結果をCEKに返します。

### Payload fields

| フィールド名       | データ型    | フィールドの説明                     | 必須/選択 |
|---------------|---------|-----------------------------|:---------:|
| `channel`               | [TVChannelInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#TVChannelInfoObject) | 現在のテレビチャンネルの情報を持つオブジェクト                                | 選択    |
| `previousState`            | object | エンドポイントの前の状況情報を持つオブジェクト                           | 選択    |
| `previousState.channel` | [TVChannelInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#TVChannelInfoObject) | 前のテレビチャンネル情報を持つオブジェクト                                | 選択    |

### 備考

エンドポイントからペイロードに入力する情報を取得できない場合、値を省略できます。その場合、ユーザーには具体的な情報なしに、リクエストが正常に処理されたことを通知します。

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
    "previousState": {
      "channel": {
        "value": 13
      }
    }
  }
}
```
{% endraw %}

### 次の項目も参照してください。
* [`DecrementChannelRequest`](#DecrementChannelRequest)

## DecrementChannelRequest {#DecrementChannelRequest}
主にテレビやセットトップボックスを制御する際に使用します。テレビのチャンネルを指定された値に下げるようClova Home Extensionにリクエストします。このリクエストに対するレスポンスとして、[`DecrementChannelConfirmation`](#DecrementChannelConfirmation)メッセージを使用する必要があります。

### Payload fields

| フィールド名       | データ型    | フィールドの説明                     | 任意 |
|---------------|---------|-----------------------------|:---------:|
| `accessToken`      | string                                  | IoTサービスのユーザーアカウントのアクセストークン。CEKは、外部サービスの認可サーバーから取得したユーザーアカウントのアクセストークンを渡します。詳細については、[ユーザーアカウントをリンクする](/CEK/Guides/Link_User_Account.md)を参照してください。                          | 常時    |
| `appliance`        | [ApplianceInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#ApplianceInfoObject)     | エンドポイントの情報を持つオブジェクト。`applianceId`フィールドは必須です。     | 常時    |
| `deltaChannel`       | [TVChannelInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#TVChannelInfoObject)             | 変更するテレビチャンネルの値を持つオブジェクト                              | 常時    |

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

### 次の項目も参照してください。
* [`DecrementChannelConfirmation`](#DecrementChannelConfirmation)

## DecrementFanSpeedConfirmation {#DecrementFanSpeedConfirmation}
[`DecrementFanSpeedRequest`](#DecrementFanSpeedRequest)メッセージに対するレスポンスです。ファンの速度を下げるように設定した結果をCEKに返します。

### Payload fields

| フィールド名       | データ型    | フィールドの説明                     | 必須/選択 |
|---------------|---------|-----------------------------|:---------:|
| `fanSpeed`       | [SpeedInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#SpeedInfoObject)             | 現在のファンの速度情報を持つオブジェクト。ファンの速度とは風速のことで、次のいずれかになります。<ul><li><code>1</code>：弱風(1段階)</li><li><code>2</code>：中風(2段階)</li><li><code>3</code>：強風(3段階)</li></ul> | 選択    |
| `previousState`     | object                                  | エンドポイントの前の状況情報を持つオブジェクト                           | 選択    |
| `previousState.fanSpeed` | [SpeedInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#SpeedInfoObject)     | 前のファンの速度情報を持つオブジェクト。ファンの速度とは風速のことで、次のいずれかになります。<ul><li><code>1</code>：弱風(1段階)</li><li><code>2</code>：中風(2段階)</li><li><code>3</code>：強風(3段階)</li></ul> | 選択    |

### 備考

エンドポイントからペイロードに入力する情報を取得できない場合、値を省略できます。その場合、ユーザーには具体的な情報なしに、リクエストが正常に処理されたことを通知します。

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

### 次の項目も参照してください。
* [`DecrementFanSpeedRequest`](#DecrementFanSpeedRequest)

## DecrementFanSpeedRequest {#DecrementFanSpeedRequest}
主に空気清浄機などのデバイスを制御する際に使用します。ファンの速度を指定された値に下げるようClova Home Extensionにリクエストします。このリクエストに対するレスポンスとして、[`DecrementFanSpeedConfirmation`](#DecrementFanSpeedConfirmation)メッセージを使用する必要があります。

### Payload fields

| フィールド名       | データ型    | フィールドの説明                     | 任意 |
|---------------|---------|-----------------------------|:---------:|
| `accessToken`      | string                                  | IoTサービスのユーザーアカウントのアクセストークン。CEKは、外部サービスの認可サーバーから取得したユーザーアカウントのアクセストークンを渡します。詳細については、[ユーザーアカウントをリンクする](/CEK/Guides/Link_User_Account.md)を参照してください。                          | 常時    |
| `appliance`        | [ApplianceInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#ApplianceInfoObject)     | エンドポイントの情報を持つオブジェクト。`applianceId`フィールドは必須です。     | 常時    |
| `deltaFanSpeed`       | [SpeedInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#SpeedInfoObject)             | 変更するファンの速度情報を持つオブジェクト。ファンの速度とは風速のことで、次のいずれかになります。<ul><li><code>1</code>：弱風(1段階)</li><li><code>2</code>：中風(2段階)</li><li><code>3</code>：強風(3段階)</li></ul> | 常時    |

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

### 次の項目も参照してください。
* [`DecrementFanSpeedConfirmation`](#DecrementFanSpeedConfirmation)

## DecrementIntensityLevelConfirmation {#DecrementIntensityLevelConfirmation}
[`DecrementIntensityLevelRequest`](#DecrementIntensityLevelRequest)メッセージに対するレスポンスです。圧力や水圧などの強度を下げるように設定した結果をCEKに返します。

### Payload fields

| フィールド名       | データ型    | フィールドの説明                     | 必須/選択 |
|---------------|---------|-----------------------------|:---------:|
| `intensityLevel` | [IntensityLevelInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#IntensityLevelInfoObject) | 現在の圧力/水圧などの強度情報を持つオブジェクト                  | 選択    |
| `previousState`  | object                                  | エンドポイントの前の状況情報を持つオブジェクト                           | 選択    |
| `previousState.intensityLevel` | [IntensityLevelInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#IntensityLevelInfoObject) | 前の圧力/水圧などの強度情報を持つオブジェクト    | 選択    |

### 備考

エンドポイントからペイロードに入力する情報を取得できない場合、値を省略できます。その場合、ユーザーには具体的な情報なしに、リクエストが正常に処理されたことを通知します。

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

### 次の項目も参照してください。
* [`DecrementIntensityLevelRequest`](#DecrementIntensityLevelRequest)

## DecrementIntensityLevelRequest {#DecrementIntensityLevelRequest}
主にエアコンやサーモスタットのようなデバイスの制御に使用します。圧力や水圧の強度を指定された値に下げるようClova Home Extensionにリクエストします。このリクエストに対するレスポンスとして、[`DecrementIntensityLevelConfirmation`](#DecrementIntensityLevelConfirmation)メッセージを使用する必要があります。

### Payload fields

| フィールド名       | データ型    | フィールドの説明                     | 任意 |
|---------------|---------|-----------------------------|:---------:|
| `accessToken`      | string                                  | IoTサービスのユーザーアカウントのアクセストークン。CEKは、外部サービスの認可サーバーから取得したユーザーアカウントのアクセストークンを渡します。詳細については、[ユーザーアカウントをリンクする](/CEK/Guides/Link_User_Account.md)を参照してください。                          | 常時    |
| `appliance`        | [ApplianceInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#ApplianceInfoObject)     | エンドポイントの情報を持つオブジェクト。`applianceId`フィールドは必須です。 | 常時    |
| `deltaIntensity`   | [IntensityLevelInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#TemperatureInfoObject) | 変更する強度情報を持つオブジェクト                            | 常時    |

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

### 次の項目も参照してください。
* [`DecrementIntensityLevelConfirmation`](#DecrementIntensityLevelConfirmation)

## DecrementTargetTemperatureConfirmation {#DecrementTargetTemperatureConfirmation}
[`DecrementTargetTemperatureRequest`](#DecrementTargetTemperatureRequest)メッセージに対するレスポンスです。温度を下げるように設定した結果をCEKに返します。

### Payload fields

| フィールド名       | データ型    | フィールドの説明                     | 必須/選択 |
|---------------|---------|-----------------------------|:---------:|
| `previousState`     | object                                  | エンドポイントの前の状況情報を持つオブジェクト                           | 選択    |
| `previousState.targetTemperature` | [TemperatureInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#TemperatureInfoObject) | 前の設定温度の情報を持つオブジェクト              | 選択    |
| `targetTemperature` | [TemperatureInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#TemperatureInfoObject) | デバイスに設定された温度、またはExtensionからリクエストされた設定温度の情報を持つオブジェクト                            | 選択    |

### 備考

エンドポイントからペイロードに入力する情報を取得できない場合、値を省略できます。その場合、ユーザーには具体的な情報なしに、リクエストが正常に処理されたことを通知します。

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

### 次の項目も参照してください。
* [`DecrementTargetTemperatureRequest`](#DecrementTargetTemperatureRequest)

## DecrementTargetTemperatureRequest {#DecrementTargetTemperatureRequest}
主にエアコンやサーモスタットのようなデバイスの制御に使用します。指定された値に温度を下げるようClova Home Extensionにリクエストします。このリクエストに対するレスポンスとして、[`DecrementTargetTemperatureConfirmation`](#DecrementTargetTemperatureConfirmation)メッセージを使用する必要があります。

### Payload fields

| フィールド名       | データ型    | フィールドの説明                     | 任意 |
|---------------|---------|-----------------------------|:---------:|
| `accessToken`      | string                                  | IoTサービスのユーザーアカウントのアクセストークン。CEKは、外部サービスの認可サーバーから取得したユーザーアカウントのアクセストークンを渡します。詳細については、[ユーザーアカウントをリンクする](/CEK/Guides/Link_User_Account.md)を参照してください。                          | 常時    |
| `appliance`        | [ApplianceInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#ApplianceInfoObject)     | エンドポイントの情報を持つオブジェクト。`applianceId`フィールドは必須です。 | 常時    |
| `deltaTemperature` | [TemperatureInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#TemperatureInfoObject) | 変更する温度情報を持つオブジェクト                              | 常時    |

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

### 次の項目も参照してください。
* [`DecrementTargetTemperatureConfirmation`](#DecrementTargetTemperatureConfirmation)

## DecrementVolumeConfirmation {#DecrementVolumeConfirmation}
[`DecrementVolumeRequest`](#DecrementVolumeRequest)メッセージに対するレスポンスです。スピーカーの音量を下げるように設定した結果をCEKに返します。

### Payload fields

| フィールド名       | データ型    | フィールドの説明                     | 必須/選択 |
|---------------|---------|-----------------------------|:---------:|
| `previousState`     | object                                  | エンドポイントの前の状況情報を持つオブジェクト                        | 選択    |
| `previousState.targetVolume` | [VolumeInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#SpeedInfoObject)    | 前の音量情報を持つオブジェクト                             | 選択    |
| `targetVolume`      | [VolumeInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#SpeedInfoObject)            | デバイスに設定されたか、またはExtensionからリクエストされた音量情報を持つオブジェクト                             | 選択    |

### 備考

エンドポイントからペイロードに入力する情報を取得できない場合、値を省略できます。その場合、ユーザーには具体的な情報なしに、リクエストが正常に処理されたことを通知します。

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

### 次の項目も参照してください。
* [`DecrementVolumeRequest`](#DecrementVolumeRequest)

## DecrementVolumeRequest {#DecrementVolumeRequest}
主にテレビのセットトップボックスなどのデバイスを制御する際に使用します。スピーカーの音量を指定された値に下げるようClova Home Extensionにリクエストします。このリクエストに対するレスポンスとして、[`DecrementVolumeConfirmation`](#DecrementVolumeConfirmation)メッセージを使用する必要があります。

### Payload fields

| フィールド名       | データ型    | フィールドの説明                     | 任意 |
|---------------|---------|-----------------------------|:---------:|
| `accessToken`      | string                                  | IoTサービスのユーザーアカウントのアクセストークン。CEKは、外部サービスの認可サーバーから取得したユーザーアカウントのアクセストークンを渡します。詳細については、[ユーザーアカウントをリンクする](/CEK/Guides/Link_User_Account.md)を参照してください。                          | 常時    |
| `appliance`        | [ApplianceInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#ApplianceInfoObject)     | エンドポイントの情報を持つオブジェクト。`applianceId`フィールドは必須です。     | 常時    |
| `deltaVolume`       | [VolumeInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#VolumeInfoObject)             | 変更する音量情報を持つオブジェクト                           | 常時    |

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

### 次の項目も参照してください。
* [`DecrementVolumeConfirmation`](#DecrementVolumeConfirmation)

## GetAirQualityRequest {#GetAirQualityRequest}
主に空気清浄機などのデバイスで測定された空気質情報を確認する際に使用します。空気質情報をClova Home Extensionにリクエストします。このリクエストに対するレスポンスとして、[`GetAirQualityResponse`](#GetAirQualityResponse)メッセージを使用する必要があります。

| フィールド名       | データ型    | フィールドの説明                     | 任意 |
|---------------|---------|-----------------------------|:---------:|
| `accessToken`      | string                                  | IoTサービスのユーザーアカウントのアクセストークン。CEKは、外部サービスの認可サーバーから取得したユーザーアカウントのアクセストークンを渡します。詳細については、[ユーザーアカウントをリンクする](/CEK/Guides/Link_User_Account.md)を参照してください。                          | 常時    |
| `appliance`        | [ApplianceInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#ApplianceInfoObject)     | エンドポイントの情報を持つオブジェクト。`applianceId`フィールドは必須です。     | 常時    |

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

### 次の項目も参照してください。
* [`GetAirQualityResponse`](#GetAirQualityResponse)

## GetAirQualityResponse {#GetAirQualityResponse}
[`GetAirQualityRequest`](#GetAirQualityRequest)メッセージに対するレスポンスです。デバイスで測定された空気質情報をCEKに返します。

| フィールド名       | データ型    | フィールドの説明                     | 必須/選択 |
|---------------|---------|-----------------------------|:---------:|
| `airQuality`                 | [AirQualityInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#AirQualityInfoObject) | デバイスで測定された現在の空気質情報を持つオブジェクト   | 必須    |
| `applianceResponseTimestamp` | string | リクエストがエンドポイントで確認された日時(タイムスタンプ、<a href="https://en.wikipedia.org/wiki/ISO_8601" target="_blank">ISO 8601</a>)     | 選択    |

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

### 次の項目も参照してください。
* [`GetAirQualityRequest`](#GetAirQualityRequest)

## GetAsleepDurationRequest {#GetAsleepDurationRequest}
主に睡眠センサーで測定された情報を確認する際に使用します。デバイスで測定されたユーザーの睡眠時間をClova Home Extensionにリクエストします。このリクエストに対するレスポンスとして、[`GetAsleepDurationResponse`](#GetAsleepDurationResponse)メッセージを使用する必要があります。

| フィールド名       | データ型    | フィールドの説明                     | 任意 |
|---------------|---------|-----------------------------|:---------:|
| `accessToken`      | string                                  | IoTサービスのユーザーアカウントのアクセストークン。CEKは、外部サービスの認可サーバーから取得したユーザーアカウントのアクセストークンを渡します。詳細については、[ユーザーアカウントをリンクする](/CEK/Guides/Link_User_Account.md)を参照してください。                          | 常時    |
| `appliance`        | [ApplianceInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#ApplianceInfoObject)     | エンドポイントの情報を持つオブジェクト。`applianceId`フィールドは必須です。     | 常時    |
| `period`           | [PeriodInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#PeriodInfoObject)           | 期間情報を持つオブジェクト                                      | 条件付き  |

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
      "start": "2018-03-28T00:0:00+09:00",
      "end": "2018-03-28T23:59:59+09:00"
    }
  }
}
```

{% endraw %}

### 次の項目も参照してください。
* [`GetAsleepDurationResponse`](#GetAsleepDurationResponse)

## GetAsleepDurationResponse {#GetAsleepDurationResponse}
[`GetAsleepDurationRequest`](#GetAsleepDurationRequest)メッセージに対するレスポンスです。デバイスで測定されたユーザーの睡眠時間をCEKに返します。

| フィールド名       | データ型    | フィールドの説明                     | 必須/選択 |
|---------------|---------|-----------------------------|:---------:|
| `applianceResponseTimestamp`  | string | リクエストがエンドポイントで確認された日時(タイムスタンプ、<a href="https://en.wikipedia.org/wiki/ISO_8601" target="_blank">ISO 8601</a>)     | 選択    |
| `asleepDuration`                    | string | 睡眠時間の平均(継続時間、<a href="https://en.wikipedia.org/wiki/ISO_8601#Durations" target="_blank">ISO 8601</a>)   | 必須    |

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

### 次の項目も参照してください。
* [`GetAsleepDurationRequest`](#GetAsleepDurationRequest)

## GetAwakeDurationRequest {#GetAwakeDurationRequest}
主に睡眠センサーで測定された情報を確認する際に使用します。デバイスで測定されたユーザーの入眠潜時、つまりユーザーが就寝してから睡眠状態に入るまでの時間をClova Home Extensionにリクエストします。このリクエストに対するレスポンスとして、[`GetAwakeDurationResponse`](#GetAwakeDurationResponse)メッセージを使用する必要があります。

| フィールド名       | データ型    | フィールドの説明                     | 任意 |
|---------------|---------|-----------------------------|:---------:|
| `accessToken`      | string                                  | IoTサービスのユーザーアカウントのアクセストークン。CEKは、外部サービスの認可サーバーから取得したユーザーアカウントのアクセストークンを渡します。詳細については、[ユーザーアカウントをリンクする](/CEK/Guides/Link_User_Account.md)を参照してください。                          | 常時    |
| `appliance`        | [ApplianceInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#ApplianceInfoObject)     | エンドポイントの情報を持つオブジェクト。`applianceId`フィールドは必須です。     | 常時    |
| `period`           | [PeriodInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#PeriodInfoObject)           | 期間情報を持つオブジェクト                                      | 条件付き  |

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
      "start": "2018-03-28T00:0:00+09:00",
      "end": "2018-03-28T23:59:59+09:00"
    }
  }
}
```

{% endraw %}

### 次の項目も参照してください。
* [`GetAwakeDurationResponse`](#GetAwakeDurationResponse)

## GetAwakeDurationResponse {#GetAwakeDurationResponse}
[`GetAwakeDurationRequest`](#GetAwakeDurationRequest)メッセージに対するレスポンスです。デバイスで測定されたユーザーの入眠潜時、つまりユーザーが就寝してから睡眠状態に入るまでの時間をCEKに返します。

| フィールド名       | データ型    | フィールドの説明                     | 必須/選択 |
|---------------|---------|-----------------------------|:---------:|
| `applianceResponseTimestamp`  | string | リクエストがエンドポイントで確認された日時(タイムスタンプ、<a href="https://en.wikipedia.org/wiki/ISO_8601" target="_blank">ISO 8601</a>)     | 選択    |
| `awakeDuration`                    | string | 入眠潜時の平均(継続時間、<a href="https://en.wikipedia.org/wiki/ISO_8601#Durations" target="_blank">ISO 8601</a>)   | 必須    |

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

### 次の項目も参照してください。
* [`GetAwakeDurationRequest`](#GetAwakeDurationRequest)

## GetBatteryInfoRequest {#GetBatteryInfoRequest}
主にロボット掃除機などのワイヤレスデバイスの内蔵電池の情報を確認する際に使用します。現在の電池の情報をClova Home Extensionにリクエストします。このリクエストに対するレスポンスとして、[`GetBatteryInfoResponse`](#GetBatteryInfoResponse)メッセージを使用する必要があります。

| フィールド名       | データ型    | フィールドの説明                     | 任意 |
|---------------|---------|-----------------------------|:---------:|
| `accessToken`      | string                                  | IoTサービスのユーザーアカウントのアクセストークン。CEKは、外部サービスの認可サーバーから取得したユーザーアカウントのアクセストークンを渡します。詳細については、[ユーザーアカウントをリンクする](/CEK/Guides/Link_User_Account.md)を参照してください。                          | 常時    |
| `appliance`        | [ApplianceInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#ApplianceInfoObject)     | エンドポイントの情報を持つオブジェクト。`applianceId`フィールドは必須です。     | 常時    |

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

### 次の項目も参照してください。
* [`GetBatteryInfoResponse`](#GetBatteryInfoResponse)

## GetBatteryInfoResponse {#GetBatteryInfoResponse}
[`GetBatteryInfoRequest`](#GetBatteryInfoRequest)メッセージに対するレスポンスです。デバイスの電池の情報をCEKに返します。

| フィールド名       | データ型    | フィールドの説明                     | 必須/選択 |
|---------------|---------|-----------------------------|:---------:|
| `applianceResponseTimestamp` | string | リクエストがエンドポイントで確認された日時(タイムスタンプ、<a href="https://en.wikipedia.org/wiki/ISO_8601" target="_blank">ISO 8601</a>)     | 選択    |
| `batteryInfo`                 | [BatteryInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#BatteryInfoObject) | デバイスの現在の電池情報を持つオブジェクト   | 必須    |

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

### 次の項目も参照してください。
* [`GetBatteryInfoRequest`](#GetBatteryInfoRequest)

## GetBatteryInfoRequest {#GetBatteryInfoRequest}
主にロボット掃除機などのワイヤレスデバイスの内蔵電池の情報を確認する際に使用します。現在の電池の情報をClova Home Extensionにリクエストします。このリクエストに対するレスポンスとして、[`GetBatteryInfoResponse`](#GetBatteryInfoResponse)メッセージを使用する必要があります。

| フィールド名       | データ型    | フィールドの説明                     | 任意 |
|---------------|---------|-----------------------------|:---------:|
| `accessToken`      | string                                  | IoTサービスのユーザーアカウントのアクセストークン。CEKは、外部サービスの認可サーバーから取得したユーザーアカウントのアクセストークンを渡します。詳細については、[ユーザーアカウントをリンクする](/CEK/Guides/Link_User_Account.md)を参照してください。                          | 常時    |
| `appliance`        | [ApplianceInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#ApplianceInfoObject)     | エンドポイントの情報を持つオブジェクト。`applianceId`フィールドは必須です。     | 常時    |

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

### 次の項目も参照してください。
* [`GetBatteryInfoResponse`](#GetBatteryInfoResponse)

## GetBatteryInfoResponse {#GetBatteryInfoResponse}
[`GetBatteryInfoRequest`](#GetBatteryInfoRequest)メッセージに対するレスポンスです。デバイスの電池の情報をCEKに返します。

| フィールド名       | データ型    | フィールドの説明                     | 必須/選択 |
|---------------|---------|-----------------------------|:---------:|
| `applianceResponseTimestamp` | string | リクエストがエンドポイントで確認された日時(タイムスタンプ、<a href="https://en.wikipedia.org/wiki/ISO_8601" target="_blank">ISO 8601</a>)     | 選択    |
| `batteryInfo`                 | [BatteryInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#BatteryInfoObject) | デバイスの現在の電池情報を持つオブジェクト   | 必須    |

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

### 次の項目も参照してください。
* [`GetBatteryInfoRequest`](#GetBatteryInfoRequest)

## GetCleaningCycleRequest {#GetCleaningCycleRequest}
デバイスをクリーニングする周期を確認する際に使用します。デバイスの次のクリーニング周期までの残り時間をClova Home extensionにリクエストします。このリクエストに対するレスポンスとして、[`GetCleaningCycleResponse`](#GetCleaningCycleResponse)メッセージを使用する必要があります。

| フィールド名       | データ型    | フィールドの説明                     | 任意 |
|---------------|---------|-----------------------------|:---------:|
| `accessToken`      | string                                  | IoTサービスのユーザーアカウントのアクセストークン。CEKは、外部サービスの認可サーバーから取得したユーザーアカウントのアクセストークンを渡します。詳細については、[ユーザーアカウントをリンクする](/CEK/Guides/Link_User_Account.md)を参照してください。                          | 常時    |
| `appliance`        | [ApplianceInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#ApplianceInfoObject)     | エンドポイントの情報を持つオブジェクト。`applianceId`フィールドは必須です。     | 常時    |

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

### 次の項目も参照してください。
* [`GetCleaningCycleResponse`](#GetCleaningCycleResponse)

## GetCleaningCycleResponse {#GetCleaningCycleResponse}

[`GetCleaningCycleRequest`](#GetCleaningCycleRequest)メッセージに対するレスポンスです。デバイスの次のクリーニング周期までの残り時間をCEKに返します。

| フィールド名       | データ型    | フィールドの説明                     | 必須/選択 |
|---------------|---------|-----------------------------|:---------:|
| `applianceResponseTimestamp` | string | リクエストがエンドポイントで確認された日時(タイムスタンプ、<a href="https://en.wikipedia.org/wiki/ISO_8601" target="_blank">ISO 8601</a>)     | 選択    |
| `remainingTime`              | string | クリーニングする時点までの残り時間(Duration、<a href="https://en.wikipedia.org/wiki/ISO_8601#Durations" target="_blank">ISO 8601</a>)    | 必須    |

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

### 次の項目も参照してください。
* [`GetCleaningCycleRequest`](#GetGetCleaningCycleRequest)

## GetCloseTimeRequest {#GetCloseTimeRequest}
開閉センサーで検知された開閉状況のうち、検知対象が最後に閉まったときの日時情報をClova Home Extensionにリクエストします。このリクエストに対するレスポンスとして、[`GetCloseTimeResponse`](#GetCloseTimeResponse)メッセージを使用する必要があります。

| フィールド名       | データ型    | フィールドの説明                     | 任意 |
|---------------|---------|-----------------------------|:---------:|
| `accessToken`      | string                                  | IoTサービスのユーザーアカウントのアクセストークン。CEKは、外部サービスの認可サーバーから取得したユーザーアカウントのアクセストークンを渡します。詳細については、[ユーザーアカウントをリンクする](/CEK/Guides/Link_User_Account.md)を参照してください。                          | 常時    |
| `appliance`        | [ApplianceInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#ApplianceInfoObject)     | エンドポイントの情報を持つオブジェクト。`applianceId`フィールドは必須です。     | 常時    |

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

### 次の項目も参照してください。
* [`GetCloseTimeResponse`](#GetCloseTimeResponse)

## GetCloseTimeResponse {#GetCloseTimeResponse}

[`GetCloseTimeRequest`](#GetCloseTimeRequest)メッセージに対するレスポンスです。開閉センサーの検知対象が最後に閉まったときの日時情報をCEKに返します。

| フィールド名       | データ型    | フィールドの説明                     | 必須/選択 |
|---------------|---------|-----------------------------|:---------:|
| `applianceResponseTimestamp` | string | リクエストがエンドポイントで確認された日時(タイムスタンプ、<a href="https://en.wikipedia.org/wiki/ISO_8601" target="_blank">ISO 8601</a>)     | 選択    |
| `closeTimestamp`             | string | 検知対象が最後に閉まった日時(タイムスタンプ、<a href="https://en.wikipedia.org/wiki/ISO_8601" target="_blank">ISO 8601</a>)     | 必須    |

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
    "closeTime": "2018-03-13T23:17:50+09:00",
    "applianceResponseTimestamp": "2017-11-23T20:30:19+09:00"
  }
}
```

{% endraw %}

### 次の項目も参照してください。
* [`GetCloseTimeRequest`](#GetCloseTimeRequest)

## GetConsumptionRequest {#GetConsumptionRequest}
主にスマートプラグやスマートテーブルタップのようなデバイスで測定された、現在までのエネルギーまたはリソースを確認する際に使用します。測定されたエネルギーまたはリソースの情報をClova Home Extensionにリクエストします。このリクエストに対するレスポンスとして、[`GetConsumptionResponse`](#GetConsumptionResponse)メッセージを使用する必要があります。

| フィールド名       | データ型    | フィールドの説明                     | 任意 |
|---------------|---------|-----------------------------|:---------:|
| `accessToken`      | string                                  | IoTサービスのユーザーアカウントのアクセストークン。CEKは、外部サービスの認可サーバーから取得したユーザーアカウントのアクセストークンを渡します。詳細については、[ユーザーアカウントをリンクする](/CEK/Guides/Link_User_Account.md)を参照してください。                          | 常時    |
| `appliance`        | [ApplianceInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#ApplianceInfoObject)     | エンドポイントの情報を持つオブジェクト。`applianceId`フィールドは必須です。     | 常時    |

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

### 次の項目も参照してください。
* [`GetConsumptionResponse`](#GetConsumptionResponse)

## GetConsumptionResponse {#GetConsumptionResponse}
[`GetConsumptionRequest`](#GetConsumptionRequest)メッセージに対するレスポンスです。現在まで測定されたエネルギーまたはリソースの情報をCEKに返します。

| フィールド名       | データ型    | フィールドの説明                     | 必須/選択 |
|---------------|---------|-----------------------------|:---------:|
| `applianceResponseTimestamp` | string | リクエストがエンドポイントで確認された日時(タイムスタンプ、<a href="https://en.wikipedia.org/wiki/ISO_8601" target="_blank">ISO 8601</a>)     | 選択    |
| `consumption[]`              | [ConsumptionInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#ConsumptionInfoObject) array | デバイスで現在まで測定されたエネルギーまたはリソースの情報を持つオブジェクト   | 必須    |

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
        "name": "電気使用量",
        "value": 79.7,
        "unit": "kW"
      }
    ],
    "applianceResponseTimestamp": "2017-11-23T20:30:54+09:00"
  }
}
```

{% endraw %}

### 次の項目も参照してください。
* [GetConsumptionRequest](#GetConsumptionRequest)

## GetCurrentBillRequest {#GetCurrentBillRequest}
主にスマートプラグやスマートテーブルタップのようなデバイスで測定された、現在までのエネルギー使用量に基づいた利用料金を確認する際に使用します。測定された料金情報をClova Home Extensionにリクエストします。このリクエストに対するレスポンスとして、[`GetCurrentBillResponse`](#GetCurrentBillResponse)メッセージを使用する必要があります。

| フィールド名       | データ型    | フィールドの説明                     | 任意 |
|---------------|---------|-----------------------------|:---------:|
| `accessToken`      | string                                  | IoTサービスのユーザーアカウントのアクセストークン。CEKは、外部サービスの認可サーバーから取得したユーザーアカウントのアクセストークンを渡します。詳細については、[ユーザーアカウントをリンクする](/CEK/Guides/Link_User_Account.md)を参照してください。                          | 常時    |
| `appliance`        | [ApplianceInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#ApplianceInfoObject)     | エンドポイントの情報を持つオブジェクト。`applianceId`フィールドは必須です。     | 常時    |

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

### 次の項目も参照してください。
* [`GetCurrentBillResponse`](#GetCurrentBillResponse)

## GetCurrentBillResponse {#GetCurrentBillResponse}
[`GetCurrentBillRequest`](#GetCurrentBillRequest)メッセージに対するレスポンスです。現在まで測定された料金情報をCEKに返します。

| フィールド名       | データ型    | フィールドの説明                     | 必須/選択 |
|---------------|---------|-----------------------------|:---------:|
| `applianceResponseTimestamp` | string | リクエストがエンドポイントで確認された日時(タイムスタンプ、<a href="https://en.wikipedia.org/wiki/ISO_8601" target="_blank">ISO 8601</a>)     | 選択    |
| `currentBill`                 | [BillInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#BillInfoObject) | 現在まで測定された料金情報を持つオブジェクト   | 必須    |

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

### 次の項目も参照してください。
* [GetCurrentBillRequest](#GetCurrentBillRequest)

## GetCurrentTemperatureRequest {#GetCurrentTemperatureRequest}
主にエアコンやサーモスタットのようなデバイスで測定された現在の温度を確認する際に使用します。現在の温度をClova Home Extensionにリクエストします。このリクエストに対するレスポンスとして、[`GetCurrentTemperatureResponse`](#GetCurrentTemperatureResponse)メッセージを使用する必要があります。

| フィールド名       | データ型    | フィールドの説明                     | 任意 |
|---------------|---------|-----------------------------|:---------:|
| `accessToken`      | string                                  | IoTサービスのユーザーアカウントのアクセストークン。CEKは、外部サービスの認可サーバーから取得したユーザーアカウントのアクセストークンを渡します。詳細については、[ユーザーアカウントをリンクする](/CEK/Guides/Link_User_Account.md)を参照してください。                          | 常時    |
| `appliance`        | [ApplianceInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#ApplianceInfoObject)     | エンドポイントの情報を持つオブジェクト。`applianceId`フィールドは必須です。     | 常時    |

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

### 次の項目も参照してください。
* [`GetCurrentTemperatureResponse`](#GetCurrentTemperatureResponse)
* [`GetTargetTemperatureRequest`](#GetTargetTemperatureRequest)

## GetCurrentTemperatureResponse {#GetCurrentTemperatureResponse}
[`GetCurrentTemperatureRequest`](#GetCurrentTemperatureRequest)メッセージに対するレスポンスです。デバイスで測定された現在の温度をCEKに返します。

| フィールド名       | データ型    | フィールドの説明                     | 必須/選択 |
|---------------|---------|-----------------------------|:---------:|
| `applianceResponseTimestamp` | string | リクエストがエンドポイントで確認された日時(タイムスタンプ、<a href="https://en.wikipedia.org/wiki/ISO_8601" target="_blank">ISO 8601</a>)     | 選択    |
| `currentTemperature`          | [TemperatureInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#TemperatureInfoObject) | デバイスで測定された現在の温度情報を持つオブジェクト  | 必須    |

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

### 次の項目も参照してください。
* [`GetCurrentTemperatureRequest`](#GetCurrentTemperatureRequest)
* [`GetTargetTemperatureResponse`](#GetTargetTemperatureResponse)

## GetDeviceStateRequest {#GetDeviceStateRequest}

デバイスが提供するすべてのステータス情報と測定情報を確認する際に使用します。例えば、空気清浄機から空気質、湿度、微細粉塵(PM10)、超微細粉塵(PM2.5)の情報を、それぞれ[`GetAirQualityRequest`](#GetAirQualityRequest)、[`GetHumidityRequest`](#GetHumidityRequest)、[`GetFineDustRequest`](#GetFineDustRequest)、[`GetUltraFineDustRequest`](#GetUltraFineDustRequest)メッセージで確認できます。あるいは`GetDeviceStateRequest`メッセージで一度に確認することもできます。一部の測定情報を確認するには、期間を設定する必要があります。その場合、`period`に期間を設定します。このリクエストに対するレスポンスとして、[`GetDeviceStateResponse`](#GetDeviceStateResponse)メッセージを使用する必要があります。

| フィールド名       | データ型    | フィールドの説明                     | 任意 |
|---------------|---------|-----------------------------|:---------:|
| `accessToken`      | string                                  | IoTサービスのユーザーアカウントのアクセストークン。CEKは、外部サービスの認可サーバーから取得したユーザーアカウントのアクセストークンを渡します。詳細については、[ユーザーアカウントをリンクする](/CEK/Guides/Link_User_Account.md)を参照してください。                          | 常時    |
| `appliance`        | [ApplianceInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#ApplianceInfoObject)     | エンドポイントの情報を持つオブジェクト。`applianceId`フィールドは必須です。     | 常時    |
| `period`           | [PeriodInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#PeriodInfoObject)           | 期間情報を持つオブジェクト                                         | 条件付き   |

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
      "start": "2018-03-28T00:0:00+09:00",
      "end": "2018-03-28T23:59:59+09:00"
    }
  }
}
```

{% endraw %}

### 次の項目も参照してください。
* [`GetDeviceStateResponse`](#GetDeviceStateResponse)

## GetDeviceStateResponse {#GetDeviceStateResponse}
[`GetDeviceStateRequest`](#GetDeviceStateRequest)メッセージに対するレスポンスです。デバイスが提供するすべてのステータス情報をCEKに返します。

| フィールド名       | データ型    | フィールドの説明                     | 必須/選択 |
|---------------|---------|-----------------------------|:---------:|
| `applianceResponseTimestamp` | string | リクエストがエンドポイントで確認された日時(タイムスタンプ、<a href="https://en.wikipedia.org/wiki/ISO_8601" target="_blank">ISO 8601</a>)     | 選択    |
| `states[]`                   | [CustomInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#CustomInfoObject) array  | デバイス提供するすべてのステータス情報を持つオブジェクト                    | 必須  |

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
        "name" : "冷凍室の温度",
        "value" : -11,
        "unit" : "celsius"
      },
      {
        "name" : "冷蔵室の温度",
        "value" : 2,
        "unit" : "celsius"
      },
      {
        "name" : "冷蔵室の湿度",
        "value" : 10,
        "unit" : "percentage"
      }
    ],
    "applianceResponseTimestamp": "2017-11-23T20:31:18+09:00"
  }
}
```

{% endraw %}

### 次の項目も参照してください。
* [`GetDeviceStateRequest`](#GetDeviceStateRequest)

## GetEstimateBillRequest {#GetEstimateBillRequest}
主にスマートプラグやスマートテーブルタップのようなデバイスで測定されたエネルギー使用量に基づいて、利用料金を推定する際に使用します。推定された料金情報をClova Home Extensionにリクエストします。このリクエストに対するレスポンスとして、[`GetEstimateBillResponse`](#GetEstimateBillResponse)メッセージを使用する必要があります。

| フィールド名       | データ型    | フィールドの説明                     | 任意 |
|---------------|---------|-----------------------------|:---------:|
| `accessToken`      | string                                  | IoTサービスのユーザーアカウントのアクセストークン。CEKは、外部サービスの認可サーバーから取得したユーザーアカウントのアクセストークンを渡します。詳細については、[ユーザーアカウントをリンクする](/CEK/Guides/Link_User_Account.md)を参照してください。                          | 常時    |
| `appliance`        | [ApplianceInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#ApplianceInfoObject)     | エンドポイントの情報を持つオブジェクト。`applianceId`フィールドは必須です。     | 常時    |

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

### 次の項目も参照してください。
* [`GetEstimateBillResponse`](#GetEstimateBillResponse)

## GetEstimateBillResponse {#GetEstimateBillResponse}
[`GetEstimateBillRequest`](#GetEstimateBillRequest)メッセージに対するレスポンスです。推定された料金情報をCEKに返します。

| フィールド名       | データ型    | フィールドの説明                     | 必須/選択 |
|---------------|---------|-----------------------------|:---------:|
| `applianceResponseTimestamp` | string | リクエストがエンドポイントで確認された日時(タイムスタンプ、<a href="https://en.wikipedia.org/wiki/ISO_8601" target="_blank">ISO 8601</a>)     | 選択    |
| `estimateBill`                 | [BillInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#BillInfoObject) | デバイスで推定された料金情報を持つオブジェクト   | 必須    |

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

### 次の項目も参照してください。
* [GetEstimateBillRequest](#GetEstimateBillRequest)

## GetExpendableStateRequest {#GetExpendableStateRequest}

フィルターなど、デバイスの消耗品の使用量や残り寿命を確認する際に使用します。デバイスが持つ消耗品の使用量や寿命情報をリクエストします。このリクエストに対するレスポンスとして、[`GetExpendableStateResponse`](#GetExpendableStateResponse)メッセージを使用する必要があります。

| フィールド名       | データ型    | フィールドの説明                     | 任意 |
|---------------|---------|-----------------------------|:---------:|
| `accessToken`      | string                                  | IoTサービスのユーザーアカウントのアクセストークン。CEKは、外部サービスの認可サーバーから取得したユーザーアカウントのアクセストークンを渡します。詳細については、[ユーザーアカウントをリンクする](/CEK/Guides/Link_User_Account.md)を参照してください。                          | 常時    |
| `appliance`        | [ApplianceInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#ApplianceInfoObject)     | エンドポイントの情報を持つオブジェクト。`applianceId`フィールドは必須です。     | 常時    |

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

### 次の項目も参照してください。
* [`GetExpendableStateResponse`](#GetExpendableStateResponse)

## GetExpendableStateResponse {#GetExpendableStateResponse}
[`GetExpendableStateRequest`](#GetExpendableStateRequest)メッセージに対するレスポンスです。デバイスが提供するすべての消耗品の使用量や寿命情報をCEKに返します。

| フィールド名       | データ型    | フィールドの説明                     | 必須/選択 |
|---------------|---------|-----------------------------|:---------:|
| `applianceResponseTimestamp` | string | リクエストがエンドポイントで確認された日時(タイムスタンプ、<a href="https://en.wikipedia.org/wiki/ISO_8601" target="_blank">ISO 8601</a>)     | 選択    |
| `expendableInfo[]`           | [ExpendableInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#ExpendableInfoObject) array  | 消耗品の使用量や寿命情報を持つオブジェクト                    | 必須  |

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
        "name" : "パッキン",
        "remainingTime": "P0001-04-10"
      },
      {
        "name" : "フィルター1",
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

### 次の項目も参照してください。
* [`GetExpendableStateRequest`](#GetExpendableStateRequest)

## GetFineDustRequest {#GetFineDustRequest}
主に空気清浄機などのデバイスで測定された微細粉塵(PM10)の情報を確認する際に使用します。微細粉塵(PM10)の情報をClova Home Extensionにリクエストします。このリクエストに対するレスポンスとして、[`GetFineDustResponse`](#GetFineDustResponse)メッセージを使用する必要があります。

| フィールド名       | データ型    | フィールドの説明                     | 任意 |
|---------------|---------|-----------------------------|:---------:|
| `accessToken`      | string                                  | IoTサービスのユーザーアカウントのアクセストークン。CEKは、外部サービスの認可サーバーから取得したユーザーアカウントのアクセストークンを渡します。詳細については、[ユーザーアカウントをリンクする](/CEK/Guides/Link_User_Account.md)を参照してください。                          | 常時    |
| `appliance`        | [ApplianceInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#ApplianceInfoObject)     | エンドポイントの情報を持つオブジェクト。`applianceId`フィールドは必須です。     | 常時    |

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

### 次の項目も参照してください。
* [`GetFineDustResponse`](#GetFineDustResponse)

## GetFineDustResponse {#GetFineDustResponse}
[`GetFineDustRequest`](#GetFineDustRequest)メッセージに対するレスポンスです。デバイスで測定された微細粉塵(PM10)の情報をCEKに返します。

| フィールド名       | データ型    | フィールドの説明                     | 必須/選択 |
|---------------|---------|-----------------------------|:---------:|
| `applianceResponseTimestamp` | string | リクエストがエンドポイントで確認された日時(タイムスタンプ、<a href="https://en.wikipedia.org/wiki/ISO_8601" target="_blank">ISO 8601</a>)     | 選択    |
| `fineDust`                 | [FineDustInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#FineDustInfoObject) | デバイスで測定された現在の微細粉塵(PM10)の情報を持つオブジェクト   | 必須    |

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

### 次の項目も参照してください。
* [`GetFineDustRequest`](#GetFineDustRequest)

## GetHumidityRequest {#GetHumidityRequest}
主に加湿器などのデバイスで測定された湿度を確認する際に使用します。湿度をClova Home Extensionにリクエストします。このリクエストに対するレスポンスとして、[`GetHumidityResponse`](#GetHumidityResponse)メッセージを使用する必要があります。

| フィールド名       | データ型    | フィールドの説明                     | 任意 |
|---------------|---------|-----------------------------|:---------:|
| `accessToken`      | string                                  | IoTサービスのユーザーアカウントのアクセストークン。CEKは、外部サービスの認可サーバーから取得したユーザーアカウントのアクセストークンを渡します。詳細については、[ユーザーアカウントをリンクする](/CEK/Guides/Link_User_Account.md)を参照してください。                          | 常時    |
| `appliance`        | [ApplianceInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#ApplianceInfoObject)     | エンドポイントの情報を持つオブジェクト。`applianceId`フィールドは必須です。     | 常時    |

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

### 次の項目も参照してください。
* [`GetHumidityResponse`](#GetHumidityResponse)

## GetHumidityResponse {#GetHumidityResponse}
[`GetHumidityRequest`](#GetHumidityRequest)メッセージに対するレスポンスです。デバイスで測定された湿度をCEKに返します。

| フィールド名       | データ型    | フィールドの説明                     | 必須/選択 |
|---------------|---------|-----------------------------|:---------:|
| `applianceResponseTimestamp` | string | リクエストがエンドポイントで確認された日時(タイムスタンプ、<a href="https://en.wikipedia.org/wiki/ISO_8601" target="_blank">ISO 8601</a>)     | 選択    |
| `humidity`                 | [HumidityInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#HumidityInfoObject) | デバイスで測定された現在の湿度情報を持つオブジェクト   | 必須    |

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

### 次の項目も参照してください。
* [GetHumidityRequest](#GetHumidityRequest)

## GetKeepWarmTimeRequest {#GetKeepWarmTimeRequest}
炊飯器のようなデバイスで、食べ物が保温された時間を確認する際に使用します。デバイスで保温モードが維持された時間の情報をClova Home Extensionにリクエストします。このリクエストに対するレスポンスとして、[`GetKeepWarmTimeResponse`](#GetKeepWarmTimeResponse)メッセージを使用する必要があります。

| フィールド名       | データ型    | フィールドの説明                     | 任意 |
|---------------|---------|-----------------------------|:---------:|
| `accessToken`      | string                                  | IoTサービスのユーザーアカウントのアクセストークン。CEKは、外部サービスの認可サーバーから取得したユーザーアカウントのアクセストークンを渡します。詳細については、[ユーザーアカウントをリンクする](/CEK/Guides/Link_User_Account.md)を参照してください。                          | 常時    |
| `appliance`        | [ApplianceInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#ApplianceInfoObject)     | エンドポイントの情報を持つオブジェクト。`applianceId`フィールドは必須です。     | 常時    |

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

### 次の項目も参照してください。
* [`GetKeepWarmTimeResponse`](#GetKeepWarmTimeResponse)

## GetKeepWarmTimeResponse {#GetKeepWarmTimeResponse}

[`GetKeepWarmTimeRequest`](#GetKeepWarmTimeRequest)メッセージに対するレスポンスです。保温モードが維持された時間の情報をCEKに返します。

| フィールド名       | データ型    | フィールドの説明                     | 必須/選択 |
|---------------|---------|-----------------------------|:---------:|
| `applianceResponseTimestamp` | string | リクエストがエンドポイントで確認された日時(タイムスタンプ、<a href="https://en.wikipedia.org/wiki/ISO_8601" target="_blank">ISO 8601</a>)        | 選択    |
| `keepWarmTime`               | string | 保温モードを維持した時間(継続時間、<a href="https://en.wikipedia.org/wiki/ISO_8601#Durations" target="_blank">ISO 8601</a>)       | 必須    |

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

### 次の項目も参照してください。
* [`GetKeepWarmTimeRequest`](#GetKeepWarmTimeRequest)

## GetLockStateRequest {#GetLockStateRequest}
主にスマートバルブなどのデバイスの状態を確認する際に使用します。デバイスが持っているロック装置の現在のロック状態をClova Home Extensionにリクエストします。このリクエストに対するレスポンスとして、[`GetLockStateResponse`](#GetLockStateResponse)メッセージを使用する必要があります。

| フィールド名       | データ型    | フィールドの説明                     | 任意 |
|---------------|---------|-----------------------------|:---------:|
| `accessToken`      | string                                  | IoTサービスのユーザーアカウントのアクセストークン。CEKは、外部サービスの認可サーバーから取得したユーザーアカウントのアクセストークンを渡します。詳細については、[ユーザーアカウントをリンクする](/CEK/Guides/Link_User_Account.md)を参照してください。                          | 常時    |
| `appliance`        | [ApplianceInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#ApplianceInfoObject)     | エンドポイントの情報を持つオブジェクト。`applianceId`フィールドは必須です。     | 常時    |

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

### 次の項目も参照してください。
* [`GetLockStateResponse`](#GetLockStateResponse)

## GetLockStateResponse {#GetLockStateResponse}
[`GetLockStateRequest`](#GetLockStateRequest)メッセージに対するレスポンスです。デバイスが持っているロック装置の現在のロック状態をCEKに返します。

| フィールド名       | データ型    | フィールドの説明                     | 必須/選択 |
|---------------|---------|-----------------------------|:---------:|
| `applianceResponseTimestamp` | string | リクエストがエンドポイントで確認された日時(タイムスタンプ、<a href="https://en.wikipedia.org/wiki/ISO_8601" target="_blank">ISO 8601</a>)     | 選択    |
| `lockState`                  | string | デバイスのロック装置のロック状態。以下の値を持ちます。<ul><li><code>"LOCKED"</code>：ロック装置がロックされている</li><li><code>"UNLOCKED"</code>：ロック装置がロックされていない</li></ul> | 必須    |


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

### 次の項目も参照してください。
* [`GetLockStateRequest`](#GetLockStateRequest)

## GetOpenStateRequest {#GetOpenStateRequest}
主に開閉センサーで検知された開閉状況のうち、検知対象の現在の状態(開いている/閉まっている)をClova Home Extensionにリクエストします。このリクエストに対するレスポンスとして、[`GetOpenStateResponse`](#GetOpenStateResponse)メッセージを使用する必要があります。

| フィールド名       | データ型    | フィールドの説明                     | 任意 |
|---------------|---------|-----------------------------|:---------:|
| `accessToken`      | string                                  | IoTサービスのユーザーアカウントのアクセストークン。CEKは、外部サービスの認可サーバーから取得したユーザーアカウントのアクセストークンを渡します。詳細については、[ユーザーアカウントをリンクする](/CEK/Guides/Link_User_Account.md)を参照してください。                          | 常時    |
| `appliance`        | [ApplianceInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#ApplianceInfoObject)     | エンドポイントの情報を持つオブジェクト。`applianceId`フィールドは必須です。     | 常時    |

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

### 次の項目も参照してください。
* [`GetOpenStateResponse`](#GetOpenStateResponse)

## GetOpenStateResponse {#GetOpenStateResponse}
[`GetOpenStateRequest`](#GetOpenStateRequest)メッセージに対するレスポンスです。主に検知対象の現在の状態(開いている/閉まっている)をCEKに返します。

| フィールド名       | データ型    | フィールドの説明                     | 必須/選択 |
|---------------|---------|-----------------------------|:---------:|
| `applianceResponseTimestamp` | string | リクエストがエンドポイントで確認された日時(タイムスタンプ、<a href="https://en.wikipedia.org/wiki/ISO_8601" target="_blank">ISO 8601</a>)     | 選択    |
| `openState`                  | string | カバーやドア、窓などから検知された状態。<ul><li><code>"CLOSED"</code>：カバーやドア、窓などが閉まっている</li><li><code>"OPENED"</code>：カバーやドア、窓などが開いている</li></ul> | 必須    |


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

### 次の項目も参照してください。
* [`GetOpenStateRequest`](#GetOpenStateRequest)

## GetOpenTimeRequest {#GetOpenTimeRequest}
主に開閉センサーで検知された開閉状況のうち、検知対象が最後に開いたときの日時情報をClova Home Extensionにリクエストします。このリクエストに対するレスポンスとして、[`GetOpenTimeResponse`](#GetOpenTimeResponse)メッセージを使用する必要があります。

| フィールド名       | データ型    | フィールドの説明                     | 任意 |
|---------------|---------|-----------------------------|:---------:|
| `accessToken`      | string                                  | IoTサービスのユーザーアカウントのアクセストークン。CEKは、外部サービスの認可サーバーから取得したユーザーアカウントのアクセストークンを渡します。詳細については、[ユーザーアカウントをリンクする](/CEK/Guides/Link_User_Account.md)を参照してください。                          | 常時    |
| `appliance`        | [ApplianceInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#ApplianceInfoObject)     | エンドポイントの情報を持つオブジェクト。`applianceId`フィールドは必須です。     | 常時    |

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

### 次の項目も参照してください。
* [`GetOpenTimeResponse`](#GetOpenTimeResponse)

## GetOpenTimeResponse {#GetOpenTimeResponse}

[`GetOpenTimeRequest`](#GetOpenTimeRequest)メッセージに対するレスポンスです。開閉センサーの検知対象が最後に開いたときの日時情報をCEKに返します。

| フィールド名       | データ型    | フィールドの説明                     | 必須/選択 |
|---------------|---------|-----------------------------|:---------:|
| `applianceResponseTimestamp` | string | リクエストがエンドポイントで確認された日時(タイムスタンプ、<a href="https://en.wikipedia.org/wiki/ISO_8601" target="_blank">ISO 8601</a>)     | 選択    |
| `openTimestamp`              | string | 検知対象が最後に開いた日時(タイムスタンプ、<a href="https://en.wikipedia.org/wiki/ISO_8601" target="_blank">ISO 8601</a>)     | 必須    |

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
    "closeTime": "2018-03-13T23:20:15+09:00",
    "applianceResponseTimestamp": "2017-11-23T20:30:19+09:00"
  }
}
```

{% endraw %}

### 次の項目も参照してください。
* [`GetOpenTimeRequest`](#GetOpenTimeRequest)

## GetPhaseRequest {#GetPhaseRequest}
主に炊飯器や洗濯機など、動作に段階があるデバイスで、現在の動作段階を確認する際に使用します。デバイスの現在の動作段階をClova Home Extensionにリクエストします。このリクエストに対するレスポンスとして、[`GetPhaseResponse`](#GetPhaseResponse)メッセージを使用する必要があります。

| フィールド名       | データ型    | フィールドの説明                     | 任意 |
|---------------|---------|-----------------------------|:---------:|
| `accessToken`      | string                                  | IoTサービスのユーザーアカウントのアクセストークン。CEKは、外部サービスの認可サーバーから取得したユーザーアカウントのアクセストークンを渡します。詳細については、[ユーザーアカウントをリンクする](/CEK/Guides/Link_User_Account.md)を参照してください。                          | 常時    |
| `appliance`        | [ApplianceInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#ApplianceInfoObject)     | エンドポイントの情報を持つオブジェクト。`applianceId`フィールドは必須です。     | 常時    |

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

### 次の項目も参照してください。
* [`GetPhaseResponse`](#GetPhaseResponse)

## GetPhaseResponse {#GetPhaseResponse}
[`GetPhaseRequest`](#GetPhaseRequest)メッセージに対するレスポンスです。デバイスの現在の動作段階をCEKに返します。

| フィールド名       | データ型    | フィールドの説明                     | 必須/選択 |
|---------------|---------|-----------------------------|:---------:|
| `applianceResponseTimestamp` | string | リクエストがエンドポイントで確認された日時(タイムスタンプ、<a href="https://en.wikipedia.org/wiki/ISO_8601" target="_blank">ISO 8601</a>)     | 選択    |
| `phase`                 | [PhaseInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#PhaseInfoObject) | エンドポイントの現在の動作段階の情報を持つオブジェクト   | 必須    |

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

### 次の項目も参照してください。
* [`GetPhaseRequest`](#GetPhaseRequest)

## GetProgressiveTaxBracketRequest {#GetProgressiveTaxBracketRequest}
主に電力量計やスマートプラグなどのデバイスで、累進税の段階を確認する際に使用します。判断された累進税の段階をClova Home Extensionにリクエストします。このリクエストに対するレスポンスとして、[`GetProgressiveTaxBracketResponse`](#GetProgressiveTaxBracketResponse)メッセージを使用する必要があります。

| フィールド名       | データ型    | フィールドの説明                     | 任意 |
|---------------|---------|-----------------------------|:---------:|
| `accessToken`      | string                                  | IoTサービスのユーザーアカウントのアクセストークン。CEKは、外部サービスの認可サーバーから取得したユーザーアカウントのアクセストークンを渡します。詳細については、[ユーザーアカウントをリンクする](/CEK/Guides/Link_User_Account.md)を参照してください。                          | 常時    |
| `appliance`        | [ApplianceInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#ApplianceInfoObject)     | エンドポイントの情報を持つオブジェクト。`applianceId`フィールドは必須です。     | 常時    |

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

### 次の項目も参照してください。
* [`GetProgressiveTaxBracketResponse`](#GetProgressiveTaxBracketResponse)

## GetProgressiveTaxBracketResponse {#GetProgressiveTaxBracketResponse}

[`GetProgressiveTaxBracketRequest`](#GetProgressiveTaxBracketRequest)メッセージに対するレスポンスです。デバイスで判断された累進税の段階情報をCEKに返します。

| フィールド名       | データ型    | フィールドの説明                     | 必須/選択 |
|---------------|---------|-----------------------------|:---------:|
| `applianceResponseTimestamp` | string | リクエストがエンドポイントで確認された日時(タイムスタンプ、<a href="https://en.wikipedia.org/wiki/ISO_8601" target="_blank">ISO 8601</a>)     | 選択    |
| `progressiveTaxBracket`      | [ProgressiveTaxBracketInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#ProgressiveTaxBracketInfoObject) | 累進税の段階情報を持つオブジェクト  | 必須    |

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

### 次の項目も参照してください。
* [`GetProgressiveTaxBracketRequest`](#GetProgressiveTaxBracketRequest)

## GetRemainingTimeRequest {#GetRemainingTimeRequest}
主に炊飯器や洗濯機のようなデバイスで、動作終了までの残り時間を確認する際に使用します。デバイスの動作終了までの残り時間をClova Home Extensionにリクエストします。このリクエストに対するレスポンスとして、[`GetRemainingTimeResponse`](#GetRemainingTimeResponse)メッセージを使用する必要があります。

| フィールド名       | データ型    | フィールドの説明                     | 任意 |
|---------------|---------|-----------------------------|:---------:|
| `accessToken`      | string                                  | IoTサービスのユーザーアカウントのアクセストークン。CEKは、外部サービスの認可サーバーから取得したユーザーアカウントのアクセストークンを渡します。詳細については、[ユーザーアカウントをリンクする](/CEK/Guides/Link_User_Account.md)を参照してください。                          | 常時    |
| `appliance`        | [ApplianceInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#ApplianceInfoObject)     | エンドポイントの情報を持つオブジェクト。`applianceId`フィールドは必須です。     | 常時    |

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

### 次の項目も参照してください。
* [`GetRemainingTimeResponse`](#GetRemainingTimeResponse)

## GetRemainingTimeResponse {#GetRemainingTimeResponse}

[`GetRemainingTimeRequest`](#GetRemainingTimeRequest)メッセージに対するレスポンスです。デバイスの動作終了までの残り時間をCEKに返します。

| フィールド名       | データ型    | フィールドの説明                     | 必須/選択 |
|---------------|---------|-----------------------------|:---------:|
| `applianceResponseTimestamp` | string | リクエストがエンドポイントで確認された日時(タイムスタンプ、<a href="https://en.wikipedia.org/wiki/ISO_8601" target="_blank">ISO 8601</a>)     | 選択    |
| `remainingTime`              | string | 動作終了までの残り時間(継続時間、<a href="https://en.wikipedia.org/wiki/ISO_8601#Durations" target="_blank">ISO 8601</a>)    | 必須    |

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

### 次の項目も参照してください。
* [`GetRemainingTimeRequest`](#GetRemainingTimeRequest)

## GetRightPostureRatioRequest {#GetRightPostureRatioRequest}
ユーザーが正しい姿勢でデバイスを使用した割合を確認する際に使用します。ユーザーがデバイスを使用する際、特定の期間または現在まで正しい姿勢を保った割合の情報をClova Home Extensionにリクエストします。このリクエストに対するレスポンスとして、[`GetRightPostureRatioResponse`](#GetRightPostureRatioResponse)メッセージを使用する必要があります。

| フィールド名       | データ型    | フィールドの説明                     | 任意 |
|---------------|---------|-----------------------------|:---------:|
| `accessToken`      | string                                  | IoTサービスのユーザーアカウントのアクセストークン。CEKは、外部サービスの認可サーバーから取得したユーザーアカウントのアクセストークンを渡します。詳細については、[ユーザーアカウントをリンクする](/CEK/Guides/Link_User_Account.md)を参照してください。                          | 常時    |
| `appliance`        | [ApplianceInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#ApplianceInfoObject)     | エンドポイントの情報を持つオブジェクト。`applianceId`フィールドは必須です。     | 常時    |
| `period`           | [PeriodInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#PeriodInfoObject)           | 期間情報を持つオブジェクト                                     | 常時   |

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
      "start": "2018-03-28T00:0:00+09:00",
      "end": "2018-03-28T23:59:59+09:00"
    }
  }
}
```

{% endraw %}

### 次の項目も参照してください。
* [`GetRightPostureRatioResponse`](#GetRightPostureRatioResponse)

## GetRightPostureRatioResponse {#GetRightPostureRatioResponse}

[`GetRightPostureRatioRequest`](#GetRightPostureRatioRequest)メッセージに対するレスポンスです。ユーザーが正しい姿勢でデバイスを使用した割合をCEKに返します。

| フィールド名       | データ型    | フィールドの説明                     | 必須/選択 |
|---------------|---------|-----------------------------|:---------:|
| `applianceResponseTimestamp` | string | リクエストがエンドポイントで確認された日時(タイムスタンプ、<a href="https://en.wikipedia.org/wiki/ISO_8601" target="_blank">ISO 8601</a>)     | 選択    |
| `rightPostureRatio`          | [RatioInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#RatioInfoObject) | ユーザーが正しい姿勢でデバイスを使用した割合の情報を持つオブジェクト   | 必須    |

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

### 次の項目も参照してください。
* [`GetRightPostureRatioRequest`](#GetRightPostureRatioRequest)

## GetCurrentSittingStateRequest {#GetCurrentSittingStateRequest}
スマートチェアなどのデバイスで、ユーザーの使用状況を確認する際に使用します。デバイスで検知されたユーザーの着席情報と、直近でユーザーがデバイスを使用した時間の情報をClova Home Extensionにリクエストします。このリクエストに対するレスポンスとして、[`GetCurrentSittingStateResponse`](#GetCurrentSittingStateResponse)メッセージを使用する必要があります。

| フィールド名       | データ型    | フィールドの説明                     | 任意 |
|---------------|---------|-----------------------------|:---------:|
| `accessToken`      | string                                  | IoTサービスのユーザーアカウントのアクセストークン。CEKは、外部サービスの認可サーバーから取得したユーザーアカウントのアクセストークンを渡します。詳細については、[ユーザーアカウントをリンクする](/CEK/Guides/Link_User_Account.md)を参照してください。                          | 常時    |
| `appliance`        | [ApplianceInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#ApplianceInfoObject)     | エンドポイントの情報を持つオブジェクト。`applianceId`フィールドは必須です。     | 常時    |

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

### 次の項目も参照してください。
* [`GetCurrentSittingStateResponse`](#GetCurrentSittingStateResponse)

## GetCurrentSittingStateResponse {#GetCurrentSittingStateResponse}
[`GetCurrentSittingStateRequest`](#GetCurrentSittingStateRequest)メッセージに対するレスポンスです。デバイスで検知されたユーザーの着席情報と、直近でユーザーがデバイスを使用した時間の情報をCEKに返します。

| フィールド名       | データ型    | フィールドの説明                     | 必須/選択 |
|---------------|---------|-----------------------------|:---------:|
| `applianceResponseTimestamp` | string  | リクエストがエンドポイントで確認された日時(タイムスタンプ、<a href="https://en.wikipedia.org/wiki/ISO_8601" target="_blank">ISO 8601</a>)     | 選択    |
| `sittingState`               | [SittingStateInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#SittingStateInfoObject) |  スマートチェアなどのエンドポイントに対する、ユーザーの着席情報を持っています。              | 必須    |
| `recentlySittingPeriod`      | [PeriodInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#PeriodInfoObject) | 直近の使用時間情報を持っているオブジェクト              | 選択    |

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

### 次の項目も参照してください。
* [`GetCurrentSittingStateRequest`](#GetCurrentSittingStateRequest)

## GetSleepScoreRequest {#GetSleepScoreRequest}
睡眠センサーのようなデバイスで、ユーザーの睡眠スコアの情報を確認する際に使用します。デバイスで評価されたユーザーの睡眠スコアをClova Home Extensionにリクエストします。このリクエストに対するレスポンスとして、[`GetSleepScoreResponse`](#GetSleepScoreResponse)メッセージを使用する必要があります。

| フィールド名       | データ型    | フィールドの説明                     | 任意 |
|---------------|---------|-----------------------------|:---------:|
| `accessToken`      | string                                  | IoTサービスのユーザーアカウントのアクセストークン。CEKは、外部サービスの認可サーバーから取得したユーザーアカウントのアクセストークンを渡します。詳細については、[ユーザーアカウントをリンクする](/CEK/Guides/Link_User_Account.md)を参照してください。                          | 常時    |
| `appliance`        | [ApplianceInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#ApplianceInfoObject)     | エンドポイントの情報を持つオブジェクト。`applianceId`フィールドは必須です。     | 常時    |
| `period`           | [PeriodInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#PeriodInfoObject)           | 期間情報を持つオブジェクト                                          | 条件付き  |

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
      "start": "2018-03-28T00:0:00+09:00",
      "end": "2018-03-28T23:59:59+09:00"
    }
  }
}
```

{% endraw %}

### 次の項目も参照してください。
* [`GetSleepScoreResponse`](#GetSleepScoreResponse)

## GetSleepScoreResponse {#GetSleepScoreResponse}
[`GetSleepScoreRequest`](#GetSleepScoreRequest)メッセージに対するレスポンスです。デバイスで評価されたユーザーの睡眠スコアをCEKに返します。

| フィールド名       | データ型    | フィールドの説明                     | 必須/選択 |
|---------------|---------|-----------------------------|:---------:|
| `applianceResponseTimestamp` | string  | リクエストがエンドポイントで確認された日時(タイムスタンプ、<a href="https://en.wikipedia.org/wiki/ISO_8601" target="_blank">ISO 8601</a>)     | 選択    |
| `sleepScore`                 | [SleepScoreInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#SleepScoreInfoObject)  | 睡眠スコアの情報を持つオブジェクト                                                       | 必須    |

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

### 次の項目も参照してください。
* [`GetSleepScoreRequest`](#GetSleepScoreRequest)

## GetSleepStartTimeRequest {#GetSleepStartTimeRequest}
睡眠センサーのようなデバイスで、ユーザーの睡眠スコアの情報を確認する際に使用します。デバイスで測定されたユーザーの睡眠開始時間をClova Home Extensionにリクエストします。このリクエストに対するレスポンスとして、[`GetSleepStartTimeResponse`](#GetSleepStartTimeResponse)メッセージを使用する必要があります。

| フィールド名       | データ型    | フィールドの説明                     | 任意 |
|---------------|---------|-----------------------------|:---------:|
| `accessToken`      | string                                  | IoTサービスのユーザーアカウントのアクセストークン。CEKは、外部サービスの認可サーバーから取得したユーザーアカウントのアクセストークンを渡します。詳細については、[ユーザーアカウントをリンクする](/CEK/Guides/Link_User_Account.md)を参照してください。                          | 常時    |
| `appliance`        | [ApplianceInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#ApplianceInfoObject)     | エンドポイントの情報を持つオブジェクト。`applianceId`フィールドは必須です。     | 常時    |
| `period`           | [PeriodInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#PeriodInfoObject)           | 期間情報を持つオブジェクト                                          | 条件付き  |

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
      "start": "2018-03-28T00:0:00+09:00",
      "end": "2018-03-28T23:59:59+09:00"
    }
  }
}
```

{% endraw %}

### 次の項目も参照してください。
* [`GetSleepStartTimeResponse`](#GetSleepStartTimeResponse)

## GetSleepStartTimeResponse {#GetSleepStartTimeResponse}
[`GetSleepStartTimeRequest`](#GetSleepStartTimeRequest)メッセージに対するレスポンスです。デバイスで測定されたユーザーの睡眠開始時間をCEKに返します。

| フィールド名       | データ型    | フィールドの説明                     | 必須/選択 |
|---------------|---------|-----------------------------|:---------:|
| `applianceResponseTimestamp` | string  | リクエストがエンドポイントで確認された日時(タイムスタンプ、<a href="https://en.wikipedia.org/wiki/ISO_8601" target="_blank">ISO 8601</a>)     | 選択    |
| `startTimestampList[]`       | string  | 日時順で睡眠開始時間を保存している配列                                      | 必須    |

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

### 次の項目も参照してください。
* [`GetSleepStartTimeRequest`](#GetSleepStartTimeRequest)

## GetTargetTemperatureRequest {#GetTargetTemperatureRequest}
主にエアコンやサーモスタットのようなデバイスで、設定温度を確認する際に使用します。デバイスの設定温度をClova Home Extensionにリクエストします。このリクエストに対するレスポンスとして、[`GetTargetTemperatureResponse`](#GetTargetTemperatureResponse)メッセージを使用する必要があります。

| フィールド名       | データ型    | フィールドの説明                     | 任意 |
|---------------|---------|-----------------------------|:---------:|
| `accessToken`      | string                                  | IoTサービスのユーザーアカウントのアクセストークン。CEKは、外部サービスの認可サーバーから取得したユーザーアカウントのアクセストークンを渡します。詳細については、[ユーザーアカウントをリンクする](/CEK/Guides/Link_User_Account.md)を参照してください。                          | 常時    |
| `appliance`        | [ApplianceInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#ApplianceInfoObject)     | エンドポイントの情報を持つオブジェクト。`applianceId`フィールドは必須です。     | 常時    |

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

### 次の項目も参照してください。
* [`GetTargetTemperatureResponse`](#GetTargetTemperatureResponse)

## GetTargetTemperatureResponse {#GetTargetTemperatureResponse}
[`GetTargetTemperatureRequest`](#GetTargetTemperatureRequest)メッセージに対するレスポンスです。デバイスの設定温度をCEKに返します。

| フィールド名       | データ型    | フィールドの説明                     | 必須/選択 |
|---------------|---------|-----------------------------|:---------:|
| `applianceResponseTimestamp` | string | リクエストがエンドポイントで確認された日時(タイムスタンプ、<a href="https://en.wikipedia.org/wiki/ISO_8601" target="_blank">ISO 8601</a>)     | 選択    |
| `targetTemperature`          | [TemperatureInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#TemperatureInfoObject) | デバイスに設定された温度、またはExtensionからリクエストされた設定温度の情報を持つオブジェクト  | 必須    |

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

### 次の項目も参照してください。
* [`GetTargetTemperatureRequest`](#GetTargetTemperatureRequest)

## GetUltraFineDustRequest {#GetUltraFineDustRequest}
主に空気清浄機などのデバイスで測定された超微細粉塵(PM2.5)の情報を確認する際に使用します。超微細粉塵(PM2.5)の情報をClova Home Extensionにリクエストします。このリクエストに対するレスポンスとして、[`GetUltraFineDustResponse`](#GetUltraFineDustResponse)メッセージを使用する必要があります。

| フィールド名       | データ型    | フィールドの説明                     | 任意 |
|---------------|---------|-----------------------------|:---------:|
| `accessToken`      | string                                  | IoTサービスのユーザーアカウントのアクセストークン。CEKは、外部サービスの認可サーバーから取得したユーザーアカウントのアクセストークンを渡します。詳細については、[ユーザーアカウントをリンクする](/CEK/Guides/Link_User_Account.md)を参照してください。                          | 常時    |
| `appliance`        | [ApplianceInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#ApplianceInfoObject)     | エンドポイントの情報を持つオブジェクト。`applianceId`フィールドは必須です。     | 常時    |

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

### 次の項目も参照してください。
* [`GetUltraFineDustResponse`](#GetUltraFineDustResponse)

## GetUltraFineDustResponse {#GetUltraFineDustResponse}
[`GetUltraFineDustRequest`](#GetUltraFineDustRequest)メッセージに対するレスポンスです。デバイスで測定された超微細粉塵(PM2.5)の情報をCEKに返します。

| フィールド名       | データ型    | フィールドの説明                     | 必須/選択 |
|---------------|---------|-----------------------------|:---------:|
| `applianceResponseTimestamp` | string | リクエストがエンドポイントで確認された日時(タイムスタンプ、<a href="https://en.wikipedia.org/wiki/ISO_8601" target="_blank">ISO 8601</a>)     | 選択    |
| `ultraFineDust`                 | [UltraFineDustInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#UltraFineDustInfoObject) | デバイスで測定された現在の超微細粉塵(PM2.5)の情報を持つオブジェクト   | 必須    |

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

### 次の項目も参照してください。
* [`GetUltraFineDustRequest`](#GetUltraFineDustRequest)

## GetUsageTimeRequest {#GetUsageTimeRequest}
デバイスの使用時間を確認する際に使用します。特定の期間または現在までの累積使用時間をClova Home Extensionにリクエストします。このリクエストに対するレスポンスとして、[`GetUsageTimeResponse`](#GetUsageTimeResponse)メッセージを使用する必要があります。

| フィールド名       | データ型    | フィールドの説明                     | 任意 |
|---------------|---------|-----------------------------|:---------:|
| `accessToken`      | string                                  | IoTサービスのユーザーアカウントのアクセストークン。CEKは、外部サービスの認可サーバーから取得したユーザーアカウントのアクセストークンを渡します。詳細については、[ユーザーアカウントをリンクする](/CEK/Guides/Link_User_Account.md)を参照してください。                          | 常時    |
| `appliance`        | [ApplianceInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#ApplianceInfoObject)     | エンドポイントの情報を持つオブジェクト。`applianceId`フィールドは必須です。     | 常時    |
| `period`           | [PeriodInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#PeriodInfoObject)           | 期間情報を持つオブジェクト                                     | 常時   |

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
      "start": "2018-03-28T00:0:00+09:00",
      "end": "2018-03-28T23:59:59+09:00"
    }
  }
}
```

{% endraw %}

### 次の項目も参照してください。
* [`GetUsageTimeResponse`](#GetUsageTimeResponse)

## GetUsageTimeResponse {#GetUsageTimeResponse}

[`GetUsageTimeRequest`](#GetUsageTimeRequest)メッセージに対するレスポンスです。デバイスの累積使用時間をCEKに返します。

| フィールド名       | データ型    | フィールドの説明                     | 必須/選択 |
|---------------|---------|-----------------------------|:---------:|
| `applianceResponseTimestamp` | string | リクエストがエンドポイントで確認された日時(タイムスタンプ、<a href="https://en.wikipedia.org/wiki/ISO_8601" target="_blank">ISO 8601</a>)     | 選択    |
| `usageTime`                  | string | 使用時間(継続時間、<a href="https://en.wikipedia.org/wiki/ISO_8601#Durations" target="_blank">ISO 8601</a>)               | 必須    |

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

### 次の項目も参照してください。
* [`GetUsageTimeRequest`](#GetUsageTimeRequest)

## HealthCheckRequest {#HealthCheckRequest}
デバイスのステータスを把握する際に使用します。デバイスのステータス情報をClova Home Extensionにリクエストします。このリクエストに対するレスポンスとして、[`HealthCheckResponse`](#HealthCheckResponse)メッセージを使用する必要があります。

### Payload fields

| フィールド名       | データ型    | フィールドの説明                     | 任意 |
|---------------|---------|-----------------------------|:---------:|
| `accessToken`   | string  | Clova Home Extensionのアクセストークン | 常時    |
| `appliance`     | [ApplianceInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#ApplianceInfoObject)     | エンドポイントの情報を持つオブジェクト。`applianceId`フィールドは必須です。     | 常時    |

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

### 次の項目も参照してください。
* [`HealthCheckResponse`](#HealthCheckResponse)

## HealthCheckResponse {#HealthCheckResponse}
[`HealthCheckRequest`](#HealthCheckRequest)メッセージに対するレスポンスです。デバイスのステータス情報をCEKに返します。

### Payload fields

| フィールド名       | データ型    | フィールドの説明                     | 必須/選択 |
|---------------|---------|-----------------------------|:---------:|
| `isReachable` | boolean | ネットワークでデバイスにアクセスできるかを示す値。<ul><li><code>true</code>：アクセス可能(オンライン)</li><li><code>false</code>：アクセス不可(オフライン)</li></ul> | 必須    |
| `isTurnOn`    | boolean | デバイスの動作状態を示す値。<ul><li><code>true</code>：アイドル状態</li><li><code>false</code>：動作中</li></ul>                  | 必須    |

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

### 次の項目も参照してください。
* [`HealthCheckRequest`](#HealthCheckRequest)

## IncrementBrightnessConfirmation {#IncrementBrightnessConfirmation}
[`IncrementBrightnessRequest`](#IncrementBrightnessRequest)メッセージに対するレスポンスです。照明の輝度を上げるように設定した結果をCEKに返します。

### Payload fields

| フィールド名       | データ型    | フィールドの説明                     | 必須/選択 |
|---------------|---------|-----------------------------|:---------:|
| `brightness`               | [BrightnessInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#BrightnessInfoObject) | 現在の輝度情報を持つオブジェクト                                | 選択    |
| `previousState`            | object | エンドポイントの前の状況情報を持つオブジェクト                           | 選択    |
| `previousState.brightness` | [BrightnessInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#BrightnessInfoObject) | 前の輝度情報を持つオブジェクト                                | 選択    |

### 備考

エンドポイントからペイロードに入力する情報を取得できない場合、値を省略できます。その場合、ユーザーには具体的な情報なしに、リクエストが正常に処理されたことを通知します。

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

### 次の項目も参照してください。
* [`IncrementBrightnessRequest`](#IncrementBrightnessRequest)

## IncrementBrightnessRequest {#IncrementBrightnessRequest}
主に照明などのデバイスを制御する際に使用します。照明の輝度を指定された値に上げるようClova Home Extensionにリクエストします。このリクエストに対するレスポンスとして、[`IncrementBrightnessConfirmation`](#IncrementBrightnessConfirmation)メッセージを使用する必要があります。

### Payload fields

| フィールド名       | データ型    | フィールドの説明                     | 任意 |
|---------------|---------|-----------------------------|:---------:|
| `accessToken`      | string                                  | IoTサービスのユーザーアカウントのアクセストークン。CEKは、外部サービスの認可サーバーから取得したユーザーアカウントのアクセストークンを渡します。詳細については、[ユーザーアカウントをリンクする](/CEK/Guides/Link_User_Account.md)を参照してください。                          | 常時    |
| `appliance`        | [ApplianceInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#ApplianceInfoObject)     | エンドポイントの情報を持つオブジェクト。`applianceId`フィールドは必須です。     | 常時    |
| `deltaBrightness`       | [BrightnessInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#BrightnessInfoObject)             | 変更する輝度情報を持つオブジェクト                              | 常時    |

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

### 次の項目も参照してください。
* [`IncrementBrightnessConfirmation`](#IncrementBrightnessConfirmation)

## IncrementChannelConfirmation {#IncrementChannelConfirmation}
[`IncrementChannelRequest`](#IncrementChannelRequest)メッセージに対するレスポンスです。テレビのチャンネルを上げるように設定した結果をCEKに返します。

### Payload fields

| フィールド名       | データ型    | フィールドの説明                     | 必須/選択 |
|---------------|---------|-----------------------------|:---------:|
| `channel`               | [TVChannelInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#TVChannelInfoObject) | 現在のテレビチャンネルの情報を持つオブジェクト                                | 選択    |
| `previousState`            | object | エンドポイントの前の状況情報を持つオブジェクト                           | 選択    |
| `previousState.channel` | [TVChannelInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#TVChannelInfoObject) | 前のテレビチャンネル情報を持つオブジェクト                                | 選択    |

### 備考

エンドポイントからペイロードに入力する情報を取得できない場合、値を省略できます。その場合、ユーザーには具体的な情報なしに、リクエストが正常に処理されたことを通知します。

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
    "previousState": {
      "channel": {
        "value": 15
      }
    }
  }
}
```

{% endraw %}

### 次の項目も参照してください。
* [`IncrementChannelRequest`](#IncrementChannelRequest)

## IncrementChannelRequest {#IncrementChannelRequest}
主にテレビやセットトップボックスを制御する際に使用します。テレビのチャンネルを指定された値に上げるようClova Home Extensionにリクエストします。このリクエストに対するレスポンスとして、[`IncrementChannelConfirmation`](#IncrementChannelConfirmation)メッセージを使用する必要があります。

### Payload fields

| フィールド名       | データ型    | フィールドの説明                     | 任意 |
|---------------|---------|-----------------------------|:---------:|
| `accessToken`      | string                                  | IoTサービスのユーザーアカウントのアクセストークン。CEKは、外部サービスの認可サーバーから取得したユーザーアカウントのアクセストークンを渡します。詳細については、[ユーザーアカウントをリンクする](/CEK/Guides/Link_User_Account.md)を参照してください。                          | 常時    |
| `appliance`        | [ApplianceInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#ApplianceInfoObject)     | エンドポイントの情報を持つオブジェクト。`applianceId`フィールドは必須です。     | 常時    |
| `deltaChannel`       | [TVChannelInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#TVChannelInfoObject)             | 変更するテレビチャンネルの値を持つオブジェクト                              | 常時    |

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

### 次の項目も参照してください。
* [`IncrementChannelConfirmation`](#IncrementChannelConfirmation)

## IncrementFanSpeedConfirmation {#IncrementFanSpeedConfirmation}
[`IncrementFanSpeedRequest`](#IncrementFanSpeedRequest)メッセージに対するレスポンスです。ファンの速度を上げるように設定した結果をCEKに返します。

### Payload fields

| フィールド名       | データ型    | フィールドの説明                     | 必須/選択 |
|---------------|---------|-----------------------------|:---------:|
| `fanSpeed`            | [SpeedInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#SpeedInfoObject) | 現在のファンの速度情報を持つオブジェクト。ファンの速度とは風速のことで、次のいずれかになります。<ul><li><code>1</code>：弱風(1段階)</li><li><code>2</code>：中風(2段階)</li><li><code>3</code>：強風(3段階)</li></ul> | 選択    |
| `previousState`          | object                      | エンドポイントの前の状況情報を持つオブジェクト                 | 選択    |
| `previousState.FanSpeed` | [SpeedInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#SpeedInfoObject) | 前のファンの速度情報を持つオブジェクト。ファンの速度とは風速のことで、次のいずれかになります。<ul><li><code>1</code>：弱風(1段階)</li><li><code>2</code>：中風(2段階)</li><li><code>3</code>：強風(3段階)</li></ul> | 選択    |

### 備考

エンドポイントからペイロードに入力する情報を取得できない場合、値を省略できます。その場合、ユーザーには具体的な情報なしに、リクエストが正常に処理されたことを通知します。

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

### 次の項目も参照してください。
* [`IncrementFanSpeedRequest`](#IncrementFanSpeedRequest)

## IncrementFanSpeedRequest {#IncrementFanSpeedRequest}
主に空気清浄機などのデバイスを制御する際に使用します。ファンの速度を指定された値に上げるようClova Home Extensionにリクエストします。このリクエストに対するレスポンスとして、[`IncrementFanSpeedConfirmation`](#IncrementFanSpeedConfirmation)メッセージを使用する必要があります。

### Payload fields

| フィールド名       | データ型    | フィールドの説明                     | 任意 |
|---------------|---------|-----------------------------|:---------:|
| `accessToken`      | string                                  | IoTサービスのユーザーアカウントのアクセストークン。CEKは、外部サービスの認可サーバーから取得したユーザーアカウントのアクセストークンを渡します。詳細については、[ユーザーアカウントをリンクする](/CEK/Guides/Link_User_Account.md)を参照してください。                          | 常時    |
| `appliance`        | [ApplianceInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#ApplianceInfoObject)     | エンドポイントの情報を持つオブジェクト。`applianceId`フィールドは必須です。 | 常時    |
| `deltaFanSpeed` | [SpeedInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#SpeedInfoObject) | 変更する速度情報を持っているオブジェクト。ファンの速度とは風速のことで、次のいずれかになります。<ul><li><code>1</code>：弱風(1段階)</li><li><code>2</code>：中風(2段階)</li><li><code>3</code>：強風(3段階)</li></ul>  | 常時    |

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

### 次の項目も参照してください。
* [`IncrementFanSpeedConfirmation`](#IncrementFanSpeedConfirmation)

## IncrementIntensityLevelConfirmation {#IncrementIntensityLevelConfirmation}
[`DecrementIntensityLevelRequest`](#DecrementIntensityLevelRequest)メッセージに対するレスポンスです。圧力や水圧などの強度を上げるように設定した結果をCEKに返します。

### Payload fields

| フィールド名       | データ型    | フィールドの説明                     | 必須/選択 |
|---------------|---------|-----------------------------|:---------:|
| `intensityLevel` | [IntensityLevelInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#IntensityLevelInfoObject) | 現在の圧力/水圧などの強度情報を持つオブジェクト                  | 選択    |
| `previousState`  | object                                  | エンドポイントの前の状況情報を持つオブジェクト                           | 選択    |
| `previousState.intensityLevel` | [IntensityLevelInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#IntensityLevelInfoObject) | 前の圧力/水圧などの強度情報を持つオブジェクト    | 選択    |

### 備考

エンドポイントからペイロードに入力する情報を取得できない場合、値を省略できます。その場合、ユーザーには具体的な情報なしに、リクエストが正常に処理されたことを通知します。

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

### 次の項目も参照してください。
* [`IncrementIntensityLevelRequest`](#IncrementIntensityLevelRequest)

## IncrementIntensityLevelRequest {#IncrementIntensityLevelRequest}
圧力や水圧などの強度を指定された値に上げるようClova Home Extensionにリクエストします。このリクエストに対するレスポンスとして、[`IncrementIntensityLevelConfirmation`](#IncrementIntensityLevelConfirmation)メッセージを使用する必要があります。

### Payload fields

| フィールド名       | データ型    | フィールドの説明                     | 任意 |
|---------------|---------|-----------------------------|:---------:|
| `accessToken`      | string                                  | IoTサービスのユーザーアカウントのアクセストークン。CEKは、外部サービスの認可サーバーから取得したユーザーアカウントのアクセストークンを渡します。詳細については、[ユーザーアカウントをリンクする](/CEK/Guides/Link_User_Account.md)を参照してください。                          | 常時    |
| `appliance`        | [ApplianceInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#ApplianceInfoObject)     | エンドポイントの情報を持つオブジェクト。`applianceId`フィールドは必須です。 | 常時    |
| `deltaIntensity`   | [IntensityLevelInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#IntensityLevelInfoObject) | 変更する圧力や水圧の強度情報を持っているオブジェクト           | 常時    |

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

### 次の項目も参照してください。
* [`IncrementIntensityLevelConfirmation`](#IncrementIntensityLevelConfirmation)

## IncrementTargetTemperatureConfirmation {#IncrementTargetTemperatureConfirmation}
[`IncrementTargetTemperatureRequest`](#IncrementTargetTemperatureRequest)メッセージに対するレスポンスです。温度を上げるように設定した結果をCEKに返します。

### Payload fields

| フィールド名       | データ型    | フィールドの説明                     | 必須/選択 |
|---------------|---------|-----------------------------|:---------:|
| `previousState`     | object                                  | エンドポイントの前の状況情報を持つオブジェクト                              | 選択    |
| `previousState.targetTemperature` | [TemperatureInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#TemperatureInfoObject) | 前の設定温度の情報を持つオブジェクト                 | 選択    |
| `targetTemperature` | [TemperatureInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#TemperatureInfoObject) | デバイスに設定された温度、またはExtensionからリクエストされた設定温度の情報を持つオブジェクト                               | 選択    |

### 備考

エンドポイントからペイロードに入力する情報を取得できない場合、値を省略できます。その場合、ユーザーには具体的な情報なしに、リクエストが正常に処理されたことを通知します。

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

### 次の項目も参照してください。
* [`IncrementTargetTemperatureRequest`](#IncrementTargetTemperatureRequest)

## IncrementTargetTemperatureRequest {#IncrementTargetTemperatureRequest}
主にエアコンやサーモスタットのようなデバイスを制御する際に使用します。指定された値に温度を上げるようClova Home Extensionにリクエストします。このリクエストに対するレスポンスとして、[`IncrementTargetTemperatureConfirmation`](#IncrementTargetTemperatureConfirmation)メッセージを使用する必要があります。

### Payload fields

| フィールド名       | データ型    | フィールドの説明                     | 任意 |
|---------------|---------|-----------------------------|:---------:|
| `accessToken`      | string | IoTサービスのユーザーアカウントのアクセストークン。CEKは、外部サービスの認可サーバーから取得したユーザーアカウントのアクセストークンを渡します。詳細については、[ユーザーアカウントをリンクする](/CEK/Guides/Link_User_Account.md)を参照してください。 | 常時    |
| `appliance`        | [ApplianceInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#ApplianceInfoObject)     | エンドポイントの情報を持つオブジェクト。`applianceId`フィールドは必須です。 | 常時    |
| `deltaTemperature` | [TemperatureInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#TemperatureInfoObject) | 変更する温度情報を持つオブジェクト                              | 常時    |

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

### 次の項目も参照してください。
* [`IncrementTargetTemperatureConfirmation`](#IncrementTargetTemperatureConfirmation)

## IncrementVolumeConfirmation {#IncrementVolumeConfirmation}
[`IncrementVolumeRequest`](#IncrementVolumeRequest)メッセージに対するレスポンスです。スピーカーの音量を上げるように設定した結果をCEKに返します。

### Payload fields

| フィールド名       | データ型    | フィールドの説明                     | 必須/選択 |
|---------------|---------|-----------------------------|:---------:|
| `previousState`     | object                                 | エンドポイントの前の状況情報を持つオブジェクト                              | 選択    |
| `previousState.targetVolume` | [VolumeInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#VolumeInfoObject) | 前の音量情報を持つオブジェクト                 | 選択    |
| `targetVolume` | [VolumeInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#VolumeInfoObject)               | デバイスに設定されたか、またはExtensionからリクエストされた音量情報を持つオブジェクト                 | 選択    |

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

### 次の項目も参照してください。
* [`IncrementVolumeRequest`](#IncrementVolumeRequest)

## IncrementVolumeRequest {#IncrementVolumeRequest}
主にテレビのセットトップボックスなどのデバイスを制御する際に使用します。スピーカーの音量を指定された値に上げるようClova Home Extensionにリクエストします。このリクエストに対するレスポンスとして、[`IncrementVolumeConfirmation`](#IncrementVolumeConfirmation)メッセージを使用する必要があります。

### Payload fields

| フィールド名       | データ型    | フィールドの説明                     | 任意 |
|---------------|---------|-----------------------------|:---------:|
| `accessToken`      | string                                  | IoTサービスのユーザーアカウントのアクセストークン。CEKは、外部サービスの認可サーバーから取得したユーザーアカウントのアクセストークンを渡します。詳細については、[ユーザーアカウントをリンクする](/CEK/Guides/Link_User_Account.md)を参照してください。                          | 常時    |
| `appliance`        | [ApplianceInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#ApplianceInfoObject)     | エンドポイントの情報を持つオブジェクト。`applianceId`フィールドは必須です。 | 常時    |
| `deltaVolume` | [VolumeInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#VolumeInfoObject)                | 変更する音量情報を持つオブジェクト                              | 常時    |

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

### 次の項目も参照してください。
* [`IncrementVolumeConfirmation`](#IncrementVolumeConfirmation)

## LowerConfirmation {#LowerConfirmation}
[`LowerRequest`](#LowerRequest)メッセージに対するレスポンスです。デバイスの高さを下げるように設定した結果をCEKに返します。

### Payload fields

なし

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

### 次の項目も参照してください。
* [`LowerRequest`](#LowerRequest)

## LowerRequest {#LowerRequest}
スマートベッドなどのデバイスを制御する際に使用します。デバイスの高さを下げるようClova Home Extensionにリクエストします。このリクエストに対するレスポンスとして、[`LowerConfirmation`](#LowerConfirmation)メッセージを使用する必要があります。

### Payload fields

| フィールド名       | データ型    | フィールドの説明                     | 任意 |
|---------------|---------|-----------------------------|:---------:|
| `accessToken`      | string                                  | IoTサービスのユーザーアカウントのアクセストークン。CEKは、外部サービスの認可サーバーから取得したユーザーアカウントのアクセストークンを渡します。詳細については、[ユーザーアカウントをリンクする](/CEK/Guides/Link_User_Account.md)を参照してください。                          | 常時    |
| `appliance`        | [ApplianceInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#ApplianceInfoObject)     | エンドポイントの情報を持つオブジェクト。`applianceId`フィールドは必須です。     | 常時    |

### 備考
デバイスの高さは、調整できる範囲内の最大値まで調整されます。高さの調整を途中で止めるには、[StopRequest](#StopRequest)メッセージを受け取る必要があります。

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

### 次の項目も参照してください。
* [`RaiseRequest`](#RaiseRequest)
* [`LowerConfirmation`](#LowerConfirmation)

## MuteConfirmation {#MuteConfirmation}
[`MuteRequest`](#MuteRequest)メッセージに対するレスポンスです。デバイスの音をミュートにするように設定した結果をCEKに返します。

### Payload fields
なし

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

### 次の項目も参照してください。
* [`MuteRequest`](#MuteRequest)

## MuteRequest {#MuteRequest}
主にテレビやセットトップボックスなどのデバイスを制御する際に使用します。デバイスの音をミュートにするようClova Home Extensionにリクエストします。このリクエストに対するレスポンスとして、[`MuteConfirmation`](#MuteConfirmation)メッセージを使用する必要があります。

### Payload fields

| フィールド名       | データ型    | フィールドの説明                     | 任意 |
|---------------|---------|-----------------------------|:---------:|
| `accessToken`      | string                                  | IoTサービスのユーザーアカウントのアクセストークン。CEKは、外部サービスの認可サーバーから取得したユーザーアカウントのアクセストークンを渡します。詳細については、[ユーザーアカウントをリンクする](/CEK/Guides/Link_User_Account.md)を参照してください。                          | 常時    |
| `appliance`        | [ApplianceInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#ApplianceInfoObject)     | エンドポイントの情報を持つオブジェクト。`applianceId`フィールドは必須です。 | 常時    |

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

### 次の項目も参照してください。
* [`MuteConfirmation`](#MuteConfirmation)

## OpenConfirmation {#OpenConfirmation}
[`OpenRequest`](#OpenRequest)メッセージに対するレスポンスです。スマートカーテンや温水洗浄便座の蓋を開けるように設定した結果をCEKに返します。

### Payload fields

なし

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

### 次の項目も参照してください。
* [`OpenRequest`](#OpenRequest)

## OpenRequest {#OpenRequest}
スマートカーテンや温水洗浄便座などのデバイスを制御する際に使用します。スマートカーテンや温水洗浄便座の蓋を開けるようClova Home Extensionにリクエストします。このリクエストに対するレスポンスとして、[`OpenConfirmation`](#OpenConfirmation)メッセージを使用する必要があります。

### Payload fields

| フィールド名       | データ型    | フィールドの説明                     | 任意 |
|---------------|---------|-----------------------------|:---------:|
| `accessToken`      | string                                  | IoTサービスのユーザーアカウントのアクセストークン。CEKは、外部サービスの認可サーバーから取得したユーザーアカウントのアクセストークンを渡します。詳細については、[ユーザーアカウントをリンクする](/CEK/Guides/Link_User_Account.md)を参照してください。                          | 常時    |
| `appliance`        | [ApplianceInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#ApplianceInfoObject)     | エンドポイントの情報を持つオブジェクト。`applianceId`フィールドは必須です。     | 常時    |

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

### 次の項目も参照してください。
* [`OpenConfirmation`](#OpenConfirmation)

## RaiseConfirmation {#RaiseConfirmation}
[`RaiseRequest`](#RaiseRequest)メッセージに対するレスポンスです。デバイスの高さを上げるように設定した結果をCEKに返します。

### Payload fields

なし

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

### 次の項目も参照してください。
* [`RaiseRequest`](#RaiseRequest)

## RaiseRequest {#RaiseRequest}
スマートベッドなどのデバイスを制御する際に使用します。デバイスの高さを上げるようClova Home Extensionにリクエストします。このリクエストに対するレスポンスとして、[`RaiseConfirmation`](#RaiseConfirmation)メッセージを使用する必要があります。

### Payload fields

| フィールド名       | データ型    | フィールドの説明                     | 任意 |
|---------------|---------|-----------------------------|:---------:|
| `accessToken`      | string                                  | IoTサービスのユーザーアカウントのアクセストークン。CEKは、外部サービスの認可サーバーから取得したユーザーアカウントのアクセストークンを渡します。詳細については、[ユーザーアカウントをリンクする](/CEK/Guides/Link_User_Account.md)を参照してください。                          | 常時    |
| `appliance`        | [ApplianceInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#ApplianceInfoObject)     | エンドポイントの情報を持つオブジェクト。`applianceId`フィールドは必須です。     | 常時    |

### 備考
デバイスの高さは、調整できる範囲内の最大値まで調整されます。高さの調整を途中で止めるには、[StopRequest](#StopRequest)メッセージを受け取る必要があります。

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

### 次の項目も参照してください。

* [`LowerRequest`](#LowerRequest)
* [`RaiseConfirmation`](#RaiseConfirmation)

## ReleaseModeConfirmation {#ReleaseModeConfirmation}
[`ReleaseModeRequest`](#ReleaseModeRequest)メッセージに対するレスポンスです。デバイスの現在の運転モード(operation mode)を解除するように設定した結果をCEKに返します。

### Payload fields

| フィールド名       | データ型    | フィールドの説明                     | 必須/選択 |
|---------------|---------|-----------------------------|:---------:|
| `mode`          | [ModeInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#ModeInfoObject)  | 運転モード解除のリクエストによってデバイスに設定されたか、またはExtensionから戻るようにリクエストされた運転モードの情報を持つオブジェクト      | 選択    |
| `previousState` | [ModeInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#ModeInfoObject)  | 運転モード解除のリクエストを受信する前に、デバイスに設定されていた運転モードの情報を持つオブジェクト      | 選択    |

### 備考

エンドポイントからペイロードに入力する情報を取得できない場合、値を省略できます。その場合、ユーザーには具体的な情報なしに、リクエストが正常に処理されたことを通知します。

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

### 次の項目も参照してください。
* [`ReleaseModeRequest`](#ReleaseModeRequest)

## ReleaseModeRequest {#ReleaseModeRequest}
現在、デバイスに設定されている運転モード(operation mode)を解除する際に使用します。デバイスの運転モードを解除し、前の運転モードまたはデフォルトの運転モードに戻るようにClova Home Extensionにリクエストします。このリクエストに対するレスポンスとして、[`ReleaseModeConfirmation`](#ReleaseModeConfirmation)メッセージを使用する必要があります。

### Payload fields

| フィールド名       | データ型    | フィールドの説明                     | 任意 |
|---------------|---------|-----------------------------|:---------:|
| `accessToken` | string  | IoTサービスのユーザーアカウントのアクセストークン。CEKは、外部サービスの認可サーバーから取得したユーザーアカウントのアクセストークンを渡します。詳細については、[ユーザーアカウントをリンクする](/CEK/Guides/Link_User_Account.md)を参照してください。 | 常時    |
| `appliance`   | [ApplianceInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#ApplianceInfoObject)     | エンドポイントの情報を持つオブジェクト。`applianceId`フィールドは必須です。 | 常時    |
| `mode`        | [ModeInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#ModeInfoObject) | デバイスから解除する運転モードの情報を持つオブジェクト                         | 常時    |

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

### 次の項目も参照してください。
* [`ReleaseModeConfirmation`](#ReleaseModeConfirmation)

## SetBrightnessConfirmation {#SetBrightnessConfirmation}
[`SetBrightnessRequest`](#SetBrightnessRequest)メッセージに対するレスポンスです。照明の輝度を変更するように設定した結果をCEKに返します。

### Payload fields

| フィールド名       | データ型    | フィールドの説明                     | 必須/選択 |
|---------------|---------|-----------------------------|:---------:|
| `brightness`               | [BrightnessInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#BrightnessInfoObject) | デバイスに設定されたか、またはExtensionからリクエストされた輝度情報を持つオブジェクト                                | 選択    |

### 備考

エンドポイントからペイロードに入力する情報を取得できない場合、値を省略できます。その場合、ユーザーには具体的な情報なしに、リクエストが正常に処理されたことを通知します。

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

### 次の項目も参照してください。
* [`SetBrightnessRequest`](#SetBrightnessRequest)

## SetBrightnessRequest {#SetBrightnessRequest}
主に照明などのデバイスを制御する際に使用します。照明の輝度を指定された値に変更するようClova Home Extensionにリクエストします。このリクエストに対するレスポンスとして、[`SetBrightnessConfirmation`](#SetBrightnessConfirmation)メッセージを使用する必要があります。

### Payload fields

| フィールド名       | データ型    | フィールドの説明                     | 任意 |
|---------------|---------|-----------------------------|:---------:|
| `accessToken`   | string | IoTサービスのユーザーアカウントのアクセストークン。CEKは、外部サービスの認可サーバーから取得したユーザーアカウントのアクセストークンを渡します。詳細については、[ユーザーアカウントをリンクする](/CEK/Guides/Link_User_Account.md)を参照してください。                          | 常時    |
| `appliance`     | [ApplianceInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#ApplianceInfoObject) | エンドポイントの情報を持つオブジェクト。`applianceId`フィールドは必須です。 | 常時    |
| `brightness`       | [BrightnessInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#BrightnessInfoObject) | 設定する輝度情報を持つオブジェクト                | 常時    |

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

### 次の項目も参照してください。
* [`SetBrightnessConfirmation`](#SetBrightnessConfirmation)

## SetChannelByNameConfirmation {#SetChannelByNameConfirmation}
[`SetChannelByNameRequest`](#SetChannelByNameRequest)メッセージに対するレスポンスです。指定されたチャンネル名にテレビのチャンネルを変更するように設定した結果をCEKに返します。

### Payload fields

| フィールド名       | データ型    | フィールドの説明                     | 必須/選択 |
|---------------|---------|-----------------------------|:---------:|
| `channelName`               | [TVChannelNameInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#TVChannelNameInfoObject) | デバイスに設定されたか、またはExtensionからリクエストされたチャンネル名の情報を持つオブジェクト                                | 選択    |

### 備考

エンドポイントからペイロードに入力する情報を取得できない場合、値を省略できます。その場合、ユーザーには具体的な情報なしに、リクエストが正常に処理されたことを通知します。

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

### 次の項目も参照してください。
* [`SetChannelByNameRequest`](#SetChannelByNameRequest)

## SetChannelByNameRequest {#SetChannelByNameRequest}
主にテレビのセットトップボックスなどのデバイスを制御する際に使用します。指定されたチャンネル名にチャンネルを変更するようClova Home Extensionにリクエストします。このリクエストに対するレスポンスとして、[`SetChannelByNameConfirmation`](#SetChannelByNameConfirmation)メッセージを使用する必要があります。

### Payload fields

| フィールド名       | データ型    | フィールドの説明                     | 任意 |
|---------------|---------|-----------------------------|:---------:|
| `accessToken`   | string | IoTサービスのユーザーアカウントのアクセストークン。CEKは、外部サービスの認可サーバーから取得したユーザーアカウントのアクセストークンを渡します。詳細については、[ユーザーアカウントをリンクする](/CEK/Guides/Link_User_Account.md)を参照してください。                          | 常時    |
| `appliance`     | [ApplianceInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#ApplianceInfoObject) | エンドポイントの情報を持つオブジェクト。`applianceId`フィールドは必須です。 | 常時    |
| `channelName`       | [TVChannelNameInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#TVChannelNameInfoObject) | 設定するテレビチャンネル名の情報を持つオブジェクト                | 常時    |

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

### 次の項目も参照してください。
* [`SetChannelByNameConfirmation`](#SetChannelByNameConfirmation)

## SetChannelConfirmation {#SetChannelConfirmation}
[`SetChannelRequest`](#SetChannelRequest)メッセージに対するレスポンスです。指定されたチャンネル番号にテレビのチャンネルを変更するように設定した結果をCEKに返します。

### Payload fields

| フィールド名       | データ型    | フィールドの説明                     | 必須/選択 |
|---------------|---------|-----------------------------|:---------:|
| `channel`     | [TVChannelInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#TVChannelInfoObject)  | デバイスに設定されたか、またはExtensionからリクエストされたチャンネルの情報を持つオブジェクト      | 選択    |

### 備考

エンドポイントからペイロードに入力する情報を取得できない場合、値を省略できます。その場合、ユーザーには具体的な情報なしに、リクエストが正常に処理されたことを通知します。

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
    }
  }
}
```

{% endraw %}

### 次の項目も参照してください。
* [`SetChannelRequest`](#SetChannelRequest)

## SetChannelRequest {#SetChannelRequest}
主にテレビのセットトップボックスなどのデバイスを制御する際に使用します。指定されたチャンネル番号にチャンネルを変更するようClova Home Extensionにリクエストします。このリクエストに対するレスポンスとして、[`SetChannelConfirmation`](#SetChannelConfirmation)メッセージを使用する必要があります。

### Payload fields

| フィールド名       | データ型    | フィールドの説明                     | 任意 |
|---------------|---------|-----------------------------|:---------:|
| `accessToken`   | string | IoTサービスのユーザーアカウントのアクセストークン。CEKは、外部サービスの認可サーバーから取得したユーザーアカウントのアクセストークンを渡します。詳細については、[ユーザーアカウントをリンクする](/CEK/Guides/Link_User_Account.md)を参照してください。                          | 常時    |
| `appliance`     | [ApplianceInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#ApplianceInfoObject) | エンドポイントの情報を持つオブジェクト。`applianceId`フィールドは必須です。 | 常時    |
| `channel`       | [TVChannelInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#TVChannelInfoObject) | 設定するテレビチャンネルの情報を持つオブジェクト                | 常時    |

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
    }
  }
}
```

{% endraw %}

### 次の項目も参照してください。
* [`SetChannelConfirmation`](#SetChannelConfirmation)

## SetColorConfirmation {#SetColorConfirmation}
[`SetColorRequest`](#SetColorRequest)メッセージに対するレスポンスです。照明や画面、電球の色を変更するように設定した結果をCEKに返します。

### Payload fields

| フィールド名       | データ型    | フィールドの説明                     | 必須/選択 |
|---------------|---------|-----------------------------|:---------:|
| `color`   | [ColorInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#ColorInfoObject) | デバイスに設定されたか、またはExtensionからリクエストされた照明や画面、電球の色の情報を持つオブジェクト                                | 選択    |

### 備考

エンドポイントからペイロードに入力する情報を取得できない場合、値を省略できます。その場合、ユーザーには具体的な情報なしに、リクエストが正常に処理されたことを通知します。

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

### 次の項目も参照してください。
* [`SetColorRequest`](#SetColorRequest)

## SetColorRequest {#SetColorRequest}
主にスマート照明などのデバイスを制御する際に使用します。照明や画面、電球の色を変更するようClova Home Extensionにリクエストします。このリクエストに対するレスポンスとして、[`SetColorConfirmation`](#SetColorConfirmation)メッセージを使用する必要があります。

### Payload fields

| フィールド名       | データ型    | フィールドの説明                     | 任意 |
|---------------|---------|-----------------------------|:---------:|
| `accessToken`   | string | IoTサービスのユーザーアカウントのアクセストークン。CEKは、外部サービスの認可サーバーから取得したユーザーアカウントのアクセストークンを渡します。詳細については、[ユーザーアカウントをリンクする](/CEK/Guides/Link_User_Account.md)を参照してください。                          | 常時    |
| `appliance`     | [ApplianceInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#ApplianceInfoObject) | エンドポイントの情報を持つオブジェクト。`applianceId`フィールドは必須です。 | 常時    |
| `color`         | [ColorInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#ColorInfoObject) | 照明や画面、電球に設定する色の情報を持っているオブジェクト            | 常時    |

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

### 次の項目も参照してください。
* [`SetColorConfirmation`](#SetColorConfirmation)

## SetColorTemperatureConfirmation {#SetColorTemperatureConfirmation}
[`SetColorTemperatureRequest`](#SetColorTemperatureRequest)メッセージに対するレスポンスです。照明や画面、電球の色温度を変更するように設定した結果をCEKに返します。

### Payload fields

| フィールド名       | データ型    | フィールドの説明                     | 必須/選択 |
|---------------|---------|-----------------------------|:---------:|
| `colorTemperature`   | [ColorTemperatureInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#ColorTemperatureInfoObject) | デバイスに設定されたか、またはExtensionからリクエストされた照明や画面、電球の色温度の情報を持つオブジェクト                                | 選択    |

### 備考

エンドポイントからペイロードに入力する情報を取得できない場合、値を省略できます。その場合、ユーザーには具体的な情報なしに、リクエストが正常に処理されたことを通知します。

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

### 次の項目も参照してください。
* [`SetColorTemperatureRequest`](#SetColorTemperatureRequest)

## SetColorTemperatureRequest {#SetColorTemperatureRequest}
主にスマート照明などのデバイスを制御する際に使用します。照明や画面、電球の色温度を変更するようClova Home extensionにリクエストします。このリクエストに対するレスポンスとして、[`SetColorTemperatureConfirmation`](#SetColorTemperatureConfirmation)メッセージを使用する必要があります。

### Payload fields

| フィールド名       | データ型    | フィールドの説明                     | 任意 |
|---------------|---------|-----------------------------|:---------:|
| `accessToken`   | string | IoTサービスのユーザーアカウントのアクセストークン。CEKは、外部サービスの認可サーバーから取得したユーザーアカウントのアクセストークンを渡します。詳細については、[ユーザーアカウントをリンクする](/CEK/Guides/Link_User_Account.md)を参照してください。                          | 常時    |
| `appliance`     | [ApplianceInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#ApplianceInfoObject) | エンドポイントの情報を持つオブジェクト。`applianceId`フィールドは必須です。 | 常時    |
| `colorTemperature` | [ColorTemperatureInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#ColorTemperatureInfoObject) | 照明や画面、電球に設定する色温度の情報を持っているオブジェクト                | 常時    |

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

### 次の項目も参照してください。
* [`SetColorTemperatureConfirmation`](#SetColorTemperatureConfirmation)

## SetFanSpeedConfirmation {#SetFanSpeedConfirmation}
[`SetFanSpeedRequest`](#SetFanSpeedRequest)メッセージに対するレスポンスです。ファンの速度を変更するように設定した結果をCEKに返します。

### Payload fields

| フィールド名       | データ型    | フィールドの説明                     | 必須/選択 |
|---------------|---------|-----------------------------|:---------:|
| `fanSpeed`               | [SpeedInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#SpeedInfoObject) | デバイスに設定されたか、またはExtensionからリクエストされたファンの速度情報を持つオブジェクト。ファンの速度とは風速のことで、次のいずれかになります。<ul><li><code>1</code>：弱風(1段階)</li><li><code>2</code>：中風(2段階)</li><li><code>3</code>：強風(3段階)</li></ul>   | 選択    |

### 備考

エンドポイントからペイロードに入力する情報を取得できない場合、値を省略できます。その場合、ユーザーには具体的な情報なしに、リクエストが正常に処理されたことを通知します。

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

### 次の項目も参照してください。
* [`SetFanSpeedRequest`](#SetFanSpeedRequest)

## SetFanSpeedRequest {#SetFanSpeedRequest}
主に空気清浄機などのデバイスを制御する際に使用します。ファンの速度を指定された値に変更するようClova Home Extensionにリクエストします。このリクエストに対するレスポンスとして、[`SetFanSpeedConfirmation`](#SetFanSpeedConfirmation)メッセージを使用する必要があります。

### Payload fields

| フィールド名       | データ型    | フィールドの説明                     | 任意 |
|---------------|---------|-----------------------------|:---------:|
| `accessToken`   | string | IoTサービスのユーザーアカウントのアクセストークン。CEKは、外部サービスの認可サーバーから取得したユーザーアカウントのアクセストークンを渡します。詳細については、[ユーザーアカウントをリンクする](/CEK/Guides/Link_User_Account.md)を参照してください。                          | 常時    |
| `appliance`     | [ApplianceInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#ApplianceInfoObject) | エンドポイントの情報を持つオブジェクト。`applianceId`フィールドは必須です。 | 常時    |
| `fanSpeed`       | [SpeedInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#SpeedInfoObject) | 設定するファンの速度情報を持つオブジェクトファンの速度とは風速のことで、次のいずれかになります。<ul><li><code>1</code>：弱風(1段階)</li><li><code>2</code>：中風(2段階)</li><li><code>3</code>：強風(3段階)</li></ul>     | 常時    |

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

### 次の項目も参照してください。
* [`SetFanSpeedConfirmation`](#SetFanSpeedConfirmation)

## SetFreezerTargetTemperatureConfirmation {#SetFreezerTargetTemperatureConfirmation}
[`SetFreezerTargetTemperatureRequest`](#SetFreezerTargetTemperatureRequest)メッセージに対するレスポンスです。冷凍室の設定温度を変更するように設定した結果をCEKに返します。

### Payload fields

| フィールド名       | データ型    | フィールドの説明                     | 必須/選択 |
|---------------|---------|-----------------------------|:---------:|
| `targetTemperature`               | [TemperatureInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#TemperatureInfoObject) | デバイスに設定された温度、またはExtensionからリクエストされた設定温度の情報を持つオブジェクト                                | 選択    |

### 備考

エンドポイントからペイロードに入力する情報を取得できない場合、値を省略できます。その場合、ユーザーには具体的な情報なしに、リクエストが正常に処理されたことを通知します。

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

### 次の項目も参照してください。
* [`SetFreezerTargetTemperatureRequest`](#SetFreezerTargetTemperatureRequest)

## SetFreezerTargetTemperatureRequest {#SetFreezerTargetTemperatureRequest}
冷蔵庫などのデバイスを制御する際に使用します。冷凍庫の設定温度を指定された値に変更するようClova Home extensionにリクエストします。このリクエストに対するレスポンスとして、[`SetFreezerTargetTemperatureConfirmation`](#SetFreezerTargetTemperatureConfirmation)メッセージを使用する必要があります。

### Payload fields

| フィールド名       | データ型    | フィールドの説明                     | 任意 |
|---------------|---------|-----------------------------|:---------:|
| `accessToken`   | string | IoTサービスのユーザーアカウントのアクセストークン。CEKは、外部サービスの認可サーバーから取得したユーザーアカウントのアクセストークンを渡します。詳細については、[ユーザーアカウントをリンクする](/CEK/Guides/Link_User_Account.md)を参照してください。                          | 常時    |
| `appliance`     | [ApplianceInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#ApplianceInfoObject) | エンドポイントの情報を持つオブジェクト。`applianceId`フィールドは必須です。        | 常時    |
| `targetTemperature`       | [TemperatureInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#TemperatureInfoObject) | 設定する温度情報を持つオブジェクト     | 常時    |

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

### 次の項目も参照してください。
* [`SetFreezerTargetTemperatureConfirmation`](#SetFreezerTargetTemperatureConfirmation)

## SetFridgeTargetTemperatureConfirmation {#SetFridgeTargetTemperatureConfirmation}
[`SetFridgeTargetTemperatureRequest`](#SetFridgeTargetTemperatureRequest)メッセージに対するレスポンスです。冷蔵室の設定温度を変更するように設定した結果をCEKに返します。

### Payload fields

| フィールド名       | データ型    | フィールドの説明                     | 必須/選択 |
|---------------|---------|-----------------------------|:---------:|
| `targetTemperature`               | [TemperatureInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#TemperatureInfoObject) | デバイスに設定された温度、またはExtensionからリクエストされた設定温度の情報を持つオブジェクト                                | 選択    |

### 備考

エンドポイントからペイロードに入力する情報を取得できない場合、値を省略できます。その場合、ユーザーには具体的な情報なしに、リクエストが正常に処理されたことを通知します。

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

### 次の項目も参照してください。
* [`SetFridgeTargetTemperatureRequest`](#SetFridgeTargetTemperatureRequest)

## SetFridgeTargetTemperatureRequest {#SetFridgeTargetTemperatureRequest}
冷蔵庫などのデバイスを制御する際に使用します。冷蔵室の設定温度を指定された値に変更するようClova Home extensionにリクエストします。このリクエストに対するレスポンスとして、[`SetFridgeTargetTemperatureConfirmation`](#SetFridgeTargetTemperatureConfirmation)メッセージを使用する必要があります。

### Payload fields

| フィールド名       | データ型    | フィールドの説明                     | 任意 |
|---------------|---------|-----------------------------|:---------:|
| `accessToken`   | string | IoTサービスのユーザーアカウントのアクセストークン。CEKは、外部サービスの認可サーバーから取得したユーザーアカウントのアクセストークンを渡します。詳細については、[ユーザーアカウントをリンクする](/CEK/Guides/Link_User_Account.md)を参照してください。                          | 常時    |
| `appliance`     | [ApplianceInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#ApplianceInfoObject) | エンドポイントの情報を持つオブジェクト。`applianceId`フィールドは必須です。        | 常時    |
| `targetTemperature`       | [TemperatureInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#TemperatureInfoObject) | 設定する温度情報を持つオブジェクト     | 常時    |

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

### 次の項目も参照してください。
* [`SetFridgeTargetTemperatureConfirmation`](#SetFridgeTargetTemperatureConfirmation)

## SetLockStateConfirmation {#SetLockStateConfirmation}
[`SetLockStateRequest`](#SetLockStateRequest)メッセージに対するレスポンスです。デバイスの開閉を設定した結果をCEKに返します。

### Payload fields

| フィールド名       | データ型    | フィールドの説明                     | 必須/選択 |
|---------------|---------|-----------------------------|:---------:|
| `lockState`   | string  | デバイスに設定されたか、またはExtensionからリクエストされたデバイスのロック状態。次のいずれかになります。<ul><li><code>"LOCKED"</code></li><li><code>"UNLOCKED"</code></li></ul> | 必須    |


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

### 次の項目も参照してください。
* [`SetLockStateRequest`](#SetLockStateRequest)

## SetLockStateRequest {#SetLockStateRequest}
主にスマートバルブなどのデバイスを制御する際に使用します。デバイスの開閉をClova Home Extensionにリクエストします。このリクエストに対するレスポンスとして、[`SetLockStateConfirmation`](#SetLockStateConfirmation)メッセージを使用する必要があります。

### Payload fields

| フィールド名       | データ型    | フィールドの説明                     | 任意 |
|---------------|---------|-----------------------------|:---------:|
| `accessToken`   | string | IoTサービスのユーザーアカウントのアクセストークン。CEKは、外部サービスの認可サーバーから取得したユーザーアカウントのアクセストークンを渡します。詳細については、[ユーザーアカウントをリンクする](/CEK/Guides/Link_User_Account.md)を参照してください。                          | 常時    |
| `appliance`     | [ApplianceInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#ApplianceInfoObject) | エンドポイントの情報を持つオブジェクト。`applianceId`フィールドは必須です。 | 常時    |
| `lockState`       | string | 設定するデバイスのロック状態。次のいずれかになります。<ul><li><code>"LOCKED"</code></li><li><code>"UNLOCKED"</code></li></ul> | 常時    |

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

### 次の項目も参照してください。
* [`SetLockStateConfirmation`](#SetLockStateConfirmation)

## SetModeConfirmation {#SetModeConfirmation}
[`SetModeRequest`](#SetModeRequest)メッセージに対するレスポンスです。運転モード(operation mode)を変更するように設定した結果をCEKに返します。

### Payload fields

| フィールド名       | データ型    | フィールドの説明                     | 必須/選択 |
|---------------|---------|-----------------------------|:---------:|
| `mode`        | [ModeInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#ModeInfoObject)  | デバイスに設定されたか、またはExtensionからリクエストされた運転モードの情報を持つオブジェクト      | 選択    |

### 備考

エンドポイントからペイロードに入力する情報を取得できない場合、値を省略できます。その場合、ユーザーには具体的な情報なしに、リクエストが正常に処理されたことを通知します。

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

### 次の項目も参照してください。
* [`SetModeRequest`](#SetModeRequest)

## SetModeRequest {#SetModeRequest}
デバイスの運転モードを制御する際に使用します。指定された値に運転モードを変更するようClova Home Extensionにリクエストします。このリクエストに対するレスポンスとして、[`SetModeConfirmation`](#SetModeConfirmation)メッセージを使用する必要があります。

### Payload fields

| フィールド名       | データ型    | フィールドの説明                     | 任意 |
|---------------|---------|-----------------------------|:---------:|
| `accessToken` | string  | IoTサービスのユーザーアカウントのアクセストークン。CEKは、外部サービスの認可サーバーから取得したユーザーアカウントのアクセストークンを渡します。詳細については、[ユーザーアカウントをリンクする](/CEK/Guides/Link_User_Account.md)を参照してください。 | 常時    |
| `appliance`   | [ApplianceInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#ApplianceInfoObject)     | エンドポイントの情報を持つオブジェクト。`applianceId`フィールドは必須です。 | 常時    |
| `mode`        | [ModeInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#ModeInfoObject) | 設定する運転モードの情報を持つオブジェクト                         | 常時    |

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

### 次の項目も参照してください。
* [`SetModeConfirmation`](#SetModeConfirmation)

## SetTargetTemperatureConfirmation {#SetTargetTemperatureConfirmation}
[`SetTargetTemperatureRequest`](#SetTargetTemperatureRequest)メッセージに対するレスポンスです。設定温度変更のリクエストを処理した結果をCEKに返します。

### Payload fields

| フィールド名       | データ型    | フィールドの説明                     | 必須/選択 |
|---------------|---------|-----------------------------|:---------:|
| `targetTemperature`               | [TemperatureInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#TemperatureInfoObject) | デバイスに設定された温度、またはExtensionからリクエストされた設定温度の情報を持つオブジェクト                                | 選択    |

### 備考

エンドポイントからペイロードに入力する情報を取得できない場合、値を省略できます。その場合、ユーザーには具体的な情報なしに、リクエストが正常に処理されたことを通知します。

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

### 次の項目も参照してください。
* [`SetTargetTemperatureRequest`](#SetTargetTemperatureRequest)

## SetTargetTemperatureRequest {#SetTargetTemperatureRequest}
主にエアコンやサーモスタットのようなデバイスの制御に使用します。設定温度を指定された値に変更するようClova Home Extensionにリクエストします。このリクエストに対するレスポンスとして、[`SetTargetTemperatureConfirmation`](#SetTargetTemperatureConfirmation)メッセージを使用する必要があります。

### Payload fields

| フィールド名       | データ型    | フィールドの説明                     | 任意 |
|---------------|---------|-----------------------------|:---------:|
| `accessToken`   | string | IoTサービスのユーザーアカウントのアクセストークン。CEKは、外部サービスの認可サーバーから取得したユーザーアカウントのアクセストークンを渡します。詳細については、[ユーザーアカウントをリンクする](/CEK/Guides/Link_User_Account.md)を参照してください。                          | 常時    |
| `appliance`     | [ApplianceInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#ApplianceInfoObject) | エンドポイントの情報を持つオブジェクト。`applianceId`フィールドは必須です。 | 常時    |
| `targetTemperature`       | [TemperatureInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#TemperatureInfoObject) | 設定する温度情報を持つオブジェクト                | 常時    |

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

### 次の項目も参照してください。
* [`SetTargetTemperatureConfirmation`](#SetTargetTemperatureConfirmation)

## StopConfirmation {#StopConfirmation}
[`StopRequest`](#StopRequest)メッセージに対するレスポンスです。動作中止のリクエストを処理した結果をCEKに返します。

### Payload fields

| フィールド名       | データ型    | フィールドの説明                     | 必須 |
|---------------|---------|-----------------------------|:---------:|
| `phase`       | [PhaseInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#PhaseInfoObject) | デバイスが停止する直前に入っていた動作段階の情報を持つオブジェクト   | 選択  |

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
      "value": "洗濯"
    }
  }
}
```

{% endraw %}

### 次の項目も参照してください。
* [`StopRequest`](#StopRequest)

## StopRequest {#StopRequest}
デバイスの現在の動作を中止するようClova Home Extensionにリクエストします。このリクエストに対するレスポンスとして、[`StopConfirmation`](#StopConfirmation)メッセージを使用する必要があります。

### Payload fields

| フィールド名       | データ型    | フィールドの説明                     | 任意 |
|---------------|---------|-----------------------------|:---------:|
| `accessToken`      | string                                  | IoTサービスのユーザーアカウントのアクセストークン。CEKは、外部サービスの認可サーバーから取得したユーザーアカウントのアクセストークンを渡します。詳細については、[ユーザーアカウントをリンクする](/CEK/Guides/Link_User_Account.md)を参照してください。                          | 常時    |
| `appliance`        | [ApplianceInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#ApplianceInfoObject)     | エンドポイントの情報を持つオブジェクト。`applianceId`フィールドは必須です。     | 常時    |

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

### 次の項目も参照してください。
* [`StopConfirmation`](#StopConfirmation)

## TurnOffConfirmation {#TurnOffConfirmation}
[`TurnOffRequest`](#TurnOffRequest)メッセージに対するレスポンスです。デバイスの電源をオフにするように設定した結果をCEKに返します。

### Payload fields
なし

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

### 次の項目も参照してください。
* [`TurnOffRequest`](#TurnOffRequest)

## TurnOffRequest {#TurnOffRequest}
デバイスの電源をオフにするようClova Home Extensionにリクエストします。このリクエストに対するレスポンスとして、[`TurnOffConfirmation`](#TurnOffConfirmation)メッセージを使用する必要があります。

### Payload fields

| フィールド名       | データ型    | フィールドの説明                     | 任意 |
|---------------|---------|-----------------------------|:---------:|
| `accessToken`      | string                                  | IoTサービスのユーザーアカウントのアクセストークン。CEKは、外部サービスの認可サーバーから取得したユーザーアカウントのアクセストークンを渡します。詳細については、[ユーザーアカウントをリンクする](/CEK/Guides/Link_User_Account.md)を参照してください。                          | 常時    |
| `appliance`        | [ApplianceInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#ApplianceInfoObject)     | エンドポイントの情報を持つオブジェクト。`applianceId`フィールドは必須です。 | 常時    |

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

### 次の項目も参照してください。
* [`TurnOffConfirmation`](#TurnOffConfirmation)

## TurnOnConfirmation {#TurnOnConfirmation}
[`TurnOnRequest`](#TurnOnRequest)メッセージに対するレスポンスです。デバイスの電源をオンにするように設定した結果をCEKに返します。

### Payload fields
なし

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

### 次の項目も参照してください。
* [`TurnOnRequest`](#TurnOnRequest)

## TurnOnRequest {#TurnOnRequest}
デバイスの電源をオンにするようClova Home Extensionにリクエストします。このリクエストに対するレスポンスとして、[`TurnOnConfirmation`](#TurnOnConfirmation)メッセージを使用する必要があります。

### Payload fields

| フィールド名       | データ型    | フィールドの説明                     | 任意 |
|---------------|---------|-----------------------------|:---------:|
| `accessToken`      | string                                  | IoTサービスのユーザーアカウントのアクセストークン。CEKは、外部サービスの認可サーバーから取得したユーザーアカウントのアクセストークンを渡します。詳細については、[ユーザーアカウントをリンクする](/CEK/Guides/Link_User_Account.md)を参照してください。                          | 常時    |
| `appliance`        | [ApplianceInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#ApplianceInfoObject)     | エンドポイントの情報を持つオブジェクト。`applianceId`フィールドは必須です。 | 常時    |

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

### 次の項目も参照してください。
* [`TurnOnConfirmation`](#TurnOnConfirmation)

## UnmuteConfirmation {#UnmuteConfirmation}
[`UnmuteRequest`](#UnmuteRequest)メッセージに対するレスポンスです。デバイスのミュートを解除するように設定した結果をCEKに返します。

### Payload fields
なし

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

### 次の項目も参照してください。
* [`UnmuteRequest`](#UnmuteRequest)

## UnmuteRequest {#UnmuteRequest}
主にテレビやセットトップボックスなどのデバイスを制御する際に使用します。デバイスのミュートを解除するようClova Home Extensionにリクエストします。このリクエストに対するレスポンスとして、[`UnmuteConfirmation`](#UnmuteConfirmation)メッセージを使用する必要があります。

### Payload fields

| フィールド名       | データ型    | フィールドの説明                     | 任意 |
|---------------|---------|-----------------------------|:---------:|
| `accessToken`      | string                                  | IoTサービスのユーザーアカウントのアクセストークン。CEKは、外部サービスの認可サーバーから取得したユーザーアカウントのアクセストークンを渡します。詳細については、[ユーザーアカウントをリンクする](/CEK/Guides/Link_User_Account.md)を参照してください。                          | 常時    |
| `appliance`        | [ApplianceInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#ApplianceInfoObject)     | エンドポイントの情報を持つオブジェクト。`applianceId`フィールドは必須です。 | 常時    |

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

### 次の項目も参照してください。
* [`UnmuteConfirmation`](#UnmuteConfirmation)
