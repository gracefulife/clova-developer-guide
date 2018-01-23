# Terms and abbreviations

<div class="note">
  <p><strong>Note!</strong></p>
  <p>This page is updated on an ongoing basis.</p>
</div>

### Account Linking {#AccountLinking}
Used when an [extension](#ClovaExtension) provides a 3rd party service that requires users to authenticate their account. See [Linking user account](/CEK/Guides/Link_User_Account.md) for more details.

### CEK
The abbreviation of [Clova Extensions Kit](#CEK)

### CIC
The abbreviation of [Clova Interface Connect](#CIC)

### CIC API {#CIC API}
REST API which CIC provides to clients. Clients use CIC API to exchange information with Clova.

### Client credentials {#ClientCredentialInfo}
Credentials obtained by registering a client in the [Clova Developer Console](#ClovaDeveloperConsole). They are used to obtain [Clova access tokens](#ClovaAccessToken). See [Creating Clova access token](/CIC/Guides/Interact_with_CIC.md#CreateClovaAccessToken) for more details.

### Clova {#Clova}
[Clova](http://clova.ai) is an AI (artificial intelligence) platform developed and serviced by {{ book.TargetServiceForClientAuth }}. Clova recognizes user's speech or images, analyzes them, and provides information or services that users have requested. 3rd party developers, by leveraging the Clova technologies, can make a device or home appliance that provides an AI service. They can also offer their content or services to users through Clova.

### Clova access token {#ClovaAccessToken}
A means used by Clova to authorize a client when the client tries to send [event messages](#Event) to [Clova Interface Connect](#CIC). See [Creating Clova access token](/CIC/Guides/Interact_with_CIC.md#CreateClovaAccessToken) for more details.

### Clova Developer Console {#ClovaDeveloperConsole}
A [web tool](https://developers.naver.com/console/clova/) that provides the following features for development of a client device or [Clova extension](#ClovaExtension) that interacts with the Clova platform.
* Registering a client device and obtains client credentials
* Clova extension registration (/DevConsole/Guides/CEK/Register_Extension.md) and [deployment](/DevConsole/Guides/CEK/Deploy_Extension.md)
* [Registering an interaction model](/DevConsole/Guides/CEK/Define_Interaction_Model.md)
* Viewing statistics related to Clova services

### Clova extension {#ClovaExtension}
A web application that provides extended capabilities to Clova for more diverse user experience, including the capability of controlling IoT appliances at home or 3rd party services such as music, shopping, and banking. It is commonly called an extension and the Clova platform currently supports and provides two types of Clova extensions. To regular users, the extension is refered to as "an extension feature".
* [Custom extension](#CustomExtension)
* [Clova Home extension](#ClovaHomeExtension)

### Clova Extensions Kit (CEK) {#CEK}
A platform that provides tools and interfaces for development and deployment of a Clova extension. It supports [communication between Clova and extensions](/CEK/CEK_Overview.md).

### Clova Home extension {#ClovaHomeExtension}
An extension that provides a service for controlling IoT appliances. See [Building Clova Home extension](/CEK/Guides/Build_Clova_Home_Extension.md) for more details.

### Clova Home extension message {#ClovaHomeExtMessage}
Messages used by [Clova Home extensions](#ClovaHomeExtension) when they exchange information with [Clova Extensions Kit](#CEK) to control IoT appliances. See [Clova Home extension message](/CEK/References/CEK_API.md#ClovaHomeExtMessage) for more details.

### Clova Interface Connect (CIC) {#CIC}
A platform that serves as an interface between Clova and a client aiming to provide AI assistant services, such as PC/mobile apps, mobile devices or home appliances. See [CIC overview](/CIC/CIC_Overview.md) for more details.

### Clova Auth API {#ClovaAuthAPI}
An API used by clients to obtain [Clova access tokens](#ClovaAccessToken). See [Clova Auth API](/CIC/References/Clova_Auth_API.md) for more details.

### Content Template {#ContentTemplate}
Standardized formats for displaying content returned from CIC. See [Content template](/CIC/References/Content_Templates.md) for more details.

### Context objects {#ContextObjects}
Objects that express current [context information] of a client(#Context). See [Context information](/CIC/References/Context_Objects.md) for more details.

### Context information {#Context}
Context indicates various states of a client. It is expressed with [context objects](#ContextObjects). See [Context information](/CIC/References/Context_Objects.md) for more details.

### Custom extension {#CustomExtension}
An [extension](#ClovaExtension) that provides extended capabilities. A custom extension lets you provide 3rd party services such as music, shopping, or banking. See [Building custom extension](/CEK/Guides/Build_Custom_Extension.md) for more details.

### Custom extension message {#CustomExtMessage}
Messages used by [Clova Extensions Kit](#CEK) and [custom extensions](#CustomExtension) to exchange information. See [Custom extension message](/CEK/References/CEK_API.md#CustomExtMessage) for more details.

### Device discovery {#Discovery}
A feature that provides client devices with a list of IoT appliances registered to a user account. See [Providing device discovery](/CEK/Guides/Build_Clova_Home_Extension.md#ProvideDeviceDiscovery) for more details.

### Dialog ID {#DialogID}
A dialog ID is created every time a user initiates new speech input. It is included when clients send [Recognize](/CIC/References/CICInterface/SpeechRecognizer.md#Recognize) [event messages](#Event) to [Clova Interface Connect](#CIC). Dialog IDs are also included in [directive messages](#Directive) when responses are returned from a server side to map those responses to corresponding event messages. Clients check a dialog ID included in a directive message and determine which directive message is responding to which event message. If the dialog ID at the client side is different from that of the directive message, the directive message must be disregarded. See [Dialog model](/CIC/CIC_Overview.md#DialogModel) for more details.

### Directive message {#Directive}
Messages that sent from [Clova Interface Connect](#CIC) to control behavior of clients. Directive messages are used when CIC returns responses to event messages from clients, or when CIC sends information to clients under certain conditions.

### Downchannel {#Downchannel}
A downchannel is an [HTTP/2](#HTTP2) stream through which clients receive directive messages from [Clova Interface Connect](#CIC). See [Connecting with CIC](/CIC/Guides/Interact_with_CIC.md#ConnectToCIC) for more details.

### Extension
Another name for a [Clova extension](#ClovaExtension)

### Event message {#Event}
Messages that sent from clients to [Clova Interface Connect](#CIC). Event messages send user requests (speech input) or notify that a client state has changed.

### HTTP/2 {#HTTP2}
The second version of the HTTP protocol. It is based on [SPDY](https://en.wikipedia.org/wiki/SPDY) and developed by Internet Engineering Task Force (IETF). It is the enhanced version of HTTP 1.1, which was standardized in RFC 2068 in 1997. It was presented as a Proposed Standard in December 2014 and approved by IESG as Proposed Standard on February 17, 2015. It was published as [RFC 7540](https://tools.ietf.org/html/rfc7540) in May 2015.

### Intent {#Intent}
An intent is a segment that distinguishes the user requests for a Clova extension to handle. The intent is divided into two: a custom intent and a built-in intent. Before implementing a [custom extension](#CustomExtension), an [interaction model](#InteractionModel) consisting of a set of intents has to be defined. See [An interaction model](/DevConsole/Guides/CEK/Define_Interaction_Model.md) for more details.

### IntentRequest {#IntentRequest}
A type of request message that sends analysis details of a user request ([Intent](#Intent)) to a [custom extension](#CustomExtension). See [Handling custom extension request](/CEK/Guides/Build_Custom_Extension.md#HandleCustomExtensionRequest) for more details.

### Interaction model {#InteractionModel}
A model that defines a rule to convert to the standardized format (JSON) for [Custom extension](#CustomeExtension) to pass user's voice requests to extension.  See [An interaction model](/DevConsole/Guides/CEK/Create_Interaction_Model.md for more details.

### LaunchRequest {#LaunchRequest}
A type of request message that notifies that a user has requested to start a certain mode or [custom extension](#CustomExtension). See [Handling custom extension request](/CEK/Guides/Build_Custom_Extension.md#HandleCustomExtensionRequest) for more details.

### Message ID {#MessageID}
A message ID is an identifier for distinguishing individual messages. All [event messages](#Event) and [directive messages](#Directive) have their own message ID.

### OAuth 2.0
A public standard for delegation of access permission. The protocol allows internet users to grant account access right to other web services or applications. On the Clova platform, it is used for [account linking](/CEK/Guides/Link_User_Account.md) when clients try to obtain [Clova access tokens](#ClovaAccessToken) or users try to use a certain extension. Refer to [https://tools.ietf.org/html/rfc6749](https://tools.ietf.org/html/rfc6749) for more details.

### SessionEndedRequest {#SessionEndedRequest}
A type of request message that notifies that a user has requested to end a certain mode or [custom extension](#CustomExtension). See [Handling custom extension request](/CEK/Guides/Build_Custom_Extension.md#HandleCustomExtensionRequest) for more details.

### Session ID {#SessionID}
A session ID is a session identifier used by [extensions](#ClovaExtension) to distinguish context of user requests. Generally, a one-time request has a unique session ID whereas a particular mode or multi-turn request has a same session ID. A session ID is created when [Clova Extensions Kit](#CEK) sends a user request to an extension. A same session ID is maintained when requests such as [LaunchRequest](#LaunchRequest) are made or when an extension sets the `response.shouldEndSession` field to `false`. See [Building custom extension](/CEK/Guides/Build_Custom_Extension.md) for more details.

### Slot {#Slot}
Information necessary for processing a request declared in an [intent](#Intent). It must be defined in pair with the intent. Clova analyzes a user request and extracts information specific to slots. See [An interaction model](/DevConsole/Guides/CEK/Define_Interaction_Model.md) for more details.

### User speech example {#UserUtteranceExample}
A list of examples showing how user's spoken request can be put in. You can define several example sentences for each [intent](#Intent). Example sentences are denoted with [slots](#Slot). See [An interaction model](/DevConsole/Guides/CEK/Define_Interaction_Model.md) for more details.
