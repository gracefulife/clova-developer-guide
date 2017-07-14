# Building custom extension

A custom extension lets you provide extended capabilities or 3rd party services besides standard features and services of Clova. For example, you can build a custom extension that provides web searching service or news clipping service. You can also build a custom extension for a 3rd party service that requires user authentication such as music, shopping or banking. When CEK sends analysis details of user's speech input to your custom extension, your custom extension takes an appropriate action and returns processing results. This page explains what preparations are required before you start building your custom extension and how your extension can perform actions and exchange messages with CEK.

The following topics provide essential information for custom extension developers.

1. [Preparation](#Preparation)
2. [Handling custom extension](#HandleCustomExtensionRequest)
   * [Handling LaunchRequest](#HandleLaunchRequest)
   * [Handling IntentRequest](#HandleIntentRequest)
   * [Handling SessionEndedRequest](#HandleSessionEndedRequest)
3. [Returning custom extension response](#ReturnCustomExtensionResponse)

{% include "./BuildCustomExtension/Preparation.md" %}

{% include "./BuildCustomExtension/Handle_Custom_Extension_Request.md" %}

{% include "./BuildCustomExtension/Return_Custom_Extension_Response.md" %}