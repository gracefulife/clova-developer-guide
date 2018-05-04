## AudioPlayer.PlaybackState {#PlaybackState}
`AudioPlayer.PlaybackState` is a format for reporting to CIC the details of media currently playing or the last media played.

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

| Field name       | Data type    | Description                     | Required |
|---------------|---------|-----------------------------|:---------:|
| `offsetInMilliseconds` | number | The most recent playback position (offset) of the recently played media. The unit is in milliseconds. This field is omissible if the `playerActivity` field is set to `"IDLE"`.                                                  | Optional |
| `playerActivity`       | string | Indicates the state of the player. Available values are:<ul><li><code>"IDLE"</code>: Deactivated</li><li><code>"PLAYING"</code>: Playing</li><li><code>"PAUSED"</code>: Paused</li><li><code>"STOPPED"</code>: Stopped</li></ul> | Required |
| `repeatMode`           | string  | The repeat mode.<ul><li><code>"NONE"</code>: None</li><li><code>"REPEAT_ONE"</code>: Repeat one song</li></ul>                                                   | Required  |
| `stream`               | [AudioStreamInfoObject](/CIC/References/CICInterface/AudioPlayer.md#AudioStreamInfoObject) | The details of the currently playing media. This field is omissible if the `playerActivity` field is set as `"IDLE"`. Enter the details with the information defined in the `stream` object provided by the [`AudioPlayer.Play`](/CIC/References/CICInterface/AudioPlayer.md#Play) directive or [`AudioPlayer.StreamDeliver`](/CIC/References/CICInterface/AudioPlayer.md#StreamDeliver) directive. | Optional |
| `totalInMilliseconds`  | number | The total duration of the recently played media. Enter the value of the `durationInMilliseconds` field of the [AudioStreamInfoObject](/CIC/References/CICInterface/AudioPlayer.md#AudioStreamInfoObject) provided by the [`AudioPlayer.Play`](/CIC/References/CICInterface/AudioPlayer.md#Play) directive, if the value is available. The unit is in milliseconds. This field is omissible if the `playerActivity` field is set to `"IDLE"`.                                                               | Optional |

### Object example

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

// Example 2: The player is deactivated
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

### See also
* [`AudioPlayer.Play`](/CIC/References/CICInterface/AudioPlayer.md#Play)
* [`AudioPlayer.StreamDeliver`](/CIC/References/CICInterface/AudioPlayer.md#StreamDeliver)
* [`AudioPlayer.StreamRequested`](/CIC/References/CICInterface/AudioPlayer.md#StreamRequested)
