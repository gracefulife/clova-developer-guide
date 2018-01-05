## Managing message queues {#ManageMessageQ}

Clients constantly send and receive messages to and from CIC. Directives, the messages clients receive from CIC, have the following characteristics.

* Multiple directives and additional information can come within an HTTP response.
* Directives are sent through a downchannel or as an HTTP response.
* Directives within an HTTP response may have different dialog IDs.
* The order in which the message parts with additional information is not guaranteed.

Due to these characteristics, we recommend you to use a queue to manage directives, either received through a downchannel or an HTTP response. Push and pop directives in the order they were received. We call this queue a "message queue."

Make your client process directives in the message queue one at a time. Ignore directives with [dialog ID](/CIC/CIC_Overview.md#DialogModel) different to that of the one kept in your client. This is for your client to provide a valid respond to user's request. User requests are identifiable by dialog IDs and your client shall keep the dialog ID of the latest request. If your message queue is keeping any directive with a dialog ID of a canceled dialog, remove the directive from the queue.

Determine the following as you wish or depending on UX design.

* The number of message queues and each queue size
* Priority over message queues

For example, if the nature of a service requires seamless UX, such as receiving user's vocal input whilst playing music, use two message queues; one for playing the music and one for processing vocal input. However, there are a number of Clova services that send a single directive simultaneously. For such services, no separate message queues are required.
