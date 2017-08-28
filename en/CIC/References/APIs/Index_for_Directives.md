# Directive messages index

| Namespace          | Message name       | Description                                             |
|--------------------|----------------|-------------------------------------------------|
| Alerts             | [`DeleteAlert`](/CIC/References/APIs/Alerts.md#DeleteAlert)             | Instructs your client to delete alarms or timers.                                                  |
| Alerts             | [`GetAlert`](/CIC/References/APIs/Alerts.md#GetAlert)                   | Instructs your client to look up alarms or timers.                                                  |
| Alerts             | [`SetAlert`](/CIC/References/APIs/Alerts.md#SetAlert)                   | Instructs your client to set alarms or timers.                                                  |
| AudioPlayer        | [`Play`](/CIC/References/APIs/AudioPlayer.md#Play)                      | Instructs your client to start playback of a specified audio stream or add it to a playback queue.                          |
| AudioPlayer        | [`StreamDeliver`](/CIC/References/APIs/AudioPlayer.md#StreamDeliver)    | Returns audio stream details necessary for playback. This is a response message to an [`AudioPlayer.StreamRequested`](/CIC/References/APIs/AudioPlayer.md#StreamRequested) event message. |
| Clova              | [`AddMemo`](/CIC/References/APIs/Clova.md#AddMemo)                      | Instructs your client to add new memos.                                                  |
| Clova              | [`AddReminder`](/CIC/References/APIs/Clova.md#AddReminder)              | Instructs your client to add new reminders.                                               |
| Clova              | [`AddSchedule`](/CIC/References/APIs/Clova.md#AddSchedule)              | Instructs your client to add new schedules.                                                  |
| Clova              | [`CountSchedule`](/CIC/References/APIs/Clova.md#CountSchedule)          | Instructs your client to count the number of schedules within a specified period.                                 |
| Clova              | [`DeleteMemo`](/CIC/References/APIs/Clova.md#DeleteMemo)                | Instructs your client to delete memos.                                                       |
| Clova              | [`DeleteReminder`](/CIC/References/APIs/Clova.md#DeleteReminder)        | Instructs your client to delete reminders.                                                    |
| Clova              | [`DeleteSchedule`](/CIC/References/APIs/Clova.md#DeleteSchedule)        | Instructs your client to delete schedules.                                                       |
| Clova              | [`FinishExtension`](/CIC/References/APIs/Clova.md#FinishExtension)      | Instructs your client to finish a specified extension.                                             |
| Clova              | [`GetMemo`](/CIC/References/APIs/Clova.md#GetMemo)                      | Instructs your client to look up memos.                                                       |
| Clova              | [`GetReminder`](/CIC/References/APIs/Clova.md#GetReminder)              | Instructs your client to look up reminders.                                                    |
| Clova              | [`GetSchedule`](#GetSchedule)                                           | Instructs your client to look up schedules.                                                       |
| Clova              | [`Hello`](#Hello)                                                       | Notifies your client that a downchannel connection has been established.                                       |
| Clova              | [`RenderMemoList`](/CIC/References/APIs/Clova.md#RenderMemoList)        | Instructs your client to display a list of memos.                                                   |
| Clova              | [`RenderReminderList`](/CIC/References/APIs/Clova.md#RenderReminderList) | Instructs your client to display a list of reminders.                                               |
| Clova              | [`RenderTemplate`](/CIC/References/APIs/Clova.md#RenderTemplate)        | Instructs your client to display templates.                                                     |
| Clova              | [`RenderText`](/CIC/References/APIs/Clova.md#RenderText)                | Instructs your client to display text.                                                     |
| Clova              | [`StartExtension`](/CIC/References/APIs/Clova.md#StartExtension)        | Instructs your client to start a specified extension.                                             |
| DeviceControl      | [`BtConnect`](/CIC/References/APIs/DeviceControl.md#BtConnect)          | Instructs your client to connect a specified Bluetooth device. |
| DeviceControl      | [`BtDisconnect`](/CIC/References/APIs/DeviceControl.md#BtDisconnect)    | Instructs your client to disconnect a specified Bluetooth device. |
| DeviceControl      | [`BtStartPairing`](/CIC/References/APIs/DeviceControl.md#BtStartPairing) | Instructs your client to start a Bluetooth pairing mode. |
| DeviceControl      | [`BtStopPairing`](/CIC/References/APIs/DeviceControl.md#BtStopPairing)   | Instructs your client to stop a Bluetooth pairing mode. |
| DeviceControl      | [`Decrease`](/CIC/References/APIs/DeviceControl.md#Decrease)             | Instructs your client to turn down speaker volume or decrease screen brightness by a value of default unit. |
| DeviceControl      | [`Increase`](/CIC/References/APIs/DeviceControl.md#Increase)             | Instructs your client to turn up speaker volume or increase screen brightness by a value of default unit. |
| DeviceControl      | [`OpenScreen`](/CIC/References/APIs/DeviceControl.md#OpenScreen)         | Instructs your client to open the settings screen. |
| DeviceControl      |  [`SetPoint`](/CIC/References/APIs/DeviceControl.md#SetPoint)            | Instructs your client to set speaker volume or screen brightness to a specified value. |
| DeviceControl      | [`TurnOff`](/CIC/References/APIs/DeviceControl.md#TurnOff)               | Instructs your client to turn off or disable a specified feature or mode. |
| DeviceControl      | [`TurnOn`](/CIC/References/APIs/DeviceControl.md#TurnOn)                 | Instructs your client to turn on or enable a specified feature or mode. |
| DeviceControl      | [`UpdateDeviceState`](#UpdateDeviceState)                                | Instructs your client to update states of other client devices registered to a user account.                     |
| PlaybackController | [`Mute`](/CIC/References/APIs/PlaybackController.md#Mute)               | Instructs your client to mute its speaker volume.                                                |
| PlaybackController | [`Next`](/CIC/References/APIs/PlaybackController.md#Next)               | Instructs your client to start playback of a next audio stream in a playback queue.                               |
| PlaybackController | [`Pause`](/CIC/References/APIs/PlaybackController.md#Pause)             | Instructs your client to pause playback of a current audio stream.                                    |
| PlaybackController | [`Previous`](/CIC/References/APIs/PlaybackController.md#Previous)       | Instructs your client to start playback of a previous audio stream in a playback queue.                              |
| PlaybackController | [`Resume`](/CIC/References/APIs/PlaybackController.md#Resume)           | Instructs your client to resume playback of an audio stream.                                            |
| PlaybackController | [`Stop`](/CIC/References/APIs/PlaybackController.md#Stop)               | Instructs your client to stop playback of an audio stream.                                            |
| PlaybackController | [`TurnOffRepeatMode`](/CIC/References/APIs/PlaybackController.md#TurnOffRepeatMode) | Instructs your client to turn off the single track repeat mode.                                  |
| PlaybackController | [`TurnOnRepeatMode`](/CIC/References/APIs/PlaybackController.md#TurnOnRepeatMode) | Instructs your client to turn on the single track repeat mode.                                    |
| PlaybackController | [`Unmute`](/CIC/References/APIs/PlaybackController.md#Unmute)           | Instructs your client to unmute its speaker volume.                                           |
| PlaybackController | [`VolumeDown`](/CIC/References/APIs/PlaybackController.md#VolumeDown)   | Instructs your client to turn down its speaker volume.                                                   |
| PlaybackController | [`VolumeUp`](/CIC/References/APIs/PlaybackController.md#VolumeUp)       | Instructs your client to turn up its speaker volume.                                                   |
| SpeechRecognizer   | [`ExpectSpeech`](/CIC/References/APIs/SpeechRecognizer.md#ExpectSpeech) | Instructs your client to be ready to receive speech input from a user.                                            |
| SpeechRecognizer   | [`ShowRecognizedText`](/CIC/References/APIs/SpeechRecognizer.md#ShowRecognizedText) | Returns recognition results of user speech in real time.                             |
| SpeechRecognizer   | [`StopCapture`](/CIC/References/APIs/SpeechRecognizer.md#StopCapture)   | Instructs your client to stop recognizing user's speech.                                            |
| SpeechSynthesizer  | [`Speak`](/CIC/References/APIs/SpeechSynthesizer#Speak)                 | Instructs your client to play the synthesized TTS audio file through its speaker.                                   |
