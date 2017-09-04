## 지시 메시지 처리하기 {#HandleDirective}
지시 메시지는 CIC로부터 수신되며 클라이언트에 특정 동작을 요구합니다. 지시 메시지는 [이벤트 메시지](#SendEvent)의 응답이나 CIC와 최초 연결시 생성했던 downchannel을 통해 전달됩니다. 응답은 주로 [multipart 메시지](/CIC/References/CIC_API.md#MultipartMessage) 형태이고, JSON 포맷 형태의 [지시 메시지](/CIC/References/CIC_API.md#Directive)가 첫 번째 메시지로 먼저 수신된 후 [CIC 메시지](/CIC/References/CIC_API.md)에 따라 주로 다음과 같이 부가적인 정보(음성 데이터, 콘텐츠 정보)를 담은 메시지가 추가로 수신될 수 있습니다.

| 콘텐츠 유형            | 설명                                             |
|---------------------|-------------------------------------------------|
| 음성 데이터            | 기기 스피커를 통해 출력하려는 음성 정보                  |
| JSON 형식의 콘텐츠 정보 | <ul><li>기기의 화면을 통해 표시하려는 데이터(<a href="/CIC/References/Content_Templates.md">content template</a> 참조)</li><li>음악과 같이 재생하려는 콘텐츠의 위치와 인증 정보가 담긴 데이터</li></ul> |

클라이언트는 다음과 같이 지시 메시지를 처리해야 합니다.

<ol>
<li><p>특정 이벤트 메시지의 응답이나 downchannel을 통해 전달받는 지시 메시지를 미리 정해둔 <a href="#ManageMessageQ">메시지 큐</a>에 저장합니다.</p>
</li>
<li><p>수신된 <a href="/CIC/References/CIC_API.html#Directive">지시 메시지</a>의 메시지 헤더를 분석(parsing)합니다. 일반적으로 <code>dialogRequestId</code>는 사용자 요청, <code>namespace</code>와 <code>name</code>은 <a href="/CIC/References/CIC_API.html">API</a>를 구분하는데 사용합니다. 다음은 수신된 지시 메시지의 예입니다.</p>
<pre><code>{
  "directive": {
    "header": {
      "namespace": "SpeechSynthesizer",
      "name": "Speak",
      "messageId": "277b40c3-b046-4f61-a551-783b1547e7b7",
      "dialogRequestId": "4e4080d6-c440-498a-bb73-ae86c6312806"
    },
    "payload": {
      "format": "AUDIO_MPEG",
      "token": "b5fa5144-1e55-4193-8628-c70283083d9b",
      "ttsLang": "ko",
      "ttsText": "내일 날씨는 오전에는 맑다가 오후에는 구름이 많아지겠어요.",
      "url": "cid:9d5d37a3-0e70-41a6-a671-e1a40c7ea4d8",
      "x-clova-pause-before": 0
    }
  }
}
</code></pre>
</li>
<li>수신한 지시 메시지의 <a href="/CIC/CIC_Overview.html#DialogModel">대화 ID</a>(<code>dialogRequestId</code>)가 클라이언트가 보관하고 있는 대화 ID와 대응되는지 확인합니다.
<ul>
<li><p><strong>클라이언트가 보관하고 있는 마지막 대화 ID와 일치하면</strong>, API 명세에 따라 필요한 동작을 수행합니다. 일반적으로 지시 메시지의 <code>payload</code>에 포함된 <a href="/CIC/References/APIs/SpeechSynthesizer.html#Speak"><code>cid</code> 값을 이용</a>하여 클라이언트 동작에 필요한 부가 정보(음성 데이터)를 <a href="#ManageMessageQ">메시지 큐</a>에서 선별해 낼 수 있습니다. <code>cid</code>가 의미하는 것은 다음과 같이 multipart 메시지로 전달된 음성 데이터의 `Content-Id` 메시지 헤더를 의미합니다.</p>
<pre><code>--b4bc211bbd32e5cb5989bc7ab2d3088fdd72dcc6696253151c98176f88ba
Content-Disposition: form-data; name="attachment-39b2f844-b168-4dc2-bea7-d5c249e446e3"
Content-Id: d329085c-379e-48aa-b871-7ecebdbe831d
Content-Type: application/octet-stream<br />
[[ binary audio attachment ]]<br />
--b4bc211bbd32e5cb5989bc7ab2d3088fdd72dcc6696253151c98176f88ba
</code></pre>
</li>
<li><strong>클라이언트가 보관하고 있는 대화 ID와 일치하지 않으면</strong>, 해당 지시 메시지와 관련된 모 메시지를 무시하고 큐에서 제거합니다.</li>
</ul>
</li>
</ol>
