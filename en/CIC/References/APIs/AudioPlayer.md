# AudioPlayer

Instructs your client to play an audio stream or reports to CIC on events that occur during playback. The AudioPlayer API provides the following event and directive messages.

| Message name  | Message type  | Message description  |
|------------------|-----------|---------------------------------------------|
| [`Play`](#Play)  | Directive | Instructs your client to start playback of a specified audio stream or add it to a playback queue.  |
| [`PlayFinished`](#PlayFinished)  | Event  | Reports to CIC on audio stream details when your client finishes playback of an audio stream.  |
| [`PlayPaused`](#PlayPaused)  | Event  | Reports to CIC on audio stream details when your client pauses playback of an audio stream. |
| [`PlayResumed`](#PlayResumed)  | Event  | Reports to CIC on audio stream details when your client resumes playback of an audio stream.  |
| [`PlayStarted`](#PlayStarted)  | Event  | Reports to CIC on audio stream details when your client starts playback of an audio stream.  |
| [`PlayStopped`](#PlayStopped)  | Event  | Reports to CIC on audio stream details when your client stops playback of an audio stream.  |
| [`ProgressReportDelayPassed`](#ProgressReportPositionPassed) | Event | Reports to CIC on a current playback state ([`AudioPlayer.PlaybackState`](/CIC/References/Context_Objects.md#PlaybackState)) when a specified delay time has passed after playback has started. You can check the delay time for each audio stream when an [`AudioPlayer.Play`](#Play) directive message is returned to your client. |
| [`ProgressReportIntervalPassed`](#ProgressReportPositionPassed)| Event | Reports to CIC on a current playback state ([`AudioPlayer.PlaybackState`](/CIC/References/Context_Objects.md#PlaybackState)) regularly at a specified interval of time after playback has started. You can check the reporting interval for each audio stream when an [`AudioPlayer.Play`](#Play) directive message is returned to your client. |
| [`ProgressReportPositionPassed`](#ProgressReportPositionPassed) | Event | Reports to CIC on a current playback state ([`AudioPlayer.PlaybackState`](/CIC/References/Context_Objects.md#PlaybackState)) at a specified reporting point after playback has started. You can check the reporting point for each audio stream when an [`AudioPlayer.Play`](#Play) directive message is returned to your client. |
| [`StreamDeliver`](#StreamDeliver)  | Directive | Returns audio stream details necessary for playback. This is a response message to an [`AudioPlayer.StreamRequested`](#StreamRequested) event message. |
| [`StreamRequested`](#StreamRequested) | Event  | Requests CIC for additional audio stream details necessary for playback, such as a streaming URL.  |

## Play directive {#Play}
Instructs your client to play a specified audio stream or add it to a playback queue.

### Payload field
| Field name  | Type  | Field description  | Required |
|---------------|---------|-----------------------------|---------|
| `audioItem`  | object | An object containing metadata of an audio stream and audio stream details necessary for playback  | Yes |
| `audioItem.audioItemId`  | string | The ID for distinguishing audio stream details. You can remove redundant Play directive messages based on this value. | Yes |
| `audioItem.stream`  | [AudioStreamObject](#AudioStreamObject) | An object containing audio stream details necessary for playback  | Yes |
| `audioItem.type`  | string | A music service delimiter. It is the name of a business entity or service that provides a music streaming service. You can use this value to figure out the fields in the audioItem object for each different service and select an appropriate parser to analyze them. | Yes |
| `audioItem.[CustomField]` | any  | Service providers can add extra metadata to the audio stream for playback.  | No |
| `playBehavior`  | string | A delimiter that determines when your client will play the audio stream included in the directive message <ul><li><strong>"REPLACE_ALL"</strong>: Clears all existing playback queues and play this audio stream immediately.</li><li><strong>"ENQUEUE"</strong>: Adds this audio stream to a playback queue.</li></ul> | Yes |

### Remarks
Sometimes, due to the way music services charge users, streaming details such as a streaming URL can only be obtained right before playback. Depending on the value of the `audioItem.stream.urlPlayable` field, it can be either one of the following.
* If the `urlPlayable` field is set to **true**, you can play the audio stream directly from the URL in the `audioItem.stream.url` field.
* If the `urlPlayable` field is set to **false**, you cannot play the audio stream directly from the URL in the `audioItem.stream.url` field. Instead, you must request additional audio stream details using the [`AudioPlayer.StreamRequested`](#StreamRequested) event message.

### Message example
{% raw %}
```json
// Example of an audio stream URL which you can play from directly
{
  "audioItem": {
    "bgImageUrl": "https://api-ex.podbbang.com/img/12548/b",
    "episodeId": 22346122,
    "episodeTitle": "0803 뉴스공장 1-2부 (김성태, 안민석)",
    "playImageUrl": "https://api-ex.podbbang.com/img/12548",
    "podcastId": 12548,
    "podcastTitle": "tbs 김어준의 뉴스공장",
    "skipFullscreen": false,
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
      "url": "https://api-ex.podbbang.com/file/12548/22346122",
      "urlPlayable": true
    },
    "type": "podcast",
    "updatedDate": "2017.08.03"
  },
  "playBehavior": "REPLACE_ALL"
}

// Example of an audio stream URL which you cannot play from directly
{
  "audioItem": {
    "album": {
      "albumId": "2000240",
      "fullImageUrl": "http://musicmeta.phinf.naver.net/album/002/000/2000240.jpg?type=r1440Fll&v=20170622114402",
      "genres": [
        "발라드",
        "알앤비/어반"
      ],
      "id": "AL-NM-2000240",
      "imageUrl": "http://musicmeta.phinf.naver.net/album/002/000/2000240.jpg?type=r204Fll&v=20170622114402",
      "isAdult": false,
      "isRegular": false,
      "title": "Palette",
      "url": "http://nozzle.naver.com:10080/1/catalog/AL-NM-2000240/"
    },
    "arrangers": [
      {
        "name": "김제휘"
      }
    ],
    "artists": [
      {
        "artistId": "112579",
        "id": "AR-NM-112579",
        "imageUrl": "http://musicmeta.phinf.naver.net/artist/000/112/112579.jpg?type=r240",
        "isGroup": false,
        "name": "아이유(IU)",
        "url": "http://nozzle.naver.com:10080/1/catalog/AR-NM-112579/"
      }
    ],
    "audioItemId": "9CPWU-8362fe7c-f75c-42c6-806b-6f3e00aba8f1-c1862201",
    "discNo": 1,
    "hasLyrics": true,
    "hasNaverSyncLyrics": true,
    "hasVideo": false,
    "id": "TR-NM-17716562",
    "isAdult": false,
    "isRepresent": false,
    "isStreaming": true,
    "lyricists": [
      {
        "name": "아이유(IU)"
      }
    ],
    "lyrics": "이건 비밀이야 \n아무에게도 고백하지 않았던\n이야기를 들려주면\n큰 눈으로 너는 묻지\nHow wow wow\nWhatever\n\n나 실은 말이야\n저기 아득한 \n미래로부터 날아왔어\n쏟아질 듯이 빼곡한 \n별들 사이를 지나 \nFly fly fly\n\n있지 그곳도 사실 \n바보들투성이야\n아니 매우 반짝이는 건 오히려 \nNow now now\n\n이 하루 이 지금 우리 \n눈부셔 아름다워\n이 불꽃놀이는 끝나지 않을 거야 \nOoh Whatever\n\n흐린 날이면\n거짓말처럼 무섭게 깜깜했지\n새침데기 태양은 \n뜨겁기는 커녕 Peacoke\nBlue blue blue Whatever\n\n매일매일\n제멋대로인 바람결을 땋아서 만든\n이 나침반이 가리킨 그곳에서 발견!\nOh That's you you yes, you \n\n있지 저런 건 \n그저 자그만 돌멩이야\n빛이 나는 건 여기 있잖아\nLife is cool cool cool\n\n시간은 많아 이대로면 아마 \n영원히 살 수 있지 않을까\n안녕 나의 주인공 그래 \n너를 만나러 나\n짜잔 우아하게 등장!\n\n바로 이 하루 이 지금 우리\n눈부셔 아름다워  \n나는 확실히 알아 \n오늘의 불꽃놀이는 \n끝나지 않을 거야 \n우우우 우우우\n우우우 우우우\n\n더 놀라운 건 지금부터야",
    "naverSyncLyrics": "0|이건 비밀이야\n#2|아무에게도 고백하지 않았던\n#8|이야기를 들려주면\n#10|큰 눈으로 너는 묻지\n#13|How wow wow Whatever\n#17|나 실은 말이야\n#19|저기 아득한 미래로부터 날아왔어\n#24|쏟아질 듯이 빼곡한 별들 사이를 지나 Fly fly fly\n#32|있지 그곳도 사실 바보들투성이야\n#40|아니 매우 반짝이는 건 오히려 Now now now\n#48|이 하루 이 지금 우리\n#52|눈부셔 아름다워\n#54|이 불꽃놀이는 끝나지 않을 거야 Ooh Whatever\n#65|흐린 날이면\n#66|거짓말처럼 무섭게 깜깜했지\n#72|새침데기 태양은 뜨겁기는 커녕 Peacoke\n#76|Blue blue blue Whatever\n#81|매일매일\n#82|제멋대로인 바람결을 땋아서 만든\n#89|이 나침반이 가리킨 그곳에서 발견\n#92|Oh That's you you yes you\n#96|있지 저런 건 그저 자그만 돌멩이야\n#104|빛이 나는 건 여기 있잖아\n#107|Life is cool cool cool\n#110|시간은 많아 이대로면 아마\n#116|영원히 살 수 있지 않을까\n#120|안녕 나의 주인공 그래 너를 만나러 나\n#124|짜잔 우아하게 등장\n#127|바로 이 하루 이 지금 우리\n#132|눈부셔 아름다워\n#134|나는 확실히 알아 오늘의 불꽃놀이는\n#140|끝나지 않을 거야\n#144|우우우 우우우 우우우 우우우\n#160|더 놀라운 건 지금부터야\n#500|#@500|#@",
    "nozzle": {
      "likedByMe": false
    },
    "score": 0.8217,
    "songwriters": [
      {
        "name": "김제휘"
      }
    ],
    "station": {
      "title": "아이유 스테이션"
    },
    "stream": {
      "beginAtInMilliseconds": 0,
      "p3TapCursor": "c1862201",
      "p3TapId": "9CPWU-8362fe7c-f75c-42c6-806b-6f3e00aba8f1",
      "p3TapNextCursor": "c1867299",
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
    "totalArtistCount": 1,
    "trackId": "17716562",
    "trackNo": 1,
    "type": "navermusic",
    "url": "http://nozzle.naver.com:10080/1/catalog/TR-NM-17716562/"
  },
  "playBehavior": "REPLACE_ALL"
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
      "dialogRequestId": "277b40c3-b046-4f61-a551-783b1547e7b7",
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

1. Your client sends CIC a user's spoken request to pause playback of an audio stream, using a [`SpeechRecognizer.Recognize`](/CIC/References/APIs/SpeechRecognizer.md#Recognize) event message.
2. The Clova platform recognizes the pause request and CIC returns it to your client, using a [`PlaybackController.Pause`](/CIC/References/APIs/PlaybackController.md#Pause) directive message.
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
      "dialogRequestId": "277b40c3-b046-4f61-a551-783b1547e7b7",
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
* [`PlaybackController.Pause`](/CIC/References/APIs/PlaybackController.md#Pause)

## PlayResumed event {#PlayResuemd}
Reports to CIC on audio stream details when your client resumes playback of an audio stream. Send this event message in the following scenario.

1. Your client sends CIC a user's spoken request to resume playback of an audio stream, using a [`SpeechRecognizer.Recognize`](/CIC/References/APIs/SpeechRecognizer.md#Recognize) event message.
2. The Clova platform recognizes the resume request and CIC sends it to your client, using a [`PlaybackController.Resume`](/CIC/References/APIs/PlaybackController.md#Resume) directive message.
3. Your client resumes playback of the audio stream and sends CIC a PlayResumed event message.

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
* [`AudioPlayer.Play`](#Play)
* [`AudioPlayer.PlayPaused`](#PlayPaused)
* [`PlaybackController.Resume`](/CIC/References/APIs/PlaybackController.md#Resume)

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
      "dialogRequestId": "277b40c3-b046-4f61-a551-783b1547e7b7",
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

1. Your client sends CIC a user's spoken request to stop playback of an audio stream, using a [`SpeechRecognizer.Recognize`](/CIC/References/APIs/SpeechRecognizer.md#Recognize) event message.
2. The Clova platform recognizes the stop request and CIC returns it to your client, using a [`PlaybackController.Stop`](/CIC/References/APIs/PlaybackController.md#Stop) directive message.
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
      "dialogRequestId": "277b40c3-b046-4f61-a551-783b1547e7b7",
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
* [`PlaybackController.Stop`](/CIC/References/APIs/PlaybackController.md#Stop)

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
      "dialogRequestId": "277b40c3-b046-4f61-a551-783b1547e7b7",
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
      "dialogRequestId": "277b40c3-b046-4f61-a551-783b1547e7b7",
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
      "dialogRequestId": "277b40c3-b046-4f61-a551-783b1547e7b7",
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
Returns audio stream details necessary for playback. This is a response message to an [`AudioPlayer.StreamRequested`](#StreamRequested) event message. It must contain a streaming URL from which your client can play music.

### Payload field
| Field name | Type | Field description | Required |
|---------|------|--------|---------|
| `audioItemId` | string | A value for distinguishing audio stream details. You can remove redundant Play directive messages based on this value. | Yes |
| `audioStream`| [AudioStreamObject](#AudioStreamObject) | An object containing audio stream details necessary for playback  | Yes |

### Remarks
You can implement audio stream playback by combining the StreamDeliver directive message with `payload.audioStream` of the previously received [Play](#Play) directive message. However, you must not replace the values of the previous Play directive message with the new values passed through the `StreamDeliver` directive message. The reason is that, if any content of the `AudioStreamObject` in the `StreamDeliver` directive message overlaps with the content of the previous [`AudioPlayer.Play`](#Play) directive message, that overlapping content might be omitted. This may cause unexpected behaviors when you handle the same Play directive message more than once, for example, to play a track repeatedly or to play a previous track.

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

### Events field
| Field name  | Type  | Field description  | Required |
|---------------|---------|-----------------------------|---------|
| `audioItemId`  | string  | `audioItemId` of the Play directive message  | Yes |
| `audioStream`  | [AudioStreamObject](#AudioStreamObject) | `audioItem.stream` of the Play directive message | Yes |

### Remarks
Sometimes, due to the way music services charge users, issuing specific streaming details must be delayed till right before playback. This event API is designed for cases where you must not prepare audio stream details in advance. You must implement your client not to send this event message earlier than right before playback.

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
* [`AudioPlayer.Play`](#Play)
* [`AudioPlayer.StreamDeliver`](#StreamDeliver)

## Shared objects
Shared objects are included in a message body (`payload`) of event or directive messages when they are sent with the AudioPlayer API.

| Object name  | Object description  |
|--------------------|---------------------------------------------------|
| [AudioStreamObject](#AudioStreamObject) | An object containing playback details of an audio stream, such as streaming address or credentials |

### AudioStreamObject {#AudioStreamObject}
Contains streaming details of an audio stream. It is used when CIC returns playback streaming details to your client or when your client sends streaming details of a currently playing music to CIC.

#### Object field
| Field name  | Type  | Field description  | Required |
|---------------|---------|-----------------------------|---------|
| `beginAtInMilliseconds` | number | A starting point of playback. Unit is millisecond. If this field is specified as a non-zero value, play the audio stream from the specified point. If this field is specified as 0, play the audio stream from the beginning.  | Yes |
| `progressReport`  | object  | An object that specifies the time to report on a playback state after playback has started  | No |
| `progressReport.progressReportDelayInMilliseconds` | number | Specify this value to report on a playback state when a specified time has passed after playback has started. This field can have a null value.  | No |
| `progressReport.progressReportIntervalInMilliseconds` | number | Specify this value to report on a playback state regularly at a specified interval of time during playback. This field can have a null value.  | No |
| `progressReport.progressReportPositionInMilliseconds` | number | Specify this value to report on a playback state at each specified point during playback. This field can have a null value. | No |
| `token`  | string  | An audio stream token.  | Yes |
| `url`  | string  | An audio stream URL  | Yes |
| `urlPlayable`  | boolean | A value for determining whether the audio stream URL in the `url` field is playable or not. <ul><li><strong>true</strong>: Can play directly from the URL.</li><li><strong>false</strong>: Cannot play directly from the URL. Send an <a href="#StreamRequested"><code>AudioPlayer.StreamRequested</code></a> event message to request for audio stream details.</li></ul>  | Yes |
| `[Custom Field]`  | any  | Service providers can add any context information necessary for playback.  | No |

#### Object Example
{% raw %}
```json
// An object containing an audio stream URL which you can play from directly
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

// Example of an audio stream URL which you cannot play from directly
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
* [`AudioPlayer.progressReportDelayInMilliseconds`](#progressReportDelayInMilliseconds)
* [`AudioPlayer.ProgressReportDelayPassed`](#ProgressReportDelayPassed)
* [`AudioPlayer.ProgressReportIntervalPassed`](#ProgressReportIntervalPassed)
* [`AudioPlayer.PlaybackState`](/CIC/References/Context_Objects.md#PlaybackState)
* [`AudioPlayer.StreamRequested`](#StreamRequested)
