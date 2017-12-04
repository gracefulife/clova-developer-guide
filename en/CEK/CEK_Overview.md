# CEK overview
This documentation explains Clova Extensions Kit ('CEK' hereinafter) in detail. It will help you understand what CEK is and how it works, and provides you with the guides and references for CEK.

## What is CEK? {#WhatisCEK}
CEK is a platform that gives you access to tools and interfaces for developing Clova extensions ('extension' hereinafter). It supports communications between Clova and your extension. Extension is a web application that provides extended capabilities to Clova for more diverse user experience including the capability of controlling IoT appliances at home or 3rd party services such as music, shopping, banking and more.

![](/CEK/Resources/Images/CEK_Concept_Diagram.png)

CEK provides the following features.
* [Interaction model](/DevConsole/Guides/CEK/Define_Interaction_Model.md) management (Provide [Clova Developer Console](/DevConsole/ClovaDevConsole_Overview.md))
* Providing interfaces between Clova and your extension

## CEK interaction structure {#CEKInteractionStructure}
Clova receives user's speech input from CIC and recognizes it, and CEK analyzes the recognized speech using a pre-defined [interaction model](/DevConsole/Guides/CEK/Define_Interaction_Model.md). Following that, CEK sends analysis details of the user's speech to an extension and the extension returns processing results of the user request. During the process, messages are sent back and forth in a pre-defined format.

This diagram shows the interaction structure between the Clova platform and an extension.

![](/CEK/Resources/Images/CEK_Interaction_Structure.png)


## Extension type {#ExtensionType}
The Clova platform supports and provides two types of extensions as follows.

* [Custom extension](/CEK/Guides/Build_Custom_Extension.md): An extension that provides extended capabilities. A custom extension lets you provide 3rd party services such as music, shopping, or banking.
* [Clova Home extension](/CEK/Guides/Build_Clova_Home_Extension.md): An extension that provides a service for controlling IoT devices.
