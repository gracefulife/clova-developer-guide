# Custom Extensionを作成する

Custom Extensionとは、Clovaがビルトインで提供している機能やサービスではなく、開発者が拡張した機能や、外部のサービスを提供するExtensionです。例えば、ウェブ検索やニュースクリッピングなどのサービスだけでなく、ユーザーアカウント認証の必要な音楽、ショッピングなどの外部サービスを提供することができます。Custom Extensionは、解析されたユーザーの発話情報をCEKから受け取り、その内容を処理して、サービスの処理結果を返す必要があります。このドキュメントでは、Custom Extensionを作成する際の準備事項と、Custom ExtensionがCEKとどのようなメッセージのやり取りをして、どのように動作する必要があるかについて説明します。

Custom Extensionの開発者は、次の内容を知っておく必要があります。

1.[準備事項](#Preparation)
2.[Custom Extensionリクエストを処理する](#HandleCustomExtensionRequest)
   * [`LaunchRequest`リクエストを処理する](#HandleLaunchRequest)
   * [`IntentRequest`リクエストを処理する](#HandleIntentRequest)
   * [`SessionEndedRequest`リクエストを処理する](#HandleSessionEndedRequest)
3.[Custom Extensionレスポンスを返す](#ReturnCustomExtensionResponse)
4.[マルチターン対話をする](#DoMultiturnDialog)

{% include "/CEK/Guides/BuildCustomExtension/Preparation.md" %}

{% include "/CEK/Guides/BuildCustomExtension/Handle_Custom_Extension_Request.md" %}

{% include "/CEK/Guides/BuildCustomExtension/Return_Custom_Extension_Response.md" %}

{% include "/CEK/Guides/BuildCustomExtension/Do_Multiturn_Dialog.md" %}
