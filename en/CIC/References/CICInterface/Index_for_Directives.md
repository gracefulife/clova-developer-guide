# Directive messages index

| Namespace          | Message name       | Description                                             |
|--------------------|----------------|-------------------------------------------------|
| Alerts             | [`DeleteAlert`](/CIC/References/CICInterface/Alerts.md#DeleteAlert)             | Instructs a client to delete the specified alarm. |
| Alerts             | [`SetAlert`](/CIC/References/CICInterface/Alerts.md#SetAlert)                   | Instructs a client to add an alarm or to change the specified alarm. |
| Alerts             | [`StopAlert`](/CIC/References/CICInterface/Alerts.md#StopAlert)                 | Instructs a client to stop the specified alarm.   |
| AudioPlayer        | [`ClearQueue`](/CIC/References/CICInterface/AudioPlayer.md#ClearQueue)                      | Instructs a client to initialize the playback queue.                            |
| AudioPlayer        | [`Play`](/CIC/References/CICInterface/AudioPlayer.md#Play)                      | Instructs a client to start playing the specified audio stream or add the audio to a playback queue.                           |
| AudioPlayer        | [`StreamDeliver`](/CIC/References/CICInterface/AudioPlayer.md#StreamDeliver)    | Returns the audio stream itself as a response to the [`AudioPlayer.StreamRequested`](#StreamRequested) event.  |
| Clova              | [`ExpectLogin`](/CIC/References/CICInterface/Clova.md#ExpectLogin)              | Instructs a client to prompt a user to authenticate their {{ book.OrientedService }} account (i.e. login).          |
| Clova              | [`FinishExtension`](/CIC/References/CICInterface/Clova.md#FinishExtension)      | Instructs a client to end the specified extension.                                         |
| Clova              | [`Hello`](/CIC/References/CICInterface/Clova.md#Hello)                          | Notifies a client that a downchannel connection has been established.                                        |
| Clova              | [`Help`](/CIC/References/CICInterface/Clova.md#Help)                            | Instructs a client to provide pre-made help to the user.                                         |
| Clova              | [`RenderTemplate`](/CIC/References/CICInterface/Clova.md#RenderTemplate)        | Instructs your client to display templates.                                                |
| Clova              | [`RenderText`](/CIC/References/CICInterface/Clova.md#RenderText)                | Instructs a client to display the given text.                                   |
| Clova              | [`StartExtension`](/CIC/References/CICInterface/Clova.md#StartExtension)        | Instructs a client to start running the given extension.                                            |
| DeviceControl      | [`BtConnect`](/CIC/References/CICInterface/DeviceControl.md#BtConnect)          | Instructs a client to connect a Bluetooth speaker.                                       |
| DeviceControl      | [`BtDisconnect`](/CIC/References/CICInterface/DeviceControl.md#BtDisconnect)    | Instructs a client to disconnect a Bluetooth speaker.                                     |
| DeviceControl      | [`BtStartPairing`](/CIC/References/CICInterface/DeviceControl.md#BtStartPairing) | Instructs a client to start the Bluetooth pairing mode.                                           |
| DeviceControl      | [`BtStopPairing`](/CIC/References/CICInterface/DeviceControl.md#BtStopPairing)   | Instructs a client to terminate the Bluetooth pairing mode.                                         |
| DeviceControl      | [`Decrease`](/CIC/References/CICInterface/DeviceControl.md#Decrease)             | Instructs a client to turn down speaker volume or decrease screen brightness by a default unit.                               |
| DeviceControl      | [`ExpectReportState`](/CIC/References/CICInterface/DeviceControl.md#ExpectReportState) | Instructs a client to report the current state of the client device to CIC.                                  |
| DeviceControl      | [`Increase`](/CIC/References/CICInterface/DeviceControl.md#Increase)             | Instructs a client to turn up speaker volume or increase screen brightness by a default unit.                            |
| DeviceControl      | [`LaunchApp`](/CIC/References/CICInterface/DeviceControl.md#LaunchApp)           | Instructs a client to launch the specified app.                                                    |
| DeviceControl      | [`OpenScreen`](/CIC/References/CICInterface/DeviceControl.md#OpenScreen)         | Instructs a client to open the settings screen.                                                  |
| DeviceControl      | [`SetValue`](/CIC/References/CICInterface/DeviceControl.md#SetValue)            | Instructs a client to set speaker volume or screen brightness to a specified value.                            |
| DeviceControl      | [`SynchronizeState`](/CIC/References/CICInterface/DeviceControl.md#SynchronizeState) | Instructs a client to update states of other client's devices registered on the user account.             |
| DeviceControl      | [`TurnOff`](/CIC/References/CICInterface/DeviceControl.md#TurnOff)               | Instructs a client to turn off or disable a specified feature or mode.                                   |
| DeviceControl      | [`TurnOn`](/CIC/References/CICInterface/DeviceControl.md#TurnOn)                 | Instructs a client to turn on or enable a specified feature or mode.                                            |
| Notifier           | [`ClearIndicator`](/CIC/References/CICInterface/Notifier.md#ClearIndicator)      | Instructs a client to turn off all the notification indicators.                                        |
| Notifier           | [`SetIndicator`](/CIC/References/CICInterface/Notifier.md#SetIndicator)         | Instructs a client to turn on notification indicators or unchecked notifications.                              |
| PlaybackController | [`Mute`](/CIC/References/CICInterface/PlaybackController.md#Mute)               | Instructs a client to mute the audio player.                                                 |
| PlaybackController | [`Next`](/CIC/References/CICInterface/PlaybackController.md#Next)               | Instructs a client to start playing the next audio stream in the playback queue. .                               |
| PlaybackController | [`Pause`](/CIC/References/CICInterface/PlaybackController.md#Pause)             | Instructs a client to pause playing the current audio stream.                                  |
| PlaybackController | [`Previous`](/CIC/References/CICInterface/PlaybackController.md#Previous)       | Instructs a client to start playing the previous audio stream in the playback queue.                             |
| PlaybackController | [`Replay`](/CIC/References/CICInterface/PlaybackController.md#Replay)           | Instructs a client to replay the audio stream from the beginning.                             |
| PlaybackController | [`Resume`](/CIC/References/CICInterface/PlaybackController.md#Resume)           | Instructs a client to resume playing the audio stream.                                             |
| PlaybackController | [`Stop`](/CIC/References/CICInterface/PlaybackController.md#Stop)               | Instructs a client to stop playing the audio stream.                                            |
| PlaybackController | [`TurnOffRepeatMode`](/CIC/References/CICInterface/PlaybackController.md#TurnOffRepeatMode) | Instructs a client to turn off repeat for a single track.                                  |
| PlaybackController | [`TurnOnRepeatMode`](/CIC/References/CICInterface/PlaybackController.md#TurnOnRepeatMode) | Instructs a client to turn on repeat for a single track.                                   |
| PlaybackController | [`Unmute`](/CIC/References/CICInterface/PlaybackController.md#Unmute)           | Instructs a client to unmute the audio player.                                         |
| PlaybackController | [`VolumeDown`](/CIC/References/CICInterface/PlaybackController.md#VolumeDown)   | Instructs a client to turn down the audio player's volume.                                                    |
| PlaybackController | [`VolumeUp`](/CIC/References/CICInterface/PlaybackController.md#VolumeUp)       | Instructs a client to turn up the audio player's volume.                                                  |
| SpeechRecognizer   | [`ExpectSpeech`](/CIC/References/CICInterface/SpeechRecognizer.md#ExpectSpeech) | Instructs a client to receive speech input from a user.                                           |
| SpeechRecognizer   | [`KeepRecording`](/CIC/References/CICInterface/SpeechRecognizer.md#KeepRecording) | Instructs a client to continually receive speech input.                                                |
| SpeechRecognizer   | [`ShowRecognizedText`](/CIC/References/APIs/SpeechRecognizer.md#ShowRecognizedText) | Returns in real time the recognition result of a user's voice request.                               |
| SpeechRecognizer   | [`StopCapture`](/CIC/References/CICInterface/SpeechRecognizer.md#StopCapture)   | Instructs a client to stop taking in the user's voice request.                                            |
| SpeechSynthesizer  | [`Speak`](/CIC/References/CICInterface/SpeechSynthesizer.md#Speak)                 | Instructs a client to play the synthesized TTS audio file through the speaker.                                  |
| System             | [`SynchronizeState`](/CIC/References/CICInterface/System.md#SynchronizeState) | Instructs a client to synchronize its data with the given data provided by Clova. |
