# Event messages index

| Namespace  | Message name  | Description  |
|-------------------|----------------|-------------------------------------------------|
| AudioPlayer  | [PlayFinished](/CIC/References/APIs/AudioPlayer.md#PlayFinished) | Reports to CIC on audio stream details when your client finishes playback of an audio stream.  |
| AudioPlayer  | [PlayPaused](/CIC/References/APIs/AudioPlayer.md#PlayPaused)  | Reports to CIC on audio stream details when your client pauses playback of an audio stream.  |
| AudioPlayer  | [PlayResumed](/CIC/References/APIs/AudioPlayer.md#PlayResumed)  | Reports to CIC on audio stream details when your client resumes playback of an audio stream.  |
| AudioPlayer  | [PlayStarted](/CIC/References/APIs/AudioPlayer.md#PlayStarted)  | Reports to CIC on audio stream details when your client starts playback of an audio stream.  |
| AudioPlayer  | [PlayStopped](/CIC/References/APIs/AudioPlayer.md#PlayStopped)  | Reports to CIC on audio stream details when your client stops playback of an audio stream.  |
| AudioPlayer  | [ProgressReportDelayPassed](/CIC/References/APIs/AudioPlayer.md#ProgressReportPositionPassed) | Reports to CIC on a current playback state ([AudioPlayer.PlaybackState](/CIC/References/Context_Objects.md#PlaybackState)) after a specified delay time has passed since playback of an audio stream has started. You can check the delay time for each audio stream when an [AudioPlayer.Play](/CIC/References/APIs/AudioPlayer.md#Play) directive message is returned to your client. |
| AudioPlayer  | [ProgressReportIntervalPassed](/CIC/References/APIs/AudioPlayer.md#ProgressReportPositionPassed)| Reports to CIC on a current playback state ([AudioPlayer.PlaybackState](/CIC/References/Context_Objects.md#PlaybackState)) regularly at a specified interval of time after playback of an audio stream has started. You can check the reporting interval for each audio stream when an [AudioPlayer.Play](/CIC/References/APIs/AudioPlayer.md#Play) directive message is returned to your client. |
| AudioPlayer  | [ProgressReportPositionPassed](/CIC/References/APIs/AudioPlayer.md#ProgressReportPositionPassed) | Reports to CIC on a current playback state ([AudioPlayer.PlaybackState](/CIC/References/Context_Objects.md#PlaybackState)) at a specified reporting point after playback of an audio stream has started. You can check the reporting point for each audio stream when an [AudioPlayer.Play](/CIC/References/APIs/AudioPlayer.md#Play) directive message is returned to your client. |
| AudioPlayer  | [AudioPlayer.StreamRequested](/CIC/References/APIs/AudioPlayer.md#StreamRequested) | Requests CIC for more audio stream details necessary for playback, such as a streaming URL. |
| Memo  | [Created](/CIC/References/APIs/Memo.md#Created)  | Requests CIC to create a specified memo.  |
| Memo  | [Deleted](/CIC/References/APIs/Memo.md#Deleted)  | Requests CIC to delete a specified memo.  |
| Memo  | [Get](/CIC/References/APIs/Memo.md#Get)  | Requests CIC to get a full list of memos created by a user.  |
| Memo  | [Updated](/CIC/References/APIs/Memo.md#Updated)  | Requests CIC to update a specified memo.  |
| Reminder  | [Created](/CIC/References/APIs/Reminder.md#Created)  | Requests CIC to create a specified reminder.  |
| Reminder  | [Deleted](/CIC/References/APIs/Reminder.md#Deleted)  | Requests CIC to delete a specified reminder.  |
| Reminder  | [Get](/CIC/References/APIs/Reminder.md#Get)  | Requests CIC to get a full list of reminders created by a user.  |
| Reminder  | [Updated](/CIC/References/APIs/Reminder.md#Updated)  | Requests CIC to update a specified reminder.  |
| SpeechRecognizer  | [ExpectSpeechTimedOut](/CIC/References/APIs/SpeechRecognizer.md#ExpectSpeechTimedOut) | Reports to CIC that the specified waiting time for speech input has timed out.  |
| SpeechRecognizer  | [Recognize](/CIC/References/APIs/SpeechRecognizer.md#Recognize)  | Requests CIC to recognize speech input coming in from a user.  |
| SpeechSynthesizer | [Request](/CIC/References/APIs/SpeechSynthesizer.md#Request)  | Requests CIC to synthesize specified text into a TTS audio file.  |