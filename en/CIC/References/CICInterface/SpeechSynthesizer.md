# SpeechSynthesizer

The SpeechSynthesizer namespace provides interfaces to request CIC to synthesize text into a TTS (text-to-speech) audio file or to give a synthesized audio file to the client. SpeechSynthesizer provides the following events and directives.

| Message name         | Message type  | Description                                   |
|------------------|-----------|---------------------------------------------|
| [`Request`](#Request) | Event     | A message to request to CIC to synthesize a specified text into a TTS audio file. |
| [`Speak`](#Speak)     | Directive | Instructs a client to play the synthesized TTS audio file through the speaker. |


## Request event {#Request}

A message for requesting CIC to synthesize the given text into a TTS audio file.

### Context fields

None

### Payload fields

| Field name       | Type    | Description                     | Required |
|---------------|:---------:|-----------------------------|:---------:|
| `text`  | string | The text to synthesize into a speech.           | Required    |
| `lang`  | string | The language used for speech synthesis: <ul><li><code>"ko"</code>: Korean</li><li><code>"en"</code>: English</li><li><code>"ja"</code>: Japanese</li><li><code>"zh"</code>: Chinese</li></ul> | Required    |

### Message example

{% raw %}
```json
{
  "context": [],
  "event": {
    "header": {
      "namespace": "SpeechSynthesizer",
      "name": "Request",
      "messageId": "ab63d4cb-49f0-4a92-94fc-5ee356193551"
    },
    "payload": {
      "text": "Make me an audio file",
      "lang": "ko"
    }
  }
}
```
{% endraw %}

### See also

* [`SpeechSynthesizer.Speak`](/CIC/References/CICInterface/SpeechSynthesizer.md#Speak)

## Speak directive {#Speak}

Instructs a client to play the synthesized TTS audio file through the client's speaker. CIC can return multiple Speak directives in response to a single request. As such, your client must play audio files in the same order it has received messages. Audio files can be returned either in a [multipart message](/CIC/References/CIC_API.md#MultipartMessage) or an audio streaming address.

### Payload fields

| Field name       | Type    | Description                     | Provided |
|---------------|:---------:|-----------------------------|:---------:|
| `format`               | string  | The file format of the TTS audio file. The value is always `"AUDIO_MPEG"`. | Always |
| `url`                  | string  | The URL of the TTS audio file to play.                        | Always |
| `token`                | string  | The ID of the given TTS audio file.                    | Always |
| `ttsLang`              | string  | The language used for speech synthesis. <ul><li><code>"ko"</code>: Korean</li><li><code>"en"</code>: English</li><li><code>"ja"</code>: Japanese</li><li><code>"zh"</code>: Chinese</li></ul> | Conditional |
| `x-clova-pause-before` | number  | The idle time before playing the TTS audio. The value is an Integer and the unit is millisecond.        | Conditional |

### Remarks

The `url` field can be in either one of the following two formats. Process the audio according to the specified format.

| Format | Description |
|---------|-------------------------------|
| `cid:{Content-ID}` | The synthesized audio is returned as a multipart message. Play the audio data (binary type) that has the same `Content-ID` message header. Since messages containing audio data are not received sequentially, play audio data based on the `Content-ID` of the directives received. |
| URL | Play the audio stream specified by the `url` provided.  |

### Message example

{% raw %}
```
// cid:{Content-Id} format
// Play the audio data with the Content-Id 22f2ca4e-3b08-4d33-b32a-7eb62a8c0369

--Boundary-Text
Content-Disposition: form-data; name="speakDirective1"
Content-Type: application/json; charset=utf-8

{
  "directive": {
    "header": {
      "namespace": "SpeechSynthesizer",
      "name": "Speak",
      "messageId": "29745c13-0d70-408e-a4cc-946afba67524",
      "dialogRequestId": "caa7862a-3566-4aef-98de-489be0973e18"
    },
    "payload": {
      "format": "AUDIO_MPEG",
      "token": "cbba5103-8ce4-4e65-869b-f94d5878f579",
      "ttsLang": "ko",
      "url": "cid:22f2ca4e-3b08-4d33-b32a-7eb62a8c0369",
      "x-clova-pause-before": 0
    }
  }
}

--Boundary-Text
Content-Disposition: form-data; name="attachment"
Content-Id: 22f2ca4e-3b08-4d33-b32a-7eb62a8c0369
Content-Type: application/octet-stream

{ Audio Attachment }
--Boundary-Text--


// URL format
--Boundary-Text
{
  "directive": {
    "header": {
      "namespace": "SpeechSynthesizer",
      "name": "Speak",
      "messageId": "0313b471-ad7f-4cdd-b4e1-c046ca8b4b58",
      "dialogRequestId": "efa43b14-67f4-4f00-86bc-dfa08a08ad0b"
    },
    "payload": {
      "format": "AUDIO_MPEG",
      "token": "64ffeb07-4b86-4659-9f59-07a77b363a0b",
      "url": "https://ssl.pstatic.net/static/clova/service/clova_song/1.mp3"
    }
  }
}
--Boundary-Text--
```

{% endraw %}

### See also

* [`SpeechSynthesizer.Request`](/CIC/References/CICInterface/SpeechSynthesizer.md#Request)
