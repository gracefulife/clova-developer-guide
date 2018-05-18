# AudioPlayer

AudioPlayerインターフェースは、クライアントからオーディオストリームの再生をリクエストするか、またはオーディオストリームの再生中に発生するイベントをCICにレポートする際に使用される名前欄です。AudioPlayerが提供するイベントとディレクティブは、次の通りです。

| メッセージ         | タイプ  | 説明                                   |
|------------------|-----------|---------------------------------------------|
| [`ClearQueue`](#ClearQueue)           | ディレクティブ | クライアントに対して、オーディオストリームの再生キューをクリアするように指示します。                              |
| [`ExpectReportPlaybackState`](#ExpectReportPlaybackState) | ディレクティブ | クライアントに対して、現在の再生状態をレポートするように指示します。クライアントはこのディレクティブを受信すると、[`AudioPlayer.ReportPlaybackState`](#ReportPlaybackState)イベントをCICに送信する必要があります。 |
| [`Play`](#Play)                       | ディレクティブ | クライアントに対して、特定のオーディオストリームを再生するか、または再生キューに追加するように指示します。                         |
| [`PlayFinished`](#PlayFinished)       | イベント     | クライアントがオーディオストリームの再生を終了するとき、そのオーディオストリームの情報をCICにレポートするために使用します。     |
| [`PlayPaused`](#PlayPaused)           | イベント     | クライアントがオーディオストリームの再生を一時停止するとき、そのオーディオストリームの情報をCICにレポートするために使用します。 |
| [`PlayResumed`](#PlayResumed)         | イベント     | クライアントがオーディオストリームの再生を再開するとき、そのオーディオストリームの情報をCICにレポートするために使用します。         |
| [`PlayStarted`](#PlayStarted)         | イベント     | クライアントがオーディオストリームの再生を開始するとき、そのオーディオストリームの情報をCICにレポートするために使用します。    |
| [`PlayStopped`](#PlayStopped)         | イベント     | クライアントがオーディオストリームの再生を停止するとき、そのオーディオストリームの情報をCICにレポートするために使用します。    |
| [`ProgressReportDelayPassed`](#ProgressReportPositionPassed) | イベント | オーディオストリームの再生が開始してから、指定された遅延期間が経過したときの再生状態([`AudioPlayer.PlaybackState`](/CIC/References/Context_Objects.md#PlaybackState))をCICにレポートします。オーディオストリームの遅延期間は、[`AudioPlayer.Play`](#Play)ディレクティブがクライアントに送信されるときに確認できます。 |
| [`ProgressReportIntervalPassed`](#ProgressReportPositionPassed)| イベント | オーディオストリームの再生が開始してから、指定された間隔ごとの再生状態([`AudioPlayer.PlaybackState`](/CIC/References/Context_Objects.md#PlaybackState))を、CICにレポートします。レポートする間隔は、[`AudioPlayer.Play`](#Play)ディレクティブがクライアントに送信されるときに確認できます。|
| [`ProgressReportPositionPassed`](#ProgressReportPositionPassed) | イベント | オーディオストリームの再生が開始してから、指定されたタイミングに、そのときの再生状態([`AudioPlayer.PlaybackState`](/CIC/References/Context_Objects.md#PlaybackState))をCICにレポートします。レポートするタイミングは、[`AudioPlayer.Play`](#Play)ディレクティブがクライアントに送信されるときに確認できます。|
| [`ReportPlaybackState`](#ReportPlaybackState)           | イベント  | クライアントから、現在のストリーム再生状態をCICにレポートします。クライアントがCICから[`ExpectReportPlaybackState`](#ExpectReportPlaybackState)ディレクティブを受信した場合、`AudioPlayer.ReportPlaybackState`イベントをCICに送信する必要があります。  |
{% if book.TargetReaderType == "Internal" %}| [`RequestPlaybackState`](#RequestPlaybackState)         | イベント  | クライアントのストリーム再生状態をCICにリクエストします。CICは、`AudioPlayer.ReqeustPlaybackState`イベントを受信した場合、ユーザーアカウントに登録されているすべての、または特定のクライアントに[`ExpectReportPlaybackState`](#ExpectReportPlaybackState)ディレクティブを送信します。  |
| [`StreamDeliver`](#StreamDeliver)     | ディレクティブ | [`AudioPlayer.StreamRequested`](#StreamRequested)イベントに対する応答です。実際に再生できるオーディオストリームの情報を受信するために使用します。|{% else %}| [`StreamDeliver`](#StreamDeliver)     | ディレクティブ | [`AudioPlayer.StreamRequested`](#StreamRequested)イベントに対する応答です。実際に再生できるオーディオストリームの情報を受信するために使用します。|{% endif %}
| [`StreamRequested`](#StreamRequested) | イベント     | オーディオストリームを再生するために、ストリーミングのURLなど、追加の情報をCICにリクエストするイベントです。               |
{% if book.TargetReaderType == "Internal" %}| [`SynchronizePlaybackState`](#SynchronizePlaybackState) | ディレクティブ | クライアントのストリーム再生状態を同期するように指示します。`AudioPlayer.RequestPlaybackState`イベントを送信したクライアントは、`AudioPlayer.SynchronizePlaybackState`ディレクティブを受信します。|{% endif %}

## ストリームの再生状態を共有する {#SharePlaybackState}

1つのクライアントは、ユーザーのアカウントに登録されているすべてのクライアントまたは特定のクライアントと、ストリームの再生状態を共有することができます。ストリームの再生状態を共有される動作の流れは、次の通りです。

![](/CIC/Resources/Images/CIC_Playback_State_Sync_Work_Flow.png)

1. Clovaアプリは、{{ "[`AudioPlayer.RequestPlaybackState`](#RequestPlaybackState) イベントを使用して " if book.TargetReaderType == "Internal" }}CICにユーザーのアカウントに登録されているすべてのクライアント、または特定のクライアントのストリーム再生状態をリクエストします。
2. CICは、[`AudioPlayer.ExpectReportPlaybackState`](#ExpectReportPlaybackState)ディレクティブで、ユーザーのアカウントに登録されているすべてのクライアント、または特定のクライアントに、現在のストリーム再生状態をレポートするように指示します。
3. ストリームの再生状態をレポートするように指示されたクライアントは、[`AudioPlayer.ReportPlaybackState`](#ReportPlaybackState)イベントで、CICに現在のストリームの再生状態をレポートします。
4. CICは、{{ "[`AudioPlayer.SynchronizePlaybackState`](#SynchronizePlaybackState)を使用して " if book.TargetReaderType == "Internal" }}他のクライアントのストリーム再生状態をリクエストしたクライアントに状態情報を送信し、同期するように指示します。


## ClearQueueディレクティブ {#ClearQueue}
クライアントに対して、オーディオストリームの再生キューをクリアするように指示します。このディレクティブの`clearBehavior`フィールドの値は、キューをクリアする動作を区分します。クライアントがキューをクリアし、それと同時に現在再生中のオーディオストリームを中止するかを指定します。

### Payload fields

| フィールド名       | データ型    | 説明                     | 包含 |
|---------------|---------|-----------------------------|:---------:|
| `clearBehavior`           | string | クリアする動作を指定するフィールド<ul><li><code>"CLEAR_ALL"</code>：再生キューをすべてクリアして、現在再生中のオーディオストリームを中止します。</li><li><code>"CLEAR_ENQUEUED"</code>：再生キューをクリアして、現在のオーディオストリームの再生を続けます。</li></ul> | 常時 |

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

### 次の項目も参照してください。
* [`AudioPlayer.Play`](#Play)
* [`AudioPlayer.PlayStarted`](#PlayStarted)
* [`AudioPlayer.PlayStopped`](#PlayStopped)

## ExpectReportPlaybackStateディレクティブ {#ExpectReportPlaybackState}

クライアントに対して、現在の再生状態をレポートするように指示します。クライアントはこのディレクティブを受信すると、[`AudioPlayer.ReportPlaybackState`](#ReportPlaybackState)イベントをCICに送信する必要があります。

### Payload fields

なし

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

### 次の項目も参照してください。
* [`AudioPlayer.ReportPlaybackState`](#ReportPlaybackState)
* [ストリームの再生状態を共有する](#SharePlaybackState)

## Playディレクティブ {#Play}
クライアントに対して、特定のオーディオストリームを再生するか、または再生キューに追加するように指示します。

### Payload fields
| フィールド名       | データ型    | 説明                     | 包含 |
|---------------|---------|-----------------------------|:---------:|
| `audioItem`               | object | 再生するオーディオストリームのメタ情報と、再生に必要なオーディオストリームの情報を持つオブジェクト                     | 常時 |
| `audioItem.artImageUrl`   | string | オーディオコンテンツに関連する画像(アルバムの画像)のURL                                                  | 条件付き  |
| `audioItem.audioItemId`   | string | オーディオストリームを区別するID。クライアントはこの値に基づいて、重複するPlayディレクティブを削除できます。 | 常時 |
| `audioItem.headerText`    | string | 主に、現在の再生リストのタイトルを表すテキストフィールド                                                | 条件付き  |
| `audioItem.stream`        | [AudioStreamInfoObject](#AudioStreamInfoObject) | 再生に必要なオーディオストリームの情報を持つオブジェクト        | 常時 |
| `audioItem.titleSubText1` | string | 主にアーティスト名を表すテキストフィールド                                                          | 常時 |
| `audioItem.titleSubText2` | string | 主にアルバム名を表すサブテキストフィールド                                                      | 条件付き |
| `audioItem.titleText`     | string | 現在のオーディオコンテンツのタイトルを表すテキストフィールド                                                         | 常時  |
| `audioItem.type`          | string | **(非推奨)** ストリーミングサービスを示すフィールド。オーディオのストリーミングサービスを提供するプロバイダー、またはサービス名です。このフィールドの値は、サービスによって異なるaudioItemオブジェクトのフィールドを確認し、それを解析するためのパーサー(parser)を選択する際に使用できます。 | 常時 |
| `playBehavior`            | string | ディレクティブに含まれたオーディオストリームを、クライアントでいつ再生するかを指定するフィールド<ul><li><code>"REPLACE_ALL"</code>：再生キューをすべてクリアして、送信されたオーディオストリームをすぐに再生します。</li><li><code>"ENQUEUE"</code>：再生キューに、送信されたオーディオストリームを追加します。</li></ul> | 常時 |
| `source`                  | object | オーディオストリーミングサービスの提供元                                                    | 常時 |
| `source.logoUrl`          | string | オーディオストリーミングサービスのロゴ画像のURLこのフィールドがなかったり、またはフィールド値が空の場合や、ロゴ画像を表示できない場合、`source.name`フィールド内のオーディオストリーミングサービスの名前を表示する必要があります。  | 条件付き |
| `source.name`             | string | オーディオストリーミングサービスの名前                                                        | 常時 |

### 備考
ストリーミングサービスの課金などの理由により、実際のストリーミング情報、つまりストリーミングのURLなどの情報を、再生する直前に取得する場合があります。`audioItem.stream.urlPlayable`フィールドの値によって、次のように区分されます。
* `urlPlayable`フィールドの値が`true`の場合、`audioItem.stream.url`フィールドに含まれたURLで、オーディオストリームをすぐに再生できます。
* `urlPlayable`フィールドの値が`false`の場合、`audioItem.stream.url`フィールドに含まれたURLではオーディオストリームをすぐに再生できず、[`AudioPlayer.StreamRequested`](#StreamRequested)イベントでオーディオストリームの情報を追加でリクエストする必要があります。

### Message example
{% raw %}

```json
// すぐに再生できるオーディオストリームのURL情報が含まれたサンプル
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

// すぐに再生できないオーディオストリームのURL情報が含まれたサンプル
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

### 次の項目も参照してください。
* [`AudioPlayer.PlayPaused`](#PlayPaused)
* [`AudioPlayer.PlayResumed`](#PlayResumed)
* [`AudioPlayer.PlayStarted`](#PlayStarted)
* [`AudioPlayer.PlayStopped`](#PlayStopped)
* [`AudioPlayer.ProgressReportDelayPassed`](#ProgressReportDelayPassed)
* [`AudioPlayer.ProgressReportIntervalPassed`](#ProgressReportIntervalPassed)
* [`AudioPlayer.ProgressReportPositionPassed`](#ProgressReportPositionPassed)
* [`AudioPlayer.StreamRequested`](#StreamRequested)

## PlayFinishedイベント {#PlayFinished}
クライアントがオーディオストリームの再生を終了するとき、そのオーディオストリームの情報をCICにレポートするために使用します。

### Context fields

{% include "/CIC/References/CICInterface/Context_Objects_List.md" %}

### Payload fields

| フィールド名       | データ型    | 説明                     | 必須/任意 |
|---------------|---------|-----------------------------|:---------:|
| `token`                | string | ['AudioPlayer.Play'](#Play)ディレクティブの`audioItem.stream.token`フィールド値 | 必須 |
| `offsetInMilliseconds` | number | ストリームの現在のオフセット。ミリ秒単位です。                         | 必須  |

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

### 次の項目も参照してください。
* [`AudioPlayer.Play`](#Play)

## PlayPausedイベント {#PlayPaused}
クライアントがオーディオストリームの再生を一時停止するとき、そのオーディオストリームの情報をCICにレポートするために使用します。このイベントを送信するには、次のような事前のシナリオが必要です。

1. クライアントは、[`SpeechRecognizer.Recognize`](/CIC/References/CICInterface/SpeechRecognizer.md#Recognize)イベントで、オーディオストリームの再生を一時停止するようにリクエストするユーザーの音声をCICに送信します。
2. CICは、Clovaプラットフォームで認識された一時停止のリクエストを、[`PlaybackController.Pause`](/CIC/References/CICInterface/PlaybackController.md#Pause)ディレクティブでクライアントに送信します。
3. クライアントはオーディオストリームの再生を一時停止し、PlayPausedイベントをCICに送信します。

### Context fields

{% include "/CIC/References/CICInterface/Context_Objects_List.md" %}

### Payload fields

| フィールド名       | データ型    | 説明                     | 必須/任意 |
|---------------|---------|-----------------------------|:---------:|
| `token`                | string | ['AudioPlayer.Play'](#Play)ディレクティブの`audioItem.stream.token`フィールド値 | 必須 |
| `offsetInMilliseconds` | number | ストリームの現在のオフセット。ミリ秒単位です。                         | 必須  |

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

### 次の項目も参照してください。
* [`AudioPlayer.Play`](#Play)
* [`AudioPlayer.PlayResumed`](#PlayResumed)
* [`PlaybackController.Pause`](/CIC/References/CICInterface/PlaybackController.md#Pause)

## PlayResumedイベント {#PlayResumed}

クライアントがオーディオストリームの再生を再開するとき、そのオーディオストリームの情報をCICにレポートするために使用します。このイベントを送信するには、次のような事前のシナリオが必要です。

1. クライアントは、[`SpeechRecognizer.Recognize`](/CIC/References/CICInterface/SpeechRecognizer.md#Recognize)イベントで、オーディオストリームの再生を再開するようにリクエストするユーザーの音声をCICに送信します。
2. CICは、Clovaプラットフォームで認識された再生再開のリクエストを、[`PlaybackController.Resume`](/CIC/References/CICInterface/PlaybackController.md#Resume)ディレクティブでクライアントに送信します。
3. クライアントは、オーディオストリームの再生を再開し、PlayResumedイベントをCICに送信します。

### Context fields

{% include "/CIC/References/CICInterface/Context_Objects_List.md" %}

### Payload fields

| フィールド名       | データ型    | 説明                     | 必須/任意 |
|---------------|---------|-----------------------------|:---------:|
| `token`                | string | ['AudioPlayer.Play'](#Play)ディレクティブの`audioItem.stream.token`フィールド値 | 必須 |
| `offsetInMilliseconds` | number | ストリームの現在のオフセット。ミリ秒単位です。                         | 必須  |

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

### 次の項目も参照してください。
* [`AudioPlayer.Play`](#Play)
* [`AudioPlayer.PlayPaused`](#PlayPaused)
* [`PlaybackController.Resume`](/CIC/References/CICInterface/PlaybackController.md#Resume)

## PlayStartedイベント {#PlayStarted}
クライアントがオーディオストリームの再生を開始するとき、そのオーディオストリームの情報をCICにレポートするために使用します。

### Context fields

{% include "/CIC/References/CICInterface/Context_Objects_List.md" %}

### Payload fields

| フィールド名       | データ型    | 説明                     | 必須/任意 |
|---------------|---------|-----------------------------|:---------:|
| `token`                | string | ['AudioPlayer.Play'](#Play)ディレクティブの`audioItem.stream.token`フィールド値 | 必須 |
| `offsetInMilliseconds` | number | ストリームの現在のオフセット。ミリ秒単位です。                         | 必須  |

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

### 次の項目も参照してください。
* [`AudioPlayer.Play`](#Play)
* [`AudioPlayer.PlayStopped`](#PlayStopped)

## PlayStoppedイベント {#PlayStopped}
クライアントがオーディオストリームの再生を停止するとき、そのオーディオストリームの情報をCICにレポートするために使用します。このイベントを送信するには、次のような事前のシナリオが必要です。

1. クライアントは[`SpeechRecognizer.Recognize`](/CIC/References/CICInterface/SpeechRecognizer.md#Recognize)イベントで、オーディオストリームの再生を停止するようにリクエストするユーザーの音声をCICに送信します。
2. CICは、Clovaプラットフォームで認識された停止のリクエストを、[`PlaybackController.Stop`](/CIC/References/CICInterface/PlaybackController.md#Stop)ディレクティブでクライアントに送信します。
3. クライアントはオーディオストリームの再生を停止し、PlayStoppedイベントをCICに送信します。

### Context fields

{% include "/CIC/References/CICInterface/Context_Objects_List.md" %}

### Payload fields

| フィールド名       | データ型    | 説明                     | 必須/任意 |
|---------------|---------|-----------------------------|:---------:|
| `token`                | string | ['AudioPlayer.Play'](#Play)ディレクティブの`audioItem.stream.token`フィールド値 | 必須 |
| `offsetInMilliseconds` | number | ストリームの現在のオフセット。ミリ秒単位です。                         | 必須  |

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

### 次の項目も参照してください。
* [`AudioPlayer.Play`](#Play)
* [`AudioPlayer.PlayStarted`](#PlayStarted)
* [`PlaybackController.Stop`](/CIC/References/CICInterface/PlaybackController.md#Stop)

## ProgressReportDelayPassedイベント {#ProgressReportDelayPassed}
オーディオストリームの再生が開始してから、指定された遅延期間が経過したときの再生状態([`AudioPlayer.PlaybackState`](/CIC/References/Context_Objects.md#PlaybackState))をCICにレポートします。オーディオストリームの遅延期間は、[`AudioPlayer.Play`](#Play)ディレクティブがクライアントに送信されるときに確認できます。

### Context fields

{% include "/CIC/References/CICInterface/Context_Objects_List.md" %}

### Payload fields

| フィールド名       | データ型    | 説明                     | 必須/任意 |
|---------------|---------|-----------------------------|:---------:|
| `token`                | string | ['AudioPlayer.Play'](#Play)ディレクティブの`audioItem.stream.token`フィールド値 | 必須 |
| `offsetInMilliseconds` | number | ストリームの現在のオフセット。ミリ秒単位です。                         | 必須  |

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

### 次の項目も参照してください。
* [`AudioPlayer.Play`](#Play)
* [`AudioPlayer.ProgressReportIntervalPassed`](#ProgressReportIntervalPassed)
* [`AudioPlayer.ProgressReportPositionPassed`](#ProgressReportPositionPassed)

## ProgressReportIntervalPassedイベント {#ProgressReportIntervalPassed}
オーディオストリームの再生が開始してから、指定された間隔ごとの再生状態([`AudioPlayer.PlaybackState`](/CIC/References/Context_Objects.md#PlaybackState))を、CICにレポートします。レポートする間隔は、[`AudioPlayer.Play`](#Play)ディレクティブがクライアントに送信されるときに確認できます。

### Context fields

{% include "/CIC/References/CICInterface/Context_Objects_List.md" %}

### Payload fields

| フィールド名       | データ型    | 説明                     | 必須/任意 |
|---------------|---------|-----------------------------|:---------:|
| `token`                | string | ['AudioPlayer.Play'](#Play)ディレクティブの`audioItem.stream.token`フィールド値 | 必須 |
| `offsetInMilliseconds` | number | ストリームの現在のオフセット。ミリ秒単位です。                         | 必須  |

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

### 次の項目も参照してください。
* [`AudioPlayer.Play`](#Play)
* [`AudioPlayer.ProgressReportDelayPassed`](#ProgressReportDelayPassed)
* [`AudioPlayer.ProgressReportPositionPassed`](#ProgressReportPositionPassed)

## ProgressReportPositionPassedイベント {#ProgressReportPositionPassed}
オーディオストリームの再生が開始してから、指定されたタイミングに、そのときの再生状態([`AudioPlayer.PlaybackState`](/CIC/References/Context_Objects.md#PlaybackState))をCICにレポートします。レポートするタイミングは、[`AudioPlayer.Play`](#Play)ディレクティブがクライアントに送信されるときに確認できます。

### Context fields

{% include "/CIC/References/CICInterface/Context_Objects_List.md" %}

### Payload fields

| フィールド名       | データ型    | 説明                     | 必須/任意 |
|---------------|---------|-----------------------------|:---------:|
| `token`                | string | ['AudioPlayer.Play'](#Play)ディレクティブの`audioItem.stream.token`フィールド値 | 必須 |
| `offsetInMilliseconds` | number | ストリームの現在のオフセット。ミリ秒単位です。                         | 必須  |

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

### 次の項目も参照してください。
* [`AudioPlayer.Play`](#Play)
* [`AudioPlayer.ProgressReportDelayPassed`](#ProgressReportDelayPassed)
* [`AudioPlayer.ProgressReportIntervalPassed`](#ProgressReportIntervalPassed)

## ReportPlaybackStateイベント {#ReportPlaybackState}

クライアントから、現在のストリーム再生状態をCICにレポートします。クライアントがCICから[`AudioPlayer.ExpectReportPlaybackState`](#ExpectReportPlaybackState)ディレクティブを受信した場合、`AudioPlayer.ReportPlaybackState`イベントをCICに送信する必要があります。

### Context fields

{% include "/CIC/References/CICInterface/Context_Objects_List.md" %}

### Payload fields
| フィールド名       | データ型    | 説明                     | 必須/任意 |
|---------------|---------|-----------------------------|:---------:|
| `offsetInMilliseconds`   | number  | ストリームの現在のオフセット。ミリ秒単位です。  | 選択  |
| `playerActivity`         | string  | AudioPlayerの現在の状態。<ul><li><code>"IDLE"</code>：アイドル状態</li><li><code>"PLAYING"</code>：再生中</li><li><code>"PAUSED"</code>：一時停止</li><li><code>"STOPPED"</code>：停止状態</li></ul>  | 必須  |
| `repeatMode`             | string  | リピート再生モード<ul><li><code>"NONE"</code>：リピート再生しない</li><li><code>"REPEAT_ONE"</code>：1つのコンテンツをリピート再生する</li></ul>  | 必須  |
| `stream`                 | [AudioStreamInfoObject](#AudioStreamInfoObject) | Playディレクティブの`audioItem.stream`                                     | 選択 |
| `token`                  | string  | ['AudioPlayer.Play'](#Play)ディレクティブの`audioItem.stream.token`フィールド値                                          | 選択 |
| `totalInMilliseconds`    | number | 最近再生したオーディオの全長。[`AudioPlayer.Play`](/CIC/References/CICInterface/AudioPlayer.md#Play)ディレクティブで送信された([AudioStreamInfoObject](/CIC/References/CICInterface/AudioPlayer.md#AudioStreamInfoObject))に`durationInMilliseconds`フィールドの値がある場合、このフィールドに入力します。ミリ秒単位で、`playerActivity`の値が`"IDLE"`の場合、このフィールドの値を入力する必要はありません。 | 選択 |

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

### 次の項目も参照してください。
* [`AudioPlayer.ExpectReportPlaybackState`](#ExpectReportPlaybackState)
* [`AudioPlayer.Play`](#Play)
* [ストリームの再生状態を共有する](#SharePlaybackState)

{% if book.TargetReaderType == "Internal" %}
## RequestPlaybackStateイベント {#RequestPlaybackState}

クライアントのストリーム再生状態をCICにリクエストします。CICは、`AudioPlayer.ReqeustPlaybackState`イベントを受信した場合、ユーザーアカウントに登録されているすべての、または特定のクライアントに[`AudioPlayer.ExpectReportPlaybackState`](#ExpectReportPlaybackState)ディレクティブを送信します。

### Context fields

{% include "/CIC/References/CICInterface/Context_Objects_List.md" %}

### Payload fields
| フィールド名       | データ型    | 説明                     | 必須/任意 |
|---------------|---------|-----------------------------|:---------:|
| `deviceId`    | string  | 対象クライアントのID。任意の形式の識別子(不透明なID)です。このフィールドが省略されると、ユーザーアカウントに登録されているすべてのクライアントにリクエストが送信されます。 | 選択 |

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

### 次の項目も参照してください。
* [`AudioPlayer.ExpectReportPlaybackState`](#ExpectReportPlaybackState)
* [`AudioPlayer.Play`](#Play)
* [ストリームの再生状態を共有する](#SharePlaybackState)
{% endif %}

## StreamDeliverディレクティブ {#StreamDeliver}
[`AudioPlayer.StreamRequested`](#StreamRequested)イベントに対する応答です。実際に再生できるオーディオストリームの情報を受信するために使用します。クライアントがコンテンツを再生できるように、オーディオストリームの情報にストリーミングURLが必ず含まれます。

### Payload fields
| フィールド名 | データ型 | 説明 | 包含 |
|---------|------|--------|:---------:|
| `audioItemId` | string | オーディオストリームの情報を区別するための値。クライアントはこの値に基づいて、重複するPlayディレクティブを削除できます。 | 常時 |
| `audioStream` | [AudioStreamInfoObject](#AudioStreamInfoObject) | 再生に必要なオーディオストリームの情報を持つオブジェクト       | 常時 |

### 備考
`StreamDeliver`ディレクティブで送信される`AudioStreamInfoObject`オブジェクトは、既存の[`AudioPlayer.Play`](#Play)ディレクティブで送信された`AudioStreamInfoObject`オブジェクトと重複しないように、一部の内容が省略されることがあります。ストリームを再生する際、`StreamDeliver`ディレクティブと、すでに受信した[`Play`](#Play)ディレクティブの`payload.audioStream`情報を組み合わせて使用する必要があります。

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

### 次の項目も参照してください。
* [`AudioPlayer.Play`](#Play)
* [`AudioPlayer.StreamRequested`](#StreamRequested)

## StreamRequestedイベント {#StreamRequested}
オーディオストリームを再生するために、ストリーミングのURLなど、追加の情報をCICにリクエストするイベントです。

### Context fields

{% include "/CIC/References/CICInterface/Context_Objects_List.md" %}

### Payload fields
| フィールド名       | データ型    | 説明                     | 必須/任意 |
|---------------|---------|-----------------------------|:---------:|
| `audioItemId`   | string  | ['AudioPlayer.Play'](#Play)ディレクティブの`audioItem.audioItemId`フィールド値       | 必須 |
| `audioStream`   | [AudioStreamInfoObject](#AudioStreamInfoObject) | Playディレクティブの`audioItem.stream` | 必須 |

### 備考
ストリーミングサービスの課金などの理由により、ときには、実際のオーディオストリームの情報の発行を、再生直前に遅延させる必要が生じます。このイベントは、このようにオーディオストリームの情報をあらかじめ準備してはいけない場合のために設計されたAPIです。クライアントは、このイベントを再生直前より先に送信しない必要があります。

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

### 次の項目も参照してください。
* [`AudioPlayer.Play`](#Play)
* [`AudioPlayer.StreamDeliver`](#StreamDeliver)

{% if book.TargetReaderType == "Internal" %}
## SynchronizePlaybackStateディレクティブ {#SynchronizePlaybackState}

クライアントのストリーム再生状態を同期するように指示します。`AudioPlayer.RequestPlaybackState`イベントを送信したクライアントは、`AudioPlayer.SynchronizePlaybackState`ディレクティブを受信します。

### Payload fields

| フィールド名       | データ型    | 説明                     | 包含 |
|---------------|---------|-----------------------------|:---------:|
| `deviceId`    | string  | 対象クライアントのID。任意の形式の識別子(不透明なID)です。  | 常時  |
| `event`       | string  | クライアントで発生したイベント。<ul><li><code>PlayFinished</code></li><li><code>PlayPaused</code></li><li><code>PlayResumed</code></li><li><code>PlayStarted</code></li><li><code>PlayStopped</code></li></ul>  | 条件付き  |
| `playbackState`          | object  | クライアントの再生状態の情報を持つオブジェクト             | 条件付き  |
| `playbackState.offsetInMilliseconds`   | number  | ストリームの現在のオフセット。ミリ秒単位で、このフィールドの値はnullの場合があります。  | 条件付き  |
| `playbackState.playerActivity`         | string  | AudioPlayerの現在の状態。<ul><li><code>"IDLE"</code>：アイドル状態</li><li><code>"PLAYING"</code>：再生中</li><li><code>"PAUSED"</code>：一時停止</li><li><code>"STOPPED"</code>：停止状態</li></ul>  | 常時  |
| `playbackState.repeatMode`             | string  | 設定されているリピート再生モード。<ul><li><code>"NONE"</code>：リピート再生しない</li><li><code>"REPEAT_ONE"</code>：1つのコンテンツをリピート再生する</li></ul>  | 常時  |
| `playbackState.stream`                 | [AudioStreamInfoObject](#AudioStreamInfoObject) | オーディオストリームに関連する情報を持つオブジェクト                                         | 常時 |
| `playbackState.token`                  | string  | ストリームの再生を識別するトークン。このフィールドは、空の文字列(`""`)を持つ場合があります。                                                    | 常時 |
| `playbackState.totalInMilliseconds`    | number | 最近再生したオーディオの全長。ミリ秒単位で、このフィールドの値はnullの場合があります。                  | 常時 |

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

### 次の項目も参照してください。
* [`AudioPlayer.ReportPlaybackState`](#ReportPlaybackState)
* [ストリームの再生状態を共有する](#SharePlaybackState)
{% endif %}

## 共有オブジェクト
AudioPlayer APIを使ってイベントまたはディレクティブを送信する際、ペイロード(`payload`)に次のオブジェクトを共有して使用します。

| オブジェクト            | 説明                                            |
|--------------------|---------------------------------------------------|
| [AudioStreamInfoObject](#AudioStreamInfoObject) | 再生するストリームの再生情報(ストリーミングのURL、認証情報など)を持つオブジェクト |

### AudioStreamInfoObject {#AudioStreamInfoObject}
再生するオーディオストリームのストリーミング情報を持つオブジェクトです。クライアントに対して再生するストリーミングの情報を送信したり、クライアントがCICに対して、現在再生しているコンテンツのストリーミング情報を送信するとき使用します。

#### Object fields
| フィールド名       | データ型    | 説明                     | 必須/包含 |
|---------------|---------|-----------------------------|:-------------:|
| `beginAtInMilliseconds`  | number | 再生を開始するオフセット。ミリ秒単位で、この値が指定されている場合、クライアントは、そのオーディオストリームを指定されたオフセットから再生する必要があります。この値が0に設定されている場合、ストリームを最初から再生します。          | 必須/常時 |
| `customData`             | string | 現在のストリームに関連して、任意の形式を持つメタデータ情報。特定のカテゴリに分類されたり、定義されないストリーミング情報は、このフィールドに含まれるか、または入力される必要があります。オーディオストリーム再生のコンテキストに必要な追加の値を、サービスプロバイダーがカスタムで追加できます。<div class="danger"><p><strong>注意</strong></p><p>クライアントは、このフィールドの値を任意に使用してはなりません。問題が発生する恐れがあります。また、このフィールドの値はストリームの再生状態を送信する際、<a href="/CIC/References/Context_Objects.html#PlaybackState">PlaybackStateコンテキスト</a>の`stream`フィールドにそのまま添付される必要があります。</p></div> | 任意/条件付き  |
| `durationInMilliseconds` | number | オーディオストリームの再生時間。クライアントは、`beginAtInMilliseconds`フィールドに指定されている再生のオフセットから、このフィールドに指定されている再生時間だけ、そのオーディオストリームをシークおよび再生できます。例えば、`beginAtInMilliseconds`フィールドの値が`10000`で、このフィールドの値が`60000`の場合、そのオーディオストリームの10秒から70秒までの区間を再生およびシークすることができます。ミリ秒単位です。   | 任意/条件付き  |
| `progressReport`         | object  | 再生が開始してから、再生状態をレポートするタイミングを指定するオブジェクト                                                  | 任意/条件付き |
| `progressReport.progressReportDelayInMilliseconds`    | number | 再生が開始してから、指定された時間が経過した後に、再生状態をレポートするように指定する値です。ミリ秒単位で、このフィールドの値はnullの場合があります。  | 任意/条件付き |
| `progressReport.progressReportIntervalInMilliseconds` | number | 再生中に、指定されたインターバルで再生状態をレポートするように指定する値です。ミリ秒単位で、このフィールドの値はnullの場合があります。        | 任意/条件付き |
| `progressReport.progressReportPositionInMilliseconds` | number | 再生中に、指定された再生位置を経過する度に、再生状態をレポートするように指定する値です。ミリ秒単位で、このフィールドの値はnullの場合があります。    | 任意/条件付き |
| `token`                  | string  | オーディオストリームのトークン                                                                                   | 必須/常時 |
| `url`                    | string  | オーディオストリームのURL                                                                                     | 必須/常時 |
| `urlPlayable`            | boolean | `url`フィールドのオーディオストリームのURLがすぐに再生できるかを示す値。<ul><li><code>true</code>：すぐに再生できるURL</li><li><code>false</code>：すぐに再生できないURL。<a href="#StreamRequested"><code>AudioPlayer.StreamRequested</code></a>イベントでオーディオストリームの情報を追加でリクエストする必要があります。</li></ul>        | 必須/常時 |

#### 備考
* クライアントが`beginAtInMilliseconds`と`durationInMilliseconds`フィールドに指定されている区間に対して、ストリームの再生を終了すると、[`AudioPlayer.PlayFinished`](#PlayFinished)イベントをCICに送信する必要があります。
* クライアントは、ユーザーが`beginAtInMilliseconds`と`durationInMilliseconds`フィールドに指定された区間外ではシーク(seek)できないように、UIを提供する必要があります。
* クライアントの現在の再生状態をCICにレポートする際、[`AudioPlayer.PlaybackState`](/CIC/References/Context_Objects.md#PlaybackState)の`totalInMilliseconds`フィールドの値は、`beginAtInMilliseconds`フィールドと`durationInMilliseconds`フィールドに指定された値の合計を入力します。

#### Object Example
{% raw %}

```json
// すぐに再生できるオーディオストリームのURL情報が含まれたオブジェクト
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

// すぐに再生できないオーディオストリームのURL情報が含まれたサンプル
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

#### 次の項目も参照してください。
* [`AudioPlayer.Play`](#Play)
* [`AudioPlayer.PlayFinished`](#PlayFinished)
* [`AudioPlayer.ProgressReportDelayPassed`](#ProgressReportDelayPassed)
* [`AudioPlayer.ProgressReportIntervalPassed`](#ProgressReportIntervalPassed)
* [`AudioPlayer.ProgressReportPositionPassed`](#ProgressReportPositionPassed)
* [`AudioPlayer.StreamRequested`](#StreamRequested)
