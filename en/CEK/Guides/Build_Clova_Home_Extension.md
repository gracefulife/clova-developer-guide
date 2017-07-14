# Building Clova Home extension

Clova Home extension lets you add remote control capabilities for home IoT devices to a 3rd party service. Clova Home extension must provide CEK with the information of IoT devices that are controllable by the user. Also, when it receives IoT device control requests from CEK, it must perform appropriate actions and return results. This picture shows how Clova Home extension works.

![](/CEK/Resources/Images/CEK_Clova_Home_Extension_Operation_Structure.png)

This page explains what preparations are required before you start building your Clova Home extension and how your extension can perform actions and exchange messages with CEK.

The following topics provide essential information for Clova Home extension developers.

1. [Preparation](#Preparation)
2. [Device discovery](#ProvideDeviceDiscovery)
3. [Handling Clova Home extension request](#HandleClovaHomeExtensionRequest)
4. [Returning Clova Home extension response](#ReturnClovaHomeExtensionResponse)

{% include "./BuildClovaHomeExtension/Preparation.md" %}

{% include "./BuildClovaHomeExtension/Provide_Device_Discovery.md" %}

{% include "./BuildClovaHomeExtension/Handle_Clova_Home_Extension_Request.md" %}

{% include "./BuildClovaHomeExtension/Return_Clova_Home_Extension_Response.md" %}