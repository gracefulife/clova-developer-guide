# PlaybackController

PlaybackControllerは、クライアントのオーディオ再生およびスピーカー出力をコントロールする際に使用する名前欄です。PlaybackControllerでは、次のイベントとディレクティブを提供しています。

| メッセージ         | タイプ  | 説明                                   |
|------------------|-----------|---------------------------------------------|
| [`CustomCommandIssued`](#CustomCommandIssued)  | イベント     | ユーザーがクライアントデバイスのショートカットボタンのうち1つを押した場合、クライアントはこのイベントをCICに送信する必要があります。  |
| [`ExpectNextCommand`](#ExpectNextCommand)      | ディレクティブ | ユーザーがクライアント上で「次」ボタン(Next)を押して、その効果が発生したときのように、クライアントが[`PlaybackController.NextCommandIssued`](#NextCommandIssued)イベントをCICに送信するように指示します。  |
| [`ExpectPauseCommand`](#ExpectPauseCommand)    | ディレクティブ | ユーザーがクライアント上で「一時停止」ボタン(Pause)を押して、その効果が発生したときのように、クライアントが[`PlaybackController.PauseCommandIssued`](#PauseCommandIssued)イベントをCICに送信するように指示します。  |
| [`ExpectPlayCommand`](#ExpectPlayCommand)      | ディレクティブ | ユーザーがクライアント上で「再生」ボタン(Play)を押して、その効果が発生したときのように、クライアントが[`PlaybackController.PlayCommandIssued`](#PlayCommandIssued)イベントをCICに送信するように指示します。  |
| [`ExpectPreviousCommand`](#ExpectPreviousCommand)  | ディレクティブ | ユーザーがクライアント上で「前」ボタン(Previous)を押して、その効果が発生したときのように、クライアントが[`PlaybackController.PreviousCommandIssued`](#PreviousCommandIssued)イベントをCICに送信するように指示します。  |
| [`ExpectResumeCommand`](#ExpectResumeCommand)  | ディレクティブ | ユーザーがクライアント上で「再開」ボタン(Resume)を押して、その効果が発生したときのように、クライアントが[`PlaybackController.ResumeCommandIssued`](#ResumeCommandIssued)イベントをCICに送信するように指示します。  |
| [`ExpectStopCommand`](#ExpectStopCommand)      | ディレクティブ | ユーザーがクライアント上で「停止」ボタン(Stop)を押して、その効果が発生したときのように、クライアントが[`PlaybackController.StopCommandIssued`](#StopCommandIssued)イベントをCICに送信するように指示します。  |
| [`Mute`](#Mute)                                | ディレクティブ | クライアントに、オーディオプレーヤーをミュートにするように指示します。            |
| [`Next`](#Next)                                | ディレクティブ | クライアントに、再生キューに入っている次のオーディオストリームを再生するように指示します。   |
| [`NextCommandIssued`](#NextCommandIssued)      | イベント     | ユーザーがクライアント上で「次」ボタン(Next)を押したり、CICから[`PlaybackController.ExpectNextCommand`](#ExpectNextCommand)ディレクティブを受信した場合、クライアントはこのイベントをCICに送信する必要があります。 |
| [`Pause`](#Pause)                              | ディレクティブ | クライアントに、再生中のオーディオストリームを一時停止するように指示します。        |
| [`PauseCommandIssued`](#PauseCommandIssued)    | イベント     | ユーザーがクライアント上で「一時停止」ボタン(Pause)を押したり、CICから[`PlaybackController.ExpectPauseCommand`](#ExpectPauseCommand)ディレクティブを受信した場合、クライアントはこのイベントをCICに送信する必要があります。  |
| [`PlayCommandIssued`](#PlayCommandIssued)      | イベント     | ユーザーがクライアント上で「再生」ボタン(Play)を押したり、CICから[`PlaybackController.ExpectPlayCommand`](#ExpectPlayCommand)ディレクティブを受信した場合、クライアントはこのイベントをCICに送信する必要があります。  |
| [`Previous`](#Previous)                        | ディレクティブ | クライアントに、再生キューにある前のオーディオストリームを再生するように指示します。 |
| [`PreviousCommandIssued`](#PreviousCommandIssued) | イベント | ユーザーがクライアント上で「前へ」ボタン(Previous)を押したり、CICから[`PlaybackController.ExpectPreviousCommand`](#ExpectPreviousCommand)ディレクティブを受信した場合、クライアントはこのイベントをCICに送信する必要があります。 |
| [`Replay`](#Replay)                            | ディレクティブ | クライアントに、オーディオストリームを最初から再度再生するように指示します。         |
| [`Resume`](#Resume)                            | ディレクティブ | クライアントに、オーディオストリームの再生を再開するように指示します。                |
| [`ResumeCommandIssued`](#ResumeCommandIssued)  | ディレクティブ | ユーザーがクライアント上で「再開」ボタン(Resume)を押したり、CICから[`PlaybackController.ExpectResumeCommand`](#ExpectResumeCommand)ディレクティブを受信した場合、クライアントはこのイベントをCICに送信する必要があります。  |
| [`SetRepeatMode`](#SetRepeatMode)              | ディレクティブ | クライアントに、指定されたリピート再生モードに再生状態を変更するように指示します。  |
| [`SetRepeatModeCommandIssued`](#SetRepeatModeCommandIssued) | イベント | ユーザーがクライアント上で「リピート再生」ボタン(Repeat)を押した場合、クライアントはこのイベントをCICに送信する必要があります。  |
| [`Stop`](#Stop)                                | ディレクティブ | クライアントに、オーディオストリームの再生を停止するように指示します。                |
| [`StopCommandIssued`](#StopCommandIssued)      | イベント     | ユーザーがクライアント上で「リピート再生」ボタン(Repeat)を押した場合、クライアントはこのイベントをCICに送信する必要があります。  |
| [`TurnOffRepeatMode`](#TurnOffRepeatMode)      | ディレクティブ | **(非推奨)** クライアントに、1曲リピート再生モードを無効にするように指示します。                  |
| [`TurnOnRepeatMode`](#TurnOnRepeatMode)        | ディレクティブ | **(非推奨)** クライアントに、1曲リピート再生モードを有効にするように指示します。                  |
| [`Unmute`](#Unmute)                            | ディレクティブ | クライアントに、オーディオプレーヤーのミュートを解除するように指示します。              |
| [`VolumeDown`](#VolumeDown)                    | ディレクティブ | クライアントに、オーディオプレーヤーの音量を下げるように指示します。                      |
| [`VolumeUp`](#VolumeUp)                        | ディレクティブ | クライアントに、オーディオプレーヤーの音量を上げるように指示します。                      |

## CustomCommandIssuedイベント {#CustomCommandIssued}
ユーザーがクライアントデバイスのショートカットボタンのうち1つを押した場合、クライアントはこのイベントをCICに送信する必要があります。CICはこのイベントを受信すると、適切なディレクティブをクライアントに送信します。

### Context fields

{% include "/CIC/References/CICInterface/Context_Objects_List.md" %}

### Payload fields
| フィールド名       | データ型    | 説明                     | 必須/任意 |
|---------------|---------|-----------------------------|:---------:|
| `button`      | string  | クライアントデバイスのショートカットボタンを区別するための値です。(例：<code>"CUSTOM_BUTTON_2"</code>) | 常時 |

### 備考
* クライアントデバイスのボタンは、ハードウェア方式の物理ボタンの場合もあり、オーディオプレーヤーウィジェットのボタンのようなソフトウェア方式のボタンの場合もあります。

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
      "namespace": "PlaybackController",
      "name": "CustomCommandIssued",
      "messageId": "4e4080d6-c440-498a-bb73-ae86c6312806"
    },
    "payload": {
      "button": "CUSTOM_BUTTON_2"
    }
  }
}
```
{% endraw %}

### 次の項目も参照してください。
* [`PlaybackController.NextCommandIssued`](#NextCommandIssued)
* [`PlaybackController.PauseCommandIssued`](#PauseCommandIssued)
* [`PlaybackController.PlayCommandIssued`](#PlayCommandIssued)
* [`PlaybackController.PreviousCommandIssued`](#PreviousCommandIssued)
* [`PlaybackController.ResumeCommandIssued`](#ResumeCommandIssued)
* [`PlaybackController.SetRepeatModeCommandIssued`](#SetRepeatModeCommandIssued)
* [`PlaybackController.StopCommandIssued`](#StopCommandIssued)

## ExpectNextCommandディレクティブ {#ExpectNextCommand}
ユーザーがクライアント上で「次」ボタン(Next)を押して、その効果が発生したときのように、クライアントが[`PlaybackController.NextCommandIssued`](#NextCommandIssued)イベントをCICに送信するように指示します。クライアントはこのディレクティブを受信すると、関連する動作を処理して、[`PlaybackController.NextCommandIssued`](#NextCommandIssued)イベントをCICに送信する必要があります。

### Payload fields
なし

### Message example
{% raw %}
```json
{
  "directive": {
    "header": {
      "namespace": "PlaybackController",
      "name": "ExpectNextCommand",
      "dialogRequestId": "42390b12-ae91-4121-aa0a-37f74e8e422b",
      "messageId": "b1f88d7d-bbb8-44fa-a0a2-c5a7553e6f8a"
    },
    "payload": {}
  }
}
```
{% endraw %}

### 次の項目も参照してください。
* [`PlaybackController.ExpectPauseCommand`](#ExpectPauseCommand)
* [`PlaybackController.ExpectPlayCommand`](#ExpectPlayCommand)
* [`PlaybackController.ExpectPreviousCommand`](#ExpectPreviousCommand)
* [`PlaybackController.ExpectResumeCommand`](#ExpectResumeCommand)
* [`PlaybackController.ExpectStopCommand`](#ExpectStopCommand)
* [`PlaybackController.NextCommandIssued`](#NextCommandIssued)

## ExpectPauseCommandディレクティブ {#ExpectPauseCommand}
ユーザーがクライアント上で「一時停止」ボタン(Pause)を押して、その効果が発生したときのように、クライアントが[`PlaybackController.PauseCommandIssued`](#PauseCommandIssued)イベントをCICに送信するように指示します。クライアントはこのディレクティブを受信すると、[`PlaybackController.PauseCommandIssued`](#PauseCommandIssued)イベントをCICに送信する必要があります。

### Payload fields
なし

### Message example
{% raw %}
```json
{
  "directive": {
    "header": {
      "namespace": "PlaybackController",
      "name": "ExpectPauseCommand",
      "dialogRequestId": "42390b12-ae91-4121-aa0a-37f74e8e422b",
      "messageId": "b1f88d7d-bbb8-44fa-a0a2-c5a7553e6f8a"
    },
    "payload": {}
  }
}
```
{% endraw %}

### 次の項目も参照してください。
* [`PlaybackController.ExpectNextCommand`](#ExpectNextCommand)
* [`PlaybackController.ExpectPlayCommand`](#ExpectPlayCommand)
* [`PlaybackController.ExpectPreviousCommand`](#ExpectPreviousCommand)
* [`PlaybackController.ExpectResumeCommand`](#ExpectResumeCommand)
* [`PlaybackController.ExpectStopCommand`](#ExpectStopCommand)
* [`PlaybackController.PauseCommandIssued`](#PauseCommandIssued)

## ExpectPlayCommandディレクティブ {#ExpectPlayCommand}
ユーザーがクライアント上で「再生」ボタン(Play)を押して、その効果が発生したときのように、クライアントが[`PlaybackController.PlayCommandIssued`](#PlayCommandIssued)イベントをCICに送信するように指示します。このディレクティブは、現在再生しているオーディオストリームを別のデバイスで再生しようとするときにも受信することがあります。クライアントはこのディレクティブを受信すると、関連する動作を処理して、[`PlaybackController.PlayCommandIssued`](#PlayCommandIssued)イベントをCICに送信する必要があります。

### Payload fields

| フィールド名       | データ型    | 説明                     | 常時/条件付き |
|---------------|---------|-----------------------------|:---------:|
| `handover`            | object  | リモートでオーディオの再生を引き継ぐときに必要な情報を持つオブジェクト。オーディオの再生を引き継ぐ場合、`handover`オブジェクトがメッセージに含まれます。`handover`オブジェクトが含まれている場合、クライアントは[`PlaybackController.PlayCommandIssued`](#PlayCommandIssued)イベントの`payload`内の`handover`オブジェクトを、このオブジェクトの内容で設定する必要があります。     | 条件付き |
| `handover.deviceId`   | string  | オーディオの再生を引き渡すクライアントデバイスのID  | 常時 |
| `handover.customData` | string  | オーディオの再生に必要な情報。               | 常時 |
| `token`               | string  | 再生するオーディオストリームのトークン。オーディオの再生を引き継ぐ場合、`token`フィールドがメッセージに含まれます。`token`フィールドが含まれている場合、クライアントは[`PlaybackController.PlayCommandIssued`](#PlayCommandIssued)イベントの`token`に、このフィールドの値を入力する必要があります。  | 条件付き  |

### Message example
{% raw %}
```json
{
  "directive": {
    "header": {
      "namespace": "PlaybackController",
      "name": "ExpectPlayCommand",
      "dialogRequestId": "42390b12-ae91-4121-aa0a-37f74e8e422b",
      "messageId": "b1f88d7d-bbb8-44fa-a0a2-c5a7553e6f8a"
    },
    "payload": {}
  }
}
```
{% endraw %}

### 次の項目も参照してください。
* [`PlaybackController.ExpectNextCommand`](#ExpectNextCommand)
* [`PlaybackController.ExpectPauseCommand`](#ExpectPauseCommand)
* [`PlaybackController.ExpectPreviousCommand`](#ExpectPreviousCommand)
* [`PlaybackController.ExpectResumeCommand`](#ExpectResumeCommand)
* [`PlaybackController.ExpectStopCommand`](#ExpectStopCommand)
* [`PlaybackController.PlayCommandIssued`](#PlayCommandIssued)

## ExpectPreviousCommandディレクティブ {#ExpectPreviousCommand}
ユーザーがクライアント上で「前」ボタン(Previous)を押して、その効果が発生したときのように、クライアントが[`PlaybackController.PreviousCommandIssued`](#PreviousCommandIssued)イベントをCICに送信するように指示します。クライアントはこのディレクティブを受信すると、関連する動作を処理して、[`PlaybackController.PreviousCommandIssued`](#PreviousCommandIssued)イベントをCICに送信する必要があります。

### Payload fields
なし

### Message example
{% raw %}
```json
{
  "directive": {
    "header": {
      "namespace": "PlaybackController",
      "name": "ExpectPreviousCommand",
      "dialogRequestId": "42390b12-ae91-4121-aa0a-37f74e8e422b",
      "messageId": "b1f88d7d-bbb8-44fa-a0a2-c5a7553e6f8a"
    },
    "payload": {}
  }
}
```
{% endraw %}

### 次の項目も参照してください。
* [`PlaybackController.ExpectNextCommand`](#ExpectNextCommand)
* [`PlaybackController.ExpectPauseCommand`](#ExpectPauseCommand)
* [`PlaybackController.ExpectPlayCommand`](#ExpectPlayCommand)
* [`PlaybackController.ExpectResumeCommand`](#ExpectResumeCommand)
* [`PlaybackController.ExpectStopCommand`](#ExpectStopCommand)
* [`PlaybackController.PreviousCommandIssued`](#PreviousCommandIssued)

## ExpectResumeCommandディレクティブ {#ExpectResumeCommand}
ユーザーがクライアント上で「再開」ボタン(Resume)を押して、その効果が発生したときのように、クライアントが[`PlaybackController.ResumeCommandIssued`](#ResumeCommandIssued)イベントをCICに送信するように指示します。クライアントはこのディレクティブを受信すると、[`PlaybackController.ResumeCommandIssued`](#ResumeCommandIssued)イベントをCICに送信する必要があります。

### Payload fields
なし

### Message example
{% raw %}
```json
{
  "directive": {
    "header": {
      "namespace": "PlaybackController",
      "name": "ExpectResumeCommand",
      "dialogRequestId": "42390b12-ae91-4121-aa0a-37f74e8e422b",
      "messageId": "b1f88d7d-bbb8-44fa-a0a2-c5a7553e6f8a"
    },
    "payload": {}
  }
}
```
{% endraw %}

### 次の項目も参照してください。
* [`PlaybackController.ExpectNextCommand`](#ExpectNextCommand)
* [`PlaybackController.ExpectPauseCommand`](#ExpectPauseCommand)
* [`PlaybackController.ExpectPlayCommand`](#ExpectPlayCommand)
* [`PlaybackController.ExpectPreviousCommand`](#ExpectPreviousCommand)
* [`PlaybackController.ExpectStopCommand`](#ExpectStopCommand)
* [`PlaybackController.ResumeCommandIssued`](#ResumeCommandIssued)

## ExpectStopCommandディレクティブ {#ExpectStopCommand}
ユーザーがクライアント上で「停止」ボタン(Stop)を押して、その効果が発生したときのように、クライアントが[`PlaybackController.StopCommandIssued`](#StopCommandIssued)イベントをCICに送信するように指示します。クライアントはこのディレクティブを受信すると、[`PlaybackController.StopCommandIssued`](#StopCommandIssued)イベントをCICに送信する必要があります。

### Payload fields
なし

### Message example
{% raw %}
```json
{
  "directive": {
    "header": {
      "namespace": "PlaybackController",
      "name": "ExpectStopCommand",
      "dialogRequestId": "42390b12-ae91-4121-aa0a-37f74e8e422b",
      "messageId": "b1f88d7d-bbb8-44fa-a0a2-c5a7553e6f8a"
    },
    "payload": {}
  }
}
```
{% endraw %}

### 次の項目も参照してください。
* [`PlaybackController.ExpectNextCommand`](#ExpectNextCommand)
* [`PlaybackController.ExpectPauseCommand`](#ExpectPauseCommand)
* [`PlaybackController.ExpectPlayCommand`](#ExpectPlayCommand)
* [`PlaybackController.ExpectPreviousCommand`](#ExpectPreviousCommand)
* [`PlaybackController.ExpectResumeCommand`](#ExpectResumeCommand)
* [`PlaybackController.StopCommandIssued`](#StopCommandIssued)

## Muteディレクティブ {#Mute}
クライアントに、オーディオプレーヤーをミュートにするように指示します。クライアントはこのディレクティブを受信すると、オーディオストリームの再生に関連するスピーカーをミュートにする必要があります。

### Payload fields
なし

### 備考

Clovaは、スピーカーの出力に関連するコントロールの場合、通知のためのオーディオファイルを[`SpeechSynthesizer.Speak`](/CIC/References/CICInterface/SpeechSynthesizer.md#Speak)ディレクティブに添付しません。それは、ユーザーの音楽鑑賞などのUXを向上させるためで、その場合には音声案内の代わりに、クライアントデバイスのライトや、短い効果音などで音量が調節されたことをユーザーに通知する必要があります。

### Message example
{% raw %}
```json
{
  "directive": {
    "header": {
      "namespace": "PlaybackController",
      "name": "Mute",
      "dialogRequestId": "42390b12-ae91-4121-aa0a-37f74e8e422b",
      "messageId": "b1f88d7d-bbb8-44fa-a0a2-c5a7553e6f8a"
    },
    "payload": {}
  }
}
```
{% endraw %}

### 次の項目も参照してください。
* [`SpeechRecognizer.Recognize`](/CIC/References/CICInterface/SpeechRecognizer.md#Recognize)

## Nextディレクティブ {#Next}
クライアントに、再生キューに入っている次のオーディオストリームを再生するように指示します。クライアントは、このディレクティブを受信すると、次のオーディオストリームを再生する必要があります。

### Payload fields
なし

### Message example
{% raw %}
```json
{
  "directive": {
    "header": {
      "namespace": "PlaybackController",
      "name": "Next",
      "dialogRequestId": "42390b12-ae91-4121-aa0a-37f74e8e422b",
      "messageId": "b1f88d7d-bbb8-44fa-a0a2-c5a7553e6f8a"
    },
    "payload": {}
  }
}
```
{% endraw %}

### 次の項目も参照してください。
* [`SpeechRecognizer.Recognize`](/CIC/References/CICInterface/SpeechRecognizer.md#Recognize)

## NextCommandIssuedイベント {#NextCommandIssued}
ユーザーがクライアント上で「次」ボタン(Next)を押したり、CICから[`PlaybackController.ExpectNextCommand`](#ExpectNextCommand)ディレクティブを受信した場合、クライアントはこのイベントをCICに送信する必要があります。CICはこのイベントを受信すると、適切なディレクティブをクライアントに送信します。


### Context fields

{% include "/CIC/References/CICInterface/Context_Objects_List.md" %}

### Payload fields

| フィールド名       | データ型    | 説明                     | 必須/任意 |
|---------------|---------|-----------------------------|:---------:|
| `deviceId`    | string  | クライアントデバイスのID。オーディオの再生をリモートでコントロールする状況でない場合、このフィールドは省略します。 | 選択 |

### 備考
* クライアントデバイスのボタンは、ハードウェア方式の物理ボタンの場合もあり、オーディオプレーヤーウィジェットのボタンのようなソフトウェア方式のボタンの場合もあります。

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
      "namespace": "PlaybackController",
      "name": "NextCommandIssued",
      "messageId": "4e4080d6-c440-498a-bb73-ae86c6312806"
    },
    "payload": {}
  }
}
```
{% endraw %}

### 次の項目も参照してください。
* [`PlaybackController.CustomCommandIssued`](#CustomCommandIssued)
* [`PlaybackController.ExpectNextCommand`](#ExpectNextCommand)
* [`PlaybackController.PauseCommandIssued`](#PauseCommandIssued)
* [`PlaybackController.PlayCommandIssued`](#PlayCommandIssued)
* [`PlaybackController.PreviousCommandIssued`](#PreviousCommandIssued)
* [`PlaybackController.ResumeCommandIssued`](#ResumeCommandIssued)
* [`PlaybackController.SetRepeatModeCommandIssued`](#SetRepeatModeCommandIssued)
* [`PlaybackController.StopCommandIssued`](#StopCommandIssued)

## Pauseディレクティブ {#Pause}
クライアントに、再生中のオーディオストリームを一時停止するように指示します。クライアントは、このディレクティブを受信すると、オーディオストリームの再生を一時停止する必要があります。

### Payload fields
なし

### Message example
{% raw %}
```json
{
  "directive": {
    "header": {
      "namespace": "PlaybackController",
      "name": "Pause",
      "dialogRequestId": "42390b12-ae91-4121-aa0a-37f74e8e422b",
      "messageId": "b1f88d7d-bbb8-44fa-a0a2-c5a7553e6f8a"
    },
    "payload": {}
  }
}
```
{% endraw %}

### 次の項目も参照してください。
* [`AudioPlayer.PlayPaused`](/CIC/References/CICInterface/AudioPlayer.md#PlayPaused)
* [`SpeechRecognizer.Recognize`](/CIC/References/CICInterface/SpeechRecognizer.md#Recognize)

## PauseCommandIssuedイベント {#PauseCommandIssued}
ユーザーがクライアント上で「一時停止」ボタン(Pause)を押したり、CICから[`PlaybackController.ExpectPauseCommand`](#ExpectPauseCommand)ディレクティブを受信した場合、クライアントはこのイベントをCICに送信する必要があります。CICはこのイベントを受信すると、適切なディレクティブをクライアントに送信します。


### Context fields

{% include "/CIC/References/CICInterface/Context_Objects_List.md" %}

### Payload fields

| フィールド名       | データ型    | 説明                     | 必須/任意 |
|---------------|---------|-----------------------------|:---------:|
| `deviceId`    | string  | クライアントデバイスのID。オーディオの再生をリモートでコントロールする状況でない場合、このフィールドは省略します。 | 選択 |

### 備考
* クライアントデバイスのボタンは、ハードウェア方式の物理ボタンの場合もあり、オーディオプレーヤーウィジェットのボタンのようなソフトウェア方式のボタンの場合もあります。

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
      "namespace": "PlaybackController",
      "name": "PauseCommandIssued",
      "messageId": "4e4080d6-c440-498a-bb73-ae86c6312806"
    },
    "payload": {}
  }
}
```
{% endraw %}

### 次の項目も参照してください。
* [`PlaybackController.CustomCommandIssued`](#CustomCommandIssued)
* [`PlaybackController.ExpectPauseCommand`](#ExpectNextCommand)
* [`PlaybackController.NextCommandIssued`](#NextCommandIssued)
* [`PlaybackController.PlayCommandIssued`](#PlayCommandIssued)
* [`PlaybackController.PreviousCommandIssued`](#PreviousCommandIssued)
* [`PlaybackController.ResumeCommandIssued`](#ResumeCommandIssued)
* [`PlaybackController.SetRepeatModeCommandIssued`](#SetRepeatModeCommandIssued)
* [`PlaybackController.StopCommandIssued`](#StopCommandIssued)

## PlayCommandIssuedイベント {#PlayCommandIssued}
ユーザーがクライアント上で「再生」ボタン(Play)を押したり、CICから[`PlaybackController.ExpectPlayCommand`](#ExpectPlayCommand)ディレクティブを受信した場合、クライアントはこのイベントをCICに送信する必要があります。CICはこのイベントを受信すると、適切なディレクティブをクライアントに送信します。CICから送信された[`PlaybackController.ExpectPlayCommand`](#ExpectPlayCommand)ディレクティブの`payload`に`handover`フィールドが含まれている場合、そのまま使用してオーディオ再生の引き継ぐ必要があります。


### Context fields

{% include "/CIC/References/CICInterface/Context_Objects_List.md" %}

### Payload fields

| フィールド名       | データ型    | 説明                     | 必須/任意 |
|---------------|---------|-----------------------------|:---------:|
| `deviceId`            | string  | クライアントデバイスのID。リモートでオーディオの再生を引き渡す状況でない場合、`deviceId`フィールドは省略します。 | 選択 |
| `handover`            | object  | リモートでオーディオの再生を引き継ぐときに必要な情報を持つオブジェクト。オーディオ再生を引き継ぐ必要がある場合、`handover`オブジェクトの内容を、[`PlaybackController.ExpectPlayCommand`](#ExpectPlayCommand)ディレクティブの`payload`の`handover`オブジェクトで設定する必要があります。     | 選択 |
| `handover.deviceId`   | string  | オーディオの再生を引き渡すクライアントデバイスのID  | 必須 |
| `handover.customData` | string  | オーディオの再生に必要な情報。               | 必須 |
| `token`               | string  | 再生するオーディオストリームのトークン。ユーザーがリストからトラックを選んで再生ボタンを押した場合、[`TemplateRuntime.RenderPlayerInfo`](/CIC/References/CICInterface/TemplateRuntime.md#RenderPlayerInfo)ディレクティブの`playableItems[].token`フィールドの値が適用される必要があります。[`PlaybackController.ExpectPlayCommand`](#ExpectPlayCommand)ディレクティブを受信した場合、そのメッセージの`token`フィールドの値を入力することもあります。  | 選択  |

### 備考
* クライアントデバイスのボタンは、ハードウェア方式の物理ボタンの場合もあり、オーディオプレーヤーウィジェットのボタンのようなソフトウェア方式のボタンの場合もあります。

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
      "namespace": "PlaybackController",
      "name": "PlayCommandIssued",
      "messageId": "4e4080d6-c440-498a-bb73-ae86c6312806"
    },
    "payload": {}
  }
}
```
{% endraw %}

### 次の項目も参照してください。
* [`PlaybackController.CustomCommandIssued`](#CustomCommandIssued)
* [`PlaybackController.ExpectPlayCommand`](#ExpectNextCommand)
* [`PlaybackController.NextCommandIssued`](#NextCommandIssued)
* [`PlaybackController.PauseCommandIssued`](#PauseCommandIssued)
* [`PlaybackController.PreviousCommandIssued`](#PreviousCommandIssued)
* [`PlaybackController.ResumeCommandIssued`](#ResumeCommandIssued)
* [`PlaybackController.SetRepeatModeCommandIssued`](#SetRepeatModeCommandIssued)
* [`PlaybackController.StopCommandIssued`](#StopCommandIssued)

## Previousディレクティブ {#Previous}
クライアントに、再生キューにある前のオーディオストリームを再生するように指示します。クライアントは、このディレクティブを受信すると、前のオーディオストリームを再生する必要があります。

### Payload fields
なし

### Message example
{% raw %}
```json
{
  "directive": {
    "header": {
      "namespace": "PlaybackController",
      "name": "Previous",
      "dialogRequestId": "42390b12-ae91-4121-aa0a-37f74e8e422b",
      "messageId": "b1f88d7d-bbb8-44fa-a0a2-c5a7553e6f8a"
    },
    "payload": {}
  }
}
```
{% endraw %}

### 次の項目も参照してください。
* [`SpeechRecognizer.Recognize`](/CIC/References/CICInterface/SpeechRecognizer.md#Recognize)


## PreviousCommandIssuedイベント {#PreviousCommandIssued}
ユーザーがクライアント上で「前へ」ボタン(Previous)を押したり、CICから[`PlaybackController.ExpectPreviousCommand`](#ExpectPreviousCommand)ディレクティブを受信した場合、クライアントはこのイベントをCICに送信する必要があります。CICはこのイベントを受信すると、適切なディレクティブをクライアントに送信します。


### Context fields

{% include "/CIC/References/CICInterface/Context_Objects_List.md" %}

### Payload fields

| フィールド名       | データ型    | 説明                     | 必須/任意 |
|---------------|---------|-----------------------------|:---------:|
| `deviceId`    | string  | クライアントデバイスのID。オーディオの再生をリモートでコントロールする状況でない場合、このフィールドは省略します。 | 選択 |

### 備考
* クライアントデバイスのボタンは、ハードウェア方式の物理ボタンの場合もあり、オーディオプレーヤーウィジェットのボタンのようなソフトウェア方式のボタンの場合もあります。

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
      "namespace": "PlaybackController",
      "name": "PreviousCommandIssued",
      "messageId": "4e4080d6-c440-498a-bb73-ae86c6312806"
    },
    "payload": {}
  }
}
```
{% endraw %}

### 次の項目も参照してください。
* [`PlaybackController.CustomCommandIssued`](#CustomCommandIssued)
* [`PlaybackController.ExpectPreviousCommand`](#ExpectNextCommand)
* [`PlaybackController.NextCommandIssued`](#NextCommandIssued)
* [`PlaybackController.PauseCommandIssued`](#PauseCommandIssued)
* [`PlaybackController.PlayCommandIssued`](#PlayCommandIssued)
* [`PlaybackController.ResumeCommandIssued`](#ResumeCommandIssued)
* [`PlaybackController.SetRepeatModeCommandIssued`](#SetRepeatModeCommandIssued)
* [`PlaybackController.StopCommandIssued`](#StopCommandIssued)

## Replayディレクティブ {#Replay}
クライアントに、オーディオストリームを最初から再度再生するように指示します。クライアントはこのディレクティブを受信すると、再生位置をオーディオストリームの最初に移動し、すぐにオーディオストリームの再生を開始する必要があります。もし、オーディオストリームの再生が一時停止していた場合には、オーディオストリームの再生を再開します。

### Payload fields
なし

### Message example
{% raw %}
```json
{
  "directive": {
    "header": {
      "namespace": "PlaybackController",
      "name": "Replay",
      "dialogRequestId": "42390b12-ae91-4121-aa0a-37f74e8e422b",
      "messageId": "b1f88d7d-bbb8-44fa-a0a2-c5a7553e6f8a"
    },
    "payload": {}
  }
}
```
{% endraw %}

### 次の項目も参照してください。
* [`PlaybackController.Pause`](#Pause)
* [`PlaybackController.Resume`](#Resume)
* [`SpeechRecognizer.Recognize`](/CIC/References/CICInterface/SpeechRecognizer.md#Recognize)

## Resumeディレクティブ {#Resume}
クライアントに、オーディオストリームの再生を再開するように指示します。クライアントは、このディレクティブを受信すると、オーディオストリームの再生を再開する必要があります。

### Payload fields
なし

### Message example
{% raw %}
```json
{
  "directive": {
    "header": {
      "namespace": "PlaybackController",
      "name": "Resume",
      "dialogRequestId": "42390b12-ae91-4121-aa0a-37f74e8e422b",
      "messageId": "b1f88d7d-bbb8-44fa-a0a2-c5a7553e6f8a"
    },
    "payload": {}
  }
}
```
{% endraw %}

### 次の項目も参照してください。
* [`AudioPlayer.PlayResumed`](/CIC/References/CICInterface/AudioPlayer.md#PlayResumed)
* [`SpeechRecognizer.Recognize`](/CIC/References/CICInterface/SpeechRecognizer.md#Recognize)

## ResumeCommandIssuedイベント {#ResumeCommandIssued}
ユーザーがクライアント上で「再開」ボタン(Resume)を押したり、CICから[`PlaybackController.ExpectResumeCommand`](#ExpectResumeCommand)ディレクティブを受信した場合、クライアントはこのイベントをCICに送信する必要があります。CICはこのイベントを受信すると、適切なディレクティブをクライアントに送信します。


### Context fields

{% include "/CIC/References/CICInterface/Context_Objects_List.md" %}

### Payload fields

| フィールド名       | データ型    | 説明                     | 必須/任意 |
|---------------|---------|-----------------------------|:---------:|
| `deviceId`    | string  | クライアントデバイスのID。オーディオの再生をリモートでコントロールする状況でない場合、このフィールドは省略します。 | 選択 |

### 備考
* クライアントデバイスのボタンは、ハードウェア方式の物理ボタンの場合もあり、オーディオプレーヤーウィジェットのボタンのようなソフトウェア方式のボタンの場合もあります。

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
      "namespace": "PlaybackController",
      "name": "ResumeCommandIssued",
      "messageId": "4e4080d6-c440-498a-bb73-ae86c6312806"
    },
    "payload": {}
  }
}
```
{% endraw %}

### 次の項目も参照してください。
* [`PlaybackController.CustomCommandIssued`](#CustomCommandIssued)
* [`PlaybackController.ExpectResumeCommand`](#ExpectNextCommand)
* [`PlaybackController.NextCommandIssued`](#NextCommandIssued)
* [`PlaybackController.PauseCommandIssued`](#PauseCommandIssued)
* [`PlaybackController.PlayCommandIssued`](#PlayCommandIssued)
* [`PlaybackController.PreviousCommandIssued`](#PreviousCommandIssued)
* [`PlaybackController.SetRepeatModeCommandIssued`](#SetRepeatModeCommandIssued)
* [`PlaybackController.StopCommandIssued`](#StopCommandIssued)

## SetRepeatModeディレクティブ {#SetRepeatMode}

クライアントに、指定されたリピート再生モードに再生状態を変更するように指示します。クライアントはこのディレクティブを受信すると、リピートモードの状態([コンテキストオブジェクト](/CIC/References/Context_Objects.md))を指定された値に変更し、[`AudioPlayer.PlaybackState`](/CIC/References/Context_Objects.md#PlaybackState)イベントの`repeatMode`フィールドを指定された値に設定して送信する必要があります。

### Payload fields

| フィールド名       | データ型    | 説明                     | 常時/条件付き |
|---------------|---------|-----------------------------|:---------:|
| `repeatMode`  | string  | 選択されたリピートモード<ul><li><code>NONE</code>：リピート再生しない</li><code>REPEAT_ONE</code>：一曲リピート再生</li></ul>  | 常時 |

### Message example
{% raw %}
```json
{
  "directive": {
    "header": {
      "namespace": "PlaybackController",
      "name": "SetRepeatMode",
      "dialogRequestId": "42390b12-ae91-4121-aa0a-37f74e8e422b",
      "messageId": "b1f88d7d-bbb8-44fa-a0a2-c5a7553e6f8a"
    },
    "payload": {
      "repeatMode": "NONE"
    }
  }
}
```
{% endraw %}

### 次の項目も参照してください。
* [`PlaybackController.ExpectNextCommand`](#ExpectNextCommand)
* [`PlaybackController.ExpectPauseCommand`](#ExpectPauseCommand)
* [`PlaybackController.ExpectPreviousCommand`](#ExpectPreviousCommand)
* [`PlaybackController.ExpectResumeCommand`](#ExpectResumeCommand)
* [`PlaybackController.ExpectStopCommand`](#ExpectStopCommand)
* [`PlaybackController.PlayCommandIssued`](#PlayCommandIssued)

## SetRepeatModeCommandIssuedイベント {#SetRepeatModeCommandIssued}
ユーザーがクライアント上で「リピート再生」ボタン(Repeat)を押した場合、クライアントはこのイベントをCICに送信する必要があります。CICはこのイベントを受信すると、[`PlaybackController.SetRepeatMode`](#SetRepeatMode)ディレクティブを対象のクライアントに送信します。


### Context fields

{% include "/CIC/References/CICInterface/Context_Objects_List.md" %}

### Payload fields

| フィールド名       | データ型    | 説明                     | 必須/任意 |
|---------------|---------|-----------------------------|:---------:|
| `deviceId`    | string  | クライアントデバイスのID。オーディオの再生をリモートでコントロールする状況でない場合、このフィールドは省略します。                               | 選択 |
| `repeatMode`  | string  | 選択されたリピートモード<ul><li><code>NONE</code>：リピート再生しない</li><code>REPEAT_ONE</code>：一曲リピート再生</li></ul>  | 必須 |

### 備考
* クライアントデバイスのボタンは、ハードウェア方式の物理ボタンの場合もあり、オーディオプレーヤーウィジェットのボタンのようなソフトウェア方式のボタンの場合もあります。

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
      "namespace": "PlaybackController",
      "name": "SetRepeatModeCommandIssued",
      "messageId": "4e4080d6-c440-498a-bb73-ae86c6312806"
    },
    "payload": {
      "repeatMode": "NONE"
    }
  }
}
```
{% endraw %}

### 次の項目も参照してください。
* [`PlaybackController.CustomCommandIssued`](#CustomCommandIssued)
* [`PlaybackController.SetRepeatMode`](#SetRepeatMode)
* [`PlaybackController.NextCommandIssued`](#NextCommandIssued)
* [`PlaybackController.PauseCommandIssued`](#PauseCommandIssued)
* [`PlaybackController.PlayCommandIssued`](#PlayCommandIssued)
* [`PlaybackController.PreviousCommandIssued`](#PreviousCommandIssued)
* [`PlaybackController.ResumeCommandIssued`](#ResumeCommandIssued)
* [`PlaybackController.StopCommandIssued`](#StopCommandIssued)

## Stopディレクティブ {#Stop}
クライアントに、オーディオストリームの再生を停止するように指示します。クライアントは、このディレクティブを受信すると、オーディオストリームの再生を停止する必要があります。

### Payload fields
なし

### Message example
{% raw %}
```json
{
  "directive": {
    "header": {
      "namespace": "PlaybackController",
      "name": "Stop",
      "dialogRequestId": "42390b12-ae91-4121-aa0a-37f74e8e422b",
      "messageId": "b1f88d7d-bbb8-44fa-a0a2-c5a7553e6f8a"
    },
    "payload": {}
  }
}
```
{% endraw %}

### 次の項目も参照してください。
* [`AudioPlayer.PlayStopped`](/CIC/References/CICInterface/AudioPlayer.md#PlayStopped)
* [`SpeechRecognizer.Recognize`](/CIC/References/CICInterface/SpeechRecognizer.md#Recognize)

## StopCommandIssuedイベント {#StopCommandIssued}
ユーザーがクライアント上で「再開」ボタン(Resume)を押したり、CICから[`PlaybackController.ExpectStopCommand`](#ExpectStopCommand)ディレクティブを受信した場合、クライアントはこのイベントをCICに送信する必要があります。CICはこのイベントを受信すると、適切なディレクティブをクライアントに送信します。


### Context fields

{% include "/CIC/References/CICInterface/Context_Objects_List.md" %}

### Payload fields

| フィールド名       | データ型    | 説明                     | 必須/任意 |
|---------------|---------|-----------------------------|:---------:|
| `deviceId`    | string  | クライアントデバイスのID。オーディオの再生をリモートでコントロールする状況でない場合、このフィールドは省略します。 | 選択 |

### 備考
* クライアントデバイスのボタンは、ハードウェア方式の物理ボタンの場合もあり、オーディオプレーヤーウィジェットのボタンのようなソフトウェア方式のボタンの場合もあります。

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
      "namespace": "PlaybackController",
      "name": "StopCommandIssued",
      "messageId": "4e4080d6-c440-498a-bb73-ae86c6312806"
    },
    "payload": {}
  }
}
```
{% endraw %}

### 次の項目も参照してください。
* [`PlaybackController.CustomCommandIssued`](#CustomCommandIssued)
* [`PlaybackController.ExpectResumeCommand`](#ExpectNextCommand)
* [`PlaybackController.NextCommandIssued`](#NextCommandIssued)
* [`PlaybackController.PauseCommandIssued`](#PauseCommandIssued)
* [`PlaybackController.PlayCommandIssued`](#PlayCommandIssued)
* [`PlaybackController.PreviousCommandIssued`](#PreviousCommandIssued)
* [`PlaybackController.ResumeCommandIssued`](#ResumeCommandIssued)
* [`PlaybackController.SetRepeatModeCommandIssued`](#SetRepeatModeCommandIssued)

## TurnOffRepeatModeディレクティブ {#TurnOffRepeatMode}
**(非推奨)** クライアントに、1曲リピート再生モードを無効にするように指示します。

### Payload fields
なし

### Message example
{% raw %}
```json
{
  "directive": {
    "header": {
      "namespace": "PlaybackController",
      "name": "TurnOffRepeatMode",
      "dialogRequestId": "42390b12-ae91-4121-aa0a-37f74e8e422b",
      "messageId": "b1f88d7d-bbb8-44fa-a0a2-c5a7553e6f8a"
    },
    "payload": {}
  }
}
```
{% endraw %}

### 次の項目も参照してください。
* [`SpeechRecognizer.Recognize`](/CIC/References/CICInterface/SpeechRecognizer.md#Recognize)

## TurnOnRepeatModeディレクティブ {#TurnOnRepeatMode}
**(非推奨)** クライアントに、1曲リピート再生モードを有効にするように指示します。クライアントは、このディレクティブを受信すると、現在再生しているオーディオストリームをリピート再生する必要があります。

### Payload fields
なし

### Message example
{% raw %}
```json
{
  "directive": {
    "header": {
      "namespace": "PlaybackController",
      "name": "TurnOnRepeatMode",
      "dialogRequestId": "42390b12-ae91-4121-aa0a-37f74e8e422b",
      "messageId": "b1f88d7d-bbb8-44fa-a0a2-c5a7553e6f8a"
    },
    "payload": {}
  }
}
```
{% endraw %}

### 次の項目も参照してください。
* [`SpeechRecognizer.Recognize`](/CIC/References/CICInterface/SpeechRecognizer.md#Recognize)

## Unmuteディレクティブ {#Unmute}
クライアントに、オーディオプレーヤーのミュートを解除するように指示します。クライアントはこのディレクティブを受信すると、スピーカーのミュートを解除して、元の音量に戻す必要があります。

### Payload fields
なし

### 備考

Clovaは、スピーカーの出力に関連するコントロールの場合、通知のためのオーディオファイルを[`SpeechSynthesizer.Speak`](/CIC/References/CICInterface/SpeechSynthesizer.md#Speak)ディレクティブに添付しません。それは、ユーザーの音楽鑑賞などのUXを向上させるためで、その場合には音声案内の代わりに、クライアントデバイスのライトや、短い効果音などで音量が調節されたことをユーザーに通知する必要があります。

### Message example
{% raw %}
```json
{
  "directive": {
    "header": {
      "namespace": "PlaybackController",
      "name": "Unmute",
      "dialogRequestId": "42390b12-ae91-4121-aa0a-37f74e8e422b",
      "messageId": "b1f88d7d-bbb8-44fa-a0a2-c5a7553e6f8a"
    },
    "payload": {}
  }
}
```
{% endraw %}

### 次の項目も参照してください。
* [`SpeechRecognizer.Recognize`](/CIC/References/CICInterface/SpeechRecognizer.md#Recognize)

## VolumeDownディレクティブ {#VolumeDown}
クライアントに、オーディオプレーヤーの音量を下げるように指示します。クライアントはこのディレクティブを受信すると、オーディオストリームの再生に関連するスピーカーの音量を下げる必要があります。下げる量は、クライアントのUX基準に従います。

<div class="note">
  <p><strong>メモ</strong></p>
  <p><code>PlaybackController.VolumeDown</code>ディレクティブは、今後サポートされない予定です。このディレクティブの代わりに、<a href="/CIC/References/CICInterface/DeviceControl.md#Decrease"><code>DiviceControl.Decrease</code></a>ディレクティブを使用することを推奨します。</p>
</div>

### Payload fields
なし

### Message example
{% raw %}
```json
{
  "directive": {
    "header": {
      "namespace": "PlaybackController",
      "name": "VolumeDown",
      "dialogRequestId": "42390b12-ae91-4121-aa0a-37f74e8e422b",
      "messageId": "b1f88d7d-bbb8-44fa-a0a2-c5a7553e6f8a"
    },
    "payload": {}
  }
}
```
{% endraw %}

### 次の項目も参照してください。
* [`SpeechRecognizer.Recognize`](/CIC/References/CICInterface/SpeechRecognizer.md#Recognize)

## VolumeUpディレクティブ {#VolumeUp}

クライアントに、オーディオプレーヤーの音量を上げるように指示します。クライアントはこのディレクティブを受信すると、オーディオストリームの再生に関連するスピーカーの音量を上げる必要があります。上げる量は、クライアントのUX基準に従います。

<div class="note">
  <p><strong>メモ</strong></p>
  <p><code>PlaybackController.VolumeUp</code>ディレクティブは、今後サポートされない予定です。このディレクティブの代わりに、<a href="/CIC/References/CICInterface/DeviceControl.md#Increase"><code>DiviceControl.Increase</code></a>ディレクティブを使用することを推奨します。</p>
</div>

### Payload fields
なし

### Message example
{% raw %}
```json
{
  "directive": {
    "header": {
      "namespace": "PlaybackController",
      "name": "VolumeUp",
      "dialogRequestId": "42390b12-ae91-4121-aa0a-37f74e8e422b",
      "messageId": "b1f88d7d-bbb8-44fa-a0a2-c5a7553e6f8a"
    },
    "payload": {}
  }
}
```
{% endraw %}

### 次の項目も参照してください。
* [`SpeechRecognizer.Recognize`](/CIC/References/CICInterface/SpeechRecognizer.md#Recognize)
