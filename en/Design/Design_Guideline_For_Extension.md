# Design guidelines for extensions

When creating an extension, you must first consider how your technology and services can bring convenience and the most benefit to users through Clova. The document provides guidelines for designing an extension to bring a healthy and beneficial service to users.

It is possible to create an extension for web service information lookup, shopping and delivery services, interactive games, broadcasts, real-time briefings, IoT device control, and even for other voice-initiated activities or services. Once you know the type of extension you want to create, make sure to create it in accordance with the design guidelines. The details covered here are only the basic recommendations for designing the extension with examples. You can further design and implement the extension according to your own business experience and service characteristics.

* [Setting goals](#SettingGoal)
* [Writing user scenario scripts](#MakeUseCaseScenarioScript)
* [Defining an interaction model](#DefineInteractionModel)
* [Precautions](#Precautions)
* [Supported audio compression formats](#SupportedAudioCompressionFormat)
* [Continuous updates](#ContinuousUpdate)

## Setting goals {#SettingGoal}

The first thing you should do when designing an extension is to set the goals of extension. Setting goals of an extension is a process of deciding what to deliver to users and the method that will be used for delivering it. This process becomes the basis for anticipating the functions to provide to users later on and the user scenarios for using the functions. It may be a single basic and abstract goal for the extension, as shown below.

```
Provide a pizza delivery service to users.
```

This goal can be written again into a series of detailed, more specific goals. See the following items for defining detailed goals:

* Write the detailed goals from the user's point of view.
* Include the details on the ways that the user will call the extension.
* Include the prerequisites fulfilling the detailed goals and the outcomes that can be achieved. The prerequisites may include:
  - Actions or states required in advance
  - Functions or resources required by the extension (e.g. GPS, camera, or microphone)
  - Information on external services or platforms (e.g. information on mobile device contacts or SNS accounts)
* Check to that the collection of detailed goals meets the scopes of extension goals.
* Each detailed goal is recommended to be written on the level of a single user action–a unit that is classified and processed in the service.

Below is an example of detailed goals for a pizza delivery service.

| Detailed goal ID | Classification                | Goal                                                            |
|------------|--------------------|---------------------------------------------------------------|
| #1         | Call service           | A user can start using the pizza delivery service by saying, "On the Pizzabot."    |
| #2         | Usage suggestions or recommendations     | Once the pizza delivery service starts, the user can receive information on the next or the anticipated action for pizza delivery. |
| #3         | Brand lookup and selection     | The user can select a pizza brand of their choice.                                 |
| #4         | Menu lookup and selection      | The user can view the pizza menu.                                   |
| #5         | Order and payment          | The user can order pizza if there is information on the pizza type, quantity, and delivery address. |
| #6         | Usage suggestions or recommendations     | If the user selects a pizza brand of their choice, they can get suggestions for the pizza, the delivery destination, and the payment method based on their latest order information. |
| #7         | Usage suggestions or recommendations     | If the user requests a different menu, they can get a menu recommendation from the extension. |
| #8         | Order and payment          | For payment, the user can apply coupon discounts using the camera.                    |
| #9         | Checking delivery             | Once the order is complete, the user check the preparation and delivery status.  |
| ...        | ...                 | ...                                                            |

<div class="note">
  <p><strong>Note!</strong></p>
  <p>The detailed goals prepared this way become the basis for <a href="#MakeUseCaseScenarioScript">writing user scenario scripts</a> or defining the <a href="#DefineInteractionModel">interaction model</a>. Also, this information is required for <a href="/DevConsole/Guides/CEK/Deploy_Extension.md#InputDeploymentInfo">deploying the extension</a> and will be used as a basis to <a href="/DevConsole/Guides/CEK/Deploy_Extension.md#RequestExtensionSubmission">evaluate</a> the proper operation of the extension.</p>
</div>

## Writing user scenario scripts {#MakeUseCaseScenarioScript}

The user scenario script anticipates the conversation between the user and Clova in advance. By predicting the conversation between the user and Clova, that would be exchanged in various user scenarios based on detailed goals, the level of convenience and flow of the service can be examined. You should write the anticipated user scenario scripts based on the detailed goals defined in [Setting goals](#SettingGoal). This may be used again when registering an [interaction model](#DefineInteractionModel) later on.

See the following recommendations for writing user scenario scripts:

* Write in a colloquial style rather than a written style.
* Do not give too much information or choices when providing information.
* The extension must make suggestions on the next action or make recommendations on service usage to the user.
* Avoid use of repetitive expressions.
* Keep in mind that an unexpected user request or situation can occur at any point.


Below is an sample of a user scenario script.

| Speaker   | Sample utterance                                              | Relevant detailed goal  |
|-----------|------------------------------------------------------|-------------|
| User      | Order a pizza from Pizzabot.                                   | #1           |
| Extension | We have your order history from XX Pizza and YY Pizza. Which one would you like?      | #2, #3       |
| User      | XX Pizza.                                         | #3           |
| Extension | I can order you one combination pizza and one 1.5 liter coke from XX Pizza in XX, to Apartment AA-111. The total is 15 USD and you can pay directly to the deliveryman. Shall I order it?   | #2, #6  |
| User      | Tell me another menu.                                        | #7           |
| Extension | I can order you one super supreme pizza and one 1.5 liter coke to Apartment AA-111. The total is 20 USD and you can pay directly to the deliveryman. Shall I order it? | #2, #7  |
| User      | Yes.                                                  | #5           |
| Extension | I have made your order. Ask me again if you want an update on the order status. | #2, #9       |
| User      | What's the status on my order?                                       | #9           |
| Extension | It's on its way. Please wait a little while longer.                 | #9           |

## Defining an Interaction Model {#DefineInteractionModel}

An interaction model in Clova is a set of rules to convert the voice user request into a standardized format (JSON) to be processed in the extension. For example, if a custom extension is providing a pizza delivery service, a user might say "Order two pepperoni pizzas." The interaction model defines the rules to convert such requests into the format required for providing the service (JSON) as shown below.

![](/Design/Resources/Images/Extension_Design-Interaction_Model_Analysis_Diagram.png)

Before defining the interaction model in the Clova developer console, there is a need to understand and design the model first. If the interaction model is registered in the Clova developer console without such process, the task efficiency may drop or the user requests may not be converted as intended. In order to make an interaction model that accurately identifies the real intention of users, you must first understand the following content before applying it into creating an interaction model.

* [Intent](#Intent)
* [Slot](#Slot)
* [Sample utterances](#UtteranceExample)

### Intent {#Intent}

Intent is a category used for processing user requests. It is usually classified using the **verb** factor in the user’s speech. Then it is divided into a custom intent or built-in intent.

* [Custom intent](#CustomIntent)
* [Built-in intent](#BuiltinIntent)

#### Custom intent {#CustomIntent}

Unlike the built-in intent, custom intent defines the type of user request specialized for the service to be provided. The specification of the custom intent include the following content:
* What type of user requests exist in the service?
* What kind of information ([Slot](#Slot)) is required for each type of user request?
* What are the [Sample utterances](#UtteranceExample) in each type of user request?

Continuing with the example of the pizza delivery service, the service would contain the following request types:

* Request to view menu
* Request to order
* Request to update on delivery status

Based on this example we can see that defining the interaction model of a pizza delivery service (extension) is declaring the intent list, such as view menu intent, order intent, view delivery status intent, and listing the possible utterances and information (slot) required by each intent. Therefore, **the first thing to do when defining an interaction model is to define and list the type of requests that will be processed by the extension.** This also becomes the standard for dividing the business logic–in other words, the branch of program–when developing an extension.

![](/Design/Resources/Images/Extension_Design-Design_Interaction_Model.png)

**Once we have divided the type of user requests, we must name each type.** This will later on become the name of the intent. The "order intent" of a pizza delivery service is an abstract concept and it must be declared as a specific name that can be known by the extension–an indemnifiable string. For example, "order intent" can be declared a name like "OrderPizza.”

Then, you must **define what information ([Slot](#Slot)) is to be recognized** from the utterance of the "OrderPizza" intent and **list various [sample utterances](#UtteranceExample)** on the types of user utterances that can be processed.

#### Built-in intent {#BuiltinIntent}

The built-in intent is a specification declared by the Clova platform for shared used on common user request types. As a commonly invoked intents, the following user requests are allowed:

| Built-in intent       | Intent               | Sample response utterance                                      |
|---------------------------|-------------------|----------------------------------------------------------|
| Clova.GuideIntent         | Help request          | "What can you show me?", "Tell me what you can do.", "What can you do?" |
| Clova.CancelIntent        | Undo action request        | "Cancel.", "Cancel please."                                          |
| Clova.YesIntent           | Positive response (e.g. Yes.)   | "Yes.", "Sure.", "All right.", "Certainly.", "Okay."                   |
| Clova.NoIntent            | Negative response (e.g. No.) | "No.", "No, thank you.", "Absolutely not."                                     |

### Slot {#Slot}

Slot is the information acquired from user utterance and the **noun**factor used in the utterance can become a slot. When defining [custom intent](#Intent), you must define the slot required by the corresponding intent. To explain this more by comparing it with software development, the intent is a function or handler to process a specific type of user request and the slot becomes a parameter required for this function or handler. From the utterance, "Order two pepperoni pizzas." mentioned above, you can see that information on pizza type "pepperoni pizza" and quantity "two" are required to process the "OrderPizza" intent. Therefore, you must identify the information (slot) needed before defining the intent.

When declaring a slot, you must classify the type of information in the slot–called slot type. The slot type is comprised of built-in slot type and custom slot type.

* [Built-in slot type](#BuiltinSlotType)
* [Custom slot type](#CustomSlotType)

#### Built-in slot type {#BuiltinSlotType}

The built-in slot type is an information type pre-defined by Clova which defines information expression that can be universally used in all services (extension). The built-in slot type is mainly used for recognizing information, such as time, place, and quantity. For the above utterance, the built-in slot type can be used to recognize information referring to "2 boxes." Clova provides the following built-in slot types:

| Built-in slot type | Description                                            |
| ----------------------|------------------------------------------------|
| CLOVA.DATETIME      | Information indicating date and time. (e.g.: "10 mins 30 secs,” "9 am,” "1 hour ago,” "12 pm,” "Noon,” "August 4, 2017,” "Last day of previous month") |
| CLOVA.DURATION      | Information indicating a period of time. (e.g.: "One day,” "Overnight,” "One month,” "Next week,” "Weekend") |
| CLOVA.NUMBER        | Information indicating numbers. It includes quantity nouns. (e.g.: "Once,” "7 people,” "One,” "30 years old,” "Around 8,” "16 columns") |
| CLOVA.RELATIVETIME  | Information indicating relative time expressions. (e.g.: "From now on,” "Later,” "In a bit,” "Just now,” "Earlier") |
| CLOVA.UNIT          | Information indicating unit expressions. (e.g.: "374 square meters," "100 MB," "25 miles") |
| CLOVA.ORDER         | Information indicating sequencing expressions. (e.g.: "Next," "Front," "Before," "Last," "This," "Previous") |
| CLOVA.KO_ADDRESS_[Unit for administrative district] | This information indicates the place names that are called according to the domestic unit of administrative districts. You can find the unit of administrative districts provided by Clova in the Clova developer console. |
| CLOVA.WORLD_COUNTRY | Information indicating worldwide country names. (e.g.: "Ghana,” "Japan,” "Korea,” "France") |
| CLOVA.WORLD_CITY    | Information indicating worldwide city names. (e.g.: "New York,” "Paris,” "London") |
| CLOVA.CURRENCY      | Information indicating currency. (e.g.: "Yuan,” "Yen,” "Dollar,” "Russian money,” "British currency") |
| CLOVA.OFFICIALDATE  | Information indicating holidays, national holidays, and memorial days. (e.g.: "Onset of Spring," "New Year's Day," "Buddha's Birthday," "Independence Day") |

#### Custom slot type {#CustomSlotType}

The custom slot type defines information type specialized to the domain of the provided service (extension) and is mainly comprised of proper nouns or nouns. For the aforementioned utterance, the "OrderPizza" intent must identify the relevant information (slot) for the pizza type from user utterance, but there is also a high possibility that the pizza type expressions will be used only in services related to pizza. Therefore, you can define a custom slot type like "PIZZA_TYPE" and declare various items in "PIZZA_TYPE", such as "pepperoni pizza," "combination pizza," and "cheese pizza," which can be ordered from the pizza delivery service.

In a sentence however, these items can be expressed in various ways with a same or similar meaning. "Barbecue pizza" has the same meaning as "BBQ pizza" and long names, such as "shrimp golden crust pizza," may be shortened to "shrimp gold-crust pizza." Therefore, there is a need to not only declare the items classified by the concept, but also the representative term in each item and its synonyms when declaring custom slot types. This allows for converting the various synonyms used in the user utterance to the representative term during the recognition process and helps to receive a unified value of information under a similar concept for when the extension is handling the intent.

Once the slot type is defined in this way, you must define the name of the slot to be used in each intent and declare its slot type. For example, you can declare a "pizzaType" slot for the pizza type information and "pizzaAmount" for the pizza cost for the "OrderPizza" intent and designate the "PIZZA_TYPE" custom slot type predefined to each slot and the CLOVA.NUMBER built-in slot type from the library.

###  Sample utterances {#UtteranceExample}
You can list various sample of user utterances when defining the intent. These sample become the base data necessary for Clova to recognize diverse user expressions with similar intentions and can be used for identifying the location of the aforementioned slot within user utterance. Well written sample utterances help to build a strong interaction model for user intention recognition. When writing sample utterances, it is highly recommended that you follow the recommendations below:

* Input as many sample utterances as possible conveying the same intention but with different expressions.
* Write sample utterances with variations without duplicated patterns.
* Follow the standard below for the required number of sample utterances:
  * For a built-in slot type of an intent or for custom slot type with human-recognizable dictionary size, there should be at least 30 utterance sentences including the slot.
  * For a slot type of an intent with a massive dictionary, such as singer names, song titles, movie titles, or company names, there should be at least 100 utterance sentences including the slot.
  * For an intent in a simple form, only around 10 utterance sentences are required.
* If a new expression is found or there has been a recognition problem with the exiting expression, you should add new samples even after completing the sample utterances in accordance to the recommendations.
* If there is an ambiguous value that is difficult to determine as a slot among the values preregistered in the slot type dictionary, you should specify it as a slot by using it as a sample utterance. However, it is even better to not define any ambiguous values as a slot type in the first place.

The image below provides an understanding on the variations needed for sample utterance without duplicated patterns.

![](/Design/Resources/Images/Extension_Design-Diagram_for_Utterance_Example.png)

For example, let's assume that the following sample utterances was written on intent (OrderPizza) for the pizza delivery service.

```
Order one box of pepperoni pizza.
Get me one pepperoni pizza.
Call for one box of pepperoni pizza.
I wanna one pepperoni pizza.
```

If Clova learns with the above sample utterances where the value `"pepperoni"` and `"one"` is included in the user utterance, the possibility for the utterance to be recognized as the `OrderPizza` intent becomes very high. For example, this means that an utterance that intends to check the menu, such as "How much is one pepperoni pizza?" is likely to be processed as a request to order pizza.

Therefore, writing the sample utterances in the following format is recommended:

```
Order two boxes of pepperoni pizza.
Could you order one box of BBQ pizza?
Please order three combinations.
Get one shrimp gold-crust pizza.
```

The above utterances are organized in the pattern of noun (pizza type), noun (quantity), and verb (intention), and it also includes commonly used prepositions, endings, adverbs, and interjections. Once you have used up all of the possible utterance patterns, you can reuse the patterns but change the slot values to meet the recommended number of utterance sentences. Add to the sample utterances by complying with the following details:
* Add new sentences by changing the slot value used in the sample utterance.
* Add new sentences by changing the style of the sentence, such as the use of prepositions, endings, adverbs, and interjections.
* **Please make sure to avoid repeated use of set combination values.** For example, the utterance "Order two boxes of pepperoni pizza." and "Please order just one pepperoni pizza for me." may have different endings, prepositions, and quantity values, but they have an overlapping combination of values `"pepperoni"` and `"order"`.

```
Quick, order 5 BBQs.
I'll just have one pepperoni.
One vegetable pizza, please.
Please get four tasty cheese pizzas for me.
```

Then the utterance related to the "OrderPizza" intent is enumerated as text and displays the slot sections as below:

{% raw %}

```
Order <pizzaAmount>two boxes</pizzaAmount> <pizzaType>of pepperoni pizza</pizzaType>.
Could you order <pizzaAmount>one box</pizzaAmount> of <pizzaType>BBQ pizza</pizzaType>?
Please order <pizzaAmount>three</pizzaAmount> <pizzaType>combinations</pizzaType>.
Get one <pizzaType>shrimp gold-crust pizza</pizzaType>.
Quick, order <pizzaAmount>5</pizzaAmount> <pizzaType>BBQs</pizzaType>.
I'll just have <pizzaAmount>one</pizzaAmount> <pizzaType>pepperoni</pizzaType>.
One <pizzaType>vegetable pizza</pizzaType>, please.
Please get <pizzaAmount>four</pizzaAmount> tasty <pizzaType>cheese pizzas</pizzaType> for me.
...
```
{% endraw %}

<div class="note">
  <p><strong>Note!</strong></p>
  <p>You can make a continued optimization efforts through <a href="/DevConsole/Guides/CEK/Test_Extension.html#TestInteractionModel">interaction model testing</a> or actual user logs. It is ideal for persons other than the writers of the utterances to test the interaction model. This method will be helpful to find new expression patterns.</p>
</div>


If you [register the interaction model](/DevConsole/Guides/CEK/Register_Interaction_Model.md) as defined above using the [Clova developer console](/DevConsole/ClovaDevConsole_Overview.md), the [registered custom extension](/DevConsole/Guides/CEK/Register_Extension.md) will receive the following JSON message.

{% raw %}

```json
// Custom intent: Order two pepperoni pizzas.
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
          "value": "Pepperoni"
        }
      }
    }
  }
}

// Built-in intent: Cancel, please.
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

## Precautions {#Precautions}

When designing extension, you must take precautionary actions to prevent any potential social or legal issues as described in this section. It is strongly recommended that the details below are reviewed not only at the extension creation phase but also upon registration in Clova and before deployment.

* Review for any violations on copyright protection obligations
* Review for any violations on privacy obligations
* Review for a continuous, not one-time basis, service connection or provision of data
* Review for any provocative content that can be harmful to children or general users

## Supported Audio Compression Formats {#SupportedAudioCompressionFormat}

If audio content is provided by the extension, it must be in an audio compression format supported by Clova.

{% include "/Design/SupportedMediaFormat/Supported_Audio_Compression_Format.md" %}

<div class="danger">
  <p><strong>Caution!</strong></p>
  <p>If music is provided using an audio compression format not supported by Clova, the client may not be able to play the music properly.</p>
</div>

## Continuous updates {#ContinuousUpdate}

During the extension development phase, user scenarios are created based on anticipated user utterances which is then applied to the extension. This helps to develop the extension, however, the actual way that it is used by users can be different and there can even be some unexpected use patterns from users. Basically, users can use the extension differently than anticipated. Therefore, continuous improvement efforts are required to enhance user satisfaction after deploying the extension, such as efforts to improve the extension functions and conversation flow.

Please update the extension after registration, by analyzing the statistics provided by the Clova platform or the incoming user utterance record (scheduled to be provided in the future).
