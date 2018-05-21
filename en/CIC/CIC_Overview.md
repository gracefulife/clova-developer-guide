# CIC overview
Learn what Clova Interface Connect (hereinafter referred to as "CIC") is and how it works. This document will help you understand how CIC operates and includes CIC guides and references.

## What is CIC? {#WhatisCIC}
CIC is a platform that serves as an interface between Clova and a client providing AI assistant services on computers, mobile apps, mobile devices, or home appliances. CIC provides the [CIC API](/CIC/References/CIC_API.md), with which clients can send user requests to Clova and Clova can return responses to clients.

![](/CIC/Resources/Images/CIC_Interaction_Structure.png)

## CIC interaction structure {#CICInteractionStructure}
Clients use the CIC API to send user requests to CIC and also to receive responses from CIC. All communications with CIC is made over the [HTTP/2 protocol](https://tools.ietf.org/html/rfc7540). The [CIC API](/CIC/References/CIC_API.md) provides interfaces for speech recognition, playing synthesized speech and music, calendar management, setting alarms/timers, and many other features.

Through the CIC API, various communications are made between clients and CIC in the form of messages. The message type depends on who the message sender is as follows.

* [Event](/CIC/References/CIC_API.md#Event): Messages that clients send to CIC. Send events to CIC to pass users voice requests (speech input) to CIC and to notify CIC when your client states have changed.

* [Directive](/CIC/References/CIC_API.md#Directive): Messages that CIC sends to clients to control client behavior. For example, a directive can instruct an app to display certain information or play synthesized speech. Directives are sent to clients when:
    * Responding to user requests. After recognizing user voice request (user intent), CIC returns directives to instruct clients to perform certain actions relevant to the user intent.
    * Certain conditions require CIC to send directives to clients without any preceding user requests.

The following sequence diagram shows how messages are sent back and forth between CIC and a client.

![](/CIC/Resources/Images/CIC_Interaction_Example_in_Sequence_Diagram.png)

## Dialogue model {#DialogModel}
This section covers the following topics to provide an understanding of the CIC dialogue model:

* [Indirect dialogue structure](#IndirectDialog)
* [Dialogue ID and client behavior](#DialogIDandClientOP)

### Indirect dialogue structure {#IndirectDialog}
Users can have a series of dialogues with Clova. In general, users make requests to Clova to get information or to perform certain actions. Clova returns requested information or performs the requested action. Such dialogues between users and Clova are relayed by clients and CIC.

Dialogues between users and Clova usually proceed as followings:

1. A user starts to speak to Clova.
2. The client records the user speech and sends the recording to CIC.
3. CIC returns result to the client. The client delivers the result to the user through synthesized speech or display.

Having CIC and a client in between, dialogueues between users and Clova are rather indirect and have the following limitations:

* Delivering requests and receiving responses take more time compared to direct dialogueues.
* Response is not immediate when new requests are made or new dialogueues are initiated by users.

Suppose a user asks Clova, "How's the weather today?" Before Clova responds or while Clova is responding, the user makes another request: "Play some upbeat music." The user will probably no longer want the weather information. Had the dialogue been direct, you would simply ignore the weather information returned. However, since dialogueues are relayed by a client to Clova, the client must recognize the dialogue status and take appropriate actions to provide what user wants.

### Dialogue ID and client action {#DialogIDandClientOP}

To overcome the restrictions of indirect dialogueues, we use a **dialogue ID**. To identify individual user request, a **dialogue ID** is created every time a user starts speaking to Clova. Keep a copy of the dialogue ID of the latest user request sent to CIC. Update the latest dialogue ID every time you send a user request to CIC.

A directive, returned from CIC as a response to the user request, contains a dialogue ID. This dialogue ID is identical to the one that had been embedded in the user request. In short, dialogue IDs help you identify whether the Clova response corresponds to the latest user request or not. To use dialogue IDs:

1. Create a **new dialogue ID** every time a user initiates a dialogue.
2. Send the user request to CIC with the [SpeechRecognizer.Recognize](/CIC/References/CICInterface/SpeechRecognizer.md) event.
  * Replace the **latest dialogue ID** with the newly created dialogue ID.
  * When the latest dialogue ID is replaced, discard all directives associated to dialogue IDs other than the latest, regardless of whether the directives are being processed or are waiting to be processed.
3. When CIC returns a directive with the request result, compare the dialogue ID of the directive with the latest dialogue ID kept on the client.
  * **If the IDs match**, return the result contained in the directive to the user.
  * **If the IDs do not match**, discard the received directive.
