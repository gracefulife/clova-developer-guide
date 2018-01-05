## Sending events {#SendEvent}
Clients deliver their requests to CIC in [events](/CIC/References/CIC_API.md#Event), in the form of [multipart messages](/CIC/References/CIC_API.md#MultipartMessage). Multipart messages may contain JSON objects and/or binary data.

To send a user's vocal data to CIC, use the [`SpeechRecognizer.Recognize`](/CIC/References/CICInterface/SpeechRecognizer.md#Recognize) event as instructed below:

<ol>
<li><p>Import an <a href="#RequiredLibrary">HTTP/2 library</a> library on the client and make sure you have a <a href="#Authorization">Clova access token</a> ready.</p>
</li>
<li><p>Specify the HTTP header based on the <a href="/CIC/References/CIC_API.html#SendEvent">CIC API</a> specification, and send the HTTP request using the HTTP/2 library.</p>
<pre><code>:method = POST
:scheme = https
:path = /v1/events
Authorization = Bearer XHapQasdfsdfFsdfasdflQQ7w-Example
content-type = multipart/form-data; boundary=Boundary-Text
</code></pre>
</li>
<li><p>Create a <a href="/CIC/CIC_Overview.html#DialogModel">dialog ID</a> (<code>dialogRequestId</code>) and a message ID (<code>messageId</code>), both in UUID format. Make sure the IDs are unique as they will later be used to find a matching directive message from <a href="#ManageMessageQ">message queues</a>.</p></li>
<li><p>Write the first part of the message and send it to CIC. The first part of the message shall contain the message header and the message body in JSON, containing event information based on the <a href="/CIC/References/CICInterface/SpeechRecognizer.html#Recognize"><code>SpeechRecognizer.Recognize</code></a> API specification.</p>
<pre><code>--Boundary-Text
Content-Disposition: form-data; name="metadata"
Content-Type: application/json; charset=UTF-8<br/>
{
  "context": [
    {
      "header": {
        "namespace": "Alerts",
        "name": "AlertsState"
      },
      "payload": {
        "allAlerts": [
          ...
        ],
        "activeAlerts": [
          ...
        ]
      }
    },
    ...
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
--Boundary-Text
</code></pre>
</li>
<li>From the second message part, send the user's speech in 200ms units. Since the message body is to contain binary data and not JSON, make sure you change the message header accordingly. Here is an example:
<pre><code>--Boundary-Text
Content-Disposition: form-data; name="audio"
Content-Type: application/octet-stream<br/>
[[ binary audio attachment ]]
--Boundary-Text--
</code></pre>
</li>
<li><p>Continue sending the vocal data until the user finishes speaking to Clova or until CIC returns the <a href="/CIC/References/CICInterface/SpeechRecognizer.html#StopCapture"><code>SpeechRecognizer.StopCapture</code></a> directive. Once the sending is complete, CIC returns an HTTP response message to the client.</p>
</li>
</ol>

<div class="note">
  <p><strong>Note!</strong></p>
  <p>To process a user's request in text, use the  <a href="/CIC/References/CICInterface/TextRecognizer.html#Recognize"><code>TextRecognizer.Recognize</code></a> event.</p>
</div>
