# HTTP/2 메시지
CIC와 연동할 때 [HTTP/2 프로토콜](https://tools.ietf.org/html/rfc7540)을 사용합니다. 클라이언트가 CIC로 전송하는 HTTP/2 메시지 구조는 다음 그림과 같습니다.

![](/CIC/Resources/Images/HTTP2_Structure.png)

여기에서는 다음에 대해 설명합니다.
* [HTTP 요청](#request)
  * [CIC base URL](#BaseURL)
  * [HTTP 헤더](#Header)
  * [Multipart 메시지](#MultipartMessage)
* [HTTP 응답](#Response)
* [HTTP 메시지 예제](#MessageExample)

## HTTP 요청 {#Request}
주로 클라이언트가 CIC로 사용자의 요청을 전달할 때 HTTP 요청을 사용하며, 이벤트 메시지를 HTTP 요청으로 보냅니다.

### CIC base URL {#BaseURL}
Clova는 아래 URL을 base URL로 사용합니다.

{% raw %}
```
https://prod-ni-cic.clova.ai/
```
{% endraw %}

### HTTP 헤더 {#Header}
CIC와 연결할 때 다음과 같은 필드가 HTTP 헤더로 필요합니다.

{% raw %}
```
:method = {{GET|POST}}
:scheme = https
:path = /{{API Version}}/{{events|directives}}
Authorization = Bearer {{Clova access token}}
Content-Type = multipart/form-data; boundary={{boundary_term}}
```
{% endraw %}

| 필드 이름          | 메시지 설명                                    |
|------------------|---------------------------------------------|
| :method        | CIC는 다음과 같은 메서드를 지원합니다. <ul><li><code>GET</code> : <a href="/CIC/Guides/Interact_with_CIC.html#CreateConnection">Downchannel</a> 생성 시 사용</li><li><code>POST</code> : <a href="/CIC/References/CIC_Message_Format.html#Event">이벤트 메시지</a>를 보낼 때 사용</li></ul> |
| :scheme        | CIC API는 https 통신을 지원합니다.                                                                            |
| :path          | 각각 다음 경로를 사용합니다. <ul><li><code>/v1/directives</code> : <a href="/CIC/Guides/Interact_with_CIC.html#CreateConnection">Downchannel</a> 생성 시 사용</li><li><code>/v1/events</code> : <a href="/CIC/References/CIC_Message_Format.html#Event">이벤트 메시지</a>를 보낼 때 사용</li></ul> |
| authorization  | Clova 인증 서버를 통해 획득한 인증 토큰을 입력합니다. 인증 토큰은 모든 요청의 헤더에 포함되어 있어야 합니다.                     |

## Multipart 메시지 {#MultipartMessage}
클라이언트는 HTTP/2를 이용해 [이벤트 메시지](/CIC/References/CIC_Message_Format.md#Event)를 주로 multipart 메시지로 전송하게 됩니다.

예를 들면, 사용자의 음성 입력을 CIC로 전달하려면 [SpeechRecognizer.Recognize](/CIC/References/APIs/SpeechRecognizer.md#Recognize) 이벤트 메시지와 함께 녹음한 사용자의 음성 데이터를 함께 전송해야 합니다. 클라이언트는 `Content-Type`을 **multipart/form-data**로 설정하고 첫 번째 메시지 블록에는 이벤트 메시지 정보가 담긴 JSON 데이터를 두 번째 메시지 블록에는 사용자의 음성이 담긴 바이너리 데이터를 담아서 보낼 수 있습니다.

이때, 메시지를 구분하기 위해 `boundary`에 경계 문구를 지정해야 합니다. 경계 문구는 메시지 블록 사이에 사용될 경우 경계 문구 왼쪽에 이중의 하이픈(-) 기호를 붙여야 하며, 마지막 메시지 블록 이후에는 경계 문구 양쪽에 이중의 하이픈(-) 기호를 붙여야 합니다. 또한, 경계 문구는 각 메시지 블록의 본문에서 나타나지 않아야 합니다.

다음은 클라이언트가 CIC로 사용자 요청을 이벤트 메시지를 보낼 때 갖추게 되는 일반적인 메시지 형태입니다.

{% raw %}
```
:method = POST
:scheme = https
:path = /v1/events
authorization = Bearer {{clova-access-token}}
Content-Type = multipart/form-data; boundary=this-is-boundary-text

--this-is-boundary-text
[ Message Header ]
Content-Disposition: form-data; name="metadata"
Content-Type: application/json; charset=UTF-8

[ Message Body ]
{
  "context": [
  ],
  "event": {
    "header": {
      "namespace": "{{string}}",
      "name": {{string}},
      "dialogRequestId": {{string}},
      "messageId": {{string}}
    },
    "payload": {{object}}
  }
}

--this-is-boundary-text
[ Message Header ]
Content-Disposition: form-data; name="audio"
Content-Type: application/octet-stream

[ PCM Audio Attachment ]
{{ Binary audio attachment }}

--this-is-boundary-text--

```
{% endraw %}

<div class="note">
  <p><strong>Note!</strong></p>
  <p><a href="/CIC/Guides/Interact_with_CIC.md#CreateConnection">Downchannel 생성</a>을 위해 <code>/v1/directives</code>에 HTTP 요청을 보낼 때는 별도의 메시지를 보내지 않기 때문에 <code>Content-Type</code>을 설정할 필요가 없습니다. 이와 같이 <code>Content-Type</code>은 상황에 맞게 작성하면 됩니다.</p>
</div>

## HTTP 응답 {#Response}
HTTP 응답은 CIC로부터 지시 메시지를 전달하거나 오류 메시지를 전달합니다. 일반적인 응답은 성공을 의미하는 [HTTP 상태 코드](https://tools.ietf.org/html/rfc7231#section-6)(200)와 함께 [지시 메시지](/CIC/References/CIC_Message_Format.md#Directive)가 전달되며, 다음과 같은 메시지 조합을 가집니다.
* [`Synthesizer.Speak`](/CIC/References/APIs/SpeechSynthesizer.md#Speak)은 음성을 출력하는 지시 메시지로 음성 데이터가 추가로 전달됩니다.
* `Synthesizer.Speak` 지시 메시지와 함께 부가 정보를 전달하는 지시 메시지가 전달될 수 있습니다. 예를 들면, 스트리밍 정보를 포함하고 있는 [`AudioPlayer.Play`](/CIC/References/APIs/AudioPlayer.md#Play) 지시 메시지가 추가로 전달될 수 있습니다.

위 설명과 같이 CIC에서 클라이언트로 전달되는 응답도 복수의 지시 메시지와 음성 데이터로 조합된 [multipart 메시지](#MultipartMessage)가 전달됩니다. 다음과 같은 구조를 가집니다.

{% raw %}
```
HTTP/2 {{HTTP STATUS CODE}}
Content-Type: multipart/related; boundary=this-is-boundary-text;
date: {{DATETIME}}

--this-is-boundary-text
[ Message Header ]
Content-Disposition: form-data; name="metadata"
Content-Type: application/json; charset=UTF-8

[ Message Body ]
{
  "directive": {
    "header": {
      "namespace": "{{string}}",
      "name": {{string}},
      "dialogRequestId": {{string}},
      "messageId": {{string}}
    },
    "payload": {{object}}
  }
}

--this-is-boundary-text
[ Message Header ]
Content-Disposition: form-data; name="audio"
Content-Type: application/octet-stream

[ PCM Audio Attachment ]
{{ Binary audio attachment }}

--this-is-boundary-text

...

--this-is-boundary-text--

```
{% endraw %}

**사용자 요청을 전달할 때 요청 형식이 잘못되었거나 내부 서버 오류가 발생한 경우** 오류 상황에 해당하는 [HTTP 상태 코드](https://tools.ietf.org/html/rfc7231#section-6)(4XX 또는 5XX)와 함께 [오류 메시지](/CIC/References/CIC_Message_Format.md#Error)가 전달됩니다. 이 경우 하나의 메시지 블록이 전달되지만 `Content-Type`은 **multipart/form-data**를 사용합니다. 오류 메시지는 다음과 같은 구조를 가집니다.

{% raw %}
```
HTTP/2 400
Content-Type: multipart/related; boundary=this-is-boundary-text;
date: Thu, 03 Aug 2017 01:23:14 GMT

--this-is-boundary-text
Content-Disposition: form-data; name="metadata"
Content-Type: application/json; charset=UTF-8

{
  "header": {
    "namespace": "System",
    "name": "Exception",
    "messageId": {{string}}
  },
  "payload": {{object}
}
--this-is-boundary-text--
```
{% endraw %}

## HTTP 메시지 예제 {#MessageExample}
다음은 클라이언트와 CIC 사이에서 주고 받은 실제 HTTP 요청/응답 메시지입니다.

### Request Example
{% raw %}
```
POST /v1/events HTTP/2
Host: https://prod-ni-cic.clova.ai/
Accept: */*
Authorization: Bearer {{clova-access-token}}
> Content-Length: 456
> Content-Type: multipart/form-data; boundary=920d6335ba920d6337a319f

--920d6335ba920d6337a319f
Content-Disposition: form-data; name="metadata"
Content-Type: application/json; charset=UTF-8

{
  "context": [
    {
      "header": {
        "namespace": "Speaker",
        "name": "VolumeState"
      },
      "payload": {
        "volume": 25,
        "muted": false
      }
    }
  ],
  "event": {
    "header": {
      "namespace": "SpeechRecognizer",
      "name": "Recognize",
      "messageId": "277b40c3-b046-4f61-a551-783b1547e7b7",
      "dialogRequestId": "4e4080d6-c440-498a-bb73-ae86c6312806"
    },
    "payload": {
      "profile": "CLOSE_TALK"
    }
  }
}

--920d6335ba920d6337a319f
Content-Disposition: form-data; name="audio"
Content-Type: application/octet-stream

{{binary audio attachment}}
--920d6335ba920d6337a319f--

```
{% endraw %}

### Response Example - 요청 성공
{% raw %}
```
HTTP/2 200
Content-Type: multipart/related; boundary=b4bc211bbd32e5cb5989bc7ab2d3088fdd72dcc6696253151c98176f88ba;
date: Fri, 04 Aug 2017 05:27:12 GMT

--b4bc211bbd32e5cb5989bc7ab2d3088fdd72dcc6696253151c98176f88ba
Content-Disposition: form-data; name="speakDirective-836d8db7-5e72-4fb2-9834-7c59291e1f8e"
Content-Type: application/json; charset=utf-8

{
  "directive":{
    "header":{
      "namespace":"SpeechSynthesizer",
      "name":"Speak",
      "messageId":"dd4d463e-85a3-4514-927e-c90103c2dd02",
      "dialogRequestId":"dialog-id-here-1"
    },
    "payload":{
      "format":"AUDIO_MPEG",
      "token":"e81f7dec-63fb-453d-8bd8-6944bed9a306",
      "ttsLang":"ko",
      "ttsText":"만나서 반가워요",
      "url":"cid:d329085c-379e-48aa-b871-7ecebdbe831d",
      "x-clova-pause-before":0
    }
  }
}

--b4bc211bbd32e5cb5989bc7ab2d3088fdd72dcc6696253151c98176f88ba
Content-Disposition: form-data; name="attachment-39b2f844-b168-4dc2-bea7-d5c249e446e3"
Content-Id: d329085c-379e-48aa-b871-7ecebdbe831d
Content-Type: application/octet-stream

{{binary audio attachment}}

--b4bc211bbd32e5cb5989bc7ab2d3088fdd72dcc6696253151c98176f88ba
Content-Disposition: form-data; name="renderTextDirective-b2c92b0f-27af-4f5c-b7e7-af7a270c464b"
Content-Type: application/json; charset=utf-8

{
  "directive":{
    "header":{
      "namespace":"Clova",
      "name":"RenderText",
      "messageId":"0fa1b36f-e86c-4979-9494-b00a162c4515",
      "dialogRequestId":"dialog-id-here-1"
    },
    "payload":{
      "text":"만나서 반가워요"
    }
  }
}

--b4bc211bbd32e5cb5989bc7ab2d3088fdd72dcc6696253151c98176f88ba--
```
{% endraw %}

### Response Example - 요청 실패
{% raw %}
```
HTTP/2 400
content-type: multipart/related; boundary=883fd3b825c9b883f99b9ffb4d2a2cbd7a24c9c61bfa69d70c51140f34ca;
date: Fri, 04 Aug 2017 09:42:46 GMT

--883fd3b825c9b883f99b9ffb4d2a2cbd7a24c9c61bfa69d70c51140f34ca
Content-Disposition: form-data; name="exception-bde71903-dab4-46c5-9714-416cf12debf0"
Content-Type: application/json; charset=utf-8

{
  "header": {
    "namespace": "System",
    "name": "Exception",
    "messageId": "369b362b-258c-4104-bdf8-dc276548fe51"
  },
  "payload": {
    "code": 400,
    "description": "Could not decode multipart"
  }
}
--883fd3b825c9b883f99b9ffb4d2a2cbd7a24c9c61bfa69d70c51140f34ca--
```
{% endraw %}
