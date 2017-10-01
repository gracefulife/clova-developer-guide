# 이벤트 메시지 색인

| 네임스페이스         | 메시지 이름       | 설명                                             |
|-------------------|----------------|-------------------------------------------------|
| Alerts            | [`AlertStarted`](/CIC/References/CICInterface/Alerts.md#AlertStarted)                 | 클라이언트가 알람이 시작되었음을 CIC로 보고하기 위해 사용됩니다. |
| Alerts            | [`AlertStopped`](/CIC/References/CICInterface/Alerts.md#AlertStopped)                 | 클라이언트가 알람이 중지되었음을 CIC로 보고하기 위해 사용됩니다. |
| Alerts            | [`DeleteAlertFailed`](/CIC/References/CICInterface/Alerts.md#DeleteAlertFailed)       | 클라이언트가 클라이언트에 설정된 특정 알람을 삭제하는데 실패했음을 CIC로 보고하기 위해 사용됩니다. |
| Alerts            | [`DeleteAlertSucceeded`](/CIC/References/CICInterface/Alerts.md#DeleteAlertSucceeded) | 클라이언트가 클라이언트에 설정된 특정 알람을 삭제하는데 성공했음을 CIC로 보고하기 위해 사용됩니다. |
| Alerts            | [`RequestAlertStop`](/CIC/References/CICInterface/Alerts.md#RequestAlertStop)         | 클라이언트가 현재 울리고 있는 알람을 중지하도록 Clova에게 요청할 때 사용됩니다.  |
| Alerts            | [`SetAlertFailed`](/CIC/References/CICInterface/Alerts.md#SetAlertFailed)             | 클라이언트가 특정 알람을 추가 또는 수정하는데 실패했음을 CIC로 보고하기 위해 사용됩니다. |
| Alerts            | [`SetAlertSucceeded`](/CIC/References/CICInterface/Alerts.md#SetAlertSucceeded)       | 클라이언트가 특정 알람을 추가 또는 수정하는데 성공했음을 CIC로 보고하기 위해 사용됩니다. |
| AudioPlayer       | [`PlayFinished`](/CIC/References/CICInterface/AudioPlayer.md#PlayFinished) | 클라이언트가 오디오 스트림 재생을 완료할 때 재생 완료된 오디오 스트림 정보를 CIC로 보고하기 위해 사용됩니다.        |
| AudioPlayer       | [`PlayPaused`](/CIC/References/CICInterface/AudioPlayer.md#PlayPaused)     | 클라이언트가 오디오 스트림 재생을 일시 정지할 때 일시 정지된 오디오 스트림 정보를 CIC로 보고하기 위해 사용됩니다.    |
| AudioPlayer       | [`PlayResumed`](/CIC/References/CICInterface/AudioPlayer.md#PlayResumed)   | 클라이언트가 오디오 스트림 재생을 재개할 때 재개된 오디오 스트림 정보를 CIC로 보고하기 위해 사용됩니다.            |
| AudioPlayer       | [`PlayStarted`](/CIC/References/CICInterface/AudioPlayer.md#PlayStarted)   | 클라이언트가 오디오 스트림 재생을 시작할 때 재생이 시작된 오디오 스트림 정보를 CIC로 보고하기 위해 사용됩니다.       |
| AudioPlayer       | [`PlayStopped`](/CIC/References/CICInterface/AudioPlayer.md#PlayStopped)   | 클라이언트가 오디오 스트림 재생을 중지할 때 재생이 중지된 오디오 스트림 정보를 CIC로 보고하기 위해 사용됩니다.       |
| AudioPlayer       | [`ProgressReportDelayPassed`](/CIC/References/CICInterface/AudioPlayer.md#ProgressReportPositionPassed) | 오디오 스트림 재생이 시작된 후 지정된 지연 시간만큼 시간이 지났을 때 현재 재생 상태([`AudioPlayer.PlaybackState`](/CIC/References/Context_Objects.md#PlaybackState))를 CIC로 보고하기 위해 사용됩니다. 각 오디오 스트림의 지연 시간은 [`AudioPlayer.Play`](/CIC/References/CICInterface/AudioPlayer.md#Play) 지시 메시지가 클라이언트로 전달될 때 확인할 수 있습니다. |
| AudioPlayer       | [`ProgressReportIntervalPassed`](/CIC/References/CICInterface/AudioPlayer.md#ProgressReportPositionPassed)| 오디오 스트림 재생이 시작된 후 지정된 간격마다 현재 재생 상태([`AudioPlayer.PlaybackState`](/CIC/References/Context_Objects.md#PlaybackState))를 CIC로 보고하기 위해 사용됩니다. 각 오디오 스트림의 보고 간격은 [`AudioPlayer.Play`](/CIC/References/CICInterface/AudioPlayer.md#Play) 지시 메시지가 클라이언트로 전달될 때 확인할 수 있습니다.|
| AudioPlayer       | [`ProgressReportPositionPassed`](/CIC/References/CICInterface/AudioPlayer.md#ProgressReportPositionPassed) | 오디오 스트림 재생이 시작된 후 지정된 보고 시점에 현재 재생 상태([`AudioPlayer.PlaybackState`](/CIC/References/Context_Objects.md#PlaybackState))를 CIC로 보고하기 위해 사용됩니다. 각 오디오 스트림의 보고 시점은 [`AudioPlayer.Play`](/CIC/References/CICInterface/AudioPlayer.md#Play) 지시 메시지가 클라이언트로 전달될 때 확인할 수 있습니다.|
| AudioPlayer       | [`AudioPlayer.StreamRequested`](/CIC/References/CICInterface/AudioPlayer.md#StreamRequested) | 오디오 스트림 재생을 위해 CIC로 스트리밍 URL과 같은 추가 정보를 요청하는 이벤트 메시지입니다. |
| DeviceControl     | [`ActionExecuted`](/CIC/References/CICInterface/DeviceControl.md#ActionExecuted) | 클라이언트가 기기 제어를 정상적으로 수행했음을 보고하기 위해 사용됩니다.                               |
| DeviceControl     | [`ActionFailed`](/CIC/References/CICInterface/DeviceControl.md#ActionFailed) | 클라이언트는 기기 제어를 수행할 수 없거나 수행에 실패했음을 CIC에 보고하기 위해 사용됩니다.                   |
| DeviceControl     | [`ReportState`](/CIC/References/CICInterface/DeviceControl.md#ReportState)   | 클라이언트는 기기의 현재 상태를 CIC로 보고할 때 이 메시지를 사용해야 합니다.                              |
| DeviceControl     | [`RequestStateSynchronization`](/CIC/References/CICInterface/DeviceControl.md#RequestStateSynchronization) | 사용자의 계정에 등록된 다른 클라이언트 기기의 현재 상태를 파악하고자 할 때 이 이벤트 메시지를 CIC로 전송합니다.  |
| PlaybackController | [`NextCommandIssued`](/CIC/References/CICInterface/PlaybackController.md#NextCommandIssued) | 사용자가 클라이언트의 기기에서 다음(Next)에 해당하는 버튼 누르거나 터치한 경우 클라이언트는 이 이벤트 메시지를 CIC에게 전송해야 합니다. |
| PlaybackController | [`PreviousCommandIssued`](/CIC/References/CICInterface/PlaybackController.md#PreviousCommandIssued) | 사용자가 클라이언트의 기기에서 이전(Previous)에 해당하는 버튼 누르거나 터치한 경우 클라이언트는 이 이벤트 메시지를 CIC에게 전송해야 합니다. |
| SpeechRecognizer  | [`ExpectSpeechTimedOut`](/CIC/References/CICInterface/SpeechRecognizer.md#ExpectSpeechTimedOut) | 음성 입력 대기 시간이 초과했음을 CIC에 보고합니다.                               |
| SpeechRecognizer  | [`Recognize`](/CIC/References/CICInterface/SpeechRecognizer.md#Recognize)  | 입력되는 사용자의 음성을 전달하여 음성 인식을 CIC에 요청합니다.                                          |
| SpeechSynthesizer | [`Request`](/CIC/References/CICInterface/SpeechSynthesizer.md#Request)     | CIC에 특정 텍스트를 TTS 음성 파일로 합성되도록 요청합니다.                                             |
| System          | [`System.RequestSynchronizeState`](/CIC/References/CICInterface/System.md#RequestSynchronizeState) | 클라이언트가 Clova의 클라우드 환경에 저장된 공유 정보를 동기화해야 할 때 이 이벤트 메시지를 CIC로 전송합니다. |
| TextRecognizer  | [`Recognize`](/CIC/References/CICInterface/TextRecognizer.md#Recognize)      | 사용자 텍스트 입력을 CIC로 전송하여 사용자가 무엇을 원하는지 인식하도록 요청합니다.                           |
