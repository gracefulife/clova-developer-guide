## AudioPlayer.PlaybackState {#PlaybackState}
`AudioPlayer.PlaybackState`は、現在再生中か、または最後に再生したオーディオの情報をCICにレポートするときに使用されるメッセージ形式です。

### Object structure
{% raw %}
```json
{
  "header": {
    "namespace": "AudioPlayer",
    "name": "PlaybackState"
  },
  "payload": {
    "offsetInMilliseconds": {{number}},
    "playerActivity": {{string}},
    "repeatMode": {{string}},
    "stream": {{AudioStreamInfoObject}},
    "totalInMilliseconds": {{number}}
  }
}
```
{% endraw %}


### Payload fields

| フィールド名       | データ型    | 説明                     | 必須/任意 |
|---------------|---------|-----------------------------|:---------:|
| `offsetInMilliseconds` | number | 最近再生したオーディオの最後の再生ポイント(オフセット)。ミリ秒単位で、`playerActivity`の値が`"IDLE"`の場合、このフィールドの値を入力する必要はありません。                                                  | 任意 |
| `playerActivity`       | string | プレイヤーの状態を示す値です。以下の値を持ちます。<ul><li><code>"IDLE"</code>：非アクティブ状態</li><li><code>"PLAYING"</code>：再生中</li><li><code>"PAUSED"</code>：一時停止状態</li><li><code>"STOPPED"</code>：停止状態</li></ul> | 必須 |
| `repeatMode`           | string  | リピート再生モード<ul><li><code>"NONE"</code>：リピート再生しない</li><li><code>"REPEAT_ONE"</code>：一曲リピート再生</li></ul>                                                   | 必須  |
| `stream`               | [AudioStreamInfoObject](/CIC/References/CICInterface/AudioPlayer.md#AudioStreamInfoObject) | 再生中のオーディオの詳細情報が保存されているオブジェクト`playerActivity`の値が`"IDLE"`の場合、このフィールドの値を入力する必要がありません。[`AudioPlayer.Play`](/CIC/References/CICInterface/AudioPlayer.md#Play)または[`AudioPlayer.StreamDeliver`](/CIC/References/CICInterface/AudioPlayer.md#StreamDeliver)ディレクティブで送信されたオーディオの情報(`stream`オブジェクト)の値を入力します。 | 任意 |
| `totalInMilliseconds`  | number | 最近再生したオーディオの全長。[`AudioPlayer.Play`](/CIC/References/CICInterface/AudioPlayer.md#Play)ディレクティブで送信された([AudioStreamInfoObject](/CIC/References/CICInterface/AudioPlayer.md#AudioStreamInfoObject))に`durationInMilliseconds`フィールドの値がある場合、このフィールドに入力します。ミリ秒単位で、`playerActivity`の値が`"IDLE"`の場合、このフィールドの値を入力する必要はありません。                                                               | 任意 |

### Object example

{% raw %}

```json
// Case 1：再生が停止された状態
{
  "header": {
    "namespace": "AudioPlayer",
    "name": "PlaybackState"
  },
  "payload": {
    "offsetInMilliseconds": 1,
    "totalInMilliseconds": 100,
    "playerActivity": "STOPPED",
    "repeatMode": "NONE",
    "stream": {
      "beginAtInMilliseconds": 0,
      "progressReport": {
        "progressReportDelayInMilliseconds": null,
        "progressReportIntervalInMilliseconds": null,
        "progressReportPositionInMilliseconds": 60000
      },
      "token": "TR-NM-17740107",
      "url": "clova:TR-NM-17740107",
      "urlPlayable": false
    }
  }
}

//サンプル2：プレイヤーが非アクティブになっている状態
{
  "header": {
    "namespace": "AudioPlayer",
    "name": "PlaybackState"
  },
  "payload": {
    "playerActivity": "IDLE",
    "repeatMode": "NONE"
  }
}
```

{% endraw %}

### 次の項目も参照してください。
* [`AudioPlayer.Play`](/CIC/References/CICInterface/AudioPlayer.md#Play)
* [`AudioPlayer.StreamDeliver`](/CIC/References/CICInterface/AudioPlayer.md#StreamDeliver)
* [`AudioPlayer.StreamRequested`](/CIC/References/CICInterface/AudioPlayer.md#StreamRequested)
