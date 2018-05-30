## Managing message queues {#ManageMessageQ}

Clients constantly send and receive messages to and from CIC. Directives, the messages clients receive from CIC, have the following characteristics.
* Multiple directives and additional information can come within an HTTP response.
* Directives are sent through a downchannel or as an HTTP response.
* Directives within an HTTP response may have different dialogue IDs.
* The order in which the message parts with additional information are received is not guaranteed.

Due to these characteristics, we recommend you use a queue to manage directives received either through a downchannel or an HTTP response and push and pop directives in the order they were received. We call this queue a "message queue."

You must develop the code so that the directives queued into each message queue are handled one at a time. Here, the message responding to the latest request of the client user must be handled. The user request can be identified with [dialogue ID](/CIC/CIC_Overview.md#DialogModel) and the client must keep the dialogue ID on the latest request. If your message queue is keeping any directive with a dialogue ID of a canceled dialogue, remove the directive from the queue.

Determine the following as you wish or depending on the UX design.
* The number of message queues and each queue size
* Priority over message queues

For example, if a UX for performing seamless actions, even during user speech input or client speech output such as playing music ([AudioPlayer](/CIC/References/CICInterface/AudioPlayer.md)) is provided, it is necessary to handle the directive of the related message queue separately. However, there are a number of Clova services that send a single directive simultaneously. For such services, no separate message queues are required.
