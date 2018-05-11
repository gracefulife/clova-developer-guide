# CICと連携する
ユーザーがClovaサービスを使用するには、クライアント(アプリまたはデバイス)がCICのインターフェースを使って、ユーザーのリクエストや状況をClovaに送信します。クライアントの開発者は、クライアントがCICとどのように接続して、どのようなメッセージをやり取りし、その際、どのような作業を処理するかについて知っておく必要があります。

このドキュメントでは、次の内容について説明します。

1. [準備事項](#Preparation)
2. [CICに接続する](#ConnectToCIC)
3. [イベントを送信する](#SendEvent)
4. [ディレクティブを処理する](#HandleDirective)

また、開発者は次の内容を理解して、実装する必要があります。
* [メッセージキューを管理する](#ManageMessageQ)
* [委任されたユーザーのリクエストを処理する](#HandleDelegation)

{% include "/CIC/Guides/InteractWithCIC/Preparation.md" %}

{% include "/CIC/Guides/InteractWithCIC/Connect_to_CIC.md" %}

{% include "/CIC/Guides/InteractWithCIC/Send_Event.md" %}

{% include "/CIC/Guides/InteractWithCIC/Handle_Directive.md" %}

{% include "/CIC/Guides/InteractWithCIC/Manage_Message_Q.md" %}

{% include "/CIC/Guides/InteractWithCIC/Handle_Delegation.md" %}
