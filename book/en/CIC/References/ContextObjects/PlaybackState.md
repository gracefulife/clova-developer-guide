## AudioPlayer.PlaybackState {#PlaybackState}
PlaybackState is a message format containing information of the media which is currently being played or was lastly played. This information may be delivered using a [custom extension message](/CEK/References/CEK_Message_Format.md#CustomExtenstionMessage) that provides music service in the future.

### Message format
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

| Field name  | Type  | Field description  | Required |
|---------------|---------|-----------------------------|---------|
| offsetInMilliseconds | number | The last playback point (offset) of the media recently played. The unit is a millisecond. This field can be left empty when *playerActivity* is "IDLE".  | No |
| playerActivity  | string | Indicates the state of the player. Available values are: <ul><li>"IDLE": Player is in an idle state</li><li>"PLAYING": Player is in a playing state</li><li>"PAUSED": Player is in a paused state</li><li>"STOPPED": Player is in a stopped state</li></ul> | Yes |
| stream  | [AudioStreamObject](/CIC/References/APIs/AudioPlayer.md#AudioStreamObject) | The object storing details of the currently playing media. This field can be left empty when *playerActivity* is "IDLE". Enter the media information (*stream* object) which was delivered in [AudioPlayer.Play](/CIC/References/APIs/AudioPlayer.md#Play) or [AudioPlayer.StreamDelivered](/CIC/References/APIs/AudioPlayer.md#StreamDelivered) Directive message. | No |
| totalInMilliseconds  | number | The total length of the media recently played. The unit is a millisecond. This field can be left empty when *playerActivity* is "IDLE".  | No |

### Message example
#### Example 1: When playback is stopped
{% raw %}
```json
// Case 1: When playback is stopped
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
      "url": "clova:TR-NM-17740107"
    }
  }
}
```
{% endraw %}

#### Example 2: When the player is in an inactive state
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
* [AudioPlayer.Play](/CIC/References/APIs/AudioPlayer.md#Play)
* [AudioPlayer.StreamDeliver](/CIC/References/APIs/AudioPlayer.md#StreamDeliver)
* [AudioPlayer.StreamRequested](/CIC/References/APIs/AudioPlayer.md#StreamRequested)
