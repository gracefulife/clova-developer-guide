## Handling directive message {#HandleDirective}
CIC returns directive messages to instruct your client to perform specific actions. A directive message is either a response to an [event message](#SendEvent) or a message sent through a downchannel created at an initial connection with CIC. A JSON-format [directive message](/CIC/CIC_Message_Format.md#Directive) is returned first followed by subsequent messages containing additional information (speech data, content details) using [CIC APIs](/CIC/References/CIC_API.md).

| Content type            | Description                                             |
|---------------------|-------------------------------------------------|
| Speech data            | Speech data to be synthesized for audio output through a device speaker                  |
| JSON content data | <ul><li>Data to be displayed on a device screen (See <a href="/CIC/References/Content_Templates.md">Content Template</a>)</li><li>Content location (necessary for music playback, for example) and credentials</li></ul> |

Implement your client to handle directive messages in the following steps.

<ol>
<li><p>When you receive a response to an event message or a directive message through a downchannel, store the message in a preset <a href="#ManageMessageQ">message queue</a>.</p>
</li>
<li><p>Parse the message header of the <a href="/CIC/References/CIC_Message_Format.html#Directive">directive message</a>. Generally, use <em>dialogRequestId</em> to find the user request, and <em>namespace</em> and <em>name</em> to fine the appropriate <a href="/CIC/References/CIC_API.html">CIC API</a>. Below is an example of a directive message.</p>
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
<li>Match the dialog ID(dialogRequestId) of the directive message to the dialog ID stored in your client.
<ul>
<li><strong>If it matches the dialog ID in your client</strong>, perform necessary actions as specified by the API. Usually, you can find the additional information (speech data) necessary for client actions in the message queue, using the cid field value contained in message payload.</li>
<li><strong>If it does not match the dialog ID in your client</strong>, disregard the directive message and its related messages and remove them from the queue.</li>
</ul>
</li>
</ol>

<div class="note">
<p><strong>Note!</strong></p>
<p>As mentioned above, you must use a queue to handle directive messages. See <a href="#ManageMessageQ">Managing message queue</a> for more details.</p>
</div>
