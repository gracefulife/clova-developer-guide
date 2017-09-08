# Building Clova Home extension

Clova Home extension lets you provide remote control capabilities for home IoT devices through a 3rd party service. Clova Home extensions must provide CEK with information on which IoT devices are controllable by a user. Also, when it receives IoT device control requests from CEK, it must perform appropriate actions and return results. This picture shows how a Clova Home extension works.

![](/CEK/Resources/Images/CEK_Clova_Home_Extension_Operation_Structure.png)

The following explains what preparations are required before you start building your Clova Home extension, and which messages your extension exchanges with CEK and how it performs necessary actions during the process.

The following topics provide essential information for building a Clova Home extension.

1. [Preparation](#Preparation)
2. [Providing device discovery](#ProvideDeviceDiscovery)
3. [Handling Clova Home extension request](#HandleClovaHomeExtensionRequest)
4. [Returning Clova Home extension response](#ReturnClovaHomeExtensionResponse)

{% include "./BuildClovaHomeExtension/Preparation.md" %}

{% include "./BuildClovaHomeExtension/Provide_Device_Discovery.md" %}

{% include "./BuildClovaHomeExtension/Handle_Clova_Home_Extension_Request.md" %}

{% include "./BuildClovaHomeExtension/Return_Clova_Home_Extension_Response.md" %}
