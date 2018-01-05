## AudioPlayer.PlaybackState {#PlaybackState}

`AudioPlayer.PlaybackState` is a format for reporting to CIC the details of media currently playing or the last media played.

### Object  structure

{% raw %}
```json
{
  "header": {
    "namespace": "AudioPlayer",
    "name": "PlaybackState"
  },
  "payload": {
    "offsetInMilliseconds": {{number}},
    "totalInMilliseconds": {{number}},
    "playerActivity": {{string}},
    "stream": {{AudioStreamInfoObject}}
  }
}
```
{% endraw %}


### Payload fields

| Field       | Type    | Description                     | Required |
|---------------|:---------:|-----------------------------|:---------:|
| `offsetInMilliseconds` | number | The last playback point (offset) of the recently played media. Unit is millisecond. This field is omissible if the `playerActivity` field is set to `"IDLE"`.                                                  | Optional |
| `playerActivity`       | string | Indicates the state of the player. Available states are:<ul><li><code>"IDLE"</code>: Player is inactive.</li><li><code>"PLAYING"</code>: Player is playing.</li><li><code>"PAUSED"</code>: Player has paused.</li><li><code>"STOPPED"</code>: Player is stopped.</li></ul> | Required |
| `stream`               | [AudioStreamInfoObject](/CIC/References/CICInterface/AudioPlayer.md#AudioStreamInfoObject) | Contains the details of the media currently playing. This field is omissible if the `playerActivity` field is set as `"IDLE"`. Enter the details with the information defined in the `stream` object, provided by the [`AudioPlayer.Play`](/CIC/References/CICInterface/AudioPlayer.md#Play) directive or [`AudioPlayer.StreamDeliver`](/CIC/References/CICInterface/AudioPlayer.md#StreamDeliver) directive. | Optional |
| `totalInMilliseconds`  | number | The total duration of the recently played media, in milliseconds. Enter the value of the `durationInMilliseconds` field of the [AudioStreamInfoObject](/CIC/References/CICInterface/AudioPlayer.md#AudioStreamInfoObject) provided by the [`AudioPlayer.Play`](/CIC/References/CICInterface/AudioPlayer.md#Play) directive, if the value is available. This field is omissible if the `playerActivity` field is set to `"IDLE"`.      | Optional |

### Example

{% raw %}

```json
// Case 1: Playing has stopped
{
  "header": {
    "namespace": "AudioPlayer",
    "name": "PlaybackState"
  },
  "payload": {
    "offsetInMilliseconds": 1,
    "totalInMilliseconds": 100,
    "playerActivity": "STOPPED",
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

// Example 2: Player is inactive
{
  "header": {
    "namespace": "AudioPlayer",
    "name": "PlaybackState"
  },
  "payload": {
    "playerActivity": "IDLE"
  }
}
```

{% endraw %}

### See also

* [`AudioPlayer.Play`](/CIC/References/CICInterface/AudioPlayer.md#Play)
* [`AudioPlayer.StreamDeliver`](/CIC/References/CICInterface/AudioPlayer.md#StreamDeliver)
* [`AudioPlayer.StreamRequested`](/CIC/References/CICInterface/AudioPlayer.md#StreamRequested)
