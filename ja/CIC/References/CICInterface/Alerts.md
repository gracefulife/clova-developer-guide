# Alerts

Alertsインターフェースは、クライアントでアラームを設定・編集・削除・開始・停止するための名前欄です。次の表は、アラームの種類を示しています。

| アラーム | 説明                                |
|---------|------------------------------------|
| アクションタイマー(`"ACTIONTIMER"`) | 指定された時間が過ぎると、特定の動作を実行します。                               |
| アラーム(`"ALARM"`)            | 指定された日付と時刻にアラームを鳴らします。                                            |
| リマインダー(`"REMINDER"`)      | 指定された日付と時刻に、ユーザーが入力した内容を表示するか、音声で再生してアラームを鳴らします。例えば、ユーザーが「明日7時に薬を飲むとリマインドして」と指示したとします。「明日7時」はアラームの時間で、「薬を飲む」はアラームを鳴らすときに通知する内容になります。クライアントは、アラームを実行する際、ユーザーにリマインドする内容を画面に表示したり、音声で再生する必要があります。       |
| タイマー(`"TIMER"`)           | 指定された時間が過ぎると、アラームを鳴らします。                                         |

ユーザーは、アラームを音声またはClovaアプリで追加できます。アラームの編集および削除は、Clovaアプリでのみ可能です。Clovaは、アラームに関連する情報をクラウドに保存し、ユーザーが設定したアラームをCICを介してクライアントに送信します。Clovaは、スヌーズアラームの場合、現在の時刻にもっとも近いアラームのみをクライアントに送信します。また、そのアラームが停止すると、次のスヌーズアラームをクライアントに送信します。

