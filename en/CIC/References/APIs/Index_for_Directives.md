# Directive messages index

| Namespace          | Message name       | Description                                             |
|--------------------|----------------|-------------------------------------------------|
| Alerts             | [DeleteAlert](/CIC/References/APIs/Alerts.md#DeleteAlert)             | Instructs your client to delete an alarm or timer.                                                  |
| Alerts             | [GetAlert](/CIC/References/APIs/Alerts.md#GetAlert)                   | Instructs your client to look up alarms or timers.                                                  |
| Alerts             | [SetAlert](/CIC/References/APIs/Alerts.md#SetAlert)                   | Instructs your client to set an alarm or timer.                                                  |
| AudioPlayer        | [Play](/CIC/References/APIs/AudioPlayer.md#Play)                      | Instructs your client to start playback of a specified audio stream or add it to a playback queue.                          |
| AudioPlayer        | [PlayNext](/CIC/References/APIs/AudioPlayer.md#PlayNext)              | Instructs your client to stop playback of a current audio stream and start playback of a next audio stream in a playback queue. |
| AudioPlayer        | [Stop](/CIC/References/APIs/AudioPlayer.md#Stop)                      | Instructs your client to stop playback of an audio stream.                                             |
| AudioPlayer        | [StreamDeliver](/CIC/References/APIs/AudioPlayer.md#StreamDeliver)    | Returns audio stream details necessary for playback. This is a response message to an [AudioPlayer.StreamRequested](/CIC/References/APIs/AudioPlayer.md#StreamRequested) event message. |
| Clova              | [AddMemo](/CIC/References/APIs/Clova.md#AddMemo)                      | Instructs your client to add a new memo.                                                   |
| Clova              | [AddReminder](/CIC/References/APIs/Clova.md#AddReminder)              | Instructs your client to add a new reminder.                                               |
| Clova              | [AddSchedule](/CIC/References/APIs/Clova.md#AddSchedule)              | Instructs your client to add a new schedule.                                                  |
| Clova              | [CountSchedule](/CIC/References/APIs/Clova.md#CountSchedule)          | Instructs your client to count the number of schedules in a specified period.                                 |
| Clova              | [DeleteMemo](/CIC/References/APIs/Clova.md#DeleteMemo)                | Instructs your client to delete a memo.                                                       |
| Clova              | [DeleteReminder](/CIC/References/APIs/Clova.md#DeleteReminder)        | Instructs your client to delete a reminder.                                                    |
| Clova              | [DeleteSchedule](/CIC/References/APIs/Clova.md#DeleteSchedule)        | Instructs your client to delete a schedule.                                                       |
| Clova              | [FinishExtension](/CIC/References/APIs/Clova.md#FinishExtension)      | Instructs your client to finish a specified extension.                                             |
| Clova              | [GetMemo](/CIC/References/APIs/Clova.md#GetMemo)                      | Instructs your client to look up memos.                                                       |
| Clova              | [GetReminder](/CIC/References/APIs/Clova.md#GetReminder)              | Instructs your client to look up reminders.                                                    |
| Clova              | [GetSchedule](#GetSchedule)                                           | Instructs your client to look up schedules.                                                       |
| Clova              | [RenderMemoList](/CIC/References/APIs/Clova.md#RenderMemoList)        | Instructs your client to display a list of memos.                                                   |
| Clova              | [RenderReminderList](/CIC/References/APIs/Clova.md#RenderReminderList) | Instructs your client to display a list of reminders.                                               |
| Clova              | [RenderTemplate](/CIC/References/APIs/Clova.md#RenderTemplate)        | Instructs your client to display templates.                                                     |
| Clova              | [RenderText](/CIC/References/APIs/Clova.md#RenderText)                | Instructs your client to display text.                                                     |
| Clova              | [StartExtension](/CIC/References/APIs/Clova.md#StartExtension)        | Instructs your client to start a specified extension.                                             |
| PlaybackController | [mute](/CIC/References/APIs/PlaybackController.md#mute)               | Instructs your client to mute speaker volume.                                                |
| PlaybackController | [next](/CIC/References/APIs/PlaybackController.md#next)               | Instructs your client to start playback of a next audio stream in a playback queue.                               |
| PlaybackController | [pause](/CIC/References/APIs/PlaybackController.md#pause)             | Instructs your client to pause a current audio stream.                                    |
| PlaybackController | [previous](/CIC/References/APIs/PlaybackController.md#previous)       | Instructs your client to start playback of a previous audio stream in a playback queue.                              |
| PlaybackController | [resume](/CIC/References/APIs/PlaybackController.md#resume)           | Instructs your client to resume playback of an audio stream.                                            |
| PlaybackController | [stop](/CIC/References/APIs/PlaybackController.md#stop)               | Instructs your client to stop playback of an audio stream.                                            |
| PlaybackController | [TurnOffRepeatMode](/CIC/References/APIs/PlaybackController.md#TurnOffRepeatMode) | Instructs your client to turn off single track repeat mode.                                  |
| PlaybackController | [TurnOnRepeatMode](/CIC/References/APIs/PlaybackController.md#TurnOnRepeatMode) | Instructs your client to turn on single track repeat mode.                                    |
| PlaybackController | [unmute](/CIC/References/APIs/PlaybackController.md#unmute)           | Instructs your client to unmute speaker volume.                                           |
| PlaybackController | [volumeDown](/CIC/References/APIs/PlaybackController.md#volumeDown)   | Instructs your client to turn down speaker volume.                                                   |
| PlaybackController | [volumeUp](/CIC/References/APIs/PlaybackController.md#volumeUp)       | Instructs your client to turn up speaker volume.                                                   |
| SpeechRecognizer   | [ExpectSpeech](/CIC/References/APIs/SpeechRecognizer.md#ExpectSpeech) | Instructs your client to be ready to receive speech input from a user.                                            |
| SpeechRecognizer   | [ShowRecognizedText](/CIC/References/APIs/SpeechRecognizer.md#ShowRecognizedText) | Returns recognition results of speech input in real time, in the form of natural language.                             |
| SpeechRecognizer   | [StopCapture](/CIC/References/APIs/SpeechRecognizer.md#StopCapture)   | Instructs your client to stop capturing user's speech input.                                            |
| SpeechSynthesizer  | [Speak](/CIC/References/APIs/SpeechSynthesizer#Speak)                 | Instructs your client to play a synthesized TTS audio file through a speaker.                                   |