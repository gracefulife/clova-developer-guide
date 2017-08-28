## Sending event message {#SendEvent}
Clients can send [event messages](/CIC/References/Message_Format.md#Event) to CIC. You use event messages to send client requests to CIC. You can send JSON-format event messages or [multipart messages](/CIC/References/HTTP2_Message_Format.md#MultipartMessage) carrying user's speech input or text input.

To send user's speech data to CIC, use a [`SpeechRecognizer.Recognize`](/CIC/References/APIs/SpeechRecognizer.md#Recognize) event message. The following explains how to send event messages to CIC using `SpeechRecognizer.Recognize`.

<ol>
<li><p>Prepare <a href="#RequiredLibrary">HTTP/2 library</a> and <a href="#Authorization">Clova access token</a> in your client.</p>
</li>
<li><p>Fill in the <a href="/CIC/References/HTTP2_Message_Format.html">HTTP/2</a> header with appropriate values and send a request using the HTTP/2 library.</p>
<pre><code>:method = POST
:scheme = https
:path = /v1/events
Authorization = Bearer XHapQasdfsdfFsdfasdflQQ7w-Example
content-type = multipart/form-data; boundary=Boundary-Text
</code></pre>
</li>
<li><p>Create <a href="/CIC/CIC_Overview.html#DialogModel">dialog ID</a>(<code>dialogRequestId</code>) and message ID(messageId) in UUID format to include in the event message. You create and send uniquely identifiable dialog ID and message ID to find matching directive messages from <a href="#ManageMessageQ">message queues</a> later.</p></li>
<li><p>In the first message part, write JSON-format event message and message header as described in the <a href="/CIC/References/APIs/SpeechRecognizer.html#Recognize"><code>SpeechRecognizer.Recognize</code></a> API and send it to CIC.</p>
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
<li>From the second message part, send the user's speech data by capturing it with the interval of 200ms. Write the message header as follows in accordance with the changed data type.
<pre><code>--Boundary-Text
Content-Disposition: form-data; name="audio"
Content-Type: application/octet-stream

{ PCM Audio Attachment }
--Boundary-Text--
</code></pre>
</li>
<li><p>Continue to send the speech data until the user finishes speaking or CIC returns a <a href="/CIC/References/APIs/SpeechRecognizer.html#StopCapture"><code>SpeechRecognizer.StopCapture</code></a> directive message. Once the sending is complete, CIC returns an HTTP response message.</p>
</li>
</ol>