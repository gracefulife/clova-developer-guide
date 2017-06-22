# PlaybackController

This API lets your client control audio playback and speaker output.

<div class="note">
  <p><strong>Note!</strong></p>
  <p>The PlaybackController was deprecated and is not supported any more. All the APIs which used to be provided by this namespace will be migrated to the <a href="/CIC/References/APIs/AudioPlayer.html">AudioPlayer</a> namespace in the future.</p>
</div>

The PlaybackController API provides the following Event and Directive messages.

| Message name  | Message type  | Message description  |
|------------------|-----------|---------------------------------------------|
| [mute](#mute)  | Directive | Instructs your client to mute the speaker volume.  |
| [next](#next)  | Directive | Instructs your client to start playback of the next audio stream in a playback queue.  |
| [pause](#pause)  | Directive | Instructs your client to pause playback of the current audio stream.  |
| [previous](#previous)  | Directive | Instructs your client to start playback the previous audio stream in a playback queue. |
| [resume](#resume)  | Directive | Instructs your client to resume playback of the audio stream.  |
| [stop](#stop)  | Directive | Instructs your client to stop playback of the audio stream.  |
| [TurnOffRepeatMode](#TurnOffRepeatMode) | Directive | Instructs your client to turn off the repeat mode.  |
| [TurnOnRepeatMode](#TurnOnRepeatMode)  | Directive | Instructs your client to turn on the repeat mode.  |
| [unmute](#unmute)  | Directive | Instructs your client to unmute the speaker volume.  |
| [volumeDown](#volumeDown)  | Directive | Instructs your client to turn down the speaker volume.  |
| [volumeUp](#volumeUp)  | Directive | Instructs your client to turn up the speaker volume.  |

## mute Directive {#mute}
Instructs your client to mute the speaker volume.

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

## next Directive {#next}
Instructs your client to start playback of the next audio stream in a playback queue.

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

## pause Directive {#pause}
Instructs your client to pause playback of the current audio stream.

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

## previous Directive {#previous}
Instructs your client to start playback of the previous audio stream in a playback queue.

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

## resume Directive {#resume}
Instructs your client to resume playback of the audio stream.

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

## stop Directive {#stop}
Instructs your client to stop playback of the audio stream.

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

## TurnOffRepeatMode Directive {#TurnOffRepeatMode}
 Instructs your client to turn off the repeat mode.

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

## TurnOnRepeatMode Directive {#TurnOnRepeatMode}
Instructs your client to turn on the repeat mode.

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

## unmute Directive {#unmute}
Instructs your client to unmute the speaker volume.

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

## volumneDown Directive {#volumeDown}
Instructs your client to turn down the speaker volume. The volume adjustment level is determined by the UX standard of each client.

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

## volumneUp Directive {#volumeUp}
Instructs your client to turn up the speaker volume. The volume adjustment level is determined by the UX standard of each client.

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
