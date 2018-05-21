# AudioPlayer

The AudioPlayer namespace provides interfaces for playing an audio stream or reporting to CIC about events that occur during playback. The AudioPlayer namespace provides the following directives and events.

| Message name         | Type  | Description                                   |
|------------------|-----------|---------------------------------------------|
| [`ClearQueue`](#ClearQueue)           | Directive | Instructs the client to initialize the playback queue of the audio stream.                              |
| [`ExpectReportPlaybackState`](#ExpectReportPlaybackState) | Directive | Instructs the client to report the current playback state. Upon receiving the directive, the client must send the [`AudioPlayer.ReportPlaybackState`](#ReportPlaybackState) event to CIC. |
| [`Play`](#Play)                       | Directive | Instructs the client to either play or add to the playback queue the specified audio stream.                         |
| [`PlayFinished`](#PlayFinished)       | Event     | Reports to CIC that the client has finished playback with the information on the audio stream.     |
| [`PlayPaused`](#PlayPaused)           | Event     | Reports to CIC that the client has paused playback with the information on the audio stream. |
| [`PlayResumed`](#PlayResumed)         | Event     | Reports to CIC that the client has resumed playback with the information on the audio stream.         |
| [`PlayStarted`](#PlayStarted)         | Event     | Reports to CIC that the client has started playback with the information on the audio stream.    |
| [`PlayStopped`](#PlayStopped)         | Event     | Reports to CIC that the client has stopped playback with the information on the audio stream.    |
| [`ProgressReportDelayPassed`](#ProgressReportPositionPassed) | Event | Reports to CIC the current playback state ([`AudioPlayer.PlaybackState`](/CIC/References/Context_Objects.md#PlaybackState)) after the delay—specified period of time—has passed. The delay is specified in the [`AudioPlayer.Play`](#Play) directive. |
| [`ProgressReportIntervalPassed`](#ProgressReportPositionPassed)| Event | Reports to CIC the current playback state ([`AudioPlayer.PlaybackState`](/CIC/References/Context_Objects.md#PlaybackState)), by the specified interval, after playback has started. The interval is specified in the [`AudioPlayer.Play`](#Play) directive.|
| [`ProgressReportPositionPassed`](#ProgressReportPositionPassed) | Event | Reports to CIC the current playback state ([`AudioPlayer.PlaybackState`](/CIC/References/Context_Objects.md#PlaybackState)) at the specified time, which is measured from the start of the audio stream. The reporting time is specified in the [`AudioPlayer.Play`](#Play) directive.|
| [`ReportPlaybackState`](#ReportPlaybackState)           | Event  | Reports to CIC the current playback state of the client. If the [`ExpectReportPlaybackState`](#ExpectReportPlaybackState) directive is received from CIC, the client must send the `AudioPlayer.ReportPlaybackState` event to CIC.  |
{% if book.TargetReaderType == "Internal" %}| [`RequestPlaybackState`](#RequestPlaybackState)         | Event  | Requests CIC the current playback state of the client. Upon receiving the `AudioPlayer.ReqeustPlaybackState` event, CIC will send the [`ExpectReportPlaybackState`](#ExpectReportPlaybackState) directive to all or specific clients registered to the user account.  |
| [`StreamDeliver`](#StreamDeliver)     | Directive | Response to the [`AudioPlayer.StreamRequested`](#StreamRequested) event used when receiving audio stream information that can be played. |{% else %}| [`StreamDeliver`](#StreamDeliver)     | Directive | Response to the [`AudioPlayer.StreamRequested`](#StreamRequested) event used when receiving audio stream information that can be played. |{% endif %}
| [`StreamRequested`](#StreamRequested) | Event     | Requests CIC for additional information needed for audio stream playback such as a streaming URL.               |
{% if book.TargetReaderType == "Internal" %}| [`SynchronizePlaybackState`](#SynchronizePlaybackState) | Directive | Instructs the client to synchronize the audio playback state. The client that had sent the `AudioPlayer.RequestPlaybackState` event will receive the `AudioPlayer.SynchronizePlaybackState` directive. |{% endif %}

## Sharing the audio playback state {#SharePlaybackState}

The client can receive a shared sound source playback state from all other or specific clients registered in the user account. The process to receive the shared audio playback state is as follows:

![](/CIC/Resources/Images/CIC_Playback_State_Sync_Work_Flow.png)

1. Clova app requests the audio playback state of all or specific clients registered in the user account to CIC using the {{ "[`AudioPlayer.RequestPlaybackState`](#RequestPlaybackState) event " if book.TargetReaderType == "Internal" }}.
2. CIC instructs all or specific clients registered in the [`AudioPlayer.ExpectReportPlaybackState`](#ExpectReportPlaybackState) user account to report the current audio playback state.
3. After receiving the report request, the client reports the current audio playback state using [`AudioPlayer.ReportPlaybackState`](#ReportPlaybackState) event.
4. CIC instructs the client that made the request to synchronize information by sending the states of the information using the {{ "[`AudioPlayer.SynchronizePlaybackState`](#SynchronizePlaybackState) event " if book.TargetReaderType == "Internal" }}.


## ClearQueue directive {#ClearQueue}
Instructs the client to initialize the playback queue of the audio stream. The `clearBehavior` field value of this directive distinguishes the reset action and the client determines whether or not to stop the currently playing audio stream by resetting the playback queue.

### Payload fields

| Field name       | Data type    | Description                     | Included |
|---------------|---------|-----------------------------|:---------:|
| `clearBehavior`           | string | The type of initialization.<ul><li><code>"CLEAR_ALL"</code>: Clear the playback queue and stop playing the audio stream.</li><li><code>"CLEAR_ENQUEUED"</code>: Clear the playback queue, but continue playing the audio stream.</li></ul> | Always |

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

## ExpectReportPlaybackState directive {#ExpectReportPlaybackState}

Instructs the client to report the current playback state. Upon receiving the directive, the client must send the [`AudioPlayer.ReportPlaybackState`](#ReportPlaybackState) event to CIC.

### Payload fields

None

### Message example
{% raw %}

```json
{
  "directive": {
    "header": {
      "namespace": "AudioPlayer",
      "name": "ExpectReportPlaybackState",
      "dialogRequestId": "9d7dc3ca-17ff-4df9-9800-91736ba2a3b6",
      "messageId": "46ccdf6c-609a-43a5-91c4-7a43b961f0c0"
    },
    "payload": {}
  }
}
```

{% endraw %}

### See also
* [`AudioPlayer.ReportPlaybackState`](#ReportPlaybackState)
* [Sharing the audio playback state](#SharePlaybackState)

## Play directive {#Play}
Instructs the client to either play or add to the playback queue the specified audio stream.

### Payload fields
| Field name       | Data type    | Description                     | Included |
|---------------|---------|-----------------------------|:---------:|
| `audioItem`               | object | The metadata of an audio stream to play and audio stream information required for playback.                     | Always |
| `audioItem.artImageUrl`   | string | The URL for the image on the audio (e.g. album image).                                                  | Conditional  |
| `audioItem.audioItemId`   | string | The ID of an audio stream. Use this ID to remove redundant Play directives. | Always |
| `audioItem.headerText`    | string | The text field used mainly to indicate the title of current play list.                                                | Conditional  |
| `audioItem.stream`        | [AudioStreamInfoObject](#AudioStreamInfoObject) | The audio stream information required for playback.        | Always |
| `audioItem.titleSubText1` | string | The text field used mainly to indicate the name of the artist.                                                          | Always |
| `audioItem.titleSubText2` | string | The text field used mainly to indicate the name of the album.                                                      | Conditional |
| `audioItem.titleText`     | string | The text field used mainly to indicate the title of the currently playing music.                                                         | Always  |
| `audioItem.type`          | string | **(Deprecated)** The name of the music service. This name can be the name of the streaming service provider or the service name. Use this value to determine which fields of the audioItem object are used for different service providers and select an appropriate parser to analyze them. | Always |
| `playBehavior`            | string | Indicates when to play the audio stream received from the directive. <ul><li><code>"REPLACE_ALL"</code>: Clear the playback queue and play the audio stream immediately.</li><li><code>"ENQUEUE"</code>: Clear the playback queue and add the audio stream.</li></ul> | Always |
| `source`                  | object | The information of the audio streaming service.                                                    | Always |
| `source.logoUrl`          | string | The URL for the logo of the audio streaming service. If this field is unavailable or undefined or if the logo cannot be displayed, you must at least display the name of the music service provider specified in the `source.name` field.  | Conditional |
| `source.name`             | string | The text field containing the name of the audio streaming service.                                                        | Always |

### Remarks
Based on the policy of music service providers, certain information required for playback (e.g. streaming URL) may not be shared to clients until right before playback. Whether extra information shall be requested is specified in the `audioItem.stream.urlPlayable` field as shown below:
* `urlPlayable` is `true`: No extra information is required. You can play the audio stream only with the URL specified in the `audioItem.stream.url` field.
* `urlPlayable` is `false`: Extra information is required for you to play the given audio stream. Make a request for extra information with the [`AudioPlayer.StreamRequested`](#StreamRequested) event.

### Message example
{% raw %}

```json
// Example: The audio stream that can be played only with the stream URL
{
  "directive": {
    "header": {
      "namespace": "AudioPlayer",
      "name": "Play",
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
        "name": "Potbbang",
        "logoUrl": "https://img.musicproviderdomain.net/logo_180125.png"
      },
      "playBehavior": "REPLACE_ALL"
    }
  }
}

// Example: The audio stream that cannot be played only with the stream URL
{
  "directive": {
    "header": {
      "namespace": "AudioPlayer",
      "name": "Play",
      "dialogRequestId": "277b40c3-b046-4f61-a551-783b1547e7b7",
      "messageId": "4e4080d6-c440-498a-bb73-ae86c6312806"
    },
    "payload": {
      "audioItem": {
        "audioItemId": "9CPWU-8362fe7c-f75c-42c6-806b-6f3e00aba8f1-c1862201",
        "album": {
          "albumId": "2000240",
          "genres": [
            "Classic"
          ],
          "title": "Wonderland - Edvard Grieg : Piano Concerto, Lyric Pieces"
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
        "title": "Symphony No.4 In A Op.90 'Italian' - III. Con Moto Moderato",
        "type": "SampleMusicProvider"
      },
      "source": {
        "name": "Sample Music Provider",
        "logoUrl": "https://img.musicproviderdomain.net/logo_180125.png"
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
Reports to CIC that the client has finished playback with the information on the audio stream.

### Context fields

{% include "/CIC/References/CICInterface/Context_Objects_List.md" %}

### Payload fields

| Field name       | Data type    | Description                     | Required |
|---------------|---------|-----------------------------|:---------:|
| `token`                | string | The `audioItem.stream.token` field value of the ['AudioPlayer.Play'](#Play) directive. | Required |
| `offsetInMilliseconds` | number | The current-time indicator of the audio playing (in milliseconds).                         | Required  |

### Message example
{% raw %}

```json
{
  "context": [
    {{Alerts.AlertsState}},
    {{AudioPlayer.PlayerState}},
    {{Device.DeviceState}},
    {{Device.Display}},
    {{Clova.Location}},
    {{Clova.SavedPlace}},
    {{Speaker.VolumeState}},
    {{SpeechSynthesizer.SpeechState}}
  ],
  "event": {
    "header": {
      "namespace": "AudioPlayer",
      "name": "PlayFinished",
      "messageId": "4e4080d6-c440-498a-bb73-ae86c6312806"
    },
    "payload": {
      "token": "TR-NM-4435786",
      "offsetInMilliseconds": 183000
    }
  }
}
```

{% endraw %}

### See also
* [`AudioPlayer.Play`](#Play)

## PlayPaused event {#PlayPaused}
Reports to CIC that the client has paused playback with the information on the audio stream. Send this event in the following scenario:

1. The client sends CIC a user voice request ([`SpeechRecognizer.Recognize`](/CIC/References/CICInterface/SpeechRecognizer.md#Recognize)) to pause playback of an audio stream.
2. CIC responds with the [`PlaybackController.Pause`](/CIC/References/CICInterface/PlaybackController.md#Pause) directive, as the result of voice recognition by Clova.
3. The client pauses playback of the audio stream and sends the PlayPaused event to CIC.

### Context fields

{% include "/CIC/References/CICInterface/Context_Objects_List.md" %}

### Payload fields

| Field name       | Data type    | Description                     | Required |
|---------------|---------|-----------------------------|:---------:|
| `token`                | string | The `audioItem.stream.token` field value of the ['AudioPlayer.Play'](#Play) directive. | Required |
| `offsetInMilliseconds` | number | The current-time indicator of the audio playing (in milliseconds).                         | Required  |

### Message example
{% raw %}

```json
{
  "context": [
    {{Alerts.AlertsState}},
    {{AudioPlayer.PlayerState}},
    {{Device.DeviceState}},
    {{Device.Display}},
    {{Clova.Location}},
    {{Clova.SavedPlace}},
    {{Speaker.VolumeState}},
    {{SpeechSynthesizer.SpeechState}}
  ],
  "event": {
    "header": {
      "namespace": "AudioPlayer",
      "name": "PlayPaused",
      "messageId": "4e4080d6-c440-498a-bb73-ae86c6312806"
    },
    "payload": {
      "token": "TR-NM-4435786",
      "offsetInMilliseconds": 83100
    }
  }
}
```

{% endraw %}

### See also
* [`AudioPlayer.Play`](#Play)
* [`AudioPlayer.PlayResumed`](#PlayResumed)
* [`PlaybackController.Pause`](/CIC/References/CICInterface/PlaybackController.md#Pause)

## PlayResumed event {#PlayResumed}

Reports to CIC that the client has resumed playback with the information on the audio stream. Send this event in the following scenario:

1. The client sends CIC a user voice request ([`SpeechRecognizer.Recognize`](/CIC/References/CICInterface/SpeechRecognizer.md#Recognize)) to resume the paused audio stream.
2. CIC responds with the [`PlaybackController.Resume`](/CIC/References/CICInterface/PlaybackController.md#Resume) directive, as the result of voice recognition by Clova.
3. The client resumes playback of the audio stream and sends the PlayResumed event to CIC.

### Context fields

{% include "/CIC/References/CICInterface/Context_Objects_List.md" %}

### Payload fields

| Field name       | Data type    | Description                     | Required |
|---------------|---------|-----------------------------|:---------:|
| `token`                | string | The `audioItem.stream.token` field value of the ['AudioPlayer.Play'](#Play) directive. | Required |
| `offsetInMilliseconds` | number | The current-time indicator of the audio playing (in milliseconds).                         | Required  |

### Message example
{% raw %}

```json
{
  "context": [
    {{Alerts.AlertsState}},
    {{AudioPlayer.PlayerState}},
    {{Device.DeviceState}},
    {{Device.Display}},
    {{Clova.Location}},
    {{Clova.SavedPlace}},
    {{Speaker.VolumeState}},
    {{SpeechSynthesizer.SpeechState}}
  ],
  "event": {
    "header": {
      "namespace": "AudioPlayer",
      "name": "PlayResumed",
      "messageId": "4e4080d6-c440-498a-bb73-ae86c6312806"
    },
    "payload": {
      "token": "TR-NM-4435786",
      "offsetInMilliseconds": 83100
    }
  }
}
```

{% endraw %}

### See also
* [`AudioPlayer.Play`](#Play)
* [`AudioPlayer.PlayPaused`](#PlayPaused)
* [`PlaybackController.Resume`](/CIC/References/CICInterface/PlaybackController.md#Resume)

## PlayStarted event {#PlayStarted}
Reports to CIC that the client has started playback with the information on the audio stream.

### Context fields

{% include "/CIC/References/CICInterface/Context_Objects_List.md" %}

### Payload fields

| Field name       | Data type    | Description                     | Required |
|---------------|---------|-----------------------------|:---------:|
| `token`                | string | The `audioItem.stream.token` field value of the ['AudioPlayer.Play'](#Play) directive. | Required |
| `offsetInMilliseconds` | number | The current-time indicator of the audio playing (in milliseconds).                         | Required  |

### Message example
{% raw %}

```json
{
  "context": [
    {{Alerts.AlertsState}},
    {{AudioPlayer.PlayerState}},
    {{Device.DeviceState}},
    {{Device.Display}},
    {{Clova.Location}},
    {{Clova.SavedPlace}},
    {{Speaker.VolumeState}},
    {{SpeechSynthesizer.SpeechState}}
  ],
  "event": {
    "header": {
      "namespace": "AudioPlayer",
      "name": "PlayStarted",
      "messageId": "4e4080d6-c440-498a-bb73-ae86c6312806"
    },
    "payload": {
      "token": "TR-NM-4435786",
      "offsetInMilliseconds": 0
    }
  }
}
```

{% endraw %}

### See also
* [`AudioPlayer.Play`](#Play)
* [`AudioPlayer.PlayStopped`](#PlayStopped)

## PlayStopped event {#PlayStopped}
Reports to CIC that the client has stopped playback with the information on the audio stream. Send this event in the following scenario:

1. The client sends CIC a user voice request ([`SpeechRecognizer.Recognize`](/CIC/References/CICInterface/SpeechRecognizer.md#Recognize)) to stop playback of an audio stream.
2. CIC responds with the [`PlaybackController.Stop`](/CIC/References/CICInterface/PlaybackController.md#Stop) directive, as the result of voice recognition by Clova.
3. The client stops playback of the audio stream and sends the PlayStopped event to CIC.

### Context fields

{% include "/CIC/References/CICInterface/Context_Objects_List.md" %}

### Payload fields

| Field name       | Data type    | Description                     | Required |
|---------------|---------|-----------------------------|:---------:|
| `token`                | string | The `audioItem.stream.token` field value of the ['AudioPlayer.Play'](#Play) directive. | Required |
| `offsetInMilliseconds` | number | The current-time indicator of the audio playing (in milliseconds).                         | Required  |

### Message example
{% raw %}

```json
{
  "context": [
    {{Alerts.AlertsState}},
    {{AudioPlayer.PlayerState}},
    {{Device.DeviceState}},
    {{Device.Display}},
    {{Clova.Location}},
    {{Clova.SavedPlace}},
    {{Speaker.VolumeState}},
    {{SpeechSynthesizer.SpeechState}}
  ],
  "event": {
    "header": {
      "namespace": "AudioPlayer",
      "name": "PlayStopped",
      "messageId": "4e4080d6-c440-498a-bb73-ae86c6312806"
    },
    "payload": {
      "token": "TR-NM-4435786",
      "offsetInMilliseconds": 83100
    }
  }
}
```

{% endraw %}

### See also
* [`AudioPlayer.Play`](#Play)
* [`AudioPlayer.PlayStarted`](#PlayStarted)
* [`PlaybackController.Stop`](/CIC/References/CICInterface/PlaybackController.md#Stop)

## ProgressReportDelayPassed event {#ProgressReportDelayPassed}
Reports to CIC the current playback state ([`AudioPlayer.PlaybackState`](/CIC/References/Context_Objects.md#PlaybackState)) after the delay—specified period of time—has passed. The delay is specified in the [`AudioPlayer.Play`](#Play) directive.

### Context fields

{% include "/CIC/References/CICInterface/Context_Objects_List.md" %}

### Payload fields

| Field name       | Data type    | Description                     | Required |
|---------------|---------|-----------------------------|:---------:|
| `token`                | string | The `audioItem.stream.token` field value of the ['AudioPlayer.Play'](#Play) directive. | Required |
| `offsetInMilliseconds` | number | The current-time indicator of the audio playing (in milliseconds).                         | Required  |

### Message example
{% raw %}

```json
{
  "context": [
    {{Alerts.AlertsState}},
    {{AudioPlayer.PlayerState}},
    {{Device.DeviceState}},
    {{Device.Display}},
    {{Clova.Location}},
    {{Clova.SavedPlace}},
    {{Speaker.VolumeState}},
    {{SpeechSynthesizer.SpeechState}}
  ],
  "event": {
    "header": {
      "namespace": "AudioPlayer",
      "name": "ProgressReportDelayPassed",
      "messageId": "4e4080d6-c440-498a-bb73-ae86c6312806"
    },
    "payload": {
      "token": "TR-NM-4435786",
      "offsetInMilliseconds": 60000
    }
  }
}
```

{% endraw %}

### See also
* [`AudioPlayer.Play`](#Play)
* [`AudioPlayer.ProgressReportIntervalPassed`](#ProgressReportIntervalPassed)
* [`AudioPlayer.ProgressReportPositionPassed`](#ProgressReportPositionPassed)

## ProgressReportIntervalPassed event {#ProgressReportIntervalPassed}
Reports to CIC the current playback state ([`AudioPlayer.PlaybackState`](/CIC/References/Context_Objects.md#PlaybackState)), by the specified interval, after playback has started. The interval is specified in the [`AudioPlayer.Play`](#Play) directive.

### Context fields

{% include "/CIC/References/CICInterface/Context_Objects_List.md" %}

### Payload fields

| Field name       | Data type    | Description                     | Required |
|---------------|---------|-----------------------------|:---------:|
| `token`                | string | The `audioItem.stream.token` field value of the ['AudioPlayer.Play'](#Play) directive. | Required |
| `offsetInMilliseconds` | number | The current-time indicator of the audio playing (in milliseconds).                         | Required  |

### Message example
{% raw %}

```json
{
  "context": [
    {{Alerts.AlertsState}},
    {{AudioPlayer.PlayerState}},
    {{Device.DeviceState}},
    {{Device.Display}},
    {{Clova.Location}},
    {{Clova.SavedPlace}},
    {{Speaker.VolumeState}},
    {{SpeechSynthesizer.SpeechState}}
  ],
  "event": {
    "header": {
      "namespace": "AudioPlayer",
      "name": "ProgressReportIntervalPassed",
      "messageId": "4e4080d6-c440-498a-bb73-ae86c6312806"
    },
    "payload": {
      "token": "TR-NM-4435786",
      "offsetInMilliseconds": 120000
    }
  }
}
```

{% endraw %}

### See also
* [`AudioPlayer.Play`](#Play)
* [`AudioPlayer.ProgressReportDelayPassed`](#ProgressReportDelayPassed)
* [`AudioPlayer.ProgressReportPositionPassed`](#ProgressReportPositionPassed)

## ProgressReportPositionPassed event {#ProgressReportPositionPassed}
Reports to CIC the current playback state ([`AudioPlayer.PlaybackState`](/CIC/References/Context_Objects.md#PlaybackState)) at the specified time, which is measured from the start of the audio stream. The reporting time is specified in the [`AudioPlayer.Play`](#Play) directive.

### Context fields

{% include "/CIC/References/CICInterface/Context_Objects_List.md" %}

### Payload fields

| Field name       | Data type    | Description                     | Required |
|---------------|---------|-----------------------------|:---------:|
| `token`                | string | The `audioItem.stream.token` field value of the ['AudioPlayer.Play'](#Play) directive. | Required |
| `offsetInMilliseconds` | number | The current-time indicator of the audio playing (in milliseconds).                         | Required  |

### Message example
{% raw %}

```json
{
  "context": [
    {{Alerts.AlertsState}},
    {{AudioPlayer.PlayerState}},
    {{Device.DeviceState}},
    {{Device.Display}},
    {{Clova.Location}},
    {{Clova.SavedPlace}},
    {{Speaker.VolumeState}},
    {{SpeechSynthesizer.SpeechState}}
  ],
  "event": {
    "header": {
      "namespace": "AudioPlayer",
      "name": "ProgressReportPositionPassed",
      "messageId": "4e4080d6-c440-498a-bb73-ae86c6312806"
    },
    "payload": {
      "token": "TR-NM-4435786",
      "offsetInMilliseconds": 150000
    }
  }
}
```

{% endraw %}

### See also
* [`AudioPlayer.Play`](#Play)
* [`AudioPlayer.ProgressReportDelayPassed`](#ProgressReportDelayPassed)
* [`AudioPlayer.ProgressReportIntervalPassed`](#ProgressReportIntervalPassed)

## ReportPlaybackState event {#ReportPlaybackState}

Reports to CIC the current playback state of the client. If the [`AudioPlayer.ExpectReportPlaybackState`](#ExpectReportPlaybackState) directive is received from CIC, the client must send the `AudioPlayer.ReportPlaybackState` event to CIC.

### Context fields

{% include "/CIC/References/CICInterface/Context_Objects_List.md" %}

### Payload fields
| Field name       | Data type    | Description                     | Required |
|---------------|---------|-----------------------------|:---------:|
| `offsetInMilliseconds`   | number  | The current-time indicator of the audio playing (in milliseconds).  | Optional  |
| `playerActivity`         | string  | The current state of audio player.<ul><li><code>"IDLE"</code>: Not in use</li><li><code>"PLAYING"</code>: Playing</li><li><code>"PAUSED"</code>: Paused</li><li><code>"STOPPED"</code>: Stopped</li></ul>  | Required  |
| `repeatMode`             | string  | The repeat mode.<ul><li><code>"NONE"</code>: None</li><li><code>"REPEAT_ONE"</code>: Repeat one song</li></ul>  | Required  |
| `stream`                 | [AudioStreamInfoObject](#AudioStreamInfoObject) | The `audioItem.stream` of the Play directive.                                     | Optional |
| `token`                  | string  | The `audioItem.stream.token` field value of the ['AudioPlayer.Play'](#Play) directive.                                          | Optional |
| `totalInMilliseconds`    | number | The total duration of the recently played media. Enter the value of the `durationInMilliseconds` field of the [AudioStreamInfoObject](/CIC/References/CICInterface/AudioPlayer.md#AudioStreamInfoObject) provided by the [`AudioPlayer.Play`](/CIC/References/CICInterface/AudioPlayer.md#Play) directive, if the value is available. The unit is in milliseconds. This field is omissible if the `playerActivity` field is set to `"IDLE"`. | Optional |

### Message example
{% raw %}

```json
{
  "context": [
    {{Alerts.AlertsState}},
    {{AudioPlayer.PlayerState}},
    {{Device.DeviceState}},
    {{Device.Display}},
    {{Clova.Location}},
    {{Clova.SavedPlace}},
    {{Speaker.VolumeState}},
    {{SpeechSynthesizer.SpeechState}}
  ],
  "event": {
    "header": {
      "namespace": "AudioPlayer",
      "name": "ReportPlaybackState",
      "messageId": "3e57f11a-a02d-4b6f-b183-fdfb6105c650"
    },
    "payload": {
      "playerActivity": "IDLE",
      "repeatMode": "NONE"
    }
  }
}
```

{% endraw %}

### See also
* [`AudioPlayer.ExpectReportPlaybackState`](#ExpectReportPlaybackState)
* [`AudioPlayer.Play`](#Play)
* [Sharing the audio playback state](#SharePlaybackState)

{% if book.TargetReaderType == "Internal" %}
## RequestPlaybackState event {#RequestPlaybackState}

Requests CIC the current playback state of the client. Upon receiving the `AudioPlayer.ReqeustPlaybackState` event, CIC will send the [`AudioPlayer.ExpectReportPlaybackState`](#ExpectReportPlaybackState) directive to all or specific clients registered to the user account.

### Context fields

{% include "/CIC/References/CICInterface/Context_Objects_List.md" %}

### Payload fields
| Field name       | Data type    | Description                     | Required |
|---------------|---------|-----------------------------|:---------:|
| `deviceId`    | string  | The ID of the target client. The opaque ID in a random format. If this field is omitted, the request is broadcasted to all clients registered in the user account. | Optional |

### Message example
{% raw %}

```json
{
  "context": [
    {{Alerts.AlertsState}},
    {{AudioPlayer.PlayerState}},
    {{Device.DeviceState}},
    {{Device.Display}},
    {{Clova.Location}},
    {{Clova.SavedPlace}},
    {{Speaker.VolumeState}},
    {{SpeechSynthesizer.SpeechState}}
  ],
  "event": {
    "header": {
      "namespace": "AudioPlayer",
      "name": "RequestPlaybackState",
      "messageId": "15323cb4-859f-4d5e-b7f4-a7b60ff41866"
    },
    "payload": {
      "deviceId": "5a849a66-c182-4c1b-8a97-b63cac2d396c"
    }
  }
}
```

{% endraw %}

### See also
* [`AudioPlayer.ExpectReportPlaybackState`](#ExpectReportPlaybackState)
* [`AudioPlayer.Play`](#Play)
* [Sharing the audio playback state](#SharePlaybackState)
{% endif %}

## StreamDeliver directive {#StreamDeliver}
Response to the [`AudioPlayer.StreamRequested`](#StreamRequested) event used when receiving audio stream information that can be played. The directive contains the URL for audio streaming as mandatory information so the client can play the audio.

### Payload fields
| Field name | Data type | Description | Included |
|---------|------|--------|:---------:|
| `audioItemId` | string | The ID of the audio stream. Use this ID to remove redundant Play directives. | Always |
| `audioStream` | [AudioStreamInfoObject](#AudioStreamInfoObject) | The audio stream information required for playback.       | Always |

### Remarks
Some contents of the `AudioStreamInfoObject` object provided by the `StreamDeliver` directive may be omitted to avoid overlapping of information with the `AudioStreamInfoObject` object provided by the [`AudioPlayer.Play`](#Play) directive. Therefore, you must combine the `payload.audioStream` information of the `StreamDeliver` directive and the received [`Play`](#Play) directive when playing the audio.

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
Requests CIC for additional information needed for audio stream playback such as a streaming URL.

### Context fields

{% include "/CIC/References/CICInterface/Context_Objects_List.md" %}

### Payload fields
| Field name       | Data type    | Description                     | Required |
|---------------|---------|-----------------------------|:---------:|
| `audioItemId`   | string  | The `audioItem.audioItemId` field value of the ['AudioPlayer.Play'](#Play) directive.       | Required |
| `audioStream`   | [AudioStreamInfoObject](#AudioStreamInfoObject) | The `audioItem.stream` of the Play directive. | Required |

### Remarks
Based on the policy of music service providers, certain information required for playback (e.g. streaming URL) may not be shared to clients until right before playback. This event is an interface for the cases where the stream information has to be held back. Do not send this event earlier than right before playing an audio stream.

### Message example
{% raw %}

```json
{
  "context": [
    {{Alerts.AlertsState}},
    {{AudioPlayer.PlayerState}},
    {{Device.DeviceState}},
    {{Device.Display}},
    {{Clova.Location}},
    {{Clova.SavedPlace}},
    {{Speaker.VolumeState}},
    {{SpeechSynthesizer.SpeechState}}
  ],
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

{% if book.TargetReaderType == "Internal" %}
## SynchronizePlaybackState directive {#SynchronizePlaybackState}

Instructs the client to synchronize the audio playback state. The client that had sent the `AudioPlayer.RequestPlaybackState` event will receive the `AudioPlayer.SynchronizePlaybackState` directive.

### Payload fields

| Field name       | Data type    | Description                     | Included |
|---------------|---------|-----------------------------|:---------:|
| `deviceId`    | string  | The ID of the target client. The opaque ID in a random format.  | Always  |
| `event`       | string  | The event occurred in the client.<ul><li><code>PlayFinished</code></li><li><code>PlayPaused</code></li><li><code>PlayResumed</code></li><li><code>PlayStarted</code></li><li><code>PlayStopped</code></li></ul>  | Conditional  |
| `playbackState`          | object  | The playback state of the client.             | Conditional  |
| `playbackState.offsetInMilliseconds`   | number  | The current-time indicator of the audio playing The unit is in milliseconds. This field can have a null value.  | Conditional  |
| `playbackState.playerActivity`         | string  | The current state of audio player.<ul><li><code>"IDLE"</code>: Not in use</li><li><code>"PLAYING"</code>: Playing</li><li><code>"PAUSED"</code>: Paused</li><li><code>"STOPPED"</code>: Stopped</li></ul>  | Always  |
| `playbackState.repeatMode`             | string  | The repeat mode.<ul><li><code>"NONE"</code>: None</li><li><code>"REPEAT_ONE"</code>: Repeat one song</li></ul>  | Always  |
| `playbackState.stream`                 | [AudioStreamInfoObject](#AudioStreamInfoObject) | The information on the audio stream.                                         | Always |
| `playbackState.token`                  | string  | The token to identify the audio playback. This field may be an empty string (`""`).                                                    | Always |
| `playbackState.totalInMilliseconds`    | number | The total duration of the recently played media. The unit is in milliseconds. This field can have a null value.                  | Always |

### Message example
{% raw %}

```json
{
  "directive": {
    "header": {
      "namespace": "AudioPlayer",
      "name": "SynchronizePlaybackState",
      "dialogRequestId": "9d7dc3ca-17ff-4df9-9800-91736ba2a3b6",
      "messageId": "46ccdf6c-609a-43a5-91c4-7a43b961f0c0"
    },
    "payload": {
      "deviceId": "2fe8f3e8-85be-4a45-863e-beec7314ba2e",
      "playbackState": {
        "playerActivity": "IDLE",
        "repeatMode": "NONE"
      }
    }
  }
}
```

{% endraw %}

### See also
* [`AudioPlayer.ReportPlaybackState`](#ReportPlaybackState)
* [Sharing the audio playback state](#SharePlaybackState)
{% endif %}

## Shared objects
Common objects are included in the message body (`payload`) of events or directives when they are sent with the AudioPlayer API.

| Object name            | Description                                            |
|--------------------|---------------------------------------------------|
| [AudioStreamInfoObject](#AudioStreamInfoObject) | The playback details of an audio stream such as a streaming address and credentials. |

### AudioStreamInfoObject {#AudioStreamInfoObject}
The streaming details of an audio stream. This object is used when CIC returns streaming details to a client or when the client sends the details of the currently playing audio stream to CIC.

#### Object fields
| Field name       | Data type    | Description                     | Required/Included |
|---------------|---------|-----------------------------|:-------------:|
| `beginAtInMilliseconds`  | number | The playback start point. The unit is in milliseconds. If this field is specified, play the audio stream from the specified point of the stream. If set to 0, play the audio stream from the beginning.          | Required/Always |
| `customData`             | string | The metadata on the current audio in a random format. Any streaming information that cannot be classified into a specific category or defined must be included or entered in this field. Streaming service providers can add custom values to the context of audio stream playback.<div class="danger"><p><strong>Caution!</strong></p><p>Clients must not use the value of this field, as it can cause problems. Make sure to insert these field values in the `stream` field of the <a href="/CIC/References/Context_Objects.html#PlaybackState">PlaybackState context</a> without any changes, when reporting the playback state to CIC.</p></div> | Optional/Conditional  |
| `durationInMilliseconds` | number | The length of the audio stream. The client can play and navigate audio from the playback time specified in the `beginAtInMilliseconds` field by the amount of time defined in this field. For example, if the value of `beginAtInMilliseconds` field is `10000` and the value of this field is `60000`, you can play and navigate within 10-70 seconds of the audio track. (in milliseconds).   | Optional/Conditional  |
| `progressReport`         | object  | The time specified to receive the playback state after the audio starts.                                                  | Optional/Conditional |
| `progressReport.progressReportDelayInMilliseconds`    | number | The duration of time specified to receive the playback state after the audio starts. The unit is in milliseconds. This field can have a null value.  | Optional/Conditional |
| `progressReport.progressReportIntervalInMilliseconds` | number | The interval specified to receive the playback state while audio is playing. The unit is in milliseconds. This field can have a null value.        | Optional/Conditional |
| `progressReport.progressReportPositionInMilliseconds` | number | The point of time specified to receive the playback state to while audio is playing. The unit is in milliseconds. This field can have a null value.    | Optional/Conditional |
| `token`                  | string  | The token of the audio stream.                                                                                   | Required/Always |
| `url`                    | string  | The URL of the audio stream.                                                                                     | Required/Always |
| `urlPlayable`            | boolean | Indicates whether the audio stream URL in the `url` field can be played immediately. <ul><li><code>true</code>: The client can play the audio without additional information.</li><li><code>false</code>: The client requires additional information. To obtain additional information on audio streaming, send the <a href="#StreamRequested"><code>AudioPlayer.StreamRequested</code></a> event to CIC.</li></ul>        | Required/Always |

#### Remarks
* Once the audio section designated in `beginAtInMilliseconds` and `durationInMilliseconds` fields finishes playing, the client must send the [`AudioPlayer.PlayFinished`](#PlayFinished) event to CIC
* The UI of a client must prevent users from navigating through the audio in times other than the section defined in `beginAtInMilliseconds` and `durationInMilliseconds` fields.
* When reporting the current playback state to CIC, set the `totalInMilliseconds` field value of [`AudioPlayer.PlaybackState`](/CIC/References/Context_Objects.md#PlaybackState) as the combined value in `beginAtInMilliseconds` and `durationInMilliseconds` fields.

#### Object Example
{% raw %}

```json
// An example of an audio stream that can be played only with the URL
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

// Example: The audio stream that cannot be played only with the stream URL
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
* [`AudioPlayer.StreamRequested`](#StreamRequested)
