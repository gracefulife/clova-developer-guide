# Creating a custom extension

A custom extension is not a default function or service of Clova; it is a tailored extension developed by a developer or an extension providing a 3rd party service. For example, a custom extension not only provides services such as web search or news clippings, but also 3rd party services such as music, shopping, or financial services that require user account authentication. Custom extensions receive analyzed information of user utterances from CEK. It must also handle the corresponding details and return the results of handling the service. This section explains the prerequisites for creating a custom extension, the types of messages exchanged with CEK, and the method of operation.

The information is provided to the custom extension developers in the following order:

1. [Prerequisites](#Preparation)
2. [Handling a custom extension request](#HandleCustomExtensionRequest)
   * [Handling a `LaunchRequest`](#HandleLaunchRequest)
   * [Handling a `IntentRequest`](#HandleIntentRequest)
   * [Handling a `SessionEndedRequest`](#HandleSessionEndedRequest)
3. [Returning a custom extension response](#ReturnCustomExtensionResponse)
4. [Engaging in a multi-turn dialog](#DoMultiturnDialog)

{% include "/CEK/Guides/BuildCustomExtension/Preparation.md" %}

{% include "/CEK/Guides/BuildCustomExtension/Handle_Custom_Extension_Request.md" %}

{% include "/CEK/Guides/BuildCustomExtension/Return_Custom_Extension_Response.md" %}

{% include "/CEK/Guides/BuildCustomExtension/Do_Multiturn_Dialog.md" %}
