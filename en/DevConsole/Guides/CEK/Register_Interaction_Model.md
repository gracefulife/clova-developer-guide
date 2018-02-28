# Registering an interaction model

When the CEK sends user request information to the extension, you must [define the interaction model](/Design/Design_Guideline_For_Extension.md#DefineInteractionModel) in advance on how to analyze user's utterances and which format to use for sending them. The interaction model is a schema that has standardized the requests to be received by the [custom extension](/CEK/Guides/Build_Custom_Extension.md).

You can register the interaction model after [registering the extension](/DevConsole/Guides/CEK/Register_Extension.md) in the Clova developer console. In the CEK menu, click the **{{ book.DevConsole.cek_edit }}** button of the extension to register an interaction model as shown below.

![](/DevConsole/Resources/Images/DevConsole-Interaction_Model_Menu.png)

Then, the following **{{ book.DevConsole.cek_interaction_model }}:{{ book.DevConsole.Dashboard }}** screen will be displayed.

![](/DevConsole/Resources/Images/DevConsole-Interaction_Model_Dashboard.png)

Register the [interaction model predefined](/Design/Design_Guideline_For_Extension.md#DefineInteractionModel) in the extension design phase in the following order:

1. [Adding a built-in slot type](#AddBuiltinSlotType)
2. [Adding a custom slot type](#AddCustomSlotType)
3. [Adding a built-in intent](#AddBuiltinIntent)
4. [Adding a custom intent](#AddCustomIntent)

<div class="note">
  <p><strong>Note!</strong></p>
  <p>Although you can add the required slot type after adding a custom intent, it is better to add the intent after adding the slot type due to the UI characteristics of the Clova developer console.</p>
</div>

## Adding a built-in slot type {#AddBuiltinSlotType}

Once you know the [built-in slot type](/Design/Design_Guideline_For_Extension.md#Slot) to be used by the extension service, you must add the built-in slot type to the interaction model of the extension. For example, if you create a pizza delivery extension, the expression about the pizza quantity can be used in a user utterance. Therefore, in order to use such built-in slot type in the extension, you must add it to the interaction model by following the steps below:

<ol>
  <li>On the top right of the <strong>{{ book.DevConsole.cek_builder_list_title_slottype }}</strong> panel or at the bottom of left menu bar, click the <img class="inlineImage" src="/DevConsole/Resources/Images/DevConsole-Plus_Button.png" /> button on the top right of the <strong>{{ book.DevConsole.cek_builder_list_title_slottype }}</strong> menu area. When you click the button, the <strong>{{ book.DevConsole.cek_interaction_model }}:{{ book.DevConsole.SlotType }}</strong> screen will be displayed.</li>
  <li>In the <strong>{{ book.DevConsole.UseBuiltInSlotType }}</strong> item, check the necessary built-in slot type checkbox.</li>
  <img src="/DevConsole/Resources/Images/DevConsole-Add_Built-in_Slot_Type.png" />
  <li>Select the required built-in slot type and click the <strong>{{ book.DevConsole.cek_save }}</strong> button at the top right of the screen.</li>
</ol>

Once you complete the above steps, you can find that the built-in slot type has been added on the **{{ book.DevConsole.cek_builder_list_title_slottype }}** panel of the **{{ book.DevConsole.cek_interaction_model }}: {{ book.DevConsole.Dashboard }}** screen as shown below.

![](/DevConsole/Resources/Images/DevConsole-Added_Built-in_Slot_Type.png)

## Adding a custom slot type {#AddCustomSlotType}

Now, the [custom slot type](/Design/Design_Guideline_For_Extension.md#Slot) to use in the extension must be defined. Continuing with the example of the pizza delivery service from [adding a built-in slot type](#AddBuiltinSlotType) section, the words used in user utterance for stating the pizza type must be defined as a custom slot type. For example, let’s say that you are adding a custom slot type called "PIZZA_TYPE" with the following representative terms and synonyms.

| Representative Term           | Synonyms                                        |
|----------------|----------------------------------------------|
| Pepperoni          | Pepperoni pizza                                  |
| Barbecue           | Barbecue pizza, BBQ pizza                           |
| Cheese             | Cheese pizza                                     |
| Vegetable             | Vegetable pizza, veggie pizza, vegetarian pizza               |
| Shrimp golden crust | Shrimp golden crust pizza, shrimp gold-crust pizza, shrimp gold-crust |

Follow the steps below to add a custom slot type.

<ol>
  <li>On the top right of the <strong>{{ book.DevConsole.cek_builder_list_title_slottype }}</strong> panel or at the bottom of left menu bar, click the <img class="inlineImage" src="/DevConsole/Resources/Images/DevConsole-Plus_Button.png" /> button on the top right of the <strong>{{ book.DevConsole.cek_builder_list_title_slottype }}</strong> menu area. When you click the button, the <strong>{{ book.DevConsole.cek_interaction_model }}: {{ book.DevConsole.SlotType }}</strong> screen will be displayed.</li>
  <li>Enter the name of the new custom slot type in the <strong>{{ book.DevConsole.CreateSlotType }}</strong> input field and click <strong>{{ book.DevConsole.cek_create }}</strong>. Once the custom slot type is created, the screen to view detailed information on the created slot type will be displayed.</li>
  <img src="/DevConsole/Resources/Images/DevConsole-Add_Custom_Slot_Type_1.png" />
  <li>Under the <strong>{{ book.DevConsole.cek_builder_slottype_dictionary_title }}</strong>, click the <img class="inlineImage" src="/DevConsole/Resources/Images/DevConsole-Plus_Button.png" /> button to add a representative term.</li>
  <img src="/DevConsole/Resources/Images/DevConsole-Add_Custom_Slot_Type_2.png" />
  <li>On the added representative term, add a synonym or a similar expression.</li>
  <img src="/DevConsole/Resources/Images/DevConsole-Add_Custom_Slot_Type_3.png" />
  <li>Finally, click <strong>{{ book.DevConsole.cek_save }}</strong> in the top right section.</li>
</ol>

Go to **{{ book.DevConsole.cek_interaction_model }}: {{ book.DevConsole.Dashboard }}** via the <strong>dashboard</strong> menu on the right to check that the custom slot type has been added.

![](/DevConsole/Resources/Images/DevConsole-Added_Custom_Slot_Type.png)

In case of having to enter large amount of information to the custom slot type, tab-separated values (TSV) file format can be used for batch upload. The first value on each line of the TSV file becomes the representative term and the values classified by the tab characters afterwards become synonyms or similar expressions of the representative term. The following is an example of expressing the definition of the "PIZZA_TYPE" custom slot type in the TSV format.

```
Pepperoni    Pepperoni pizza
Barbecue      Barbecue pizza      BBQ pizza
Cheese       Cheese pizza
Vegetable       Vegetable pizza        Veggie pizza       Vegetarian pizza
Shrimp golden crust         Shrimp golden crust pizza       Shrimp gold-crust pizza       Shrimp gold-crust
```

On the Clova developer console, the **upload** and **download** buttons are provided as follows: Click the **upload** button to upload the custom slot type predefined in the TSV file and click the **download** button to download the custom slot type currently being written on the Clova developer console as a TSV file.

![](/DevConsole/Resources/Images/DevConsole-Custom_Slot_Upload_and_Download_Button.png)

## Adding a built-in intent {#AddBuiltinIntent}

The [built-in intent](/Design/Design_Guideline_For_Extension.md#Intent) is an intent declared by the Clova platform for shared use on common user request types. For example, it has predefined negative/positive user requests or requests, such as cancellations, that can frequently occur in general. Currently, all extensions must be able to process the built-in intents provided by Clova. The details of registered built-in intents of Clova are as follows:

![](/DevConsole/Resources/Images/DevConsole-Built-in_Intent_List.png)

<div class="note">
  <p><strong>Note!</strong></p>
  <p> Changes will be made to allow selective use of built-in intents by each extension.</p>
</div>

## Adding a custom intent {#AddCustomIntent}
If the [built-in slot type](#AddBuiltinSlotType) and the [custom slot type](#AddCustomSlotType) to use for the extension are added, you only need to add the custom intent. Continuing with the previous example, let’s assume that the user is requesting a pizza order. Follow the steps below to add an intent called "OrderPizza":

<ol>
  <li>At the top right of the<strong>{{ book.DevConsole.cek_builder_list_title_intent }}</strong> panel, at the top right of panel or at the bottom of left side menu bar, at the top right of <strong>{{ book.DevConsole.cek_builder_list_title_intent }}</strong> area, click the <img class="inlineImage" src="/DevConsole/Resources/Images/DevConsole-Plus_Button.png" /> button. When you click the button, the <strong>{{ book.DevConsole.cek_interaction_model }}: {{ book.DevConsole.NewIntent }}</strong> screen will be displayed.</li>
  <li>Enter the name of the custom intent to add to the <strong>{{ book.DevConsole.CreateCustomIntent }}</strong> input field and click the <strong>{{ book.DevConsole.cek_create }}</strong>. Once the custom intent is created, the screen to view detailed information on the created custom intent will be displayed.</li>
  <img src="/DevConsole/Resources/Images/DevConsole-Add_Custom_Intent_1.png" />
  <li>Enter a slot name to add in the <strong>{{ book.DevConsole.cek_builder_intent_slot_title }}</strong> input field and click the <img class="inlineImage" src="/DevConsole/Resources/Images/DevConsole-Plus_Button.png" /> button on the right to add the slot.</li>
  <img src="/DevConsole/Resources/Images/DevConsole-Add_Custom_Intent_2.png" />
  <li>After adding Slot, specify its slot type.</li>
  <img src="/DevConsole/Resources/Images/DevConsole-Add_Custom_Intent_3.png" />
  <li>Now, enter the user sample utterance in <strong>{{ book.DevConsole.cek_builder_intent_expression_title }}</strong> and click the <img class="inlineImage" src="/DevConsole/Resources/Images/DevConsole-Plus_Button.png" /> button on the right to add the sample utterance.</li>
  <img src="/DevConsole/Resources/Images/DevConsole-Add_Custom_Intent_4.png" />
  <li>In the added sample utterance, drag the word for the slot value and specify it as the slot.</li>
  <img src="/DevConsole/Resources/Images/DevConsole-Add_Custom_Intent_5.png" />
  <li>Repeat steps 5 and 6 to add as many sample utterances as needed to the intent.</li>
  <li>Finally, click <strong>{{ book.DevConsole.cek_save }}</strong> in the top right section.</li>
</ol>

<div class="note">
  <p><strong>Note!</strong></p>
  <p>The slot type and slot name must be the name of a set or the name that has abstract concept that can be substituted by various types of values.</p>
</div>

Just like adding a custom slot type, you can also use tab-separated values (TSV) file format for batch upload. The TSV file is made up of two parts: one part to define the slot of each intent and the other to list the sample utterances. The definitions of intent’s slots are on the beginning of the file and the slots are listed after the line where `[INTENT SLOT]` is entered. The first column, classified by tab characters, is the slot name used for the intent and the second column is the slot type.

The sample utterance list of intents are on the end of file and sample utterances are listed are the line where `[INTENT EXPRESSION]` is entered. To classify a slot in the sample utterance, the expression must be surrounded using tags made from the slot name. The following is an example of a TSV file that has defined intent.

```
[INTENT SLOT]
pizzaType	PIZZA_TYPE
pizzaAmount	CLOVA.NUMBER

[INTENT EXPRESSION]
Order <pizzaAmount>two boxes</pizzaAmount> of <pizzaType>pepperoni pizza</pizzaType>.
Could you order <pizzaAmount>two boxes</pizzaAmount> of <pizzaType>BBQ pizza</pizzaType>?
Please order <pizzaAmount>two</pizzaAmount> <pizzaType>combinations</pizzaType>.
Get <pizzaAmount>one</pizzaAmount> <pizzaType>shrimp gold-crust pizza</pizzaType>.
...
```

On the Clova developer console, the **upload** and **download** buttons are provided as follows: Click the **upload** button to upload the custom intent predefined in the TSV file and click the **download** button to download the custom intent currently being written on the Clova developer console as a TSV file.

![](/DevConsole/Resources/Images/DevConsole-Utterance_Example_Upload_and_Download_Button.png)

<div class="danger">
  <p><strong>Caution!</strong></p>
  <p>Within an interaction model, declaring the same name for the slot type is recommended regardless of intent. For example, if the slot name related to pizza type ("PIZZA_TYPE") in the "OrderPizza" intent was "pizzaType,” the same name called "pizzaType" must be used by declaring the same slot type even for a different intent. However, in a situation where the purpose of use for the same slot type must be distinguished, such as for "Seoul" and "Busan” in the utterance "Tell me how long it takes from Seoul to Busan,” the name of the slot should be different.</p>
</div>

So far we have described the method of adding an intent to the interaction model. You can repeat the methods described above to add as much as needed intents to the extension to complete an interaction model as shown below.

![](/DevConsole/Resources/Images/DevConsole-Added_Interaction_Model.png)

