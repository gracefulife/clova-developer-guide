# Registering an interaction model

When CEK sends user request information to the extension, you must [define the interaction model](/Design/Design_Guideline_For_Extension.md#DefineInteractionModel) in advance on how to analyze user utterances and which format to use for sending them. The interaction model is a schema that has standardized the requests to be received by the [custom extension](/CEK/Guides/Build_Custom_Extension.md).

You can register the interaction model after [registering the extension](/DevConsole/Guides/CEK/Register_Extension.md) on the Clova developer console. In the CEK menu, press the **{{ book.DevConsole.cek_edit }}** button of the extension to register an interaction model as shown below.

![](/DevConsole/Resources/Images/DevConsole-Interaction_Model_Menu.png)

Then, the following **{{ book.DevConsole.cek_interaction_model }}: {{ book.DevConsole.cek_builder_header_title_dashboard }}** screen is displayed.

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

Once you know the [built-in slot type](/Design/Design_Guideline_For_Extension.md#Slot) to be used by the extension service, you must add the built-in slot type to the interaction model of the extension. For example, if you create a pizza delivery extension, an expression about pizza quantity can be used in a user utterance. To use such built-in slot types in the extension, you must add it to the interaction model by following the steps below:

<ol>
  <li>On the top right of the <strong>{{ book.DevConsole.cek_builder_list_title_slottype }}</strong> panel or at the bottom of left menu bar, press the <img class="inlineImage" src="/DevConsole/Resources/Images/DevConsole-Plus_Button.png" /> button located at the top right of the <strong>{{ book.DevConsole.cek_builder_list_title_slottype }}</strong> menu area. When you press the button, the <strong>{{ book.DevConsole.cek_interaction_model }}:{{ book.DevConsole.SlotType }}</strong> screen is displayed.</li>
  <li>On the <strong>{{ book.DevConsole.UseBuiltInSlotType }}</strong> item, check the necessary built-in slot type checkbox.</li>
  <img src="/DevConsole/Resources/Images/DevConsole-Add_Built-in_Slot_Type.png" />
  <li>Select the required built-in slot type and press the <strong>{{ book.DevConsole.cek_save }}</strong> button located at the top right of the screen.</li>
</ol>

Once you complete the above steps, you can find that the built-in slot type is added on the **{{ book.DevConsole.cek_builder_list_title_slottype }}** panel of the **{{ book.DevConsole.cek_interaction_model }}: {{ book.DevConsole.cek_builder_header_title_dashboard }}** screen as shown below.

![](/DevConsole/Resources/Images/DevConsole-Added_Built-in_Slot_Type.png)

## Adding a custom slot type {#AddCustomSlotType}

Now, the [custom slot type](/Design/Design_Guideline_For_Extension.md#Slot) to use in the extension must be defined. Continuing with the example of the pizza delivery service from [adding a built-in slot type](#AddBuiltinSlotType) section, the words used in the user utterance for stating the pizza type must be defined as a custom slot type. For example, let’s say that you are adding a custom slot type called "PIZZA_TYPE" with the following representative terms and synonyms.

| Representative Term | Synonyms                                                              |
|:--------------------|:----------------------------------------------------------------------|
| Pepperoni           | Pepperoni pizza                                                       |
| Barbecue            | Barbecue pizza, BBQ pizza                                             |
| Cheese              | Cheese pizza                                                          |
| Vegetable           | Vegetable pizza, veggie pizza, vegetarian pizza                       |
| Shrimp golden crust | Shrimp golden crust pizza, shrimp gold-crust pizza, shrimp gold-crust |

Follow the steps below to add a custom slot type.

<ol>
  <li>On the top right of the <strong>{{ book.DevConsole.cek_builder_list_title_slottype }}</strong> panel or at the bottom of left menu bar, press the <img class="inlineImage" src="/DevConsole/Resources/Images/DevConsole-Plus_Button.png" /> button located at the top right of the <strong>{{ book.DevConsole.cek_builder_list_title_slottype }}</strong> menu area. When you press the button, the <strong>{{ book.DevConsole.cek_interaction_model }}: {{ book.DevConsole.SlotType }}</strong> screen is displayed.</li>
  <li>Enter the name of the new custom slot type in the <strong>{{ book.DevConsole.cek_builder_new_slottype_title }}</strong> input field and press <strong>{{ book.DevConsole.cek_create }}</strong>. Once the custom slot type is created, the screen to view detailed information on the created slot type is displayed.</li>
  <img src="/DevConsole/Resources/Images/DevConsole-Add_Custom_Slot_Type_1.png" />
  <li>Under the <strong>{{ book.DevConsole.cek_builder_slottype_dictionary_title }}</strong>, press the <img class="inlineImage" src="/DevConsole/Resources/Images/DevConsole-Plus_Button.png" /> button to add a representative term.</li>
  <img src="/DevConsole/Resources/Images/DevConsole-Add_Custom_Slot_Type_2.png" />
  <li>On the added representative term, add a synonym or a similar expression.</li>
  <img src="/DevConsole/Resources/Images/DevConsole-Add_Custom_Slot_Type_3.png" />
  <li>Finally, press <strong>{{ book.DevConsole.cek_save }}</strong> in the top right section.</li>
</ol>

Go to **{{ book.DevConsole.cek_interaction_model }}: {{ book.DevConsole.cek_builder_header_title_dashboard }}** via the <strong>dashboard</strong> menu on the right to check that the custom slot type has been added.

![](/DevConsole/Resources/Images/DevConsole-Added_Custom_Slot_Type.png)

In case of having to enter large amounts of information to the custom slot type, you can use a tab-separated values (TSV) file format to batch upload. The first value on each line of the TSV file becomes the representative term and the values classified by the tab characters afterwards become synonyms or similar expressions of the representative term. The following is an example of expressing the definition of the "PIZZA_TYPE" custom slot type in the TSV format.

```
Pepperoni    Pepperoni pizza
Barbecue      Barbecue pizza      BBQ pizza
Cheese       Cheese pizza
Vegetable       Vegetable pizza        Veggie pizza       Vegetarian pizza
Shrimp golden crust         Shrimp golden crust pizza       Shrimp gold-crust pizza       Shrimp gold-crust
```

On the Clova developer console, the **upload** and **download** buttons are provided as follows: Press the **upload** button to upload the custom slot type predefined in the TSV file and press the **download** button to download the custom slot type currently being written on the Clova developer console as a TSV file.

![](/DevConsole/Resources/Images/DevConsole-Custom_Slot_Upload_and_Download_Button.png)

## Adding a built-in intent {#AddBuiltinIntent}

The [built-in intent](/Design/Design_Guideline_For_Extension.md#Intent) is an intent declared by the Clova platform for shared use on common user request types. For example, it has predefined intents that can frequently occur in general, such as negative/positive user requests or cancellations requests. Currently, all extensions must be able to process the built-in intents provided by Clova. The details of registered built-in intents of Clova are as follows:

![](/DevConsole/Resources/Images/DevConsole-Built-in_Intent_List.png)

<div class="note">
  <p><strong>Note!</strong></p>
  <p> Changes will be made to allow selective use of built-in intents by each extension.</p>
</div>

## Adding a custom intent {#AddCustomIntent}
After adding the [built-in slot type](#AddBuiltinSlotType) and the [custom slot type](#AddCustomSlotType) to use for the extension, you only need to add the custom intent. Continuing with the previous example, this section assumes that the user is requesting a pizza order. Follow the steps below to add an intent called "OrderPizza":

<ol>
  <li>At the top right of the<strong>{{ book.DevConsole.cek_builder_list_title_intent }}</strong> panel, at the top right of panel or at the bottom of left side menu bar, at the top right of <strong>{{ book.DevConsole.cek_builder_list_title_intent }}</strong> area, press the <img class="inlineImage" src="/DevConsole/Resources/Images/DevConsole-Plus_Button.png" /> button. When you press the button, the <strong>{{ book.DevConsole.cek_interaction_model }}: {{ book.DevConsole.NewIntent }}</strong> screen is displayed.</li>
  <li>Enter the name of the custom intent to add to the <strong>{{ book.DevConsole.cek_builder_new_intent }}</strong> input field and press the <strong>{{ book.DevConsole.cek_create }}</strong>. Once the custom intent is created, the screen to view detailed information on the created custom intent is displayed.</li>
  <img src="/DevConsole/Resources/Images/DevConsole-Add_Custom_Intent_1.png" />
  <li>Enter a slot name to add in the <strong>{{ book.DevConsole.cek_builder_intent_slot_title }}</strong> input field and press the <img class="inlineImage" src="/DevConsole/Resources/Images/DevConsole-Plus_Button.png" /> button on the right to add the slot.</li>
  <img src="/DevConsole/Resources/Images/DevConsole-Add_Custom_Intent_2.png" />
  <li>After adding Slot, specify its slot type.</li>
  <img src="/DevConsole/Resources/Images/DevConsole-Add_Custom_Intent_3.png" />
  <li>Now, enter the user sample utterance in <strong>{{ book.DevConsole.cek_builder_intent_expression_title }}</strong> and press the <img class="inlineImage" src="/DevConsole/Resources/Images/DevConsole-Plus_Button.png" /> button on the right to add the sample utterance.</li>
  <img src="/DevConsole/Resources/Images/DevConsole-Add_Custom_Intent_4.png" />
  <li>In the added sample utterance, drag the word for the slot value and specify it as the slot.</li>
  <img src="/DevConsole/Resources/Images/DevConsole-Add_Custom_Intent_5.png" />
  <li>Repeat steps 5 and 6 to add as many sample utterances as needed to the intent.</li>
  <li>Finally, press <strong>{{ book.DevConsole.cek_save }}</strong> in the top right section.</li>
</ol>

<div class="note">
  <p><strong>Note!</strong></p>
  <p>The slot type and slot name must be the name of a set or the name that has abstract concept that can be substituted by various types of values.</p>
</div>

As you can do when adding a custom slot type, you can also use a tab-separated values (TSV) file format for batch upload. The TSV file is comprised of two parts: one part to define the slot of each intent and the other to list the sample utterances. The definitions of intent’s slots are on the beginning of the file and the slots are listed after the line where `[INTENT SLOT]` is entered. The first column, classified by tab characters, is the slot name used for the intent and the second column is the slot type.

The sample utterance list of intents are at the end of the file and sample utterances are listed after the line where `[INTENT EXPRESSION]` is entered. To classify a slot in the sample utterance, the expression must be surrounded using tags made from the slot name. The following is an example of a TSV file that with defined intents.

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

On the Clova developer console, the **upload** and **download** buttons are provided as follows: Press the **upload** button to upload the custom intent predefined in the TSV file and press the **download** button to download the custom intent currently being written on the Clova developer console as a TSV file.

![](/DevConsole/Resources/Images/DevConsole-Utterance_Example_Upload_and_Download_Button.png)

<div class="danger">
  <p><strong>Caution!</strong></p>
  <p>Within an interaction model, declaring the same name for the slot type is recommended regardless of intent. For example, if the slot name related to pizza type ("PIZZA_TYPE") in the "OrderPizza" intent was "pizzaType,” the same name called "pizzaType" must be used by declaring the same slot type even for a different intent. However, in a situation where the purpose of use for the same slot type must be distinguished, such as for "Seoul" and "Busan” in the utterance "Tell me how long it takes from Seoul to Busan,” the name of the slot should be different.</p>
</div>

So far we have described how to add an intent to the interaction model. You can repeat the steps above as much as needed to add intents to the extension to complete an interaction model as shown below.

![](/DevConsole/Resources/Images/DevConsole-Added_Interaction_Model.png)
