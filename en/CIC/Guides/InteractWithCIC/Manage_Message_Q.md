## Managing message queue {#ManageMessageQ}

Sending and receiving messages to and from CIC occurs in a consecutive way. Directive messages returned from CIC have the following characteristics.
* CIC can return multiple directive messages and messages for additional information at one time.
* CIC can return directive messages not only through a downchannel but also through a response message to an event message.
* Directive messages can have different dialog IDs.
* CIC does not return directive messages in a sequential order.

Because of these characteristics, you must use a queue-based data structure to put in and take out response messages and downchannel messages in a sequential order. We call this data structure a "message queue."

Develop your client to process directive messages one at a time as they are enqueued in each message queue. Also, the message in processing must be the equivalent of the last user request present in your client. User requests are identifiable with dialog IDs and your client must be keeping the dialog ID of the last request. If your client is keeping any directive message with a canceled dialog ID in a message queue, such message and its related information must be removed from the queue.

Determine the following rules in consideration of your UX design plan.
* The number of messages queues and their size
* Processing priority of message queues

If you want to provide UX that runs tasks seamlessly while your client is receiving speech input or generating speech output, such as music playback ([AudioPlayer](/CIC/References/APIs/AudioPlayer.md)), you must process such directive messages separately in the message queue. Also, there are some API namespaces that send a single directive message simultaneously. For such namespaces, you do not have to manage message queues separately.
