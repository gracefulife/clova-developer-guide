# 지시 메시지 색인

| 네임스페이스          | 메시지 이름       | 설명                                             |
|--------------------|----------------|-------------------------------------------------|
| Alerts             | [`DeleteAlert`](/CIC/References/APIs/Alerts.md#DeleteAlert)             | 클라이언트에게 알람 혹은 타이머 삭제를 지시합니다.                                                  |
| Alerts             | [`GetAlert`](/CIC/References/APIs/Alerts.md#GetAlert)                   | 클라이언트에게 알람 혹은 타이머 조회를 지시합니다.                                                  |
| Alerts             | [`SetAlert`](/CIC/References/APIs/Alerts.md#SetAlert)                   | 클라이언트에게 알람 혹은 타이머 설정을 지시합니다.                                                  |
| AudioPlayer        | [`Play`](/CIC/References/APIs/AudioPlayer.md#Play)                      | 클라이언트에게 특정 오디오 스트림을 재생하거나 재생 대기열에 추가하도록 지시합니다.                          |
| AudioPlayer        | [`StreamDeliver`](/CIC/References/APIs/AudioPlayer.md#StreamDeliver)    | [`AudioPlayer.StreamRequested`](/CIC/References/APIs/AudioPlayer.md#StreamRequested) 이벤트 메시지의 응답이며, 실제 음악 재생이 가능한 오디오 스트림 정보를 수신해야 할 때 사용합니다. |
| Clova              | [`AddMemo`](/CIC/References/APIs/Clova.md#AddMemo)                      | 클라이언트에게 새로운 메모를 추가하도록 지시합니다.                                                  |
| Clova              | [`AddReminder`](/CIC/References/APIs/Clova.md#AddReminder)              | 클라이언트에게 새로운 리마인더를 추가하도록 지시합니다.                                               |
| Clova              | [`AddSchedule`](/CIC/References/APIs/Clova.md#AddSchedule)              | 클라이언트에게 새로운 일정을 추가하도록 지시합니다.                                                  |
| Clova              | [`CountSchedule`](/CIC/References/APIs/Clova.md#CountSchedule)          | 클라이언트에게 지정한 기간 사이에 있는 일정 개수를 확인하도록 지시합니다.                                 |
| Clova              | [`DeleteMemo`](/CIC/References/APIs/Clova.md#DeleteMemo)                | 클라이언트에게 메모를 삭제하도록 지시합니다.                                                       |
| Clova              | [`DeleteReminder`](/CIC/References/APIs/Clova.md#DeleteReminder)        | 클라이언트에게 리마인더를 삭제하도록 지시합니다.                                                    |
| Clova              | [`DeleteSchedule`](/CIC/References/APIs/Clova.md#DeleteSchedule)        | 클라이언트에게 일정을 삭제하도록 지시합니다.                                                       |
| Clova              | [`FinishExtension`](/CIC/References/APIs/Clova.md#FinishExtension)      | 클라이언트에게 특정 Extension을 종료하도록 지시합니다.                                             |
| Clova              | [`GetMemo`](/CIC/References/APIs/Clova.md#GetMemo)                      | 클라이언트에게 메모를 조회하도록 지시합니다.                                                       |
| Clova              | [`GetReminder`](/CIC/References/APIs/Clova.md#GetReminder)              | 클라이언트에게 리마인더를 조회하도록 지시합니다.                                                    |
| Clova              | [`GetSchedule`](/CIC/References/APIs/Clova.md#GetSchedule) | 클라이언트에게 일정을 조회하도록 지시합니다.                                                       |
| Clova              | [`Hello`](/CIC/References/APIs/Clova.md#Hello)             | 클라이언트에게 downchannel 연결 설정이 완료되었음을 알립니다.                                       |
| Clova              | [`Help`](/CIC/References/APIs/Clova.md#Help)               | 클라이언트에게 미리 준비해둔 도움말 정보를 제공하도록 지시합니다.                                       |
| Clova              | [`RenderMemoList`](/CIC/References/APIs/Clova.md#RenderMemoList)        | 클라이언트에게 메모 목록을 표시하도록 지시합니다.                                                   |
| Clova              | [`RenderReminderList`](/CIC/References/APIs/Clova.md#RenderReminderList) | 클라이언트에게 리마인더 목록을 표시하도록 지시합니다.                                               |
| Clova              | [`RenderTemplate`](/CIC/References/APIs/Clova.md#RenderTemplate)        | 클라이언트에게 템플릿을 표시하도록 지시합니다.                                                     |
| Clova              | [`RenderText`](/CIC/References/APIs/Clova.md#RenderText)                | 클라이언트에게 텍스트를 표시하도록 지시합니다.                                                     |
| Clova              | [`StartExtension`](/CIC/References/APIs/Clova.md#StartExtension)        | 클라이언트에게 특정 Extension을 시작하도록 지시합니다.                                             |
| DeviceControl      | [`BtConnect`](/CIC/References/APIs/DeviceControl.md#BtConnect)          | 클라이언트에게 특정 블루투스 기기와 연결을 설정하도록 지시합니다.                                       |
| DeviceControl      | [`BtDisconnect`](/CIC/References/APIs/DeviceControl.md#BtDisconnect)    | 클라이언트에게 특정 블루투스 기기와 연결을 해제하도록 지시합니다.                                       |
| DeviceControl      | [`BtStartPairing`](/CIC/References/APIs/DeviceControl.md#BtStartPairing) | 클라이언트에게 블루투스 페어링 모드를 시작하도록 지시합니다.                                          |
| DeviceControl      | [`BtStopPairing`](/CIC/References/APIs/DeviceControl.md#BtStopPairing)   | 클라이언트에게 블루투스 페어링 모드로 중지하도록 지시합니다.                                          |
| DeviceControl      | [`Decrease`](/CIC/References/APIs/DeviceControl.md#Decrease)             | 클라이언트에게 스피커 볼륨 또는 화면 밝기를 기본 단위만큼 줄이도록 지시합니다.                            |
| DeviceControl      | [`Increase`](/CIC/References/APIs/DeviceControl.md#Increase)             | 클라이언트에게 스피커 볼륨 또는 화면 밝기를 기본 단위만큼 높이도록 지시합니다.                            |
| DeviceControl      | [`LaunchApp`](#LaunchApp)                                                | 클라이언트에게 특정 앱을 실행하도록 지시합니다.                                                     |
| DeviceControl      | [`OpenScreen`](/CIC/References/APIs/DeviceControl.md#OpenScreen)         | 클라이언트에게 설정 화면을 열도록 지시합니다.                                                     |
| DeviceControl      | [`SetValue`](/CIC/References/APIs/DeviceControl.md#SetValue)            | 클라이언트에게 스피커 볼륨 또는 화면 밝기를 지정한 값으로 설정하도록 지시합니다.                           |
| DeviceControl      | [`TurnOff`](/CIC/References/APIs/DeviceControl.md#TurnOff)               | 클라이언트에게 지정한 기능이나 모드를 끄거나 비활성화하도록 지시합니다.                                  |
| DeviceControl      | [`TurnOn`](/CIC/References/APIs/DeviceControl.md#TurnOn)                 | 클라이언트에게 지정한 기능을 켜거나 활성화하도록 지시합니다.                                          |
| DeviceControl      | [`UpdateDeviceState`](#UpdateDeviceState)                                | 클라이언트에게 사용자 계정에 등록된 또 다른 클라이언트 기기의 상태를 업데이트하도록 지시합니다.               |
| PlaybackController | [`Mute`](/CIC/References/APIs/PlaybackController.md#Mute)               | 클라이언트에게 스피커 볼륨을 음소거하도록 지시합니다.                                                |
| PlaybackController | [`Next`](/CIC/References/APIs/PlaybackController.md#Next)               | 클라이언트에게 재생 대기열에 있는 다음 오디오 스트림 재생하도록 지시합니다.                               |
| PlaybackController | [`Pause`](/CIC/References/APIs/PlaybackController.md#Pause)             | 클라이언트에게 재생 중인 오디오 스트림을 일시 정지하도록 지시합니다.                                    |
| PlaybackController | [`Previous`](/CIC/References/APIs/PlaybackController.md#Previous)       | 클라이언트에게 재생 대기열에 있는 이전 오디오 스트림을 재생하도록 지시합니다.                              |
| PlaybackController | [`Resume`](/CIC/References/APIs/PlaybackController.md#Resume)           | 클라이언트에게 오디오 스트림 재생을 재개하도록 지시합니다.                                            |
| PlaybackController | [`Stop`](/CIC/References/APIs/PlaybackController.md#Stop)               | 클라이언트에게 오디오 스트림 재생을 중지하도록 지시합니다.                                            |
| PlaybackController | [`TurnOffRepeatMode`](/CIC/References/APIs/PlaybackController.md#TurnOffRepeatMode) | 클라이언트에게 한곡 반복 재생 모드를 끄도록 지시합니다.                                  |
| PlaybackController | [`TurnOnRepeatMode`](/CIC/References/APIs/PlaybackController.md#TurnOnRepeatMode) | 클라이언트에게 한곡 반복 재생 모드를 켜도록 지시합니다.                                    |
| PlaybackController | [`Unmute`](/CIC/References/APIs/PlaybackController.md#Unmute)           | 클라이언트에게 스피커 볼륨의 음소거를 해제하도록 지시합니다.                                           |
| PlaybackController | [`VolumeDown`](/CIC/References/APIs/PlaybackController.md#VolumeDown)   | 클라이언트에게 스피커 볼륨을 낮추도록 지시합니다.                                                   |
| PlaybackController | [`VolumeUp`](/CIC/References/APIs/PlaybackController.md#VolumeUp)       | 클라이언트에게 스피커 볼륨을 높이도록 지시합니다.                                                   |
| SpeechRecognizer   | [`ExpectSpeech`](/CIC/References/APIs/SpeechRecognizer.md#ExpectSpeech) | 클라이언트에게 사용자의 음성 입력을 대기하도록 지시합니다.                                            |
| SpeechRecognizer   | [`ShowRecognizedText`](/CIC/References/APIs/SpeechRecognizer.md#ShowRecognizedText) | 클라이언트에게 인식된 사용자 음성을 실시간으로 전달합니다.                                |
| SpeechRecognizer   | [`StopCapture`](/CIC/References/APIs/SpeechRecognizer.md#StopCapture)   | 클라이언트에게 사용자의 음성 인식을 중지하도록 지시합니다.                                            |
| SpeechSynthesizer  | [`Speak`](/CIC/References/APIs/SpeechSynthesizer#Speak)                 | 클라이언트에게 합성된 TTS 음성 파일을 스피커로 출력하도록 지시합니다.                                   |
