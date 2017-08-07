# AudioPlayer

클라이언트에서 오디오 스트림 재생을 요청하거나 오디오 스트림을 재생하는 중에 발생하는 이벤트를 CIC로 보고할 때 사용되는 API입니다. AudioPlayer API가 제공하는 이벤트 메시지와 지시 메시지는 다음과 같습니다.

| 메시지 이름         | 메시지 타입  | 메시지 설명                                   |
|------------------|-----------|---------------------------------------------|
| [`Play`](#Play)                       | Directive | 클라이언트에게 특정 오디오 스트림을 재생하거나 재생 대기열에 추가하도록 지시합니다.                         |
| [`PlayFinished`](#PlayFinished)       | Event     | 클라이언트가 오디오 스트림 재생을 완료할 때 재생 완료된 오디오 스트림 정보를 CIC로 보고하기 위해 사용됩니다.     |
| [`PlayPaused`](#PlayPaused)           | Event     | 클라이언트가 오디오 스트림 재생을 일시 정지할 때 일시 정지된 오디오 스트림 정보를 CIC로 보고하기 위해 사용됩니다. |
| [`PlayResumed`](#PlayResumed)         | Event     | 클라이언트가 오디오 스트림 재생을 재개할 때 재개된 오디오 스트림 정보를 CIC로 보고하기 위해 사용됩니다.         |
| [`PlayStarted`](#PlayStarted)         | Event     | 클라이언트가 오디오 스트림 재생을 시작할 때 재생이 시작된 오디오 스트림 정보를 CIC로 보고하기 위해 사용됩니다.    |
| [`PlayStopped`](#PlayStopped)         | Event     | 클라이언트가 오디오 스트림 재생을 중지할 때 재생이 중지된 오디오 스트림 정보를 CIC로 보고하기 위해 사용됩니다.    |
| [`ProgressReportDelayPassed`](#ProgressReportPositionPassed) | Event | 오디오 스트림 재생이 시작된 후 지정된 지연 시간만큼 시간이 지났을 때 현재 재생 상태([`AudioPlayer.PlaybackState`](/CIC/References/Context_Objects.md#PlaybackState))를 CIC로 보고하기 위해 사용됩니다. 각 오디오 스트림의 지연 시간은 [`AudioPlayer.Play`](#Play) 지시 메시지가 클라이언트로 전달될 때 확인할 수 있습니다. |
| [`ProgressReportIntervalPassed`](#ProgressReportPositionPassed)| Event | 오디오 스트림 재생이 시작된 후 지정된 간격마다 현재 재생 상태([`AudioPlayer.PlaybackState`](/CIC/References/Context_Objects.md#PlaybackState))를 CIC로 보고하기 위해 사용됩니다. 각 오디오 스트림의 보고 간격은 [`AudioPlayer.Play`](#Play) 지시 메시지가 클라이언트로 전달될 때 확인할 수 있습니다.|
| [`ProgressReportPositionPassed`](#ProgressReportPositionPassed) | Event | 오디오 스트림 재생이 시작된 후 지정된 보고 시점에 현재 재생 상태([`AudioPlayer.PlaybackState`](/CIC/References/Context_Objects.md#PlaybackState))를 CIC로 보고하기 위해 사용됩니다. 각 오디오 스트림의 보고 시점은 [`AudioPlayer.Play`](#Play) 지시 메시지가 클라이언트로 전달될 때 확인할 수 있습니다.|
| [`StreamDeliver`](#StreamDeliver)     | Directive | [`AudioPlayer.StreamRequested`](#StreamRequested) 이벤트 메시지의 응답이며, 실제 음악 재생이 가능한 오디오 스트림 정보를 수신해야 할 때 사용합니다. |
| [`StreamRequested`](#StreamRequested) | Event     | 오디오 스트림 재생을 위해 CIC로 스트리밍 URL과 같은 추가 정보를 요청하는 이벤트 메시지입니다.               |

## Play directive {#Play}
클라이언트에게 특정 오디오 스트림을 재생하거나 재생 대기열에 추가하도록 지시합니다.

### Payload field
| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|---------|
| `audioItem`               | object | 재생할 오디오 스트림의 메타 정보와 재생에 필요한 오디오 스트림 정보를 담고 있는 객체                     | 필수 |
| `audioItem.audioItemId`   | string | 오디오 스트림 정보를 구분하는 ID. 클라이언트는 이 값을 기준으로 중복된 Play 지시 메시지를 제거할 수 있습니다. | 필수 |
| `audioItem.stream`        | [AudioStreamObject](#AudioStreamObject) | 재생에 필요한 오디오 스트림 정보를 담고 있는 객체                        | 필수 |
| `audioItem.type`          | string | 음악 서비스 구분자. 음악 스트리밍 서비스를 제공하는 사업자나 서비스 이름입니다. 이 필드 값은 각 서비스마다 달라지는 audioItem 객체의 필드를 파악하고 이를 분석하는 파서(parser)를 선택하는데 이용될 수 있습니다. | 필수 |
| `audioItem.[CustomField]` | any    | 재생할 오디오 스트림에 첨부할 메타 정보를 서비스 제공자 임의대로 추가할 수 있습니다.                     | 선택 |
| `playBehavior`            | string | 지시 메시지에 포함된 오디오 스트림을 클라이언트에서 언제 재생할지를 결정하는 구분자 <ul><li><strong>"REPLACE_ALL"</strong> : 재생 대기열을 모두 비우고, 전달받은 오디오 스트림을 즉시 재생합니다.</li><li><strong>"ENQUEUE"</strong> : 재생 대기열에 전달받은 오디오 스트림을 추가합니다.</li></ul> | 필수 |

### Remarks
음악 서비스의 과금 문제 등으로 인해 실제 스트리밍 정보, 즉 스트리밍 URL과 같은 정보는 재생 직전에 획득할 수 있는 경우가 있습니다. 이는 `audioItem.stream.urlPlayable` 필드 값에 따라 다음과 같이 구분됩니다.
* `urlPlayable` 필드 값이 **true**이면 `audioItem.stream.url` 필드에 포함된 URL로 오디오 스트림을 바로 재생할 수 있습니다.
* `urlPlayable` 필드 값이 **false**이면 `audioItem.stream.url` 필드에 포함된 URL로 오디오 스트림을 바로 재생할 수 없고 [`AudioPlayer.StreamRequested`](#StreamRequested) 이벤트 메시지를 사용하여 오디오 스트림 정보를 추가로 요청해야 합니다.

### Message example
{% raw %}
```json
// 바로 재생 가능한 오디오 스트림 URL 정보가 담긴 예제
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

// 바로 재생 가능하지 않은 오디오 스트림 URL 정보가 담긴 예제
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
클라이언트가 오디오 스트림 재생을 완료할 때 재생 완료된 오디오 스트림 정보를 CIC로 보고하기 위해 사용됩니다.

### Context field
다음과 같은 [맥락 정보(Context)](/CIC/References/Context_Objects.md)를 함께 전송해야 합니다.

* [`AudioPlayer.PlaybackState`](/CIC/References/Context_Objects.md#PlaybackState)

### Payload field
없음

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
클라이언트가 오디오 스트림 재생을 일시 정지할 때 일시 정지된 오디오 스트림 정보를 CIC로 보고하기 위해 사용됩니다. 이 이벤트 메시지를 보내기 위해 필요한 사전 시나리오는 다음과 같습니다.

1. 클라이언트는 [`SpeechRecognizer.Recognize`](/CIC/References/APIs/SpeechRecognizer.md#Recognize) 이벤트 메시지로 오디오 스트림 재생을 일시 정지하도록 요청하는 사용자의 음성을 CIC로 전송합니다.
2. CIC는 Clova 플랫폼에서 인식된 일시 정지 요청을 [`PlaybackController.Pause`](/CIC/References/APIs/PlaybackController.md#Pause) 지시 메시지를 통해 클라이언트에 전달합니다.
3. 클라이언트는 오디오 스트림 재생을 일시 정지하고 PlayPaused 이벤트 메시지를 CIC에 전송합니다.

### Context field
다음과 같은 [맥락 정보(Context)](/CIC/References/Context_Objects.md)를 함께 전송해야 합니다.

* [`AudioPlayer.PlaybackState`](/CIC/References/Context_Objects.md#PlaybackState)

### Payload field
없음

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
클라이언트가 오디오 스트림 재생을 재개할 때 재개된 오디오 스트림 정보를 CIC로 보고하기 위해 사용됩니다. 이 이벤트 메시지를 보내기 위해 필요한 사전 시나리오는 다음과 같습니다.

1. 클라이언트는 [`SpeechRecognizer.Recognize`](/CIC/References/APIs/SpeechRecognizer.md#Recognize) 이벤트 메시지로 오디오 스트림 재생을 재개하도록 요청하는 사용자의 음성을 CIC로 전송합니다.
2. CIC는 Clova 플랫폼에서 인식된 재생 재개 요청을 [`PlaybackController.Resume`](/CIC/References/APIs/PlaybackController.md#Resume) 지시 메시지를 통해 클라이언트에 전달합니다.
3. 클라이언트는 오디오 스트림 재생을 재개하고 PlayResumed 이벤트 메시지를 CIC에 전송합니다.

### Context field
다음과 같은 [맥락 정보(Context)](/CIC/References/Context_Objects.md)를 함께 전송해야 합니다.

* [`AudioPlayer.PlaybackState`](/CIC/References/Context_Objects.md#PlaybackState)

### Payload field
없음

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
클라이언트가 오디오 스트림 재생을 시작할 때 재생이 시작된 오디오 스트림 정보를 CIC로 보고하기 위해 사용됩니다.

### Context field
다음과 같은 [맥락 정보(Context)](/CIC/References/Context_Objects.md)를 함께 전송해야 합니다.

* [`AudioPlayer.PlaybackState`](/CIC/References/Context_Objects.md#PlaybackState)

### Payload field
없음

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
클라이언트가 오디오 스트림 재생을 중지할 때 재생이 중지된 오디오 스트림 정보를 CIC로 보고하기 위해 사용됩니다. 이 이벤트 메시지를 보내기 위해 필요한 사전 시나리오는 다음과 같습니다.

1. 클라이언트는 [`SpeechRecognizer.Recognize`](/CIC/References/APIs/SpeechRecognizer.md#Recognize) 이벤트 메시지로 오디오 스트림 재생을 중지하도록 요청하는 사용자의 음성을 CIC로 전송합니다.
2. CIC는 Clova 플랫폼에서 인식된 중지 요청을 [`PlaybackController.Stop`](/CIC/References/APIs/PlaybackController.md#Stop) 지시 메시지를 통해 클라이언트에 전달합니다.
3. 클라이언트는 오디오 스트림 재생을 중지하고 PlayStopped 이벤트 메시지를 CIC에 전송합니다.

### Context field
다음과 같은 [맥락 정보(Context)](/CIC/References/Context_Objects.md)를 함께 전송해야 합니다.

* [`AudioPlayer.PlaybackState`](/CIC/References/Context_Objects.md#PlaybackState)

### Payload field
없음

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
오디오 스트림 재생이 시작된 후 지정된 지연 시간만큼 시간이 지났을 때 현재 재생 상태([`AudioPlayer.PlaybackState`](/CIC/References/Context_Objects.md#PlaybackState))를 CIC로 보고하기 위해 사용됩니다. 각 오디오 스트림의 지연 시간은 [`AudioPlayer.Play`](#Play) 지시 메시지가 클라이언트로 전달될 때 확인할 수 있습니다.

### Context field
다음과 같은 [맥락 정보(Context)](/CIC/References/Context_Objects.md)를 함께 전송해야 합니다.

* [`AudioPlayer.PlaybackState`](/CIC/References/Context_Objects.md#PlaybackState)

### Payload field
없음

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
오디오 스트림 재생이 시작된 후 지정된 간격마다 현재 재생 상태([`AudioPlayer.PlaybackState`](/CIC/References/Context_Objects.md#PlaybackState))를 CIC로 보고하기 위해 사용됩니다. 각 오디오 스트림의 보고 간격은 [`AudioPlayer.Play`](#Play) 지시 메시지가 클라이언트로 전달될 때 확인할 수 있습니다.

### Context field
다음과 같은 [맥락 정보(Context)](/CIC/References/Context_Objects.md)를 함께 전송해야 합니다.

* [`AudioPlayer.PlaybackState`](/CIC/References/Context_Objects.md#PlaybackState)

### Payload field
없음

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
오디오 스트림 재생이 시작된 후 지정된 보고 시점에 현재 재생 상태([`AudioPlayer.PlaybackState`](/CIC/References/Context_Objects.md#PlaybackState))를 CIC로 보고하기 위해 사용됩니다. 각 오디오 스트림의 보고 시점은 [`AudioPlayer.Play`](#Play) 지시 메시지가 클라이언트로 전달될 때 확인할 수 있습니다.

### Context field
다음과 같은 [맥락 정보(Context)](/CIC/References/Context_Objects.md)를 함께 전송해야 합니다.

* [`AudioPlayer.PlaybackState`](/CIC/References/Context_Objects.md#PlaybackState)

### Payload field
없음

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
[`AudioPlayer.StreamRequested`](#StreamRequested) 이벤트 메시지의 응답이며, 실제 음악 재생이 가능한 오디오 스트림 정보를 수신해야 할 때 사용합니다. 클라이언트가 음악을 재생할 수 있도록 오디오 스트림 정보에 스트리밍할 수 있는 URL 정보가 필수로 포함되어 있습니다.

### Payload field
| 필드 이름 | 자료형 | 필드 설명 | 필수 여부 |
|---------|------|--------|---------|
| `audioItemId` | string | 오디오 스트림 정보를 구분하는 값. 클라이언트는 이 값을 기준으로 중복된 Play 지시 메시지를 제거할 수 있습니다. | 필수 |
| `audioStream` | [AudioStreamObject](#AudioStreamObject) | 재생에 필요한 오디오 스트림 정보를 담고 있는 객체               | 필수 |

### Remarks
StreamDeliver 지시 메시지와 이미 수신한 [Play](#Play) 지시 메시지의 본문인 `payload.audioStream`을 조합하는 형태로 오디오 스트림 재생을 구현할 수 있습니다. 하지만, 기존 Play 지시 메시지를 통해 전달받은 값을 `StreamDeliver` 지시 메시지가 새로 전달한 값으로 치환하면 안 됩니다. 그 이유는 `StreamDeliver` 지시 메시지의 `AudioStreamObject의` 내용이 이미 [`AudioPlayer.Play`](#Play) 지시 메시지로 전달된 내용과 중복된 부분이 있으면 해당 내용이 생략될 수 있기 때문입니다. 이는 반복 재생이나 이전 곡 재생 등 동일한 Play 지시 메시지를 두 번 이상 처리할 때 기대와 다른 동작을 유발할 수 있습니다.

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
오디오 스트림 재생을 위해 CIC로 스트리밍 URL과 같은 추가 정보를 요청하는 이벤트 메시지입니다.

### Context field
없음

### Events field
| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|---------|
| `audioItemId`   | string  | Play 지시 메시지의 `audioItemId`                                      | 필수 |
| `audioStream`   | [AudioStreamObject](#AudioStreamObject) | Play 지시 메시지의 `audioItem.stream` | 필수 |

### Remarks
음악 서비스의 과금 등을 고려하여 실제 오디오 스트림 정보 발급을 재생 직전으로 지연 해야 할 때가 있습니다. 이 이벤트 메시지는 이처럼 오디오 스트림 정보를 미리 준비하면 안되는 경우를 위해 설계된 API이며, 따라서 클라이언트는 이 이벤트 메시지를 재생 직전 시점보다 일찍 전달하면 안됩니다.

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
AudioPlayer API를 이용하여 이벤트 메시지나 지시 메시지를 보낼 때 메시지 본문(`payload`)에 다음과 같은 객체(shared objects)를 공유하여 사용합니다.

| 객체 이름            | 객체 설명                                            |
|--------------------|---------------------------------------------------|
| [AudioStreamObject](#AudioStreamObject) | 재생할 음악의 재생 정보(스트리밍 주소, 인증 정보 등)가 담긴 객체 |

### AudioStreamObject {#AudioStreamObject}
재생할 음악의 오디오 스트림의 스트리밍 정보를 담고 있는 객체입니다. 클라이언트에게 재생할 스트리밍 정보를 전달하거나 클라이언트가 CIC로 현재 재생 중인 음악의 스트리밍 정보를 전달해야 할 때 사용합니다.

#### Object field
| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|---------|
| `beginAtInMilliseconds` | number | 재생을 시작할 지점. 단위는 밀리초이며, 이 값이 지정된 경우 클라이언트는 해당 오디오 스트림을 지정된 위치부터 재생해야 합니다. 이 값이 0이면 해당 스트림을 처음부터 재생해야 합니다.          | 필수 |
| `progressReport`    | object  | 재생 후 재생 상태 정보를 보고 받기 위해 보고 시간을 정해둔 객체                                                  | 선택 |
| `progressReport.progressReportDelayInMilliseconds` | number | 재생 시작 후 지정된 시간이 지났을 때 재생 상태 정보를 보고받기 위해 지정하는 값입니다. 이 필드는 null 값을 가질 수 있습니다.  | 선택 |
| `progressReport.progressReportIntervalInMilliseconds` | number | 재생 중 지정된 시간 간격으로 재생 상태 정보를 보고받기 위해 지정하는 값입니다. 이 필드는 null 값을 가질 수 있습니다.     | 선택 |
| `progressReport.progressReportPositionInMilliseconds` | number | 재생 중 지정된 시점을 지날 때마다 재생 상태 정보를 보고받기 위해 지정하는 값입니다. 이 필드는 null 값을 가질 수 있습니다. | 선택 |
| `token`             | string  | 오디오 스트림 toekn.                                                                                  | 필수 |
| `url`               | string  | 오디오 스트림 URL                                                                                     | 필수 |
| `urlPlayable`       | boolean | `url` 필드의 오디오 스트림 URL이 바로 재생 가능한 형태인지 구분하는 값. <ul><li><strong>true</strong> : 바로 재생이 가능한 형태의 URL</li><li><strong>false</strong> : 바로 재생이 불가능한 형태의 URL. <a href="#StreamRequested"><code>AudioPlayer.StreamRequested</code></a> 이벤트 메시지를 사용하여 오디오 스트림 정보를 추가로 요청해야 합니다.</li></ul>        | 필수 |
| `[Custom Field]`    | any     | 오디오 스트림 재생 문맥에 추가로 필요한 값을 서비스 제공자 임의대로 추가할 수 있습니다.                                | 선택 |

#### Object Example
{% raw %}
```json
// 바로 재생 가능한 오디오 스트림 URL 정보가 담긴 객체
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

// 바로 재생 가능하지 않은 오디오 스트림 URL 정보가 담긴 예제
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
