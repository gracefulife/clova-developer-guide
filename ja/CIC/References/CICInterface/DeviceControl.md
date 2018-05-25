# DeviceControl

DeviceControlインターフェースは、クライアントデバイスをコントロールしたり、クライアントデバイスをのコントロールした結果をCICにレポートするときに使用する名前欄です。

ユーザーからのリクエストには、クライアントデバイスをコントロールするためのものがあります。解析されたユーザーのリクエストが、クライアントをコントロールするものなら、`DeviceControl`名前欄を持つディレクティブが送信されます。クライアントは、受信したディレクティブに応じてクライアントデバイスをコントロールする必要があります。また、デバイスをコントロールした結果を、イベントを使用してCICに送信する必要があります。詳細については、[クライアントデバイスコントロールの仕組み](#DeviceContorlWorkFlow)を参照してください。

クライアントデバイスは、`DeviceControl`で提供されるメッセージを使って、外部のBluetoothスピーカーと接続することができます。CICはクライアントにディレクティブを送信して、外部のBluetoothデバイスと接続するように指示します。クライアントは[`Device.DeviceState`](/CIC/References/Context_Objects.md#DeviceState)コンテキストの[`BluetoothInfoObject`](/CIC/References/Context_Objects.md#BluetoothInfoObject)で、ペアリングしたデバイスの情報など、Bluetoothデバイスに関連する情報をCICに随時レポートします。接続方法の詳細については、それぞれのディレクティブとイベントの説明を参照してください。

DeviceControlでは、次のイベントとディレクティブを提供しています。

| メッセージ         | タイプ  | 説明                                   |
|------------------|-----------|---------------------------------------------|
| [`ActionExecuted`](#ActionExecuted)       | イベント     | クライアントは、デバイスを正常にコントロールした場合、このイベントをCICに送信する必要があります。           |
| [`ActionFailed`](#ActionFailed)           | イベント     | クライアントは、デバイスをコントロールできないか、またはコントロールに失敗した場合、このイベントをCICに送信する必要があります。 |
| [`BtConnect`](#BtConnect)                 | ディレクティブ | クライアントに、特定のBluetoothデバイスと接続するように指示します。                               |
| [`BtConnectByPINCode`](#BtConnectByPINCode) | ディレクティブ | クライアントに、PINコードを要求したBluetoothデバイスと接続するように指示します。                        |
| [`BtDisconnect`](#BtDisconnect)           | ディレクティブ | クライアントに、特定のBluetoothデバイスとの接続を解除するように指示します。                               |
| [`BtRequestForPINCode`](#BtRequestForPINCode) | イベント | クライアントは、BluetoothデバイスからPINコードを要求される場合、このイベントでCICにリクエストを送信する必要があります。     |
| [`BtRequestToCancelPinCodeInput`](#BtRequestToCancelPinCodeInput) | イベント | クライアントは、CICに対してPINコード入力の要求をキャンセルする場合、このイベントを送信する必要があります。 |
| [`BtStartPairing`](#BtStartPairing)       | ディレクティブ | クライアントに、Bluetoothペアリングを開始するように指示します。                                       |
| [`BtStopPairing`](#BtStopPairing)         | ディレクティブ | クライアントに、Bluetoothペアリングを解除するように指示します。                                       |
| [`Decrease`](#Decrease)                   | ディレクティブ | クライアントに、スピーカーの音量または画面の明るさを、基本値だけ下げるように指示します。                     |
| [`ExpectReportState`](#ExpectReportState) | ディレクティブ | クライアントに、デバイスの現在の状態をCICにレポートするように指示します。                                 |
| [`Increase`](#Increase)                   | ディレクティブ | クライアントに、スピーカーの音量または画面の明るさを、基本値だけ上げるように指示します。                     |
| [`LaunchApp`](#LaunchApp)                 | ディレクティブ | **(Deprecated)** クライアントに、特定のアプリを起動するように指示します。                           |
| [`Open`](#Open)                           | ディレクティブ | クライアントに、特定の画面を表示するように指示します。                                               |
| [`OpenScreen`](#OpenScreen)               | ディレクティブ | **(Deprecated)** クライアントに、設定画面を開くように指示します。                              |
| [`ReportState`](#ReportState)             | イベント     | クライアントは、デバイスの現在の状態をレポートするとき、このメッセージを使用する必要があります。                     |
| [`RequestStateSynchronization`](#RequestStateSynchronization) | イベント   | ユーザーのアカウントに登録されている他のクライアントデバイスの現在の状態を確認しようとするとき、このイベントをCICに送信します。  |
| [`SetValue`](#SetValue)                   | ディレクティブ | クライアントに、スピーカーの音量または画面の明るさを、指定された値に設定するように指示します。                    |
| [`SynchronizeState`](#SynchronizeState)   | ディレクティブ | クライアントに、ユーザーのアカウントに登録されている他のクライアントデバイスの状態を更新するように指示します。         |
| [`TurnOff`](#TurnOff)                     | ディレクティブ | クライアントに、指定された機能やモードをオフにしたり、または無効にするように指示します。                           |
| [`TurnOn`](#TurnOn)                       | ディレクティブ | クライアントに、指定された機能をオンにしたり、有効にしたりするように指示します。                                   |

## クライアントデバイスコントロールの仕組み {#DeviceContorlWorkFlow}

通常、クライアントデバイスのコントロールは、次のように行われます。

![](/CIC/Resources/Images/CIC_DeviceControl_Work_Flow1.png)

1. ユーザーがクライアントデバイスのコントロールを発話でリクエスト([`SpeechRecognizer.Recognize`](/CIC/References/CICInterface/SpeechRecognizer.md#Recognize))します。そのとき、イベントには[`Device.DeviceState`](/CIC/References/Context_Objects.md#DeviceState)コンテキストが含まれる必要があります。
2. CICは、[`Device.DeviceState`](/CIC/References/Context_Objects.md#DeviceState)コンテキストの`actions[]`フィールドを分析して、ユーザーからリクエストされた動作を、該当するクライアントで処理できるか確認します。
3. クライアントがリクエストを処理できる場合、CICは、そのリクエストの内容が含まれたDeviceControl APIのディレクティブをクライアントに送信します。
4. クライアントは、受信したディレクティブを処理して、その結果を[`DeviceControl.ActionExecuted`](#ActionExecuted)または[`DeviceControl.ActionFailed`](#ActionFailed)イベントでCICにレポートします。

また、Clovaアプリがユーザーのアカウントに登録されているクライアントデバイスの状態を確認するために、以下のように状態の情報を要求することもあります。

![](/CIC/Resources/Images/CIC_DeviceControl_Work_Flow2.png)

1. クライアント(主にClovaアプリ)が[`DeviceControl.RequestStateSynchronization`](#RequestStateSynchronization)イベントをCICに送信します。
2. CICは、ユーザーのアカウントに登録されているすべてのクライアント(Clovaアプリを除く)に[`DeviceControl.ExpectReportState`](#ExpectReportState)ディレクティブを、[ダウンチャネル](/CIC/Guides/Interact_with_CIC.md#CreateConnection)で送信します。
3. [`DeviceControl.ExpectReportState`](#ExpectReportState)ディレクティブを受信したクライアントは、[`DeviceControl.ReportState`](#ReportState)イベントをCICに送信して、現在の状態をレポートする必要があります。
4. CICは、収集されたクライアントの状態を、[`DeviceControl.SynchronizeState`](#SynchronizeState)ディレクティブを使って[ダウンチャネル](/CIC/Guides/Interact_with_CIC.md#CreateConnection)でClovaアプリに送信します。
5. [`DeviceControl.SynchronizeState`](#SynchronizeState)ディレクティブを受信すると、Clovaアプリは他のクライアントデバイスの状態を更新します。

<div class="note">
  <p><strong>メモ</strong></p>
  <p>クライアントは、ユーザーのアカウントに新規に追加されたり、CICに再接続されたりすると、<a href="#ExpectReportState"><code>DeviceControl.ExpectReportState</code></a>ディレクティブを受信します。その際、クライアントはClovaアプリに状態を共有するときと同じ動作をする必要があります。</p>
</div>

## ActionExecutedイベント {#ActionExecuted}

クライアントは、デバイスを正常にコントロールした場合、このイベントをCICに送信する必要があります。

### Context fields

{% include "/CIC/References/CICInterface/Context_Objects_List.md" %}

### Payload fields

| フィールド名       | データ型    | 説明                     | 必須/任意 |
|---------------|---------|-----------------------------|:---------:|
| `target`      | string  | コントロールする対象。<ul><li><code>"airplane"</code>：機内モード</li><li><code>"app"</code>：アプリ</li><li><code>"bluetooth"</code>：Bluetooth</li><li><code>"cellular"</code>：セルラーネットワーク</li><li><code>"channel"</code>：テレビチャンネル</li><li><code>"flashlight"</code>：フラッシュライト</li><li><code>"gps"</code>：GPS</li><li><code>"powersave"</code>：省電力モード</li><li><code>"screenbrightness"</code>：画面の明るさ</li><li><code>"soundmode"</code>：サウンドモード</li><li><code>"volume"</code>：スピーカーの音量</li><li><code>"wifi"</code>：WiFi</li></ul> | 必須     |
| `command`     | string  | 正常に実行されたアクション。<ul><li><code>"BtConnect"</code></li><li><code>"BtConnectByPINCode"</code></li><li><code>"BtDisconnect"</code></li><li><code>"BtStartPairing"</code></li><li><code>"BtStopPairing"</code></li><li><code>"Decrease"</code></li><li><code>"Increase"</code></li><li><code>"Open"</code></li><li><code>"SetValue"</code></li><li><code>"TurnOn"</code></li><li><code>"TurnOff"</code></li></ul> | 必須   |

### 備考

CICは、このイベントを受信すると、ユーザーのアカウントに登録されているすべてのアカウントに[`SynchronizeState`](#SynchronizeState)ディレクティブを送信して、特定のクライアントデバイスの変更された状態を通知します。

### Message example

{% raw %}

```json
{
  "context": [
    {{Alerts.AlertsState}},
    {{AudioPlayer.PlayerState}},
    {{Device.DeviceState}},
    {{Device.Display}},
    {{Clova.Location}},
    {{Clova.SavedPlace}},
    {{Speaker.VolumeState}},
    {{SpeechSynthesizer.SpeechState}}
  ],
  "event": {
    "header": {
      "namespace": "DeviceControl",
      "name": "ActionExecuted",
      "messageId": "23bdfff7-b655-46d4-8655-8bb473bf2bf5"
    },
    "payload": {
      "target": "gps",
      "command": "TurnOn"
    }
  }
}
```

{% endraw %}

### 次の項目も参照してください。
* [`DeviceControl.ActionFailed`](#ActionFailed)
* [`DeviceControl.BtConnect`](#BtConnect)
* [`DeviceControl.BtConnectByPINCode`](#BtConnectByPINCode)
* [`DeviceControl.BtDisconnect`](#BtDisconnect)
* [`DeviceControl.BtStartPairing`](#BtStartPairing)
* [`DeviceControl.BtStopPairing`](#BtStopPairing)

* [`DeviceControl.Decrease`](#Decrease)
* [`DeviceControl.Increase`](#Increase)
* [`DeviceControl.Open`](#Open)
* [`DeviceControl.SetValue`](#SetValue)
* [`DeviceControl.TurnOff`](#TurnOff)
* [`DeviceControl.TurnOn`](#TurnOn)

## ActionFailedイベント {#ActionFailed}

クライアントは、デバイスをコントロールできないか、またはコントロールに失敗した場合、このイベントをCICに送信する必要があります。

### Context fields

{% include "/CIC/References/CICInterface/Context_Objects_List.md" %}

### Payload fields

| フィールド名       | データ型    | 説明                     | 必須/任意 |
|---------------|---------|-----------------------------|:---------:|
| `target`      | string  | コントロールする対象。<ul><li><code>"airplane"</code>：機内モード</li><li><code>"app"</code>：アプリ</li><li><code>"bluetooth"</code>：Bluetooth</li><li><code>"cellular"</code>：セルラーネットワーク</li><li><code>"channel"</code>：テレビチャンネル</li><li><code>"flashlight"</code>：フラッシュライト</li><li><code>"gps"</code>：GPS</li><li><code>"powersave"</code>：省電力モード</li><li><code>"screenbrightness"</code>：画面の明るさ</li><li><code>"soundmode"</code>：サウンドモード</li><li><code>"volume"</code>：スピーカーの音量</li><li><code>"wifi"</code>：WiFi</li></ul> | 必須     |
| `command`     | string  | 失敗したアクション。<ul><li><code>"BtConnect"</code></li><li><code>"BtConnectByPINCode"</code></li><li><code>"BtDisconnect"</code></li><li><code>"BtStartPairing"</code></li><li><code>"BtStopPairing"</code></li><li><code>"Decrease"</code></li><li><code>"Increase"</code></li><li><code>"Open"</code></li><li><code>"SetValue"</code></li><li><code>"TurnOn"</code></li><li><code>"TurnOff"</code></li></ul> | 必須   |

### 備考

* CICは、このイベントを受信すると、ユーザーのアカウントに登録されているすべてのアカウントに[`SynchronizeState`](#SynchronizeState)ディレクティブを送信して、特定のクライアントデバイスの変更された状態を通知します。
* [`LaunchApp`](#LaunchApp)ディレクティブを受信後、アプリを起動できなかった場合、`target`フィールドを`"app"`に設定します。

### Message example

{% raw %}

```json
{
  "context": [
    {{Alerts.AlertsState}},
    {{AudioPlayer.PlayerState}},
    {{Device.DeviceState}},
    {{Device.Display}},
    {{Clova.Location}},
    {{Clova.SavedPlace}},
    {{Speaker.VolumeState}},
    {{SpeechSynthesizer.SpeechState}}
  ],
  "event": {
    "header": {
      "namespace": "DeviceControl",
      "name": "ActionFailed",
      "messageId": "23bdfff7-b655-46d4-8655-8bb473bf2bf5"
    },
    "payload": {
      "target": "gps",
      "command": "TurnOn"
    }
  }
}
```

{% endraw %}

### 次の項目も参照してください。
* [`DeviceControl.ActionExecuted`](#ActionExecuted)
* [`DeviceControl.BtConnect`](#BtConnect)
* [`DeviceControl.BtConnectByPINCode`](#BtConnectByPINCode)
* [`DeviceControl.BtDisconnect`](#BtDisconnect)
* [`DeviceControl.BtStartPairing`](#BtStartPairing)
* [`DeviceControl.BtStopPairing`](#BtStopPairing)
* [`DeviceControl.Decrease`](#Decrease)
* [`DeviceControl.Increase`](#Increase)
* [`DeviceControl.Open`](#Open)
* [`DeviceControl.SetValue`](#SetValue)
* [`DeviceControl.TurnOff`](#TurnOff)
* [`DeviceControl.TurnOn`](#TurnOn)

## BtConnectディレクティブ {#BtConnect}

クライアントに、ペアリングされたBluetoothデバイスのうち1つと接続するように指示します。接続するBluetoothデバイスは、指定されている場合もあり、指定されていない場合もあります。
* 接続するデバイスが指定されていない場合、クライアントはそれぞれの基準によって、ペアリングされたデバイスのうち、どのデバイスと接続するかを決める必要があります。例えば、最近接続した順で接続することができます。
* 接続するデバイスが指定されている場合、クライアントはそのデバイスと接続する必要があります。

### Payload fields

* 接続するデバイスが指定されていない場合

  なし

* 接続するデバイスが指定されている場合

| フィールド名       | データ型    | 説明                     | 常時/条件付き |
|---------------|---------|-----------------------------|:---------:|
| `name`       | string  | 接続するBluetoothデバイスの名前         | 常時     |
| `address`    | string  | 接続するBluetoothデバイスのMACアドレス     | 常時     |
| `connected`  | boolean | 接続するBluetoothデバイスとの接続状態。<ul><li><code>true</code>：接続している</li><li><code>false</code>：接続していない</li></ul>      | 常時     |
| `role`       | string  | 接続するBluetoothデバイスのロール。<ul><li><code>"sink"</code></li><li><code>"source"</code></li></ul> | 常時     |

### 備考

* Bluetoothスピーカーのみサポートされています。
* `payload`なしにこのメッセージを受信すると、クライアントはペアリングされたBluetoothデバイスのうち1つと接続する必要があります。
* クライアントは、このディレクティブを処理して、その結果を[`DeviceControl.ActionExecuted`](#ActionExecuted)または[`DeviceControl.ActionFailed`](#ActionFailed)イベントでCICに送信する必要があります。
* クライアントは、[`DeviceControl.ReportState`](#ReportState)イベントの[`Device.DeviceState`](/CIC/References/Context_Objects.md#DeviceState)コンテキストに、実際の接続結果を含めてCICにレポートする必要があります。

### Message example

{% raw %}

```json
{
  "directive": {
    "header": {
      "namespace": "DeviceControl",
      "name": "BtConnect",
      "messageId": "0f9950d1-c908-4e02-8c38-8e64e840634c",
      "dialogRequestId": "de0a1fd7-2ef1-4040-9469-3a5dd03ef46b"
    },
    "payload": {}
  }
}
```

{% endraw %}

### 次の項目も参照してください。
* [`DeviceControl.ActionExecuted`](#ActionExecuted)
* [`DeviceControl.ActionFailed`](#ActionFailed)
* [`DeviceControl.BtDisconnect`](#BtDisconnect)
* [`DeviceControl.BtStartPairing`](#BtStartPairing)
* [`DeviceControl.BtStopPairing`](#BtStopPairing)
* [`DeviceControl.TurnOff`](#TurnOff)
* [`DeviceControl.TurnOn`](#TurnOn)

## BtConnectByPINCodeディレクティブ {#BtConnectByPINCode}

クライアントに、PINコードを要求したBluetoothデバイスと接続するように指示します。CICは、このメッセージでユーザーから入力されたPINコードを渡します。

### Payload fields

| フィールド名       | データ型    | 説明                     | 常時/条件付き |
|---------------|---------|-----------------------------|:---------:|
| `pinCode`     | string  | BluetoothのPINコード。このフィールドが空の文字列(`""`)の場合、クライアントはペアリングを中止する必要があります。 | 常時     |

### 備考

* PINコードを使用しないBluetoothデバイスとの接続を指示する場合、このディレクティブは送信されません。
* クライアントは、このディレクティブを処理して、その結果を[`DeviceControl.ActionExecuted`](#ActionExecuted)または[`DeviceControl.ActionFailed`](#ActionFailed)イベントでCICに送信する必要があります。
* クライアントは、[`DeviceControl.ReportState`](#ReportState)イベントの[`Device.DeviceState`](/CIC/References/Context_Objects.md#DeviceState)コンテキストに、実際の接続結果を含めてCICにレポートする必要があります。

### Message example

{% raw %}
```json
{
  "directive": {
    "header": {
      "namespace": "DeviceControl",
      "name": "BtConnectByPINCode",
      "messageId": "4e4080d6-c440-498a-bb73-ae86c6312806"
    },
    "payload": {
      "pinCode": "1234"
    }
  }
}
```
{% endraw %}

### 次の項目も参照してください。

* [`DeviceControl.ActionExecuted`](#ActionExecuted)
* [`DeviceControl.ActionFailed`](#ActionFailed)
* [`DeviceControl.BtConnect`](#BtConnect)
* [`DeviceControl.BtRequestForPINCode`](#BtRequestForPINCode)
* [`DeviceControl.ReportState`](/CIC/References/Context_Objects.md#ReportState)

## BtDisconnectディレクティブ {#BtDisconnect}

クライアントに、接続されたBluetoothデバイスとの接続を解除するように指示します。

### Payload fields

なし

### 備考

* Bluetoothスピーカーのみサポートされています。
* クライアントは、コンテキストの[`Device.DeviceState`](/CIC/References/Context_Objects.md#DeviceState)オブジェクトで、Bluetoothデバイスの情報をCICに随時送信する必要があります。
* クライアントは、このディレクティブを処理して、その結果を[`DeviceControl.ActionExecuted`](#ActionExecuted)または[`DeviceControl.ActionFailed`](#ActionFailed)イベントでCICに送信する必要があります。

### Message example

{% raw %}

```json
{
  "directive": {
    "header": {
      "namespace": "DeviceControl",
      "name": "BtDisconnect",
      "messageId": "0f9950d1-c908-4e02-8c38-8e64e840634c",
      "dialogRequestId": "de0a1fd7-2ef1-4040-9469-3a5dd03ef46b"
    },
    "payload": {}
  }
}
```

{% endraw %}

### 次の項目も参照してください。
* [`DeviceControl.ActionExecuted`](#ActionExecuted)
* [`DeviceControl.ActionFailed`](#ActionFailed)
* [`DeviceControl.BtConnect`](#BtConnect)
* [`DeviceControl.BtStartPairing`](#BtStartPairing)
* [`DeviceControl.BtStopPairing`](#BtStopPairing)
* [`DeviceControl.TurnOff`](#TurnOff)
* [`DeviceControl.TurnOn`](#TurnOn)

## BtRequestForPINCodeイベント {#BtRequestForPINCode}

クライアントは、外部のBluetoothデバイスからPINコードを要求されるとき、このイベントをCICに送信します。

### Context fields

{% include "/CIC/References/CICInterface/Context_Objects_List.md" %}

### Payload fields

| フィールド名       | データ型    | 説明                     | 必須/任意 |
|---------------|---------|-----------------------------|:---------:|
| `deviceName`  | string  | 接続するBluetoothデバイスの名前。PINコード入力画面に表示されます。 | 必須     |

### 備考

* 接続するBluetoothデバイスからPINコードを要求される場合にのみ、このメッセージを送信する必要があります。通常、PINコードは、最初に接続するときに要求されます。
* CICはこのイベントを受信すると、[`DeviceControl.BtConnectByPINCode`](#BtConnectByPINCode)ディレクティブでクライアントにPINコードを送信します。

### Message example

{% raw %}
```json
{
  "context": [
    {{Alerts.AlertsState}},
    {{AudioPlayer.PlayerState}},
    {{Device.DeviceState}},
    {{Device.Display}},
    {{Clova.Location}},
    {{Clova.SavedPlace}},
    {{Speaker.VolumeState}},
    {{SpeechSynthesizer.SpeechState}}
  ],
  "event": {
    "header": {
      "namespace": "DeviceControl",
      "name": "BtRequestForPINCode",
      "messageId": "4e4080d6-c440-498a-bb73-ae86c6312806",
    },
    "payload": {
      "deviceName": "friends device"
    }
  }
}
```
{% endraw %}

### 次の項目も参照してください。

* [`DeviceControl.BtConnect`](#BtConnect)
* [`DeviceControl.BtConnectByPINCode`](#BtConnectByPINCode)
* [`DeviceControl.BtRequestToCancelPinCodeInput`](#BtRequestToCancelPinCodeInput)

## BtRequestToCancelPinCodeInputイベント {#BtRequestToCancelPinCodeInput}

クライアントは、CICに対してPINコード入力の要求をキャンセルする場合、このイベントを送信する必要があります。

### Context fields

{% include "/CIC/References/CICInterface/Context_Objects_List.md" %}

### Payload fields

なし

### 備考

* 特定の時間内にPINコードが入力されなかったり、Bluetooth接続が切れるなどの特殊な状況で、PINコード入力の要求をキャンセルすることがあります。

### Message example

{% raw %}
```json
{
  "context": [
    {{Alerts.AlertsState}},
    {{AudioPlayer.PlayerState}},
    {{Device.DeviceState}},
    {{Device.Display}},
    {{Clova.Location}},
    {{Clova.SavedPlace}},
    {{Speaker.VolumeState}},
    {{SpeechSynthesizer.SpeechState}}
  ],
  "event": {
    "header": {
      "namespace": "DeviceControl",
      "name": "BtRequestToCancelPinCodeInput",
      "messageId": "4e4080d6-c440-498a-bb73-ae86c6312806",
    },
    "payload": {}
  }
}
```
{% endraw %}

### 次の項目も参照してください。

* [`DeviceControl.BtRequestForPINCode`](#BtRequestForPINCode)

## BtStartPairingディレクティブ {#BtStartPairing}

クライアントに、Bluetoothペアリングを開始するように指示します。

### Payload fields

なし

### 備考

* Bluetoothスピーカーのみサポートされています。
* クライアントは、コンテキストの[`Device.DeviceState`](/CIC/References/Context_Objects.md#DeviceState)オブジェクトで、Bluetoothデバイスの情報をCICに随時送信する必要があります。
* クライアントは、このディレクティブを処理して、その結果を[`DeviceControl.ActionExecuted`](#ActionExecuted)または[`DeviceControl.ActionFailed`](#ActionFailed)イベントでCICに送信する必要があります。

### Message example

{% raw %}

```json
{
  "directive": {
    "header": {
      "namespace": "DeviceControl",
      "name": "BtStartPairing",
      "messageId": "0f9950d1-c908-4e02-8c38-8e64e840634c",
      "dialogRequestId": "de0a1fd7-2ef1-4040-9469-3a5dd03ef46b"
    },
    "payload": {}
  }
}
```

{% endraw %}

### 次の項目も参照してください。
* [`DeviceControl.ActionExecuted`](#ActionExecuted)
* [`DeviceControl.ActionFailed`](#ActionFailed)
* [`DeviceControl.BtConnect`](#BtConnect)
* [`DeviceControl.BtDisconnect`](#BtDisconnect)
* [`DeviceControl.BtStopPairing`](#BtStopPairing)
* [`DeviceControl.TurnOff`](#TurnOff)
* [`DeviceControl.TurnOn`](#TurnOn)

## BtStopPairingディレクティブ {#BtStopPairing}

クライアントに、Bluetoothペアリングを解除するように指示します。

### Payload fields

なし

### 備考

* Bluetoothスピーカーのみサポートされています。
* クライアントは、コンテキストの[`Device.DeviceState`](/CIC/References/Context_Objects.md#DeviceState)オブジェクトで、Bluetoothデバイスの情報をCICに随時送信する必要があります。
* クライアントは、このディレクティブを処理して、その結果を[`DeviceControl.ActionExecuted`](#ActionExecuted)または[`DeviceControl.ActionFailed`](#ActionFailed)イベントでCICに送信する必要があります。

### Message example

{% raw %}

```json
{
  "directive": {
    "header": {
      "namespace": "DeviceControl",
      "name": "BtStopPairing",
      "messageId": "0f9950d1-c908-4e02-8c38-8e64e840634c",
      "dialogRequestId": "de0a1fd7-2ef1-4040-9469-3a5dd03ef46b"
    },
    "payload": {}
  }
}
```

{% endraw %}

### 次の項目も参照してください。
* [`DeviceControl.ActionExecuted`](#ActionExecuted)
* [`DeviceControl.ActionFailed`](#ActionFailed)
* [`DeviceControl.BtConnect`](#BtConnect)
* [`DeviceControl.BtDisconnect`](#BtDisconnect)
* [`DeviceControl.BtStartPairing`](#BtStopPairing)
* [`DeviceControl.TurnOff`](#TurnOff)
* [`DeviceControl.TurnOn`](#TurnOn)

## Decreaseディレクティブ {#Decrease}

クライアントに、スピーカーの音量または画面の明るさを基本値だけ下げたり、テレビのチャンネルを前のチャンネルに変更したりするように指示します。

### Payload fields

| フィールド名       | データ型    | 説明                     | 常時/条件付き |
|---------------|---------|-----------------------------|:---------:|
| `target`      | string  | コントロールする対象。<ul><li><code>"channel"</code>：テレビのチャンネル</li><li><code>"screenbrightness"</code>：画面の明るさ</li><li><code>"volume"</code>：スピーカーの音量</li></ul> | 常時     |

### 備考

* 基本値は、クライアント側で直接設定します。
* クライアントは、コンテキストの[`Device.DeviceState`](/CIC/References/Context_Objects.md#DeviceState)オブジェクトで、スピーカーの音量と画面の明るさをCICに随時送信する必要があります。
* クライアントは、このディレクティブを処理して、その結果を[`DeviceControl.ActionExecuted`](#ActionExecuted)または[`DeviceControl.ActionFailed`](#ActionFailed)イベントでCICに送信する必要があります。
* 通常、Clovaからデバイスのコントロールに関するディレクティブをクライアントに送信するとき、ユーザーに通知するためのオーディオファイル([`SpeechSynthesizer.Speak`](/CIC/References/CICInterface/SpeechSynthesizer.md#Speak)ディレクティブ)が添付されます。ただし、`target`フィールドが`"volume"`に設定されているなど、スピーカーの出力に関するコントロールの場合には、[`SpeechSynthesizer.Speak`](/CIC/References/CICInterface/SpeechSynthesizer.md#Speak)ディレクティブにオーディオファイルが添付されません。それは、ユーザーの音楽鑑賞などのUXを向上させるためで、その場合には音声案内の代わりに、クライアントデバイスのライトや、短い効果音などで音量が調節されたことをユーザーに通知する必要があります。

### Message example

{% raw %}

```json
{
  "directive": {
    "header": {
      "namespace": "DeviceControl",
      "name": "Decrease",
      "messageId": "23bdfff7-b655-46d4-8655-8bb473bf2bf5",
      "dialogRequestId": "3c6eef8b-8427-4b46-a367-0a7a46432519"
    },
    "payload": {
      "target": "screenbrightness"
    }
  }
}
```

{% endraw %}

### 次の項目も参照してください。
* [`DeviceControl.ActionExecuted`](#ActionExecuted)
* [`DeviceControl.ActionFailed`](#ActionFailed)
* [`DeviceControl.Increase`](#Increase)
* [`DeviceControl.SetValue`](#SetValue)

## ExpectReportStateディレクティブ {#ExpectReportState}

クライアントに、デバイスの現在の状態をCICにレポートするように指示します。このメッセージを受信したクライアントは、すぐに[`DeviceControl.ReportState`](#ReportState)イベントを使用してデバイスの現在の状態をレポートし、後に`durationInSeconds`フィールドに指定された時間の間、`intervalInSeconds`フィールドに指定されたインターバルでデバイスの現在の状態をレポートする必要があります。

### Payload fields

| フィールド名       | データ型    | 説明                     | 常時/条件付き |
|---------------|---------|-----------------------------|:---------:|
| `durationInSeconds` | number  | レポートする期間。指定された時間の間、デバイスの現在の状態をレポートします。秒単位です。このフィールドがない場合、最初1回のみレポートします。 | 条件付き     |
| `intervalInSeconds` | number  | レポートするインターバル。指定されたインターバルごとに、デバイスの現在の状態をレポートします。秒単位です。このフィールドは`durationInSeconds`フィールドがある場合にのみ有効で、そのフィールドがない場合には省略されます。 | 条件付き     |

### 備考

* `DeviceControl.ExpectReportState`ディレクティブは、他のクライアントから同期のために[`DeviceControl.RequestStateSynchronization`](#RequestStateSynchronization)イベントをCICに送信したときに受信されます。
* このディレクティブはイベントに対する応答ではなく、[ダウンチャネル](/CIC/Guides/Interact_with_CIC.md#CreateConnection)で送信されます。

### Message example

{% raw %}

```json
{
  "directive": {
    "header": {
      "namespace": "DeviceControl",
      "name": "ExpectReportState",
      "messageId": "23bdfff7-b655-46d4-8655-8bb473bf2bf5",
      "dialogRequestId": "3c6eef8b-8427-4b46-a367-0a7a46432519"
    },
    "payload": {
      "durationInSeconds": 600,
      "intervalInSeconds": 60
    }
  }
}
```

{% endraw %}

### 次の項目も参照してください。
* [`DeviceControl.ReportState`](#ReportState)
* [`DeviceControl.RequestStateSynchronization`](#RequestStateSynchronization)

## Increaseディレクティブ {#Increase}

クライアントに、スピーカーの音量または画面の明るさを、基本値だけ上げたり、テレビのチャンネルを次のチャンネルに変更したりするように指示します。

### Payload fields

| フィールド名       | データ型    | 説明                     | 常時/条件付き |
|---------------|---------|-----------------------------|:---------:|
| `target`      | string  | コントロールする対象。<ul><li><code>"channel"</code>：テレビのチャンネル</li><li><code>"screenbrightness"</code>：画面の明るさ</li><li><code>"volume"</code>：スピーカーの音量</li></ul> | 常時     |

### 備考

* 基本値は、クライアント側で直接設定します。
* クライアントは、コンテキストの[`Device.DeviceState`](/CIC/References/Context_Objects.md#DeviceState)オブジェクトで、スピーカーの音量と画面の明るさをCICに随時送信する必要があります。
* クライアントは、このディレクティブを処理して、その結果を[`DeviceControl.ActionExecuted`](#ActionExecuted)または[`DeviceControl.ActionFailed`](#ActionFailed)イベントでCICに送信する必要があります。
* 通常、Clovaからデバイスのコントロールに関するディレクティブをクライアントに送信するとき、ユーザーに通知するためのオーディオファイル([`SpeechSynthesizer.Speak`](/CIC/References/CICInterface/SpeechSynthesizer.md#Speak)ディレクティブ)が添付されます。ただし、`target`フィールドが`"volume"`に設定されているなど、スピーカーの出力に関するコントロールの場合には、[`SpeechSynthesizer.Speak`](/CIC/References/CICInterface/SpeechSynthesizer.md#Speak)ディレクティブにオーディオファイルが添付されません。それは、ユーザーの音楽鑑賞などのUXを向上させるためで、その場合には音声案内の代わりに、クライアントデバイスのライトや、短い効果音などで音量が調節されたことをユーザーに通知する必要があります。

### Message example

{% raw %}

```json
{
  "directive": {
    "header": {
      "namespace": "DeviceControl",
      "name": "Increase",
      "messageId": "23bdfff7-b655-46d4-8655-8bb473bf2bf5",
      "dialogRequestId": "3c6eef8b-8427-4b46-a367-0a7a46432519"
    },
    "payload": {
      "target": "screenbrightness"
    }
  }
}
```

{% endraw %}

### 次の項目も参照してください。
* [`DeviceControl.ActionExecuted`](#ActionExecuted)
* [`DeviceControl.ActionFailed`](#ActionFailed)
* [`DeviceControl.Decrease`](#Decrease)
* [`DeviceControl.SetValue`](#SetValue)

## LaunchAppディレクティブ {#LaunchApp}

クライアントに、特定のアプリを起動するように指示します。アプリを指定する値として、アプリのカスタムURLスキーム、リレーURL、アプリ名のうち1つが含まれます。

### Payload fields

| フィールド名       | データ型    | 説明                     | 常時/条件付き |
|---------------|---------|-----------------------------|:---------:|
| `target`      | string  | 対象となりアプリの情報。次のような情報を持ちます。<ul><li>カスタムURLスキーム：対象アプリのカスタムURLスキーム(例：<code>"{{ book.OrientedServiceWithLowerCase }}searchapp://..."</code>)</li><li>リレーURL：インストールされている対象アプリがある場合、そのアプリを起動するリレーページのURL(例、<code>"http://{{ book.OrientedServiceWithLowerCase }}app.{{ book.OrientedServiceWithLowerCase }}.com/..."</code>)</li><li>アプリ名：ユーザーの発話から認識されたアプリの名前。(例、<code>"{{ book.OrientedService }}アプリ"</code>)</li></ul> | 常時     |

### 備考

* アプリを起動できない場合や、起動に失敗した場合、その結果を[`DeviceControl.ActionFailed`](#ActionFailed)イベントでCICに送信する必要があります。

### Message example

```json
{
  "directive": {
    "header": {
      "namespace": "DeviceControl",
      "name": "LaunchApp",
      "messageId": "23bdfff7-b655-46d4-8655-8bb473bf2bf5",
      "dialogRequestId": "3c6eef8b-8427-4b46-a367-0a7a46432519"
    },
    "payload": {
      "target": "{{ book.OrientedServiceWithLowerCase }}searchapp://..."
    }
  }
}
```

### 次の項目も参照してください。
* [`DeviceControl.ActionFailed`](#ActionFailed)

## Openディレクティブ {#Open}

クライアントに、特定の画面を表示するように指示します。

### Payload fields

| フィールド名       | データ型    | 説明                     | 常時/条件付き |
|---------------|---------|-----------------------------|:---------:|
| `target`      | string  | 表示する画面。現在、以下の値を入力できます。<ul><li><code>"home"</code>：ホーム画面</li><li><code>"settings"</code>：設定画面</li></ul> | 常時   |

### 備考

* クライアントは、このディレクティブを処理して、その結果を[`DeviceControl.ActionExecuted`](#ActionExecuted)または[`DeviceControl.ActionFailed`](#ActionFailed)イベントでCICに送信する必要があります。

### Message example

{% raw %}

```json
{
  "directive": {
    "header": {
      "namespace": "DeviceControl",
      "name": "Open",
      "messageId": "23bdfff7-b655-46d4-8655-8bb473bf2bf5",
      "dialogRequestId": "15ecb9a6-e727-4d58-8ba1-42cc8b63d5c0"
    },
    "payload": {
      "target": "settings"
    }
  }
}
```

{% endraw %}

### 次の項目も参照してください。
* [`DeviceControl.ActionExecuted`](#ActionExecuted)
* [`DeviceControl.ActionFailed`](#ActionFailed)


## OpenScreenディレクティブ {#OpenScreen}

**(Deprecated)** クライアントに、設定画面を開くように指示します。

### Payload fields

| フィールド名       | データ型    | 説明                     | 常時/条件付き |
|---------------|---------|-----------------------------|:---------:|
| `target`      | string  | 表示する画面。現在の設定画面を開く値である`"settings"`のみ入力されます。 | 常時     |

### 備考

クライアントは、このディレクティブを処理して、その結果を[`DeviceControl.ActionExecuted`](#ActionExecuted)または[`DeviceControl.ActionFailed`](#ActionFailed)イベントでCICに送信する必要があります。

### Message example

{% raw %}

```json
{
  "directive": {
    "header": {
      "namespace": "DeviceControl",
      "name": "OpenScreen",
      "messageId": "23bdfff7-b655-46d4-8655-8bb473bf2bf5",
      "dialogRequestId": "3c6eef8b-8427-4b46-a367-0a7a46432519"
    },
    "payload": {
      "target": "settings"
    }
  }
}
```

{% endraw %}

### 次の項目も参照してください。
* [`DeviceControl.ActionExecuted`](#ActionExecuted)
* [`DeviceControl.ActionFailed`](#ActionFailed)

## ReportStateイベント {#ReportState}

クライアントは、デバイスの現在の状態をレポートするとき、このメッセージを使用する必要があります。

### Context fields

{% include "/CIC/References/CICInterface/Context_Objects_List.md" %}

### Payload fields

なし

### 備考

* CICから、[`DeviceControl.ExpectReportState`](#ExpectReportState)ディレクティブを受信した場合、`DeviceControl.ReportState`イベントで現在の状態をレポートする必要があります。
* このイベントでレポートされた状態情報は、[`DeviceControl.SynchronizeState`](#SynchronizeState)ディレクティブでユーザーのアカウントに登録されているすべてのクライアントに送信されます。
* このイベントに対する応答として返されるディレクティブはなく、HTTPレスポンスが`204 No Content`で返されます。

### Message example

{% raw %}

```json
{
  "context": [
    {{Alerts.AlertsState}},
    {{AudioPlayer.PlayerState}},
    {{Device.DeviceState}},
    {{Device.Display}},
    {{Clova.Location}},
    {{Clova.SavedPlace}},
    {{Speaker.VolumeState}},
    {{SpeechSynthesizer.SpeechState}}
  ],
  "event": {
    "header": {
      "namespace": "DeviceControl",
      "name": "ReportState",
      "messageId": "23bdfff7-b655-46d4-8655-8bb473bf2bf5"
    },
    "payload": {}
  }
}
```

{% endraw %}

### 次の項目も参照してください。
* [`DeviceControl.ExpectReportState`](#ExpectReportState)
* [`DeviceControl.SynchronizeState`](#SynchronizeState)

## RequestStateSynchronizationイベント {#RequestStateSynchronization}

ユーザーのアカウントに登録されている他のクライアントデバイスの現在の状態を確認しようとするとき、このイベントをCICに送信します。CICは、このイベントを受信した場合、ユーザーアカウントに登録されているすべてのクライアントに[`DeviceControl.ExpectReportState`](#ExpectReportState)ディレクティブを送信します。

### Context fields

{% include "/CIC/References/CICInterface/Context_Objects_List.md" %}

### Payload fields

なし

### 備考

* このイベントの結果として、後に[ダウンチャネル](/CIC/Guides/Interact_with_CIC.md#CreateConnection)で[`DeviceControl.SynchronizeState`](#SynchronizeState)ディレクティブを受信します。
* このイベントに対する応答として返されるディレクティブはなく、HTTPレスポンスが`204 No Content`で返されます。

### Message example

{% raw %}

```json
{
  "context": [
    {{Alerts.AlertsState}},
    {{AudioPlayer.PlayerState}},
    {{Device.DeviceState}},
    {{Device.Display}},
    {{Clova.Location}},
    {{Clova.SavedPlace}},
    {{Speaker.VolumeState}},
    {{SpeechSynthesizer.SpeechState}}
  ],
  "event": {
    "header": {
      "namespace": "DeviceControl",
      "name": "RequestStateSynchronization",
      "messageId": "23bdfff7-b655-46d4-8655-8bb473bf2bf5"
    },
    "payload": {}
  }
}
```

{% endraw %}

### 次の項目も参照してください。
* [`DeviceControl.ExpectReportState`](#ExpectReportState)
* [`DeviceControl.SynchronizeState`](#SynchronizeState)

## SetValueディレクティブ {#SetValue}

クライアントに、スピーカーの音量または画面の明るさを、指定された値に設定したり、特定のテレビチャンネルに変更したりするように指示します。

### Payload fields

| フィールド名       | データ型    | 説明                     | 常時/条件付き |
|---------------|---------|-----------------------------|:---------:|
| `target`      | string  | コントロールする対象。<ul><li><code>"channel"</code>：テレビのチャンネル</li><li><code>"screenbrightness"</code>：画面の明るさ</li><li><code>"volume"</code>：スピーカーの音量</li></ul> | 常時     |
| `value`       | string  | 変更する値、またはテレビのチャンネル番号かチャンネル名        | 常時     |

### 備考

* クライアントは、コンテキストの[`Device.DeviceState`](/CIC/References/Context_Objects.md#DeviceState)オブジェクトで、スピーカーの音量と画面の明るさをCICに随時送信する必要があります。
* クライアントは、このディレクティブを処理して、その結果を[`DeviceControl.ActionExecuted`](#ActionExecuted)または[`DeviceControl.ActionFailed`](#ActionFailed)イベントでCICに送信する必要があります。
* 通常、Clovaからデバイスのコントロールに関するディレクティブをクライアントに送信するとき、ユーザーに通知するためのオーディオファイル([`SpeechSynthesizer.Speak`](/CIC/References/CICInterface/SpeechSynthesizer.md#Speak)ディレクティブ)が添付されます。ただし、`target`フィールドが`"volume"`に設定されているなど、スピーカーの出力に関するコントロールの場合には、[`SpeechSynthesizer.Speak`](/CIC/References/CICInterface/SpeechSynthesizer.md#Speak)ディレクティブにオーディオファイルが添付されません。それは、ユーザーの音楽鑑賞などのUXを向上させるためで、その場合には音声案内の代わりに、クライアントデバイスのライトや、短い効果音などで音量が調節されたことをユーザーに通知する必要があります。

### Message example

{% raw %}

```json
// 音量をコントロールする
{
  "directive": {
    "header": {
      "namespace": "DeviceControl",
      "name": "SetValue",
      "messageId": "23bdfff7-b655-46d4-8655-8bb473bf2bf5",
      "dialogRequestId": "3c6eef8b-8427-4b46-a367-0a7a46432519"
    },
    "payload": {
      "target": "volume",
      "value": "30"
    }
  }
}
```

{% endraw %}

### 次の項目も参照してください。
* [`DeviceControl.ActionExecuted`](#ActionExecuted)
* [`DeviceControl.ActionFailed`](#ActionFailed)
* [`DeviceControl.Decrease`](#Decrease)
* [`DeviceControl.Increase`](#Increase)
* [`DeviceControl.SetValue`](#SetValue)

## SynchronizeStateディレクティブ {#SynchronizeState}

クライアントに、ユーザーのアカウントに登録されている他のクライアントデバイスの状態を更新するように指示します。ユーザーは同じアカウントで、同時に複数のクライアントを使用できます。例えば、クライアントのタイプはアプリの場合もありますし、WaveのようなClova専用スピーカーの場合もあります。アプリタイプのクライアントは、スピーカータイプの他のクライアントをコントロールできます。その際、他のクライアントをコントロールした結果を`DeviceControl.SynchronizeState`で受信し、そのクライアントの変更された状態を更新します。

クライアントは、次のような状況でこのディレクティブを受信します。

* CICは、[`DeviceControl.ActionExecuted`](#ActionExecuted)または[`DeviceControl.ActionFailed`](#ActionFailed)イベントを受信すると、ユーザーのアカウントに登録されているすべてのクライアントに`DeviceControl.SynchronizeState`ディレクティブで特定のクライアントデバイスの変更された状態を送信します。
* CICは、[`DeviceControl.ReportState`](#ReportState)イベントを受信すると、ユーザーのアカウントに登録されているすべてのクライアントに、`DeviceControl.SynchronizeState`ディレクティブで特定のクライアントデバイスの現在の状態を送信します。

### Payload fields

| フィールド名       | データ型    | 説明                     | 常時/条件付き |
|---------------|---------|-----------------------------|:---------:|
| `deviceId`    | string  | 状態が更新されたクライアントデバイスのID。 | 常時     |
| `deviceState` | [Device.DeviceState](/CIC/References/Context_Objects.md#DeviceState)オブジェクト | デバイスの状態更新情報を持つオブジェクト         | 常時     |

### 備考

`DeviceControl.SynchronizeState`ディレクティブは、[ダウンチャネル](/CIC/Guides/Interact_with_CIC.md#CreateConnection)でユーザーのアカウントに登録されているすべてのクライアントにブロードキャストされます。その際、[ダイアログID(`dialogRequestId`)](/CIC/CIC_Overview.md#DialogModel)はありません。

### Message example

{% raw %}

```json
{
  "directive": {
    "header": {
      "namespace": "DeviceControl",
      "name": "SynchronizeState",
      "messageId": "23bdfff7-b655-46d4-8655-8bb473bf2bf5"
    },
    "payload": {
      "deviceId": "90de78d7-0735-43a8-8bdc-acc3c8bc4a80",
      "deviceState": {{Device.DeviceState}}
    }
  }
}
```

{% endraw %}

### 次の項目も参照してください。
* [`DeviceControl.ActionExecuted`](#ActionExecuted)
* [`DeviceControl.ActionFailed`](#ActionFailed)
* [`DeviceControl.ReportState`](#ReportState)

## TurnOffディレクティブ {#TurnOff}

クライアントに、指定された機能やモードをオフにしたり、または無効にするように指示します。例えば、このディレクティブでクライアントデバイスのBluetoothをオフにすることができます。

### Payload fields

| フィールド名       | データ型    | 説明                     | 常時/条件付き |
|---------------|---------|-----------------------------|:---------:|
| `target`      | string  | コントロールする対象。<ul><li><code>"airplane"</code>：機内モード</li><li><code>"bluetooth"</code>：Bluetooth</li><li><code>"cellular"</code>：セルラーネットワーク</li><li><code>"energysave"</code>：省エネモード</li><li><code>"flashlight"</code>：フラッシュライト</li><li><code>"gps"</code>：GPS</li><li><code>"power"</code>：電源の状態</li><li><code>"ring"</code>：着信モード</li><li><code>"silent"</code>：サイレントモード</li><li><code>"vibrate"</code>：バイブモード</li><li><code>"wifi"</code>：WiFi</li></ul> | 常時     |

### 備考

* 一部の対象をオフにしたり無効にするとき、クライアントデバイスのポリシーや状況に合わせてコントロールする必要があります。例えば、着信モードを無効にする場合、マナーモードにするか、それともミュートモードにするかは、クライアントデバイスに応じて実装する必要があります。
* クライアントは、コンテキストの[`Device.DeviceState`](/CIC/References/Context_Objects.md#DeviceState)オブジェクトで、機能やモードの状態を頻繁にCICに送信する必要があります。
* クライアントは、このディレクティブを処理して、その結果を[`DeviceControl.ActionExecuted`](#ActionExecuted)または[`DeviceControl.ActionFailed`](#ActionFailed)イベントでCICに送信する必要があります。

<div class="danger">
  <p><strong>注意</strong></p>
  <p><code>target</code>フィールドの値が<code>"power"</code>の場合、クライアントデバイスの電源をオフにします。</p>
</div>

### Message example

{% raw %}

```json
{
  "directive": {
    "header": {
      "namespace": "DeviceControl",
      "name": "TurnOff",
      "messageId": "23bdfff7-b655-46d4-8655-8bb473bf2bf5",
      "dialogRequestId": "3c6eef8b-8427-4b46-a367-0a7a46432519"
    },
    "payload": {
      "target": "bluetooth"
    }
  }
}
```

{% endraw %}

### 次の項目も参照してください。
* [`DeviceControl.ActionExecuted`](#ActionExecuted)
* [`DeviceControl.ActionFailed`](#ActionFailed)
* [`DeviceControl.TurnOn`](#TurnOn)

## TurnOnディレクティブ {#TurnOn}

クライアントに、指定された機能をオンにしたり、有効にしたりするように指示します。例えば、このディレクティブでクライアントデバイスのBluetoothをオンにすることができます。

### Payload fields

| フィールド名       | データ型    | 説明                     | 常時/条件付き |
|---------------|---------|-----------------------------|:---------:|
| `target`      | string  | コントロールする対象。<ul><li><code>"airplane"</code>：機内モード</li><li><code>"bluetooth"</code>：Bluetooth</li><li><code>"cellular"</code>：セルラーネットワーク</li><li><code>"energysave"</code>：省エネモード</li><li><code>"flashlight"</code>：フラッシュライト</li><li><code>"gps"</code>：GPS</li><li><code>"power"</code>：電源の状態</li><li><code>"ring"</code>：着信モード</li><li><code>"silent"</code>：サイレントモード</li><li><code>"vibrate"</code>：バイブモード</li><li><code>"wifi"</code>：WiFi</li></ul> | 常時     |

### 備考

* クライアントは、コンテキストの[`Device.DeviceState`](/CIC/References/Context_Objects.md#DeviceState)オブジェクトで、機能やモードの状態を頻繁にCICに送信する必要があります。
* クライアントは、このディレクティブを処理して、その結果を[`DeviceControl.ActionExecuted`](#ActionExecuted)または[`DeviceControl.ActionFailed`](#ActionFailed)イベントでCICに送信する必要があります。

### Message example

{% raw %}

```json
{
  "directive": {
    "header": {
      "namespace": "DeviceControl",
      "name": "TurnOff",
      "messageId": "23bdfff7-b655-46d4-8655-8bb473bf2bf5",
      "dialogRequestId": "3c6eef8b-8427-4b46-a367-0a7a46432519"
    },
    "payload": {
      "target": "bluetooth"
    }
  }
}
```

{% endraw %}

### 次の項目も参照してください。
* [`DeviceControl.ActionExecuted`](#ActionExecuted)
* [`DeviceControl.ActionFailed`](#ActionFailed)
* [`DeviceControl.TurnOn`](#TurnOn)
