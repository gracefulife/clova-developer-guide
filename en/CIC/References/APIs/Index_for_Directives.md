# Directive messages index

| Namespace  | Message name  | Description  |
|--------------------|----------------|-------------------------------------------------|
| Alerts  | [DeleteAlert](/CIC/References/APIs/Alerts.md#DeleteAlert)  | Instructs your client to delete alarms or timers.  |
| Alerts  | [GetAlert](/CIC/References/APIs/Alerts.md#GetAlert)  | Instructs your client to look up alarms or timers.  |
| Alerts  | [SetAlert](/CIC/References/APIs/Alerts.md#SetAlert)  | Instructs your client to set alarms or timers.  |
| AudioPlayer  | [Play](/CIC/References/APIs/AudioPlayer.md#Play)  | Instructs your client to start playback of an audio stream or add it to a playback queue.  |
| AudioPlayer  | [StreamDeliver](/CIC/References/APIs/AudioPlayer.md#StreamDeliver)  | Returns audio stream details necessary for playback. This is a response message to an [AudioPlayer.StreamRequested](/CIC/References/APIs/AudioPlayer.md#StreamRequested) event message. |
| Clova  | [AddMemo](/CIC/References/APIs/Clova.md#AddMemo)  | Instructs your client to add new memos.  |
| Clova  | [AddReminder](/CIC/References/APIs/Clova.md#AddReminder)  | Instructs your client to add new reminders.  |
| Clova  | [AddSchedule](/CIC/References/APIs/Clova.md#AddSchedule)  | Instructs your client to add new schedules.  |
| Clova  | [CountSchedule](/CIC/References/APIs/Clova.md#CountSchedule)  | Instructs your client to count the number of schedules in a specified period.  |
| Clova  | [DeleteMemo](/CIC/References/APIs/Clova.md#DeleteMemo)  | Instructs your client to delete memos.  |
| Clova  | [DeleteReminder](/CIC/References/APIs/Clova.md#DeleteReminder)  | Instructs your client to delete reminders.  |
| Clova  | [DeleteSchedule](/CIC/References/APIs/Clova.md#DeleteSchedule)  | Instructs your client to delete schedules.  |
| Clova  | [FinishExtension](/CIC/References/APIs/Clova.md#FinishExtension)  | Instructs your client to finish a specified extension.  |
| Clova  | [GetMemo](/CIC/References/APIs/Clova.md#GetMemo)  | Instructs your client to look up memos.  |
| Clova  | [GetReminder](/CIC/References/APIs/Clova.md#GetReminder)  | Instructs your client to look up reminders.  |
| Clova  | [GetSchedule](#GetSchedule)  | Instructs your client to look up schedules.  |
| Clova  | [RenderMemoList](/CIC/References/APIs/Clova.md#RenderMemoList)  | Instructs your client to display a list of memos.  |
| Clova  | [RenderReminderList](/CIC/References/APIs/Clova.md#RenderReminderList) | Instructs your client to display a list of reminders.  |
| Clova  | [RenderTemplate](/CIC/References/APIs/Clova.md#RenderTemplate)  | Instructs your client to display templates.  |
| Clova  | [RenderText](/CIC/References/APIs/Clova.md#RenderText)  | Instructs your client to display text.  |
| Clova  | [StartExtension](/CIC/References/APIs/Clova.md#StartExtension)  | Instructs your client to start a specified extension.  |
| PlaybackController | [Mute](/CIC/References/APIs/PlaybackController.md#Mute)  | Instructs your client to mute speaker volume.  |
| PlaybackController | [Next](/CIC/References/APIs/PlaybackController.md#Next)  | Instructs your client to start playback of a next audio stream in a playback queue.  |
| PlaybackController | [Pause](/CIC/References/APIs/PlaybackController.md#Pause)  | Instructs your client to pause playback of an audio stream.  |
| PlaybackController | [Previous](/CIC/References/APIs/PlaybackController.md#Previous)  | Instructs your client to start playback of a previous audio stream in a playback queue.  |
| PlaybackController | [Resume](/CIC/References/APIs/PlaybackController.md#Resume)  | Instructs your client to resume playback of an audio stream.  |
| PlaybackController | [Stop](/CIC/References/APIs/PlaybackController.md#Stop)  | Instructs your client to stop playback of an audio stream.  |
| PlaybackController | [TurnOffRepeatMode](/CIC/References/APIs/PlaybackController.md#TurnOffRepeatMode) | Instructs your client to turn off single track repeat mode.  |
| PlaybackController | [TurnOnRepeatMode](/CIC/References/APIs/PlaybackController.md#TurnOnRepeatMode) | Instructs your client to turn on single track repeat mode.  |
| PlaybackController | [Unmute](/CIC/References/APIs/PlaybackController.md#Unmute)  | Instructs your client to unmute speaker volume.  |
| PlaybackController | [VolumeDown](/CIC/References/APIs/PlaybackController.md#VolumeDown)  | Instructs your client to turn down speaker volume.  |
| PlaybackController | [VolumeUp](/CIC/References/APIs/PlaybackController.md#VolumeUp)  | Instructs your client to turn up speaker volume.  |
| SpeechRecognizer  | [ExpectSpeech](/CIC/References/APIs/SpeechRecognizer.md#ExpectSpeech) | Instructs your client to be ready to receive speech input from a user.  |
| SpeechRecognizer  | [ShowRecognizedText](/CIC/References/APIs/SpeechRecognizer.md#ShowRecognizedText) | Returns speech recognition results to your client in real time, in the form of natural language.  |
| SpeechRecognizer  | [StopCapture](/CIC/References/APIs/SpeechRecognizer.md#StopCapture)  | Instructs your client to stop capturing user's speech input.  |
| SpeechSynthesizer  | [Speak](/CIC/References/APIs/SpeechSynthesizer#Speak)  | Instructs your client to play a synthesized TTS audio file through its speaker.  |