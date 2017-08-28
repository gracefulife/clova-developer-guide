# PlaybackController

Plays audio and controls speaker output on a client. The PlaybackController API provides the following event and directive messages.

| Message name         | Message type  | Message description                                   |
|------------------|-----------|---------------------------------------------|
| [`Mute`](#Mute)                           | Directive | Instructs your client to mute its speaker volume.                    |
| [`Next`](#Next)                           | Directive | Instructs your client to start playback of a next audio stream in a playback queue.   |
| [`Pause`](#Pause)                         | Directive | Instructs your client to pause playback of a current audio stream.        |
| [`Previous`](#Previous)                   | Directive | Instructs your client to start playback of a previous audio stream in a playback queue. |
| [`Resume`](#Resume)                       | Directive | Instructs your client to resume playback of an audio stream.                |
| [`Stop`](#Stop)                           | Directive | Instructs your client to stop playback of an audio stream.                |
| [`TurnOffRepeatMode`](#TurnOffRepeatMode) | Directive | Instructs your client to turn off the single track repeat mode.                  |
| [`TurnOnRepeatMode`](#TurnOnRepeatMode)   | Directive | Instructs your client to turn on the single track repeat mode.                  |
| [`Unmute`](#Unmute)                       | Directive | Instructs your client to unmute its speaker volume.              |
| [`VolumeDown`](#VolumeDown)               | Directive | Instructs your client to turn down its speaker volume.                      |
| [`VolumeUp`](#VolumeUp)                   | Directive | Instructs your client to turn up its speaker volume.                      |

## Mute directive {#Mute}
Instructs your client to mute its speaker volume.

### Payload field
None

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
Instructs your client to start playback of a next audio stream in a playback queue.

### Payload field
None

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
Instructs your client to pause playback of a current audio stream.

### Payload field
None

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
Instructs your client to start playback of a previous audio stream in a playback queue.

### Payload field
None

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
Instructs your client to resume playback of an audio stream.

### Payload field
None

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
Instructs your client to stop playback of an audio stream.

### Payload field
None

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
 Instructs your client to turn off the single track repeat mode.

### Payload field
None

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
Instructs your client to turn on the single track repeat mode.

### Payload field
None

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
Instructs your client to unmute its speaker volume.

### Payload field
None

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
Instructs your client to turn down its speaker volume. The volume adjustment level is determined by your UX standard.

### Payload field
None

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
Instructs your client to turn up its speaker volume. The volume adjustment level is determined by your UX standard.

### Payload field
None

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