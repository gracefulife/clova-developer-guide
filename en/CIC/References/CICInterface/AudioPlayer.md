# AudioPlayer

The AudioPlayer namespace provides interfaces for playing an audio stream or reporting to CIC about events that occur during playback. The AudioPlayer namespace provides the following directives and events.

| Message name         | Message type  | Description                                   |
|------------------|-----------|---------------------------------------------|
| [`ClearQueue`](#Play)                 | Directive | Instructs a client to initialize the playback queue.                         |
| [`Play`](#Play)                       | Directive | Instructs a client to start playing the specified audio stream or add the audio to the playback queue.                         |
| [`PlayFinished`](#PlayFinished)       | Event     | A message to notify CIC that the client has finished playing an audio stream, along with the information of the audio stream the client has just finished playing.  |
| [`PlayPaused`](#PlayPaused)           | Event     | A message to notify CIC that the client has paused an audio stream, along with the information of the paused audio stream. |
| [`PlayResumed`](#PlayResumed)         | Event     | A message to notify CIC that the client has resumed playing an audio stream, along with the information of the resumed audio stream. |
| [`PlayStarted`](#PlayStarted)         | Event     | A message to notify CIC that the client has started playing an audio stream, along with the information of the audio stream the client has just started playing.     |
| [`PlayStopped`](#PlayStopped)         | Event     | A message to notify CIC that the client has stopped playing an audio stream, along with the information of the stopped audio stream.  |
| [`ProgressReportDelayPassed`](#ProgressReportPositionPassed) | Event | A message to report to CIC the current playback state  ([`AudioPlayer.PlaybackState`](/CIC/References/Context_Objects.md#PlaybackState)) after the specified time (delay) has passed from playing audio stream. The delay period for each audio stream is specified in the  [`AudioPlayer.Play`](#Play) directive. |
| [`ProgressReportIntervalPassed`](#ProgressReportPositionPassed)| Event | A message to regularly report to CIC the current playback state ([`AudioPlayer.PlaybackState`](/CIC/References/Context_Objects.md#PlaybackState)) by the specified interval once playing an audio stream. The reporting interval for an audio stream is specified in the [`AudioPlayer.Play`](#Play) directive. |
| [`ProgressReportPositionPassed`](#ProgressReportPositionPassed) | Event | A message to report to CIC the current playback state ([`AudioPlayer.PlaybackState`](/CIC/References/Context_Objects.md#PlaybackState)) when the client is playing the specified point. The reporting point for an audio stream is specified in the [`AudioPlayer.Play`](#Play) directive. |
| [`StreamDeliver`](#StreamDeliver)     | Directive | Returns the audio stream itself as a response to the [`AudioPlayer.StreamRequested`](#StreamRequested) event.  |
| [`StreamRequested`](#StreamRequested) | Event     | A message to request to CIC for additional audio stream information required for playback, such as a stream URL.               |


## ClearQueue directive {#ClearQueue}

Instructs a client to initialize the playback queue. A client is instructed either to stop playing audio stream or keep playing.

### Payload fields

| Field name       | Type    | Description                     | Provided |
|---------------|:---------:|-----------------------------|:---------:|
| `clearBehavior`           | string | Indicates whether to stop or keep playing audio stream when initializing the playback queue.<ul><li><code>"CLEAR_ALL"</code>: Initialize the queue and stop playing audio stream. </li><li><code>"CLEAR_ENQUEUED"</code>: Initialize the queue only. Keep playing the audio stream being played.</li></ul> | Always |

### Message example

{% raw %}

```json
{
  "directive": {
    "header": {
      "namespace": "AudioPlayer",
      "name": "ClearQueue",
      "dialogRequestId": "8b81296d-218e-4a08-897a-bee51daad907",
      "messageId": "823a703d-9447-438a-bad5-21fa7a62b623"
    },
    "payload": {
      "clearBehavior": "CLEAR_ALL"
    }
  }
}
```

{% endraw %}

### See also

* [`AudioPlayer.Play`](#Play)
* [`AudioPlayer.PlayStarted`](#PlayStarted)
* [`AudioPlayer.PlayStopped`](#PlayStopped)

## Play directive {#Play}

Instructs a client to either play or add to the playback queue the specified audio stream.

### Payload fields

| Field name       | Type    | Description                     | Provided |
|---------------|:---------:|-----------------------------|:---------:|
| `audioItem`               | object | Contains metadata of an audio stream to play and also the audio stream information required for playback.                     | Always |
| `audioItem.audioItemId`   | string | The ID of an audio stream. Use the value in removing redundant `Play` directives. | Always |
| `audioItem.stream`        | [AudioStreamInfoObject](#AudioStreamInfoObject) | Contains audio stream information required for playback.                        | Always |
| `audioItem.type`          | string | The name of the music service provider. Use this value to figure out which fields of the `audioItem` object are used for different service providers and select an appropriate parser to analyze them. | Always |
| `audioItem.[CustomField]` | any    | Contains the metadata added by the music service provider about the audio stream for playback.                     | Conditional |
| `playBehavior`            | string | Indicates when to play the given audio stream. <ul><li><code>"REPLACE_ALL"</code>: Empty the playback queue, and start playing the given audio stream immediately.</li><li><code>"ENQUEUE"</code>: Add the given audio stream to the playback queue.</li></ul> | Always |
| `source`                  | object | Contains information of the music service provider.                                                   | Always |
| `source.name`             | string | The name of the music service provider.                                                        | Always |
| `source.logoUrl`          | string | The URL for the logo of the music service provider. If this field is unavailable or undefined or somehow if the logo cannot be displayed, you must at least display the name of the music service provider specified in the `source.name` field.  | Conditional |

### Remarks

Based on the policy of music service providers, certain information required for playback (e.g. streaming URL) may not be shared to clients until right before playback. If not all information is provided before playback, you need to make an additional request to CIC to obtain the information. Whether extra information shall be requested is specified in the `audioItem.stream.urlPlayable` field as shown below:

* `urlPlayable` is `true`: No extra information is required. You can play the audio stream only with the URL specified in the `audioItem.stream.url` field.
* `urlPlayable` is `false`: Extra information is required for you to play the given audio stream. Make a request for extra information with the [`AudioPlayer.StreamRequested`](#StreamRequested) event.

### Message example

{% raw %}

```json
// Example: The given audio stream can be played only with the stream URL
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
          "url": "https://streaming.example.com/1212334548/2231122",
          "urlPlayable": true
        },
        "type": "podcast"
      },
      "source": {
        "name": "SamplePodCast",
        "logoUrl": "https://ssl.pstatic.net/static/clova/service/extension/com.navercorp.samplepodcast/source_logo.png"
      },
      "playBehavior": "REPLACE_ALL"
    }
  }
}

// Example: The given audio stream cannot be played only with the URL.
// Extra information is required.
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
            "Ballard",
            "R&B/Urban"
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
        "title": "All I want for Christmas is You",
        "type": "navermusic"
      },
      "source": {
        "name": "Naver Music",
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

A message for reporting to CIC that the client has finished playing an audio stream. Send along the information of the audio stream that the client has just finished playing.

### Context fields

Send the following [context information](/CIC/References/Context_Objects.md) with this event.

* [`AudioPlayer.PlaybackState`](/CIC/References/Context_Objects.md#PlaybackState)

### Payload fields

None

### Message example

{% raw %}

```json
{
  "context": [
    {{AudioPlayer.PlaybackState}}
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

A message for notifying CIC that the client has paused playing an audio stream, along with the information of the audio stream that the client has just paused.
Send this event in the following scenario:

1. A client sends CIC a user's voice request ([`SpeechRecognizer.Recognize`](/CIC/References/CICInterface/SpeechRecognizer.md#Recognize)) to pause playback of an audio stream.
2. CIC responds with the [`PlaybackController.Pause`](/CIC/References/CICInterface/PlaybackController.md#Pause) directive, as the result of voice recognition by Clova.
3. The client pauses playback of the audio stream and sends CIC the `PlayPaused` event.

### Context fields

Send the following [context information](/CIC/References/Context_Objects.md) with this event.

* [`AudioPlayer.PlaybackState`](/CIC/References/Context_Objects.md#PlaybackState)

### Payload fields

None

### Message example

{% raw %}

```json
{
  "context": [
    {{AudioPlayer.PlaybackState}}
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

A message for notifying CIC that the client has resumed playing an audio stream, along with the information of the resumed audio stream.
Send this event in the following scenario:

1. A client sends CIC a user's voice request ([`SpeechRecognizer.Recognize`](/CIC/References/CICInterface/SpeechRecognizer.md#Recognize)) to resume the paused audio stream.
2. CIC responds with the [`PlaybackController.Resume`](/CIC/References/CICInterface/PlaybackController.md#Resume) directive, as the result of voice recognition by Clova.
3. The client resumes playback of the audio stream and sends CIC the `PlayResumed` event.

### Context fields

Send the following [context information](/CIC/References/Context_Objects.md) with this event.

* [`AudioPlayer.PlaybackState`](/CIC/References/Context_Objects.md#PlaybackState)

### Payload fields

None

### Message example
{% raw %}

```json
{
  "context": [
    {{AudioPlayer.PlaybackState}}
  ],
  "event": {
    "header": {
      "namespace": "AudioPlayer",
      "name": "PlayResumed",
      "messageId": "4e4080d6-c440-498a-bb73-ae86c6312806"
    },
    "payload": {}
  }
}
```

{% endraw %}

### See also
* [`AudioPlayer.Play`](#Play)
* [`AudioPlayer.PlayPaused`](#PlayPaused)
* [`PlaybackController.Resume`](/CIC/References/CICInterface/PlaybackController.md#Resume)


## PlayStarted event {#PlayStarted}

A message for notifying CIC that the client has started playing an audtio stream, along with the information of the audio stream playing.

### Context fields

Send the following [context information](/CIC/References/Context_Objects.md) with this event.

* [`AudioPlayer.PlaybackState`](/CIC/References/Context_Objects.md#PlaybackState)

### Payload fields

None

### Message example
{% raw %}

```json
{
  "context": [
    {{AudioPlayer.PlaybackState}}
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

A message for notifying CIC that the client has stopped playing an audio stream, along with the information of the stopped audio stream.
Send this event in the following scenario:

1. A client sends CIC a user's voice request ([`SpeechRecognizer.Recognize`](/CIC/References/CICInterface/SpeechRecognizer.md#Recognize)) to pause playback of an audio stream.
2. CIC responds with the [`PlaybackController.Stop`](/CIC/References/CICInterface/PlaybackController.md#Stop), as the result of voice recognition by Clova.
3. The client stops playback of the audio stream and sends CIC the `PlayStopped` event.

### Context fields

Send the following [context information](/CIC/References/Context_Objects.md) with this event.

* [`AudioPlayer.PlaybackState`](/CIC/References/Context_Objects.md#PlaybackState)

### Payload fields

None

### Message example

{% raw %}

```json
{
  "context": [
    {{AudioPlayer.PlaybackState}}
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

A message for reporting to CIC the current playback state ([`AudioPlayer.PlaybackState`](/CIC/References/Context_Objects.md#PlaybackState)) when the specified time (delay) has elapsed after playback has started. The time for reporting is specified in the [`AudioPlayer.Play`](#Play) directive.

### Context fields

Send the following [context information](/CIC/References/Context_Objects.md) with this event.

* [`AudioPlayer.PlaybackState`](/CIC/References/Context_Objects.md#PlaybackState)

### Payload fields

None

### Message example

{% raw %}

```json
{
  "context": [
    {{AudioPlayer.PlaybackState}}
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

A message for regularly reporting to CIC the current playback state ([`AudioPlayer.PlaybackState`](/CIC/References/Context_Objects.md#PlaybackState)) by the specified interval, after playback has started. The interval is specified in the [`AudioPlayer.Play`](#Play) directive.

### Context fields

Send the following [context information](/CIC/References/Context_Objects.md) with this event.

* [`AudioPlayer.PlaybackState`](/CIC/References/Context_Objects.md#PlaybackState)

### Payload fields

None

### Message example

{% raw %}

```json
{
  "context": [
    {{AudioPlayer.PlaybackState}}
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

A message for reporting to CIC the current playback state ([`AudioPlayer.PlaybackState`](/CIC/References/Context_Objects.md#PlaybackState)) at the time specified, which is measured from the start of the audio stream. The reporting point is specified in the [`AudioPlayer.Play`](#Play) directive.

### Context fields

Send the following [context information](/CIC/References/Context_Objects.md) with this event.

* [`AudioPlayer.PlaybackState`](/CIC/References/Context_Objects.md#PlaybackState)

### Payload fields

None

### Message example

{% raw %}

```json
{
  "context": [
    {{AudioPlayer.PlaybackState}}
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

Returns audio stream information required for playback. This is a response message to the [`AudioPlayer.StreamRequested`](#StreamRequested) event. This directive always returns the stream URL for the client to play.

### Payload fields

| Field name | Type | Description | Provided |
|---------------|:---------:|-----------------------------|:---------:|
| `audioItemId` | string | Identifies for which audio stream the information is for. Make use of this ID to remove redundant `Play` directives. | Always |
| `audioStream` | [AudioStreamInfoObject](#AudioStreamInfoObject) | Contains audio stream information required for playback.               | Always |

### Remarks
You can make a use of a combination of the `StreamDeliver` directive and the `payload.audioStream` field of the [Play](#Play) directive for playback. Do NOT replace the values contained in the `Play` directive received with the values contained in the `StreamDeliver` directive.

The reason being that, if any content of the `AudioStreamInfoObject` in the `StreamDeliver` directive overlaps with the content of the previous [`AudioPlayer.Play`](#Play) directive message, that overlapping content could be omitted. This may cause unexpected behaviors when you process the same `Play` directive message more than once, for example, to play a track repeatedly or to play a previous track.

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

A message for requesting to CIC for additional audio stream details necessary for playback, such as a streaming URL.

### Context fields

None

### Payload fields

| Field name       | Type    | Description                     | Required |
|---------------|:---------:|-----------------------------|:---------:|
| `audioItemId`   | string  | The ID of the audio stream to request for. Set the value specified in the `audioItemId` field of the `Play` directive.                                              | Required |
| `audioStream`   | [AudioStreamInfoObject](#AudioStreamInfoObject) | The audio stream information. Set the values specified in the `audioItem.stream` field of the `Play` directive. | Required |

### Remarks

Based on the policy of music service providers, certain information required for playback (e.g. streaming URL) may not be shared to clients until right before playback. This event is an interface for the cases where the stream information has to be held back. Do not send this event earlier than right before playing an audio stream.

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

## Common objects

Common objects are included in the message body (`payload`) of events or directives when they are sent with the AudioPlayer API.

| Object name            | Object description                                            |
|--------------------|---------------------------------------------------|
| [AudioStreamInfoObject](#AudioStreamInfoObject) | Contains playback details of an audio stream, such as a streaming address or credentials. |

### AudioStreamInfoObject {#AudioStreamInfoObject}

Contains streaming details of an audio stream. This object is used when CIC returns streaming details to a client or when the client sends the details of the currently playing audio stream to CIC.

#### Object fields

| Field name       | Type    | Description                     | Required/Provided |
|---------------|:---------:|-----------------------------|:---------:|
| `beginAtInMilliseconds`  | number | A starting point of playback in milliseconds. If this field is specified, play the audio stream from the specified point from the starting point of the stream. If 0, play the audio stream from the beginning.          | Required/Always |
| `durationInMilliseconds` | number | The length of the audio stream in milliseconds. The client can seek within and play by the time defined. This field CANNOT be a `null`.  | Optional/Conditional  |
| `progressReport`         | object  | Specifies the time(s) to report the playback state after playback has started.                                                  | Optional/Conditional  |
| `progressReport.progressReportDelayInMilliseconds`    | number | The time after which the client is to report the playback state to CIC after playback has started. Unit is millisecond. This field can have a `null`.  | Optional/Conditional  |
| `progressReport.progressReportIntervalInMilliseconds` | number | The interval by which the client is to report the playback state to CIC after playback has started. Unit is millisecond. This field can have a `null`.        | Optional/Conditional  |
| `progressReport.progressReportPositionInMilliseconds` | number | The time from the start of the audio stream at which the client is to report the playback state to CIC. Unit is millisecond. This field can have a `null`.    | Optional/Conditional  |
| `token`                  | string  | The ID of an audio stream.                                                                                  | Required/Always |
| `url`                    | string  | The URL of the audio stream.                                                                                     | Required/Always |
| `urlPlayable`            | boolean | Indicates whether the client can play the given audio stream only with a URL or requires additional information to play.<ul><li><code>true</code>: The client can play only with the URL provided.</li><li><code>false</code>: The client requires additional information. To obtain additional information, the client is to send the <a href="#StreamRequested"><code>AudioPlayer.StreamRequested</code></a> event to CIC.</li></ul>        | Required/Always |
| `[Custom Field]`         | any     | Music service providers may provide custom values through the context of audio stream playback.<div class="danger"><p><strong>Caution!</strong></p><p>Clients must not use the custom fields added by the service providers to avoid possible issues. Note that the custom values must be specified in the `stream` field of the <a href="/CIC/References/Context_Objects.html#PlaybackState">PlaybackState context information</a> exactly as they are, when reporting the playback state to CIC.</p></div>                                | Optional/Conditional |


#### Remarks

* A client must send the [`AudioPlayer.PlayFinished`](#PlayFinished) event to CIC when finished with playing an audio stream by the end, i.e. when finished with playing for the `durationInMilliseconds` seconds.
* The audio player UI of a client shall prohibit users to seek past the point defined by the `durationInMilliseconds` field.
* When reporting the current playback state to CIC, set the `totalInMilliseconds` field of the [`AudioPlayer.PlaybackState`](/CIC/References/Context_Objects.md#PlaybackState) with the value specified in the `durationInMilliseconds` field.

#### Object Example

{% raw %}

```json
// An example of an audio stream which can be played only with the URL
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

// An example of an audio stream which cannot be played only with the URL
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
