# PlaybackController

클라이언트의 오디오 재생 및 스피커 출력을 제어할 때 사용되는 API입니다.

<div class="note">
  <p><strong>Note!</strong></p>
  <p>PlaybackController 네임스페이스는 내부적으로 지원 중지 결정(Deprecated)을 내렸고 더 이상 제공하지 않을 예정입니다. 이 네임스페이스에서 제공하던 API는 추후 <a href="/CIC/References/APIs/AudioPlayer.html">AudioPlayer</a> 네임스페이스에서 제공될 예정입니다.</p>
</div>

이 PlaybackController API가 제공하는 이벤트 메시지와 지시 메시지는 다음과 같습니다.

| 메시지 이름         | 메시지 타입  | 메시지 설명                                   |
|------------------|-----------|---------------------------------------------|
| [mute](#mute)                           | Directive | 클라이언트에게 스피커 볼륨을 음소거하도록 지시합니다.                    |
| [next](#next)                           | Directive | 클라이언트에게 재생 대기열에 있는 다음 오디오 스트림 재생하도록 지시합니다.   |
| [pause](#pause)                         | Directive | 클라이언트에게 재생 중인 오디오 스트림을 일시 정지하도록 지시합니다.        |
| [previous](#previous)                   | Directive | 클라이언트에게 재생 대기열에 있는 이전 오디오 스트림을 재생하도록 지시합니다. |
| [resume](#resume)                       | Directive | 클라이언트에게 오디오 스트림 재생을 재개하도록 지시합니다.                |
| [stop](#stop)                           | Directive | 클라이언트에게 오디오 스트림 재생을 중지하도록 지시합니다.                |
| [TurnOffRepeatMode](#TurnOffRepeatMode) | Directive | 클라이언트에게 한곡 반복 재생 모드를 끄도록 지시합니다.                  |
| [TurnOnRepeatMode](#TurnOnRepeatMode)   | Directive | 클라이언트에게 한곡 반복 재생 모드를 켜도록 지시합니다.                  |
| [unmute](#unmute)                       | Directive | 클라이언트에게 스피커 볼륨의 음소거를 해제하도록 지시합니다.              |
| [volumeDown](#volumeDown)               | Directive | 클라이언트에게 스피커 볼륨을 낮추도록 지시합니다.                      |
| [volumeUp](#volumeUp)                   | Directive | 클라이언트에게 스피커 볼륨을 높이도록 지시합니다.                      |

## mute directive {#mute}
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
            "name": "mute",
            "dialogRequestId": "dialog-id-here-1",
            "messageId": "b1f88d7d-bbb8-44fa-a0a2-c5a7553e6f8a"
        },
        "payload": {}
    }
}
```
{% endraw %}

### See also
* [Speaker.VolumeState](/CIC/References/Context_Objects.md#VolumeState)
* [SpeechRecognizer.Recognize](/CIC/References/APIs/SpeechRecognizer.md#Recognize)

## next directive {#next}
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
            "name": "next",
            "dialogRequestId": "dialog-id-here-1",
            "messageId": "b1f88d7d-bbb8-44fa-a0a2-c5a7553e6f8a"
        },
        "payload": {}
    }
}
```
{% endraw %}

### See also
* [AudioPlayer.PlayNext](/CIC/References/APIs/AudioPlayer.md#PlayNext)
* [SpeechRecognizer.Recognize](/CIC/References/APIs/SpeechRecognizer.md#Recognize)

## pause directive {#pause}
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
            "name": "pause",
            "dialogRequestId": "dialog-id-here-1",
            "messageId": "b1f88d7d-bbb8-44fa-a0a2-c5a7553e6f8a"
        },
        "payload": {}
    }
}
```
{% endraw %}

### See also
* [AudioPlayer.PlayPaused](/CIC/References/APIs/AudioPlayer.md#PlayPaused)
* [SpeechRecognizer.Recognize](/CIC/References/APIs/SpeechRecognizer.md#Recognize)

## previous directive {#previous}
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
            "name": "previous",
            "dialogRequestId": "dialog-id-here-1",
            "messageId": "b1f88d7d-bbb8-44fa-a0a2-c5a7553e6f8a"
        },
        "payload": {}
    }
}
```
{% endraw %}

### See also
* [Speaker.VolumeState](/CIC/References/Context_Objects.md#VolumeState)
* [SpeechRecognizer.Recognize](/CIC/References/APIs/SpeechRecognizer.md#Recognize)

## resume directive {#resume}
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
            "name": "resume",
            "dialogRequestId": "dialog-id-here-1",
            "messageId": "b1f88d7d-bbb8-44fa-a0a2-c5a7553e6f8a"
        },
        "payload": {}
    }
}
```
{% endraw %}

### See also
* [AudioPlayer.PlayResumed](/CIC/References/APIs/AudioPlayer.md#PlayResumed)
* [SpeechRecognizer.Recognize](/CIC/References/APIs/SpeechRecognizer.md#Recognize)

## stop directive {#stop}
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
            "name": "stop",
            "dialogRequestId": "dialog-id-here-1",
            "messageId": "b1f88d7d-bbb8-44fa-a0a2-c5a7553e6f8a"
        },
        "payload": {}
    }
}
```
{% endraw %}

### See also
* [AudioPlayer.PlayStopped](/CIC/References/APIs/AudioPlayer.md#PlayStopped)
* [SpeechRecognizer.Recognize](/CIC/References/APIs/SpeechRecognizer.md#Recognize)

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
* [SpeechRecognizer.Recognize](/CIC/References/APIs/SpeechRecognizer.md#Recognize)

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
* [SpeechRecognizer.Recognize](/CIC/References/APIs/SpeechRecognizer.md#Recognize)

## unmute directive {#unmute}
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
            "name": "unmute",
            "dialogRequestId": "dialog-id-here-1",
            "messageId": "b1f88d7d-bbb8-44fa-a0a2-c5a7553e6f8a"
        },
        "payload": {}
    }
}
```
{% endraw %}

### See also
* [Speaker.VolumeState](/CIC/References/Context_Objects.md#VolumeState)
* [SpeechRecognizer.Recognize](/CIC/References/APIs/SpeechRecognizer.md#Recognize)

## volumneDown directive {#volumeDown}
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
            "name": "volumeDown",
            "dialogRequestId": "dialog-id-here-1",
            "messageId": "b1f88d7d-bbb8-44fa-a0a2-c5a7553e6f8a"
        },
        "payload": {}
    }
}
```
{% endraw %}

### See also
* [Speaker.VolumeState](/CIC/References/Context_Objects.md#VolumeState)
* [SpeechRecognizer.Recognize](/CIC/References/APIs/SpeechRecognizer.md#Recognize)

## volumneUp directive {#volumeUp}
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
            "name": "volumeUp",
            "dialogRequestId": "dialog-id-here-1",
            "messageId": "b1f88d7d-bbb8-44fa-a0a2-c5a7553e6f8a"
        },
        "payload": {}
    }
}
```
{% endraw %}

### See also
* [Speaker.VolumeState](/CIC/References/Context_Objects.md#VolumeState)
* [SpeechRecognizer.Recognize](/CIC/References/APIs/SpeechRecognizer.md#Recognize)
