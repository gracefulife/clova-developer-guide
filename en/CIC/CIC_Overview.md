# CIC overview

Learn what Clova Interface Connect ('CIC' hereinafter) is and how it works.

## What is CIC? {#WhatisCIC}

CIC is a platform that serves as an interface between Clova and a client providing AI assistant services on computers, mobile apps, mobile devices or home appliances. CIC provides the [CIC API](/CIC/References/CIC_API.md) with which clients can send user requests to Clova and Clova can return responses to clients.

![](/CIC/Resources/Images/CIC_Interaction_Structure.png)

## CIC interaction structure {#CICInteractionStructure}

Clients use the CIC API to send user requests to CIC and also to receive responses from CIC. All communications with CIC is made over the [HTTP/2 protocol](https://tools.ietf.org/html/rfc7540). The [CIC API](/CIC/References/CIC_API.md) provides interfaces for speech recognition, playing synthesized speech and music, calendar management, setting alarms/timers, and many other features.

Through the CIC API, various communications are made between clients and CIC in the form of messages. Two types of messages are available. The message type depends on who the message sender is as follows.

* [Event](/CIC/References/CIC_API.md#Event): Messages that clients send to CIC. Send events to CIC to pass user's voice requests (speech input) to CIC and to notify CIC when your client states have changed.

* [Directive](/CIC/References/CIC_API.md#Directive): Messages that CIC sends to clients to control client behavior. For example, a directive can instruct an app to display certain information or play synthesized speech. Directives are sent to clients when:
    * Responding to user requests. After recognizing user's voice request (user intent), CIC returns directives to instruct clients to perform certain actions relevant to the user intent.
    * Certain conditions require CIC to send directives to clients without any preceding user requests.

The following sequence diagram shows how messages are sent back and forth between CIC and a client.

![](/CIC/Resources/Images/CIC_Interaction_Example_in_Sequence_Diagram.png)

## Dialog model {#DialogModel}

Learn about CIC's dialog model.

* [Indirect dialog structure](#IndirectDialog)
* [Dialog ID and client behavior](#DialogIDandClientOP)

### Indirect dialogs {#IndirectDialog}

Users can have a series of dialogs with Clova. In general, users make requests to Clova to get information or to perform certain actions. Clova returns requested information or perform the requested action. Such dialogs between users and Clova are relayed by clients and CIC.

Dialogs between users and Clova usually proceed in the following steps:

1. A user starts to speak to Clova.
2. A client records the user's speech and sends the record to CIC.
3. CIC returns result to the client.
4. The client delivers the result to the user through synthesized speech or display.

Having CIC and client in between, dialogs between users and Clova are rather indirect, having the following limitations:

* Delivering requests and receiving responses take more time compared to direct dialogs.
* Immediate response is unavailable when new requests are made or new dialogs are initiated by users.

Suppose a user asks Clova, "How's the weather today?". Before Clova responds or while Clova is responding, the user makes another request, "Play some upbeat music." The user will probably no longer want the weather information. Had the dialog been a direct dialog, you would simply ignore the weather information returned. However, since dialogs are relayed by a client to Clova, the client must recognize the dialog status and take appropriate actions to provide what user wants.

### Using Dialog ID  {#DialogIDandClientOP}

To overcome the restrictions of indirect dialogs, we use a **dialog ID**. To identify individual user request, a **dialog ID** is created every time a user starts speaking to Clova. This leaves you to do the following:

* Keep a copy of the dialog ID of the latest user request sent to CIC.
* Update the latest dialog ID every time you send a user request to CIC.

A directive, returned from CIC as a response to the user request contains a dialog ID. This dialog ID is identical to the one that had been embedded in the user request. In short, dialog IDs help you identify whether Clova's response corresponds to the latest user request or not.

To use dialog IDs:

1. Create a **new dialog ID** every time a user initiates a dialog.
2. Send the user request to CIC with the [SpeechRecognizer.Recognize](/CIC/References/CICInterface/SpeechRecognizer.md) event.
  * Replace the **latest dialog ID** with the newly created dialog ID.
  * When the latest dialog ID is replaced, discard all directives associated to dialog IDs other than the latest, regardless whether the directives are being processed or are to be processed.
3. When CIC returns a directive with the request result, compare the dialog ID of the directive with the latest dialog ID kept on the client.
  * **If the IDs match**, return the result contained in the directive to the user.
  * **If the IDs mismatch**, discard the directive received.
