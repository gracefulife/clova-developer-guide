# AudioPlayer

Instructs your client to play an audio stream or reports to CIC on events that occur during playback. AudioPlayer provides the following event and directive messages.

| Message name         | Message type  | Message description                                   |
|------------------|-----------|---------------------------------------------|
| [`Play`](#Play)                       | Directive | Instructs your client to start playback of a specified audio stream or add it to a playback queue.                         |
| [`PlayFinished`](#PlayFinished)       | Event     | Reports to CIC on audio stream details when your client finishes playback of an audio stream.     |
| [`PlayPaused`](#PlayPaused)           | Event     | Reports to CIC on audio stream details when your client pauses playback of an audio stream. |
| [`PlayResumed`](#PlayResumed)         | Event     | Reports to CIC on audio stream details when your client resumes playback of an audio stream.         |
| [`PlayStarted`](#PlayStarted)         | Event     | Reports to CIC on audio stream details when your client starts playback of an audio stream.    |
| [`PlayStopped`](#PlayStopped)         | Event     | Reports to CIC on audio stream details when your client stops playback of an audio stream.    |
| [`ProgressReportDelayPassed`](#ProgressReportPositionPassed) | Event | Reports to CIC on a current playback state ([`AudioPlayer.PlaybackState`](/CIC/References/Context_Objects.md#PlaybackState)) when a specified delay time has passed after playback has started. You can check the delay time for each audio stream when an [`AudioPlayer.Play`](#Play) directive message is returned to your client. |
| [`ProgressReportIntervalPassed`](#ProgressReportPositionPassed)| Event | Reports to CIC on a current playback state ([`AudioPlayer.PlaybackState`](/CIC/References/Context_Objects.md#PlaybackState)) regularly at a specified interval of time after playback has started. You can check the reporting interval for each audio stream when an [`AudioPlayer.Play`](#Play) directive message is returned to your client. |
| [`ProgressReportPositionPassed`](#ProgressReportPositionPassed) | Event | Reports to CIC on a current playback state ([`AudioPlayer.PlaybackState`](/CIC/References/Context_Objects.md#PlaybackState)) at a specified reporting point after playback has started. You can check the reporting point for each audio stream when an [`AudioPlayer.Play`](#Play) directive message is returned to your client. |
| [`StreamDeliver`](#StreamDeliver)     | Directive | Returns audio stream details necessary for playback. This is a response message to an [`AudioPlayer.StreamRequested`](#StreamRequested) event message. |
| [`StreamRequested`](#StreamRequested) | Event     | Requests CIC for additional audio stream details necessary for playback, such as a streaming URL.               |

## Play directive {#Play}
Instructs your client to start playback of a specified audio stream or add it to a playback queue.

### Payload field
| Field name       | Type    | Field description                     | Required |
|---------------|---------|-----------------------------|---------|
| `audioItem`               | object | An object containing metadata of an audio stream and audio stream details necessary for playback                     | Yes |
| `audioItem.audioItemId`   | string | The ID for distinguishing audio streams. You can remove redundant Play directive messages based on this value. | Yes |
| `audioItem.stream`        | [AudioStreamInfoObject](#AudioStreamInfoObject) | An object containing audio stream details necessary for the playback                        | Yes |
| `audioItem.type`          | string | A music service delimiter. It is the name of a business entity or service that provides a music streaming service. You can use this value to figure out which fields are used for the audioItem object in different services and select an appropriate parser to analyze them. | Yes |
| `audioItem.[CustomField]` | any    | Service providers can add extra metadata to the audio stream for playback.                     | No |
| `playBehavior`            | string | A delimiter that determines when your client will play the audio stream included in the directive message <ul><li><code>"REPLACE_ALL"</code>: Clears all existing playback queues and play this audio stream immediately.</li><li><code>"ENQUEUE"</code>: Adds this audio stream to a playback queue.</li></ul> | Yes |
| `source`                  | object | Source of the audio streaming service                                                    | Yes |
| `source.name`             | string | Name of the audio streaming service                                                        | Yes |
| `source.logoUrl`          | string | Logo image URL of the audio streaming service If there is no value in the field or if the logo image cannot be displayed, at least the name of audio streaming service from `source.name` field has to be labeled.  | No |

### Remarks
Sometimes, due to the way music services charge users, streaming details such as a streaming URL can only be obtained right before playback. Depending on the value of the `audioItem.stream.urlPlayable` field, it can be either one of the following.
* If `urlPlayable` is set to `true`, you can play the audio stream directly from the URL in the `audioItem.stream.url` field.
* If `urlPlayable` is set to `false`, you cannot play the audio stream directly from the URL in the `audioItem.stream.url` field. Instead, you must request additional audio stream details by sending an [`AudioPlayer.StreamRequested`](#StreamRequested) event message.

### Message example
{% raw %}

```json
// Example of an audio stream URL which you can play directly
{
  "directive": {
    "header": {
      "namespace": "AudioPlayer",
      "name": "StreamDeliver",
      "dialogRequestId": "34abac3-cb46-611c-5111-47eab87b7",
      "messageId": "ad13f0d6-bb11-ca23-99aa-312a0b213805"
    },
    "payload": {
      "audioItem": {
        "audioItemId": "90b77646-93ab-444f-acd9-60f9f278ca38",
        "episodeId": 22346122,
        "stream": {
          "beginAtInMilliseconds": 0,
          "episodeId": 22346122,
          "playType": "NONE",
          "podcastId": 12548,
          "progressReport": {
            "progressReportDelayInMilliseconds": null,
            "progressReportIntervalInMilliseconds": 60000,
            "progressReportPositionInMilliseconds": null
          },
          "url": "https://steaming.example.com/1212334548/2231122",
          "urlPlayable": true
        },
        "type": "podcast"
      },
      "source": {
        "name": "팟빵",
        "logoUrl": "https://ssl.pstatic.net/static/clova/service/extension/com.navercorp.podbbang/source_logo.png"
      },
      "playBehavior": "REPLACE_ALL"
    }
  }
}

// Example of an audio stream URL which you cannot play directly
{
  "directive": {
    "header": {
      "namespace": "AudioPlayer",
      "name": "StreamDeliver",
      "dialogRequestId": "277b40c3-b046-4f61-a551-783b1547e7b7",
      "messageId": "4e4080d6-c440-498a-bb73-ae86c6312806"
    },
    "payload": {
      "audioItem": {
        "audioItemId": "9CPWU-8362fe7c-f75c-42c6-806b-6f3e00aba8f1-c1862201",
        "album": {
          "albumId": "2000240",
          "genres": [
            "발라드",
            "알앤비/어반"
          ],
          "title": "Palette"
        },
        ...
        "stream": {
          "beginAtInMilliseconds": 0,
          "durationInMilliseconds": 60000,
          "progressReport": {
            "progressReportDelayInMilliseconds": null,
            "progressReportIntervalInMilliseconds": null,
            "progressReportPositionInMilliseconds": 60000
          },
          "token": "TR-NM-17716562",
          "url": "clova:TR-NM-17716562",
          "urlPlayable": false
        },
        "title": "이 지금",
        "type": "navermusic"
      },
      "source": {
        "name": "Sample Music Service",
        "logoUrl": "https://ssl.pstatic.net/static/clova/service/extension/com.navercorp.music/source_logo.png"
      },
      "playBehavior": "REPLACE_ALL"
    }
  }
}
```

{% endraw %}

### See also
* [`AudioPlayer.PlayPaused`](#PlayPaused)
* [`AudioPlayer.PlayResumed`](#PlayResumed)
* [`AudioPlayer.PlayStarted`](#PlayStarted)
* [`AudioPlayer.PlayStopped`](#PlayStopped)
* [`AudioPlayer.ProgressReportDelayPassed`](#ProgressReportDelayPassed)
* [`AudioPlayer.ProgressReportIntervalPassed`](#ProgressReportIntervalPassed)
* [`AudioPlayer.ProgressReportPositionPassed`](#ProgressReportPositionPassed)
* [`AudioPlayer.StreamRequested`](#StreamRequested)

## PlayFinished event {#PlayFinished}
Reports to CIC on audio stream details when your client finishes playback of an audio stream.

### Context field
Send the following [context information](/CIC/References/Context_Objects.md) together.

* [`AudioPlayer.PlaybackState`](/CIC/References/Context_Objects.md#PlaybackState)

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
      "messageId": "4e4080d6-c440-498a-bb73-ae86c6312806"
    },
    "payload": {}
  }
}
```

{% endraw %}

### See also
* [`AudioPlayer.Play`](#Play)

## PlayPaused event {#PlayPaused}
Reports to CIC on audio stream details when your client pauses playback of an audio stream. Send this event message in the following scenario.

1. Your client sends CIC a user's spoken request to pause playback of an audio stream, using a [`SpeechRecognizer.Recognize`](/CIC/References/CICInterface/SpeechRecognizer.md#Recognize) event message.
2. The Clova platform recognizes the pause request and CIC returns it to your client, using a [`PlaybackController.Pause`](/CIC/References/CICInterface/PlaybackController.md#Pause) directive message.
3. Your client pauses playback of the audio stream and sends CIC a PlayPaused event message.

### Context field
Send the following [context information](/CIC/References/Context_Objects.md) together.

* [`AudioPlayer.PlaybackState`](/CIC/References/Context_Objects.md#PlaybackState)

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
      "messageId": "4e4080d6-c440-498a-bb73-ae86c6312806"
    },
    "payload": {}
  }
}
```

{% endraw %}

### See also
* [`AudioPlayer.Play`](#Play)
* [`AudioPlayer.PlayResumed`](#PlayResumed)
* [`PlaybackController.Pause`](/CIC/References/CICInterface/PlaybackController.md#Pause)

## PlayResumed event {#PlayResumed}
l

## PlayStarted event {#PlayStarted}
Reports to CIC on audio stream details when your client starts playback of an audio stream.

### Context field
Send the following [context information](/CIC/References/Context_Objects.md) together.

* [`AudioPlayer.PlaybackState`](/CIC/References/Context_Objects.md#PlaybackState)

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
      "messageId": "4e4080d6-c440-498a-bb73-ae86c6312806"
    },
    "payload": {}
  }
}
```

{% endraw %}

### See also
* [`AudioPlayer.Play`](#Play)
* [`AudioPlayer.PlayStopped`](#PlayStopped)

## PlayStopped event {#PlayStopped}
Reports to CIC on audio stream details when your client stops playback of an audio stream. Send this event message in the following scenario.

1. Your client sends CIC a user's spoken request to pause playback of an audio stream, using a [`SpeechRecognizer.Recognize`](/CIC/References/CICInterface/SpeechRecognizer.md#Recognize) event message.
2. The Clova platform recognizes the stop request and CIC returns it to your client, using a [`PlaybackController.Stop`](/CIC/References/CICInterface/PlaybackController.md#Stop) directive message.
3. Your client stops playback of the audio stream and sends CIC a PlayStopped event message.

### Context field
Send the following [context information](/CIC/References/Context_Objects.md) together.

* [`AudioPlayer.PlaybackState`](/CIC/References/Context_Objects.md#PlaybackState)

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
      "messageId": "4e4080d6-c440-498a-bb73-ae86c6312806"
    },
    "payload": {}
  }
}
```

{% endraw %}

### See also
* [`AudioPlayer.Play`](#Play)
* [`AudioPlayer.PlayStarted`](#PlayStarted)
* [`PlaybackController.Stop`](/CIC/References/CICInterface/PlaybackController.md#Stop)

## ProgressReportDelayPassed event {#ProgressReportDelayPassed}
Reports to CIC on a current playback state ([`AudioPlayer.PlaybackState`](/CIC/References/Context_Objects.md#PlaybackState)) when a specified delay time has passed after playback has started. You can check the delay time for each audio stream when an [`AudioPlayer.Play`](#Play) directive message is returned to your client.

### Context field
Send the following [context information](/CIC/References/Context_Objects.md) together.

* [`AudioPlayer.PlaybackState`](/CIC/References/Context_Objects.md#PlaybackState)

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
      "messageId": "4e4080d6-c440-498a-bb73-ae86c6312806"
    },
    "payload": {}
  }
}
```

{% endraw %}

### See also
* [`AudioPlayer.Play`](#Play)
* [`AudioPlayer.ProgressReportIntervalPassed`](#ProgressReportIntervalPassed)
* [`AudioPlayer.ProgressReportPositionPassed`](#ProgressReportPositionPassed)

## ProgressReportIntervalPassed event {#ProgressReportIntervalPassed}
Reports to CIC on a current playback state ([`AudioPlayer.PlaybackState`](/CIC/References/Context_Objects.md#PlaybackState)) regularly at a specified interval of time after playback has started. You can check the reporting interval for each audio stream when an [`AudioPlayer.Play`](#Play) directive message is returned to your client.

### Context field
Send the following [context information](/CIC/References/Context_Objects.md) together.

* [`AudioPlayer.PlaybackState`](/CIC/References/Context_Objects.md#PlaybackState)

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
      "messageId": "4e4080d6-c440-498a-bb73-ae86c6312806"
    },
    "payload": {}
  }
}
```

{% endraw %}

### See also
* [`AudioPlayer.Play`](#Play)
* [`AudioPlayer.ProgressReportDelayPassed`](#ProgressReportDelayPassed)
* [`AudioPlayer.ProgressReportPositionPassed`](#ProgressReportPositionPassed)

## ProgressReportPositionPassed event {#ProgressReportPositionPassed}
Reports to CIC on a current playback state ([`AudioPlayer.PlaybackState`](/CIC/References/Context_Objects.md#PlaybackState)) at a specified reporting point after playback has started. You can check the reporting point for each audio stream when an [`AudioPlayer.Play`](#Play) directive message is returned to your client.

### Context field
Send the following [context information](/CIC/References/Context_Objects.md) together.

* [`AudioPlayer.PlaybackState`](/CIC/References/Context_Objects.md#PlaybackState)

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
      "messageId": "4e4080d6-c440-498a-bb73-ae86c6312806"
    },
    "payload": {}
  }
}
```

{% endraw %}

### See also
* [`AudioPlayer.Play`](#Play)
* [`AudioPlayer.ProgressReportDelayPassed`](#ProgressReportDelayPassed)
* [`AudioPlayer.ProgressReportIntervalPassed`](#ProgressReportIntervalPassed)

## StreamDeliver directive {#StreamDeliver}
Returns audio stream details necessary for playback. This is a response message to an [`AudioPlayer.StreamRequested`](#StreamRequested) event message. It contain a streaming URL in audio stream details from which your client can play music.

### Payload field
| Field name | Type | Field description | Required |
|---------|------|--------|---------|
| `audioItemId` | string | A value for distinguishing audio stream details. You can remove redundant Play directive messages based on this value. | Yes |
|`audioStream`| [AudioStreamInfoObject](#AudioStreamInfoObject) | An object containing audio stream details necessary for the playback.               | Yes |

### Remarks
You can implement audio stream playback by combining ㅁ StreamDeliver directive message with `payload.audioStream` of a previously received [Play](#Play) directive message. However, you must not replace the values of the previous Play directive message with the new values passed through the `StreamDeliver` directive message. The reason is that, if any content of `AudioStreamInfoObject` in the `StreamDeliver` directive message overlaps with the content of the previous [`AudioPlayer.Play`](#Play) directive message, that overlapping content might be omitted. This may cause unexpected behaviors when you process a same Play directive message more than once, for example, to play a track repeatedly or to play a previous track.

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
* [`AudioPlayer.Play`](#Play)
* [`AudioPlayer.StreamRequested`](#StreamRequested)

## StreamRequested event {#StreamRequested}
Requests CIC for additional audio stream details necessary for playback, such as a streaming URL.

### Context field
None

### Payload field
| Field name       | Type    | Field description                     | Required |
|---------------|---------|-----------------------------|---------|
| `audioItemId`   | string  | `audioItemId` of the Play directive message                                              | Yes |
| `audioStream`   | [AudioStreamInfoObject](#AudioStreamInfoObject) | `audioItem.stream` of the Play directive message | Yes |

### Remarks
Sometimes, due to the way music services charge users, obtaining specific streaming details must be delayed until right before playback. This event message API is designed for cases where you must not prepare audio stream details in advance. You must implement your client not to send this event message earlier than right before playback.

### Message example
{% raw %}

```json
{
  "context": [],
  "event": {
    "header": {
      "namespace": "AudioPlayer",
      "name": "StreamRequested",
      "messageId": "198cf12-4020-b98a-b73b-1234ab312806"
    },
    "payload": {
      "audioItemId": "ac192f4c-8f12-4a58-8ace-e3127eb297a4",
      "audioStream": {
        "beginAtInMilliseconds": 0,
        "progressReport": {
            "progressReportDelayInMilliseconds": null,
            "progressReportIntervalInMilliseconds": null,
            "progressReportPositionInMilliseconds": 60000
        },
        "token": "TR-NM-4435786",
        "urlPlayable": false,
        "url": "clova:TR-NM-4435786"
      }
    }
  }
}
```

{% endraw %}

### See also
* [`AudioPlayer.Play`](#Play)
* [`AudioPlayer.StreamDeliver`](#StreamDeliver)

## Shared objects
Shared objects are included in a message body (`payload`) of event or directive messages when they are sent with the AudioPlayer API.

| Object name            | Object description                                            |
|--------------------|---------------------------------------------------|
| [AudioStreamInfoObject](#AudioStreamInfoObject) | An object containing playback details of an audio stream, such as a streaming address or credentials |

### AudioStreamInfoObject {#AudioStreamInfoObject}
Contains streaming details of an audio stream. It is used when CIC returns playback streaming details to your client or when your client sends streaming details of a currently playing music to CIC.

#### Object field
| Field name       | Type    | Field description                     | Required |
|---------------|---------|-----------------------------|---------|
| `beginAtInMilliseconds`  | number | A starting point of playback. Unit is millisecond. If this field is specified as a non-zero value, play the audio stream from the specified point. If this field is specified as 0, play the audio stream from the beginning.          | Yes |
| `durationInMilliseconds` | number | Playback time of the audio stream. It is the length of the audio stream. The client can search and play the audio until a designated time in the field. Unit is millisecond. This field cannot have a null value.  | No  |
| `progressReport`         | object  | An object that specifies the time to report on a playback state after playback has started                                                  | No |
| `progressReport.progressReportDelayInMilliseconds`    | number | A value designated to receive the report of the playback status when a specified time has passed after the playback has started. Unit is millisecond. This field can have a null value.  | No |
| `progressReport.progressReportIntervalInMilliseconds` | number | A value designated to receive the report of the playback status at a specified interval of time during the playback. Unit is millisecond. This field can have a null value.        | No |
| `progressReport.progressReportPositionInMilliseconds` | number | A value designated to receive the report of the playback status as passing a specified point during the playback. Unit is millisecond. This field can have a null value.    | No |
| `token`                  | string  | An audio stream token.                                                                                  | Yes |
| `url`                    | string  | An audio stream URL                                                                                     | Yes |
| `urlPlayable`            | boolean | A value determining whether the audio stream URL in the `url` field is directly playable or not. <ul><li><code>true</code>: Can play directly from the URL</li><li><code>false</code>: Cannot play directly from the URL Send an <a href="#StreamRequested"><code>AudioPlayer.StreamRequested</code></a> event message to request for audio stream details.</li></ul>        | Yes |
| `[Custom Field]`         | any     | Service providers can add necessary value on the context of audio stream playback arbitrarily.<div class="danger"><p><strong>Caution!</strong></p><p>The client should not use the arbitrary field value added by the service providers. Or else it may cause an issue. The added field value should be attached to `stream` field located at <a href="/CIC/References/Context_Objects.html#PlaybackState">PlaybackState context information</a> when passing the audio playback status.</p></div>                                | No |

#### Remarks
* A [`AudioPlayer.PlayFinished`](#PlayFinished) directive message should be sent to CIC if the client finishes playing the audio at a designated time on `durationInMilliseconds` field.
* The client should exceed the time designated on the `durationInMilliseconds` field to provide UI where the user cannot seek the audio stream.
* The client should enter `totalInMilliseconds` field value of [`AudioPlayer.PlaybackState`](/CIC/References/Context_Objects.md#PlaybackState) on `durationInMilliseconds` field as a designated value when reporting the current playback status to CIC.

#### Object Example
{% raw %}

```json
// Example of an audio stream URL which you can play directly
{
  "beginAtInMilliseconds": 0,
  "episodeId": 22346122,
  "playType": "NONE",
  "podcastId": 12548,
  "progressReport": {
    "progressReportDelayInMilliseconds": null,
    "progressReportIntervalInMilliseconds": 60000,
    "progressReportPositionInMilliseconds": null
  },
  "url": "https://api-ex.podbbang.com/file/12548/22346122",
  "urlPlayable": true
}

// Example of an audio stream URL which you cannot play directly
{
  "beginAtInMilliseconds": 0,
  "progressReport": {
      "progressReportDelayInMilliseconds": null,
      "progressReportIntervalInMilliseconds": null,
      "progressReportPositionInMilliseconds": 60000
  },
  "token": "TR-NM-4435786",
  "urlPlayable": false,
  "url": "clova:TR-NM-4435786"
}
```

{% endraw %}

#### See also
* [`AudioPlayer.Play`](#Play)
* [`AudioPlayer.PlayFinished`](#PlayFinished)
* [`AudioPlayer.ProgressReportDelayPassed`](#ProgressReportDelayPassed)
* [`AudioPlayer.ProgressReportIntervalPassed`](#ProgressReportIntervalPassed)
* [`AudioPlayer.ProgressReportPositionPassed`](#ProgressReportPositionPassed)
* [`AudioPlayer.PlaybackState`](/CIC/References/Context_Objects.md#PlaybackState)
* [`AudioPlayer.StreamRequested`](#StreamRequested)
