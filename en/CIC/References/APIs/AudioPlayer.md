# AudioPlayer

This API is used when your client requests playback of an audio stream or reports to CIC on the events that occur during playback. The AudioPlayer API provides the following Event and Directive messages.

| Message name  | Message type  | Message description  |
|------------------|-----------|---------------------------------------------|
| [Play](#Play)  | Directive | Instructs your client to start playback of the audio stream or add it to a playback queue.  |
| [PlayFinished](#PlayFinished)  | Event  | Used to report to CIC on details of the audio stream when your client finishes playback of the audio stream.  |
| [PlayNext](#PlayNext)  | Directive | Instructs your client to stop playback of the current audio stream and start playback of the next one in a playback queue. |
| [PlayPaused](#PlayPaused)  | Event  | Used to report to CIC on details of the audio stream when your client pauses playback of the audio stream. |
| [PlayResumed](#PlayResumed)  | Event  | Used to report to CIC on details of the audio stream when your client resumes playback of the audio stream.  |
| [PlayStarted](#PlayStarted)  | Event  | Used to report to CIC on details of the audio stream when your client starts playback of the audio stream.  |
| [PlayStopped](#PlayStopped)  | Event  | Used to report to CIC on details of the audio stream when your client stops playback of the audio stream.  |
| [ProgressReportDelayPassed](#ProgressReportPositionPassed) | Event | Used to report to CIC on the current playback state ([AudioPlayer.PlaybackState](/CIC/References/Context_Objects.md#PlaybackState)) after the specified delay time has passed since the start of the playback. You can check the delay time for each audio stream when an [AudioPlayer.Play](#Play) Directive message is delivered to your client. |
| [ProgressReportIntervalPassed](#ProgressReportPositionPassed)| Event | Used to report to CIC on the current playback state ([AudioPlayer.PlaybackState](/CIC/References/Context_Objects.md#PlaybackState)) at regular intervals of time specified since the start of the playback. You can check the reporting interval for each audio stream when an [AudioPlayer.Play](#Play) Directive message is delivered to your client.
| [ProgressReportPositionPassed](#ProgressReportPositionPassed) | Event | Used to report to CIC on the current playback state ([AudioPlayer.PlaybackState](/CIC/References/Context_Objects.md#PlaybackState)) at the specified reporting point after the playback has started. You can check the reporting point for each audio stream when an [AudioPlayer.Play](#Play) Directive message is delivered to your client.
| [Stop](#Stop)  | Directive | Instructs your client to stop playback of the audio stream.  |
| [StreamDeliver](#StreamDeliver)  | Directive | This message is sent in response to an [AudioPlayer.StreamRequested](#StreamRequested) Event message. It is sent when your client needs to receive details of the audio stream necessary for playback. |
| [StreamRequested](#StreamRequested) | Event  | This Event message makes a request to CIC to provide additional information necessary for playback of the audio stream such as a streaming URL.  |

## Play Directive {#Play}
Instructs your client to start playback of the audio stream or add it to a playback queue.

### Payload field
| Field name  | Type  | Field description  | Required |
|---------------|---------|-----------------------------|---------|
| audioItem  | AudioItemObject | The object containing metadata of the audio stream and audio stream details necessary for playback  | Yes |
| audioItem.audioItemId  | string  | The ID that identifies the audio stream details. You client may use this value to remove any redundant Play Directive message. | Yes |
| audioItem.stream  | [AudioStreamObject](#AudioStreamObject) | The object containing details of the audio stream necessary for playback  | Yes |
| audioItem.[CustomField] | any  | A service provider may add extra metadata to the audio stream.  | No |
| playBehavior  | string  | A delimiter that determines when your client should start playback of the audio stream contained in the Directive message. <ul><li>"REPLACE_ALL": Clear all existing playback queues and start playback of the audio stream.</li><li>"ENQUEUE": Add the audio stream to a playback queue.</li></ul> | Yes |

### Remarks
Sometimes, due to the way music services charge users, specific streaming details such as a streaming URL can only be obtained right before playback. In this case, audio stream details in the Play Directive message may not have URL data. Therefore, when your client wants to play an audio stream but is missing URL information, it should send an [AudioPlayer.StreamRequested](#StreamRequested) Event message to request additional audio stream details.

### Message example
{% raw %}
```json
{
    "directive": {
        "header": {
            "dialogRequestId": "dialog-id-here-1",
            "messageId": "168cc207-8743-4bf8-be7d-723c58614aa2",
            "name": "Play",
            "namespace": "AudioPlayer"
        },
        "payload": {
            "audioItem": {
                "audioItemId": "5313c879-25bb-461c-93fc-f85d95edf2a0",
                "id": "TR-NM-3958459",
                "albumTitle": "3\uc9d1 Modern Times",
                "artists": ["\uc544\uc774\uc720(IU)"],
                "title": "\uc2eb\uc740 \ub0a0",
                "lyrics": "\ud0a4 \ud070 ...",
                "stream": {
                    "beginAtInMilliseconds": 0,
                    "progressReport": {
                        "progressReportDelayInMilliseconds": null,
                        "progressReportIntervalInMilliseconds": null,
                        "progressReportPositionInMilliseconds": 60000
                    },
                    "token": "b767313e-6790-4c28-ac18-5d9f8e432248",
                    "url": "https://aod.musicservice.net/b767313e.mp3"
                },
            },
            "playBehavior": "ENQUEUE"
        }
    }
}
```
{% endraw %}

### See also
* [AudioPlayer.PlayNext](#PlayNext)
* [AudioPlayer.PlayPaused](#PlayPaused)
* [AudioPlayer.PlayResumed](#PlayResumed)
* [AudioPlayer.PlayStarted](#PlayStarted)
* [AudioPlayer.PlayStopped](#PlayStopped)
* [AudioPlayer.ProgressReportDelayPassed](#ProgressReportDelayPassed)
* [AudioPlayer.ProgressReportIntervalPassed](#ProgressReportIntervalPassed)
* [AudioPlayer.ProgressReportPositionPassed](#ProgressReportPositionPassed)
* [AudioPlayer.Stop](#Stop)
* [AudioPlayer.StreamRequested](#StreamRequested)

## PlayFinished Event {#PlayFinished}
Used to report to CIC on details of the audio stream when your client finishes playback of the audio stream.

### Context field
Make sure to send the following [context information](/CIC/References/Context_Objects.md) together.

* [AudioPlayer.PlaybackState](/CIC/References/Context_Objects.md#PlaybackState)

### Payload field
None

### Message example
{% raw %}
```json
{
  "context": [
    {{AudioPlayer.PlaybackState}},
  ],
  "event": {
    "header": {
      "namespace": "AudioPlayer",
      "name": "PlayFinished",
      "dialogRequestId": "277b40c3-b046-4f61-a551-783b1547e7b7",
      "messageId": "4e4080d6-c440-498a-bb73-ae86c6312806"
    },
    "payload": {}
  }
}
```
{% endraw %}

### See also
* [AudioPlayer.Play](#Play)

## PlayNext Directive {#PlayNext}
Instructs your client to stop playback of the current audio stream and start playback of the next one in a playback queue.

### Payload field
None

### Message example
{% raw %}
```json
{
    "directive": {
        "header": {
            "dialogRequestId": "dialog-id-here-1",
            "messageId": "b1f88d7d-bbb8-44fa-a0a2-c5a7553e6f8a",
            "name": "PlayNext",
            "namespace": "AudioPlayer"
        },
        "payload": null
    }
}
```
{% endraw %}

### See also
* [AudioPlayer.Play](#Play)

## PlayPaused Event {#PlayPaused}
Used to report to CIC on details of the audio stream when your client pauses playback of the audio stream. This Event message is sent in the following scenario.

1. Using a [SpeechRecognizer.Recognize](/CIC/References/APIs/SpeechRecognizer.md#Recognize) Event message, your client transmits user's speech input to CIC asking to pause playback of the audio stream.
2. Once the Clova platform recognizes this request, CIC sends the request to your client using a [PlaybackController.pause](/CIC/References/APIs/PlaybackController.md#pause) Directive message.
3. Your client pauses the playback and sends a PlayPaused Event message to CIC.

### Context field
Make sure to send the following [context information](/CIC/References/Context_Objects.md) together.

* [AudioPlayer.PlaybackState](/CIC/References/Context_Objects.md#PlaybackState)

### Payload field
None

### Message example
{% raw %}
```json
{
  "context": [
    {{AudioPlayer.PlaybackState}},
  ],
  "event": {
    "header": {
      "namespace": "AudioPlayer",
      "name": "PlayPaused",
      "dialogRequestId": "277b40c3-b046-4f61-a551-783b1547e7b7",
      "messageId": "4e4080d6-c440-498a-bb73-ae86c6312806"
    },
    "payload": {}
  }
}
```
{% endraw %}

### See also
* [AudioPlayer.Play](#Play)
* [AudioPlayer.PlayResumed](#PlayResumed)
* [PlaybackController.pause](/CIC/References/APIs/PlaybackController.md#pause)

## PlayResumed Event {#PlayResuemd}
Used to report to CIC on details of the audio stream when your client resumes playback of the audio stream. This Event message is sent in the following scenario.

1. Using a [SpeechRecognizer.Recognize](/CIC/References/APIs/SpeechRecognizer.md#Recognize) Event message, your client transmits user's speech input to CIC asking to resume playback of the audio stream.
2. Once the Clova platform recognizes this request, CIC sends the request to your client using a [PlaybackController.resume](/CIC/References/APIs/PlaybackController.md#resume) Directive message.
3. Your client resumes the playback and sends a PlayResumed Event message to CIC.

### Context field
Make sure to send the following [context information](/CIC/References/Context_Objects.md) together.

* [AudioPlayer.PlaybackState](/CIC/References/Context_Objects.md#PlaybackState)

### Payload field
None

### Message example
{% raw %}
```json
{
  "context": [
    {{AudioPlayer.PlaybackState}},
  ],
  "event": {
    "header": {
      "namespace": "AudioPlayer",
      "name": "PlayResumed",
      "dialogRequestId": "277b40c3-b046-4f61-a551-783b1547e7b7",
      "messageId": "4e4080d6-c440-498a-bb73-ae86c6312806"
    },
    "payload": {}
  }
}
```
{% endraw %}

### See also
* [AudioPlayer.Play](#Play)
* [AudioPlayer.PlayPaused](#PlayPaused)
* [PlaybackController.resume](/CIC/References/APIs/PlaybackController.md#resume)

## PlayStarted Event {#PlayStarted}
Used to report to CIC on details of the audio stream when your client starts playback of the audio stream.

### Context field
Make sure to send the following [context information](/CIC/References/Context_Objects.md) together.

* [AudioPlayer.PlaybackState](/CIC/References/Context_Objects.md#PlaybackState)

### Payload field
None

### Message example
{% raw %}
```json
{
  "context": [
    {{AudioPlayer.PlaybackState}},
  ],
  "event": {
    "header": {
      "namespace": "AudioPlayer",
      "name": "PlayStarted",
      "dialogRequestId": "277b40c3-b046-4f61-a551-783b1547e7b7",
      "messageId": "4e4080d6-c440-498a-bb73-ae86c6312806"
    },
    "payload": {}
  }
}
```
{% endraw %}

### See also
* [AudioPlayer.Play](#Play)
* [AudioPlayer.PlayStopped](#PlayStopped)

## PlayStopped Event {#PlayStopped}
Used to report to CIC on details of the audio stream when your client stops playback of the audio stream. This Event message is sent in the following scenario.

1. Using a [SpeechRecognizer.Recognize](/CIC/References/APIs/SpeechRecognizer.md#Recognize) Event message, your client transmits user's speech input to CIC asking to stop playback of the audio stream.
2. Once the Clova platform recognizes this request, CIC sends the request to your client using a [PlaybackController.stop](/CIC/References/APIs/PlaybackController.md#stop) Directive message.
3. Your client pauses the playback and sends a PlayStopped Event message to CIC.

### Context field
Make sure to send the following [context information](/CIC/References/Context_Objects.md) together.

* [AudioPlayer.PlaybackState](/CIC/References/Context_Objects.md#PlaybackState)

### Payload field
None

### Message example
{% raw %}
```json
{
  "context": [
    {{AudioPlayer.PlaybackState}},
  ],
  "event": {
    "header": {
      "namespace": "AudioPlayer",
      "name": "PlayStopped",
      "dialogRequestId": "277b40c3-b046-4f61-a551-783b1547e7b7",
      "messageId": "4e4080d6-c440-498a-bb73-ae86c6312806"
    },
    "payload": {}
  }
}
```
{% endraw %}

### See also
* [AudioPlayer.Play](#Play)
* [AudioPlayer.PlayStarted](#PlayStarted)
* [PlaybackController.stop](/CIC/References/APIs/PlaybackController.md#stop)

## ProgressReportDelayPassed Event {#ProgressReportDelayPassed}
Used to report to CIC on the current playback state ([AudioPlayer.PlaybackState](/CIC/References/Context_Objects.md#PlaybackState)) after the specified delay time has passed since the start of the playback. You can check the delay time for each audio stream when an [AudioPlayer.Play](#Play) Directive message is delivered to your client.

### Context field
Make sure to send the following [context information](/CIC/References/Context_Objects.md) together.

* [AudioPlayer.PlaybackState](/CIC/References/Context_Objects.md#PlaybackState)

### Payload field
None

### Message example
{% raw %}
```json
{
  "context": [
    {{AudioPlayer.PlaybackState}},
  ],
  "event": {
    "header": {
      "namespace": "AudioPlayer",
      "name": "ProgressReportDelayPassed",
      "dialogRequestId": "277b40c3-b046-4f61-a551-783b1547e7b7",
      "messageId": "4e4080d6-c440-498a-bb73-ae86c6312806"
    },
    "payload": {}
  }
}
```
{% endraw %}

### See also
* [AudioPlayer.Play](#Play)
* [AudioPlayer.ProgressReportIntervalPassed](#ProgressReportIntervalPassed)
* [AudioPlayer.ProgressReportPositionPassed](#ProgressReportPositionPassed)

## ProgressReportIntervalPassed Event {#ProgressReportIntervalPassed}
Used to report to CIC on the current playback state ([AudioPlayer.PlaybackState](/CIC/References/Context_Objects.md#PlaybackState)) at regular intervals of time specified since the start of the playback. You can check the reporting interval for each audio stream when an [AudioPlayer.Play](#Play) Directive message is delivered to your client.

### Context field
Make sure to send the following [context information](/CIC/References/Context_Objects.md) together.

* [AudioPlayer.PlaybackState](/CIC/References/Context_Objects.md#PlaybackState)

### Payload field
None

### Message example
{% raw %}
```json
{
  "context": [
    {{AudioPlayer.PlaybackState}},
  ],
  "event": {
    "header": {
      "namespace": "AudioPlayer",
      "name": "ProgressReportIntervalPassed",
      "dialogRequestId": "277b40c3-b046-4f61-a551-783b1547e7b7",
      "messageId": "4e4080d6-c440-498a-bb73-ae86c6312806"
    },
    "payload": {}
  }
}
```
{% endraw %}

### See also
* [AudioPlayer.Play](#Play)
* [AudioPlayer.ProgressReportDelayPassed](#ProgressReportDelayPassed)
* [AudioPlayer.ProgressReportPositionPassed](#ProgressReportPositionPassed)

## ProgressReportPositionPassed Event {#ProgressReportPositionPassed}
Used to report to CIC on the current playback state ([AudioPlayer.PlaybackState](/CIC/References/Context_Objects.md#PlaybackState)) at the specified reporting point after the playback has started. You can check the reporting point for each audio stream when an [AudioPlayer.Play](#Play) Directive message is delivered to your client.

### Context field
Make sure to send the following [context information](/CIC/References/Context_Objects.md) together.

* [AudioPlayer.PlaybackState](/CIC/References/Context_Objects.md#PlaybackState)

### Payload field
None

### Message example
{% raw %}
```json
{
  "context": [
    {{AudioPlayer.PlaybackState}},
  ],
  "event": {
    "header": {
      "namespace": "AudioPlayer",
      "name": "ProgressReportPositionPassed",
      "dialogRequestId": "277b40c3-b046-4f61-a551-783b1547e7b7",
      "messageId": "4e4080d6-c440-498a-bb73-ae86c6312806"
    },
    "payload": {}
  }
}
```
{% endraw %}

### See also
* [AudioPlayer.Play](#Play)
* [AudioPlayer.ProgressReportDelayPassed](#ProgressReportDelayPassed)
* [AudioPlayer.ProgressReportIntervalPassed](#ProgressReportIntervalPassed)

## Stop Directive {#Stop}
Instructs your client to stop playback of the audio stream.

### Payload field
None

### Message example
{% raw %}
```json
{
    "directive": {
        "header": {
            "dialogRequestId": "dialog-id-here-1",
            "messageId": "b1f88d7d-bbb8-44fa-a0a2-c5a7553e6f8a",
            "name": “Stop”,
            "namespace": "AudioPlayer"
        },
        "payload": {}
    }
}
```
{% endraw %}

### See also
* [AudioPlayer.Play](#Play)
* [AudioPlayer.Started](#PlayStarted)
* [AudioPlayer.Stopped](#PlayStopped)

## StreamDeliver Directive {#StreamDeliver}
This message is sent in response to an [AudioPlayer.StreamRequested](#StreamRequested) Event message. It is sent when your client needs to receive details of the audio stream for playback. A streaming URL is always included in audio stream details so that your client can play the music.

### Payload field
| Field name | Type | Field description | Required |
|---------|------|--------|---------|
| audioItemId | string | The value that identifies the audio stream details. You client may use this value to remove any redundant Play Directive message. | Yes |
| audioStream | [AudioStreamObject](#AudioStreamObject) | The object containing audio stream details necessary for playback  | Yes |

### Remarks
You can implement audio stream playback by combining a StreamDeliver Directive message and the *payload.audioStream* message body of the previously received [Play](#Play) Directive message. However, you must not replace the values of the previous Play Directive message with the new values of the StreamDeliver Directive message. The reason is that if there is any content in the previous Play Directive message that overlaps with the AudioStreamObject content in the StreamDeliver Directive message, that overlapping content can be omitted. This may cause unexpected behaviors when your client handles the same Play Directive message more than twice such as repeat playback or playback of a previous song.

### Message example
{% raw %}
```json
{
  "directive": {
    "header": {
      "namespace": "AudioPlayer",
      "name": "StreamDeliver",
      "dialogRequestId": "277b40c3-b046-4f61-a551-783b1547e7b7",
      "messageId": "4e4080d6-c440-498a-bb73-ae86c6312806"
    },
    "payload": {
        "audioItemId": "5313c879-25bb-461c-93fc-f85d95edf2a0",
        "stream": {
            "token": "b767313e-6790-4c28-ac18-5d9f8e432248",
            "url": "https://aod.musicservice.net/b767313e.mp3"
        }
    }
  }
}
```
{% endraw %}

### See also
* [AudioPlayer.Play](#Play)
* [AudioPlayer.StreamRequested](#StreamRequested)

## StreamRequested Event {#StreamRequested}
This Event message makes a request to CIC to provide additional information necessary for playback of the audio stream such as a streaming URL.

### Context field
None

### Events field
| Field name  | Type  | Field description  | Required |
|---------------|---------|-----------------------------|---------|
| audioItemId  | string  | audioItemId of the Play Directive message  | Yes |
| audioStream  | [AudioStreamObject](#AudioStreamObject) | audioItem.stream of the Play Directive message | Yes |

### Remarks
Sometimes, due to the way music services charge users, providing specific streaming details must be delayed till right before playback. This Event message is used when audio stream details should not be ready too early. As such, your client must not deliver this Event message earlier than right before playback.

### Message example
{% raw %}
```json
{
  "context": [],
  "event": {
    "header": {
      "namespace": "AudioPlayer",
      "name": "StreamRequested",
      "messageId": "msg-id-here-1",
      "dialogRequestId": "dialog-id-here-1"
    },
    "payload": {
        "audioStream": {
	        "token": "TR-NM-4435786",
	        "url": "clova:TR-NM-4435786"
        }
    }
  }
}
```
{% endraw %}

### See also
* [AudioPlayer.Play](#Play)
* [AudioPlayer.StreamDeliver](#StreamDeliver)

## Shared objects
Include the following shared objects in a message body (payload) when Event or Directive messages are sent using the AudioPlayer API.

| Object name  | Object description  |
|--------------------|---------------------------------------------------|
| [AudioStreamObject](#AudioStreamObject) | The object containing playback details of the sone such as a streaming address, credentials |

### AudioStreamObject {#AudioStreamObject}
This object contains streaming details of the audio stream necessary for playback. It is used when CIC sends details of playback streaming to your client or when your client sends streaming details of the currently playing music to CIC.

#### Object field
| Field name  | Type  | Field description  | Required |
|---------------|---------|-----------------------------|---------|
| beginAtInMilliseconds | number | The starting point of playback. If this field is specified as a non-zero value, the client must play the audio stream from that point. If this field is specified as 0, the client must play the audio stream from the beginning. Unit is a millisecond. | Yes |
| progressReport  | object  | The object that specifies the time to report on the playback state after the playback has started  | No |
| progressReport.progressReportDelayInMilliseconds | number | The value is used to report on the playback state after the specified time has passed since the start of the playback.  | No |
| progressReport.progressReportIntervalInMilliseconds | number | The value is used to report on the playback state at regular intervals of time specified during the playback.  | No |
| progressReport.progressReportPositionInMilliseconds | number | The value is used to report on the playback start at each specified point during the playback.  | No |
| token  | string  | Audio stream URL  | Yes |
| url  | string  | Audio stream token  | Yes |
| [Custom Field]  | any  | A service provider may use this field to add any context information necessary for playback of the audio stream.  | No |

#### Object Example
{% raw %}
```json
{
  "beginAtInMilliseconds": 0,
  "progressReport": {
      "progressReportDelayInMilliseconds": null,
      "progressReportIntervalInMilliseconds": null,
      "progressReportPositionInMilliseconds": 60000
  },
  "token": "TR-NM-4435786",
  "url": "clova:TR-NM-4435786"
}
```
{% endraw %}

#### See also
* [AudioPlayer.Play](#Play)
* [AudioPlayer.progressReportDelayInMilliseconds](#progressReportDelayInMilliseconds)
* [AudioPlayer.ProgressReportDelayPassed](#ProgressReportDelayPassed)
* [AudioPlayer.ProgressReportIntervalPassed](#ProgressReportIntervalPassed)
* [AudioPlayer.PlaybackState](/CIC/References/Context_Objects.md#PlaybackState)
