# Handling basic built-in intents
This tutorial will guide you on how to handle basic intents such as "yes" or "no," using the Sample Dice extension created in [building a basic extension](/CEK/Tutorials/Build_Simple_Extension.md).

Clova has frequently used basic intents predefined as [built-in intents](/Design/Design_Guideline_For_Extension.md#BuiltinIntent), which can be used by all extensions. The built-in intents provided by Clova are as follows:

| Built-in intent       | Intent               | Sample response utterance                                      |
|---------------------------|-------------------|----------------------------------------------------------|
| Clova.GuideIntent         | Help request          | "What can you do?," "Tell me how to use it" |
| Clova.CancelIntent        | Undo action request        | "Cancel," "Cancel please"                                          |
| Clova.YesIntent           | Positive response (e.g. Yes)   | "Yes," "Sure," "All right," "Certainly," "Okay"                   |
| Clova.NoIntent            | Negative response (e.g. No) | "No," "No, thank you," "Absolutely not"                                     |

To handle a help request or undo an action request from the user, you can use the built-in intents in the above table without registering intents and sample phrases, just like in the first tutorial.

The process of handling built-in intents is as follows:
* Step 1. Implement built-in intent processing (on the extension server)
* Step 2. Test the built-in intent operation (on the Clova developer console)

## Step 1. Implementing built-in intent processing {#Step1}
{% include "/CEK/Tutorials/HandleBuiltinIntents/Implement_Builtin_Handler.md" %}

## Step 2. Testing the built-in intent operation {#Step2}
{% include "/CEK/Tutorials/HandleBuiltinIntents/Test_Builtin_Intent.md" %}

This way, the Sample Dice extension can respond to help requests.
If you implement the extension server to handle `Clova.CancelIntent`, `Clova.YesIntent`, and `Clova.NoIntent` using this method, the extension will be able to respond to undo actions and positive or negative requests.
