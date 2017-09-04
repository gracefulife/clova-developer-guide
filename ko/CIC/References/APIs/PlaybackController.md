# PlaybackController

PlaybackController은 클라이언트의 오디오 재생 및 스피커 출력을 제어할 때 사용되는 네임스페이스입니다. PlaybackController가 제공하는 이벤트 메시지와 지시 메시지는 다음과 같습니다.

| 메시지 이름         | 메시지 타입  | 메시지 설명                                   |
|------------------|-----------|---------------------------------------------|
| [`Mute`](#Mute)                           | Directive | 클라이언트에게 스피커 볼륨을 음소거하도록 지시합니다.                    |
| [`Next`](#Next)                           | Directive | 클라이언트에게 재생 대기열에 있는 다음 오디오 스트림 재생하도록 지시합니다.   |
| [`Pause`](#Pause)                         | Directive | 클라이언트에게 재생 중인 오디오 스트림을 일시 정지하도록 지시합니다.        |
| [`Previous`](#Previous)                   | Directive | 클라이언트에게 재생 대기열에 있는 이전 오디오 스트림을 재생하도록 지시합니다. |
| [`Resume`](#Resume)                       | Directive | 클라이언트에게 오디오 스트림 재생을 재개하도록 지시합니다.                |
| [`Stop`](#Stop)                           | Directive | 클라이언트에게 오디오 스트림 재생을 중지하도록 지시합니다.                |
| [`TurnOffRepeatMode`](#TurnOffRepeatMode) | Directive | 클라이언트에게 한곡 반복 재생 모드를 끄도록 지시합니다.                  |
| [`TurnOnRepeatMode`](#TurnOnRepeatMode)   | Directive | 클라이언트에게 한곡 반복 재생 모드를 켜도록 지시합니다.                  |
| [`Unmute`](#Unmute)                       | Directive | 클라이언트에게 스피커 볼륨의 음소거를 해제하도록 지시합니다.              |
| [`VolumeDown`](#VolumeDown)               | Directive | 클라이언트에게 스피커 볼륨을 낮추도록 지시합니다.                      |
| [`VolumeUp`](#VolumeUp)                   | Directive | 클라이언트에게 스피커 볼륨을 높이도록 지시합니다.                      |

## Mute directive {#Mute}
클라이언트에게 스피커 볼륨을 음소거하도록 지시합니다.

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
* [`SpeechRecognizer.Recognize`](/CIC/References/APIs/SpeechRecognizer.md#Recognize)

## Next directive {#Next}
클라이언트에게 재생 대기열에 있는 다음 오디오 스트림 재생하도록 지시합니다.

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
* [`SpeechRecognizer.Recognize`](/CIC/References/APIs/SpeechRecognizer.md#Recognize)

## Pause directive {#Pause}
클라이언트에게 재생 중인 오디오 스트림을 일시 정지하도록 지시합니다.

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
* [`AudioPlayer.PlayPaused`](/CIC/References/APIs/AudioPlayer.md#PlayPaused)
* [`SpeechRecognizer.Recognize`](/CIC/References/APIs/SpeechRecognizer.md#Recognize)

## Previous directive {#Previous}
클라이언트에게 재생 대기열에 있는 이전 오디오 스트림을 재생하도록 지시합니다.

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
* [`SpeechRecognizer.Recognize`](/CIC/References/APIs/SpeechRecognizer.md#Recognize)

## Resume directive {#Resume}
클라이언트에게 오디오 스트림 재생을 재개하도록 지시합니다.

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
* [`AudioPlayer.PlayResumed`](/CIC/References/APIs/AudioPlayer.md#PlayResumed)
* [`SpeechRecognizer.Recognize`](/CIC/References/APIs/SpeechRecognizer.md#Recognize)

## Stop directive {#Stop}
클라이언트에게 오디오 스트림 재생을 중지하도록 지시합니다.

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
* [`AudioPlayer.PlayStopped`](/CIC/References/APIs/AudioPlayer.md#PlayStopped)
* [`SpeechRecognizer.Recognize`](/CIC/References/APIs/SpeechRecognizer.md#Recognize)

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
* [`SpeechRecognizer.Recognize`](/CIC/References/APIs/SpeechRecognizer.md#Recognize)

## TurnOnRepeatMode directive {#TurnOnRepeatMode}
클라이언트에게 한곡 반복 재생 모드를 켜도록 지시합니다.

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
* [`SpeechRecognizer.Recognize`](/CIC/References/APIs/SpeechRecognizer.md#Recognize)

## Unmute directive {#Unmute}
클라이언트에게 스피커 볼륨의 음소거를 해제하도록 지시합니다.

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
* [`SpeechRecognizer.Recognize`](/CIC/References/APIs/SpeechRecognizer.md#Recognize)

## VolumneDown directive {#VolumeDown}
클라이언트에게 스피커 볼륨을 낮추도록 지시합니다. 볼륨을 낮추는 정도는 각 클라이언트의 UX 기준을 따릅니다.

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
* [`SpeechRecognizer.Recognize`](/CIC/References/APIs/SpeechRecognizer.md#Recognize)

## VolumneUp directive {#VolumeUp}
클라이언트에게 스피커 볼륨을 높이도록 지시합니다. 볼륨을 올리는 정도는 각 클라이언트의 UX 기준을 따릅니다.

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
* [`SpeechRecognizer.Recognize`](/CIC/References/APIs/SpeechRecognizer.md#Recognize)
