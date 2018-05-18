## イベントを送信する {#SendEvent}
クライアントは、CICに[イベント](/CIC/References/CIC_API.md#Event)を送信することができます。イベントは、クライアントからのリクエストをCICに送るために使用されます。JSON形式のメッセージと、ユーザーからの音声入力を[マルチパートメッセージ](/CIC/References/CIC_API.md#MultipartMessage)で送信します。

クライアントからユーザーの音声データをCICに送信する際、[`SpeechRecognizer.Recognize`](/CIC/References/CICInterface/SpeechRecognizer.md#Recognize)イベントを使用します。以下では、`SpeechRecognizer.Recognize`を使ってCICにイベントを送信する方法について説明します。

<ol>
  <li>イベントを送信するために、クライアントに<a href="#RequiredLibrary">HTTP/2ライブラリ</a>と<a href="#Authorization">Clovaアクセストークン</a>を用意します。</li>
  <li>
    <p>次のように<a href="/CIC/References/CIC_API.html#SendEvent">CIC API</a>に合わせて、HTTPヘッダーに用意した値を設定し、HTTP/2ライブラリでリクエストを送信します。</p>
    <pre><code>:method = POST
:scheme = https
:path = /v1/events
User-Agent: MyOrganizationName/MyAppName/2.1.2-release (Android 7.0;SettopBox;target=KR;other=sample)
Authorization: Bearer XHapQasdfsdfFsdfasdflQQ7w-Example
Content-Type: multipart/form-data; boundary=Boundary-Text
</code></pre>
  </li>
  <li>イベントに含める<a href="/CIC/CIC_Overview.html#DialogModel">ダイアログID</a>(<code>dialogRequestId</code>)とメッセージID(<code>messageId</code>)をUUID形式に作成します。後ほど<a href="#ManageMessageQ">メッセージキュー</a>でディレクティブを確認できるように、識別できるダイアログIDとメッセージIDを作成して送信します。</li>
  <li>
    <p>最初のメッセージパートに、<a href="/CIC/References/CICInterface/SpeechRecognizer.html#Recognize"><code>SpeechRecognizer.Recognize</code></a>API仕様に準じて作成されたJSON形式のイベントとメッセージヘッダーを入力して、CICに送信します。</p>
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
      "lang": "ko",
      "profile": "CLOSE_TALK",
      "format": "AUDIO_L16_RATE_16000_CHANNELS_1",
      "initiator": {
        "type": "WAKEWORD",
        "inputSource": "SELF",
        "payload": {
          "deviceUUID": "f003af9d-14c5-424b-b1f9-f0134bd0ed86",
          "wakeWord": {
            "name": "clova",
            "confidence": 0.812312,
            "indices": {
              "startIndexInSamples": 0,
              "endIndexInSamples": 16000
            }
          }
        }
      }
    }
  }
}
--Boundary-Text--
</code></pre>
  </li>
  <li>
    <p>2つ目のメッセージパートから、ユーザーが入力した音声データを200ミリ秒ずつ切って送信します。データ形式が変更されたため、メッセージヘッダーも次のように変更して作成します。</p>
    <pre><code>--Boundary-Text
Content-Disposition: form-data; name="audio"
Content-Type: application/octet-stream<br/>
[[ binary audio attachment ]]
--Boundary-Text--
</code></pre>
  </li>
  <li>ユーザーが音声入力を終えるか、またはCICから<a href="/CIC/References/CICInterface/SpeechRecognizer.html#StopCapture"><code>SpeechRecognizer.StopCapture</code></a>ディレクティブを受信するまで、音声データを送り続けます。送信が完了すると、CICからHTTPレスポンスメッセージを受信します。</li>
</ol>

<div class="note">
  <p><strong>メモ</strong></p>
  <p><a href="/CIC/References/CICInterface/TextRecognizer.html#Recognize"><code>TextRecognizer.Recognize</code></a>を使用して、ユーザーのテキスト入力を処理することもできます。</p>
</div>
