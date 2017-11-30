# Defining the interaction model

The interaction model should be defined in advance on how to analyze user speech and in what form it should be sent when CEK is sending a user request details to the extension. An interaction model is a schema which standardizes requests received by [custom extension](/CEK/Guides/Build_Custom_Extension.md).

The interaction model can be defined after [registering extension](/DevConsole/Guides/CEK/Register_Extension.md) on Clova developer console. Select **Interaction Model** from the Registering a Clova Extension

![](/DevConsole/Resources/Images/DevConsole-Interaction_Model_Menu.png)

When clicking **Interaction Model**, the page will move on to **Interaction Model: Dashboard**.

![](/DevConsole/Resources/Images/DevConsole-Interaction_Model_Dashboard.png)

Now, define the interaction model by following the below steps.

1. (Prerequisites) [Understanding the interaction model](#UnderstandInteractionModel)
2. [Adding a built-in slot type](#AddBuiltinSlotType)
3. [Adding a custom slot type](#AddCustomSlotType)
4. [Adding a built-in intent](#AddBuiltinIntent)
5. [Adding a custom intent](#AddCustomIntent)

<div class="note">
  <p><strong>Note!</strong></p>
  <p>The slot type can be added after adding the custom intent but due to the nature of UI provided by the Clova developer console, it is recommended to add the intent after adding the slot type first. </p>
</div>

## Understanding the interaction model {#UnderstandInteractionModel}

The interaction model in Clova specifies how to convert user request from user speech into a JSON format, for Clova to deliver the user request to a custom extension. Suppose we have a custom extension which provides a pizza delivery service, and a user requests for a pizza by saying, “Order two boxes of pepperoni pizza". Instead of delivering the whole speech, Clova breaks the request into a JSON format based on the specification defined on the developer console. This specification is the interaction model.

![](/DevConsole/Resources/Images/DevConsole-Interaction_Model_Analysis_Diagram.png)

Before defining the interaction model from the Clova developer console, it is significant to go through a process of understanding and designing the model. If conducting registration on the Clova developer console right away without having the process, it would cause poor productivity and the user request might not be converted as intended. To create an interaction model with comprehensive understanding of users' intention, the following three subjects have to be well understood and reflected on the model design.

* [Intent](#Intent)
* [Slot](#Slot)
* [User speech example](#UtteranceExample)

### Intent {#Intent}

An intent is a segment that distinguishes the user requests for an extension to handle. The intent is divided into two: a custom intent and a built-in intent. The built-in intent is specified for Clova platform to define categories of users’ common requests and to share the categories. Frequently used intents are predefined as below table. You can choose which built-in intent to use from the extension. The chosen built-in intent should be handled from the extension it is going to be registered to.

| Names of Built-in Intent       | Intention               | Examples of user speech                                      |
|---------------------------|-------------------|----------------------------------------------------------|
| Clova.GuideIntent         | Asking for help          | “What are you capable of?”, “What can you do?”, “Say what you can do” |
| Clova.CancelIntent        | Request for cancellation        | “Cancel”, “Please cancel”                                          |
| Clova.YesIntent           | Positive answer (Yes)   | “Yes”, “Sure”, “Alright”, “Got it”, “Okay”                   |
| Clova.NoIntent            | Negative answer (No) | “No”, “Nope”, “Don’t want it”                                     |

The custom intent specifies the following information:

* What various request categories exist in service
* What [Slots](#Slot) are required for each request category
* What types of [speech examples](#UtteranceExample) are in each request category

To give an example with the pizza delivery service, the specific service will have the following categories of requests.

* Request to view the menu
* Request to order
* Request to track the delivery

To define an interaction model for the pizza delivery service means to declare intent lists such as view the menu intent, order intent, and track delivery intent. It also lists which slots will be applied to which intent and what types of examples of speeches there are. Thus, **the first thing that has to be done when defining the interaction model is to define which category the extension should handle and make a list them**. This would be the standard to distinguish the program branches that is, the business logic, when developing an extension.

![](/DevConsole/Resources/Images/DevConsole-Design_Interaction_Model.png)

**If the categories of the user requests are distinguished, names for each category has to be defined.** The defined names become the name of the intent. “The order intent” of the pizza delivery service is an abstract idea yet the category has to be defined in a concrete name, in order words, in strings that can be recognized by the extension. For instance, “the order intent” can be defined as “OrderPizza” as a name.

Now, “Order pizza” intent should be **defined in which type of information([Slot](#Slot)) it takes** from the user speech. Also, various [speech examples](#UtteranceExample) have to be listed to show which types of speeches can be processed.

### Slot {#Slot}

A slot is an information acquired from the user speech. When defining the [custom intent](#Intent), the slot required by the intent also have to be defined. To give an explanation compared to the software development, the intent is a function or handler to process a specified range of user requests and the slot is a required parameter for the function or handler. When we take a look at the user speech saying “order two boxes of pepperoni pizza”, we can see that it requires a type of pizza as “pepperoni pizza” and a quantity as “two boxes” to handle the “OrderPizza” intent. Therefore, when defining an intent, it is important to grasp what types of information(slot) are needed.

When declaring a slot, it has to be identified which type of information it is. An identified slot is called ‘a slot type’. The slot type can be distinguished into two types: a built-in slot type and a custom slot type. The built-in slot type is a type of information predefined by Clova. It defines information that can be used for general purposes from all service extensions. The built-in slot type is used to recognize information such as time, place, quantity and more. In case of the pizza delivery order, the built-in slot type can be applied to recognize the information of “two boxes”. Below table shows the types of built-in slot that are provided from Clova.

| Names of Built-in slot | Explanations                                            |
| ----------------------|------------------------------------------------|
| CLOVA.DATETIME      | Date and time details (Ex. “10 min 30 sec”, “9a.m.”, “An hour ago”, “12p.m.”, “Noon”, “24th August 2017”, and “The last day of the previous month”) |
| CLOVA.DURATION      | Duration details (Ex. “A day”, “All night”, “A month”, “Next month”, “Weekends”) |
| CLOVA.NUMBER        | Number details  including quantity nouns (Ex. “Once”, “Seven men”, “One”, “30 years-old”, “About eight”, and “16 spaces”) |
| CLOVA.RELATIVETIME  | Relative time details (Ex. “In the future”, “Later”, “In a moment”, “Just now”, “A while ago”) |
| CLOVA.UNIT          | Unit details (Ex. “113 pyeong”, “100 megabytes”, and “25 miles”) |
| CLOVA.ORDER         | Order details (Ex. “Next”, “Previous”, “Before”, “Last”, “Next”, “Now”, and “Past”) |
| CLOVA.KO_ADDRESS_[Administrative districts unit] | Regional names of administrative districts in domestic. The unit of administrative districts provided by Clova can be viewed from the Clova developer console. |
| CLOVA.WORLD_COUNTRY | Country name details (Ex. “Ghana”, “Japan”, “Republic of Korea”, and “France”) |
| CLOVA.WORLD_CITY    | City name details (Ex. “New York”, “Paris”, and “London”) |
| CLOVA.CURRENCY      | Currency details (Ex. “Yuan”, “Yen”, “Dollar”, “Russian money”, and “British currency”) |
| CLOVA.OFFICIALDATE  | Public, national holidays and anniversaries details (Ex. “Onset of Spring”, “New Year’s Day”, “Buddha’s Birthday”, and “National Liberation Day”) |

The custom slot type defines types of information specified for a domain of supported service extensions. It usually designates pronouns and nouns when creating the custom slot type. The “OrderPizza” intent has to acquire an information (slot) that falls into the category of types of pizza from the user speech. There is a high chance that pizza types are only used from pizza related services. Thus, define a custom slot type as “PIZZA_TYPE” and a list of items that can be applied for pizza delivery service such as “Pepperoni pizza”, “Combination pizza”, and “Cheese pizza”.

Note that the list of items may have the same meaning in sentences but can be expressed similarly or differently. For instance, “Barbeque pizza” is considered as a synonym to “BBQ pizza” and an extended name like “Shrimp gold crust pizza” is usually shortened as “Shrimp GC
 pizza”. Due to the variety, items categorized by ideas have to be declared. Representative words and synonyms have to be defined as well to specify the custom slot types. By doing so, synonyms expressed differently by users will be converted into representative words. Also, while the extension is processing the intent, it will return the ideas that falls into same categories as a coherent value.

Decide a name for each slot that would be used for the intent after defining them and declare what kinds of type the slots have. For instance, the “OrderPizza” intent will declare “pizzaType” for types of pizza and “pizzaAmount” for amount of pizza. For each slot, predefined "PIZZA_TYPE" custom slot type and CLOVA.NUMBER built-in slot type already in service can be designated.

### User speech examples {#UtteranceExample}
Various user speech examples can be listed to define the intent. The speech examples become fundamental data for Clova to recognize expressions with same meaning but different wordings. It is also used to find out at which segment of the speech the slot is located. The intent is decided usually by a predicate (a verb) in the sentence. When writing speech examples, it is better to list expressions with similar meanings than repeating expressions that express exact meaning of the intent. This will lead to make a best interaction model that will do an excellent job to recognize users’ intents.

The following is a list of user speech related to the pizza delivery service intent (OderPizza). It shows appropriate examples and inappropriate examples.

<table>
  <thead>
    <tr>
      <th width="50%">Appropriate Examples</th>
      <th width="50%">Inappropriate Examples</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>
        <pre>Order a pepperoni pizza
Could you order two BBQ pizza?
Order three combination pizza
Please order a shrimp GC
 pizza
...</pre>
      </td>
      <td>
        <pre>Order a pepperoni pizza
Order a combination pizza
Order a bulgoggi pizza
Order a cheese pizza
...</pre>
      </td>
    </tr>
  </tbody>
</table>

List the “OrderPizza” intent related speech as above and mark the segments that belong to the slot according to below example.

{% raw %}

```
Order <pizzaAmount>two boxes of</pizzaAmount><pizzaType>pepperoni</pizzaType>.
Could you deliver <pizzaAmount>two</pizzaAmount><pizzaType>BBQ pizza</pizzaType>?
Get me <pizzaAmount>two</pizzaAmount><pizzaType>combination pizza</pizzaType>.
Please get <pizzaAmount>one</pizzaAmount><pizzaType>Shrimp GC</pizzaType>.
...
```
{% endraw %}


The custom extension will receive the following message.

{% raw %}

```json
// Custom intent: Order two boxes of pepperoni pizza
{
  "version": "0.1.0",
  "session": {
    "new": false,
    "sessionAttributes": {},
    "sessionId": "a29cfead-c5ba-474d-8745-6c1a6625f0c5",
    "user": {
      "userId": "V0qe",
      "accessToken": "XHapQasdfsdfFsdfasdflQQ7"
    }
  },
  "context": {
    "System": {
      "user": {
        "userId": "V0qe",
        "accessToken": "XHapQasdfsdfFsdfasdflQQ7"
      },
      "device": {
        "deviceId": "096e6b27-1717-33e9-b0a7-510a48658a9b"
      }
    }
  },
  "request": {
    "type": "IntentRequest",
    "intent": {
      "name": "OrderPizza",
      "slots": {
        "pizzaAmount": {
          "name": "pizzaAmount",
          "value": "2"
        },
        "pizzaType": {
          "name": "pizzaType",
          "value": "pepperoni"
        }
      }
    }
  }
}

// Built-in intent: Cancel the order
{
  "version": "0.1.0",
  "session": {
    "new": false,
    "sessionAttributes": {},
    "sessionId": "a29cfead-c5ba-474d-8745-6c1a6625f0c5",
    "user": {
      "userId": "V0qe",
      "accessToken": "XHapQasdfsdfFsdfasdflQQ7"
    }
  },
  "context": {
    "System": {
      "user": {
        "userId": "V0qe",
        "accessToken": "XHapQasdfsdfFsdfasdflQQ7"
      },
      "device": {
        "deviceId": "096e6b27-1717-33e9-b0a7-510a48658a9b"
      }
    }
  },
  "request": {
    "type": "IntentRequest",
    "intent": {
      "name": "Clova.CancelIntent",
      "slots": {}
    }
  }
}
```

{% endraw %}

## Adding a built-in slot type {#AddBuiltinSlotType}

After deciding which [built-in slot type](#Slot) to be applied for the service extension, add the decided type to the interaction model of the extension. Suppose you are making an extension for the pizza delivery service, the pizza amount information will be used for the user speech. To use a related built-in type at the extension, follow below steps to add the type to the extension.

<ol>
  <li>Click <img src="/DevConsole/Resources/Images/DevConsole-Plus_Button.png" /> button located at top right side of the <strong>slot type</strong> penal or at top right side of the <strong>slot type menu in use</strong> located at the bottom of the <strong>Interaction model build menu</strong>. Upon clicking the button, the page will move on to <strong>Interaction model: Add slot type</strong>.</li>
  <li>Check check-boxes of the built-in slot type.</li>
  <img src="/DevConsole/Resources/Images/DevConsole-Add_Built-in_Slot.png" />
  <li>After checking the type, click <strong>Create</strong> button located at the bottom of the page.</li>
</ol>

After processing the steps, you can see that the built-in type has been added to **Slot type penal** from the **Interaction mode: Dashboard** page.

![](/DevConsole/Resources/Images/DevConsole-Added_Built-in_Slot.png)

## Adding a custom slot type {#AddCustomSlotType}

For the next step, a [custom slot type](#Slot) for your extension has to be defined. Let’s take a look at the pizza delivery service extension example again in extension to the [adding a built-in slot type](#AddBuiltinSlotType). In a user speech, a segment referring to the type of pizza can be defined as the custom slot type. Let's assume that we are adding a custom slot type called “PIZZA_TYPE” with representative words and synonyms as below.

| Representative words           | Synonyms                                        |
|----------------|----------------------------------------------|
| Pepperoni          | Pepperoni pizza                                  |
| Barbeque           | Barbeque pizza, BBQ pizza                           |
| Cheese             | Cheese pizza                                     |
| Vegetable             | Vegetable pizza, Veggie pizza, Vegetarian pizza               |
| Shrimp Gold Crust | Shrimp Gold Crust pizza, Shrimp GC
 pizza, Shrimp GC |

Follow the steps to add the custom slot type.

<ol>
  <li>Click <img src="/DevConsole/Resources/Images/DevConsole-Plus_Button.png" /> button that is located at top right side of the <strong>slot type</strong> penal or at top right side of the <strong>slot type menu in use</strong> located at the bottom of the <strong>Interaction model build menu</strong>. Upon clicking the button, the page will move on to <strong>Interaction model: Add slot type</strong>.</li>
  <li>Enter a name of the custom slot type that will be added on <strong>Create a new slot type field</strong> and click the <strong>Create</strong> button. When the creation is completed, a page where details of the custom slot type can be viewed will appear. </li>
  <img src="/DevConsole/Resources/Images/DevConsole-Add_Custom_Slot_1.png" />
  <li>Click <img src="/DevConsole/Resources/Images/DevConsole-Plus_Button.png" /> button located at <strong>Slot type dictionary</strong> and add the representative words.</li>
  <img src="/DevConsole/Resources/Images/DevConsole-Add_Custom_Slot_2.png" />
  <li>Add synonyms next to the representative words.</li>
  <img src="/DevConsole/Resources/Images/DevConsole-Add_Custom_Slot_3.png" />
  <li>Click <strong>Save</strong> button at the top right side of the page.</li>
</ol>

Move to the **Interaction model: Dashboard** page through the <strong>Dashboard</strong> menu to verify added custom slot types.

![](/DevConsole/Resources/Images/DevConsole-Added_Custom_Slot.png)

If bulk amount of information has to be added to the custom slot type, you can upload it in TSV (Tab-separated values, .tsv) file format. Values of first columns of the TSV file will have the representative words and the following values distinguished as tab characters will have synonyms of the representative words. Below table is an example of the definition of the “PIZZA_TYPE” custom slot type in TSV format.

```
pepperoni    Pepperoni pizza
Barbeque      Barbeque pizza     BBQ pizza
Cheese       Cheese pizza
Vegetable       Vegetable pizza        Veggie pizza      Vegetarian pizza
Shrimp Gold Crust         Shrimp Gold Crust pizza      Shrimp GC pizza       Shrimp GC
```

Click **Upload** to upload a custom slot type predefined in TSV file and click **Download** to download a custom slot type currently being written at the Clova developer console in TSV file format.

![](/DevConsole/Resources/Images/DevConsole-Custom_Slot_Upload_and_Download_Button.png)

## Adding a built-in intent {#AddBuiltinIntent}

A [built-in intent](#Intent) is an intent defined by the Clova platform for it to set a common user request categories and to share them. It predefines frequently made requests from the users such as positive/negative or stop/cancel requests. The built-in intent for the extension can be selectively added.

<div class="note">
  <p><strong>Note!</strong></p>
  <p>All extensions should be able to support the built-in intent provided by Clova. In the near future, we are going to make a change so that developers can choose the built-in intent selectively by extensions. This part of the writing will be updated soon.</p>
</div>

## Adding a custom intent {#AddCustomIntent}
If the [built-in slot type](#AddBuiltinSlotType) and the [custom slot type](#AddCustomSlotType) are successfully added, the custom intent can be added.  Again, with the pizza delivery intent example, let’s add an intent named “OrderPizza” following the below steps.

<ol>
  <li>Click the <img src="/DevConsole/Resources/Images/DevConsole-Plus_Button.png" /> button located at top right side of <strong>Intents</strong> penal or at top right side of <strong>Intent in use</strong> located at the bottom of the <strong>Interaction model builder menu</strong>. Upon clicking the button, the page will move on to the <strong>Interaction model: Add slot type</strong>.</li>
  <li>Enter the name of the custom slot type on <strong>Create a new slot type field</strong> and click the <strong>Create</strong> button. When the creation is completed, a page where details of the custom intenet can be viewed will appear.</li>
  <img src="/DevConsole/Resources/Images/DevConsole-Add_Custom_Intent_1.png" />
  <li>Enter slot names on the <strong>Intent slot list</strong> field and click <img src="/DevConsole/Resources/Images/DevConsole-Plus_Button.png" /> button located at the top right side of the page to add.</li>
  <img src="/DevConsole/Resources/Images/DevConsole-Add_Custom_Intent_2.png" />
  <li>After adding the slot, designate a type for the slot.</li>
  <img src="/DevConsole/Resources/Images/DevConsole-Add_Custom_Intent_3.png" />
  <li>Enter examples of the user speech on <strong>List of user expression</strong> and click <img src="/DevConsole/Resources/Images/DevConsole-Plus_Button.png" /> button located at the right side to add.</li>
  <img src="/DevConsole/Resources/Images/DevConsole-Add_Custom_Intent_4.png" />
  <li>Drag a segment from the added speech examples to designate as the slot.</li>
  <img src="/DevConsole/Resources/Images/DevConsole-Add_Custom_Intent_5.png" />
  <li>Repeat step 5 and 6 and add speech examples in the intent as much as needed.</li>
  <li>Click <strong>Save</strong> button on the top right side of the page.</li>
</ol>

The speech examples are the basic data to analyze the user speech. The more the examples and expressions there are, it will have better chances to analyze the speeches. Therefore, it is recommended to enter more than 30 examples in one intent.

The bulk amount of information can be uploaded in TSV (Tab-separated values, .tsv) file format just as it was possible when adding the custom slot type. The TVS file can be divided into two. One is to define slots of intents and the other is to list speech examples. The part of defining slots of the intent should be located at the top of the file and the slots will be listed follwing the line where `[INTENT SLOT]` is. The first column identified as the tab character is the part with slot names and the second column is the part with slot types.

The explanation part of the intent speech examples comes latter part of the file. The speech examples will be listed following the column where `[INTENT EXPRESSION]` is entered. To distinguish the slots from the speech examples, wrap the slot-equivalent expressions with the slot-named tags. The following is an example of TSV file defining the intent.

```
[INTENT SLOT]
pizzaType	PIZZA_TYPE
pizzaAmount	CLOVA.NUMBER

[INTENT EXPRESSION]
Order <pizzaAmount>two boxes of</pizzaAmount><pizzaType>pepperoni</pizzaType>.
Could you deliver <pizzaAmount>two</pizzaAmount><pizzaType>BBQ pizza</pizzaType>?
Get me <pizzaAmount>two</pizzaAmount><pizzaType>combination pizza</pizzaType>.
Please get <pizzaAmount>one</pizzaAmount><pizzaType>Shrimp GC</pizzaType>.
...
```

Click **Upload** to upload a custom slot predefined in TSV file and click **Download** to download a custom slot currently being written at the Clova developer console in TSV file format.

![](/DevConsole/Resources/Images/DevConsole-Utterance_Example_Upload_and_Download_Button.png)

<div class="danger">
  <p><strong>Caution!</strong></p>
  <p>It is recommended to declare the same name to the slot types despite any intent within the same interaction model. For example, from the “OrderPizza” intent, if a name of slot related to pizza type (“PIZZA_TYPE”) is “pizzaType”, the same slot type has to be declared from other intents so that the same name (“pizzaType”) would be applied. However, note that there are cases where slots have a same type but their names have to be written differently. In a user speech saying, “Tell me how many hours it takes to go to Busan from Seoul”, “Seoul” and “Busan” are the same slot types but their purpose has to be distinguished separately and therefore the slot names have to be differentiated.</p>
</div>

Up to here, a guidance to add intents to an interaction model was explained. Repeat the same steps as explained above to add intents on your extension as many as necessary. If then, an interaction model as below will be created.

a![](/DevConsole/Resources/Images/DevConsole-Added_Interaction_Model.png)
