## Managing message queue {#ManageMessageQ}

Sending and receiving messages to and from CIC occur in a consecutive way. When CIC returns directive messages, they have the following characteristics.
* CIC can return multiple directive messages and messages for additional information at one time.
* CIC can return directive messages not only through a downchannel but also through a response message to an event message.
* CIC can return directive messages with different dialog IDs.
* CIC does not return directive messages in a sequential order.

Because of these characteristics, you must use a queue-based data structure to put in and take out messages in a sequential order, whether the messages are responses to event messages or whether they are messages sent through a downchannel. We call this data structure a "message queue."

Develop your client to process directive messages one at a time as they are enqueued in each message queue. Also, the message in processing must correspond to the last user request in your client. User requests are identifiable by [dialog IDs](/CIC/CIC_Overview.md#DialogModel) and the dialog ID of the last request must be kept at the client side. If your client is keeping any directive message which has a canceled dialog ID in a message queue, such message and its related information must be removed from the queue.

Determine the following rules in consideration of your UX design plan.
* The number of message queues and their size
* Processing priority of message queues

If you provide UX that runs tasks seamlessly while your client is receiving speech input or playing speech audio, such as music playback ([AudioPlayer](/CIC/References/CICInterface/AudioPlayer.md)), process message queues separately for such directive messages. Also, some API namespaces send a single directive message simultaneously. For such namespaces, you do not have to manage message queues separately.
