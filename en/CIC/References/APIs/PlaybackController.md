# PlaybackController

Plays audio and controls speaker output on a client.

<div class="note">
  <p><strong>Note!</strong></p>
  <p>The PlaybackController was deprecated and is not supported any more. All the APIs which used to be provided by this namespace will be migrated to the <a href="/CIC/References/APIs/AudioPlayer.html">AudioPlayer</a> namespace.</p>
</div>

The PlaybackController API provides the following event and directive messages.

| Message name         | Message type  | Message description                                   |
|------------------|-----------|---------------------------------------------|
| [mute](#mute)                           | Directive | Instructs your client to mute speaker volume.                    |
| [next](#next)                           | Directive | Instructs your client to start playback of a next audio stream in a playback queue.   |
| [pause](#pause)                         | Directive | Instructs your client to pause playback of a current audio stream.        |
| [previous](#previous)                   | Directive | Instructs your client to start playback of a previous audio stream in a playback queue. |
| [resume](#resume)                       | Directive | Instructs your client to resume playback of an audio stream.                |
| [stop](#stop)                           | Directive | Instructs your client to stop playback of an audio stream.                |
| [TurnOffRepeatMode](#TurnOffRepeatMode) | Directive | Instructs your client to turn off single track repeat mode.                  |
| [TurnOnRepeatMode](#TurnOnRepeatMode)   | Directive | Instructs your client to turn on single track repeat mode.                  |
| [unmute](#unmute)                       | Directive | Instructs your client to unmute speaker volume.              |
| [volumeDown](#volumeDown)               | Directive | Instructs your client to turn down speaker volume.                      |
| [volumeUp](#volumeUp)                   | Directive | Instructs your client to turn up speaker volume.                      |

## mute directive {#mute}
Instructs your client to mute speaker volume.

### Payload field
None

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
 Instructs your client to turn off single track repeat mode.

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
* [SpeechRecognizer.Recognize](/CIC/References/APIs/SpeechRecognizer.md#Recognize)

## TurnOnRepeatMode directive {#TurnOnRepeatMode}
Instructs your client to turn on single track repeat mode.

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
* [SpeechRecognizer.Recognize](/CIC/References/APIs/SpeechRecognizer.md#Recognize)

## unmute directive {#unmute}
Instructs your client to unmute speaker volume.

### Payload field
None

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
Instructs your client to turn down speaker volume. The volume adjustment level is determined by your UX standard.

### Payload field
None

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
Instructs your client to turn up speaker volume. The volume adjustment level is determined by your UX standard.

### Payload field
None

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