## AudioPlayer.PlaybackState {#PlaybackState}
PlaybackState는 현재 재생하고 있거나 마지막으로 재생한 미디어 정보를 가지는 메시지 포맷입니다. 이 정보는 추후 음악 서비스를 제공하는 [extension으로 전달](/CEK/References/Custom_Extension_Message_Format.md)될 수 있습니다.

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

| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|---------|
| offsetInMilliseconds | number | 최근 재생 미디어의 마지막 재생 지점(offset). 단위는 밀리초이며, *playerActivity* 값이 "IDLE"이면 이 필드 값은 입력하지 않아도 됩니다.                                                  | 선택 |
| playerActivity       | string | 플레이어의 상태를 나타내는 값이며 다음과 같은 값을 가집니다.<ul><li>"IDLE": 비활성 상태</li><li>"PLAYING": 재생 중인 상태</li><li>"PAUSED": 일시 정지 상태</li><li>"STOPPED": 중지 상태</li></ul> | 필수 |
| stream               | [AudioStreamObject](/CIC/References/APIs/AudioPlayer.md#AudioStreamObject) | 재생 중인 미디어의 상세 정보를 보관한 객체. *playerActivity* 값이 "IDLE"이면 이 필드 값은 입력하지 않아도 됩니다. [AudioPlayer.Play](/CIC/References/APIs/AudioPlayer.md#Play) 또는 [AudioPlayer.StreamDelivered](/CIC/References/APIs/AudioPlayer.md#StreamDelivered) 지시 메시지로 전달되었던 미디어 정보(*stream* 객체)의 값을 입력합니다. | 선택 |
| totalInMilliseconds  | number | 최근 재생 미디어의 전체 길이. 단위는 밀리초이며, *playerActivity* 값이 "IDLE"이면 이 필드 값은 입력하지 않아도 됩니다.                                                               | 선택 |

### Message example
#### 예제 1: 재생이 중지된 상태
{% raw %}
```json
// Case 1: 재생이 중지된 상태
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

#### 예제 2: 플레이어가 비활성화된 상태
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
