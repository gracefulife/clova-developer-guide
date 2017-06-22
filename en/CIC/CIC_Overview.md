# CIC overview
This document explains Clova Interface Connect (hereinafter CIC) in detail. It will help you understand what CIC is and how it works, and provides you with the guides and references for CIC.

## What is CIC? {#WhatisCIC}
CIC is a platform that serves as an interface to Clova, allowing your client to connect to Clova. It supports various types of clients which aim to provide an AI assistant service, including PC/mobile app, mobile device, or home electronics. CIC provides [CIC APIs](/CIC/References/CIC_API.md) with which your client can send user requests to Clova and delivers responses from Clova to your client.

![](/CIC/Resources/Images/CIC_Interaction_Structure.png)

## CIC interaction structure {#CICInteractionStructure}
Basically, your client uses the CIC APIs to send a user request to CIC and receive a response from CIC. All communications with CIC is done over the HTTP/2 protocol. The [CIC APIs](/CIC/References/CIC_API.md) provide various functionalities such as speech recognition, speech synthesis, music playback, personal schedule management, and alarm/timer setup.

Various communications occur between your client and CIC through these CIC APIs. Depending on which way a message is directed to, the message type can be either one of the following.

* [Event message](/CIC/References/CIC_Message_Format.md#Event): This type of message is sent from your client to CIC. It is sent to deliver a user request (speech input) or to notify that your client state has changed.

* [Directive message](/CIC/References/CIC_Message_Format.md#Directive): This type of message is sent from CIC to your client to control the behavior of the client. For example, a Directive message may ask your app to display certain information or speak synthesized speech output. A Directive message is sent when:
    * CIC needs to instruct a client to do a specific action after recognizing the user's speech input. This type of Directive message is sent to respond to a user request.
    * Certain conditions require CIC to send a Directive message to a client although there is no preceding user request.

This sequence diagram shows how CIC and a client send and receive messages between them.

![](/CIC/Resources/Images/CIC_Interaction_Example_in_Sequence_Diagram.png)