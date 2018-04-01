# AudioPlayer

AudioPlayer 인터페이스는 클라이언트에서 오디오 스트림 재생을 요청하거나 오디오 스트림을 재생하는 중에 발생하는 이벤트를 CIC로 보고할 때 사용되는 네임스페이스입니다. AudioPlayer가 제공하는 이벤트 메시지와 지시 메시지는 다음과 같습니다.

| 메시지 이름         | 메시지 타입  | 메시지 설명                                   |
|------------------|-----------|---------------------------------------------|
| [`ClearQueue`](#ClearQueue)           | Directive | 클라이언트에게 오디오 스트림 재생 대기열(queue)을 초기화하도록 지시합니다.                              |
| [`ExpectReportPlaybackState`](#ExpectReportPlaybackState) | Directive | 클라이언트에게 현재 재생 상태를 보고하도록 지시합니다. 클라이언트는 이 지시 메시지를 받으면 [`AudioPlayer.ReportPlaybackState`](#ReportPlaybackState) 이벤트 메시지를 CIC로 전송해야 합니다. |
| [`Play`](#Play)                       | Directive | 클라이언트에게 특정 오디오 스트림을 재생하거나 재생 대기열에 추가하도록 지시합니다.                         |
| [`PlayFinished`](#PlayFinished)       | Event     | 클라이언트가 오디오 스트림 재생을 완료할 때 재생 완료된 오디오 스트림 정보를 CIC로 보고하기 위해 사용됩니다.     |
| [`PlayPaused`](#PlayPaused)           | Event     | 클라이언트가 오디오 스트림 재생을 일시 정지할 때 일시 정지된 오디오 스트림 정보를 CIC로 보고하기 위해 사용됩니다. |
| [`PlayResumed`](#PlayResumed)         | Event     | 클라이언트가 오디오 스트림 재생을 재개할 때 재개된 오디오 스트림 정보를 CIC로 보고하기 위해 사용됩니다.         |
| [`PlayStarted`](#PlayStarted)         | Event     | 클라이언트가 오디오 스트림 재생을 시작할 때 재생이 시작된 오디오 스트림 정보를 CIC로 보고하기 위해 사용됩니다.    |
| [`PlayStopped`](#PlayStopped)         | Event     | 클라이언트가 오디오 스트림 재생을 중지할 때 재생이 중지된 오디오 스트림 정보를 CIC로 보고하기 위해 사용됩니다.    |
| [`ProgressReportDelayPassed`](#ProgressReportPositionPassed) | Event | 오디오 스트림 재생이 시작된 후 지정된 지연 시간만큼 시간이 지났을 때 현재 재생 상태([`AudioPlayer.PlaybackState`](/CIC/References/Context_Objects.md#PlaybackState))를 CIC로 보고하기 위해 사용됩니다. 각 오디오 스트림의 지연 시간은 [`AudioPlayer.Play`](#Play) 지시 메시지가 클라이언트로 전달될 때 확인할 수 있습니다. |
| [`ProgressReportIntervalPassed`](#ProgressReportPositionPassed)| Event | 오디오 스트림 재생이 시작된 후 지정된 간격마다 현재 재생 상태([`AudioPlayer.PlaybackState`](/CIC/References/Context_Objects.md#PlaybackState))를 CIC로 보고하기 위해 사용됩니다. 각 오디오 스트림의 보고 간격은 [`AudioPlayer.Play`](#Play) 지시 메시지가 클라이언트로 전달될 때 확인할 수 있습니다.|
| [`ProgressReportPositionPassed`](#ProgressReportPositionPassed) | Event | 오디오 스트림 재생이 시작된 후 지정된 보고 시점에 현재 재생 상태([`AudioPlayer.PlaybackState`](/CIC/References/Context_Objects.md#PlaybackState))를 CIC로 보고하기 위해 사용됩니다. 각 오디오 스트림의 보고 시점은 [`AudioPlayer.Play`](#Play) 지시 메시지가 클라이언트로 전달될 때 확인할 수 있습니다.|
| [`ReportPlaybackState`](#ReportPlaybackState)           | Event  | 클라이언트의 현재 음원 재생 상태를 CIC로 보고합니다. 클라이언트가 CIC로부터 [`ExpectReportPlaybackState`](#ExpectReportPlaybackState) 지시 메시지를 받은 경우 `AudioPlayer.ReportPlaybackState` 이벤트 메시지를 CIC로 전송해야 합니다.  |
| [`RequestPlaybackState`](#RequestPlaybackState)         | Event  | 클라이언트의 음원 재생 상태를 CIC에게 요청합니다. CIC는 `AudioPlayer.ReqeustPlaybackState` 이벤트 메시지를 전달받으면 사용자 계정에 등록된 모든 또는 특정 클라이언트에게 [`ExpectReportPlaybackState`](#ExpectReportPlaybackState) 지시 메시지를 전송합니다.  |
| [`StreamDeliver`](#StreamDeliver)     | Directive | [`AudioPlayer.StreamRequested`](#StreamRequested) 이벤트 메시지의 응답이며, 실제 음악 재생이 가능한 오디오 스트림 정보를 수신해야 할 때 사용합니다. |
| [`StreamRequested`](#StreamRequested) | Event     | 오디오 스트림 재생을 위해 CIC로 스트리밍 URL과 같은 추가 정보를 요청하는 이벤트 메시지입니다.               |
| [`SynchronizePlaybackState`](#SynchronizePlaybackState) | Directive | 클라이언트의 음원 재생 상태를 동기화하도록 지시합니다. `AudioPlayer.RequestPlaybackState` 이벤트 메시지를 전송했던 클라이언트는 `AudioPlayer.SynchronizePlaybackState` 지시 메시지를 수신하게 됩니다. |

## 음원 재생 상태 공유 {#SharePlaybackState}

한 클라이언트는 사용자 계정에 등록된 다른 모든 클라이언트 또는 특정 클라이언트로부터 음원 재생 상태를 공유받을 수 있습니다. 음원 재생 상태를 공유 받는 동작의 흐름은 다음과 같습니다.

![](/CIC/Resources/Images/CIC_Playback_State_Sync_Work_Flow.png)

1. 클라이언트는 [`AudioPlayer.RequestPlaybackState`](#RequestPlaybackState) 이벤트 메시지를 사용하여 CIC에게 사용자 계정에 등록된 모든 클라이언트 또는 특정 클라이언트의 음원 재생 상태 정보를 요청합니다.
2. CIC는 [`AudioPlayer.ExpectReportPlaybackState`](#ExpectReportPlaybackState)사용자 계정에 등록된 모든 클라이언트 또는 특정 클라이언트에게 현재 음원 재생 상태를 보고하도록 지시합니다.
3. 음원 재생 상태 보고 요청을 받은 클라이언트는 [`AudioPlayer.ReportPlaybackState`](#ReportPlaybackState) 이벤트 메시지를 사용하여 CIC에게 현재 음원 재생 상태를 보고합니다.
4. CIC는 [`AudioPlayer.SynchronizePlaybackState`](#SynchronizePlaybackState)를 사용하여 다른 클라이언트의 음원 재생 상태를 요청했던 클라이언트에게 상태 정보를 전달하여 정보를 동기화하도록 지시합니다.


## ClearQueue directive {#ClearQueue}
클라이언트에게 오디오 스트림 재생 대기열(queue)을 초기화하도록 지시합니다. 이 지시 메시지의 `clearBehavior` 필드 값은 초기화 동작을 구분하며, 클라이언트가 재생 대기열을 초기화하면서 현재 재생 중인 오디오 스트림의 재생을 멈춰야 하는지를 결정합니다.

### Payload fields

| 필드 이름       | 자료형    | 필드 설명                     | 포함 여부 |
|---------------|---------|-----------------------------|:---------:|
| `clearBehavior`           | string | 초기화 동작을 결정하는 구분자<ul><li><code>"CLEAR_ALL"</code>: 재생 대기열을 모두 비우고, 현재 재생 중인 오디오 스트림의 재생을 즉시 멈춥니다.</li><li><code>"CLEAR_ENQUEUED"</code>: 재생 대기열만 비우고, 현재 재생 중인 오디오 스트림은 계속 재생합니다.</li></ul> | 항상 |

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

클라이언트에게 현재 재생 상태를 보고하도록 지시합니다. 클라이언트는 이 지시 메시지를 받으면 [`AudioPlayer.ReportPlaybackState`](#ReportPlaybackState) 이벤트 메시지를 CIC로 전송해야 합니다.

### Payload fields

없음

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
* [음원 재생 상태 공유](#SharePlaybackState)

## Play directive {#Play}
클라이언트에게 특정 오디오 스트림을 재생하거나 재생 대기열에 추가하도록 지시합니다.

### Payload fields
| 필드 이름       | 자료형    | 필드 설명                     | 포함 여부 |
|---------------|---------|-----------------------------|:---------:|
| `audioItem`               | object | 재생할 오디오 스트림의 메타 정보와 재생에 필요한 오디오 스트림 정보를 담고 있는 객체                     | 항상 |
| `audioItem.artImageUrl`   | string | 오디오 콘텐츠 관련 이미지(앨범 이미지)의 URL                                                  | 조건부  |
| `audioItem.audioItemId`   | string | 오디오 스트림 정보를 구분하는 ID. 클라이언트는 이 값을 기준으로 중복된 Play 지시 메시지를 제거할 수 있습니다. | 항상 |
| `audioItem.headerText`    | string | 주로 현재 재생 목록의 제목을 표현하는 텍스트 필드                                                | 조건부  |
| `audioItem.stream`        | [AudioStreamInfoObject](#AudioStreamInfoObject) | 재생에 필요한 오디오 스트림 정보를 담고 있는 객체        | 항상 |
| `audioItem.titleSubText1` | string | 주로 가수 이름을 표현하는 텍스트 필드                                                          | 항상 |
| `audioItem.titleSubText2` | string | 주로 앨범 이름을 표현하는 보조 텍스트 필드                                                      | 조건부 |
| `audioItem.titleText`     | string | 현재 음악의 제목을 표현하는 텍스트 필드                                                         | 항상  |
| `audioItem.type`          | string | **(Deprecated)** 음악 서비스 구분자. 음악 스트리밍 서비스를 제공하는 사업자나 서비스 이름입니다. 이 필드 값은 각 서비스마다 달라지는 audioItem 객체의 필드를 파악하고 이를 분석하는 파서(parser)를 선택하는데 이용될 수 있습니다. | 항상 |
| `playBehavior`            | string | 지시 메시지에 포함된 오디오 스트림을 클라이언트에서 언제 재생할지를 결정하는 구분자 <ul><li><code>"REPLACE_ALL"</code>: 재생 대기열을 모두 비우고, 전달받은 오디오 스트림을 즉시 재생합니다.</li><li><code>"ENQUEUE"</code>: 재생 대기열에 전달받은 오디오 스트림을 추가합니다.</li></ul> | 항상 |
| `source`                  | object | 오디오 스트리밍 서비스의 출처 정보                                                    | 항상 |
| `source.logoUrl`          | string | 오디오 스트리밍 서비스의 로고 이미지 URL. 이 필드 또는 필드의 값이 없거나 로고 이미지를 표시할 수 없을 경우 `source.name` 필드에 있는 오디오 스트리밍 서비스의 이름이라도 표시해야 합니다.  | 조건부 |
| `source.name`             | string | 오디오 스트리밍 서비스의 이름                                                        | 항상 |

### Remarks
음악 서비스의 과금 문제 등으로 인해 실제 스트리밍 정보, 즉 스트리밍 URL과 같은 정보는 재생 직전에 획득할 수 있는 경우가 있습니다. 이는 `audioItem.stream.urlPlayable` 필드 값에 따라 다음과 같이 구분됩니다.
* `urlPlayable` 필드 값이 `true`이면 `audioItem.stream.url` 필드에 포함된 URL로 오디오 스트림을 바로 재생할 수 있습니다.
* `urlPlayable` 필드 값이 `false`이면 `audioItem.stream.url` 필드에 포함된 URL로 오디오 스트림을 바로 재생할 수 없고 [`AudioPlayer.StreamRequested`](#StreamRequested) 이벤트 메시지를 사용하여 오디오 스트림 정보를 추가로 요청해야 합니다.

### Message example
{% raw %}

```json
// 바로 재생 가능한 오디오 스트림 URL 정보가 담긴 예제
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

// 바로 재생 가능하지 않은 오디오 스트림 URL 정보가 담긴 예제
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
클라이언트가 오디오 스트림 재생을 완료할 때 재생 완료된 오디오 스트림 정보를 CIC로 보고하기 위해 사용됩니다.

### Context fields

{% include "/CIC/References/CICInterface/Context_Objects_List.md" %}

### Payload fields

| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|:---------:|
| `token`                | string | ['AudioPlayer.Play'](#Play) 지시 메시지의 `audioItem.stream.token` 필드 값 | 필수 |
| `offsetInMilliseconds` | number | 현재 재생하고 있는 음원의 재생 시점. 단위는 밀리 초입니다.                         | 필수  |

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
클라이언트가 오디오 스트림 재생을 일시 정지할 때 일시 정지된 오디오 스트림 정보를 CIC로 보고하기 위해 사용됩니다. 이 이벤트 메시지를 보내기 위해 필요한 사전 시나리오는 다음과 같습니다.

1. 클라이언트는 [`SpeechRecognizer.Recognize`](/CIC/References/CICInterface/SpeechRecognizer.md#Recognize) 이벤트 메시지로 오디오 스트림 재생을 일시 정지하도록 요청하는 사용자의 음성을 CIC로 전송합니다.
2. CIC는 Clova 플랫폼에서 인식된 일시 정지 요청을 [`PlaybackController.Pause`](/CIC/References/CICInterface/PlaybackController.md#Pause) 지시 메시지를 통해 클라이언트에 전달합니다.
3. 클라이언트는 오디오 스트림 재생을 일시 정지하고 PlayPaused 이벤트 메시지를 CIC에 전송합니다.

### Context fields

{% include "/CIC/References/CICInterface/Context_Objects_List.md" %}

### Payload fields

| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|:---------:|
| `token`                | string | ['AudioPlayer.Play'](#Play) 지시 메시지의 `audioItem.stream.token` 필드 값 | 필수 |
| `offsetInMilliseconds` | number | 현재 재생하고 있는 음원의 재생 시점. 단위는 밀리 초입니다.                         | 필수  |

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

클라이언트가 오디오 스트림 재생을 재개할 때 재개된 오디오 스트림 정보를 CIC로 보고하기 위해 사용됩니다. 이 이벤트 메시지를 보내기 위해 필요한 사전 시나리오는 다음과 같습니다.

1. 클라이언트는 [`SpeechRecognizer.Recognize`](/CIC/References/CICInterface/SpeechRecognizer.md#Recognize) 이벤트 메시지로 오디오 스트림 재생을 재개하도록 요청하는 사용자의 음성을 CIC로 전송합니다.
2. CIC는 Clova 플랫폼에서 인식된 재생 재개 요청을 [`PlaybackController.Resume`](/CIC/References/CICInterface/PlaybackController.md#Resume) 지시 메시지를 통해 클라이언트에 전달합니다.
3. 클라이언트는 오디오 스트림 재생을 재개하고 PlayResumed 이벤트 메시지를 CIC에 전송합니다.

### Context fields

{% include "/CIC/References/CICInterface/Context_Objects_List.md" %}

### Payload fields

| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|:---------:|
| `token`                | string | ['AudioPlayer.Play'](#Play) 지시 메시지의 `audioItem.stream.token` 필드 값 | 필수 |
| `offsetInMilliseconds` | number | 현재 재생하고 있는 음원의 재생 시점. 단위는 밀리 초입니다.                         | 필수  |

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
클라이언트가 오디오 스트림 재생을 시작할 때 재생이 시작된 오디오 스트림 정보를 CIC로 보고하기 위해 사용됩니다.

### Context fields

{% include "/CIC/References/CICInterface/Context_Objects_List.md" %}

### Payload fields

| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|:---------:|
| `token`                | string | ['AudioPlayer.Play'](#Play) 지시 메시지의 `audioItem.stream.token` 필드 값 | 필수 |
| `offsetInMilliseconds` | number | 현재 재생하고 있는 음원의 재생 시점. 단위는 밀리 초입니다.                         | 필수  |

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
클라이언트가 오디오 스트림 재생을 중지할 때 재생이 중지된 오디오 스트림 정보를 CIC로 보고하기 위해 사용됩니다. 이 이벤트 메시지를 보내기 위해 필요한 사전 시나리오는 다음과 같습니다.

1. 클라이언트는 [`SpeechRecognizer.Recognize`](/CIC/References/CICInterface/SpeechRecognizer.md#Recognize) 이벤트 메시지로 오디오 스트림 재생을 중지하도록 요청하는 사용자의 음성을 CIC로 전송합니다.
2. CIC는 Clova 플랫폼에서 인식된 중지 요청을 [`PlaybackController.Stop`](/CIC/References/CICInterface/PlaybackController.md#Stop) 지시 메시지를 통해 클라이언트에 전달합니다.
3. 클라이언트는 오디오 스트림 재생을 중지하고 PlayStopped 이벤트 메시지를 CIC에 전송합니다.

### Context fields

{% include "/CIC/References/CICInterface/Context_Objects_List.md" %}

### Payload fields

| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|:---------:|
| `token`                | string | ['AudioPlayer.Play'](#Play) 지시 메시지의 `audioItem.stream.token` 필드 값 | 필수 |
| `offsetInMilliseconds` | number | 현재 재생하고 있는 음원의 재생 시점. 단위는 밀리 초입니다.                         | 필수  |

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
오디오 스트림 재생이 시작된 후 지정된 지연 시간만큼 시간이 지났을 때 현재 재생 상태([`AudioPlayer.PlaybackState`](/CIC/References/Context_Objects.md#PlaybackState))를 CIC로 보고하기 위해 사용됩니다. 각 오디오 스트림의 지연 시간은 [`AudioPlayer.Play`](#Play) 지시 메시지가 클라이언트로 전달될 때 확인할 수 있습니다.

### Context fields

{% include "/CIC/References/CICInterface/Context_Objects_List.md" %}

### Payload fields

| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|:---------:|
| `token`                | string | ['AudioPlayer.Play'](#Play) 지시 메시지의 `audioItem.stream.token` 필드 값 | 필수 |
| `offsetInMilliseconds` | number | 현재 재생하고 있는 음원의 재생 시점. 단위는 밀리 초입니다.                         | 필수  |

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
오디오 스트림 재생이 시작된 후 지정된 간격마다 현재 재생 상태([`AudioPlayer.PlaybackState`](/CIC/References/Context_Objects.md#PlaybackState))를 CIC로 보고하기 위해 사용됩니다. 각 오디오 스트림의 보고 간격은 [`AudioPlayer.Play`](#Play) 지시 메시지가 클라이언트로 전달될 때 확인할 수 있습니다.

### Context fields

{% include "/CIC/References/CICInterface/Context_Objects_List.md" %}

### Payload fields

| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|:---------:|
| `token`                | string | ['AudioPlayer.Play'](#Play) 지시 메시지의 `audioItem.stream.token` 필드 값 | 필수 |
| `offsetInMilliseconds` | number | 현재 재생하고 있는 음원의 재생 시점. 단위는 밀리 초입니다.                         | 필수  |

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
오디오 스트림 재생이 시작된 후 지정된 보고 시점에 현재 재생 상태([`AudioPlayer.PlaybackState`](/CIC/References/Context_Objects.md#PlaybackState))를 CIC로 보고하기 위해 사용됩니다. 각 오디오 스트림의 보고 시점은 [`AudioPlayer.Play`](#Play) 지시 메시지가 클라이언트로 전달될 때 확인할 수 있습니다.

### Context fields

{% include "/CIC/References/CICInterface/Context_Objects_List.md" %}

### Payload fields

| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|:---------:|
| `token`                | string | ['AudioPlayer.Play'](#Play) 지시 메시지의 `audioItem.stream.token` 필드 값 | 필수 |
| `offsetInMilliseconds` | number | 현재 재생하고 있는 음원의 재생 시점. 단위는 밀리 초입니다.                         | 필수  |

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

클라이언트의 현재 음원 재생 상태를 CIC로 보고합니다. 클라이언트가 CIC로부터 [`AudioPlayer.ExpectReportPlaybackState`](#ExpectReportPlaybackState) 지시 메시지를 받은 경우 `AudioPlayer.ReportPlaybackState` 이벤트 메시지를 CIC로 전송해야 합니다.

### Context fields

{% include "/CIC/References/CICInterface/Context_Objects_List.md" %}

### Payload fields
| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|:---------:|
| `offsetInMilliseconds`   | number  | 현재 재생하고 있는 음원의 재생 시점. 단위는 밀리 초입니다.  | 선택  |
| `playerActivity`         | string  | 오디오 플레이어의 현재 상태.<ul><li><code>"IDLE"</code>: 미사용 상태</li><li><code>"PLAYING"</code>: 재생 중인 상태</li><li><code>"PAUSED"</code>: 일시 중지된 상태</li><li><code>"STOPPED"</code>: 정지된 상태</li></ul>  | 필수  |
| `repeatMode`             | string  | 반복 재생 모드.<ul><li><code>"NONE"</code>: 반복 재생 안함</li><li><code>"REPEAT_ONE"</code>: 한 곡 반복 재생</li></ul>  | 필수  |
| `stream`                 | [AudioStreamInfoObject](#AudioStreamInfoObject) | Play 지시 메시지의 `audioItem.stream`                                     | 선택 |
| `token`                  | string  | ['AudioPlayer.Play'](#Play) 지시 메시지의 `audioItem.stream.token` 필드 값                                          | 선택 |
| `totalInMilliseconds`    | number | 최근 재생 미디어의 전체 길이. [`AudioPlayer.Play`](/CIC/References/CICInterface/AudioPlayer.md#Play) 지시 메시지를 통해 전달받은 오디오 정보([AudioStreamInfoObject](/CIC/References/CICInterface/AudioPlayer.md#AudioStreamInfoObject))에 `durationInMilliseconds` 필드 값이 있는 경우 이 필드의 값으로 입력하면 됩니다. 단위는 밀리초이며, `playerActivity` 값이 `"IDLE"`이면 이 필드 값은 입력하지 않아도 됩니다. | 선택 |

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
* [음원 재생 상태 공유](#SharePlaybackState)

## RequestPlaybackState event {#RequestPlaybackState}

클라이언트의 음원 재생 상태를 CIC에게 요청합니다. CIC는 `AudioPlayer.ReqeustPlaybackState` 이벤트 메시지를 전달받으면 사용자 계정에 등록된 모든 또는 특정 클라이언트에게 [`AudioPlayer.ExpectReportPlaybackState`](#ExpectReportPlaybackState) 지시 메시지를 전송합니다.

### Context fields

{% include "/CIC/References/CICInterface/Context_Objects_List.md" %}

### Payload fields
| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|:---------:|
| `deviceId`    | string  | 대상 클라이언트의 ID. 임의의 형식으로 된 식별자(Opaque ID)입니다. 이 필드가 생략되면 사용자 계정에 등록된 모든 클라이언트에게 요청을 보냅니다. | 선택 |

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
* [음원 재생 상태 공유](#SharePlaybackState)

## StreamDeliver directive {#StreamDeliver}
[`AudioPlayer.StreamRequested`](#StreamRequested) 이벤트 메시지의 응답이며, 실제 음악 재생이 가능한 오디오 스트림 정보를 수신해야 할 때 사용합니다. 클라이언트가 음악을 재생할 수 있도록 오디오 스트림 정보에 스트리밍할 수 있는 URL 정보가 필수로 포함되어 있습니다.

### Payload fields
| 필드 이름 | 자료형 | 필드 설명 | 포함 여부 |
|---------|------|--------|:---------:|
| `audioItemId` | string | 오디오 스트림 정보를 구분하는 값. 클라이언트는 이 값을 기준으로 중복된 Play 지시 메시지를 제거할 수 있습니다. | 항상 |
| `audioStream` | [AudioStreamInfoObject](#AudioStreamInfoObject) | 재생에 필요한 오디오 스트림 정보를 담고 있는 객체       | 항상 |

### Remarks
`StreamDeliver` 지시 메시지를 통해 전달받는 `AudioStreamInfoObject` 객체는 기존 [`AudioPlayer.Play`](#Play) 지시 메시지를 통해 전달받은 `AudioStreamInfoObject` 객체의 내용과 중복을 피하기 위해 일부 내용이 생략될 수 있습니다. 따라서, 음원을 재생할 때 `StreamDeliver` 지시 메시지와 이미 수신한 [`Play`](#Play) 지시 메시지의 `payload.audioStream` 정보를 조합해서 사용해야 합니다.

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

### Context fields

{% include "/CIC/References/CICInterface/Context_Objects_List.md" %}

### Payload fields
| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|:---------:|
| `audioItemId`   | string  | ['AudioPlayer.Play'](#Play) 지시 메시지의 `audioItem.audioItemId` 필드 값       | 필수 |
| `audioStream`   | [AudioStreamInfoObject](#AudioStreamInfoObject) | Play 지시 메시지의 `audioItem.stream` | 필수 |

### Remarks
음악 서비스의 과금 등을 고려하여 실제 오디오 스트림 정보 발급을 재생 직전으로 지연 해야 할 때가 있습니다. 이 이벤트 메시지는 이처럼 오디오 스트림 정보를 미리 준비하면 안되는 경우를 위해 설계된 API이며, 따라서 클라이언트는 이 이벤트 메시지를 재생 직전 시점보다 일찍 전달하면 안됩니다.

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

## SynchronizePlaybackState directive {#SynchronizePlaybackState}

클라이언트의 음원 재생 상태를 동기화하도록 지시합니다. `AudioPlayer.RequestPlaybackState` 이벤트 메시지를 전송했던 클라이언트는 `AudioPlayer.SynchronizePlaybackState` 지시 메시지를 수신하게 됩니다.

### Payload fields

| 필드 이름       | 자료형    | 필드 설명                     | 포함 여부 |
|---------------|---------|-----------------------------|:---------:|
| `deviceId`    | string  | 대상 클라이언트의 ID. 임의의 형식으로 된 식별자(Opaque ID)입니다.  | 항상  |
| `event`       | string  | 클라이언트에서 발생한 이벤트.<ul><li><code>PlayFinished</code></li><li><code>PlayPaused</code></li><li><code>PlayResumed</code></li><li><code>PlayStarted</code></li><li><code>PlayStopped</code></li></ul>  | 조건부  |
| `playbackState`          | object  | 클라이언트의 재생 상태 정보를 담고 있는 객체             | 조건부  |
| `playbackState.offsetInMilliseconds`   | number  | 현재 재생하고 있는 음원의 재생 시점. 단위는 밀리 초이며, 이 필드는 null 값을 가질 수 있습니다.  | 조건부  |
| `playbackState.playerActivity`         | string  | 오디오 플레이어의 현재 상태.<ul><li><code>"IDLE"</code>: 미사용 상태</li><li><code>"PLAYING"</code>: 재생 중인 상태</li><li><code>"PAUSED"</code>: 일시 중지된 상태</li><li><code>"STOPPED"</code>: 정지된 상태</li></ul>  | 항상  |
| `playbackState.repeatMode`             | string  | 설정된 반복 재생 모드.<ul><li><code>"NONE"</code>: 반복 재생 안함</li><li><code>"REPEAT_ONE"</code>: 한 곡 반복 재생</li></ul>  | 항상  |
| `playbackState.stream`                 | [AudioStreamInfoObject](#AudioStreamInfoObject) | 오디오 스트림과 관련된 정보가 담긴 객체                                         | 항상 |
| `playbackState.token`                  | string  | 음원 재생을 식별하는 token. 이 필드는 빈 문자열(`""`)을 가질 수도 있습니다.                                                    | 항상 |
| `playbackState.totalInMilliseconds`    | number | 최근 재생 미디어의 전체 길이. 단위는 밀리초이며, 이 필드는 null 값을 가질 수 있습니다.                  | 항상 |

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
* [음원 재생 상태 공유](#SharePlaybackState)

## Shared objects
AudioPlayer API를 이용하여 이벤트 메시지나 지시 메시지를 보낼 때 메시지 본문(`payload`)에 다음과 같은 객체(shared objects)를 공유하여 사용합니다.

| 객체 이름            | 객체 설명                                            |
|--------------------|---------------------------------------------------|
| [AudioStreamInfoObject](#AudioStreamInfoObject) | 재생할 음악의 재생 정보(스트리밍 주소, 인증 정보 등)가 담긴 객체 |

### AudioStreamInfoObject {#AudioStreamInfoObject}
재생할 음악의 오디오 스트림의 스트리밍 정보를 담고 있는 객체입니다. 클라이언트에게 재생할 스트리밍 정보를 전달하거나 클라이언트가 CIC로 현재 재생 중인 음악의 스트리밍 정보를 전달해야 할 때 사용합니다.

#### Object fields
| 필드 이름       | 자료형    | 필드 설명                     | 필수/포함 여부 |
|---------------|---------|-----------------------------|:-------------:|
| `beginAtInMilliseconds`  | number | 재생을 시작할 지점. 단위는 밀리초이며, 이 값이 지정된 경우 클라이언트는 해당 오디오 스트림을 지정된 위치부터 재생해야 합니다. 이 값이 0이면 해당 스트림을 처음부터 재생해야 합니다.          | 필수/항상 |
| `customData`             | string | 현재 음원과 관련하여 임의의 형식을 가지는 메타 데이터 정보. 특정 범주로 분류되거나 정의될 수 없는 스트리밍 정보는 이 필드에 포함되거나 입력되어야 합니다. 오디오 스트림 재생 문맥에 추가로 필요한 값을 서비스 제공자 임의대로 추가할 수 있습니다.<div class="danger"><p><strong>Caution!</strong></p><p>이 필드의 값을 클라이언트가 임의로 이용해서는 안되며 이는 문제를 발생시킬 수 있습니다. 또한, 이 필드 값은 오디오 재생 상태를 전달할 때 <a href="/CIC/References/Context_Objects.html#PlaybackState">PlaybackState 문맥 정보</a>의 `stream` 필드에 그대로 첨부되어야 합니다.</p></div> | 선택/조건부  |
| `durationInMilliseconds` | number | 오디오 스트림의 재생 시간. 클라이언트는 `beginAtInMilliseconds` 필드에 지정된 재생 시작 시점부터 이 필드에 지정된 재생 시간만큼 해당 오디오 스트림을 탐색 및 재생할 수 있습니다. 예를 들면, `beginAtInMilliseconds` 필드의 값이 `10000`이고, 이 필드의 값이 `60000`이면 해당 오디오 스트림의 10초부터 70초까지의 구간을 재생 및 탐색할 수 있게 됩니다. 단위는 밀리 초입니다.   | 선택/조건부  |
| `progressReport`         | object  | 재생 후 재생 상태 정보를 보고 받기 위해 보고 시간을 정해둔 객체                                                  | 선택/조건부 |
| `progressReport.progressReportDelayInMilliseconds`    | number | 재생 시작 후 지정된 시간이 지났을 때 재생 상태 정보를 보고받기 위해 지정되는 값입니다. 단위는 밀리 초이며, 이 필드는 null 값을 가질 수 있습니다.  | 선택/조건부 |
| `progressReport.progressReportIntervalInMilliseconds` | number | 재생 중 지정된 시간 간격으로 재생 상태 정보를 보고받기 위해 지정되는 값입니다. 단위는 밀리 초이며, 이 필드는 null 값을 가질 수 있습니다.        | 선택/조건부 |
| `progressReport.progressReportPositionInMilliseconds` | number | 재생 중 지정된 시점을 지날 때마다 재생 상태 정보를 보고받기 위해 지정되는 값입니다. 단위는 밀리 초이며, 이 필드는 null 값을 가질 수 있습니다.    | 선택/조건부 |
| `token`                  | string  | 오디오 스트림 token                                                                                   | 필수/항상 |
| `url`                    | string  | 오디오 스트림 URL                                                                                     | 필수/항상 |
| `urlPlayable`            | boolean | `url` 필드의 오디오 스트림 URL이 바로 재생 가능한 형태인지 구분하는 값. <ul><li><code>true</code>: 바로 재생이 가능한 형태의 URL</li><li><code>false</code>: 바로 재생이 불가능한 형태의 URL. <a href="#StreamRequested"><code>AudioPlayer.StreamRequested</code></a> 이벤트 메시지를 사용하여 오디오 스트림 정보를 추가로 요청해야 합니다.</li></ul>        | 필수/항상 |

#### Remarks
* 클라이언트가 `beginAtInMilliseconds`와 `durationInMilliseconds` 필드에 지정된 구간에 대해 음악 재생을 완료하면 [`AudioPlayer.PlayFinished`](#PlayFinished) 이벤트 메시지를 CIC로 전송해야 합니다.
* 클라이언트는 `beginAtInMilliseconds`와 `durationInMilliseconds` 필드에 지정된 구간 이외의 시간을 사용자가 탐색(seek)할 수 없도록 UI를 제공해야 합니다.
* 클라이언트가 현재 재생 중인 상태를 CIC에 보고할 때 [`AudioPlayer.PlaybackState`](/CIC/References/Context_Objects.md#PlaybackState)의 `totalInMilliseconds` 필드 값은 `beginAtInMilliseconds` 필드와 `durationInMilliseconds` 필드에 지정된 값을 더한 값으로 입력하면 됩니다.

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
* [`AudioPlayer.PlayFinished`](#PlayFinished)
* [`AudioPlayer.ProgressReportDelayPassed`](#ProgressReportDelayPassed)
* [`AudioPlayer.ProgressReportIntervalPassed`](#ProgressReportIntervalPassed)
* [`AudioPlayer.ProgressReportPositionPassed`](#ProgressReportPositionPassed)
* [`AudioPlayer.StreamRequested`](#StreamRequested)
