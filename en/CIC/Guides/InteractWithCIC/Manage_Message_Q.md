## Managing message queue {#ManageMessageQ}

A client sends and receives messages to and from CIC in sequence. When a client receives a Directive message from CIC, the message may have the following characteristics.
* Your client may receive a multiple number of Directive messages and messages containing additional information in one delivery from CIC.
* Your client may receive a Directive message through a Downchannel and as a response to an Event message as well.
* Your client may receive Directive messages whose dialogue IDs are different.
* When CIC sends Directive messages, it may not send them in a sequential order.

For this reason, your client should use queue data structure called a "message queue," with which your client can put in and take out messages sequentially that are sent through a Downchannel or as a response to an Event message.

You should develop your client to process Directive messages one at a time as they are being enqueued in a message queue. Also, the message being processed should match the dialog ID of the last user request in your client. If there is any Directive message whose dialog ID has been canceled, that message and all related additional information should be removed from the message queue.

Client developers should determine the following by considering their UX design plan.
* The number of message queues and their size
* Processing priority of message queues

If you want to provide UX that runs tasks seamlessly while your client is receiving speech input or producing speech output such as music playback ([AudioPlayer](/CIC/References/APIs/AudioPlayer.md)), you may have to process such Directive messages separately in the related message queue.

Also, some API namespaces send a single Directive message simultaneously. You may not need to manage message queues for such namespaces.
