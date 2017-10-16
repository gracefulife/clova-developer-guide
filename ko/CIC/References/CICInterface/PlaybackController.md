# PlaybackController

PlaybackController은 클라이언트의 오디오 재생 및 스피커 출력을 제어할 때 사용되는 네임스페이스입니다. PlaybackController가 제공하는 이벤트 메시지와 지시 메시지는 다음과 같습니다.

| 메시지 이름         | 메시지 타입  | 메시지 설명                                   |
|------------------|-----------|---------------------------------------------|
| [`Mute`](#Mute)                           | Directive | 클라이언트에게 오디오 플레이어의 볼륨을 음소거하도록 지시합니다.            |
| [`Next`](#Next)                           | Directive | 클라이언트에게 재생 대기열에 있는 다음 오디오 스트림 재생하도록 지시합니다.   |
| [`NextCommandIssued`](#NextCommandIssued) | Event     | 사용자가 클라이언트의 기기에서 다음(Next)에 해당하는 버튼 누르거나 터치한 경우 클라이언트는 이 이벤트 메시지를 CIC에게 전송해야 합니다. |
| [`Pause`](#Pause)                         | Directive | 클라이언트에게 재생 중인 오디오 스트림을 일시 정지하도록 지시합니다.        |
| [`Previous`](#Previous)                   | Directive | 클라이언트에게 재생 대기열에 있는 이전 오디오 스트림을 재생하도록 지시합니다. |
| [`PreviousCommandIssued`](#PreviousCommandIssued) | Event | 사용자가 클라이언트의 기기에서 이전(Previous)에 해당하는 버튼 누르거나 터치한 경우 클라이언트는 이 이벤트 메시지를 CIC에게 전송해야 합니다. |
| [`Replay`](#Replay)                       | Directive | 클라이언트에게 오디오 스트림을 처음부터 다시 재생하도록 지시합니다.         |
| [`Resume`](#Resume)                       | Directive | 클라이언트에게 오디오 스트림 재생을 재개하도록 지시합니다.                |
| [`Stop`](#Stop)                           | Directive | 클라이언트에게 오디오 스트림 재생을 중지하도록 지시합니다.                |
| [`TurnOffRepeatMode`](#TurnOffRepeatMode) | Directive | 클라이언트에게 한곡 반복 재생 모드를 끄도록 지시합니다.                  |
| [`TurnOnRepeatMode`](#TurnOnRepeatMode)   | Directive | 클라이언트에게 한곡 반복 재생 모드를 켜도록 지시합니다.                  |
| [`Unmute`](#Unmute)                       | Directive | 클라이언트에게 오디오 플레이어 볼륨의 음소거를 해제하도록 지시합니다.              |
| [`VolumeDown`](#VolumeDown)               | Directive | 클라이언트에게 오디오 플레이어 볼륨을 낮추도록 지시합니다.                      |
| [`VolumeUp`](#VolumeUp)                   | Directive | 클라이언트에게 오디오 플레이어 볼륨을 높이도록 지시합니다.                      |

## Mute directive {#Mute}
클라이언트에게 오디오 플레이어 볼륨을 음소거하도록 지시합니다. 클라이언트는 이 지시 메시지를 받은 후 오디오 스트림 재생과 관련된 스피커 볼륨을 무음이 되도록 변경해야 합니다.

### Payload field
없음

### Message example
{% raw %}
```json
{
    "directive": {
        "header": {
            "namespace": "PlaybackController",
            "name": "Mute",
            "dialogRequestId": "dialog-id-here-1",
            "messageId": "b1f88d7d-bbb8-44fa-a0a2-c5a7553e6f8a"
        },
        "payload": {}
    }
}
```
{% endraw %}

### See also
* [`Speaker.VolumeState`](/CIC/References/Context_Objects.md#VolumeState)
* [`SpeechRecognizer.Recognize`](/CIC/References/CICInterface/SpeechRecognizer.md#Recognize)

## Next directive {#Next}
클라이언트에게 재생 대기열에 있는 다음 오디오 스트림 재생하도록 지시합니다. 클라이언트는 이 지시 메시지를 받은 후 다음 오디오 스트림을 재생해야 합니다.

### Payload field
없음

### Message example
{% raw %}
```json
{
    "directive": {
        "header": {
            "namespace": "PlaybackController",
            "name": "Next",
            "dialogRequestId": "dialog-id-here-1",
            "messageId": "b1f88d7d-bbb8-44fa-a0a2-c5a7553e6f8a"
        },
        "payload": {}
    }
}
```
{% endraw %}

### See also
* [`SpeechRecognizer.Recognize`](/CIC/References/CICInterface/SpeechRecognizer.md#Recognize)

## NextCommandIssued event {#NextCommandIssued}
사용자가 클라이언트의 기기에서 다음(Next)에 해당하는 버튼 누르거나 터치한 경우 클라이언트는 이 이벤트 메시지를 CIC에게 전송해야 합니다. Clova는 클라이언트의 상황에 따라 필요한 동작을 수행해줍니다. 예를 들어, 클라이언트가 팟캐스트와 같은 extension을 사용하고 있었다면 Clova는 즉각 다음 콘텐츠를 재생할 수 있도록 처리해줍니다.

### Context field

필수 상태 정보 없음

### Payload field

없음

### Remarks
* 클라이언트 기기의 버튼은 물리적인 하드웨어 방식의 버튼일 수도 있고 음악 플레이어 위젯 버튼과 같은 소프트웨어 방식의 버튼일 수도 있습니다.

### Message example

{% raw %}

```json
{
  "context": [],
  "event": {
    "header": {
      "namespace": "PlaybackController",
      "name": "NextCommandIssued",
      "messageId": "4e4080d6-c440-498a-bb73-ae86c6312806"
    },
    "payload": {}
  }
}
```
{% endraw %}

### See also
* [`PalybackController.PreviousCommandIssued`](#PreviousCommandIssued)

## Pause directive {#Pause}
클라이언트에게 재생 중인 오디오 스트림을 일시 정지하도록 지시합니다. 클라이언트는 이 지시 메시지를 받은 후 오디오 스트림 재생을 일시 정지해야 합니다.

### Payload field
없음

### Message example
{% raw %}
```json
{
    "directive": {
        "header": {
            "namespace": "PlaybackController",
            "name": "Pause",
            "dialogRequestId": "dialog-id-here-1",
            "messageId": "b1f88d7d-bbb8-44fa-a0a2-c5a7553e6f8a"
        },
        "payload": {}
    }
}
```
{% endraw %}

### See also
* [`AudioPlayer.PlayPaused`](/CIC/References/CICInterface/AudioPlayer.md#PlayPaused)
* [`SpeechRecognizer.Recognize`](/CIC/References/CICInterface/SpeechRecognizer.md#Recognize)

## Previous directive {#Previous}
클라이언트에게 재생 대기열에 있는 이전 오디오 스트림을 재생하도록 지시합니다. 클라이언트는 이 지시 메시지를 받은 후 이전 오디오 스트림을 재생해야 합니다.

### Payload field
없음

### Message example
{% raw %}
```json
{
    "directive": {
        "header": {
            "namespace": "PlaybackController",
            "name": "Previous",
            "dialogRequestId": "dialog-id-here-1",
            "messageId": "b1f88d7d-bbb8-44fa-a0a2-c5a7553e6f8a"
        },
        "payload": {}
    }
}
```
{% endraw %}

### See also
* [`Speaker.VolumeState`](/CIC/References/Context_Objects.md#VolumeState)
* [`SpeechRecognizer.Recognize`](/CIC/References/CICInterface/SpeechRecognizer.md#Recognize)


## PreviousCommandIssued event {#PreviousCommandIssued}
사용자가 클라이언트의 기기에서 이전(Previous)에 해당하는 버튼 누르거나 터치한 경우 클라이언트는 이 이벤트 메시지를 CIC에게 전송해야 합니다. Clova는 클라이언트의 상황에 따라 필요한 동작을 수행해줍니다. 예를 들어, 클라이언트가 팟캐스트와 같은 extension을 사용하고 있었다면 Clova는 즉각 이전 콘텐츠를 재생할 수 있도록 처리해줍니다.

### Context field

필수 상태 정보 없음

### Payload field

없음

### Remarks
* 클라이언트 기기의 버튼은 물리적인 하드웨어 방식의 버튼일 수도 있고 음악 플레이어 위젯 버튼과 같은 소프트웨어 방식의 버튼일 수도 있습니다.

### Message example

{% raw %}

```json
{
  "context": [],
  "event": {
    "header": {
      "namespace": "PlaybackController",
      "name": "PreviousCommandIssued",
      "messageId": "4e4080d6-c440-498a-bb73-ae86c6312806"
    },
    "payload": {}
  }
}
```
{% endraw %}

### See also
* [`PalybackController.NextCommandIssued`](#NextCommandIssued)

## Replay directive {#Replay}
클라이언트에게 오디오 스트림을 처음부터 다시 재생하도록 지시합니다. 클라이언트는 이 지시 메시지를 받은 후 재생 위치를 오디오 스트림의 처음으로 이동시켜야 하며, 이동시킨 후 바로 오디오 스트림 재생을 시작해야 합니다. 만약 오디오 스트림 재생이 일시 정지(paused)되어 있었다면 오디오 스트림 재생을 재개(resume)해야 합니다.

### Payload field
없음

### Message example
{% raw %}
```json
{
    "directive": {
        "header": {
            "namespace": "PlaybackController",
            "name": "Replay",
            "dialogRequestId": "dialog-id-here-1",
            "messageId": "b1f88d7d-bbb8-44fa-a0a2-c5a7553e6f8a"
        },
        "payload": {}
    }
}
```
{% endraw %}

### See also
* [`PlaybackController.Pause`](#Pause)
* [`PlaybackController.Resume`](#Resume)
* [`SpeechRecognizer.Recognize`](/CIC/References/CICInterface/SpeechRecognizer.md#Recognize)

## Resume directive {#Resume}
클라이언트에게 오디오 스트림 재생을 재개하도록 지시합니다. 클라이언트는 이 지시 메시지를 받은 후 오디오 스트림 재생을 재개해야 합니다.

### Payload field
없음

### Message example
{% raw %}
```json
{
    "directive": {
        "header": {
            "namespace": "PlaybackController",
            "name": "Resume",
            "dialogRequestId": "dialog-id-here-1",
            "messageId": "b1f88d7d-bbb8-44fa-a0a2-c5a7553e6f8a"
        },
        "payload": {}
    }
}
```
{% endraw %}

### See also
* [`AudioPlayer.PlayResumed`](/CIC/References/CICInterface/AudioPlayer.md#PlayResumed)
* [`SpeechRecognizer.Recognize`](/CIC/References/CICInterface/SpeechRecognizer.md#Recognize)

## Stop directive {#Stop}
클라이언트에게 오디오 스트림 재생을 중지하도록 지시합니다. 클라이언트는 이 지시 메시지를 받은 후 오디오 스트림 재생을 중지해야 합니다.

### Payload field
없음

### Message example
{% raw %}
```json
{
    "directive": {
        "header": {
            "namespace": "PlaybackController",
            "name": "Stop",
            "dialogRequestId": "dialog-id-here-1",
            "messageId": "b1f88d7d-bbb8-44fa-a0a2-c5a7553e6f8a"
        },
        "payload": {}
    }
}
```
{% endraw %}

### See also
* [`AudioPlayer.PlayStopped`](/CIC/References/CICInterface/AudioPlayer.md#PlayStopped)
* [`SpeechRecognizer.Recognize`](/CIC/References/CICInterface/SpeechRecognizer.md#Recognize)

## TurnOffRepeatMode directive {#TurnOffRepeatMode}
 클라이언트에게 한곡 반복 재생 모드를 끄도록 지시합니다.

### Payload field
없음

### Message example
{% raw %}
```json
{
    "directive": {
        "header": {
            "namespace": "PlaybackController",
            "name": "TurnOffRepeatMode",
            "dialogRequestId": "dialog-id-here-1",
            "messageId": "b1f88d7d-bbb8-44fa-a0a2-c5a7553e6f8a"
        },
        "payload": {}
    }
}
```
{% endraw %}

### See also
* [`SpeechRecognizer.Recognize`](/CIC/References/CICInterface/SpeechRecognizer.md#Recognize)

## TurnOnRepeatMode directive {#TurnOnRepeatMode}
클라이언트에게 한곡 반복 재생 모드를 켜도록 지시합니다. 클라이언트는 이 지시 메시지를 받은 후 현재 재생 중인 오디오 스트림을 계속 반복 재생해야 합니다.

### Payload field
없음

### Message example
{% raw %}
```json
{
    "directive": {
        "header": {
            "namespace": "PlaybackController",
            "name": "TurnOnRepeatMode",
            "dialogRequestId": "dialog-id-here-1",
            "messageId": "b1f88d7d-bbb8-44fa-a0a2-c5a7553e6f8a"
        },
        "payload": {}
    }
}
```
{% endraw %}

### See also
* [`SpeechRecognizer.Recognize`](/CIC/References/CICInterface/SpeechRecognizer.md#Recognize)

## Unmute directive {#Unmute}
클라이언트에게 오디오 플레이어 볼륨의 음소거를 해제하도록 지시합니다. 클라이언트는 이 지시 메시지를 받은 후 무음으로 설정했던 스피커 볼륨을 원래 크기로 되돌려야 합니다.

### Payload field
없음

### Message example
{% raw %}
```json
{
    "directive": {
        "header": {
            "namespace": "PlaybackController",
            "name": "Unmute",
            "dialogRequestId": "dialog-id-here-1",
            "messageId": "b1f88d7d-bbb8-44fa-a0a2-c5a7553e6f8a"
        },
        "payload": {}
    }
}
```
{% endraw %}

### See also
* [`Speaker.VolumeState`](/CIC/References/Context_Objects.md#VolumeState)
* [`SpeechRecognizer.Recognize`](/CIC/References/CICInterface/SpeechRecognizer.md#Recognize)

## VolumneDown directive {#VolumeDown}
클라이언트에게 오디오 플레이어 볼륨을 낮추도록 지시합니다. 클라이언트는 이 지시 메시지를 받은 후 오디오 스트림 재생과 관련된 스피커 볼륨을 낮춰야 합니다. 볼륨을 낮추는 정도는 각 클라이언트의 UX 기준을 따릅니다.

### Payload field
없음

### Message example
{% raw %}
```json
{
    "directive": {
        "header": {
            "namespace": "PlaybackController",
            "name": "VolumeDown",
            "dialogRequestId": "dialog-id-here-1",
            "messageId": "b1f88d7d-bbb8-44fa-a0a2-c5a7553e6f8a"
        },
        "payload": {}
    }
}
```
{% endraw %}

### See also
* [`Speaker.VolumeState`](/CIC/References/Context_Objects.md#VolumeState)
* [`SpeechRecognizer.Recognize`](/CIC/References/CICInterface/SpeechRecognizer.md#Recognize)

## VolumneUp directive {#VolumeUp}
클라이언트에게 오디오 플레이어 볼륨을 높이도록 지시합니다. 클라이언트는 이 지시 메시지를 받은 후 오디오 스트림 재생과 관련된 스피커 볼륨을 높여야 합니다. 볼륨을 올리는 정도는 각 클라이언트의 UX 기준을 따릅니다.

### Payload field
없음

### Message example
{% raw %}
```json
{
    "directive": {
        "header": {
            "namespace": "PlaybackController",
            "name": "VolumeUp",
            "dialogRequestId": "dialog-id-here-1",
            "messageId": "b1f88d7d-bbb8-44fa-a0a2-c5a7553e6f8a"
        },
        "payload": {}
    }
}
```
{% endraw %}

### See also
* [`Speaker.VolumeState`](/CIC/References/Context_Objects.md#VolumeState)
* [`SpeechRecognizer.Recognize`](/CIC/References/CICInterface/SpeechRecognizer.md#Recognize)
