# PlaybackController

The PlaybackController namespace provides interfaces for playing audio and controlling sound on a client. The PlaybackController namespace provides the following events and directives.

| Message name         | Message type  | Message description                                   |
|------------------|-----------|---------------------------------------------|
| [`Mute`](#Mute)                           | Directive | Instructs a client to mute the audio player.            |
| [`Next`](#Next)                           | Directive | Instructs a client to start playing the next audio stream in the playback queue.   |
| [`NextCommandIssued`](#NextCommandIssued) | Event     | A message to notify CIC that the user has pressed the 'Next' button on the client device. |
| [`Pause`](#Pause)                         | Directive | Instructs a client to pause playing the current audio stream.        |
| [`Previous`](#Previous)                   | Directive | Instructs a client to start playing the previous audio stream in the playback queue. |
| [`PreviousCommandIssued`](#PreviousCommandIssued) | Event | A message to notify CIC that the user has pressed the 'Previous' button on the client device. |
| [`Replay`](#Replay)                       | Directive | Instructs a client to replay the audio stream from the beginning.         |
| [`Resume`](#Resume)                       | Directive | Instructs a client to resume playing the audio stream.                |
| [`Stop`](#Stop)                           | Directive | Instructs a client to stop playing the audio stream.                |
| [`TurnOffRepeatMode`](#TurnOffRepeatMode) | Directive | Instructs a client to turn off repeat for a single track.                  |
| [`TurnOnRepeatMode`](#TurnOnRepeatMode)   | Directive | Instructs a client to turn on repeat for a single track.                  |
| [`Unmute`](#Unmute)                       | Directive | Instructs a client to unmute the audio player.              |
| [`VolumeDown`](#VolumeDown)               | Directive | Instructs a client to turn down the audio player's volume.                      |
| [`VolumeUp`](#VolumeUp)                   | Directive | Instructs a client to turn up the audio player's volume.                      |

## Mute directive {#Mute}

Instructs a client to mute the audio player. Upon receiving this directive, the client must mute the speaker for the audio stream playback.

### Payload fields

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
* [`SpeechRecognizer.Recognize`](/CIC/References/CICInterface/SpeechRecognizer.md#Recognize)

## Next directive {#Next}

Instructs a client to start playing the next audio stream in the playback queue. Upon receiving this directive, the client must play the next audio stream in the queue.

### Payload fields

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

* [`SpeechRecognizer.Recognize`](/CIC/References/CICInterface/SpeechRecognizer.md#Recognize)

## NextCommandIssued event {#NextCommandIssued}

A message for reporting to CIC that the user has pressed the 'Next' button on the client device. Clova will handle the user's action based on the client's state. For instance, if the client was using an extension such as Podcast, Clova will take an action to make the client play the next podcast instantly.

### Context fields

Send the following [context information](/CIC/References/Context_Objects.md) with this event.

* [`AudioPlayer.PlaybackState`](/CIC/References/Context_Objects.md#PlaybackState)

### Payload fields

None

### Remarks

* The button on the client device can either be a physical button or a software button like a widget button on a music player.

### Message example

{% raw %}

```json
{
  "context": [
    {{AudioPlayer.PlaybackState}}
  ],
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

* [`PlaybackController.PreviousCommandIssued`](#PreviousCommandIssued)
* [`AudioPlayer.PlaybackState`](/CIC/References/Context_Objects.md#PlaybackState)

## Pause directive {#Pause}

Instructs a client to pause playing the current audio stream. Upon receiving this directive, the client must pause playing.


### Payload fields

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

* [`AudioPlayer.PlayPaused`](/CIC/References/CICInterface/AudioPlayer.md#PlayPaused)
* [`SpeechRecognizer.Recognize`](/CIC/References/CICInterface/SpeechRecognizer.md#Recognize)

## Previous directive {#Previous}

Instructs a client to start playing the previous audio stream in the playback queue. Upon receiving this directive, the client must play the previous audio stream.

### Payload fields

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
* [`SpeechRecognizer.Recognize`](/CIC/References/CICInterface/SpeechRecognizer.md#Recognize)

## PreviousCommandIssued event {#PreviousCommandIssued}

A message for notifying CIC that the user has pressed the 'Previous' button on the client device. Clova will handle the user's action based on the client's state. For instance, if the client was using an extension such as Podcast, Clova will take an action to make the client play the previous podcast instantly.

### Context fields

Send the following [context information](/CIC/References/Context_Objects.md) with this event.

* [`AudioPlayer.PlaybackState`](/CIC/References/Context_Objects.md#PlaybackState)

### Payload fields

None

### Remarks

* The button on the client device can either be a physical button or a software button like a widget button on a music player.

### Message example

{% raw %}

```json
{
  "context": [
    {{AudioPlayer.PlaybackState}}
  ],
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

* [`PlaybackController.NextCommandIssued`](#NextCommandIssued)
* [`AudioPlayer.PlaybackState`](/CIC/References/Context_Objects.md#PlaybackState)

## Replay directive {#Replay}

Instructs a client to replay the current audio stream from the beginning. Upon receiving this directive, the client must play the currently playing audio stream from the beginning. If playing had been paused, then resume playing the audio stream.

### Payload fields

None

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

Instructs a client to resume playing paused audio stream. Upon receiving this directive, the client must resume playing the audio stream.

### Payload fields

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

* [`AudioPlayer.PlayResumed`](/CIC/References/CICInterface/AudioPlayer.md#PlayResumed)
* [`SpeechRecognizer.Recognize`](/CIC/References/CICInterface/SpeechRecognizer.md#Recognize)

## Stop directive {#Stop}

Instructs a client to stop playing an audio stream. When The client should stop playback of the audio stream upon receiving this directive message.

### Payload fields
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

* [`AudioPlayer.PlayStopped`](/CIC/References/CICInterface/AudioPlayer.md#PlayStopped)
* [`SpeechRecognizer.Recognize`](/CIC/References/CICInterface/SpeechRecognizer.md#Recognize)

## TurnOffRepeatMode directive {#TurnOffRepeatMode}

Instructs a client to stop repeating a song.

### Payload fields

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

* [`SpeechRecognizer.Recognize`](/CIC/References/CICInterface/SpeechRecognizer.md#Recognize)

## TurnOnRepeatMode directive {#TurnOnRepeatMode}

Instructs a client to repeat a song. After receiving this directive, repeat playing the currently played audio stream.

### Payload fields

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

* [`SpeechRecognizer.Recognize`](/CIC/References/CICInterface/SpeechRecognizer.md#Recognize)

## Unmute directive {#Unmute}

Instructs a client to unmute the audio player. Restore the volume level to the level before the player had been muted.

### Payload fields

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
* [`SpeechRecognizer.Recognize`](/CIC/References/CICInterface/SpeechRecognizer.md#Recognize)

## VolumeDown directive {#VolumeDown}

Instructs a client to turn down the volume of the audio player. Upon receiving this directive, the client must turn down the volume of the audio player. The volume adjustment level depends on the client's UX standard.

<div class="note">
  <p><strong>Note!</strong></p>
  <p>The <code>PlaybackController.VolumeDown</code> directive is to be deprecated. Use the <a href="/CIC/References/CICInterface/DeviceControl.html#Decrease"><code>DeviceControl.Decrease</code></a> directive instead.</p>
</div>

### Payload fields

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
* [`SpeechRecognizer.Recognize`](/CIC/References/CICInterface/SpeechRecognizer.md#Recognize)

## VolumeUp directive {#VolumeUp}

Instructs a client to turn up the volume of the audio player. Upon receiving this directive, the client must turn up the volume of the audio player. The volume adjustment level depends on the client's UX standard.

<div class="note">
  <p><strong>Note!</strong></p>
  <p>The <code>PlaybackController.VolumeUp</code> directive is to be deprecated. Use the <a href="/CIC/References/CICInterface/DeviceControl.html#Decrease"><code>DeviceControl.Increase</code></a> directive instead.</p>
</div>

### Payload fields

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
* [`SpeechRecognizer.Recognize`](/CIC/References/CICInterface/SpeechRecognizer.md#Recognize)
