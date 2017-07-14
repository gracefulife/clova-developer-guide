# CEK overview
This documentation explains Clova Extension Kit (hereinafter CEK) in detail. It will help you understand what CEK is and how it works, and provides you with the guides and references for CEK.

## What is CEK? {#WhatisCEK}
Clova extension is a web application that provides extended capabilities for Clova. By providing Clova extensions, you can let your users access 3rd party services such as music, shopping, banking or control their home IoT devices through Clova, assuring more diverse user experience. CEK is a platform that helps you develop your own extension by providing all the necessary tools and interfaces. It also handles communication between Clova and your extension.

![](/CEK/Resources/Images/CEK_Concept_Diagram.png)

CEK provides the following features.
* Managing your interaction model (provided in Clova Developer Console)
* Providing interfaces between Clova and your extension

<div class="note">
  <p><strong>Note!</strong></p>
    <p>Clova Developer Console is still under development. Contact your counterpart contact personnel to ask for help with defining an interaction model.</p>
</div>

## CEK interaction structure {#CEKInteractionStructure}
Clova recognizes user's spoken request by receiving speech input from CIC and CEK analyzes the recognized speech input using a pre-defined [interaction model](/CEK/Guides/Build_Custom_Extension.md#InteractionModel). Following that, CEK sends analysis details of user's speech input to your extension and your extension returns processing results of the user request. All messages are exchanged in a pre-defined message format.

This diagram shows the interaction structure between the Clova platform and an extension.

![](/CEK/Resources/Images/CEK_Interaction_Structure.png)


## Extension type {#ExtensionType}
The Clova platform currently supports and provides two types of extensions.

* [Custom extension](/CEK/Guides/Build_Custom_Extension.md): An extension that provides extended capabilities of your own choosing. A custom extension lets you provide 3rd party services such as music, shopping or banking.
* [Clova Home extension](/CEK/Guides/Build_Clova_Home_Extension.md): An extension that provides a service for controlling IoT devices.
