# CIC integration
To enable access to Clova services for your users, your client (app or device) should deliver user requests with necessary contextual information to Clova using the CIC interface. Firstly, you need to understand how your client should connect with CIC, which messages should be sent and received and which tasks should be done during the process.

This document covers the following topics to provide essential information for client developers.

1. [Preparation](#Preparation)
2. [Connecting with CIC](#ConnectToCIC)
3. [Sending Event message](#SendEvent)
4. [Handling Directive message](#HandleDirective)
5. [Managing message queue](#ManageMessageQ)

{% include "./InteractWithCIC/Preparation.md" %}

{% include "./InteractWithCIC/Connect_to_CIC.md" %}

{% include "./InteractWithCIC/Send_Event.md" %}

{% include "./InteractWithCIC/Handle_Directive.md" %}

{% include "./InteractWithCIC/Manage_Message_Q.md" %}