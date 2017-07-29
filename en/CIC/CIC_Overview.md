# CIC overview
This documentation explains Clova Interface Connect (hereinafter CIC) in detail. It will help you understand what CIC is and how it works, and provides you with the guides and references for CIC.

## What is CIC? {#WhatisCIC}
CIC is a platform that serves as an interface between Clova and a client aiming to provide AI assistant services, such as PC/mobile apps, mobile devices or home appliances. CIC provides [CIC APIs](/CIC/References/CIC_API.md) with which clients can send user requests to Clova and Clova can return responses to clients.

![](/CIC/Resources/Images/CIC_Interaction_Structure.png)

## CIC interaction structure {#CICInteractionStructure}
Your client uses the CIC APIs to send user requests to CIC and receive responses from CIC. All communications with CIC is done over the [HTTP/2 protocol](https://tools.ietf.org/html/rfc7540). The [CIC APIs](/CIC/References/CIC_API.md) provide functions such as speech recognition, speech synthesis for audio output, music playback, personal schedule management, and alarm/timer setup.

Various communications occur between a client and CIC through these CIC APIs. Depending on which way a communication is directed to, the message type can be either one of the following.

* [Event message](/CIC/References/CIC_Message_Format.md#Event): Messages that your client sends to CIC. Event messages send user requests (speech input) or notify that client state has changed.

* [Directive message](/CIC/References/CIC_Message_Format.md#Directive): Messages that CIC returns to control the behavior of your client. For example, a directive message can instruct an app to display certain information or generate synthesized speech. A directive message is returned in the following situations.
    * CIC returns a response message for a user request, after recognizing user's speech input, to instruct your client to do a specific action.
    * CIC sends a directive message to your client when it did not receive any user request but certain conditions were met.

This sequence diagram shows how CIC and a client send and receive messages.

![](/CIC/Resources/Images/CIC_Interaction_Example_in_Sequence_Diagram.png)