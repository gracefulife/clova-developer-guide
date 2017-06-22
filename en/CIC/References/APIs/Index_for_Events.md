# Event messages index

| Namespace  | Message name  | Description  |
|-------------------|----------------|-------------------------------------------------|
| AudioPlayer  | [PlayFinished](/CIC/References/APIs/AudioPlayer.md#PlayFinished) | Used to report to CIC on details of the audio stream when your client finishes playback of the audio stream.  |
| AudioPlayer  | [PlayPaused](/CIC/References/APIs/AudioPlayer.md#PlayPaused)  | Used to report to CIC on details of the audio stream when your client pauses playback of the audio stream.  |
| AudioPlayer  | [PlayResumed](/CIC/References/APIs/AudioPlayer.md#PlayResumed)  | Used to report to CIC on details of the audio stream when your client resumes playback of the audio stream.  |
| AudioPlayer  | [PlayStarted](/CIC/References/APIs/AudioPlayer.md#PlayStarted)  | Used to report to CIC on details of the audio stream when your client starts playback of the audio stream.  |
| AudioPlayer  | [PlayStopped](/CIC/References/APIs/AudioPlayer.md#PlayStopped)  | Used to report to CIC on details of the audio stream when your client stops playback of the audio stream.  |
| AudioPlayer  | [ProgressReportDelayPassed](/CIC/References/APIs/AudioPlayer.md#ProgressReportPositionPassed) | Used to report to CIC on the current playback state ([AudioPlayer.PlaybackState](/CIC/References/Context_Objects.md#PlaybackState)) after the sepcified delay time has passed from the start of the playback. You can check the delay time for each audio stream when an [AudioPlayer.Play](/CIC/References/APIs/AudioPlayer.md#Play) Directive message is delivered to your client. |
| AudioPlayer  | [ProgressReportIntervalPassed](/CIC/References/APIs/AudioPlayer.md#ProgressReportPositionPassed) | Used to report to CIC on the current playback state ([AudioPlayer.PlaybackState](/CIC/References/Context_Objects.md#PlaybackState)) at regular intervals of time specified since the start of the playback. You can check the reporting interval for each audio stream when an [AudioPlayer.Play](/CIC/References/APIs/AudioPlayer.md#Play) Directive message is delivered to your client. |
| AudioPlayer  | [ProgressReportPositionPassed](/CIC/References/APIs/AudioPlayer.md#ProgressReportPositionPassed) | Used to report to CIC on the current playback state ([AudioPlayer.PlaybackState](/CIC/References/Context_Objects.md#PlaybackState)) at the specified reporting point after the playback has started. You can check the reporting point for each audio stream when an [AudioPlayer.Play](/CIC/References/APIs/AudioPlayer.md#Play) Directive message is delivered to your client. |
| AudioPlayer  | [AudioPlayer.StreamRequested](/CIC/References/APIs/AudioPlayer.md#StreamRequested) | This is an Event message which makes a request to CIC to provide additional information necessary for playback of the audio stream such as a streaming URL. |
| Memo  | [Created](/CIC/References/APIs/Memo.md#Created)  | Asks CIC to create a memo.  |
| Memo  | [Deleted](/CIC/References/APIs/Memo.md#Deleted)  | Asks CIC to delete a memo.  |
| Memo  | [Get](/CIC/References/APIs/Memo.md#Get)  | Asks CIC to provide the full list of memos created by the user.  |
| Memo  | [Updated](/CIC/References/APIs/Memo.md#Updated)  | Asks CIC to update a memo.  |
| Reminder  | [Created](/CIC/References/APIs/Reminder.md#Created)  | Asks CIC to create a reminder.  |
| Reminder  | [Deleted](/CIC/References/APIs/Reminder.md#Deleted)  | Asks CIC to delete a reminder.  |
| Reminder  | [Get](/CIC/References/APIs/Reminder.md#Get)  | Asks CIC to provide the full list of reminders created by the user.  |
| Reminder  | [Updated](/CIC/References/APIs/Reminder.md#Updated)  | Asks CIC to update a reminder.  |
| SpeechRecognizer  | [ExpectSpeechTimedOut](/CIC/References/APIs/SpeechRecognizer.md#ExpectSpeechTimedOut) | Reports to CIC that the specified waiting time for speech input has timed out.  |
| SpeechRecognizer  | [Recognize](/CIC/References/APIs/SpeechRecognizer.md#Recognize)  | Transmits user's speech input to CIC and asks to recognize it.  |
| SpeechSynthesizer | [Request](/CIC/References/APIs/SpeechSynthesizer.md#Request)  | Asks CIC to synthesize texts into a TTS audio file.  |