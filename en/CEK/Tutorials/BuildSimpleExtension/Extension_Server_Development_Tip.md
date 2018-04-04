Clova analyzes user utterances and sends the analyzed results to the extension server, so the server should be implemented to respond accordingly to the received details.

* **If the analyzed result is the separated registered user intent (**[Custom intent](/Design/Design_Guideline_For_Extension.md#CustomIntent)**),**

  Clova sends one of three types of request messages: run extension, run registered intent, or exit extension. When the server receives these requests, the server must handle the processes and return the results of starting the extension, handling the designated intent, or exiting the extension.

* **If the analyzed result is the intent provided by Clova as the default (**[Built-in intent](/Design/Design_Guideline_For_Extension.md#BuiltinIntent)**),**

  Clova sends a request message such as help, positive response, negative response, or undo action, according to the built-in intent. When the server receives these requests, the server must return a typical response.
