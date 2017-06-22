# Directive messages index

| Namespace  | Message name  | Description  |
|--------------------|----------------|-------------------------------------------------|
| Alerts  | [DeleteAlert](/CIC/References/APIs/Alerts.md#DeleteAlert)  | Instructs your client to delete an alarm or a timer.  |
| Alerts  | [GetAlert](/CIC/References/APIs/Alerts.md#GetAlert)  | Instructs your client to look up an alarm or a timer.  |
| Alerts  | [SetAlert](/CIC/References/APIs/Alerts.md#SetAlert)  | Instructs your client to set an alarm or a timer.  |
| AudioPlayer  | [Play](/CIC/References/APIs/AudioPlayer.md#Play)  | Instructs your client to start playback of the audio stream or add it to a playback queue.  |
| AudioPlayer  | [PlayNext](/CIC/References/APIs/AudioPlayer.md#PlayNext)  | Instructs your client to stop playback of the current audio stream and start playback of the next one in a playback queue. |
| AudioPlayer  | [Stop](/CIC/References/APIs/AudioPlayer.md#Stop)  | Instructs your client to stop playback of the audio stream.  |
| AudioPlayer  | [StreamDeliver](/CIC/References/APIs/AudioPlayer.md#StreamDeliver)  | This message is sent in response to an [AudioPlayer.StreamRequested](/CIC/References/APIs/AudioPlayer.md#StreamRequested) Event message. It is sent when your client needs to receive details of the audio stream necessary for playback. |
| Clova  | [AddMemo](/CIC/References/APIs/Clova.md#AddMemo)  | Instructs your client to add a new memo.  |
| Clova  | [AddReminder](/CIC/References/APIs/Clova.md#AddReminder)  | Instructs your client to add a new reminder.  |
| Clova  | [AddSchedule](/CIC/References/APIs/Clova.md#AddSchedule)  | Instructs your client to add a new schedule.  |
| Clova  | [CountSchedule](/CIC/References/APIs/Clova.md#CountSchedule)  | Instructs your client to count the number of schedules within the specified period.  |
| Clova  | [DeleteMemo](/CIC/References/APIs/Clova.md#DeleteMemo)  | Instructs your client to delete a memo.  |
| Clova  | [DeleteReminder](/CIC/References/APIs/Clova.md#DeleteReminder)  | Instructs your client to delete a reminder.  |
| Clova  | [DeleteSchedule](/CIC/References/APIs/Clova.md#DeleteSchedule)  | Instructs your client to delete a schedule.  |
| Clova  | [FinishExtension](/CIC/References/APIs/Clova.md#FinishExtension)  | Instructs your client to finish an extension.  |
| Clova  | [GetMemo](/CIC/References/APIs/Clova.md#GetMemo)  | Instructs your client to look up a memo.  |
| Clova  | [GetReminder](/CIC/References/APIs/Clova.md#GetReminder)  | Instructs your client to look up a reminder.  |
| Clova  | [GetSchedule](#GetSchedule)  | Instructs your client to look up a schedule.  |
| Clova  | [RenderMemoList](/CIC/References/APIs/Clova.md#RenderMemoList)  | Instructs your client to display the list of memos.  |
| Clova  | [RenderReminderList](/CIC/References/APIs/Clova.md#RenderReminderList) | Instructs your client to display the list of reminders.  |
| Clova  | [RenderTemplate](/CIC/References/APIs/Clova.md#RenderTemplate)  | Instructs your client to display a template.  |
| Clova  | [RenderText](/CIC/References/APIs/Clova.md#RenderText)  | Instructs your client to display a text.  |
| Clova  | [StartExtension](/CIC/References/APIs/Clova.md#StartExtension)  | Instructs your client to start an extension.  |
| PlaybackController | [mute](/CIC/References/APIs/PlaybackController.md#mute)  | Instructs your client to mute the speaker volume.  |
| PlaybackController | [next](/CIC/References/APIs/PlaybackController.md#next)  | Instructs your client to start playback of the next audio stream in a playback queue.  |
| PlaybackController | [pause](/CIC/References/APIs/PlaybackController.md#pause)  | Instructs your client to pause playback of the audio stream.  |
| PlaybackController | [previous](/CIC/References/APIs/PlaybackController.md#previous)  | Instructs your client to start playback of the previous audio stream in a playback queue.  |
| PlaybackController | [resume](/CIC/References/APIs/PlaybackController.md#resume)  | Instructs your client to resume playback of the audio stream.  |
| PlaybackController | [stop](/CIC/References/APIs/PlaybackController.md#stop)  | Instructs your client to stop playback of the audio stream.  |
| PlaybackController | [TurnOffRepeatMode](/CIC/References/APIs/PlaybackController.md#TurnOffRepeatMode) | Instructs your client to turn off the repeat mode.  |
| PlaybackController | [TurnOnRepeatMode](/CIC/References/APIs/PlaybackController.md#TurnOnRepeatMode) | Instructs your client to turn on the repeat mode.  |
| PlaybackController | [unmute](/CIC/References/APIs/PlaybackController.md#unmute)  | Instructs your client to unmute the speaker volume.  |
| PlaybackController | [volumeDown](/CIC/References/APIs/PlaybackController.md#volumeDown)  | Instructs your client to turn down the speaker volume.  |
| PlaybackController | [volumeUp](/CIC/References/APIs/PlaybackController.md#volumeUp)  | Instructs your client to turn up the speaker volume.  |
| SpeechRecognizer  | [ExpectSpeech](/CIC/References/APIs/SpeechRecognizer.md#ExpectSpeech) | Instructs your client to prepare to listen to the user's speech input.  |
| SpeechRecognizer  | [ShowRecognizedText](/CIC/References/APIs/SpeechRecognizer.md#ShowRecognizedText) | Delivers the recognized speech input to your client in real time using a natural language.  |
| SpeechRecognizer  | [StopCapture](/CIC/References/APIs/SpeechRecognizer.md#StopCapture)  | Instructs your client to stop capturing the user's speech input.  |
| SpeechSynthesizer  | [Speak](/CIC/References/APIs/SpeechSynthesizer#Speak)  | Instructs your client to play the synthesized TTS audio file with its speaker.  |
