# 지시 메시지 색인

| 네임스페이스          | 메시지 이름       | 설명                                             |
|--------------------|----------------|-------------------------------------------------|
| Alerts             | [`DeleteAlert`](/CIC/References/CICInterface/Alerts.md#DeleteAlert)             | 클라이언트에게 알람 혹은 타이머 삭제를 지시합니다.                                                  |
| Alerts             | [`GetAlert`](/CIC/References/CICInterface/Alerts.md#GetAlert)                   | 클라이언트에게 알람 혹은 타이머 조회를 지시합니다.                                                  |
| Alerts             | [`SetAlert`](/CIC/References/CICInterface/Alerts.md#SetAlert)                   | 클라이언트에게 알람 혹은 타이머 설정을 지시합니다.                                                  |
| AudioPlayer        | [`Play`](/CIC/References/CICInterface/AudioPlayer.md#Play)                      | 클라이언트에게 특정 오디오 스트림을 재생하거나 재생 대기열에 추가하도록 지시합니다.                          |
| AudioPlayer        | [`StreamDeliver`](/CIC/References/CICInterface/AudioPlayer.md#StreamDeliver)    | [`AudioPlayer.StreamRequested`](/CIC/References/CICInterface/AudioPlayer.md#StreamRequested) 이벤트 메시지의 응답이며, 실제 음악 재생이 가능한 오디오 스트림 정보를 수신해야 할 때 사용합니다. |
| Clova              | [`AddMemo`](/CIC/References/CICInterface/Clova.md#AddMemo)                      | 클라이언트에게 새로운 메모를 추가하도록 지시합니다.                                                  |
| Clova              | [`AddReminder`](/CIC/References/CICInterface/Clova.md#AddReminder)              | 클라이언트에게 새로운 리마인더를 추가하도록 지시합니다.                                               |
| Clova              | [`AddSchedule`](/CIC/References/CICInterface/Clova.md#AddSchedule)              | 클라이언트에게 새로운 일정을 추가하도록 지시합니다.                                                  |
| Clova              | [`CountSchedule`](/CIC/References/CICInterface/Clova.md#CountSchedule)          | 클라이언트에게 지정한 기간 사이에 있는 일정 개수를 확인하도록 지시합니다.                                 |
| Clova              | [`DeleteMemo`](/CIC/References/CICInterface/Clova.md#DeleteMemo)                | 클라이언트에게 메모를 삭제하도록 지시합니다.                                                       |
| Clova              | [`DeleteReminder`](/CIC/References/CICInterface/Clova.md#DeleteReminder)        | 클라이언트에게 리마인더를 삭제하도록 지시합니다.                                                    |
| Clova              | [`DeleteSchedule`](/CIC/References/CICInterface/Clova.md#DeleteSchedule)        | 클라이언트에게 일정을 삭제하도록 지시합니다.                                                       |
| Clova              | [`FinishExtension`](/CIC/References/CICInterface/Clova.md#FinishExtension)      | 클라이언트에게 특정 Extension을 종료하도록 지시합니다.                                             |
| Clova              | [`GetMemo`](/CIC/References/CICInterface/Clova.md#GetMemo)                      | 클라이언트에게 메모를 조회하도록 지시합니다.                                                       |
| Clova              | [`GetReminder`](/CIC/References/CICInterface/Clova.md#GetReminder)              | 클라이언트에게 리마인더를 조회하도록 지시합니다.                                                    |
| Clova              | [`GetSchedule`](/CIC/References/CICInterface/Clova.md#GetSchedule)              | 클라이언트에게 일정을 조회하도록 지시합니다.                                                       |
| Clova              | [`Hello`](/CIC/References/CICInterface/Clova.md#Hello)                          | 클라이언트에게 downchannel 연결 설정이 완료되었음을 알립니다.                                       |
| Clova              | [`Help`](/CIC/References/CICInterface/Clova.md#Help)                            | 클라이언트에게 미리 준비해둔 도움말 정보를 제공하도록 지시합니다.                                       |
| Clova              | [`RenderMemoList`](/CIC/References/CICInterface/Clova.md#RenderMemoList)        | 클라이언트에게 메모 목록을 표시하도록 지시합니다.                                                   |
| Clova              | [`RenderReminderList`](/CIC/References/CICInterface/Clova.md#RenderReminderList) | 클라이언트에게 리마인더 목록을 표시하도록 지시합니다.                                               |
| Clova              | [`RenderTemplate`](/CIC/References/CICInterface/Clova.md#RenderTemplate)        | 클라이언트에게 템플릿을 표시하도록 지시합니다.                                                     |
| Clova              | [`RenderText`](/CIC/References/CICInterface/Clova.md#RenderText)                | 클라이언트에게 텍스트를 표시하도록 지시합니다.                                                     |
| Clova              | [`StartExtension`](/CIC/References/CICInterface/Clova.md#StartExtension)        | 클라이언트에게 특정 Extension을 시작하도록 지시합니다.                                             |
| DeviceControl      | [`BtConnect`](/CIC/References/CICInterface/DeviceControl.md#BtConnect)          | 클라이언트에게 특정 블루투스 기기와 연결을 설정하도록 지시합니다.                                       |
| DeviceControl      | [`BtDisconnect`](/CIC/References/CICInterface/DeviceControl.md#BtDisconnect)    | 클라이언트에게 특정 블루투스 기기와 연결을 해제하도록 지시합니다.                                       |
| DeviceControl      | [`BtStartPairing`](/CIC/References/CICInterface/DeviceControl.md#BtStartPairing) | 클라이언트에게 블루투스 페어링 모드를 시작하도록 지시합니다.                                          |
| DeviceControl      | [`BtStopPairing`](/CIC/References/CICInterface/DeviceControl.md#BtStopPairing)   | 클라이언트에게 블루투스 페어링 모드로 중지하도록 지시합니다.                                          |
| DeviceControl      | [`Decrease`](/CIC/References/CICInterface/DeviceControl.md#Decrease)             | 클라이언트에게 스피커 볼륨 또는 화면 밝기를 기본 단위만큼 줄이도록 지시합니다.                            |
| DeviceControl      | ['ExpectReportState'](/CIC/References/CICInterface/DeviceControl.md#ExpectReportState) | 클라이언트에게 기기의 현재 상태를 CIC로 보고하도록 지시합니다.                                 |
| DeviceControl      | [`Increase`](/CIC/References/CICInterface/DeviceControl.md#Increase)             | 클라이언트에게 스피커 볼륨 또는 화면 밝기를 기본 단위만큼 높이도록 지시합니다.                            |
| DeviceControl      | [`LaunchApp`](#LaunchApp)                                                       | 클라이언트에게 특정 앱을 실행하도록 지시합니다.                                                     |
| DeviceControl      | [`OpenScreen`](/CIC/References/CICInterface/DeviceControl.md#OpenScreen)         | 클라이언트에게 설정 화면을 열도록 지시합니다.                                                     |
| DeviceControl      | [`SetValue`](/CIC/References/CICInterface/DeviceControl.md#SetValue)            | 클라이언트에게 스피커 볼륨 또는 화면 밝기를 지정한 값으로 설정하도록 지시합니다.                           |
| DeviceControl      | [`SynchronizeState`](/CIC/References/CICInterface/DeviceControl.md#SynchronizeState) | 클라이언트에게 사용자 계정에 등록된 또 다른 클라이언트 기기의 상태를 업데이트하도록 지시합니다.           |
| DeviceControl      | [`TurnOff`](/CIC/References/CICInterface/DeviceControl.md#TurnOff)               | 클라이언트에게 지정한 기능이나 모드를 끄거나 비활성화하도록 지시합니다.                                  |
| DeviceControl      | [`TurnOn`](/CIC/References/CICInterface/DeviceControl.md#TurnOn)                 | 클라이언트에게 지정한 기능을 켜거나 활성화하도록 지시합니다.                                          |
| Notifier           | [`ClearIndicator`](/CIC/References/CICInterface/Notifier.md#ClearIndicator)      | 클라이언트에게 알림을 나타내는 표시를 모두 끄도록 지시합니다.                                         |
| Notifier           | [`SetIndicator`](/CIC/References/CICInterface/Notifier.md#SetIndicator)         | 클라이언트에게 확인하지 않은 알림이 있음을 나타내는 표시를 켜도록 지시합니다.                              |
| PlaybackController | [`Mute`](/CIC/References/CICInterface/PlaybackController.md#Mute)               | 클라이언트에게 스피커 볼륨을 음소거하도록 지시합니다.                                                |
| PlaybackController | [`Next`](/CIC/References/CICInterface/PlaybackController.md#Next)               | 클라이언트에게 재생 대기열에 있는 다음 오디오 스트림 재생하도록 지시합니다.                               |
| PlaybackController | [`Pause`](/CIC/References/CICInterface/PlaybackController.md#Pause)             | 클라이언트에게 재생 중인 오디오 스트림을 일시 정지하도록 지시합니다.                                    |
| PlaybackController | [`Previous`](/CIC/References/CICInterface/PlaybackController.md#Previous)       | 클라이언트에게 재생 대기열에 있는 이전 오디오 스트림을 재생하도록 지시합니다.                              |
| PlaybackController | [`Resume`](/CIC/References/CICInterface/PlaybackController.md#Resume)           | 클라이언트에게 오디오 스트림 재생을 재개하도록 지시합니다.                                            |
| PlaybackController | [`Stop`](/CIC/References/CICInterface/PlaybackController.md#Stop)               | 클라이언트에게 오디오 스트림 재생을 중지하도록 지시합니다.                                            |
| PlaybackController | [`TurnOffRepeatMode`](/CIC/References/CICInterface/PlaybackController.md#TurnOffRepeatMode) | 클라이언트에게 한곡 반복 재생 모드를 끄도록 지시합니다.                                  |
| PlaybackController | [`TurnOnRepeatMode`](/CIC/References/CICInterface/PlaybackController.md#TurnOnRepeatMode) | 클라이언트에게 한곡 반복 재생 모드를 켜도록 지시합니다.                                    |
| PlaybackController | [`Unmute`](/CIC/References/CICInterface/PlaybackController.md#Unmute)           | 클라이언트에게 스피커 볼륨의 음소거를 해제하도록 지시합니다.                                           |
| PlaybackController | [`VolumeDown`](/CIC/References/CICInterface/PlaybackController.md#VolumeDown)   | 클라이언트에게 스피커 볼륨을 낮추도록 지시합니다.                                                   |
| PlaybackController | [`VolumeUp`](/CIC/References/CICInterface/PlaybackController.md#VolumeUp)       | 클라이언트에게 스피커 볼륨을 높이도록 지시합니다.                                                   |
| SpeechRecognizer   | [`ExpectSpeech`](/CIC/References/CICInterface/SpeechRecognizer.md#ExpectSpeech) | 클라이언트에게 사용자의 음성 입력을 대기하도록 지시합니다.                                            |
| SpeechRecognizer   | [`ShowRecognizedText`](/CIC/References/CICInterface/SpeechRecognizer.md#ShowRecognizedText) | 클라이언트에게 인식된 사용자 음성을 실시간으로 전달합니다.                                |
| SpeechRecognizer   | [`StopCapture`](/CIC/References/CICInterface/SpeechRecognizer.md#StopCapture)   | 클라이언트에게 사용자의 음성 인식을 중지하도록 지시합니다.                                            |
| SpeechSynthesizer  | [`Speak`](/CIC/References/CICInterface/SpeechSynthesizer#Speak)                 | 클라이언트에게 합성된 TTS 음성 파일을 스피커로 출력하도록 지시합니다.                                   |
