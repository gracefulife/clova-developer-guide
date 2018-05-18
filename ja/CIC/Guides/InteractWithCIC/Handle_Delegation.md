## 委任されたユーザーのリクエストを処理する {#HandleDelegation}

ユーザーはClovaアプリを使用する際、リクエストの処理結果をClovaアプリではなく、ユーザーが持っている別のクライアントデバイスで処理するように指定することができます。例えば、Clovaアプリで特定のアーティストの曲を再生するとき、ユーザーのスマートフォンではなく、Clovaフレンズスピーカーで再生するようにリクエストすることができます。そのことを、Clovaアプリがユーザーのリクエストを別のクライアントデバイスに委任したといいます。

Clovaアプリがリクエストの処理を委任すると、委任されるクライアントがダウンチャネルで不意にディレクティブを受信します。次は、ユーザーがリクエストを委任する仕組みを示します。**次の説明のうち、委任されるクライアントの動作を実装する必要があります。**

![](/CIC/Resources/Images/CIC_Handle_Event_Delegation.png)

<ol>
  <li>Clovaアプリは、CICにユーザーのリクエストを送信する際、別のクライアントデバイスに委任を要求します。</li>
  <li>
    <p>CICは、リクエストの処理を委任されたクライアントデバイスに、次のような<a href="/CIC/References/CICInterface/Clova.html#HandleDelegatedEvent"><code>Clova.HandleDelegatedEvent</code></a>ディレクティブを<a href="/CIC/Guides/Interact_with_CIC.md#CreateConnection">ダウンチャネル</a>で送信します。<p>
    <pre><code>{
  "directive": {
    "header": {
      "messageId": "b17df741-2b5b-4db4-a608-85ecb1307b33",
      "namespace": "Clova",
      "name": "HandleDelegatedEvent"
    },
    "payload": {
      "delegationId": "99e86204-710a-4e94-b949-a763e78348a7"
    }
  }
}</code></pre>
  </li>
  <li>
    <p>クライアントは、委任されたリクエストの処理結果をCICから受け取るために、<a href="/CIC/References/CICInterface/Clova.html#ProcessDelegatedEvent"><code>Clova.ProcessDelegatedEvent</code></a>イベントをCICに送信する必要があります。その際、ステップ2で受け取った<code>delegationId</code>フィールドの値を、そのまま<code>payload</code>フィールドに入力します。</p>
    <pre><code>{
  "context": [
    ...
  ],
  "event": {
    "header": {
      "namespace": "Clova",
      "name": "ProcessDelegatedEvent",
      "messageId": "b120c3e0-e6b9-4a3d-96de-71539e5f6214"
    },
    "payload": {
      "delegationId": "99e86204-710a-4e94-b949-a763e78348a7"
    }
  }
}</code></pre>
  </li>
  <li>CICは、クライアントに<a href="/CIC/References/CICInterface/Clova.html#ProcessDelegatedEvent"><code>Clova.ProcessDelegatedEvent</code></a>イベントのレスポンスとして、ユーザーが委任したリクエストの処理結果を返します。</li>
  <li>クライアントは、通常の<a href="/CIC/Guides/Interact_with_CIC.html#HandleDirective">ディレクティブ</a>の処理と同じく、レスポンスとして受け取ったディレクティブを処理します。</li>
</ol>
