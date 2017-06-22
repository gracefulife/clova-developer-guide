## Sending Event message {#SendEvent}
Your client can send an [Event message](/CIC/References/Message_Format.md#Event) to CIC. It is used to send a client request to CIC. An Event message can be sent either as a JSON format message or a multipart message carrying user's speech input or text input.

<div class="note">
<p><strong>Note!</strong></p>
<p>CIC processes user requests in the order they come in. Therefore, you should implement your client to start processing a new request from the point the response to the previous request begins to return.</p>
</div>

When your client sends user's speech data, it uses a [SpeechRecognizer.Recognize](/CIC/References/APIs/SpeechRecognizer.md#Recognize) Event message. The following explains how to send an Event message to CIC using the SpeechRecognizer.Recognize API.

<ol>
<li><p>Prepare an <a href="#RequiredLibrary">HTTP/2 library</a> and a <a href="#Authorization">Clova access token</a> in your client.</p>
</li>
<li><p>Fill in the <a href="/CIC/References/HTTP2_Message_Format.html">HTTP/2</a> header with appropriate values and send a request using the HTTP/2 library.</p>
<pre><code>:method = POST
:scheme = https
:path = /v1/events
Authorization = Bearer XHapQasdfsdfFsdfasdflQQ7w-Example
content-type = multipart/form-data; boundary=Boundary-Text
</code></pre>
</li>
<li>Create a dialog ID (dialogRequestId) and a message ID (messageId) in UUID format which will be included in the Event message. You create a unique dialog ID and a message ID so that associated Directive messages can be sorted out from a <a href="#ManageMessageQ">message queue</a> at a later step.</li>
<li>In the first part of a message, write a JSON-format message and a message header as described in the <a href="/CIC/References/APIs/SpeechRecognizer.html#Recognize">SpeechRecognizer.Recognize</a> API and send it to CIC.
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
<li>From the second part of a message, send audio data by capturing the speech input with the interval of 200ms. Since the data type has changed, write the message header as follows.
<pre><code>--Boundary-Text
Content-Disposition: form-data; name="audio"
Content-Type: application/octet-stream

{ PCM Audio Attachment }
--Boundary-Text--
</code></pre>
</li>
<li><p>Keep sending the audio data until the user finishes speaking or CIC sends a <a href="/CIC/References/APIs/SpeechRecognizer.html#StopCapture">SpeechRecognizer.StopCapture</a> Directive message through a Downchannel. Once the sending is complete, an HTTP response message is received from CIC.</p>
</li>
</ol>