クライアントは、Alertsインターフェースを使用して、次の動作を実行する必要があります。
* CICからディレクティブを受信すると、ディレクティブの内容に応じてアラームを設定・編集・削除します。
* 指定された時刻にアラームを実行します。
* アラームを設定・編集・削除・開始・停止した場合、必ずCICにレポートします。そうすることで、CICはレポートを受け、適切な結果をクライアントに返すことができます。
* イベントを送信する際、必ず[`Alerts.AlertsState`](/CIC/References/Context_Objects.md#AlertsState)コンテキストオブジェクトを含めて、クライアントに設定されているアラームの状態をレポートする必要があります。

<div class="note">
  <p><strong>Note!</strong></p>
  <p>アラームが設定・編集・削除・開始・停止する仕組みについては、<a href="#AlertsWorkFlow">アラームの仕組み</a>を参照してください。</p>
</div>

Alertsが提供するイベントとディレクティブは、次の通りです。

| メッセージ         | タイプ  | 説明                                   |
|------------------|-----------|---------------------------------------------|
| [`AlertStarted`](#AlertStarted)                 | イベント     | クライアントから、アラームが開始したことをCICにレポートします。 |
| [`AlertStopped`](#AlertStopped)                 | イベント     | クライアントから、アラームが停止したことをCICにレポートします。 |
| [`DeleteAlert`](#DeleteAlert)                   | ディレクティブ | クライアントに対して、特定のアラームを削除するように指示します。 |
| [`DeleteAlertFailed`](#DeleteAlertFailed)       | イベント     | クライアントから、クライアントに設定されている特定のアラームを削除できなかったことをCICにレポートします。 |
| [`DeleteAlertSucceeded`](#DeleteAlertSucceeded) | イベント     | クライアントから、クライアントに設定されている特定のアラームを正常に削除したことをCICにレポートします。 |
| [`RequestAlertStop`](#RequestAlertStop)         | イベント     | クライアントから、アクティブなアラームを停止するようにCICにリクエストします。  |
| [`RequestSynchronizeAlert`](#RequestSynchronizeAlert) | イベント | クライアントから、Clovaのクラウドに保存されたユーザーのアラームデータを同期する必要がある場合、CICにこのイベントを送信します。 |
| [`SetAlert`](#SetAlert)                         | ディレクティブ | クライアントに対して、アラームを追加するか、または特定のアラームを編集するように指示します。 |
| [`SetAlertFailed`](#SetAlertFailed)             | イベント     | クライアントから、特定のアラームを追加または編集できなかったことをCICにレポートします。 |
| [`SetAlertSucceeded`](#SetAlertSucceeded)       | イベント     | クライアントから、特定のアラームを正常に追加または編集したことをCICにレポートします。 |
| [`StopAlert`](#StopAlert)                       | ディレクティブ | クライアントに対して、特定のアラームを停止するように指示します。  |
| [`SynchronizeAlert`](#SynchronizeAlert)         | ディレクティブ | クライアントに対して、`payload`内にあるユーザーのアラームデータを同期するように指示します。  |

上記のメッセージのうち、[`RequestSynchronizeAlert`](#RequestSynchronizeAlert)イベントと[`SynchronizeAlert`](#SynchronizeAlert)ディレクティブは、Clovaとクライアントの間でアラームやスケジュールのように、ユーザーアカウントに関連する情報を同期する際に使用されます。次のような状況で同期が発生します。

* ユーザーアカウントを利用するクライアントデバイスが追加されたとき
* クライアントがネットワーク接続障害などの理由により、CICに再接続するとき
* 他のユーザーが使用を開始したため、クライアントデバイスに登録されているユーザーアカウントが変更されたとき
* クライアントデバイスとペアリングアプリとの接続が解除され、再設定されるとき

<div class="note">
  <p><strong>Note!</strong></p>
  <p>ネットワークが切れたり、ユーザーアカウントの連携が解除された場合、アカウントに設定されているアラームデータをデバイスから削除する必要があります。</p>
</div>

## アラームの仕組み {#AlertsWorkFlow}

通常、アラームを設定してから停止するまでの流れは、次の通りです。

![](/CIC/Resources/Images/CIC_Alerts_Work_Flow.png)

1. ユーザーがアラームの設定を発話でリクエスト([`SpeechRecognizer.Recognize`](/CIC/References/CICInterface/SpeechRecognizer.md#Recognize))します。
2. Clovaは、ユーザーの発話を解析して、ユーザーのクライアントデバイスがアラームを追加するように[`Alerts.SetAlert`](#SetAlert)ディレクティブを送信します。
3. クライアントがアラームを設定して、その結果をCICに送信します([`Alerts.SetAlertSucceeded`](#SetAlertSucceeded)イベント、[`Alerts.SetAlertFailed`](#SetAlertFailed)イベントを使用する)。
4. Clovaは、アラームが設定された結果をユーザーに通知するために、[`SpeechSynthesizer.Speak`](/CIC/References/CICInterface/SpeechSynthesizer.md#Speak)ディレクティブと[`Clova.RenderTemplate`](/CIC/References/CICInterface/Clova.md#RenderTemplate)ディレクティブをクライアントに送信します。
5. 指定された時刻になると、クライアントはアラームを実行し、そのことを[`Alerts.AlertStarted`](#AlertStarted)イベントでCICにレポートします。アラームが開始したら、クライアントは、CICに送信するすべてのイベントに、現在アクティブなアラームの情報を含める必要があります。その際、[`Alert.AlertsState`](/CIC/References/Context_Objects.md#AlertsState)コンテキストの`activeAlerts`フィールドを使用します。
6. ユーザーは発話([`SpeechRecognizer.Recognize`](/CIC/References/CICInterface/SpeechRecognizer.md#Recognize))、物理ボタン(ハードウェア)、またはGUIボタン(ソフトウェア)でアラームを停止するようにリクエスト([`Alerts.RequestAlertStop`](#RequestAlertStop))します。
7. Clovaは、クライアントがアラームを停止するように、クライアントに[`Alerts.StopAlert`](#StopAlert)ディレクティブを送信します。
8. クライアントは、アラームを停止して、そのことを[`Alerts.AlertStopped`](#SetAlertSucceeded)イベントでレポートする必要があります。
9. アクションタイマーの場合、Clovaはクライアントに対して、ユーザーが予約した動作に該当するディレクティブを送信します。

<div class="note">
<p><strong>Note!</strong></p>
<p>スヌーズアラームの場合、現在の時刻からもっとも近いアラームのみをクライアントに設定し、実行します。クライアントに設定されているスヌーズアラームが一度実行されてから停止すると、次のスヌーズアラームをCICから新しく受信します。もし、ネットワークに長い間接続できない場合、スヌーズアラームが正常に動作しない可能性があります。</p>
</div>

上記の流れで、アラームを編集または削除できるのはステップ4までです。また、Clovaアプリでのみ編集および削除することができます。なお、ユーザーの発話に対するレスポンスとしてのディレクティブではない場合、ディレクティブは[ダウンチャネル](/CIC/Guides/Interact_with_CIC.md#CreateConnection)ストリーム上でクライアントに送信されます。

アラームを編集または削除する流れは、次の通りです。

1. ユーザーがClovaアプリでアラームを修正するか、削除しようとします。
2. Clovaはリクエストを処理するために、[`Alerts.SetAlert`](#SetAlert)ディレクティブまたは[`Alerts.DeleteAlert`](#DeleteAlert)ディレクティブをクライアントに送信します。
3. クライアントは、アラームを編集または削除した結果をCICに送信します。(関連イベントを使用する)

ユーザーのクライアントデバイスがが追加されたり、一部または特定のクライアントのネットワーク接続が解除され、再接続する場合、あるいはクライアントに登録されているユーザーのアカウントが変更される場合には、次の手順に従って、サーバーに登録されているユーザーのアラームデータをクライアントと同期する必要があります。

1. クライアントは、CICに接続または再接続した場合、[`System.RequestSynchronizeState`](/CIC/References/CICInterface/System.md#RequestSynchronizeState)イベントをCICに送信します。
2. クライアントは、CICから[`System.SynchronizeState`](/CIC/References/CICInterface/System.md#SynchronizeState)ディレクティブを受信します。その際、`allAlerts`フィールドのアラームデータをデバイスのアラームデータと同期します。

<div class="danger">
<p><strong>Caution!</strong></p>
<p>上記のような仕組みにより、クライアントがネットワークに接続しない場合、アラームに関連するすべての動作は正常に実行されません。</p>
</div>

## AlertStartedイベント {#AlertStarted}

クライアントから、アラームが開始したことをCICにレポートします。クライアントは、アラームが開始したら、必ずこのイベントをCICに送信する必要があります。

### Context fields

{% include "/CIC/References/CICInterface/Context_Objects_List.md" %}

### Payload fields

| フィールド名       | データ型    | 説明                     | 必須/任意 |
|---------------|---------|-----------------------------|:---------:|
| `token`   | string | 開始したアラームの識別子                  | 必須 |
| `type`    | string | アラームの種類。次のいずれかになります。<ul><li><code>"ACTIONTIMER"</code></li><li><code>"ALARM"</code></li><li><code>"REMINDER"</code></li><li><code>"TIMER"</code></li></ul>  | 必須 |

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
      "namespace": "Alerts",
      "name": "AlertStarted",
      "messageId": "4e4080d6-c440-498a-bb73-ae86c6312806"
    },
    "payload": {
      "token": "876afa88-8ad5-427b-9878-2edb5b103117",
      "type": "ALARM"
    }
  }
}
```

{% endraw %}

### 次の項目も参照してください。
* [`Alerts.AlertStopped`](#AlertStopped)

## AlertStoppedイベント {#AlertStopped}

クライアントから、アラームが停止したことをCICにレポートします。クライアントは、鳴っていたアラームが停止した場合、必ずこのイベントをCICに送信する必要があります。
* **普通のアラームが停止した場合**、CICから[`Alerts.DeleteAlert`](#DeleteAlert)ディレクティブを受信します。
* **スヌーズアラームが停止した場合**、次のスヌーズアラームを設定するために、CICから[`Alerts.SetAlert`](#SetAlert)ディレクティブを受信します。

### Context fields

{% include "/CIC/References/CICInterface/Context_Objects_List.md" %}

### Payload fields

| フィールド名       | データ型    | 説明                     | 必須/任意 |
|---------------|---------|-----------------------------|:---------:|
| `token`   | string | 停止したアラームの識別子                  | 必須 |
| `type`    | string | アラームの種類。次のいずれかになります。<ul><li><code>"ACTIONTIMER"</code></li><li><code>"ALARM"</code></li><li><code>"REMINDER"</code></li><li><code>"TIMER"</code></li></ul>  | 必須 |

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
      "namespace": "Alerts",
      "name": "AlertStopped",
      "messageId": "4e4080d6-c440-498a-bb73-ae86c6312806"
    },
    "payload": {
      "token": "876afa88-8ad5-427b-9878-2edb5b103117",
      "type": "ALARM"
    }
  }
}
```

{% endraw %}

### 次の項目も参照してください。
* [`Alerts.AlertStarted`](#AlertStarted)

## DeleteAlertディレクティブ {#DeleteAlert}

クライアントに対して、特定のアラームを削除するように指示します。クライアントは特定のアラームを削除し、その結果を次のイベントでCICにレポートする必要があります。

* [`Alerts.DeleteAlertSucceeded`](#DeleteAlertSucceeded)イベント：特定のアラームを正常に削除した場合
* [`Alerts.DeleteAlertFailed`](#DeleteAlertFailed)イベント：特定のアラームを削除できなかった場合

### Payload fields

| フィールド名       | データ型    | 説明                     | 包含 |
|---------------|---------|-----------------------------|:---------:|
| `token`   | string | 削除するアラームの識別子              | 常時 |
| `type`    | string | アラームの種類。次のいずれかになります。<ul><li><code>"ACTIONTIMER"</code></li><li><code>"ALARM"</code></li><li><code>"REMINDER"</code></li><li><code>"TIMER"</code></li></ul>  | 常時 |

### Message example
{% raw %}

```json
{
  "directive": {
    "header": {
      "namespace": "Alerts",
      "name": "DeleteAlert",
      "messageId": "4e4080d6-c440-498a-bb73-ae86c6312806",
      "dialogRequestId": "6b4061db-fbc1-45a2-9c54-b7c62d366b98"
    },
    "payload": {
      "token": "876afa88-8ad5-427b-9878-2edb5b103117",
      "type": "ALARM"
    }
  }
}
```

{% endraw %}

### 次の項目も参照してください。
* [`Alerts.DeleteAlertFailed`](#DeleteAlertFailed)
* [`Alerts.DeleteAlertSucceeded`](#DeleteAlertSucceeded)

## DeleteAlertFailedイベント {#DeleteAlertFailed}

クライアントから、クライアントに設定されている特定のアラームを削除できなかったことをCICにレポートします。クライアントは、[Alerts.DeleteAlert](#DeleteAlert)ディレクティブを受信して、特定のアラームを削除できなかった場合、必ずこのイベントをCICに送信する必要があります。

### Context fields

{% include "/CIC/References/CICInterface/Context_Objects_List.md" %}

### Payload fields

| フィールド名       | データ型    | 説明                     | 必須/任意 |
|---------------|---------|-----------------------------|:---------:|
| `token`   | string | 削除できなかったアラームの識別子             | 必須 |
| `type`    | string | アラームの種類。次のいずれかになります。<ul><li><code>"ACTIONTIMER"</code></li><li><code>"ALARM"</code></li><li><code>"REMINDER"</code></li><li><code>"TIMER"</code></li></ul>  | 必須 |

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
      "namespace": "Alerts",
      "name": "DeleteAlertFailed",
      "messageId": "4e4080d6-c440-498a-bb73-ae86c6312806"
    },
    "payload": {
      "token": "876afa88-8ad5-427b-9878-2edb5b103117",
      "type": "ALARM"
    }
  }
}
```

{% endraw %}

### 次の項目も参照してください。
* [`Alerts.DeleteAlert`](#DeleteAlert)
* [`Alerts.DeleteAlertSucceeded`](#DeleteAlertSucceeded)

## DeleteAlertSucceededイベント {#DeleteAlertSucceeded}

クライアントから、クライアントに設定されている特定のアラームを正常に削除したことをCICにレポートします。クライアントは、[Alerts.DeleteAlert](#DeleteAlert)ディレクティブを受信して、特定のアラームを正常に削除した場合、必ずこのイベントをCICに送信する必要があります。

### Context fields

{% include "/CIC/References/CICInterface/Context_Objects_List.md" %}

### Payload fields

| フィールド名       | データ型    | 説明                     | 必須/任意 |
|---------------|---------|-----------------------------|:---------:|
| `token`   | string | 削除したアラームの識別子                  | 必須 |
| `type`    | string | アラームの種類。次のいずれかになります。<ul><li><code>"ACTIONTIMER"</code></li><li><code>"ALARM"</code></li><li><code>"REMINDER"</code></li><li><code>"TIMER"</code></li></ul>  | 必須 |

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
      "namespace": "Alerts",
      "name": "DeleteAlertSucceeded",
      "messageId": "4e4080d6-c440-498a-bb73-ae86c6312806"
    },
    "payload": {
      "token": "876afa88-8ad5-427b-9878-2edb5b103117",
      "type": "ALARM"
    }
  }
}
```

{% endraw %}

### 次の項目も参照してください。
* [`Alerts.DeleteAlert`](#DeleteAlert)
* [`Alerts.DeleteAlertFailed`](#DeleteAlertFailed)

## RequestAlertStopイベント {#RequestAlertStop}

クライアントから、アクティブなアラームを停止するようにClovaに対してリクエストします。クライアントは、ユーザーが、発話ではなく物理ボタン(ハードウェア)またはGUIボタン(ソフトウェア)でアラームを停止した場合、CICにこのイベントを送信する必要があります。クライアントがCICにこのイベントを送信すると、後でCICから[`Alerts.StopAlert`](#StopAlert)ディレクティブを受信します。

### Context fields

{% include "/CIC/References/CICInterface/Context_Objects_List.md" %}

### Payload fields

| フィールド名       | データ型    | 説明                     | 必須/任意 |
|---------------|---------|-----------------------------|:---------:|
| `token`   | string | 停止するアラームの識別子                  | 必須 |
| `type`    | string | アラームの種類。次のいずれかになります。<ul><li><code>"ACTIONTIMER"</code></li><li><code>"ALARM"</code></li><li><code>"REMINDER"</code></li><li><code>"TIMER"</code></li></ul>  | 必須 |

### 備考
クライアントデバイスで、ユーザーがボタンを押して直接アラームを停止した場合にも、このイベントをCICに送信して、[`Alerts.StopAlert`](#StopAlert)ディレクティブを受信してからアラームを終了する必要があります。それはアラームを終了するプロセスの一貫性を保つためのもので、アラームの状態を同期する際に役立ちます。しかしそのせいで、アラームを終了するまで時間がかかる可能性があるので、[`Alerts.StopAlert`](#StopAlert)ディレクティブを受信するまでアラームの表示を止めるか、アラーム音をミュートにするなどの処理をする必要があります。

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
      "namespace": "Alerts",
      "name": "RequestAlertStop",
      "messageId": "4e4080d6-c440-498a-bb73-ae86c6312806"
    },
    "payload": {
      "token": "876afa88-8ad5-427b-9878-2edb5b103117",
      "type": "ALARM"
    }
  }
}
```

{% endraw %}

### 次の項目も参照してください。
* [`Alerts.StopAlert`](#StopAlert)

## RequestSynchronizeAlertイベント {#RequestSynchronizeAlert}

クライアントから、Clovaのクラウドに保存されたユーザーのアラームデータを同期する必要がある場合、CICにこのイベントを送信します。CICはこのイベントを受信すると、クライアントに[`Alerts.SynchronizeAlert`](#SynchronizeAlert)ディレクティブを送信します。

### Context fields

{% include "/CIC/References/CICInterface/Context_Objects_List.md" %}

### Payload fields

なし

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
      "namespace": "Alerts",
      "name": "RequestSynchronizeAlert",
      "messageId": "dd4f2794-6b14-4cc4-ae1b-5bfa1c469028"
    },
    "payload": {}
  }
}
```
{% endraw %}

### 次の項目も参照してください。
* [`System.SynchronizeAlert`](/CIC/References/CICInterface/Alerts.md#SynchronizeAlert)

## SetAlertディレクティブ {#SetAlert}

クライアントに対して、アラームを追加するか、または特定のアラームを編集するように指示します。クライアントは、次のようにアラームを追加または編集することができます。

* **`token`フィールドの値と同じ識別子を持つアラームが、現在クライアントデバイスにない場合**、受信したアラームを追加します。
* **`token`フィールドの値と同じ識別子を持つアラームが、現在クライアントデバイスにある場合**、そのアラームを編集します。

また、その結果を次のイベントでCICにレポートする必要があります。

* [`Alerts.SetAlertSucceeded`](#SetAlertSucceeded)イベント：特定のアラームを正常に追加・編集した場合
* [`Alerts.SetAlertFailed`](#SetAlertFailed)イベント：特定のアラームを追加・編集できなかった場合

### Payload field {#SetAlertPayload}

| フィールド名       | データ型    | 説明                     | 包含 |
|---------------|---------|-----------------------------|:---------:|
| `assets[]`         | object array | リマインダー(`"REMINDER"`)またはアクションタイマー(`"ACTIONTIMER"`)タイプのアラームが実行される際、再生するTTSオーディオのリストを持つオブジェクト配列。リマインダーとアクションタイマーにのみこのフィールドが含まれます。   | 条件付き |
| `assets[].assetId` | string | TTSオーディオの識別子       | 常時 |
| `assets[].url`     | string | TTSオーディオのURLもしこのフィールドの値が`"clova://alert/bell/{type}"`形式の場合、クライアントはアラームの種類(`type`)によって、クライアントが持っている着信音のうち、適切なものを再生する必要があります。現在、次のいずれかになります。<ul><li><code>"clova://alert/bell/reminder"</code>：リマインダーの着信音を再生する</li></ul>    | 常時 |
| `assetPlayOrder[]` | string array | `assets`フィールド内のTTSオーディオの再生順序を保存している配列。配列のインデックスの順番に合わせて、再生するTTSオーディオの識別子(`assets[].assetId`)が入力されています。リマインダー(`"REMINDER"`)とアクションタイマー(`"ACTIONTIMER"`)にのみこのフィールドが含まれます。  | 条件付き  |
| `label`          | string | リマインダーまたはアクションタイマーの内容                             | 条件付き |
| `scheduledTime`  | string | アラームを鳴らす日付と時間の情報(YYYY-MM-DDThh:mm:ssZの形式)   | 常時 |
| `token`          | string | 追加または編集するアラームの識別子                        | 常時 |
| `type`           | string | アラームの種類。次のいずれかになります。<ul><li><code>"ACTIONTIMER"</code></li><li><code>"ALARM"</code></li><li><code>"REMINDER"</code></li><li><code>"TIMER"</code></li></ul>  | 常時 |

### Message example
{% raw %}

```json
{
  "directive": {
    "header": {
      "namespace": "Alerts",
      "name": "SetAlert",
      "messageId": "9a440fa9-983a-48a8-8ad5-faee1250abde",
      "dialogRequestId": "688b051d-6832-4bfd-8cf8-5ff073cd2a82"
    },
    "payload": {
      "type": "REMINDER",
      "token": "77179dbd-b65f-4341-a579-c1b2b97fc5b7",
      "scheduledTime": "2017-09-25T09:00:50+09:00",
      "assets": [
        {
          "assetId": "5141f693-5b39-46b7-80e4-3d71ed5508da",
          "url": "clova://alert/bell/reminder"
        },
        {
          "assetId": "b403ebe5-f911-4c5c-98b3-9f5320510235",
          "url": "http://abc.de.fe/tts2"
        }
      ],
      "label": "入金する",
      "assetPlayOrder": [
        "5141f693-5b39-46b7-80e4-3d71ed5508da",
        "b403ebe5-f911-4c5c-98b3-9f5320510235"
      ]
    }
  }
}
```

{% endraw %}

### 次の項目も参照してください。
* [`Alerts.SetAlertFailed`](#SetAlertFailed)
* [`Alerts.SetAlertSucceeded`](#SetAlertSucceeded)

## SetAlertFailedイベント {#SetAlertFailed}

クライアントから、特定のアラームを追加または編集できなかったことをCICにレポートします。クライアントは、[Alerts.SetAlert](#SetAlert)ディレクティブを受信して、特定のアラームを追加または編集できなかった場合、必ずこのイベントをCICに送信する必要があります。

### Context fields

{% include "/CIC/References/CICInterface/Context_Objects_List.md" %}

### Payload fields

| フィールド名       | データ型    | 説明                     | 必須/任意 |
|---------------|---------|-----------------------------|:---------:|
| `token`   | string | 追加または編集できなかったアラームの識別子     | 必須 |
| `type`    | string | アラームの種類。次のいずれかになります。<ul><li><code>"ACTIONTIMER"</code></li><li><code>"ALARM"</code></li><li><code>"REMINDER"</code></li><li><code>"TIMER"</code></li></ul>  | 必須 |

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
      "namespace": "Alerts",
      "name": "SetAlertFailed",
      "messageId": "4e4080d6-c440-498a-bb73-ae86c6312806"
    },
    "payload": {
      "token": "876afa88-8ad5-427b-9878-2edb5b103117",
      "type": "ALARM"
    }
  }
}
```

{% endraw %}

### 次の項目も参照してください。
* [`Alerts.SetAlert`](#SetAlert)
* [`Alerts.SetAlertSucceeded`](#SetAlertSucceeded)


## SetAlertSucceededイベント {#SetAlertSucceeded}

クライアントから、特定のアラームを正常に追加または編集したことをCICにレポートします。クライアントは、[Alerts.SetAlert](#SetAlert)ディレクティブを受信して、特定のアラームを正常に追加または編集した場合、必ずこのイベントをCICに送信する必要があります。

### Context fields

{% include "/CIC/References/CICInterface/Context_Objects_List.md" %}

### Payload fields

| フィールド名       | データ型    | 説明                     | 必須/任意 |
|---------------|---------|-----------------------------|:---------:|
| `token`   | string | 追加または編集したアラームの識別子          | 必須 |
| `type`    | string | アラームの種類。次のいずれかになります。<ul><li><code>"ACTIONTIMER"</code></li><li><code>"ALARM"</code></li><li><code>"REMINDER"</code></li><li><code>"TIMER"</code></li></ul>  | 必須 |

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
      "namespace": "Alerts",
      "name": "SetAlertSucceeded",
      "messageId": "4e4080d6-c440-498a-bb73-ae86c6312806"
    },
    "payload": {
      "token": "876afa88-8ad5-427b-9878-2edb5b103117",
      "type": "ALARM"
    }
  }
}
```

{% endraw %}

### 次の項目も参照してください。
* [`Alerts.SetAlert`](#SetAlert)
* [`Alerts.SetAlertFailed`](#SetAlertFailed)

## StopAlertディレクティブ {#StopAlert}

クライアントに対して、特定のアラームを停止するように指示します。クライアントは指定されたアラームを停止し、[`AlertStopped`](#AlertStopped)イベントでその結果をCICにレポートする必要があります。


### Payload fields

| フィールド名       | データ型    | 説明                     | 包含 |
|---------------|---------|-----------------------------|:---------:|
| `token`   | string | 停止するアラームの識別子              | 常時 |
| `type`    | string | アラームの種類。次のいずれかになります。<ul><li><code>"ACTIONTIMER"</code></li><li><code>"ALARM"</code></li><li><code>"REMINDER"</code></li><li><code>"TIMER"</code></li></ul>  | 常時 |

### Message example
{% raw %}

```json
{
  "directive": {
    "header": {
      "namespace": "Alerts",
      "name": "DeleteAlert",
      "messageId": "4e4080d6-c440-498a-bb73-ae86c6312806",
      "dialogRequestId": "6b4061db-fbc1-45a2-9c54-b7c62d366b98"
    },
    "payload": {
      "token": "876afa88-8ad5-427b-9878-2edb5b103117",
      "type": "ALARM"
    }
  }
}
```

{% endraw %}

### 次の項目も参照してください。
* [`Alerts.AlertStopped`](#AlertStopped)

## SynchronizeAlertディレクティブ {#SynchronizeAlert}
クライアントに対して、`payload`内にあるユーザーのアラームデータを同期するように指示します。クライアントは、CICから受信したデータに応じて、クライアントに設定されているアラームの値を変更する必要があります。

### Payload fields

| フィールド名       | データ型    | 説明                     | 包含 |
|---------------|---------|-----------------------------|:---------:|
| `allAlerts[]`   | object array | クライアントが同期すべきアラームのリストを含むオブジェクト配列[`Alerts.SetAlert`](#SetAlert)ディレクティブで使用される[`payload`](#SetAlertPayload)オブジェクトと同じ形式です。 | 常時    |

### Message example

{% raw %}

```json
{
  "directive": {
    "header": {
      "namespace": "Alerts",
      "name": "SynchronizeAlert",
      "messageId": "29745c13-0d70-408e-a4cc-946afba67524"
    },
    "payload": {
      "allAlerts": [
        {
          "type": "REMINDER",
          "token": "77179dbd-b65f-4341-a579-c1b2b97fc5b7",
          "scheduledTime": "2017-09-25T09:00:50+09:00",
          "assets": [
            {
              "assetId": "5141f693-5b39-46b7-80e4-3d71ed5508da",
              "url": "clova://alert/bell/reminder"
            },
            {
              "assetId": "b403ebe5-f911-4c5c-98b3-9f5320510235",
              "url": "http://abc.de.fe/tts2"
            }
          ],
          "assetPlayOrder": ["5141f693-5b39-46b7-80e4-3d71ed5508da", "b403ebe5-f911-4c5c-98b3-9f5320510235"]
        },
        {
          "type": "ALARM",
          "token": "ee4da70c-8328-4456-ab6f-c28cec626ae6",
          "scheduledTime": "2017-09-26T11:00:50+09:00"
        },
        ...
      ]
    }
  }
}
```

{% endraw %}

### 次の項目も参照してください。
* [`Alerts.RequestSynchronizeAlert`](#RequestSynchronizeAlert)
