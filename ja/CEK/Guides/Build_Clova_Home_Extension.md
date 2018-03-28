# Clova Home Extensionを作成する

Clova Home Extensionは、外部のIoTサービスを利用して、家庭内のIoTデバイスに遠隔操作機能を提供するExtensionです。Clova Home Extensionは、ユーザーが操作できるIoTデバイスの情報をCEKに提供する必要があります。また、CEKからIoTデバイス操作のリクエストを受け取り、それを処理して結果を返す必要があります。以下の図は、Clova Home Extensionの仕組みを示しています。

![](/CEK/Resources/Images/CEK_Clova_Home_Extension_Operation_Structure.png)

Clova Home Extensionを作成する際の事前準備と、Custom ExtensionがCEKとどのようなメッセージをやり取りし、どのように動作するかについて説明します。

Clova Home Extensionの開発者は、次の内容を知っておく必要があります。

1. [準備事項](#Preparation)
2. [Discovery機能を提供する](#ProvideDeviceDiscovery)
3. [Clova Home Extensionリクエストを処理する](#HandleClovaHomeExtensionRequest)
4. [Clova Home Extensionレスポンスを返す](#ReturnClovaHomeExtensionResponse)

{% include "/CEK/Guides/BuildClovaHomeExtension/Preparation.md" %}

{% include "/CEK/Guides/BuildClovaHomeExtension/Provide_Device_Discovery.md" %}

{% include "/CEK/Guides/BuildClovaHomeExtension/Handle_Clova_Home_Extension_Request.md" %}

{% include "/CEK/Guides/BuildClovaHomeExtension/Return_Clova_Home_Extension_Response.md" %}
