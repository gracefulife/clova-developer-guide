Clova sends the analyzed result of user audio input to the extension server, so the server should be implemented to respond accordingly to the received details.

* **If the analyzed result is the separated registered user intent (**[Custom intent](/Design/Design_Guideline_For_Extension.md#CustomIntent)**),**

  Clova sends one of the request messages: run extension, run registered intent, and exit extension request types. Then, the server should start the extension, handle the designated intent, or exit the extension, respectively, and return the result.

* **If the analyzed result is the intent provided by Clova as the default (**[Built-in intent](/Design/Design_Guideline_For_Extension.md#BuiltinIntent)**),**

  Clova sends a request message, such as a help guide or a positive, negative, or undo action accordingly. Then, the server should respond normally to the message.
