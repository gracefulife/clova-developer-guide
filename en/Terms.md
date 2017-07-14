# Terms and abbreviations

<div class="note">

<p><strong>Note!</strong></p>  <p>This page is updated on an ongoing basis.</p>
</div>

### Account Linking {#AccountLinking}
Used by an [extension](#ClovaExtension) to authenticate a user account to provide a 3rd party service. See [Linking user account](/CEK/Guides/LinkUserAccount.md) for more details.

### CEK
The abbreviation of [Clova Extension Kit](#CEK)

### CIC
The abbreviation of [Clova Interface Connect](#CIC)

### CIC API {#CIC API}
The format for [event messages](#Event) and [directive messages](#Directive) which are categorized into namespaces by the functionalities of Clova. See [CIC API](/CIC/References/CIC_API.md) for more details.

### CIC message {#CIC Message}
The [event messages](#Event) and [directive messages](#Directive) which are used by a client and [Clova Interface Connect](#CIC) to send and receive data.

### Client credentials {#ClientCredentialInfo}
Credential information obtained by registering a client in [Clova Developer Console](#ClovaDeveloperConsole). It is used to obtain a [Clova access token](#ClovaAccessToken). See [Creating Clova access token](/CIC/Guides/Interact_with_CIC.md#CreateClovaAccessToken) for more details.

### Clova {#Clova}
[Clova](http://clova.ai) is an AI (artificial intelligence) platform developed and serviced by {{ book.TargetServiceForClientAuth }}. Clova recognizes user's speech input or images, analyzes them, and provides information or service as requested by the user. 3rd party developers, by leveraging the Clova technologies, can make a device or home appliance that provides an AI service. They can also offer their content or services to users through Clova.

### Clova access token {#ClovaAccessToken}
A means used by Clova to authorize a client when the client tries to send an [event message](#Event) to [Clova Interface Cconnect](#CIC). See [Creating Clova access token](/CIC/Guides/Interact_with_CIC.md#CreateClovaAccessToken) for more details.

### Clova Developer Console {#ClovaDeveloperConsole}
The web tool that provides the following features for a client device that interacts with the Clova platform or for developers who build [Clova extension](#ClovaExtension).
* Registration of a client device and client credentials
* Registration and deployment of a Clova extension
* Registration of an interaction model
* Statistics related to Clova services

<div class="note">

<p><strong>Note!</strong></p>  <p>Clova Developer Console is still under development. Contact your counterpart contact personnel to ask for help with Clova Developer Console.</p>
</div>

### Clova extension {#ClovaExtension}
The web application that provides extended capabilities for Clova to enable users to access 3rd party services such as music, shopping, banking or control their home IoT devices. It is commonly called an extension and the Clova platform currently supports and provides the two types of Clova extensions.
* [Custom extension](#CustomExtension)
* [Clova Home extension](#ClovaHomeExtension)

### Clova Extension Kit (CEK) {#CEK}
The platform that provides the necessary tools and interfaces for developing a Clova extension. It supports [communication between Clova and extension](/CEK/CEK_Overview.md).

### Clova Home API {#ClovaHomeAPI}
The API used to control IoT devices. It uses the [Clova Home extension message](#ClovaHomeExtensionMessage) format. See [Clova Home API](/CEK/References/Clova_Home_API.md) for more details.

The API provides a format for [event message](#Event) or [directive message](#Directive) which are categorized into namespaces by the functionalities of Clova. See [CIC API](/CIC/References/CIC_API.md) for more details.

### Clova Home extension {#ClovaHomeExtension}
The extension that provides a service for controlling IoT devices. See [Building Clova Home extension](/CEK/Guides/Build_Clova_Home_Extension.md) for more details.

### Clova Home extension message {#ClovaHomeExtensionMessage}
A message used by a [Clova Home extension](#ClovaHomeExtension) when communicating information with [Clova Extensino Kit](#CEK) to control IoT devices. See [Clova Home extension message](/CEK/References/Clova_Home_Extension_Message_Format.md) for more details.

### Clova Interface Connection (CIC) {#CIC}
The platform that serves as an interface to Clova. It supports various types of clients which aim to provide an AI assistant service, including PC/mobile app, mobile device, or home appliances. See [CIC overview](/CIC/CIC_Overview.md) for more details.

### Clova Auth API {#ClovaAuthAPI}
The API used by a client to obtain a [Clova access token](#ClovaAccessToken). See [Clova Auth API](/CIC/References/Clova_Auth_API.md) for more details.

### Content Template {#ContentTemplate}
A standardized format for displaying content sent through CIC. See [Content Template](/CIC/References/Content_Templates.md) for more details.

### Context information {#Context}
Context indicates various states information of a client, using [context objects](#ContextObjects). See [Context information](/CIC/References/Context_Objects.md) for more details.

### Context Objects {#ContextObjects}
Objects that display [context information](#Context). See [Context information](/CIC/References/Context_Objects.md) for more details.

### Custom extension {#CustomExtension}
An [extension](#ClovaExtension) that provides extended capabilities. A custom extension lets you provide 3rd party services such as music, shopping or banking. See [Building custom extension](/CEK/Guides/Build_Custom_Extension.md) for more details.

### Custom extension message {#CustomExtensionMessage}
A message used by [Clova Extension Kit](#CEK) and [custom extension](#CustomExtension) to send and receive information. See [Custom extension message](/CEK/References/Custom_Extension_Message_Format.md) for more details.

### Device discovery {#Discovery}
A discovery feature that provides a client device with a list of IoT devices that are registered to a user account. See [Device discovery](/CEK/Guides/Build_Clova_Home_Extension.md#ProvideDeviceDiscovery) for more details.

### Dialogue ID {#DialogueID}
A dialogue ID is a dialogue identifier for distinguishing contexts of a user's spoken request. Users can have a logical dialogue with Clova and a single dialogue can have multiple [messages](#MessageID). Generally, each one-time request have its own unique dialogue ID and a dialogue consisting of multi-turn requests have the same dialogue ID. A dialog ID is created when a client sends an [event message](#Event) to [Clova Interface Cconnect](#CIC). It is also included in a [directive message](#Directive) which is returned as a response, and the client uses it to determine which event message this directive message is responding to.

### Directive message (Directive) {#Directive}
A message sent from [Clova Interface Cconnect](#CIC) to control the behavior of a client. A directive message is used to respond to an event message from a client or to send information to a client under certain conditions.


### Downchannel {#Downchannel}
A downchannel is an [HTTP/2](#HTTP2) stream used when a client receives a directive message from [Clova Interface Cconnect](#CIC). See [Connecting with CIC](/CIC/Guides/Interact_with_CIC.md#ConnectToCIC) for more details.

### Event message (Event) {#Event}
A message sent from a client to [Clova Interface Cconnect](#CIC). The message is used to send a user request (speech input) or to notify that a client state has changed.

### Extension
Another name for [Clova extension](#ClovaExtension).

### HTTP/2 {#HTTP2}
The second version of HTTP protocol. It is based on [SPDY](https://en.wikipedia.org/wiki/SPDY) and developed by Internet Engineering Task Force (IETF). It is the enhanced version of HTTP 1.1, which was standardized in RFC 2068 in 1997. It was presented as a Proposed Standard in December 2014 and approved by IESG as Proposed Standard on February 17, 2015. It was published as [RFC 7540](https://tools.ietf.org/html/rfc7540) in May 2015.

### Intent {#Intent}
The specification that defines different types of user requests. A [custom extension](#CustomExtension) requires its own [interaction model](#InteractionModel) consisting of a set of intents. See [Interaction model](/CEK/Guides/Build_Custom_Extension.md#InteractionModel) for more details.

### IntentRequest {#IntentRequest}

A request message used to send analysis details of a user request ([Intent](#Intent)) to a [custom extension](#CustomExtension). See [Handling custom extension request](/CEK/Guides/Build_Custom_Extension.md#HandleCustomExtensionRequest) for more details.

### Interaction model {#InteractionModel}
A schema that standardizes each type of request that will be sent to a [custom extension](#CustomeExtension). See [Interaction model](/CEK/Guides/Build_Custom_Extension.md#InteractionModel) for more details.

### LaunchRequest {#LaunchRequest}
A request message used to notify that a user has requested to start a particular mode or [custom extension](#CustomExtension). See [Handling custom extension request](/CEK/Guides/Build_Custom_Extension.md#HandleCustomExtensionRequest) for more details.

### Message ID {#MessageID}
A message ID is an identifier for distinguishing each message in a [dialogue](#DialogueID). Assume a dialogue of ordering pizzas and asking weather. The dialogues and messages can be identified as follows.
* Dialogue 1, message 1: Order pizza.
* Dialogue 1, message 2: How many pizza do you want to order?
* Dialogue 1, message 3: Two pizzas.
* Dialogue 1, message 4: Order has been made.
* Dialogue 2, message 1: How is the weather today?
* Dialogue 2, message 2: It's sunny today.

### OAuth 2.0
A public standard for delegation of access permission. The protocol allows internet users to grant account access permission to other web services or applications. On the Clova platform, it is used for [account linking](/CEK/Guides/LinkUserAccount.md) when a client obtains a [Clova access token](#ClovaAccessToken) or a user uses a particular extension. See [https://tools.ietf.org/html/rfc6749](https://tools.ietf.org/html/rfc6749) for more details.

### SessionEndedRequest {#SessionEndedRequest}
A request message used to notify that a user has requested to end a particular mode or [custom extension](#CustomExtension). See [Handling custom extension request](/CEK/Guides/Build_Custom_Extension.md#HandleCustomExtensionRequest) for more details.

### Slot {#Slot}
Information necessary for processing a request declared in an [intent](#Intent). It must be defined together when defining an *intent*. Clova analyzes a user request and extracts information related to slots. See [Interaction model](/CEK/Guides/Build_Custom_Extension.md#InteractionModel) for more details.

### User speech example {#UserUtteranceExample}

The list of examples showing how user's spoken request can be put in. You can define several example sentences for each [intent](#Intent). Example sentences are denoted with [slots](#Slot). See [Context information](/CIC/References/Context_Objects.md) for more details.

### Session ID {#SessionID}
A session ID is a session identifier used by an [extension](#ClovaExtension) to distinguish contexts of a user request. Generally, each one-time request has a unique session ID, and a particular mode (Freetalk, for example) or multi-turn requests have the same session ID. A session ID is created when [Clova Extension Kit](#CEK) sends a user request to an extension. A same session ID is maintained when a request such as [LaunchRequest](#LaunchRequest) is received or when an extension sets the *response.shouldEndSession* field to **false**. See [Building custom extension](/CEK/Guides/Build_Custom_Extension.md) for more details.
