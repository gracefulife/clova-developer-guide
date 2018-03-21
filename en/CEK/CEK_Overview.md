# CEK Overview
This documentation provides detailed description on Clova Extensions Kit (hereinafter referred to as ‘CEK’). You can use the documentation together with the CEK guides and references to understand how CEK operates.

## What is CEK? {#WhatisCEK}
CEK is a platform that provides tools and interfaces for developing and deploying a Clova extension (hereinafter referred to as 'extension'). It supports communication between Clova and extensions. An extension is a Web application that provides extended capabilities to Clova for a more diverse user experience, including the capability to control IoT appliances at home or 3rd party services, such as music, shopping, and banking services.

![](/CEK/Resources/Images/CEK_Concept_Diagram.png)

CEK provides the following features:
* [Interaction model](/Design/Design_Guideline_For_Extension.md#DefineInteractionModel) management (provided by the [Clova developer console](/DevConsole/ClovaDevConsole_Overview.md))
* Interface between Clova and extension

## CEK interaction structure {#CEKInteractionStructure}
Clova recognizes user utterances input from CIC and analyzes it via the [interaction model](/DevConsole/Guides/CEK/Register_Interaction_Model.md) registered in CEK. CEK delivers the analyzed user utterance information to the extension, and the extension must return the processed result of user request as a response. At this time, the messages are exchanged according to the predefined message format. The communication between CEK and the extension must use the <a href="https://tools.ietf.org/html/rfc2616" target="_blank">HTTP/1.1 protocol</a>.

The diagram below shows the operating structure between the Clova platform and extension.

![](/CEK/Resources/Images/CEK_Interaction_Structure.png)


## Extension types {#ExtensionType}
The Clova platform currently supports and provides two types of extensions as follows:

* [Custom extension](/CEK/Guides/Build_Custom_Extension.md): An extension that provides tailored extended functions. A custom extension lets you provide 3rd party services, such as music, shopping, or banking services.
* [Clova Home extension](/CEK/Guides/Build_Clova_Home_Extension.md): An extension that provides a service for controlling IoT appliances.

