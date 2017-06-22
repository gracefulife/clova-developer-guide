# SpeechSynthesizer

This API is used when your client asks CIC to synthesize texts into a TTS (text-to-speech) audio file or when CIC delivers a synthesized audio file to your client. This API provides the following Event and Directive messages.

| Message name  | Message type  | Message description  |
|------------------|-----------|---------------------------------------------|
| [Request](#Request) | Event  | Asks CIC to synthesize texts into a TTS audio file. |
| [Speak](#Speak)  | Directive | Instructs your client to play the synthesized TTS audio file with its speaker. |


## Request Event {#Request}

Asks CIC to synthesize texts into a TTS audio file.

### Context field

None

### Payload field
| Field name  | Type  | Field description  | Required |
|---------------|---------|-----------------------------|---------|
| text  | string | The text to be converted to TTS  | Yes  |
| lang  | string | The language used for speech synthesis. <ul><li>"ko": Korean</li><li>"en": English</li><li>"ja": Japanese</li><li>"zh": Chinese</li></ul> | Yes  |

### Message example
{% raw %}
```json
{
  "context": [],
  "event": {
    "header": {
      "namespace": "SpeechSynthesizer",
      "name": "Request",
      "dialogRequestId": "caa7862a-3566-4aef-98de-489be0973e18",
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
* [SpeechSynthesizer.Speak](/CIC/References/APIs/SpeechSynthesizer.md#Speak)

## Speak Directive {#Speak}
Instructs your client to play a synthesized TTS audio file with its speaker. Your client may receive multiple Speak Directive messages in response to a single request. As such, your client must play the audio files in the same order it received the messages. Audio files can be delivered either using an [HTTP multipart message](/CIC/References/HTTP2_Message_Format.md#MultipartMessage) or using an audio streaming address.

### Payload field
| Field name  | Type  | Field description  | Required |
|---------------|---------|-----------------------------|---------|
| format  | string  | File format. The value is currently fixed to "AUDIO_MPEG". | Yes  |
| url  | string  | The URL of the audio file to play  | Yes  |
| token  | string  | The token value that identifies the TTS file  | Yes  |
| ttsLang  | string  | The language used for speech synthesis. <ul><li>"ko": Korean</li><li>"en": English</li><li>"ja": Japanese</li><li>"zh": Chinese</li></ul> | No  |
| ttsText  | string  | The TTS text in the synthesized file  | No  |
| x-clova-pause-before | integer | Idle time before playing the file. Unit is a millisecond.  | No  |

### Remarks

The *url* can be presented in two formats. Your client should process audio output differently depending on the format.

| Format | Description |
|---------|-------------------------------|
| cid:{Content-Id} format | When the *url* value is of cid:{Content-Id} format, the synthesized audio is delivered using a multipart message. And the audio data (binary format) whose message header has the same *Content-Id* should be played. Messages that contain audio data are not delivered sequentially. Thus, audio data should be played based on the Content-ID value of the Directive message.|
| URL format | The audio stream of the *url* should be played.  |

### Message example

{% raw %}
```
// cid:{Content-Id} format
// Plays the audio data message whose Content-Id is 22f2ca4e-3b08-4d33-b32a-7eb62a8c0369.

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
      "ttsText": "음성파일 만들어줘",
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
* [SpeechSynthesizer.Request](/CIC/References/APIs/SpeechSynthesizer.md#Request)