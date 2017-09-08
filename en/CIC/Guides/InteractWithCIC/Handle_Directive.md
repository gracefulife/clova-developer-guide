## Handling directive message {#HandleDirective}
CIC returns directive messages to instruct your client to perform specific actions. A directive message is either a response to an [event message](#SendEvent) or a message sent through a downchannel created at an initial connection with CIC. Responses are usually a [multipart message](/CIC/References/CIC_API.md#MultipartMessage). A JSON-format [directive message](/CIC/References/CIC_API.md#Directive) is returned first, followed by subsequent messages containing additional information (speech data, content details) as specified by the [CIC messages](/CIC/References/CIC_API.md).

| Content type            | Description                                             |
|---------------------|-------------------------------------------------|
| Speech data            | Speech audio to play through a device speaker                  |
| JSON content data | <ul><li>Data to be displayed on a device screen (See <a href="/CIC/References/Content_Templates.md">Content template</a>)</li><li>Data that contains content's location (for example, music to play) and its credentials</li></ul> |

Implement your client to handle directive messages in the following steps.

<ol>
<li><p>When a directive message is returned in response to an event message or is sent through a downchannel, store the message in a preset <a href="#ManageMessageQ">message queue</a>.</p>
</li>
<li><p>Parse the message header of the <a href="/CIC/References/CIC_API.html#Directive">directive message</a>. Generally, use <code>dialogRequestId</code> to find the user request, and <code>namespace</code> and <code>name</code> to determine which <a href="/CIC/References/CIC_API.html">API</a> is used. Below is an example of a directive message received.</p>
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
<li>Check whether the <a href="/CIC/CIC_Overview.html#DialogModel">dialog ID</a>(<code>dialogRequestId</code>) of the directive message matches the dialog ID kept on the client.
<ul>
<li><p><strong>If it matches the dialog ID kept on the client</strong>, perform necessary actions as specified by the API. Usually, you can pick out additional necessary information (speech data) from <a href="#ManageMessageQ">message queues</a>, <a href="/CIC/References/APIs/SpeechSynthesizer.html#Speak">using the<code>cid</code> value</a> contained in <code>payload</code> of the directive message. <code>cid</code> indicates a `Content-Id` message header of speech data returned in a multipart message, as shown below.</p>
<pre><code>--b4bc211bbd32e5cb5989bc7ab2d3088fdd72dcc6696253151c98176f88ba
Content-Disposition: form-data; name="attachment-39b2f844-b168-4dc2-bea7-d5c249e446e3"
Content-Id: d329085c-379e-48aa-b871-7ecebdbe831d
Content-Type: application/octet-stream<br />
[[ binary audio attachment ]]<br />
--b4bc211bbd32e5cb5989bc7ab2d3088fdd72dcc6696253151c98176f88ba
</code></pre>
</li>
<li><strong>If it does not match the dialog ID kept on the client</strong>, disregard the directive message and all related messages and remove them from the queue.</li>
</ul>
</li>
</ol>