# 用語および略語

<div class="note">
  <p><strong>メモ</strong></p>
  <p>このページは随時更新されます。</p>
</div>

### CEK
[Clova Extensions Kit](#CEK)の略語

### CIC
[Clova Interface Connect](#CIC)の略語

### CIC API {#CICAPI}
CICがクライアントに提供するREST APIです。クライアントは、CIC APIを使用してClovaと情報を交換します。

### Clova {#Clova}
[Clova](http://clova.ai)は、{{ book.TargetServiceForClientAuth }}が開発およびサービスを提供しているAIプラットフォームです。ユーザーの音声やイメージを認識し、それを解析して、ユーザーの希望する情報やサービスを提供します。サードパーティの開発者は、Clovaの持つ技術を活用して、AIサービスを提供するデバイスまたは家電製品を制作できます。また、Clovaを利用して、保有しているコンテンツやサービスを提供することもできます。

### Clovaアクセストークン {#ClovaAccessToken}
クライアントが[Clova Interface Connect](#CIC)で[イベント](#Event)を送る際、Clovaがクライアントを認証する手段です。詳細については、[Clovaアクセストークンを生成する](/CIC/Guides/Interact_with_CIC.md#CreateClovaAccessToken)ドキュメントを参照してください。

### Clova Developer Console {#ClovaDeveloperConsole}
Clovaプラットフォームと連携するクライアントデバイス、または[Clova extension](#ClovaExtension)を開発する開発者に次の内容を提供する<a target="_blank" href="https://developers.naver.com/console/clova/">ウェブツール</a>です。
* クライアントデバイスの登録およびクライアントの認証情報を提供(今後サービス予定)
* Clova extensionの[登録](/DevConsole/Guides/CEK/Register_Extension.md)および[配布](/DevConsole/Guides/CEK/Deploy_Extension.md)
* [Interaction modelの登録](/DevConsole/Guides/CEK/Register_Interaction_Model.md)
* Clovaサービスに関する統計資料の提供(今後サービス予定)

### Clova extension {#ClovaExtension}
音楽、ショッピング、金融などの外部のサービス(サードパーティサービス)、または家庭のIoTデバイスの制御など、Clovaの機能を拡張して、ユーザーに様々な経験を提供するウェブアプリケーションです。通常、extensionと呼ばれます。Clovaプラットフォームは、現在次の2種類のClova extensionをサポートおよび提供しています。エンドユーザーには、「拡張サービス」という表現で提供されます。
* [Custom extension](#CustomExtension)
* [Clova Home extension](#ClovaHomeExtension)

### Clova Extensions Kit(CEK) {#CEK}
Clova extensionを開発および配布する際に、必要なツールとインターフェースを提供するプラットフォームです。[Clovaとextensionのコミュニケーション](/CEK/CEK_Overview.md)をサポートしています。

### Clova Home extension {#ClovaHomeExtension}
IoTデバイス制御サービスを提供するためのextensionです。詳細については、[Clova Home extensionを作成する](/CEK/Guides/Build_Clova_Home_Extension.md)ドキュメントを参照してください。

### Clova Home extensionのメッセージ {#ClovaHomeExtMessage}
IoTデバイスを制御する[Clova Home extension](#ClovaHomeExtension)が[Clova Extensions Kit](#CEK)と情報のやり取りをする際、専用で使用するメッセージです。詳細については、[Clova Home extensionのメッセージ](/CEK/References/CEK_API.md#ClovaHomeExtMessage)ドキュメントを参照してください。

### Clova Interface Connection(CIC) {#CIC}
AIアシスタントサービスを提供するパソコン/モバイルアプリ、モバイルデバイスまたは家電製品などのクライアントに、Clovaとの連携ができるインターフェースを提供するプラットフォームです。詳細については、[CICの概要](/CIC/CIC_Overview.md)ドキュメントを参照してください。

### Clovaアプリ {#ClovaApp}

{{ book.OrientedService }}が開発し、iOSおよびAndroidプラットフォームで配布したClovaアプリです。Clovaに指示を与えるだけでなく、Clovaデバイスを登録し、管理できるアプリです。

### Clova認証API {#ClovaAuthAPI}
クライアントが[Clovaアクセストークン](#ClovaAccessToken)を取得するために使用するAPIです。詳細については、[Clova認証API](/CIC/References/Clova_Auth_API.md)ドキュメントを参照してください。

### コンテンツテンプレート {#ContentTemplate}
CICから渡されるコンテンツ情報をスケジュールカテゴリに合った形で標準化したものです。詳細については、[コンテンツテンプレート](/CIC/References/Content_Templates.md)ドキュメントを参照してください。

### コンテクストオブジェクト {#ContextObjects}
クライアントの現在の[コンテクスト](#Context)を表現するオブジェクトです。詳細については、[コンテクスト](/CIC/References/Context_Objects.md)ドキュメントを参照してください。

### Custom extension {#CustomExtension}
任意の拡張された機能を提供する[extension](#ClovaExtension)です。Custom extensionを利用すると、音楽、ショッピング、金融など、外部サービスの機能を提供できます。詳細については、[Custom extensionを作成する](/CEK/Guides/Build_Custom_Extension.md)ドキュメントを参照してください。

### Custom extensionのメッセージ {#CustomExtMessage}
[Clova Extensions Kit](#CEK)と[custom extension](#CustomExtension)が情報のやり取りをする際に使用するメッセージです。詳細については、[Custom extensionのメッセージ](/CEK/References/CEK_API.md#CustomExtMessage)ドキュメントを参照してください。

### Discovery機能 {#Discovery}
ユーザーアカウントに登録されたIoTデバイスのリストをクライアントデバイスに提供する機能です。詳細については、[Discoveryを提供する](/CEK/Guides/Build_Clova_Home_Extension.md#ProvideDeviceDiscovery)ドキュメントを参照してください。

### ダウンチャネル {#Downchannel}
クライアントが[Clova Interface Connect](#CIC)からディレクティブを渡される際に使用される[HTTP/2](#HTTP2)ストリームです。詳細については、[CICに接続する](/CIC/Guides/Interact_with_CIC.md#ConnectToCIC)ドキュメントを参照してください。

### Extension {#Extension}
[Clova extension](#ClovaExtension)の別の言い方

### Extensionストア {#ExtensionStore}

Extensionをユーザーに提供するために構築されたプラットフォームです。

### Extensionストアホーム {#ExtensionStoreHome}

Extensionストアに登録されたextensionが表示されるページです。Clovaアプリの**拡張サービス管理**メニューを指す用語です。

### Extensionページ {#ExtensionPage}

Extensionストアホーム(**拡張サービス管理**メニュー)で特定のextensionを選択すると表示されるページです。Extensionに関する詳しい説明が提供されます。

### HTTP/2 {#HTTP2}
HTTPプロトコルの2番目のバージョンです。[SPDY](https://en.wikipedia.org/wiki/SPDY)に基づき、インターネット技術タスクフォース(IETF)において開発されています。1997年にRFC 2068として規定されたHTTP/1.1をバージョンアップしたものであり、2014年12月にProposed Standard(標準への提唱)として制定され、2015年2月17日にIESGで正式な仕様として承認されました。2015年5月に[RFC 7540](https://tools.ietf.org/html/rfc7540)として公開されました。

### Intent {#Intent}
Clova extensionが処理するユーザーの意図を区分したカテゴリです。Custom intentとbuilt-in intentの2種類があります。[Custom extension](#CustomExtension)を実装する前に、まずintentの集合である[interaction model](#InteractionModel)を定義する必要があります。詳細については、[Interaction modelを定義する](/Design/Design_Guideline_For_Extension.md#DefineInteractionModel)ドキュメントを参照してください。

### IntentRequest {#IntentRequest}

ユーザーのリクエストを解析した結果([Intent](#Intent))を[custom extension](#CustomExtension)に送る際に使用されるリクエストメッセージタイプです。詳細については、[Custom extensionでリクエストを処理する](/CEK/Guides/Build_Custom_Extension.md#HandleCustomExtensionRequest)ドキュメントを参照してください。

### Interaction model {#InteractionModel}
[Custom extension](#CustomExtension)が音声から認識されたユーザーのリクエストをextensionに送るために、標準化したフォーマット(JSON)に変換するルールを指定したものです。詳細については、[Interaction model](/Design/Design_Guideline_For_Extension.md#DefineInteractionModel)ドキュメントを参照してください。

### LaunchRequest {#LaunchRequest}
ユーザーが特定のモードまたは特定の[custom extension](#CustomExtension)を使用すると宣言したことを知らせるために送るリクエストメッセージです。詳細については、[Custom extensionでリクエストを処理する](/CEK/Guides/Build_Custom_Extension.md#HandleCustomExtensionRequest)ドキュメントを参照してください。

### OAuth 2.0
アクセス権限を委任するためのオープン標準です。インターネットのユーザーが他のウェブサービスやアプリケーションのユーザーアカウントにアクセスできる権限を付与する規約です。Clovaプラットフォームでは、クライアントが[Clovaアクセストークン](#ClovaAccessToken)を取得したり、ユーザーが特定のextensionを使用する際、自身の[アカウントをリンク](/CEK/Guides/Link_User_Account.md)するために使用されます。詳細については、[https://tools.ietf.org/html/rfc6749](https://tools.ietf.org/html/rfc6749)を参照してください。

### SessionEndedRequest {#SessionEndedRequest}
ユーザーが特定のモードまたは特定の[custom extension](#CustomExtension)の使用を中止すると宣言したことを知らせるために送るリクエストメッセージです。詳細については、[Custom extensionでリクエストを処理する](/CEK/Guides/Build_Custom_Extension.md#HandleCustomExtensionRequest)ドキュメントを参照してください。

### Slot {#Slot}
[Intent](#Intent)に宣言されたリクエストを処理する際に必要な情報です。Intentを定義するとき、共に定義する必要があります。Clovaはユーザーのリクエストを解析して、slotに該当する情報を抽出します。詳細については、[Interaction modelを定義する](/Design/Design_Guideline_For_Extension.md#DefineInteractionModel)ドキュメントを参照してください。

### ダイアログID {#DialogID}
ダイアログIDは、ユーザーが新しい発話を開始するたびに生成され、クライアントが[Recognize](/CIC/References/CICInterface/SpeechRecognizer.md#Recognize)[イベント](#Event)を[Clova Interface Connect](#CIC)に渡す際に含まれます。ダイアログIDは、サーバー側からレスポンスを返す際に、どのイベントに対するレスポンスか結び付けるために使用され、[ディレクティブ](#Directive)にも含まれます。クライアントはディレクティブに含まれたダイアログIDから、どのイベントに対するレスポンスかを判断する必要があります。もしクライアントが現在持っているダイアログIDとディレクティブのダイアログIDが異なる場合、受信したディレクティブを無視する必要があります。詳細については、[ダイアログモデル](/CIC/CIC_Overview.md#DialogModel)ドキュメントを参照してください。

### コンテクスト {#Context}
コンテクストは、クライアントの様々な状態を意味します。[コンテクストオブジェクト](#ContextObjects)として表現されます。詳細については、[コンテクスト](/CIC/References/Context_Objects.md)ドキュメントを参照してください。

### メッセージID {#MessageID}
メッセージIDは個々のメッセージを区別するための識別子です。[イベント](#Event)と[ディレクティブ](#Directive)は、それぞれのメッセージIDを持ちます。

### アカウントリンク {#AccountLinking}
[Extension](#ClovaExtension)がユーザーのアカウント認証を必要とする外部サービスを提供する際に使用されます。詳細については、[ユーザーアカウントをリンクする](/CEK/Guides/Link_User_Account.md)ドキュメントを参照してください。

### ユーザーのサンプル発話 {#UserUtteranceExample}

ユーザーのリクエスト発話がどのように入力されるかを例で表現したリストです。[Intent](#Intent)ごとに複数の例を定義できます。また、例には[slot](#Slot)が表示されます。詳細については、[Interaction modelを定義する](/Design/Design_Guideline_For_Extension.md#DefineInteractionModel)ドキュメントを参照してください。

### セッションID {#SessionID}
[Extension](#ClovaExtension)がユーザーリクエストのコンテクストを区分するためのセッション識別子です。通常、一回性のユーザーリクエストはそのたびにセッションIDが変わりますが、特定のモードや連続的な(マルチターン)ユーザーリクエストの場合、同じセッションIDを持ちます。このセッションIDは、[Clova Extensions Kit](#CEK)がextensionにユーザーのリクエストを渡すとき生成されます。セッションIDが維持されるのは、[LaunchRequest](#LaunchRequest)のようなリクエストを受け取ったか、またはextensionが必要に応じて`response.shouldEndSession`フィールドを`false`に設定した場合です。詳細については、[Custom extensionを作成する](/CEK/Guides/Build_Custom_Extension.md)ドキュメントを参照してください。

### イベント(Event) {#Event}
クライアントから[Clova Interface Connect](#CIC)に渡すメッセージです。ユーザーのリクエストを渡したり、またはクライアントの状態が変更されたことを知らせるためにこのメッセージを送信します。

### ディレクティブ(Directive) {#Directive}
[Clova Interface Connect](#CIC)がクライアントのアクションを制御するように指定したメッセージです。ディレクティブはクライアントがリクエストしたイベントに応答したり、特定の条件によってクライアントに情報を渡す際に使用されます。

### クライアントの認証情報 {#ClientCredentialInfo}
[Clova Developer Console](#ClovaDeveloperConsole)でクライアントを登録し、取得した認証情報です。[Clovaアクセストークン](#ClovaAccessToken)の取得に使用されます。詳細については、[Clovaアクセストークンを生成する](/CIC/Guides/Interact_with_CIC.md#CreateClovaAccessToken)ドキュメントを参照してください。
