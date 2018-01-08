## Handling directives {#HandleDirective}

CIC returns directives to instruct a client to perform specific actions. A directive is either a response to an [event](#SendEvent) or a message initiated by CIC. Directives as a message is sent to a client through the downchannel and as a response are usually sent as a [multipart message](/CIC/References/CIC_API.md#MultipartMessage). The first part of a multipart message contains the [directive](/CIC/References/CIC_API.md#Directive) itself in JSON, and is followed by subsequent parts specified according to the [CIC API](/CIC/References/CIC_API.md) specification, containing the following additional information.

| Content type            | Description                                             |
|---------------------|-------------------------------------------------|
| Speech data         | Speech audio to play through a client speaker                  |
| JSON content data | <ul><li>Data to be displayed on a cient screen (See <a href="/CIC/References/Content_Templates.md">Content template</a>)</li><li>Data that contains content's location (for example, music to play) and its credentials</li></ul> |

To process directives received on a client:

<ol>
<li><p>Store the directive, received either as an HTTP response or through a downchannel, in a <a href="#ManageMessageQ">message queue</a>.</p>
</li>
<li><p>Parse the header of the <a href="/CIC/References/CIC_API.html#Directive">directive</a>. In parsing a message—be it an event or directive—use the <code>dialogRequestId</code> field to identify a user request, and the <code>namespace</code> and the <code>name</code> fields to identify what type of <a href="/CIC/References/CIC_API.html">CIC message</a> is being parsed. Here is an example of a directive received.</p>
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
<li>Check whether the <a href="/CIC/CIC_Overview.html#DialogModel">dialog ID</a> (<code>dialogRequestId</code>) of the directive matches the dialog ID kept on the client.
<ul>
<li><p><strong>If the two dialog IDs match</strong>: Perform the actions directed by CIC. To retrieve relevant additional information (e.g. speech data) from the <a href="#ManageMessageQ">message queue</a>, <a href="/CIC/References/CICInterface/SpeechSynthesizer.html#Speak">use the<code>cid</code> value</a>, contained in the <code>url</code> field of the directive's <code>payload</code>. The <code>cid</code> represents the <code>Content-Id</code> message header field of a multipart message. Here is an example of a message header.</p>
<pre><code>--b4bc211bbd32e5cb5989bc7ab2d3088fdd72dcc6696253151c98176f88ba
Content-Disposition: form-data; name="attachment-39b2f844-b168-4dc2-bea7-d5c249e446e3"
Content-Id: d329085c-379e-48aa-b871-7ecebdbe831d
Content-Type: application/octet-stream<br />
[[ binary audio attachment ]]<br />
--b4bc211bbd32e5cb5989bc7ab2d3088fdd72dcc6696253151c98176f88ba
</code></pre>
</li>
<li><strong>If the two dialog IDs do not match</strong>: Disregard and remove from the message queue, the directive and all the other messages related to the given directive.</li>
</ul>
</li>
</ol>
