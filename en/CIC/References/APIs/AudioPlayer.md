# AudioPlayer

Instructs your client to play an audio stream or reports to CIC on events that occur during playback. The AudioPlayer API provides the following event and directive messages.

| Message name         | Message type  | Message description                                   |
|------------------|-----------|---------------------------------------------|
| [Play](#Play)                       | Directive | Instructs your client to start playback of an audio stream or add it to a playback queue.                         |
| [PlayFinished](#PlayFinished)       | Event     | Reports to CIC on audio stream details when your client finishes playback of an audio stream.     |
| [PlayNext](#PlayNext)               | Directive | Instructs your client to stop playback of a current audio stream and start playback of a next audio stream in a playback queue. |
| [PlayPaused](#PlayPaused)           | Event     | Reports to CIC on audio stream details when your client pauses playback of an audio stream. |
| [PlayResumed](#PlayResumed)         | Event     | Reports to CIC on audio stream details when your client resumes playback of an audio stream.         |
| [PlayStarted](#PlayStarted)         | Event     | Reports to CIC on audio stream details when your client starts playback of an audio stream.    |
| [PlayStopped](#PlayStopped)         | Event     | Reports to CIC on audio stream details when your client stops playback of an audio stream.    |
| [ProgressReportDelayPassed](#ProgressReportPositionPassed) | Event | Reports to CIC on a current playback state ([AudioPlayer.PlaybackState](/CIC/References/Context_Objects.md#PlaybackState)) after a specified delay time has passed since your client has started playback of an audio stream. You can check the delay time for each audio stream when an [AudioPlayer.Play](#Play) directive message is returned to your client. |
| [ProgressReportIntervalPassed](#ProgressReportPositionPassed)| Event | Reports to CIC on a current playback state ([AudioPlayer.PlaybackState](/CIC/References/Context_Objects.md#PlaybackState)) regularly at a specified interval of time after your client has started playback of an audio stream. You can check the reporting interval for each audio stream when an [AudioPlayer.Play](#Play) directive message is returned to your client. |
| [ProgressReportPositionPassed](#ProgressReportPositionPassed) | Event | Reports to CIC on a current playback state ([AudioPlayer.PlaybackState](/CIC/References/Context_Objects.md#PlaybackState)) at a specified reporting point after your client started playback of an audio stream. You can check the reporting point for each audio stream when an [AudioPlayer.Play](#Play) directive message is returned to your client. |
| [Stop](#Stop)                       | Directive | Instructs your client to stop playback of an audio stream.                                            |
| [StreamDeliver](#StreamDeliver)     | Directive | Returns audio stream details necessary for music playback. This is a response message to an [AudioPlayer.StreamRequested](#StreamRequested) event message. |
| [StreamRequested](#StreamRequested) | Event     | Requests CIC for more audio stream details necessary for playback, such as a streaming URL.               |

## Play directive {#Play}
Instructs your client to play an audio stream or add it to a playback queue.

### Payload field
| Field name       | Type    | Field description                     | Required |
|---------------|---------|-----------------------------|---------|
| audioItem               | AudioItemObject | An object that contains audio stream metadata and audio stream details necessary for playback                     | Yes |
| audioItem.audioItemId   | string          | An ID for identifying audio stream details. You can use this value to remove any redundant Play directive messages. | Yes |
| audioItem.stream        | [AudioStreamObject](#AudioStreamObject) | An object that contains audio stream details necessary for playback                        | Yes |
| audioItem.[CustomField] | any             | Service providers can add extra metadata to an audio stream for playback.                     | No |
| playBehavior            | string         | A delimiter that determines when to start playback of an audio stream contained in a directive message <ul><li>"REPLACE_ALL": Clears all existing playback queues and starts playback of the returned audio stream.</li><li>"ENQUEUE": Adds the returned audio stream to a playback queue.</li></ul> | Yes |

### Remarks
Sometimes, due to the way music services charge users, streaming details such as a streaming URL can only be obtained right before playback. In this case, audio stream details contained in a Play directive message may be missing URL information. If URL information is missing, you must send an [AudioPlayer.StreamRequested](#StreamRequested) event message to request necessary audio stream information.

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

## PlayFinished event {#PlayFinished}
Reports to CIC on audio stream details when your client finishes playback of an audio stream.

### Context field
Send the following [context information](/CIC/References/Context_Objects.md) together.

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

## PlayNext directive {#PlayNext}
Instructs your client to stop playback of a current audio stream and start playback of a next audio stream in a playback queue.

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

## PlayPaused event {#PlayPaused}
Reports to CIC on audio stream details when your client pauses playback of an audio stream. Send this event message in the following scenario.

1. Your client sends CIC a user's spoken request for pausing playback of an audio stream, using a [SpeechRecognizer.Recognize](/CIC/References/APIs/SpeechRecognizer.md#Recognize) event message.
2. The Clova platform recognizes the pause request and CIC returns it to your client, using a [PlaybackController.pause](/CIC/References/APIs/PlaybackController.md#pause) directive message.
3. Your client pauses playback of the audio stream and sends CIC a PlayPaused event message.

### Context field
Send the following [context information](/CIC/References/Context_Objects.md) together.

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

## PlayResumed event {#PlayResuemd}
Reports to CIC on audio stream details when your client resumes playback of an audio stream. Send this event message in the following scenario.

1. Your client sends CIC a user's spoken request for resuming playback of an audio stream, using a [SpeechRecognizer.Recognize](/CIC/References/APIs/SpeechRecognizer.md#Recognize) event message.
2. The Clova platform recognizes the resume request and CIC returns it to your client, using a [PlaybackController.resume](/CIC/References/APIs/PlaybackController.md#resume) directive message.
3. Your client resumes playback of the audio stream and sends CIC a PlayResumed event message.

### Context field
Send the following [context information](/CIC/References/Context_Objects.md) together.

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

## PlayStarted event {#PlayStarted}
Reports to CIC on audio stream details when your client starts playback of an audio stream.

### Context field
Send the following [context information](/CIC/References/Context_Objects.md) together.

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

## PlayStopped event {#PlayStopped}
Reports to CIC on audio stream details when your client stops playback of an audio stream. Send this event message in the following scenario.

1. Your client sends CIC a user's spoken request for stopping playback of an audio stream, using a [SpeechRecognizer.Recognize](/CIC/References/APIs/SpeechRecognizer.md#Recognize) event message.
2. The Clova platform recognizes the stop request and CIC returns it to your client, using a [PlaybackController.stop](/CIC/References/APIs/PlaybackController.md#stop) directive message.
3. Your client pauses playback of the audio stream and sends CIC a PlayStopped event message.

### Context field
Send the following [context information](/CIC/References/Context_Objects.md) together.

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

## ProgressReportDelayPassed event {#ProgressReportDelayPassed}
Reports to CIC on a current playback state ([AudioPlayer.PlaybackState](/CIC/References/Context_Objects.md#PlaybackState)) after a specified delay time has passed since your client has started playback of an audio stream. You can check the delay time for each audio stream when an [AudioPlayer.Play](#Play) directive message is returned to your client.

### Context field
Send the following [context information](/CIC/References/Context_Objects.md) together.

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

## ProgressReportIntervalPassed event {#ProgressReportIntervalPassed}
Reports to CIC on a current playback state ([AudioPlayer.PlaybackState](/CIC/References/Context_Objects.md#PlaybackState)) regularly at a specified interval of time since your client has started playback of an audio stream. You can check the reporting interval for each audio stream when an [AudioPlayer.Play](#Play) directive message is returned to your client.

### Context field
Send the following [context information](/CIC/References/Context_Objects.md) together.

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

## ProgressReportPositionPassed event {#ProgressReportPositionPassed}
Reports to CIC on a current playback state ([AudioPlayer.PlaybackState](/CIC/References/Context_Objects.md#PlaybackState)) at a specified reporting point after your client has started playback of an audio stream. You can check the reporting point for each audio stream when an [AudioPlayer.Play](#Play) directive message is returned to your client.

### Context field
Send the following [context information](/CIC/References/Context_Objects.md) together.

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

## Stop directive {#Stop}
Instructs your client to stop playback of an audio stream.

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

## StreamDeliver directive {#StreamDeliver}
Returns audio stream details necessary for playback. This is a response message to an [AudioPlayer.StreamRequested](#StreamRequested) event message. It always contains a streaming URL from which your client can play music.

### Payload field
| Field name | Type | Field description | Required |
|---------|------|--------|---------|
| audioItemId | string | A value for identifying audio stream details. You can use this value to remove any redundant Play directive messages. | Yes |
| audioStream | [AudioStreamObject](#AudioStreamObject) | An object that contains audio stream details necessary for playback               | Yes |

### Remarks
You can implement playback of audio streams by combining a StreamDeliver directive message with a *payload.audioStream* body returned in a [Play](#Play) directive message. However, you must not replace the values of the previous Play directive message with the new values returned in the StreamDeliver directive message. The reason is that if there is any content in the previous Play directive message that overlaps with the AudioStreamObject content of the StreamDeliver directive message, that overlapping content might be omitted. This may cause unexpected behaviors when your client handles the same Play directive message more than once, such as repeat playback or previous track playback.

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

## StreamRequested event {#StreamRequested}
Requests CIC for more audio stream information necessary for playback, such as a streaming URL.

### Context field
None

### Events field
| Field name       | Type    | Field description                     | Required |
|---------------|---------|-----------------------------|---------|
| audioItemId   | string  | audioItemId of a Play directive message                                      | Yes |
| audioStream   | [AudioStreamObject](#AudioStreamObject) | audioItem.stream of a Play directive message | Yes |

### Remarks
Sometimes, due to the way music services charge users, issuing specific streaming details must be delayed till right before playback. This event message API is designed for such case when audio stream details should not be ready too early. As such, you must implement your client not to send this event message earlier than right before playback.

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
Include the shared object in a message body (payload) when sending an event message or directive message using the AudioPlayer API.

| Object name            | Object description                                            |
|--------------------|---------------------------------------------------|
| [AudioStreamObject](#AudioStreamObject) | An object that contains playback details of an audio stream, such as streaming address or credentials |

### AudioStreamObject {#AudioStreamObject}
Contains streaming details of an audio stream for playback. It is used when CIC returns playback streaming details to your client or when your client sends streaming details of a currently playing music to CIC.

#### Object field
| Field name       | Type    | Field description                     | Required |
|---------------|---------|-----------------------------|---------|
| beginAtInMilliseconds | number | A starting point of playback. If this field is specified as a non-zero value, the client must play the audio stream from that point.  If this field is specified as 0, the client must play the audio stream from the beginning. Unit is millisecond.          | Yes |
| progressReport    | object  | An object that specifies the time to report on a playback state after playback has started                                                  | No |
| progressReport.progressReportDelayInMilliseconds | number | Specify this value to report on a playback state after a specified time has passed since playback has started.   | No |
| progressReport.progressReportIntervalInMilliseconds | number | Specify this value to report on a playback state regularly at a specified interval of time during playback.      | No |
| progressReport.progressReportPositionInMilliseconds | number | Specify this value to report on a playback state at specified points during playback.  | No |
| token             | string  | An audio stream URL                                                                                     | Yes |
| url               | string  | An audio stream token                                                                                     | Yes |
| [Custom Field]    | any     | Service providers can add any context information for an audio stream necessary for playback.                                | No |

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