## Sending event message {#SendEvent}
Clients can send [event messages](/CIC/References/Message_Format.md#Event) to CIC. Use event messages to send client requests to CIC. You can send either JSON-format event messages or multipart messages carrying user's speech input or text input.

<div class="note">
<p><strong>Note!</strong></p>
<p>CIC processes user requests in the order they come in. Therefore, implement your client to process a new request from the point when a response to a previous request begins to return.</p>
</div>

To send user's speech data to CIC, use a [SpeechRecognizer.Recognize](/CIC/References/APIs/SpeechRecognizer.md#Recognize) event message. The following explains how to send an event message to CIC using the SpeechRecognizer.Recognize API.

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
<li>Create a dialog ID (dialogRequestId) and message ID(messageId) in UUID format to include in the event message. You create and send uniquely identifiable dialog ID and message ID to find directive messages in a <a href="#ManageMessageQ">message queue</a> at a later step.</li>
<li>In the first part of a message, write a JSON-format event message and a message header as described in the <a href="/CIC/References/APIs/SpeechRecognizer.html#Recognize">SpeechRecognizer.Recognize</a> API and send it to CIC.
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
<li>From the second part of a message, send user's speech input data by capturing it with the interval of 200ms. Write the message header as follows to match the changed data type.
<pre><code>--Boundary-Text
Content-Disposition: form-data; name="audio"
Content-Type: application/octet-stream

{ PCM Audio Attachment }
--Boundary-Text--
</code></pre>
</li>
<li><p>Continue to send the speech input data until the user finishes speaking or CIC sends a <a href="/CIC/References/APIs/SpeechRecognizer.html#StopCapture">SpeechRecognizer.StopCapture</a> directive message through a downchannel. Once the sending is complete, CIC returns an HTTP response message.</p>
</li>
</ol>