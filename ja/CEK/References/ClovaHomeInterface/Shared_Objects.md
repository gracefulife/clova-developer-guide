# Shared objects {#SharedObjects}
[Clova Home Extensionメッセージ](/CEK/References/CEK_API.md#ClovaHomeExtMessage)を送信する際、ペイロードには次の共有オブジェクトが含まれます。

| オブジェクト            | 説明                                            |
|--------------------|---------------------------------------------------|
| [ActionInforObject](#ActionInforObject)                   | エンドポイント制御動作の情報を持っています。  |
| [AirQualityInfoObject](#AirQualityInfoObject)             | 空気質の情報を持っています。            |
| [ApplianceInfoObject](#ApplianceInfoObject)               | IoTデバイスの情報を持っています。        |
| [BatteryInfoObject](#BatteryInfoObject)                   | バッテリーの情報を持っています。            |
| [BillInfoObject](#BillInfoObject)                         | 利用料金の情報を持っています。             |
| [BrightnessInfoObject](#BrightnessInfoObject)             | 照明や画面の輝度情報を持っています。 |
| [ColorInfoObject](#ColorInfoObject)                       | エンドポイントの照明や画面、電球の色の情報を持っています。  |
| [ColorTemperatureInfoObject](#ColorTemperatureInfoObject) | エンドポイントの照明や画面、電球の色温度の情報を持っています。  |
| [ConsumptionInfoObject](#ConsumptionInfoObject)           | 電力の使用量情報を持っています。       |
| [CustomCommandInfoObject](#CustomCommandInfoObject)       | カスタムコマンドの情報を持っています。   |
| [CustomInfoObject](#CustomInfoObject)                     | 任意の名前、必要な単位・数値情報を直接入力する際に使用できます。 |   |   |
| [ExpendableInfoObject](#ExpendableInfoObject)             | エンドポイントの消耗品の使用量や残り寿命に関する情報を持っています。  |
| [FineDustInfoObject](#FineDustInfoObject)                 | PM10の情報を持っています。          |
| [IntensityLevelInfoObject](#IntensityLevelInfoObject)     | 圧力や水圧の強度情報を持っています。   |
| [ModeInfoObject](#ModeInfoObject)                         | 運転モードの情報を持っています。          |
| [HumidityInfoObject](#HumidityInfoObject)                 | 湿度情報を持っています。              |
| [PeriodInfoObject](#PeriodInfoObject)                     | 期間情報を持っています。          |
| [PhaseInfoObject](#PhaseInfoObject)                       | エンドポイントの動作の段階情報を持っています。
| [ProgressiveTaxBracketInfoObject](#ProgressiveTaxBracketInfoObject)  | 累進税の段階情報を持っています。       |
| [SittingStateInfoObject](#SittingStateInfoObject)         | スマートチェアなどのエンドポイントに対する、ユーザーの着席情報を持っています。  |
| [SleepScoreInfoObject](#SleepScoreInfoObject)             | 睡眠スコアの情報を持っています。          |
| [SpeedInfoObject](#SpeedInfoObject)                       | 速度情報を持っています。              |
| [TemperatureInfoObject](#TemperatureInfoObject)           | 温度情報を持っています。          |
| [TVChannelNameInfoObject](#TVChannelNameInfoObject)       | テレビのチャンネル名を持っています。      |
| [TVChannelInfoObject](#TVChannelInfoObject)               | テレビチャンネルの情報を持っています。           |
| [UltraFineDustInfoObject](#UltraFineDustInfoObject)       | PM2.5の情報を持っています。         |
| [VolumeInfoObject](#VolumeInfoObject)                     | 音量情報を持っています。          |

## ActionInforObject {#ActionInforObject}
エンドポイント制御動作の情報を持っているオブジェクトです。1つのデバイスに対して、1つの動作を指示するコマンドを表します。

### Object fields
| フィールド名       | データ型    | フィールドの説明                     | 必須/任意 |
|---------------|---------|-----------------------------|:-------------:|
| `applianceId` | string  | エンドポイントのID                      | 必須/常時     |
| `action`      | string  | エンドポイントの制御動作動作のリストについては、[ApplianceInfoObject](#ApplianceInfoObject)の[Actions](#Actions)項目を参照してください。     | 必須/常時     |

### Object Example
{% raw %}

```json
// サンプル：DiscoverAppliancesResponseメッセージで使用されたサンプル
{
  "header": {
    "messageId": "99f9d8ff-9366-4cab-a90c-b4c7eca0abbe",
    "name": "DiscoverAppliancesResponse",
    "namespace": "ClovaHome",
    "payloadVersion": "1.0"
  },
  "payload": {
    "customCommands": [
      {
        "name": "おはよう",
        "actions": [
          {
            "applianceId": "device-001",
            "action": "TurnOn"
          },
          {
            "applianceId": "device-0012",
            "action": "TurnOff"
          },
          {
            "applianceId": "device-0013",
            "action": "TurnOn"
          }
        ]
      },
      {
        "name": "おやすみ",
        "actions": [
          {
            "applianceId": "device-0011",
            "action": "TurnOn"
          },
          {
            "applianceId": "device-0012",
            "action": "TurnOff"
          },
          {
            "applianceId": "device-0013",
            "action": "TurnOn"
          }
        ]
      }
    ],
    "discoveredAppliances": [
      {
        "applianceId": "device-001",
        "manufacturerName": "device-manufacturer-name",
        "modelName": "スマート照明",
        "version": "v1.0",
        "friendlyName": "リビングの照明",
        "friendlyDescription": "スマートフォンで制御できる照明",
        "isReachable": true,
          "actions": [
            "DecrementBrightness",
            "HealthCheck",
            "IncrementBrightness",
            "SetBrightness",
            "TurnOn",
            "TurnOff"
        ],
        "applianceTypes": ["LIGHT"],
        "additionalApplianceDetails": {}
      },
      {
        "applianceId": "device-002",
        "manufacturerName": "device-manufacturer-name",
        "modelName": "スマートコンセント",
        "version": "v1.0",
        "friendlyName": "キッチンのコンセント",
        "friendlyDescription": "節電コンセント",
        "isReachable": true,
        "actions": [
          "HealthCheck",
          "TurnOn",
          "TurnOff"
        ],
        "applianceTypes": ["SMARTPLUG"],
        "additionalApplianceDetails": {},
        "location": "LIVING_ROOM",
        "tags": ["勉強", "ブラウンの部屋", "おでかけの際に電源をオフにするデバイス"]
      }
    ]
  }
}
```

{% endraw %}

### See also
* [CustomCommandInfoObject](#CustomCommandInfoObject)
* [`DiscoverAppliancesResponse`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#DiscoverAppliancesResponse)

## AirQualityInfoObject {#AirQualityInfoObject}
空気質の情報を持っているオブジェクトです。エンドポイントで測定された空気質を示します。文字列で表されます。

### Object fields
| フィールド名       | データ型    | フィールドの説明                     | 必須/任意 |
|---------------|---------|-----------------------------|:-------------:|
| `index`       | string  | 空気質の指数。次のいずれかの値を持ちます。<ul><li><code>"good"</code>：良い</li><li><code>"normal"</code>：普通</li><li><code>"bad"</code>：悪い</li><li><code>"verybad"</code>：非常に悪い</li></ul> | 必須/常時     |

### Object Example
{% raw %}

```json
// サンプル：GetAirQualityResponseメッセージで使用されたサンプル
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
IoTデバイスの情報を持っているオブジェクトです。ユーザーアカウントに登録されているデバイスのリストをCEKに渡したり、特定のエンドポイントをターゲットに指定して、Clova Home Extensionにそのエンドポイントの操作をリクエストする際に使われます。

### Object fields
| フィールド名       | データ型    | フィールドの説明                     | 必須/任意 |
|---------------|---------|-----------------------------|:-------------:|
| `actions[]`                  | string array  | エンドポイントでサポートされている動作のリスト。クライアントは、ユーザーがIoTデバイスを操作する際、エンドポイントでサポートされている動作の範囲内でリクエストするように案内する必要があります。 | 任意/常時    |
| `additionalApplianceDetails` | object        | メーカーまたはIoTサービスが提供する追加情報を持っているフィールド                                 | 任意/条件付き    |
| `applianceId`                | string        | エンドポイントのID                                                                        | 必須/常時    |
| `applianceTypes[]`           | string array  | エンドポイントのタイプ。`applicationType`によって、そのエンドポイントでサポートされている動作を示す`actions`フィールドの値が異なります。IoTサービスでユーザーアカウントに登録されているエンドポイントのタイプを、次のいずれかに指定する必要があります。備考を参考にして、エンドポイントのタイプを入力します。                                                                              | 必須/常時    |
| `friendlyName`               | string        | ユーザーがつけたエンドポイントの名前                                                           | 任意/常時    |
| `friendlyDescription`        | string        | エンドポイントの説明                                                                  | 任意/常時    |
| `isReachable`                | boolean       | 現在、エンドポイントが遠隔操作できる状態にあるかどうかを示します。<ul><li>true：遠隔操作できる</li><li>false：遠隔操作できない</li></ul> | 任意/常時    |
| `manufacturerName`           | string        | デバイスメーカーの名前                                                                  | 任意/常時    |
| `modelName`                  | string        | デバイスのモデル名                                                                   | 任意/常時    |
| `version`                    | string        | メーカーのソフトウェアバージョン                                                            | 任意/常時    |
| `location`                   | string        | エンドポイントが設置されている場所。[Locations](#Locations)項目内のコードを入力します。入力したコードに対応する位置情報のテキストが`tags`フィールドに追加されます。            | 任意/常時    |
| `tags`                       | string array  | ユーザーがデバイスに追加したタグのリスト。ユーザーはClovaアプリまたはIoTサービスで、デバイスの設置場所、使用目的、メーカーなど、さまざまな属性をタグとしてデバイスに追加することができます。同じ属性(タグ)を持つデバイスは、同じグループになります。同じグループ内に、同じ動作がサポートされているデバイスがある場合、同時に制御することができます。  | 任意/常時  |

### Remarks
[`DiscoverAppliancesRequest`](/CEK/References/ClovaHomeInterface/Discovery_Interfaces.md#DiscoverAppliancesRequest)メッセージでユーザーのデバイスリストをリクエストすると、Clova Home Extensionは`additionalApplianceDetails`を除くすべてのフィールドを設定して返す必要があります。その際、 `actions` の値は通常`applianceTypes`によって決定され、`applianceTypes`フィールドの値により次の値を持ちます。

| applianceTypes | 説明         | サポートされる動作                                  |
|----------------|-------------|-------------------------------------------------|
| `"AIRCONDITIONER"`  | 冷暖房機         | DecrementFanSpeed、DecrementTargetTemperature、GetCurrentTemperature、GetTargetTemperature、HealthCheck、IncrementFanSpeed、IncrementTargetTemperature、SetFanSpeed、SetMode、SetTargetTemperature、TurnOff、TurnOn               |
| `"AIRPURIFIER"`     | 空気清浄機        | DecrementFanSpeed、GetAirQuality、GetFineDust、GetUltraFineDust、HealthCheck、IncrementFanSpeed、SetFanSpeed、TurnOff、TurnOn    |
| `"AIRSENSOR"`       | 空気質測定器     | GetAirQuality、GetCurrentTemperature、GetFineDust、GetHumidity、GetUltraFineDust、HealthCheck                                     |
| `"BIDET"`           | 温水洗浄便座            | Close、GetDeviceState、GetExpendableState、HealthCheck、Open、TurnOff、TurnOn                                                         |
| `"BODYWEIGHTSCALE"` | 体重計          | GetDeviceState、HealthCheck                                                                                                             |
| `"CLOTHESCAREMACHINE"` | 衣類管理機    | GetRemainingTime、HealthCheck、TurnOff、TurnOn                                                                                     |
| `"CLOTHESDRYER"`    | 衣類乾燥機       | GetDeviceState、HealthCheck、TurnOff、TurnOn                                                                                           |
| `"CLOTHESWASHER"`   | 洗濯機       | GetPhase、GetRemainingTime、HealthCheck、TurnOff、TurnOn                                                                           |
| `"DEHUMIDIFIER"`    | 除湿器           | GetCurrentTemperature、GetHumidity、HealthCheck、SetFanSpeed、TurnOff、TurnOn                                                    |
| `"DISHWASHER"`      | 食器洗い機       | GetPhase、GetRemainingTime、HealthCheck、TurnOff、TurnOn                                                                           |
| `"ELECTRICKETTLE"`  | 電気ポット       | GetCurrentTemperature、HealthCheck、TurnOff、TurnOn                                                                              |
| `"ELECTRICTOOTHBRUSH"` | 電動歯ブラシ     | GetDeviceState、HealthCheck                                                                                                            |
| `"FAN"`             | 扇風機           | HealthCheck、SetMode、TurnOff、TurnOn                                                                                            |
| `"HEATER"`          | ヒーター            | DecrementTargetTemperature、GetCurrentTemperature、HealthCheck、IncrementTargetTemperature、TurnOff、TurnOn                      |
| `"HUMIDIFIER"`      | 加湿器           | GetCurrentTemperature、GetHumidity、HealthCheck、SetFanSpeed、TurnOff、TurnOn                                                    |
| `"KIMCHIREFRIGERATOR"` | キムチ冷蔵庫    | GetDeviceState、HealthCheck                                                                                                            |
| `"LIGHT"`           | スマート照明   | DecrementBrightness、DecrementVolume HealthCheck、IncrementBrightness、IncrementVolume SetBrightness、TurnOff、TurnOn            |
| `"MASSAGECHAIR"`    | マッサージチェア        | DecrementIntensityLevel、HealthCheck、IncrementIntensityLevel、TurnOff、TurnOn                                                     |
| `"MICROWAVE"`       | 電子レンジ      | GetRemainingTime、HealthCheck、TurnOff、TurnOn                                                                                      |
| `"MOTIONSENSOR"`    | モーションセンサー    | GetDeviceState、HealthCheck                                                                                                             |
| `"OPENCLOSESENSOR"` | 開閉センサー    | GetCloseTime、GetLockState、GetOpenTime、HealthCheck                                                                                   |
| `"OVEN"`            | オーブン            | GetDeviceState、HealthCheck                                                                                                             |
| `"POWERSTRIP"`      | テーブルタップ         | GetConsumption、GetEstimateBill、GetProgressiveTaxBracket、HealthCheck、TurnOff、TurnOn                                                                     |
| `"PURIFIER"`        | 浄水器          | GetDeviceState、GetExpendableState、HealthCheck、SetMode、SetTargetTemperature                                                     |
| `"RANGE"`           | クッキングヒーター・コンロ          | GetDeviceState、HealthCheck                                                                                                             |
| `"RANGEHOOD"`       | レンジフード      | HealthCheck、TurnOff、TurnOn                                                                                                      |
| `"REFRIGERATOR"`    | 冷蔵庫          | GetDeviceState、HealthCheck、SetFreezerTargetTemperature、SetFridgeTargetTemperature、SetMode                                           |
| `"RICECOOKER"`      | 炊飯器        | GetExpendableState、GetKeepWarmTime、GetPhase、GetRemainingTime、HealthCheck、SetMode、Stop、TurnOff、TurnOn                |
| `"ROBOTVACUUM"`     | ロボット掃除機       | Charge、GetBatteryInfo、HealthCheck、TurnOff、TurnOn                                                                             |
| `"SETTOPBOX"`       | セットトップボックス     | DecrementChannel、DecrementVolume、HealthCheck、IncrementChannel、IncrementVolume、Mute、SetChannel、SetChannelByName、TurnOff、TurnOn、Unmute |
| `"SLEEPINGMONITOR"` | 睡眠センサー        | GetAsleepDuration、GetAwakeDuration、GetDeviceState、GetSleepScore、GetSleepStartTime、HealthCheck、TurnOff、TurnOn              |
| `"SMARTBED"`        | スマートベッド      | HealthCheck、Lower、Raise、Stop                                                                                                   |
| `"SMARTCHAIR"`      | スマートチェア      | GetCurrentSittingState、GetRightPostureRatio、GetUsageTime、HealthCheck                                                                                       |
| `"SMARTCURTAIN"`    | スマートカーテン      | Close、HealthCheck、Open、Stop                                                                                                    |
| `"SMARTHUB"`        | スマートハブ      | GetCurrentTemperature、GetHumidity、GetTargetTemperature、HealthCheck、SetMode                                                    |
| `"SMARTMETER"`      | 電力量計      | GetConsumption、GetCurrentBill、GetEstimateBill、GetProgressiveTaxBracket、HealthCheck                                            |
| `"SMARTPLUG"`       | スマートプラグ     | GetProgressiveTaxBracket、HealthCheck、TurnOff、TurnOn                                                                                                     |
| `"SMARTTV"`         | スマートテレビ       | DecrementChannel、DecrementVolume、HealthCheck、IncrementChannel、IncrementVolume、Mute、SetChannel、SetChannelByName、TurnOff、TurnOn、Unmute |
| `"SMARTVALVE"`      | スマートバルブ      | GetLockState、SetLockState                                                                                                        |
| `"SMOKESENSOR"`     | 煙センサー       | GetDeviceState、HealthCheck                                                                                                             |
| `"SWITCH"`          | 家庭内のコンセントの電源を制御するスイッチ | HealthCheck、TurnOff、TurnOn                                                                                       |
| `"THERMOSTAT"`      | 温度調節器   | DecrementTargetTemperature、GetCurrentTemperature、HealthCheck、IncrementTargetTemperature、SetMode、SetTargetTemperature TurnOff、TurnOn       |
| `"VENTILATOR"`      | 換気扇          | GetDeviceState、HealthCheck、TurnOff、TurnOn                                                                                            |
| `"WATERBOILER"`     | 温水器          | HealthCheck、SetMode、TurnOff、TurnOn                                                                                             |

<div class="note">
<p><strong>Note!</strong></p>
<p>エンドポイントデバイスの機能上の制約によって、そのエンドポイントのapplianceTypesでサポートされているactionsのうち、いずれかを選択して使用することもできます。例えば、ユーザーが登録した空気清浄機(<code>AIRPURIFIER</code>タイプ)にファンの回転速度を調節する機能がない場合、そのエンドポイントのタイプでサポートされているactionsのうち、IncrementFanSpeedとDecrementFanSpeedを除いてDiscoverAppliancesResponseメッセージを返す必要があります。ちなみに、ユーザーがエンドポイントでサポートされていない動作(action)をリクエストした場合、CEKはすぐユーザーに有効な範囲外のリクエストであることを伝えます。</p>
</div>

### Actions {#Actions}
actions項目と関連する[インターフェース](/CEK/References/CEK_API.md#ClovaHomeExtInterface)は、以下の表のとおりです。

| actions                    | 関連インターフェース                            |
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
| GetAsleepDuration              | [`GetAsleepDurationRequest`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#GetAsleepDurationRequest), [`GetAsleepDurationResponse`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#GetAsleepDurationResponse) |
| GetAwakeDuration              | [`GetAwakeDurationRequest`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#GetAwakeDurationRequest), [`GetAwakeDurationResponse`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#GetAwakeDurationResponse) |
| GetBatteryInfo              | [`GetBatteryInfoRequest`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#GetBatteryInfoRequest), [`GetBatteryInfoResponse`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#GetBatteryInfoResponse) |
| GetCloseTime                | [`GetCloseTimeRequest`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#GetCloseTimeRequest), [`GetCloseTimeResponse`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#GetCloseTimeResponse)  |
| GetConsumption              | [`GetConsumptionRequest`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#GetConsumptionRequest), [`GetConsumptionResponse`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#GetConsumptionResponse)  |
| GetCurrentBill              | [`GetCurrentBillRequest`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#GetCurrentBillRequest), [`GetCurrentBillResponse`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#GetCurrentBillResponse)  |
| GetCurrtentSittingState     | [`GetCurrtentSittingStateRequest`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#GetCurrtentSittingStateRequest), [`GetCurrtentSittingStateResponse`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#GetCurrtentSittingStateResponse) |
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
| GetSleepScore              | [`GetSleepScoreRequest`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#GetSleepScoreRequest), [`GetSleepScoreResponse`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#GetSleepScoreResponse) |
| GetSleepStartTime          | [`GetSleepStartTimeRequest`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#GetSleepStartTimeRequest), [`GetSleepStartTimeResponse`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#GetSleepStartTimeResponse) |
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
<p><a href="/CEK/References/ClovaHomeInterface/Discovery_Interfaces.html#DiscoverAppliancesResponse"><code>DiscoverAppliancesResponse</code></a>メッセージでユーザーが登録したIoTデバイスのリストをCEKに返す際、各デバイスの位置を`location`フィールドに追加しておくと、そのIoTデバイスの位置が自動的に設定されます。</p>
</div>

### Locations {#Locations}

以下の表は、`location`フィールドでサポートされている位置情報です。ユーザーの発話を分析したり、ユーザーにデバイスを見せる際に使用します。

{% include "/CEK/References/ClovaHomeInterface/Location.md" %}

### Object Example
{% raw %}

```json
//例1：DiscoverAppliancesResponseメッセージで使用されたサンプル
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
        "modelName": "スマート照明",
        "version": "v1.0",
        "friendlyName": "リビングの照明",
        "friendlyDescription": "スマートフォンで制御できる照明",
        "isReachable": true,
          "actions": [
            "HealthCheck",
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
        "modelName": "スマートコンセント",
        "version": "v1.0",
        "friendlyName": "キッチンのコンセント",
        "friendlyDescription": "節電コンセント",
        "isReachable": true,
        "actions": [
          "HealthCheck",
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

//例2：TurnOnRequestメッセージで使用されたサンプル
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
エンドポイントのバッテリー情報を持っているオブジェクトです。バッテリー残量のパーセントを示す整数(0~100)で表されます。

### Object fields
| フィールド名       | データ型    | フィールドの説明                     | 必須/任意 |
|---------------|---------|-----------------------------|:-------------:|
| `value`       | number  | バッテリー残量(%)                 | 必須/常時     |

### Object Example
{% raw %}

```json
//例1：GetBatteryInfoRequestメッセージで使用されたサンプル
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

//例2：GetBatteryInfoResponseメッセージで使用されたサンプル
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
エンドポイントが測定した電力使用量に基づいて計算された料金情報を持っているオブジェクトです。金額と通貨単位が別のフィールドで表されます。

### Object fields
| フィールド名       | データ型    | フィールドの説明                     | 必須/任意 |
|---------------|---------|-----------------------------|:-------------:|
| `currency`    | string  | 通貨単位(<a href="https://en.wikipedia.org/wiki/ISO_4217" target="_blank">ISO 4217</a>)  | 必須/常時 |
| `value`       | number  | 料金の金額                    | 必須/常時   |

### Object Example
{% raw %}

```json
// サンプル：GetCurrentBillResponseメッセージで使用されたサンプル
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
照明や画面の輝度情報を持っているオブジェクトです。変更する照明や画面の明るさ、または変更前後の明るさのパーセントを示す整数(0~100)で表されます。

### Object fields
| フィールド名       | データ型    | フィールドの説明                     | 必須/任意 |
|---------------|---------|-----------------------------|:-------------:|
| `value`       | number  | 輝度(%)                      | 必須/常時     |

### Object Example
{% raw %}

```json
//例1：IncrementBrightnessRequestメッセージで使用されたサンプル
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

//例2：IncrementBrightnessConfirmationメッセージで使用されたサンプル
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
エンドポイントの照明や画面、電球の色の情報を持っているオブジェクトです。変更するエンドポイントの照明や画面、電球の色や変更前後の色を示します。(<a href="https://en.wikipedia.org/wiki/HSL_and_HSV" target="_blank">HSV</a>)値で表されます。

### Object fields
| フィールド名       | データ型    | フィールドの説明                     | 必須/任意 |
|---------------|---------|-----------------------------|:-------------:|
| `brightness`  | number  | 明度(0~100)。                  | エンドポイントの明るさの設定に[BrightnessInfoObject](#BrightnessInfoObject)が使用されている場合、このフィールドは省略できます。  | 任意/条件付き |
| `hue`         | number  | 色相(0~360)                  | 必須/常時 |
| `saturation`  | number  | 彩度(0~100)                  | 必須/常時 |

### Object Example
{% raw %}

```json
// サンプル：SetColorRequestメッセージで使用されたサンプル
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
エンドポイントの照明や画面、電球の色温度情報を持っているオブジェクトです。変更するエンドポイントの照明や画面、電球の色温度、または変更前後の色温度を示します。単位はK(ケルビン)です。

### Object fields
| フィールド名       | データ型    | フィールドの説明                     | 必須/任意 |
|---------------|---------|-----------------------------|:-------------:|
| `value`       | number  | 色温度(K、ケルビン)             | 必須/常時     |

### Object Example
{% raw %}

```json
// サンプル：SetColorTemperatureRequestメッセージで使用されたサンプル
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
エンドポイントが測定したエネルギーの使用量情報を持っているオブジェクトです。エネルギー使用量の数値と単位が別のフィールドで表されます。

### Object fields
| フィールド名       | データ型    | フィールドの説明                     | 必須/任意 |
|---------------|---------|-----------------------------|:-------------:|
| `unit`        | string  | エネルギーの単位(電力の場合、kW)            | 必須/常時  |
| `value`       | number  | エネルギー使用量の数値                    | 必須/常時   |

### Object Example
{% raw %}

```json
// サンプル：GetCurrentBillResponseメッセージで使用されたサンプル
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

## CustomCommandInfoObject {#CustomCommandInfoObject}

カスタムコマンドの情報を持っているオブジェクトです。ユーザーがClovaアプリで登録したカスタムコマンドの情報を持っています。[`DiscoverAppliancesResponse`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#DiscoverAppliancesResponse)メッセージ内のデバイス照会結果に、ユーザーのアカウントに登録されているコマンドが追加されます。このオブジェクトには、カスタムコマンドを呼び出すと処理されるエンドポイント制御動作が含まれます。

### Object fields

| フィールド名       | データ型    | フィールドの説明                     | 必須/任意 |
|---------------|---------|-----------------------------|:-------------:|
| `name`        | string  | カスタムコマンドの名前。             | 必須/常時      |
| `actions[]`   | [ActionInforObject](#ActionInforObject) array | カスタムコマンドで処理するエンドポイント制御動作のリスト  | 必須/常時  |

### Object Example
{% raw %}

```json
// サンプル：DiscoverAppliancesResponseメッセージで使用されたサンプル
{
  "header": {
    "messageId": "99f9d8ff-9366-4cab-a90c-b4c7eca0abbe",
    "name": "DiscoverAppliancesResponse",
    "namespace": "ClovaHome",
    "payloadVersion": "1.0"
  },
  "payload": {
    "customCommands": [
      {
        "name": "おはよう",
        "actions": [
          {
            "applianceId": "device-001",
            "action": "TurnOn"
          },
          {
            "applianceId": "device-0012",
            "action": "TurnOff"
          },
          {
            "applianceId": "device-0013",
            "action": "TurnOn"
          }
        ]
      },
      {
        "name": "おやすみ",
        "actions": [
          {
            "applianceId": "device-0011",
            "action": "TurnOn"
          },
          {
            "applianceId": "device-0012",
            "action": "TurnOff"
          },
          {
            "applianceId": "device-0013",
            "action": "TurnOn"
          }
        ]
      }
    ],
    "discoveredAppliances": [
      {
        "applianceId": "device-001",
        "manufacturerName": "device-manufacturer-name",
        "modelName": "スマート照明",
        "version": "v1.0",
        "friendlyName": "リビングの照明",
        "friendlyDescription": "スマートフォンで制御できる照明",
        "isReachable": true,
          "actions": [
            "DecrementBrightness",
            "HealthCheck",
            "IncrementBrightness",
            "SetBrightness",
            "TurnOn",
            "TurnOff"
        ],
        "applianceTypes": ["LIGHT"],
        "additionalApplianceDetails": {}
      },
      {
        "applianceId": "device-002",
        "manufacturerName": "device-manufacturer-name",
        "modelName": "スマートコンセント",
        "version": "v1.0",
        "friendlyName": "キッチンのコンセント",
        "friendlyDescription": "節電コンセント",
        "isReachable": true,
        "actions": [
          "HealthCheck",
          "TurnOn",
          "TurnOff"
        ],
        "applianceTypes": ["SMARTPLUG"],
        "additionalApplianceDetails": {},
        "location": "LIVING_ROOM",
        "tags": ["勉強", "ブラウンの部屋", "おでかけの際に電源をオフにするデバイス"]
      }
    ]
  }
}
```

{% endraw %}

### See also
* [ActionInforObject](#ActionInforObject)
* [`DiscoverAppliancesResponse`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#DiscoverAppliancesResponse)

## CustomInfoObject {#CustomInfoObject}

任意の名前、必要な単位や数値で情報を直接入力する際に使用されるオブジェクトです。[共有オブジェクト](#SharedObjects)で提供されるオブジェクトで情報を表すことができない場合、このオブジェクトを使用するか、または[`GetDeviceStateResponse`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#GetDeviceStateResponse)メッセージでエンドポイントのすべての情報を提供することができます。

### Object fields
| フィールド名       | データ型    | フィールドの説明                     | 必須/任意 |
|---------------|---------|-----------------------------|:-------------:|
| `name`        | string            | エンドポイントのステータス情報や測定対象を示す任意の名前。ユーザーに応答する際、このフィールドに入力された値が音声で出力されます。 | 必須/常時 |
| `value`       | numberまたはstring | ステータス値または測定値                                                                             | 必須/常時 |
| `unit`        | string            | エンドポイントのステータス値または測定値の単位。`value`フィールドの型がstringの場合には省略され、numberの場合には次の値を持ちます。<ul><li><code>"celcius"</code>：摂氏温度</li><li><code>"percentage"</code>：パーセント</li></ul> | 任意/条件付き |

### Object Example
{% raw %}

```json
// サンプル：GetDeviceStateResponseメッセージで使用されたサンプル
{
  "header": {
    "messageId": "33da6561-0149-4532-a30b-e0de8f75c4cf",
    "name": "GetDeviceStateResponse",
    "namespace": "ClovaHome",
    "payloadVersion": "1.0"
  },
  "payload": {
    "states": [
      {
        "name": "冷凍室の温度",
        "value": -11,
        "unit": "celsius"
      },
      {
        "name": "冷蔵室の温度",
        "value": 2,
        "unit": "celsius"
      },
      {
        "name": "冷蔵室の湿度",
        "value": 10,
        "unit": "percentage"
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
エンドポイントの消耗品の使用量や残り寿命に関する情報を持っているオブジェクトです。エンドポイントの消耗品の使用量や残り寿命を示します。

### Object fields
| フィールド名       | データ型    | フィールドの説明                     | 必須/任意 |
|---------------|---------|-----------------------------|:-------------:|
| `name`          | string  | 消耗品名                  | 必須/常時 |
| `remainingTime` | string   | 消耗品の残り寿命(継続時間、<a href="https://en.wikipedia.org/wiki/ISO_8601#Durations" target="_blank">ISO 8601</a>)    | 任意/条件付き |
| `usage`         | [CustomInfoObject](#CustomInfoObject)          | 消耗品の使用量(回数またはパーセントで表す)      | 任意/条件付き |

### Object Example
{% raw %}

```json
// サンプル：GetExpendableStateResponseメッセージで使用されたサンプル
{
  "header": {
    "messageId": "33da6561-0149-4532-a30b-e0de8f75c4cf",
    "name": "GetExpendableStateResponse",
    "namespace": "ClovaHome",
    "payloadVersion": "1.0"
  },
  "payload": {
    "expendableInfo": [
      {
        "name": "パッキン",
        "remainingTime": "P0001-04-10"
      },
      {
        "name": "フィルター1",
        "usage": {
          "value": 80,
          "unit": "percentage"
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
PM10の情報を持っているオブジェクトです。エンドポイントが測定したPM10の指数やレベルを示す数字で表されます。

### Object fields
| フィールド名       | データ型    | フィールドの説明                     | 必須/任意 |
|---------------|---------|-----------------------------|:-------------:|
| `value`       | number  | PM10指数                  | 任意/条件付き    |
| `index`       | string  | PM10レベル次のいずれかの値を持ちます。<ul><li><code>"good"</code>：良い</li><li><code>"normal"</code>：普通</li><li><code>"bad"</code>：悪い</li><li><code>"verybad"</code>：非常に悪い</li></ul> | 必須/常時     |

### Object Example
{% raw %}

```json
// サンプル：GetFineDustResponseメッセージで使用されたサンプル
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
圧力/水圧の強度情報を持っているオブジェクトです。エンドポイントの持つ圧力/水圧の強度を示します。

### Object fields
| フィールド名       | データ型    | フィールドの説明                     | 必須/任意 |
|---------------|---------|-----------------------------|:-------------:|
| `value`       | number  | 圧力/水圧の強度            | 任意/条件付き    |

### Object Example
{% raw %}

```json
// サンプル：IncrementIntensityLevelConfirmationメッセージで使用されたサンプル
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
運転モード(operation mode)の情報を持っているオブジェクトです。変更する運転モードの名前や、変更前後の運転モードを示します。文字列で表されます。

### Object fields
| フィールド名       | データ型    | フィールドの説明                     | 必須/任意 |
|---------------|---------|-----------------------------|:-------------:|
| `value`       | string  | [運転モード](#OperationModes)(Operation mode)    | 必須/常時     |

### Operation modes {#OperationModes}

<table>
  <thead>
    <tr>
      <th style="width:20%">エンドポイントのタイプ</th><th style="width:80%">運転モードのリストおよび説明</th>
    </tr>
  </thead>
  <tdoby>
    <tr>
      <td><code>"AIRCONDITIONER"</code></td>
      <td>
        <ul>
          <li><code>"cool"</code>：冷房モード。主にエアコンで使用されるモードです。</li>
          <li><code>"dehumidify"</code>：除湿モード。主にエアコンや除湿器のようなエンドポイントで使用されるモードです。</li>
          <li><code>"sleep"</code>：スリープモード。主にスマートハブのようなエンドポイントで使用されるモードです。</li>
        </ul>
      </td>
    </tr>
    <tr>
      <td><code>"FAN"</code></td>
      <td>
        <ul>
          <li><code>"auto"</code>：自動モード</li>
          <li><code>"baby"</code>：ベビーモード</li>
          <li><code>"sleep"</code>：スリープモード</li>
      </td>
    </tr>
    <tr>
      <td><code>"LIGHT"</code></td>
      <td>
        <ul>
          <li><code>"concentration"</code>：集中モード</li>
          <li><code>"reading"</code>：読書モード</li>
          <li><code>"rest"</code>：リラックスモード</li>
          <li><code>"sleep"</code>：スリープモード</li>
          <li><code>"vitality"</code>：生き生きモード</li>
          <li><code>"wakeup"</code>：ウェイクアップモード</li>
        </ul>
      </td>
    </tr>
    <tr>
      <td><code>"PURIFIER"</code></td>
      <td>
        <ul>
          <li><code>"coldwater"</code>：冷水モード</li>
          <li><code>"general"</code>：一般モード</li>
          <li><code>"hotwater"</code>：温水モード</li>
          <li><code>"smartchecking"</code>：スマート点検モード</li>
        </ul>
      </td>
    </tr>
    <tr>
      <td><code>"REFRIGERATOR"</code></td>
      <td>
        <ul>
          <li><code>"filter"</code>：除菌脱臭モード</li>
          <li><code>"freeze"</code>：急速冷凍モード</li>
          <li><code>"powersaving"</code>：節電モード</li>
        </ul>
      </td>
    </tr>
    <tr>
      <td><code>"RICECOOKER"</code></td>
      <td>
        <ul>
          <li><code>"general"</code>：一般モード</li>
          <li><code>"keepwarm"</code>：保温モード</li>
          <li><code>"powersaving"</code>：節電モード</li>
          <li><code>"reheating"</code>：再加熱モード</li>
        </ul>
      </td>
    </tr>
    <tr>
      <td><code>"SMARTHUB"</code></td>
      <td>
        <ul>
          <li><code>"away"</code>：おでかけモード</li>
          <li><code>"hotwater"</code>：温水モード</li>
          <li><code>"indoor"</code>：在宅モード</li>
          <li><code>"sleep"</code>：スリープモード</li>
        </ul>
      </td>
    </tr>
    <tr>
      <td><code>"THERMOSTAT"</code></td>
      <td>
        <ul>
          <li><code>"away"</code>：おでかけモード</li>
          <li><code>"hotwater"</code>：温水モード</li>
          <li><code>"indoor"</code>：在宅モード</li>
          <li><code>"sleep"</code>：スリープモード</li>
        </ul>
      </td>
    </tr>
    <tr>
      <td><code>"WATERBOILER"</code></td>
      <td>
        <ul>
          <li><code>"hotwater"</code>：給湯モード</li>
          <li><code>"reheating"</code>：再加熱モード</li>
        </ul>
      </td>
    </tr>
  </tdoby>
</table>

### Object Example
{% raw %}

```json
//例1：SetModeRequestメッセージで使用されたサンプル-サーモスタット
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

//例2：SetModeRequestメッセージで使用されたサンプル-スマートハブ
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

//例3：SetModeConfirmationメッセージで使用されたサンプル
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
湿度情報を持っているオブジェクトです。エンドポイントで測定された湿度を示します。文字列で表されます。

### Object fields
| フィールド名       | データ型    | フィールドの説明                     | 必須/任意 |
|---------------|---------|-----------------------------|:-------------:|
| `value`       | number  | 湿度(%)                      | 必須/常時     |

### Object Example
{% raw %}

```json
// サンプル：GetHumidityResponseメッセージで使用されたサンプル
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

使用量や推定料金などの測定データを照会する際に、その照会期間の情報を持っているオブジェクトです。

### Object fields

| フィールド名       | データ型    | フィールドの説明                     | 必須/任意 |
|---------------|---------|-----------------------------|:-------------:|
| `end`         | string  | 期間の終了日時(タイムスタンプ、<a href="https://en.wikipedia.org/wiki/ISO_8601" target="_blank">ISO 8601</a>)    | 必須/常時      |
| `start`       | string  | 期間の開始日時(タイムスタンプ、<a href="https://en.wikipedia.org/wiki/ISO_8601" target="_blank">ISO 8601</a>)    | 必須/常時      |

### Object Example
{% raw %}

```json
// サンプル：GetUsageTimeRequestメッセージで使用されたサンプル
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
      "start": "2018-03-28T00:10:00+09:00",
      "end": "2018-03-28T23:59:59+09:00"
    }
  }
}
```

{% endraw %}

### See also
* [`GetUsageTimeRequest`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#GetUsageTimeRequest)

## PhaseInfoObject {#PhaseInfoObject}

エンドポイントの動作の段階情報を持っているオブジェクトです。現在の動作の段階、または以前の動作の段階を示します。

### Object fields

| フィールド名       | データ型    | フィールドの説明                     | 必須/任意 |
|---------------|---------|-----------------------------|:-------------:|
| `value`       | string  | 動作の段階を表す文字列        | 必須/常時      |

### Object Example
{% raw %}

```json
//例1：GetPhaseResponseメッセージで使用されたサンプル
{
  "header": {
    "messageId": "b502dd42-b698-4d3b-9ddb-bbdda70f254f",
    "name": "GetPhaseResponse",
    "namespace": "ClovaHome",
    "payloadVersion": "1.0"
  },
  "payload": {
    "phase": {
        "value": "脱水",
    },
    "applianceResponseTimestamp": "2017-11-23T20:30:19+09:00"
  }
}

//例2：StopConfirmationメッセージで使用されたサンプル
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

### See also
* [`GetPhaseRequest`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#GetPhaseRequest)
* [`GetPhaseResponse`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#GetPhaseResponse)
* [`StopConfirmation`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#StopConfirmation)
* [`StopRequest`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#StopRequest)

## ProgressiveTaxBracketInfoObject {#ProgressiveTaxBracketInfoObject}
累進税の段階情報を持っているオブジェクトです。

### Object fields
| フィールド名       | データ型    | フィールドの説明                     | 必須/任意 |
|---------------|---------|-----------------------------|:-------------:|
| `value`       | number  | 累進税の段階                    | 必須/常時     |

### Object Example
{% raw %}

```json
//例1：GetProgressiveTaxBracketResponseメッセージで使用されたサンプル
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

## SittingStateInfoObject {#SittingStateInfoObject}
スマートチェアなどのデバイスに対する、ユーザーの着席情報を持っているオブジェクトです。

### Object fields
| フィールド名       | データ型    | フィールドの説明                     | 必須/任意 |
|---------------|---------|-----------------------------|:-------------:|
| `value`       | boolean | 着席状態<ul><li><code>true</code>：着席中</li><li><code>false</code>：着席中ではない</li></ul>       | 必須/常時     |

### Object Example
{% raw %}

```json
// サンプル：GetCurrentSittingStateResponseメッセージで使用されたサンプル
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
* [`GetCurrentSittingStateRequest`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#GetCurrentSittingStateRequest)
* [`GetCurrentSittingStateResponse`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#GetCurrentSittingStateResponse)

## SleepScoreInfoObject {#SleepScoreInfoObject}
睡眠スコアの情報を持っているオブジェクトです。期間に対する結果の場合、平均値です。

### Object fields
| フィールド名       | データ型    | フィールドの説明                     | 必須/任意 |
|---------------|---------|-----------------------------|:-------------:|
| `value`       | number  | 睡眠スコア                     | 必須/常時     |

### Object Example
{% raw %}

```json
// サンプル：GetSleepScoreResponseメッセージで使用されたサンプル
{
  "header": {
    "messageId": "33da6561-0149-4532-a30b-e0de8f75c4cf",
    "name": "GetSleepScoreResponse",
    "namespace": "ClovaHome",
    "payloadVersion": "1.0"
  },
  "payload": {
    "sleepScore": {
      "value": 80,
    },
    "applianceResponseTimestamp": "2018-03-29T14:32:13+09:00"
  }
}
```

{% endraw %}

### See also
* [`GetSleepScoreRequest`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#GetSleepScoreRequest)
* [`GetSleepScoreResponse`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#GetSleepScoreResponse)

## SpeedInfoObject {#SpeedInfoObject}
速度情報を持っているオブジェクトです。変更する速度や、変更前後の設定速度を示します。整水で表されます。

### Object fields
| フィールド名       | データ型    | フィールドの説明                     | 必須/任意 |
|---------------|---------|-----------------------------|:-------------:|
| `value`       | number  | 速度の値                       | 必須/常時     |

### Object Example
{% raw %}

```json
//例1：IncrementFanSpeedRequestメッセージで使用されたサンプル
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

//例2：IncrementFanSpeedConfirmationメッセージで使用されたサンプル
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

## TemperatureInfoObject {#TemperatureInfoObject}
温度情報を持っているオブジェクトです。変更する温度の度合、変更前後の設定温度や現在の設定温度を示します。小数第1位までの数字で表されます。

### Object fields
| フィールド名       | データ型    | フィールドの説明                     | 必須/任意 |
|---------------|---------|-----------------------------|:-------------:|
| `value`       | number  | 温度の値                       | 必須/常時     |

### Object Example
{% raw %}

```json
//例1：IncrementTargetTemperatureRequestメッセージで使用されたサンプル
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

//例2：IncrementTargetTemperatureConfirmationメッセージで使用されたサンプル
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
* [`GetCurrentTemperatureRequest`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#GetCurrentTemperatureRequest)
* [`GetCurrentTemperatureResponse`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#GetCurrentTemperatureResponse)
* [`GetTargetTemperatureRequest`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#GetTargetTemperatureRequest)
* [`GetTargetTemperatureResponse`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#GetTargetTemperatureResponse)
* [`IncrementTargetTemperatureConfirmation`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#IncrementTargetTemperatureConfirmation)
* [`IncrementTargetTemperatureRequest`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#IncrementTargetTemperatureRequest)
* [`SetFreezerTargetTemperatureConfirmation`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#SetFreezerTargetTemperatureConfirmation)
* [`SetFreezerTargetTemperatureRequest`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#SetFreezerTargetTemperatureRequest)
* [`SetFridgeTargetTemperatureConfirmation`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#SetFridgeTargetTemperatureConfirmation)
* [`SetFridgeTargetTemperatureRequest`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#SetFridgeTargetTemperatureRequest)
* [`SetTargetTemperatureConfirmation`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#SetTargetTemperatureConfirmation)
* [`SetTargetTemperatureRequest`](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#SetTargetTemperatureRequest)

## TVChannelNameInfoObject {#TVChannelNameInfoObject}
テレビのチャンネル名の情報を持っているオブジェクトです。変更するチャンネルや変更前後のチャンネル名を示します。文字列で表されます。

### Object fields
| フィールド名       | データ型    | フィールドの説明                     | 必須/任意 |
|---------------|---------|-----------------------------|:-------------:|
| `value`       | string  | テレビのチャンネル名                  | 必須/常時     |

### Object Example
{% raw %}

```json
//例1：SetChannelByNameRequestメッセージで使用されたサンプル
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

//例2：SetChannelByNameConfirmationメッセージで使用されたサンプル
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
テレビのチャンネル番号情報を持っているオブジェクトです。変更するチャンネルや変更前後のチャンネル番号を示します。数字で表されます。

### Object fields
| フィールド名       | データ型    | フィールドの説明                     | 必須/任意 |
|---------------|---------|-----------------------------|:-------------:|
| `value`       | number  | テレビのチャンネル番号                  | 必須/常時     |

### Object Example
{% raw %}

```json
//例1：SetChannelRequestメッセージで使用されたサンプル
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

//例2：SetChannelConfirmationメッセージで使用されたサンプル
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

## UltraFineDustInfoObject {#UltraFineDustInfoObject}
PM2.5の情報を持っているオブジェクトです。エンドポイントで測定されたPM2.5の指数を示します。数字で表されます。

### Object fields
| フィールド名       | データ型    | フィールドの説明                     | 必須/任意 |
|---------------|---------|-----------------------------|:-------------:|
| `value`       | number  | PM2.5指数                | 任意/条件付き    |
| `index`       | number  | PM2.5レベル次のいずれかの値を持ちます。<ul><li><code>"good"</code>：良い</li><li><code>"normal"</code>：普通</li><li><code>"bad"</code>：悪い</li><li><code>"verybad"</code>：非常に悪い</li></ul> | 必須/常時     |

### Object Example
{% raw %}

```json
// サンプル：GetUltraFineDustResponseメッセージで使用されたサンプル
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

## VolumeInfoObject {#VolumeInfoObject}
スピーカーの音量情報を持っているオブジェクトです。調整する音量や調整前後の音量を示します。整水で表されます。

### Object fields
| フィールド名       | データ型    | フィールドの説明                     | 必須/任意 |
|---------------|---------|-----------------------------|:-------------:|
| `value`       | number  | 音量の値                       | 必須/常時     |

### Object Example
{% raw %}

```json
//例1：IncrementVolumeRequestメッセージで使用されたサンプル
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

//例2：IncrementVolumeConfirmationメッセージで使用されたサンプル
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
