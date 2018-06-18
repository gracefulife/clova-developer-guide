# ディレクティブの索引

| 名前欄          | メッセージ       | 説明                                             |
|--------------------|----------------|-------------------------------------------------|
| Alerts             | [`DeleteAlert`](/CIC/References/CICInterface/Alerts.md#DeleteAlert)             | クライアントに対して、特定のアラームを削除するように指示します。 |
| Alerts             | [`SetAlert`](/CIC/References/CICInterface/Alerts.md#SetAlert)                   | クライアントに対して、アラームを追加するか、または特定のアラームを編集するように指示します。 |
| Alerts             | [`StopAlert`](/CIC/References/CICInterface/Alerts.md#StopAlert)                 | クライアントに対して、特定のアラームを停止するように指示します。  |
| Alerts             | [`SynchronizeAlert`](/CIC/References/CICInterface/Alerts.md#SynchronizeAlert)   | クライアントに対して、`payload`内にあるユーザーのアラームデータを同期するように指示します。  |
| AudioPlayer        | [`ClearQueue`](/CIC/References/CICInterface/AudioPlayer.md#ClearQueue)          | クライアントに対して、オーディオストリームの再生キューをクリアするように指示します。                              |
| AudioPlayer        | [`ExpectReportPlaybackState`](/CIC/References/CICInterface/AudioPlayer.md#ExpectReportPlaybackState) | クライアントに対して、現在の再生状態をレポートするように指示します。クライアントはこのディレクティブを受信すると、[`AudioPlayer.ReportPlaybackState`](/CIC/References/CICInterface/AudioPlayer.md#ReportPlaybackState)イベントをCICに送信する必要があります。 |
| AudioPlayer        | [`Play`](/CIC/References/CICInterface/AudioPlayer.md#Play)                      | クライアントに対して、特定のオーディオストリームを再生するか、または再生キューに追加するように指示します。                          |
| AudioPlayer        | [`StreamDeliver`](/CIC/References/CICInterface/AudioPlayer.md#StreamDeliver)    | [`AudioPlayer.StreamRequested`](/CIC/References/CICInterface/AudioPlayer.md#StreamRequested)イベントに対する応答です。実際に再生できるオーディオストリームの情報を受信するために使用します。 |
{% if book.TargetReaderType == "Internal" %}|AudioPlayer        | [`SynchronizePlaybackState`](/CIC/References/CICInterface/AudioPlayer.md#SynchronizePlaybackState) | クライアントのストリーム再生状態を同期するように指示します。[`AudioPlayer.RequestPlaybackState`](#/CIC/References/CICInterface/AudioPlayer.md#RequestPlaybackState)イベントを送信したクライアントは、`AudioPlayer.SynchronizePlaybackState`ディレクティブを受信します。 |
| Clova              | [`ExpectLogin`](/CIC/References/CICInterface/Clova.md#ExpectLogin)              | クライアントに対して、ユーザーの{{ book.OrientedService }}アカウント認証(ログイン)を行うように指示します。          |{% else %}|Clova              | [`ExpectLogin`](/CIC/References/CICInterface/Clova.md#ExpectLogin)              | クライアントに対して、ユーザーの{{ book.OrientedService }}アカウント認証(ログイン)を行うように指示します。          |{% endif %}
| Clova              | [`FinishExtension`](/CIC/References/CICInterface/Clova.md#FinishExtension)      | クライアントに対して、特定のExtensionを終了するように指示します。                                             |
| Clova              | [`HandleDelegatedEvent`](/CIC/References/CICInterface/Clova.md#HandleDelegatedEvent) | クライアントに対して、Clovaアプリから[委任されたユーザーのリクエストを処理する](/CIC/Guides/Interact_with_CIC.md#HandleDelegation)ように指示します。   |
| Clova              | [`Hello`](/CIC/References/CICInterface/Clova.md#Hello)                          | クライアントに対して、ダウンチャネルが確立したことを通知します。                                       |
| Clova              | [`Help`](/CIC/References/CICInterface/Clova.md#Help)                            | クライアントに対して、あらかじめ用意されたヘルプを提供するように指示します。                                       |
| Clova              | [`LaunchURI`](/CIC/References/CICInterface/Clova.md#LaunchURI)     | クライアントに、URIで表現されるウェブサイトまたはアプリを開いたり、起動するように指示します。       |
| Clova              | [`RenderTemplate`](/CIC/References/CICInterface/Clova.md#RenderTemplate)        | クライアントに対して、テンプレートを表示するように指示します。                                                     |
| Clova              | [`RenderText`](/CIC/References/CICInterface/Clova.md#RenderText)                | クライアントに対して、テキストを表示するように指示します。                                                     |
| Clova              | [`StartExtension`](/CIC/References/CICInterface/Clova.md#StartExtension)        | クライアントに対して、特定のExtensionを起動するように指示します。                                             |
| DeviceControl      | [`BtConnect`](/CIC/References/CICInterface/DeviceControl.md#BtConnect)          | クライアントに、特定のBluetoothデバイスと接続するように指示します。                                       |
| DeviceControl      | [`BtConnectByPINCode`](/CIC/References/CICInterface/DeviceControl.md#BtConnectByPINCode) | クライアントに、PINコードを要求したBluetoothデバイスと接続するように指示します。                      |
| DeviceControl      | [`BtDisconnect`](/CIC/References/CICInterface/DeviceControl.md#BtDisconnect)    | クライアントに、特定のBluetoothデバイスとの接続を解除するように指示します。                                       |
| DeviceControl      | [`BtStartPairing`](/CIC/References/CICInterface/DeviceControl.md#BtStartPairing) | クライアントに、Bluetoothペアリングを開始するように指示します。                                              |
| DeviceControl      | [`BtStopPairing`](/CIC/References/CICInterface/DeviceControl.md#BtStopPairing)   | クライアントに、Bluetoothペアリングを解除するように指示します。                                              |
| DeviceControl      | [`Decrease`](/CIC/References/CICInterface/DeviceControl.md#Decrease)             | クライアントに、スピーカーの音量または画面の明るさを、基本値だけ下げるように指示します。                            |
| DeviceControl      | [`ExpectReportState`](/CIC/References/CICInterface/DeviceControl.md#ExpectReportState) | クライアントに、デバイスの現在の状態をCICにレポートするように指示します。                                  |
| DeviceControl      | [`Increase`](/CIC/References/CICInterface/DeviceControl.md#Increase)             | クライアントに、スピーカーの音量または画面の明るさを、基本値だけ上げるように指示します。                            |
| DeviceControl      | [`LaunchApp`](/CIC/References/CICInterface/DeviceControl.md#LaunchApp)           | **(Deprecated)** クライアントに、特定のアプリを起動するように指示します。                                                    |
| DeviceControl      | [`Open`](/CIC/References/CICInterface/DeviceControl.md#Open)                     | クライアントに、特定の画面を表示するように指示します。  |
| DeviceControl      | [`OpenScreen`](/CIC/References/CICInterface/DeviceControl.md#OpenScreen)         | **(Deprecated)** クライアントに、設定画面を開くように指示します。                                                     |
| DeviceControl      | [`SetValue`](/CIC/References/CICInterface/DeviceControl.md#SetValue)            | クライアントに、スピーカーの音量または画面の明るさを、指定された値に設定するように指示します。                           |
| DeviceControl      | [`SynchronizeState`](/CIC/References/CICInterface/DeviceControl.md#SynchronizeState) | クライアントに、ユーザーのアカウントに登録されている他のクライアントデバイスの状態を更新するように指示します。           |
| DeviceControl      | [`TurnOff`](/CIC/References/CICInterface/DeviceControl.md#TurnOff)               | クライアントに、指定された機能やモードをオフにしたり、または無効にするように指示します。                                  |
| DeviceControl      | [`TurnOn`](/CIC/References/CICInterface/DeviceControl.md#TurnOn)                 | クライアントに、指定された機能をオンにしたり、有効にしたりするように指示します。                                          |
| Notifier           | [`ClearIndicator`](/CIC/References/CICInterface/Notifier.md#ClearIndicator)      | クライアントに、通知インジケーターをすべてクリアするように指示します。                                         |
| Notifier           | [`Notify`](/CIC/References/CICInterface/Notifier.md#Notify)                      | クライアントに、通知の内容をユーザーに伝えるように指示します。                                          |
| Notifier           | [`SetIndicator`](/CIC/References/CICInterface/Notifier.md#SetIndicator)          | クライアントに、未読の通知があることを表示するように指示します。                                  |
| PlaybackController | [`ExpectNextCommand`](/CIC/References/CICInterface/PlaybackController.md#ExpectNextCommand)         | ユーザーがクライアント上で「次」ボタン(Next)を押して、その効果が発生したときのように、クライアントが[`PlaybackController.NextCommandIssued`](/CIC/References/CICInterface/PlaybackController.md#NextCommandIssued)イベントをCICに送信するように指示します。  |
| PlaybackController | [`ExpectPauseCommand`](/CIC/References/CICInterface/PlaybackController.md#ExpectPauseCommand)       | ユーザーがクライアント上で「一時停止」ボタン(Pause)を押して、その効果が発生したときのように、クライアントが[`PlaybackController.PauseCommandIssued`](/CIC/References/CICInterface/PlaybackController.md#PauseCommandIssued)イベントをCICに送信するように指示します。  |
| PlaybackController | [`ExpectPlayCommand`](/CIC/References/CICInterface/PlaybackController.md#ExpectPlayCommand)         | ユーザーがクライアント上で「再生」ボタン(Play)を押して、その効果が発生したときのように、クライアントが[`PlaybackController.PlayCommandIssued`](/CIC/References/CICInterface/PlaybackController.md#PlayCommandIssued)イベントをCICに送信するように指示します。  |
| PlaybackController | [`ExpectPreviousCommand`](/CIC/References/CICInterface/PlaybackController.md#ExpectPreviousCommand) | ユーザーがクライアント上で「前」ボタン(Previous)を押して、その効果が発生したときのように、クライアントが[`PlaybackController.PreviousCommandIssued`](/CIC/References/CICInterface/PlaybackController.md#PreviousCommandIssued)イベントをCICに送信するように指示します。  |
| PlaybackController | [`ExpectResumeCommand`](/CIC/References/CICInterface/PlaybackController.md#ExpectResumeCommand)     | ユーザーがクライアント上で「再開」ボタン(Resume)を押して、その効果が発生したときのように、クライアントが[`PlaybackController.ResumeCommandIssued`](/CIC/References/CICInterface/PlaybackController.md#ResumeCommandIssued)イベントをCICに送信するように指示します。  |
| PlaybackController | [`ExpectStopCommand`](/CIC/References/CICInterface/PlaybackController.md#ExpectStopCommand)         | ユーザーがクライアント上で「停止」ボタン(Stop)を押して、その効果が発生したときのように、クライアントが[`PlaybackController.StopCommandIssued`](/CIC/References/CICInterface/PlaybackController.md#StopCommandIssued)イベントをCICに送信するように指示します。  |
| PlaybackController | [`Mute`](/CIC/References/CICInterface/PlaybackController.md#Mute)               | クライアントに、スピーカーをミュートにするように指示します。                                                |
| PlaybackController | [`Next`](/CIC/References/CICInterface/PlaybackController.md#Next)               | クライアントに、再生キューに入っている次のオーディオストリームを再生するように指示します。                               |
| PlaybackController | [`Pause`](/CIC/References/CICInterface/PlaybackController.md#Pause)             | クライアントに、再生中のオーディオストリームを一時停止するように指示します。                                    |
| PlaybackController | [`Previous`](/CIC/References/CICInterface/PlaybackController.md#Previous)       | クライアントに、再生キューにある前のオーディオストリームを再生するように指示します。                              |
| PlaybackController | [`Replay`](/CIC/References/CICInterface/PlaybackController.md#Replay)           | クライアントに、オーディオストリームを最初から再度再生するように指示します。                                     |
| PlaybackController | [`Resume`](/CIC/References/CICInterface/PlaybackController.md#Resume)           | クライアントに、オーディオストリームの再生を再開するように指示します。                                            |
| PlaybackController | [`SetRepeatMode`](/CIC/References/CICInterface/PlaybackController.md#SetRepeatMode) | クライアントに、指定されたリピート再生モードに再生状態を変更するように指示します。                                |
| PlaybackController | [`Stop`](/CIC/References/CICInterface/PlaybackController.md#Stop)               | クライアントに、オーディオストリームの再生を停止するように指示します。                                            |
| PlaybackController | [`TurnOffRepeatMode`](/CIC/References/CICInterface/PlaybackController.md#TurnOffRepeatMode) | **(非推奨)** クライアントに、1曲リピート再生モードを無効にするように指示します。                |
| PlaybackController | [`TurnOnRepeatMode`](/CIC/References/CICInterface/PlaybackController.md#TurnOnRepeatMode) | **(非推奨)** クライアントに、1曲リピート再生モードを有効にするように指示します。                  |
| PlaybackController | [`Unmute`](/CIC/References/CICInterface/PlaybackController.md#Unmute)           | クライアントに、スピーカーのミュートを解除するように指示します。                                           |
| PlaybackController | [`VolumeDown`](/CIC/References/CICInterface/PlaybackController.md#VolumeDown)   | クライアントに、スピーカーの音量を下げるように指示します。                                                   |
| PlaybackController | [`VolumeUp`](/CIC/References/CICInterface/PlaybackController.md#VolumeUp)       | クライアントに、スピーカーの音量を上げるように指示します。                                                   |
| SpeechRecognizer   | [`ExpectSpeech`](/CIC/References/CICInterface/SpeechRecognizer.md#ExpectSpeech) | クライアントに、ユーザーの音声の取得を待機するように指示します。                                            |
| SpeechRecognizer   | [`KeepRecording`](/CIC/References/CICInterface/SpeechRecognizer.md#KeepRecording) | クライアントに、ユーザーの音声の取得を続けるように指示します。                                                |
{% if book.TargetReaderType == "Internal" or book.TargetReaderType == "Uplus" %}|SpeechRecognizer   | [`ShowRecognizedText`](/CIC/References/CICInterface/SpeechRecognizer.md#ShowRecognizedText) | クライアントに、認識されたユーザーの音声をリアルタイムで送信します。                                |
| SpeechRecognizer   | [`StopCapture`](/CIC/References/CICInterface/SpeechRecognizer.md#StopCapture)   | クライアントに、ユーザーの音声の認識を停止するように指示します。                                            |{% else %}|SpeechRecognizer   | [`StopCapture`](/CIC/References/CICInterface/SpeechRecognizer.md#StopCapture)   | クライアントに、ユーザーの音声の認識を停止するように指示します。                                            |{% endif %}
| SpeechSynthesizer  | [`Speak`](/CIC/References/CICInterface/SpeechSynthesizer.md#Speak)                 | クライアントに、合成された音声をスピーカーで出力するように指示します。                                |
| System             | [`SynchronizeState`](/CIC/References/CICInterface/System.md#SynchronizeState) | クライアントに、`payload`のデータを同期するように指示します。                                   |
| TemplateRuntime    | [`ExpectRequestPlayerInfo`](/CIC/References/CICInterface/TemplateRuntime.md#ExpectRequestPlayerInfo)  | クライアントに、再生メタデータをリクエストするように指示します。クライアントはこのディレクティブを受信すると、[`TemplateRuntime.RequestPlayerInfo`](#RequestPlayerInfo)イベントをCICに送信する必要があります。 |
| TemplateRuntime    | [`RenderPlayerInfo`](/CIC/References/CICInterface/TemplateRuntime.md#RenderPlayerInfo)                | CICから、メディアプレーヤーに表示する再生リスト、アルバムの画像、歌詞のような再生メタデータをクライアントに送信し、表示するように指示します。 |
