## AudioPlayer.PlaybackState {#PlaybackState}
PlaybackState is a message format that contains details of media currently playing or previously played. The details can be sent to an [extension](/CEK/References/CEK_API.md#CustomExtMessage) that provides a music streaming service.

### Message structure

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
    "stream": {{AudioStreamObject}}
  }
}
```
{% endraw %}


### Payload field

| Field name       | Type    | Field description                     | Required |
|---------------|---------|-----------------------------|---------|
| `offsetInMilliseconds` | number | The last playback point (offset) of the recently played media. Unit is millisecond. You do not have to enter a value in this field if `playerActivity` is set to `"IDLE"`.                                                  | No |
| `playerActivity`       | string | Indicates a state of the player. Available values are:<ul><li><code>"IDLE"</code>: Player is idle</li><li><code>"PLAYING"</code>: Player is playing</li><li><code>"PAUSED"</code>: Player paused playing</li><li><code>"STOPPED"</code>: Player stopped playing</li></ul> | Yes |
| `stream`               | [AudioStreamObject](/CIC/References/APIs/AudioPlayer.md#AudioStreamObject) | An object containing details of the currently playing media. You do not have to enter a value in this field if `playerActivity` is set to `"IDLE"`. Enter media details (`stream` object) returned from [`AudioPlayer.Play`](/CIC/References/APIs/AudioPlayer.md#Play) or [`AudioPlayer.StreamDelivered`](/CIC/References/APIs/AudioPlayer.md#StreamDelivered) directive message. | No |
| `totalInMilliseconds`  | number | The total length of the recently played media. Unit is millisecond. You do not have to enter a value in this field if `playerActivity` is set to `"IDLE"`.                                                               | No |

### Message example
#### Example 1: When playback has stopped

{% raw %}
```json
// Case 1: Playback has stopped
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
```
{% endraw %}

#### Example 2: When a player is inactivated

{% raw %}
```json
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
* [`AudioPlayer.Play`](/CIC/References/APIs/AudioPlayer.md#Play)
* [`AudioPlayer.StreamDeliver`](/CIC/References/APIs/AudioPlayer.md#StreamDeliver)
* [`AudioPlayer.StreamRequested`](/CIC/References/APIs/AudioPlayer.md#StreamRequested)
