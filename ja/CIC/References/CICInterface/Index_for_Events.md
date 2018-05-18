# イベントの索引

| 名前欄         | メッセージ       | 説明                                             |
|-------------------|----------------|-------------------------------------------------|
| Alerts            | [`AlertStarted`](/CIC/References/CICInterface/Alerts.md#AlertStarted)                 | クライアントから、アラームが開始したことをCICにレポートします。 |
| Alerts            | [`AlertStopped`](/CIC/References/CICInterface/Alerts.md#AlertStopped)                 | クライアントから、アラームが停止したことをCICにレポートします。 |
| Alerts            | [`DeleteAlertFailed`](/CIC/References/CICInterface/Alerts.md#DeleteAlertFailed)       | クライアントから、クライアントに設定されている特定のアラームを削除できなかったことをCICにレポートします。 |
| Alerts            | [`DeleteAlertSucceeded`](/CIC/References/CICInterface/Alerts.md#DeleteAlertSucceeded) | クライアントから、クライアントに設定されている特定のアラームを正常に削除したことをCICにレポートします。 |
| Alerts            | [`RequestAlertStop`](/CIC/References/CICInterface/Alerts.md#RequestAlertStop)         | クライアントから、アクティブなアラームを停止するようにCICにリクエストします。  |
| Alerts            | [`RequestSynchronizeAlert`](/CIC/References/CICInterface/Alerts.md#RequestSynchronizeAlert) | クライアントから、Clovaのクラウドに保存されたユーザーのアラームデータを同期する必要がある場合、CICにこのイベントを送信します。 |
| Alerts            | [`SetAlertFailed`](/CIC/References/CICInterface/Alerts.md#SetAlertFailed)             | クライアントから、特定のアラームを追加または編集できなかったことをCICにレポートします。 |
| Alerts            | [`SetAlertSucceeded`](/CIC/References/CICInterface/Alerts.md#SetAlertSucceeded)       | クライアントから、特定のアラームを正常に追加または編集したことをCICにレポートします。 |
| AudioPlayer       | [`PlayFinished`](/CIC/References/CICInterface/AudioPlayer.md#PlayFinished) | クライアントがオーディオストリームの再生を終了するとき、そのオーディオストリームの情報をCICにレポートするために使用します。
        |
| AudioPlayer       | [`PlayPaused`](/CIC/References/CICInterface/AudioPlayer.md#PlayPaused)     | クライアントがオーディオストリームの再生を一時停止するとき、そのオーディオストリームの情報をCICにレポートするために使用します。
    |
| AudioPlayer       | [`PlayResumed`](/CIC/References/CICInterface/AudioPlayer.md#PlayResumed)   | クライアントがオーディオストリームの再生を再開するとき、そのオーディオストリームの情報をCICにレポートするために使用します。            |
| AudioPlayer       | [`PlayStarted`](/CIC/References/CICInterface/AudioPlayer.md#PlayStarted)   | クライアントがオーディオストリームの再生を開始するとき、そのオーディオストリームの情報をCICにレポートするために使用します。
       |
| AudioPlayer       | [`PlayStopped`](/CIC/References/CICInterface/AudioPlayer.md#PlayStopped)   | クライアントがオーディオストリームの再生を停止するとき、そのオーディオストリームの情報をCICにレポートするために使用します。       |
| AudioPlayer       | [`ProgressReportDelayPassed`](/CIC/References/CICInterface/AudioPlayer.md#ProgressReportPositionPassed) | オーディオストリームの再生が開始してから、指定された遅延期間が経過したときの再生状態([`AudioPlayer.PlaybackState`](/CIC/References/Context_Objects.md#PlaybackState))をCICにレポートします。オーディオストリームの遅延期間は、[`AudioPlayer.Play`](/CIC/References/CICInterface/AudioPlayer.md#Play)ディレクティブがクライアントに送信されるときに確認できます。 |
| AudioPlayer       | [`ProgressReportIntervalPassed`](/CIC/References/CICInterface/AudioPlayer.md#ProgressReportPositionPassed)| オーディオストリームの再生が開始してから、指定された間隔ごとの再生状態([`AudioPlayer.PlaybackState`](/CIC/References/Context_Objects.md#PlaybackState))を、CICにレポートします。レポートする間隔は、[`AudioPlayer.Play`](/CIC/References/CICInterface/AudioPlayer.md#Play)ディレクティブがクライアントに送信されるときに確認できます。|
| AudioPlayer       | [`ProgressReportPositionPassed`](/CIC/References/CICInterface/AudioPlayer.md#ProgressReportPositionPassed) | オーディオストリームの再生が開始してから、指定されたタイミングに、そのときの再生状態([`AudioPlayer.PlaybackState`](/CIC/References/Context_Objects.md#PlaybackState))をCICにレポートします。レポートするタイミングは、[`AudioPlayer.Play`](/CIC/References/CICInterface/AudioPlayer.md#Play)ディレクティブがクライアントに送信されるときに確認できます。|
| AudioPlayer       | [`ReportPlaybackState`](/CIC/References/CICInterface/AudioPlayer.md#ReportPlaybackState) | クライアントから、現在のストリーム再生状態をCICにレポートします。クライアントがCICから[`ExpectReportPlaybackState`](/CIC/References/CICInterface/AudioPlayer.md#ExpectReportPlaybackState)ディレクティブを受信した場合、`AudioPlayer.ReportPlaybackState`イベントをCICに送信する必要があります。  |
{% if book.TargetReaderType == "Internal" %}|AudioPlayer       | [`RequestPlaybackState`](/CIC/References/CICInterface/AudioPlayer.md#RequestPlaybackState) | クライアントのストリーム再生状態をCICにリクエストします。CICは、`AudioPlayer.ReqeustPlaybackState`イベントを受信した場合、ユーザーアカウントに登録されているすべての、または特定のクライアントに[`AudioPlayer.ExpectReportPlaybackState`](/CIC/References/CICInterface/AudioPlayer.md#ExpectReportPlaybackState)ディレクティブを送信します。  |
| AudioPlayer       | [`StreamRequested`](/CIC/References/CICInterface/AudioPlayer.md#StreamRequested) | オーディオストリームを再生するために、ストリーミングのURLなど、追加の情報をCICにリクエストするイベントです。|{% else %}|AudioPlayer       | [`StreamRequested`](/CIC/References/CICInterface/AudioPlayer.md#StreamRequested) | オーディオストリームを再生するために、ストリーミングのURLなど、追加の情報をCICにリクエストするイベントです。|{% endif %}
| Clova              | [`ProcessDelegatedEvent`](/CIC/References/CICInterface/Clova.md#ProcessDelegatedEvent)                          | クライアントが、[委任されたユーザーのリクエスト](/CIC/Guides/Interact_with_CIC.md#HandleDelegation)に対する結果をCICから受信するために使用します。  |
| DeviceControl     | [`ActionExecuted`](/CIC/References/CICInterface/DeviceControl.md#ActionExecuted) | クライアントから、デバイスを正常にコントロールしたことをレポートします。                               |
| DeviceControl     | [`ActionFailed`](/CIC/References/CICInterface/DeviceControl.md#ActionFailed) | クライアントから、デバイスをコントロールできないか、またはコントロールに失敗したことをレポートします。                   |
| DeviceControl     | [`BtRequestForPINCode`](/CIC/References/CICInterface/DeviceControl.md#BtRequestForPINCode) | クライアントは、BluetoothデバイスからPINコードを要求される場合、このイベントでCICにリクエストを送信する必要があります。       |
| DeviceControl     | [`BtRequestToCancelPinCodeInput`](/CIC/References/CICInterface/DeviceControl.md#BtRequestToCancelPinCodeInput) | クライアントは、CICに対してPINコード入力の要求をキャンセルする場合、このイベントを送信する必要があります。 |
| DeviceControl     | [`ReportState`](/CIC/References/CICInterface/DeviceControl.md#ReportState)   | クライアントは、デバイスの現在の状態をレポートするとき、このメッセージを使用する必要があります。                              |
| DeviceControl     | [`RequestStateSynchronization`](/CIC/References/CICInterface/DeviceControl.md#RequestStateSynchronization) | ユーザーのアカウントに登録されている他のクライアントデバイスの現在の状態を確認しようとするとき、このイベントをCICに送信します。  |
| PlaybackController | [`CustomCommandIssued`](/CIC/References/CICInterface/PlaybackController.md#CustomCommandIssued)               | ユーザーがクライアント上で任意の機能を設定したボタンを押したり、タップした場合、クライアントはこのイベントをCICに送信する必要があります。  |
| PlaybackController | [`NextCommandIssued`](/CIC/References/CICInterface/PlaybackController.md#NextCommandIssued)                   | ユーザーがクライアント上で「次」ボタン(Next)を押したり、CICから[`PlaybackController.ExpectNextCommand`](/CIC/References/CICInterface/PlaybackController.md#ExpectNextCommand)ディレクティブを受信した場合、クライアントはこのイベントをCICに送信する必要があります。 |
| PlaybackController | [`PauseCommandIssued`](/CIC/References/CICInterface/PlaybackController.md#PauseCommandIssued)                 | ユーザーがクライアント上で「一時停止」ボタン(Pause)を押したり、CICから[`PlaybackController.ExpectPauseCommand`](/CIC/References/CICInterface/PlaybackController.md#ExpectPauseCommand)ディレクティブを受信した場合、クライアントはこのイベントをCICに送信する必要があります。  |
| PlaybackController | [`PlayCommandIssued`](/CIC/References/CICInterface/PlaybackController.md#PlayCommandIssued)                   | ユーザーがクライアント上で「再生」ボタン(Play)を押したり、CICから[`PlaybackController.ExpectPlayCommand`](/CIC/References/CICInterface/PlaybackController.md#ExpectPlayCommand)ディレクティブを受信した場合、クライアントはこのイベントをCICに送信する必要があります。  |
| PlaybackController | [`PreviousCommandIssued`](/CIC/References/CICInterface/PlaybackController.md#PreviousCommandIssued)           | ユーザーがクライアント上で「前へ」ボタン(Previous)を押したり、CICから[`PlaybackController.ExpectPreviousCommand`](/CIC/References/CICInterface/PlaybackController.md#ExpectPreviousCommand)ディレクティブを受信した場合、クライアントはこのイベントをCICに送信する必要があります。 |
| PlaybackController | [`ResumeCommandIssued`](/CIC/References/CICInterface/PlaybackController.md#ResumeCommandIssued)               | ユーザーがクライアント上で「再開」ボタン(Resume)を押したり、CICから[`PlaybackController.ExpectResumeCommand`](/CIC/References/CICInterface/PlaybackController.md#ExpectResumeCommand)ディレクティブを受信した場合、クライアントはこのイベントをCICに送信する必要があります。  |
| PlaybackController | [`SetRepeatModeCommandIssued`](/CIC/References/CICInterface/PlaybackController.md#SetRepeatModeCommandIssued) | ユーザーがクライアント上で「リピート再生」ボタン(Repeat)を押した場合、クライアントはこのイベントをCICに送信する必要があります。  |
| PlaybackController | [`StopCommandIssued`](/CIC/References/CICInterface/PlaybackController.md#StopCommandIssued)                   | ユーザーがクライアント上で「リピート再生」ボタン(Repeat)を押した場合、クライアントはこのイベントをCICに送信する必要があります。  |
| SpeechRecognizer  | [`Recognize`](/CIC/References/CICInterface/SpeechRecognizer.md#Recognize)  | 取得されるユーザーの音声を送信して、その音声を認識するようにCICにリクエストします。                                          |
| SpeechSynthesizer | [`Request`](/CIC/References/CICInterface/SpeechSynthesizer.md#Request)     | CICに、特定のテキストを音声に合成するようにリクエストします。                                             |
| SpeechSynthesizer | [`SpeechFinished`](/CIC/References/CICInterface/SpeechSynthesizer.md#SpeechFinished)   | クライアントから、合成音声の再生を完了したことをCICにレポートします。                                 |
| SpeechSynthesizer | [`SpeechStarted`](/CIC/References/CICInterface/SpeechSynthesizer.md#SpeechStarted)     | クライアントから、合成音声の再生を開始したことをCICにレポートします。                                 |
| SpeechSynthesizer | [`SpeechStopped`](/CIC/References/CICInterface/SpeechSynthesizer.md#SpeechStopped)     | クライアントから、合成音声の再生を停止したことをCICにレポートします。                                 |
| System          | [`RequestSynchronizeState`](/CIC/References/CICInterface/System.md#RequestSynchronizeState) | クライアントから、Clovaのクラウドに保存された共有データを同期する必要がある場合、CICにこのイベントを送信します。 |
| TemplateRuntime    | [`LikeCommandIssued`](/CIC/References/CICInterface/TemplateRuntime.md#LikeCommandIssued) | ユーザーがクライアントのメディアプレーヤーで、特定のメディアに対して「いいね」ボタンを押した場合、クライアントはこのイベントをCICに送信する必要があります。 |
| TemplateRuntime    | [`RequestPlayerInfo`](/CIC/References/CICInterface/TemplateRuntime.md#RequestPlayerInfo) | クライアントから、メディアプレーヤーに表示する再生リスト、アルバムの画像、歌詞のような再生メタデータをCICにリクエストします。 |
| TemplateRuntime    | [`UnlikeCommandIssued`](/CIC/References/CICInterface/TemplateRuntime.md#UnlikeCommandIssued) | ユーザーがクライアントのメディアプレーヤーで、特定のメディアに対して「いいね」を取り消すボタン(Unlike)を押した場合、クライアントはこのイベントをCICに送信する必要があります。 |
| TextRecognizer  | [`Recognize`](/CIC/References/CICInterface/TextRecognizer.md#Recognize)      | ユーザーから取得したテキストをCICに送信して、ユーザーの意図を認識するようにリクエストします。                           |
