## Handling Directive message {#HandleDirective}
A Directive message is sent from CIC to instruct your client to perform a specific action. A Directive message is sent either in response to an [Event message](#SendEvent) or through a Downchannel which is created when an initial connection with CIC is established. Firstly, a [Directive message](/CIC/CIC_Message_Format.md#Directive) formatted in JSON is received followed by subsequent messages containing additional information (audio data, content information) using appropriate [CIC APIs](/CIC/References/CIC_API.md).

| Content type  | Description  |
|---------------------|-------------------------------------------------|
| Audio data  | Audio output to be played back through a device speaker  |
| JSON content data | <ul><li>Data to be displayed on a device screen (See <a href="/CIC/References/Content_Templates.md">Content Template</a>)</li><li>Data containing the location of content (necessary for music playback, for example) and credential information</li></ul> |

Your client should handle a Directive message in the following steps.

<ol>
<li><p>Stores the Directive message in a preset <a href="#ManageMessageQ">message queue</a> when your client receives one, whether it is a response to an Event message or it is a Directive message delivered through a Downchannel.</p>
</li>
<li><p>Parse the message header of the <a href="/CIC/References/CIC_Message_Format.html#Directive">Directive message</a>. Typically, you use a <em>dialogRequestId</em> to identify the user request associated with the message, and <em>namespace</em> and <em>name</em> to identify the <a href="/CIC/References/CIC_API.html">CIC API</a>. This is an example of a Directive message.</p>
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
<li>Match the dialog ID(dialogRequestId) of the Directive message to the dialog ID stored in your client.
<ul>
<li><strong>If it matches the dialog ID stored in your client</strong>, your client performs a necessary action as specified by the API. Usually, additional information (audio data) necessary for the client action can be sorted out from the message queue using the cid field value contained in the message payload.</li>
<li><strong>If it does not match the dialog ID stored in your client</strong>, the Directive message and its related messages are disregarded and removed from the queue.</li>
</ul>
</li>
</ol>

<div class="note">
<p><strong>Note!</strong></p>
<p>As mentioned above, your client should use a queue when handling Directive messages. See <a href="#ManageMessageQ">Managing message queue</a> for more details.</p>
</div>
