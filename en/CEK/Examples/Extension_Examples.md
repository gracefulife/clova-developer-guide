# Extension examples

Here is an explanation of some extensions that are currently serviced by Clova. As these extensions perform simple actions, these examples will be helpful for when implementing your own extension.

* [Magic ball](#MagicBall)
* [Rain sound](#RainSound)
* [Dice drawer](#DiceDrawer)
* [Coin helper](#CoinHelper)

## Magic ball {#MagicBall}

Magic Ball is an extension that returns a random response to a user’s question from 20 positive or negative predefined expressions.

### Features
* It has a simple interaction model, since a random response is given regardless of the user utterance.
* It can be seen as the simplest “echo” level example in terms of server-client programming.
* It is implemented by the Go programming language.

### GitHub repository
https://github.com/naver/clova-extension-sample-magicball

## Rain sound {#RainSound}

Rain Sound is an extension that responds by making the client play the pre-recorded audio file (.mp3) upon user request.

### Features
* The user can select the number of repeats for the rain audio. The interaction of the extension defines the value of repeats as a slot.
* It sends the [response message](/CEK/References/CEK_API.md#CustomExtRequestType) by including not only the guide message but also the [`AudioPlayer.Play`](/CIC/References/CICInterface/AudioPlayer.md#Play) directive message to CEK so that the client can play the audio content.
* It is implemented in Node.js.

### GitHub repository
https://github.com/naver/clova-extension-sample-rainsound

## Dice drawer {#DiceDrawer}

Dice Drawer is an extension that rolls a dice upon a user’s request and tells the results. It tells the sum of results if more than one dice is rolled.

### Features
* The user can select the number of dice to roll. The interaction model of the extension defines the value of the number of dice as a slot.
* The expression returned as a response varies depending on whether the number of rolled dice is one or more than one.
* It is implemented in Node.js.

### GitHub repository
https://github.com/naver/clova-extension-sample-dice

## Coin helper {#CoinHelper}

Coin Helper is an extension that returns the market price information upon a user’s request by calling the REST API provided by an external virtual currency exchange.

### Features
* The user can decide which virtual currency exchange information to use and which virtual currency market price to check. The interaction model of the extension defines the value from the virtual currency exchange and virtual currency type as a slot.
* It uses REST API of an external service to check data from another service.
* It has a slightly more complicated interaction model than other examples.
* It is implemented by the Go programming language.

### GitHub repository

https://github.com/naver/clova-extension-sample-coinhelper
