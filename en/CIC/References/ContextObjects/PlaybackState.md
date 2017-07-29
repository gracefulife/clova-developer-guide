## AudioPlayer.PlaybackState {#PlaybackState}
PlaybackState is a message format that contains information of media currently playing or previously played. This information can be sent to an [extension](/CEK/References/Custom_Extension_Message_Format.md) that provides a music streaming service.

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

| Field name       | Type    | Field description                     | Required |
|---------------|---------|-----------------------------|---------|
| offsetInMilliseconds | number | Recently played media's last playback point (offset). Unit is millisecond. You can leave the field empty when *playerActivity* is "IDLE".                                                  | No |
| playerActivity       | string | Indicates a player state. Available values are:<ul><li>"IDLE": In an idle state</li><li>"PLAYING": In a playing state</li><li>"PAUSED": In a paused state</li><li>"STOPPED": In a stopped state</li></ul> | Yes |
| stream               | [AudioStreamObject](/CIC/References/APIs/AudioPlayer.md#AudioStreamObject) | An object that contains details of media currently playing. You can leave the field empty when *playerActivity* is "IDLE". Enter media details (*stream* object) returned from [AudioPlayer.Play](/CIC/References/APIs/AudioPlayer.md#Play) or [AudioPlayer.StreamDelivered](/CIC/References/APIs/AudioPlayer.md#StreamDelivered) directive message. | No |
| totalInMilliseconds  | number | Total length of the media recently played. Unit is millisecond. You can leave the field empty when *playerActivity* is "IDLE".                                                               | No |

### Message example
#### Example 1: When playback has stopped
{% raw %}
```json
// Case 1: When playback has stopped
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
* [AudioPlayer.Play](/CIC/References/APIs/AudioPlayer.md#Play)
* [AudioPlayer.StreamDeliver](/CIC/References/APIs/AudioPlayer.md#StreamDeliver)
* [AudioPlayer.StreamRequested](/CIC/References/APIs/AudioPlayer.md#StreamRequested)