# SpeechSynthesizer

SpeechSynthesizer는 클라이언트가 특정 텍스트를 TTS(text-to-speech) 음성 파일로 합성되도록 CIC에 요청하거나, CIC가 합성된 음성 파일을 클라이언트에 전달할 때 사용되는 네임스페이스입니다. SpeechSynthesizer가 제공하는 이벤트 메시지와 지시 메시지는 다음과 같습니다.

| 메시지 이름         | 메시지 타입  | 메시지 설명                                   |
|------------------|-----------|---------------------------------------------|
| [`Request`](#Request) | Event     | CIC에 특정 텍스트를 TTS 음성 파일로 합성되도록 요청합니다. |
| [`Speak`](#Speak)     | Directive | 클라이언트에게 합성된 TTS 음성 파일을 스피커로 출력하도록 지시합니다. |


## Request event {#Request}

CIC에 특정 텍스트를 TTS 음성 파일로 합성되도록 요청합니다.

### Context field

필수 상태 정보 없음

### Payload field
| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|---------|
| `text`  | string | TTS 음성 합성을 요청할 대상 텍스트           | 필수    |
| `lang`  | string | 음성 합성에 사용할 언어. <ul><li><code>"ko"</code> : 한국어</li><li><code>"en"</code> : 영어</li><li><code>"ja"</code> : 일본어</li><li><code>"zh"</code> : 중국어</li></ul> | 필수    |

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
클라이언트에게 합성된 TTS 음성 파일을 스피커로 출력하도록 지시합니다. 클라이언트는 하나의 요청에 대한 응답으로 복수의 Speak 지시 메시지를 전달받을 수 있습니다. 따라서, 클라이언트는 메시지를 수신한 순서대로 음성 파일을 재생해야 합니다. 음성 파일은 [multipart 메시지](/CIC/References/CIC_API.md#MultipartMessage)로 전달될 수도 있고 오디오 스트리밍 주소 형태로 전달될 수도 있습니다.

### Payload field
| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|---------|
| `format`               | string  | 파일 포맷. 현재는 `"AUDIO_MPEG"`로 고정되어 있습니다. | 필수    |
| `url`                  | string  | 재생할 음성 파일의 URL                        | 필수    |
| `token`                | string  | TTS 파일을 식별하는 토큰 값                    | 필수    |
| `ttsLang`              | string  | 음성 합성에 사용할 언어. <ul><li><code>"ko"</code> : 한국어</li><li><code>"en"</code> : 영어</li><li><code>"ja"</code> : 일본어</li><li><code>"zh"</code> : 중국어</li></ul> | 선택    |
| `x-clova-pause-before` | number  | 파일 재생 전 유휴 시간. 정수 형태 값이며, 단위는 밀리초(millisecond)입니다.        | 선택    |

### Remarks

`url`은 아래와 같이 두 가지의 포맷을 가집니다. 클라이언트는 각 포맷에 따라 음성 출력 처리를 다음과 같이 다르게 해야 합니다.

| 포맷 | 설명 |
|---------|-------------------------------|
| `cid:{Content-ID}` 포맷 | 클라이언트의 `url` 값이 `cid:{Content-ID}` 포맷이면 합성된 음성이 multipart 메시지로 전달됩니다. 메시지 헤더 중 `Content-ID` 값이 같은 메시지의 오디오 데이터(바이너리 형식)을 재생해야 합니다. 오디오 데이터가 포함된 메시지는 순서가 보장되지 않기 때문에 전달된 지시 메시지의 `Content-ID` 값을 기준으로 음성 데이터를 출력합니다.|
| URL 포맷 | 전달받은 `url`의 오디오 스트림을 재생해야 합니다.  |

### Message example

{% raw %}
```
// cid:{Content-Id} 포맷
// Content-Id가 22f2ca4e-3b08-4d33-b32a-7eb62a8c0369인 오디오 데이터 메시지를 재생해야 합니다.

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


// URL 포맷
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
