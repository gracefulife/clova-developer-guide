## Handling directives {#HandleDirective}
CIC returns directives to instruct a client to perform specific actions. A directive is either a response to an [event](#SendEvent) or a message initiated by CIC. Directives that are messages are sent to a client through the downchannel and those that are responses are usually sent as a [multipart message](/CIC/References/CIC_API.md#MultipartMessage). The first part of a multipart message contains the [directive](/CIC/References/CIC_API.md#Directive) itself in JSON and is followed by subsequent parts specified according to the [CIC API](/CIC/References/CIC_API.md) specification that contains the following additional information.

| Content Type            | Description                                             |
|---------------------|-------------------------------------------------|
| Audio data            | Audio data to output through a client speaker                  |
| JSON content data | <ul><li>Data to be displayed on a client display (see <a href="/CIC/References/Content_Templates.md">content template</a>)</li><li>Data that contains content location (for example, music to play) and its credentials</li></ul> |

To process directives received on a client:

<ol>
  <li>Store the directive, received either as an HTTP response or through a downchannel, in a <a href="#ManageMessageQ">message queue</a>.</li>
  <li>
    <p>Parse the header of the <a href="/CIC/References/CIC_API.html#Directive">directive</a>. Generally, <code>dialogRequestId</code> is used to distinguish user request. The <code>namespace</code> and <code>name</code> are used to distinguish <a href="/CIC/References/CIC_API.html">API</a>. Here is an example of a received directive.</p>
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
      "ttsLang": "ko"
      "url": "cid:9d5d37a3-0e70-41a6-a671-e1a40c7ea4d8",
      "x-clova-pause-before": 0
    }
  }
}
</code></pre>
  </li>
  <li>Check whether the <a href="/CIC/CIC_Overview.html#DialogModel">dialogue ID</a> (<code>dialogRequestId</code>) of the directive matches the latest dialogue ID kept on the client.
    <ul>
      <li>
        <p><strong>If the two dialogue IDs match</strong>, the client performs the required action in the API reference. Generally, you can distinguish the additional information (audio data) required for the client action on the <a href="#ManageMessageQ">message queue</a> <a href="/CIC/References/CICInterface/SpeechSynthesizer.html#Speak">using the <code>cid</code> value</a> in the <code>payload</code> of the directive. <code>cid</code> refers to the <code>Content-ID</code> message header of the audio data, as shown below, that is sent as a part of the multipart message.</p>
        <pre><code>--b4bc211bbd32e5cb5989bc7ab2d3088fdd72dcc6696253151c98176f88ba
Content-Disposition: form-data; name="attachment-39b2f844-b168-4dc2-bea7-d5c249e446e3"
Content-ID: d329085c-379e-48aa-b871-7ecebdbe831d
Content-Type: application/octet-stream<br />
[[ binary audio attachment ]]<br />
--b4bc211bbd32e5cb5989bc7ab2d3088fdd72dcc6696253151c98176f88ba
</code></pre>
      </li>
      <li><strong>If the two dialogue IDs do not match</strong>, the client ignores the directive and all related messages and removes it from the message queue.</li>
    </ul>
  </li>
</ol>

<div class="danger">
  <p><strong>Caution!</strong></p>
  <p>The client must ignore any unsupported or unknown directives received. It is important to note that a client can receive many directives from CIC at once as a multipart message. Then a client must only ignore unsupported or unknown directives from this message.</p>
</div>
