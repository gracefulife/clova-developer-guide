# HTTP/2 메시지
CIC와 연동할 때 [HTTP/2 프로토콜](https://tools.ietf.org/html/rfc7540)을 사용합니다. 클라이언트가 CIC로 전송하는 HTTP/2 메시지 구조는 다음 그림과 같습니다.

![](/CIC/Resources/Images/HTTP2_Structure.png)

여기에서는 다음에 대해 설명합니다.
* [HTTP 요청](#request)
  * [CIC base URL](#BaseURL)
  * [HTTP 헤더](#Header)
  * [HTTP multipart 메시지](#MultipartMessage)
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
content-type = multipart/form-data; boundary={{boundary_term}}
```
{% endraw %}

| 필드 이름          | 메시지 설명                                    |
|------------------|---------------------------------------------|
| :method        | CIC는 다음과 같은 메서드를 지원합니다. <ul><li>GET: <a href="/CIC/Guides/Interact_with_CIC.html#CreateConnection">Downchannel</a> 생성 시 사용</li><li>POST: <a href="/CIC/References/CIC_Message_Format.html#Event">이벤트 메시지</a>를 보낼 때 사용</li></ul> |
| :scheme        | CIC API는 https 통신을 지원합니다.                                                                            |
| :path          | 각각 다음 경로를 사용합니다. <ul><li>/v1/directives : <a href="/CIC/Guides/Interact_with_CIC.html#CreateConnection">Downchannel</a> 생성 시 사용</li><li>/v1/events : <a href="/CIC/References/CIC_Message_Format.html#Event">이벤트 메시지</a>를 보낼 때 사용</li></ul> |
| authorization  | Clova 인증 서버를 통해 획득한 인증 토큰을 입력합니다. 인증 토큰은 모든 요청의 헤더에 포함되어 있어야 합니다.                     |
| content-type   | HTTP 메시지의 콘텐츠 타입이며, 이벤트 메시지를 전송할 때 사용합니다. multipart 메시지를 보내기 때문에 항상 *multipart/form-data*여야 합니다. 또한, 메시지를 구분하는 메시지 경계 문구를 지정해야 하며, 이 문구는 메시지의 본문에서 나타나지 않아야 합니다. 참고로 각 메시지에 대한 콘텐츠 타입은 메시지 헤더에서 정의하며, 이벤트 메시지. |

### HTTP multipart 메시지 {#MultipartMessage}
HTTP 헤더를 전달한 이후 연결이 설정되면 stream이 생성됩니다. 이 stream을 통해 CIC와 클라이언트가 이벤트 메시지 또는 지시 메시지를 전송합니다. 각 메시지는 요청이나 응답에 대한 정보를 담고 있는 JSON 형식의 데이터를 담고 있거나 사용자의 음성이 녹음된 바이너리 형식의 데이터로 구성됩니다. 각각의 메시지 구성은 데이터의 타입에 따라 다음과 같이 구분됩니다.

#### JSON 데이터 형식의 메시지 구성
JSON 포맷의 메시지는 이벤트 메시지 정보를 담고 있거나 또는 콘텐츠 정보를 담을 때 사용됩니다. JSON 형식의 데이터를 보낼 때 메시지는 다음 예처럼 헤더와 본문으로 구성됩니다.

{% raw %}
```
[ Message Header ]
Content-Disposition: form-data; name="metadata"
Content-Type: application/json; charset=UTF-8

[ Message Body ]
{
  "context": [
  ],
  "event": {
    "header": {
      "namespace": {{string}},
      "name": {{string}},
      "dialogRequestId": {{string}},
      "messageId": {{string}}
    },
    "payload": {{object}}
  }
}

```
{% endraw %}

각 이벤트 메시지는 CIC가 제공하는 API에 따라 그 구성이 달라질 수 있습니다. 메시지의 구성과 API에 대한 자세한 정보는 [메시지 포맷](/CIC/References/CIC_Message_Format.md)과 [API](/CIC/References/CIC_API.md)를 참조합니다.

#### 음성 데이터 형식의 메시지 구성
음성 데이터는 다음과 같은 헤더를 가지며, 본문에는 바이너리 데이터가 포함됩니다. 자세한 내용은 [SpeechRecognizer.Recognize](/CIC/References/APIs/SpeechRecognizer.md#Recognize)를 참조합니다.

{% raw %}
```
[ Message Header ]
Content-Disposition: form-data; name="audio"
Content-Type: application/octet-stream

[ PCM Audio Attachment ]
{{ Binary audio attachment }}
```
{% endraw %}

## HTTP 응답 {#Response}
일반적인 HTTP 응답은 CIC로부터 전달되는 지시 메시지이며, 다음과 같은 메시지 조합을 가집니다.
* [Synthesizer.Speak](/CIC/References/APIs/SpeechSynthesizer.md#Speak)은 음성을 출력하는 지시 메시지로 음성 데이터가 추가로 전달됩니다.
* *Synthesizer.Speak* 지시 메시지와 함게 부가 정보를 전달하는 지시 메시지가 전달될 수 있습니다. 예를 들면, 스트리밍 정보를 포함하고 있는 [AudioPlayer.Play](/CIC/References/APIs/AudioPlayer.md#Play) 지시 메시지가 추가로 전달될 수 있습니다.

<div class="note">
  <p><strong>Note!</strong></p>
  <p>현재 HTTP 상태 코드로 오류 상황을 전달하고 있으나 곧 exception 응답을 별도로 준비할 예정입니다.</p>
</div>

## HTTP 메시지 예제 {#MessageExample}
다음은 클라이언트와 CIC 사이에서 주고 받은 HTTP 요청/응답 메시지 예제입니다.

### Request Example
{% raw %}
```
:method = POST
:scheme = https
:path = /v1/events
authorization = Bearer {{clova-access-token}}
content-type = multipart/form-data; boundary=Boundary-Text

--Boundary-Text
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

--Boundary-Text

Content-Disposition: form-data; name="audio"
Content-Type: application/octet-stream

{{binary audio attachment}}
--Boundary-Text--

```
{% endraw %}

### Response Example
{% raw %}
```
:status = 200
content-type = multipart/related; boundary=Boundary-Text; type="application/json"

--Boundary-Text
Content-Type: application/json; charset=UTF-8

{
    "directive": {
        "header": {
            "namespace": "SpeechSynthesizer",
            "name": "Speak",
            "messageId": "277b40c3-b046-4f61-a551-783b1547e7b7",
            "dialogRequestId": "4e4080d6-c440-498a-bb73-ae86c6312806"
        },
        "payload": {
            "url": "cid:1234",
            "format": "AUDIO_MPEG"
            "token": "kr17447380422"
        }
    }
}

--Boundary-Text
Content-Type: application/octet-stream
Content-ID: <1234>

{{binary audio attachment}}
--Boundary-Text--
```
{% endraw %}
