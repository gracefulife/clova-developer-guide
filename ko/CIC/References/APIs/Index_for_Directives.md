# 지시 메시지 색인

| 네임스페이스          | 메시지 이름       | 설명                                             |
|--------------------|----------------|-------------------------------------------------|
| Alerts             | [DeleteAlert](/CIC/References/APIs/Alerts.md#DeleteAlert)             | 클라이언트에게 알람 혹은 타이머 삭제를 지시합니다.                                                  |
| Alerts             | [GetAlert](/CIC/References/APIs/Alerts.md#GetAlert)                   | 클라이언트에게 알람 혹은 타이머 조회를 지시합니다.                                                  |
| Alerts             | [SetAlert](/CIC/References/APIs/Alerts.md#SetAlert)                   | 클라이언트에게 알람 혹은 타이머 설정을 지시합니다.                                                  |
| AudioPlayer        | [Play](/CIC/References/APIs/AudioPlayer.md#Play)                      | 클라이언트에게 특정 오디오 스트림을 재생하거나 재생 대기열에 추가하도록 지시합니다.                          |
| AudioPlayer        | [PlayNext](/CIC/References/APIs/AudioPlayer.md#PlayNext)              | 클라이언트에게 재생 중인 오디오 스트림 재생을 중지하고 재생 대기열에 있는 다음 오디오 스트림 재생하도록 지시합니다. |
| AudioPlayer        | [Stop](/CIC/References/APIs/AudioPlayer.md#Stop)                      | 클라이언트에게 오디오 스트림 재생을 중지하도록 지시합니다.                                             |
| AudioPlayer        | [StreamDeliver](/CIC/References/APIs/AudioPlayer.md#StreamDeliver)    | [AudioPlayer.StreamRequested](/CIC/References/APIs/AudioPlayer.md#StreamRequested) 이벤트 메시지의 응답이며, 실제 음악 재생이 가능한 오디오 스트림 정보를 수신해야 할 때 사용합니다. |
| Clova              | [FinishExtension](/CIC/References/APIs/Clova.md#FinishExtension)      | 클라이언트에게 특정 Extension을 종료하도록 지시합니다.                                             |
| Clova              | [RenderTemplate](/CIC/References/APIs/Clova.md#RenderTemplate)        | 클라이언트에게 템플릿을 표시하도록 지시합니다.                                                     |
| Clova              | [RenderText](/CIC/References/APIs/Clova.md#RenderText)                | 클라이언트에게 텍스트를 표시하도록 지시합니다.                                                     |
| Clova              | [StartExtension](/CIC/References/APIs/Clova.md#StartExtension)        | 클라이언트에게 특정 Extension을 시작하도록 지시합니다.                                             |
| PlaybackController | [mute](/CIC/References/APIs/PlaybackController.md#mute)               | 클라이언트에게 스피커 볼륨을 음소거하도록 지시합니다.                                                |
| PlaybackController | [next](/CIC/References/APIs/PlaybackController.md#next)               | 클라이언트에게 재생 대기열에 있는 다음 오디오 스트림 재생하도록 지시합니다.                               |
| PlaybackController | [pause](/CIC/References/APIs/PlaybackController.md#pause)             | 클라이언트에게 재생 중인 오디오 스트림을 일시 정지하도록 지시합니다.                                    |
| PlaybackController | [previous](/CIC/References/APIs/PlaybackController.md#previous)       | 클라이언트에게 재생 대기열에 있는 이전 오디오 스트림을 재생하도록 지시합니다.                              |
| PlaybackController | [resume](/CIC/References/APIs/PlaybackController.md#resume)           | 클라이언트에게 오디오 스트림 재생을 재개하도록 지시합니다.                                            |
| PlaybackController | [stop](/CIC/References/APIs/PlaybackController.md#stop)               | 클라이언트에게 오디오 스트림 재생을 중지하도록 지시합니다.                                            |
| PlaybackController | [TurnOffRepeatMode](/CIC/References/APIs/PlaybackController.md#TurnOffRepeatMode) | 클라이언트에게 한곡 반복 재생 모드를 끄도록 지시합니다.                                  |
| PlaybackController | [TurnOnRepeatMode](/CIC/References/APIs/PlaybackController.md#TurnOnRepeatMode) | 클라이언트에게 한곡 반복 재생 모드를 켜도록 지시합니다.                                    |
| PlaybackController | [unmute](/CIC/References/APIs/PlaybackController.md#unmute)           | 클라이언트에게 스피커 볼륨의 음소거를 해제하도록 지시합니다.                                           |
| PlaybackController | [volumeDown](/CIC/References/APIs/PlaybackController.md#volumeDown)   | 클라이언트에게 스피커 볼륨을 낮추도록 지시합니다.                                                   |
| PlaybackController | [volumeUp](/CIC/References/APIs/PlaybackController.md#volumeUp)       | 클라이언트에게 스피커 볼륨을 높이도록 지시합니다.                                                   |
| SpeechRecognizer   | [ExpectSpeech](/CIC/References/APIs/SpeechRecognizer.md#ExpectSpeech) | 클라이언트에게 사용자의 음성 입력을 대기하도록 지시합니다.                                            |
| SpeechRecognizer   | [ShowRecognizedText](/CIC/References/APIs/SpeechRecognizer.md#ShowRecognizedText) | 클라이언트에게 음성으로 인식된 자연어를 실시간으로 전달합니다.                             |
| SpeechRecognizer   | [StopCapture](/CIC/References/APIs/SpeechRecognizer.md#StopCapture)   | 클라이언트에게 사용자의 음성 인식을 중지하도록 지시합니다.                                            |
| SpeechSynthesizer  | [Speak](/CIC/References/APIs/SpeechSynthesizer#Speak)                 | 클라이언트에게 합성된 TTS 음성 파일을 스피커로 출력하도록 지시합니다.                                   |
