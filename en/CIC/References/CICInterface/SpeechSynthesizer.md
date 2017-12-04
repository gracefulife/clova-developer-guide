# SpeechSynthesizer

Requests CIC to synthesize text into a TTS (text-to-speech) audio file or returns a synthesized audio file to your client. SpeechSynthesizer provides the following event and directive messages.

| Message name         | Message type  | Message description                                   |
|------------------|-----------|---------------------------------------------|
| [`Request`](#Request) | Event     | Requests CIC to synthesize specified text into a TTS audio file. |
| [`Speak`](#Speak)     | Directive | Instructs your client to play the synthesized TTS audio file through the speaker. |


## Request event {#Request}

Requests CIC to synthesize specified text into a TTS audio file.

### Context field

There is no required state information

### Payload field
| Field name       | Type    | Field description                     | Required |
|---------------|---------|-----------------------------|---------|
| `text`  | string | The text to synthesize into TTS           | Yes    |
| `lang`  | string | The language used for speech synthesis. <ul><li><code>"ko"</code>: Korean</li><li><code>"en"</code>: English</li><li><code>"ja"</code>: Japanese</li><li><code>"zh"</code>: Chinese</li></ul> | Yes    |

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
      "text": "음성파일 만들어줘",
      "lang": "ko"
    }
  }
}
```
{% endraw %}

### See also
* [`SpeechSynthesizer.Speak`](/CIC/References/CICInterface/SpeechSynthesizer.md#Speak)

## Speak directive {#Speak}
Instructs your client to play the synthesized TTS audio file through the speaker. It can return multiple Speak directive messages in response to a single request. As such, your client must play audio files in the same order it has received messages. Audio files can be returned either in a [multipart message](/CIC/References/CIC_API.md#MultipartMessage) or an audio streaming address.

### Payload field
| Field name       | Type    | Field description                     | Required |
|---------------|---------|-----------------------------|---------|
| `format`               | string  | The file format. Currently returns `"AUDIO_MPEG"`. | Yes    |
| `url`                  | string  | The URL of the audio file to play                        | Yes    |
| `token`                | string  | A token for identifying the TTS file                    | Yes    |
| `ttsLang`              | string  | The language used for speech synthesis. <ul><li><code>"ko"</code>: Korean</li><li><code>"en"</code>: English</li><li><code>"ja"</code>: Japanese</li><li><code>"zh"</code>: Chinese</li></ul> | No    |
| `x-clova-pause-before` | number  | Idle time before playing the file. The value is in integer form and the unit is millisecond.        | No    |

### Remarks

The `url` can be either one of the two formats. Process audio output appropriately for each format.

| Format | Description |
|---------|-------------------------------|
| `cid:{Content-ID}` format | If the format of the `url` is `cid:{Content-ID}`, the synthesized audio is returned in a multipart message. You must play audio data (binary type) that has the same `Content-ID` message header. Since messages that contain audio data are not returned sequentially, you must play audio data based on the `Content-ID` of the directive messages returned. |
| URL format | Play the audio stream from the `url` returned.  |

### Message example

{% raw %}
```
// cid:{Content-Id} format
// Plays an audio data message with Content-Id 22f2ca4e-3b08-4d33-b32a-7eb62a8c0369

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
