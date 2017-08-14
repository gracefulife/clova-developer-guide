# 이벤트 메시지 색인

| 네임스페이스         | 메시지 이름       | 설명                                             |
|-------------------|----------------|-------------------------------------------------|
| AudioPlayer       | [`PlayFinished`](/CIC/References/APIs/AudioPlayer.md#PlayFinished) | 클라이언트가 오디오 스트림 재생을 완료할 때 재생 완료된 오디오 스트림 정보를 CIC로 보고하기 위해 사용됩니다.        |
| AudioPlayer       | [`PlayPaused`](/CIC/References/APIs/AudioPlayer.md#PlayPaused)     | 클라이언트가 오디오 스트림 재생을 일시 정지할 때 일시 정지된 오디오 스트림 정보를 CIC로 보고하기 위해 사용됩니다.    |
| AudioPlayer       | [`PlayResumed`](/CIC/References/APIs/AudioPlayer.md#PlayResumed)   | 클라이언트가 오디오 스트림 재생을 재개할 때 재개된 오디오 스트림 정보를 CIC로 보고하기 위해 사용됩니다.            |
| AudioPlayer       | [`PlayStarted`](/CIC/References/APIs/AudioPlayer.md#PlayStarted)   | 클라이언트가 오디오 스트림 재생을 시작할 때 재생이 시작된 오디오 스트림 정보를 CIC로 보고하기 위해 사용됩니다.       |
| AudioPlayer       | [`PlayStopped`](/CIC/References/APIs/AudioPlayer.md#PlayStopped)   | 클라이언트가 오디오 스트림 재생을 중지할 때 재생이 중지된 오디오 스트림 정보를 CIC로 보고하기 위해 사용됩니다.       |
| AudioPlayer       | [`ProgressReportDelayPassed`](/CIC/References/APIs/AudioPlayer.md#ProgressReportPositionPassed) | 오디오 스트림 재생이 시작된 후 지정된 지연 시간만큼 시간이 지났을 때 현재 재생 상태([`AudioPlayer.PlaybackState`](/CIC/References/Context_Objects.md#PlaybackState))를 CIC로 보고하기 위해 사용됩니다. 각 오디오 스트림의 지연 시간은 [`AudioPlayer.Play`](/CIC/References/APIs/AudioPlayer.md#Play) 지시 메시지가 클라이언트로 전달될 때 확인할 수 있습니다. |
| AudioPlayer       | [`ProgressReportIntervalPassed`](/CIC/References/APIs/AudioPlayer.md#ProgressReportPositionPassed)| 오디오 스트림 재생이 시작된 후 지정된 간격마다 현재 재생 상태([`AudioPlayer.PlaybackState`](/CIC/References/Context_Objects.md#PlaybackState))를 CIC로 보고하기 위해 사용됩니다. 각 오디오 스트림의 보고 간격은 [`AudioPlayer.Play`](/CIC/References/APIs/AudioPlayer.md#Play) 지시 메시지가 클라이언트로 전달될 때 확인할 수 있습니다.|
| AudioPlayer       | [`ProgressReportPositionPassed`](/CIC/References/APIs/AudioPlayer.md#ProgressReportPositionPassed) | 오디오 스트림 재생이 시작된 후 지정된 보고 시점에 현재 재생 상태([`AudioPlayer.PlaybackState`](/CIC/References/Context_Objects.md#PlaybackState))를 CIC로 보고하기 위해 사용됩니다. 각 오디오 스트림의 보고 시점은 [`AudioPlayer.Play`](/CIC/References/APIs/AudioPlayer.md#Play) 지시 메시지가 클라이언트로 전달될 때 확인할 수 있습니다.|
| AudioPlayer       | [`AudioPlayer.StreamRequested`](/CIC/References/APIs/AudioPlayer.md#StreamRequested) | 오디오 스트림 재생을 위해 CIC로 스트리밍 URL과 같은 추가 정보를 요청하는 이벤트 메시지입니다. |
| DeviceControl     | [`ActionExecuted`](/CIC/References/APIs/DeviceControl.md#ActionExecuted) | 클라이언트는 기기 제어를 정상적으로 수행한 경우 이 지시 메시지를 CIC로 전송해야 합니다. |
| DeviceControl     | [`ActionFailed`](/CIC/References/APIs/DeviceControl.md#ActionFailed) | 클라이언트는 기기 제어를 수행할 수 없거나 수행에 실패한 경우 이 지시 메시지를 CIC로 전송해야 합니다. |
| Memo              | [`Created`](/CIC/References/APIs/Memo.md#Created)                  | CIC에 특정 메모를 등록하도록 요청합니다.                                                            |
| Memo              | [`Deleted`](/CIC/References/APIs/Memo.md#Deleted)                  | CIC에 특정 메모를 삭제하도록 요청합니다.                                                            |
| Memo              | [`Get`](/CIC/References/APIs/Memo.md#Get)                          | CIC에 사용자가 생성한 모든 메모 목록을 요청합니다.                                                    |
| Memo              | [`Updated`](/CIC/References/APIs/Memo.md#Updated)                  | CIC에 특정 메모를 갱신하도록 요청합니다.                                                            |
| Reminder          | [`Created`](/CIC/References/APIs/Reminder.md#Created)              | CIC에 특정 리마인더를 생성하도록 요청합니다.                                                         |
| Reminder          | [`Deleted`](/CIC/References/APIs/Reminder.md#Deleted)              | CIC에 특정 리마인더를 삭제하도록 요청합니다.                                                         |
| Reminder          | [`Get`](/CIC/References/APIs/Reminder.md#Get)                      | CIC에 사용자가 생성한 모든 리마인더 목록을 요청합니다.                                                 |
| Reminder          | [`Updated`](/CIC/References/APIs/Reminder.md#Updated)              | CIC에 특정 리마인더를 갱신하도록 요청합니다.                                                         |
| SpeechRecognizer  | [`ExpectSpeechTimedOut`](/CIC/References/APIs/SpeechRecognizer.md#ExpectSpeechTimedOut) | 음성 입력 대기 시간이 초과했음을 CIC에 보고합니다.                               |
| SpeechRecognizer  | [`Recognize`](/CIC/References/APIs/SpeechRecognizer.md#Recognize)  | 입력되는 사용자의 음성을 전달하여 음성 인식을 CIC에 요청합니다.                                          |
| SpeechSynthesizer | [`Request`](/CIC/References/APIs/SpeechSynthesizer.md#Request)     | CIC에 특정 텍스트를 TTS 음성 파일로 합성되도록 요청합니다.                                             |
