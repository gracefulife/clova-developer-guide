## 이벤트 메시지 전송하기 {#SendEvent}
클라이언트는 CIC로 [이벤트 메시지](/CIC/References/Message_Format.md#Event)를 전송할 수 있습니다. 이벤트 메시지는 클라이언트 요청을 CIC로 전달할 때 사용됩니다. 메시지는 JSON 포맷의 이벤트 메시지뿐만 아니라 사용자 음성 입력이나 텍스트 입력을 [multipart 형태의 메시지](/CIC/References/HTTP2_Message_Format.md#MultipartMessage)로 전송합니다.

클라이언트에서 사용자의 음성 데이터를 CIC로 보낼 때 [`SpeechRecognizer.Recognize`](/CIC/References/APIs/SpeechRecognizer.md#Recognize) 이벤트 메시지를 사용합니다. 다음은 `SpeechRecognizer.Recognize`를 이용해 CIC로 이벤트 메시지를 전송하는 방법을 설명합니다.

<ol>
<li><p>이벤트 메시지 전송을 위해 클라이언트에 <a href="#RequiredLibrary">HTTP/2용 라이브러리</a>와 <a href="#Authorization">Clova access token</a>을 준비합니다.</p>
</li>
<li><p>다음과 같이 <a href="/CIC/References/HTTP2_Message_Format.html">HTTP/2</a>의 헤더를 준비한 값으로 채우고 HTTP/2용 라이브러리를 이용해 요청을 전달합니다.</p>
<pre><code>:method = POST
:scheme = https
:path = /v1/events
Authorization = Bearer XHapQasdfsdfFsdfasdflQQ7w-Example
content-type = multipart/form-data; boundary=Boundary-Text
</code></pre>
</li>
<li>이벤트 메시지에 포함시킬 <a href="/CIC/CIC_Overview.html#DialogModel">대화 ID</a>(<code>dialogRequestId</code>)와 메시지 ID(messageId)를 UUID 포맷으로 생성합니다. 추후 <a href="#ManageMessageQ">메시지 큐</a>에서 지시 메시지를 선별할 수 있도록 식별 가능한 대화 ID와 메시지 ID를 생성해서 전달합니다.</li>
<li>첫 번째 메시지 파트에 <a href="/CIC/References/APIs/SpeechRecognizer.html#Recognize"><code>SpeechRecognizer.Recognize</code></a> API 스펙에 맞게 작성된 JSON 포맷의 이벤트 메시지와 메시지 헤더를 함께 입력한 후 CIC로 전송합니다.
<pre><code>--Boundary-Text
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
--Boundary-Text--
</code></pre>
</li>
<li>두 번째 메시지 파트부터 사용자가 입력한 음성 데이터를 200ms 간격으로 끊어서 전송합니다. 데이터 형식 변경에 따라 메시지 헤더도 아래와 같이 작성합니다.
<pre><code>--Boundary-Text
Content-Disposition: form-data; name="audio"
Content-Type: application/octet-stream

{ PCM Audio Attachment }
--Boundary-Text--
</code></pre>
</li>
<li><p>사용자가 음성 입력을 마치거나 CIC로부터 <a href="/CIC/References/APIs/SpeechRecognizer.html#StopCapture"><code>SpeechRecognizer.StopCapture</code></a> 지시 메시지가 전달될 때까지 음성 데이터를 계속 전송합니다. 전송이 완료되면 CIC로부터 HTTP 응답 메시지가 수신됩니다.</p>
</li>
</ol>
