# CIC overview
This documentation explains Clova Interface Connect ('CIC' hereinafter) in detail. It will help you understand what CIC is and how it works, and provides you with the guides and references for CIC.

## What is CIC? {#WhatisCIC}
CIC is a platform that serves as an interface between Clova and a client aiming to provide AI assistant services, such as PC/mobile apps, mobile devices or home appliances. CIC provides [CIC APIs](/CIC/References/CIC_API.md) with which clients can send user requests to Clova and Clova can return responses to clients.

![](/CIC/Resources/Images/CIC_Interaction_Structure.png)

## CIC interaction structure {#CICInteractionStructure}
Clients use the CIC APIs to send user requests to CIC and receive responses from CIC. All communications with CIC is done over the [HTTP/2 protocol](https://tools.ietf.org/html/rfc7540). The [CIC APIs](/CIC/References/CIC_API.md) provide functions such as speech recognition, speech synthesis and generation of audio output, music playback, personal schedule management, and alarm/timer setup.

Various communications occur between clients and CIC through these CIC APIs. Depending on which way a communication is directed to, the message type can be either one of the following.

* [Event message](/CIC/References/CIC_Message_Format.md#Event): Messages that clients send to CIC. You send event messages to send user requests (speech input) or notify when client states have changed.

* [Directive message](/CIC/References/CIC_Message_Format.md#Directive): Messages that CIC returns to clients to control their behavior. For example, a directive message can instruct an app to display certain information or play synthesized speech. Directive messages are returned in the following situations.
  * When responding to user requests. Directive messages are returned to instruct clients to do specific actions after recognizing user's speech input (user intent).
  * When certain conditions require CIC to send directive messages to clients without any preceding user requests.

This sequence diagram shows how messages are sent back and forth between CIC and client.

![](/CIC/Resources/Images/CIC_Interaction_Example_in_Sequence_Diagram.png)