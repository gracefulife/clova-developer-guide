# PlaybackController

Plays audio and controls speaker output on a client. PlaybackController provides the following event and directive messages.

| Message name         | Message type  | Message description                                   |
|------------------|-----------|---------------------------------------------|
| [`Mute`](#Mute)                           | Directive | Instructs your client to mute the audio player.            |
| [`Next`](#Next)                           | Directive | Instructs your client to start playback of a next audio stream in a playback queue.   |
| [`NextCommandIssued`](#NextCommandIssued) | Event     | The client should send this event message to CIC when the user clicked or touched the 'Next' button on the client device. |
| [`Pause`](#Pause)                         | Directive | Instructs your client to pause playback of a current audio stream.        |
| [`Previous`](#Previous)                   | Directive | Instructs your client to start playback of a previous audio stream in a playback queue. |
| [`PreviousCommandIssued`](#PreviousCommandIssued) | Event | The client should send this event message to CIC when the user clicked or touched the 'Previous' button on the client device. |
| [`Replay`](#Replay)                       | Directive | Instructs your client to replay the audio stream from the beginning.         |
| [`Resume`](#Resume)                       | Directive | Instructs your client to resume playback of an audio stream.                |
| [`Stop`](#Stop)                           | Directive | Instructs your client to stop playback of an audio stream.                |
| [`TurnOffRepeatMode`](#TurnOffRepeatMode) | Directive | Instructs your client to turn off the single track repeat mode.                  |
| [`TurnOnRepeatMode`](#TurnOnRepeatMode)   | Directive | Instructs your client to turn on the single track repeat mode.                  |
| [`Unmute`](#Unmute)                       | Directive | Instructs your client to unmute the audio player volume.              |
| [`VolumeDown`](#VolumeDown)               | Directive | Instructs your client to turn down the audio player volume.                      |
| [`VolumeUp`](#VolumeUp)                   | Directive | Instructs your client to turn up the audio player volume.                      |

## Mute directive {#Mute}
Instructs your client to mute the audio player. The client should mute the speaker volume related to the audio stream playback after receiving this directive message.

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
* [`SpeechRecognizer.Recognize`](/CIC/References/CICInterface/SpeechRecognizer.md#Recognize)

## Next directive {#Next}
Instructs your client to start playback of a next audio stream in a playback queue. The client should play the audio stream upon receiving this directive message.

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
* [`SpeechRecognizer.Recognize`](/CIC/References/CICInterface/SpeechRecognizer.md#Recognize)

## NextCommandIssued event {#NextCommandIssued}
The client should send this event message to CIC when the user clicked or touched the 'Next' button on the client device. Clova should carry out necessary actions depending on the client's situations. For instance, if the client was using extensions such as podcast, Clova should process an action to make the client play the next content instantly.

### Context field

There is no required state information

### Payload field

None

### Remarks
* The button on the client device can either be a physical button in hardware method or in software method such as a widget button on music player.

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
Instructs your client to pause playback of a current audio stream. The client should pause playback of the audio stream upon receiving this directive message.

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
* [`AudioPlayer.PlayPaused`](/CIC/References/CICInterface/AudioPlayer.md#PlayPaused)
* [`SpeechRecognizer.Recognize`](/CIC/References/CICInterface/SpeechRecognizer.md#Recognize)

## Previous directive {#Previous}
Instructs your client to start playback of a previous audio stream in a playback queue. The client should play the previous audio stream upon receiving this directive message.

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
* [`SpeechRecognizer.Recognize`](/CIC/References/CICInterface/SpeechRecognizer.md#Recognize)


## PreviousCommandIssued event {#PreviousCommandIssued}
The client should send this event message to CIC when the user clicked or touched the 'Previous' button on the client device. Clova should carry out necessary actions depending on the client's situations. For instance, if the client was using extensions such as podcast, Clova should process an action to make the client play the previous content instantly.

### Context field

There is no required state information

### Payload field

None

### Remarks
* The button on the client device can either be a physical button in hardware method or in software method such as a widget button on music player.

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
Instructs your client to replay the audio stream from the beginning. The client should replace the playback location to the beginning part of the audio stream after receiving this directive message. Start the audio stream instantly after the replacement. If the audio stream playback is paused, it should be resumed.

### Payload field
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
Instructs your client to resume playback of an audio stream. The client should resume playback of the audio stream upon receiving this directive message.

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
* [`AudioPlayer.PlayResumed`](/CIC/References/CICInterface/AudioPlayer.md#PlayResumed)
* [`SpeechRecognizer.Recognize`](/CIC/References/CICInterface/SpeechRecognizer.md#Recognize)

## Stop directive {#Stop}
Instructs your client to stop playback of an audio stream. The client should stop playback of the audio stream upon receiving this directive message.

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
* [`AudioPlayer.PlayStopped`](/CIC/References/CICInterface/AudioPlayer.md#PlayStopped)
* [`SpeechRecognizer.Recognize`](/CIC/References/CICInterface/SpeechRecognizer.md#Recognize)

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
* [`SpeechRecognizer.Recognize`](/CIC/References/CICInterface/SpeechRecognizer.md#Recognize)

## TurnOnRepeatMode directive {#TurnOnRepeatMode}
Instructs your client to turn on the single track repeat mode. The client should repeatedly play the current playbakck of audio stream upon receiving this directive message.

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
* [`SpeechRecognizer.Recognize`](/CIC/References/CICInterface/SpeechRecognizer.md#Recognize)

## Unmute directive {#Unmute}
Instructs your client to unmute the audio player volume. The client should replace the volume level to where it was before the mute upon receiving this directive message.

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
* [`SpeechRecognizer.Recognize`](/CIC/References/CICInterface/SpeechRecognizer.md#Recognize)

## VolumeDown directive {#VolumeDown}
Instructs your client to turn down the audio player. The client should turn down the speaker volume related to the audio stream playback after receiving this directive message. The volume adjustment level is determined by your UX standard.

<div class="note">
  <p><strong>Note!</strong></p>
  <p>A <code>PlaybackController.VolumeDown</code> directive message will no longer be provided.  It is recommended to use a <a href="/CIC/References/CICInterface/DeviceControl.html#Decrease"><code>DiviceControl.Decrease</code></a> directive message instead.</p>
</div>

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
* [`SpeechRecognizer.Recognize`](/CIC/References/CICInterface/SpeechRecognizer.md#Recognize)

## VolumeUp directive {#VolumeUp}

Instructs your client to turn up the audio player. The client should turn up the speaker volume related to the audio stream playback after receiving this directive message. The volume adjustment level is determined by your UX standard.

<div class="note">
  <p><strong>Note!</strong></p>
  <p>A <code>PlaybackController.VolumeUp</code> directive message will no longer be provided. It is recommended to use a <a href="/CIC/References/CICInterface/DeviceControl.html#Increase"><code>DiviceControl.Increase</code></a> directive message instead.</p>
</div>

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
* [`SpeechRecognizer.Recognize`](/CIC/References/CICInterface/SpeechRecognizer.md#Recognize)