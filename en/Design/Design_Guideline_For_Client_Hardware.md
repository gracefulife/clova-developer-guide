# Design guidelines for client devices

A consistent UI and UX must be provided to users of Clova client devices for a familiar, convenient experience when using the product. The design guidelines on the following items are provided for designing the client devices which access Clova.

* [Client states and events](#ClientStateAndEvent)
* [Buttons](#Button)
* [Lights](#Light)
* [Audio](#Audio)
* [Screen](#Screen)

<div class="note">
  <p><strong>Note!</strong></p>
  <p>Any guidelines or specifications not mentioned in this document can be implemented according to the manufacturer's needs or policies. However, if you are uncertain and need help to decide, contact the partnership team.</p>
</div>

## Client states and events {#ClientStateAndEvent}

You should design and implement the client devices for easy user recognition and operation, such as for user voice inputs, Clova voice outputs, microphone states, or error occurrences (e.g. an error in the Clova service or network). For this, you need to understand the states of the client device, and the actions and flow between states. The following diagram shows the client state cycle.

![](/Design/Resources/Images/Clova-Client-State_Diagram.png)

The description on the client states are as follows:

| State                | Description                                                            |
|------------------------|--------------------------------------------------------------------|
| Attending              | A state where the client is waiting for user's voice input.                        |
| Error                  | A state where a system error has occurred.                                                |
| Hearing                | A state where the client is receiving user's voice input.                            |
| Idle                   | A state where client is not performing any tasks.                             |
| Mute on                | A state where microphone is set to mute.                                               |
| Processing & reporting | A state where Clova is processing the user's voice request or Clova's voice is being output through the speakers. |

The above states can be expressed using [Lights](#Light), [Sound effects](#SoundEffect), or [Screens](#Screen). And the transition between states can be initiated or executed by the user's voice, [Buttons](#Button) controls, or other environmental factors.

The following events can occur in the client and it must also be expressed using sounds or lights.

| Event               | Description                                                           |
|------------------------|--------------------------------------------------------------------|
| Alarm             | Sounds at a specified date and time.                                           |
| Reminder       | Displays or reads out content input by the user at a specified date and time.         |
| Timer            | Sounds after a specified time has elapsed.                                        |

## Buttons {#Button}

A client device must provide buttons to allow the user to control the device directly instead of speaking. This section describes the buttons that can be provided by the client and the guidelines for implementation.

* [Button types](#Buttons)
* [Button guidelines](#ButtonGuideline)

### Button types {#Buttons}

A client device must provide the following buttons:

| Button                        | Description                                                     | Required |
|----------------------------|-------------------------------------------------------------|:---------:|
| Power             | Turns the device on or off.                                        | Required      |
| Mic mute    | Enables or disables the microphone.                                | Required      |
| Volume up       | Increases volume of the speaker.                                         | Required      |
| Volume down   | Decreases volume of the speaker.                                          | Required      |
| Play/Pause | Plays or pauses the music. Or, pauses a task in progress.         | Required      |
| Wake up   | Switches to the attending state, a mode to receive the user's voice input. An example of this action is a user saying "Clova." | Optional      |
| Wi-Fi          | Connects or disconnects to a wireless network.                                 | Optional      |
| Bluetooth     | Pairs with, connects to, or disconnects from the Bluetooth device.                              | Optional      |
| Reset          | Resets the device.                                              | Optional      |

### Button guidelines {#ButtonGuideline}

The following guidelines must be followed when providing buttons.

* The power and the mic mute buttons are recommended to be provided as physical buttons.
* Buttons other than the power and the mic mute buttons can be provided in various forms according to the manufacturer's policy, such as a physical or touch UI buttons.
* The most commonly used buttons are recommended to be placed on the front or the top of the client device for easy operation.
* If you are providing a touch UI button, make sure that the defined action is executed upon the touch release gesture.
* If there are no predefined combinations of buttons, only the function of the first recognized button must be executed at a simultaneous input of multiple buttons.
* If there is new button input while a task is already in progress from a previous input, the feedback effect on the previous input must be stopped to provide the feedback effect on the latest input.
* It is permitted to provide the play and pause button as GUIs for devices supporting UI screens.
* The buttons may be provided via the following methods:
  - An exclusive button for one type of function only (e.g. a button for Bluetooth)
  - Using the long-press gesture on the button to provide a function (e.g. reset via the long press gesture of the power button)
  - Using a combination of buttons to provide a function (e.g. reset by pressing the power and play button simultaneously)

## LED {#Light}

A client device must provide lights to indicate the [Client states and events](#ClientStateAndEvent) or the feedback on user request. This section describes the lights that can be provided by the client and the guidelines for implementation.

* [Light colors](#LightColor)
* [Light effects](#LightEffect)
* [Light guidelines](#LightGuideline)

### Light colors {#LightColor}

The client must use the following colors of light:

| Light color     | RGB value                | Description                                   | Required |
|-------------|----------------------|---------------------------------------|:--------:|
| Green       | <span style="color:#32C864; font-size:150%; vertical-align:middle;">&#9724;</span> 50, 200, 100(#32C864)   | Receive user audio input                                  | Required  |
| Yellow Green | <span style="color:#B4FF00; font-size:150%; vertical-align:middle;">&#9724;</span> 180, 255, 0(#B4FF00)    | Clova notifications                             | Required  |
| Red         | <span style="color:#FF0000; font-size:150%; vertical-align:middle;">&#9724;</span> 255, 0, 0(#FF0000)      | Errors, such as mic mute, network connection error, or low battery     | Required  |
| Warm White   | <span style="color:#EDE9E5; font-size:150%; vertical-align:middle;">&#9724;</span> 237, 233, 229(#EDE9E5)  | Output Clova voice through speakers, receive alarm/reminder/timer events                             | Required  |

The following image shows the implementation of light colors on Wave:

| Green       | Yellow Green | Red         | Warm White   |
|-------------|-------------|-------------|-------------|
| ![](/Design/Resources/Images/Clova-Client-Light-Wave_Green.png) | ![](/Design/Resources/Images/Clova-Client-Light-Wave_Yellow_Green.png) | ![](/Design/Resources/Images/Clova-Client-Light-Wave_Red.png) | ![](/Design/Resources/Images/Clova-Client-Light-Wave_Warm_White.png) |

### Light effects {#LightEffect}

Light effects are used for the purpose of delivering a more detailed on the meaning or state on top of the meaning delivered by the [Light colors](#LightColor).

The table below shows the light effects that must be expressed when implemented on a client device along with its descriptions and examples.

| Light effect                            | Description                                      | Example                                                               |
|------------------------------------|------------------------------------------|-------------------------------------------------------------------|
| Lights up                     | Switches directly to the light on state without any other effects.   | ![](/Design/Resources/Images/Clova-Client-Light-Wave_Sustain.gif)              |
| Repeat pulse         | Slowly brightens and dims the intensity of a light repeatedly. | ![](/Design/Resources/Images/Clova-Client-Light-Wave_Repeat_Blink_Slowly.gif)  |
| Fade out                 | Slowly dims the intensity of light to turn off in the end. | ![](/Design/Resources/Images/Clova-Client-Light-Wave_Fade_Out.gif)             |
| Repeat splash          | Repeats the sideways rippling effect. | ![](/Design/Resources/Images/Clova-Client-Light-Wave_Splash.gif)         |

The table below shows how to express the client device's [states and events](#ClientStateAndEvent) using light.

| State or event               | Light effect                | Required |
|----------------------------|----------------------------|:---------:|
| Attending & hearing state     | Turn on the Green light.              | Required     |
| End state                    | Slowly turn off the Warm White light.     | Required     |
| Error state                  | Slowly flicker the Red light repeatedly.       | Required     |
| Mute on state                | Turn on the Red light.                | Required     |
| Processing & reporting state | Slowly flicker the Warm White light repeatedly. | Required     |
| Disabling the mute on state            | Slowly turn off the Red light.           | Required     |
| Immediately after exceeding the wait time           | Slowly turn off the Green light.         | Required     |
| Start alarm, reminder, or timer      | Repeat the rippling effect of the Warm White light.  | Optional     |

### Light guidelines {#LightGuideline}

The following guidelines must be followed when providing lights.
  - A person with eyesight of 0.7 (decimal visual acuity) must be able to distinguish the [Light colors](#LightColor) within 1 meter distance.
  - For light colors, avoid applying states or meanings other than the predefined.
  - The light colors must be applied so that the user can perceive the graphic RGB color and the actual light color as the same.
  - In addition to the essential [Light effects](#LightEffect), you can add other light colors or effects depending on your UX policies or for appropriate situations, such as bootup, speaker volume controls, charging status, and button feedback.
  - It is recommended that you do not express too many meanings or states with a single light color or effect.
  - For screenless devices, it is recommended to indicate the level of the speaker volume by methods, such as brightness of lights.
  - For battery powered portable devices, it is recommended to implement the light effect so the information on the charging status can be gained from the light.

## Sound {#Audio}

This section describes the guidelines for outputting audio content or sound effects from the client device.

* [Rules for basic audio playback](#AudioInterruptionRule)
* [Audio playback rules for user utterance](#AudioInterruptionRuleForUserUtterance)
* [Sound effects](#SoundEffect)
* [Supported audio compression formats](#SupportedAudioCompressionFormat)

### Rules for basic audio playback {#AudioInterruptionRule}

A client may have to play other audio content during audio playback. In this case, the client must play audio content according to the rules for audio playback. The rules for audio playback were written based on the types of audio content. Thus, an understanding of the types of audio content is required before understanding the audio playback rules. The types of audio content are as follows:

| Audio content type | Description                                                                          |
|---------------|-------------------------------------------------------------------------------|
| Alert         | Audio content, such as notification sounds, reminder utterance, alarm sounds, timer sounds, and emergency warning sounds.                   |
| Content       | Audio content, such as music, stories, news, and podcasts provided upon user request.                            |
| Dialogue      | TTS audio content provided on the user request.                                                  |
| Notification  | Beep sound, alarm speech, message push, and system notification (e.g. notification for low battery or Bluetooth disconnection).         |

<div class="note">
  <p><strong>Note!</strong></p>
  <p>Alert and notification types recognize the alarm sounds, beep sounds, and utterance as a single audio content. For example, the reminder recognizes the notification sound and reminder utterance as a single alert audio content. For a low battery notification, the "Not enough battery." notification and the beep sound becomes a single notification audio content.</p>
</div>

The rules for audio playback are as follows:

* For physical buttons, the sound effects must be played instantly being output in the mixing method.
* Audio contents must be played instantly. If an audio content is playing, it must be processed as background audio to play the new audio.
* However, if the [Content type](#AudioInterruptionRule) of the audio playing and the new audio is the same, follow the process below.
  - For **Alert, Dialogue, Content type**: cancel the audio content playing and play the new audio content.
  - For **Notification type**: continue playing the audio content and keep the new audio content in the playback queue. After finishing the current audio content, play the following audio content in the queue order.

Based on above rules, the following table shows how to process the playing audio content for each audio content type:

<table style="text-align:center">
  <thead>
    <tr>
      <th rowspan="2">Type of playing content</th>
      <th colspan="4">Type of content to play</th>
      <th rowspan="2">Sound effect of physical button</th>
    </tr>
    <tr>
      <th>Alert</th>
      <th>Content</th>
      <th>Dialogue</th>
      <th>Notification</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Alert</th>
      <td>Cancel play</td>
      <td>Process as background audio</td>
      <td>Process as background audio</td>
      <td>Process as background audio</td>
      <td rowspan="4">Process mixing</td>
    </tr>
    <tr>
      <th>Content</th>
      <td>Process as background audio</td>
      <td>Cancel play</td>
      <td>Process as background audio</td>
      <td>Process as background audio</td>
    </tr>
    <tr>
      <th>Dialogue</th>
      <td>Process as background audio</td>
      <td>Process as background audio</td>
      <td>Cancel play</td>
      <td>Process as background audio</td>
    </tr>
    <tr>
      <th>Notification</th>
      <td>Process as background audio</td>
      <td>Process as background audio</td>
      <td>Process as background audio</td>
      <td>Continue playing (queue)</td>
    </tr>
  </tbody>
</table>

### Audio playback rules for user utterance {#AudioInterruptionRuleForUserUtterance}

If a user attempts voice input while the client is playing audio content, follow the rules below:

* If there is an audio content being played, process it as a background audio from the attending state to the processing & reporting state.
* If the waiting time for voice input has been exceeded or the user request processing has failed, the audio content processed as the background audio must be played in the original mode.
* In case of having to play other audio content depending on the processed result of the request, audio contents must be played in accordance with the [Rules for basic audio playback](#AudioInterruptionRule).
* The same rules apply for the hearing and processing & reporting states gained from attempting multi-turn conversations.

If there is a request to play a new audio content during the attending and hearing state, process the request as follows:

* For playing audio content of **alert/dialogue/content** type, the audio content must be played after canceling the receipt of user's voice input.
* For playing audio content of **notification** type, the notification audio content must be played as the background audio.

### Sound effects {#SoundEffect}

A client must provide sound effects in addition to the [Lights](#Light) in order to convey the device status or feedback on a user's request. This section explains the types of sound effects to be provided by the client to the user and the situations for providing it.

* [Types of sound effects](#SoundEffects)
* [Sound effect guidelines](#SoundEffectGuideline)

#### Sound effect type {#SoundEffects}

In order to express [states and events](#ClientStateAndEvent) of the client, the following sound effects must be provided:

| State or event              | Sample sound effect                     | Required |
|---------------------------|------------------------------|:---------:|
| Entering the attending state         | <audio title="Attending" controls><source src="./Resources/Sounds/Clova-Client-Soundeffect-Attending.wav" type="audio/wav" /></audio> | Required     |
| Entering the error state             | <audio title="Error" controls><source src="./Resources/Sounds/Clova-Client-SoundEffect-Error.wav" type="audio/wav" /></audio>         | Required     |
| Entering the mute on state           | <audio title="Mute on" controls><source src="./Resources/Sounds/Clova-Client-SoundEffect-Mute_On.wav" type="audio/wav" /></audio>     | Required     |
| Disabling the mute on state           | <audio title="Mute off" controls><source src="./Resources/Sounds/Clova-Client-SoundEffect-Mute_Off.wav" type="audio/wav" /></audio>   | Required     |
| Alarm/reminder (When an event occurs, repeat the sound effect.) | <audio title="Alarm" controls><source src="./Resources/Sounds/Clova-Client-SoundEffect-Alarm.wav" type="audio/wav" /></audio>         | Required     |
| Timer (When an event occurs, repeat the sound effect.)      | <audio title="Timer" controls><source src="./Resources/Sounds/Clova-Client-SoundEffect-Timer.wav" type="audio/wav" /></audio>         | Required     |

#### Sound effect guidelines {#SoundEffectGuideline}

The following guidelines must be followed when providing sound effects.

* It is recommended that the provided sound effects are used without any alteration.
* Other sound effects may be added depending on your UX policies or for appropriate situations.
* Users must be able to recognize each situation by the sound.
* The sound effects must be consistent with the light effects or screen states.
* If you are providing a sound effect for button feedback, it must be suitable to the property and feeling of a button.

### Supported audio compression formats {#SupportedAudioCompressionFormat}

Since a client must play the audio content delivered by Clova, it must be able to play the audio compression formats supported by Clova.

{% include "/Design/SupportedMediaFormat/Supported_Audio_Compression_Format.md" %}

## Screens {#Screen}

The following UI components must be provided on the screen via the display device of the client.

* [Bootscreen](#BootingScreen)
* [Logo display](#DisplayingLogo)
* [Voice agent](#VoiceAgent)

### Bootscreen {#BootingScreen}

This is a screen displayed when device is turned on until booting is complete. A logo is usually displaying on the bootscreen, and the Clova logo must be solely displayed without other logos.

<ul>
  <li>
    <p><strong>Good examples</strong></p>
    <img src="/Design/Resources/Images/Clova-Client-Partner_Logo_on_Loading_Screen.png" /> <img src="/Design/Resources/Images/Clova-Client-Clova_Logo_on_Loading_Screen.png" />
  </li>
  <li>
    <p><strong>Bad examples</strong></p>
    <img src="/Design/Resources/Images/Clova-Client-_Logo_on_Loading_Screen_Bad_Example1.png" /> <img src="/Design/Resources/Images/Clova-Client-_Logo_on_Loading_Screen_Bad_Example2.png" />
  </li>
</ul>

### Logo display {#DisplayingLogo}

The Clova logo can be placed in one of the following layouts on the UI screen.

* [Logo layout A](#LogoLayoutA)
* [Logo layout B](#LogoLayoutB)
* [Logo layout C](#LogoLayoutC)

#### Logo layout A {#LogoLayoutA}

The UI screen covers the entire screen or a section on the lower part of the screen. The Clova logo is placed on the top left section.

![](/Design/Resources/Images/Clova-Client-Logo_Display-Layout_A-Bottom_Overlay.png) ![](/Design/Resources/Images/Clova-Client-Logo_Display-Layout_A-Full_Screen_Overlay.png)

* The Clova logo must be placed on the top left section.
* The Clova logo must not be transparent.

#### Logo layout B {#LogoLayoutB}

Similar to [Logo layout A](#LogoLayoutA), the UI screen covers the entire screen or a section on the lower part of the screen. The Clova logo is placed on the top right section.

![](/Design/Resources/Images/Clova-Client-Logo_Display-Layout_B-Bottom_Overlay.png) ![](/Design/Resources/Images/Clova-Client-Logo_Display-Layout_B-Full_Screen_Overlay.png)

* The Clova logo must be placed on the top right section.
* The Clova logo must not be transparent.

#### Logo layout C {#LogoLayoutC}

The screen only displays simple text format. The Clova logo is placed on the top section.

![](/Design/Resources/Images/Clova-Client-Logo_Display-Layout_C.png)

* The Clova logo must be placed on the top section.
* The source of the content must be stated at the bottom of the content.

### Voice agent {#VoiceAgent}

The voice agent is a UI to express states related to Clova's voice actions, such as receipt of user audio input or Clova audio output. A client device with a screen must implement the voice agent. This section describes the colors used by the voice agent and the guidelines for expressing actions and states according to voice agent types.

* [Voice agent colors](#VoiceAgentColor)
* [Bar type](#BarType)
* [A type icon](#IconAType)
* [B type icon](#IconBType)

#### Voice agent colors {#VoiceAgentColor}

A client must be able to express the [Client states](#ClientStateAndEvent) on the voice agent using the following colors:

| Color      | RGB value             | Color      | RGB value             |
|--------------|-------------------|--------------|-------------------|
| Green1       | <span style="color:#12D5B2; font-size:150%; vertical-align:middle;">&#9724;</span> 18, 213, 178(#12D5B2)   | Green2       | <span style="color:#05D484; font-size:150%; vertical-align:middle;">&#9724;</span> 5, 212, 132 (#05D484)   |
| Red          | <span style="color:#FF0000; font-size:150%; vertical-align:middle;">&#9724;</span> 255, 0, 0(#FF0000)      | Warm White    | <span style="color:#EEFFFC; font-size:150%; vertical-align:middle;">&#9724;</span> 238, 255, 252(#EEFFFC)  |

#### Bar type {#BarType}

A bar-type voice agent is displayed in the form of a long bar as shown in the image below. It is comprised of an area to display voice as text, colors to express state, and a logo. Icons may be included depending on the situation. Below is an example of a bar-type voice agent displayed on a screen.

![](/Design/Resources/Images/Clova-Client-Voice_Agent-Bar_Type.png)

The bar-type voice agent must be expressed as follows for the corresponding situation:

| State                | Animation effect                                                                  | Example                                                                             |
|------------------------|------------------------------------------------------------------------------|---------------------------------------------------------------------------------|
| Attending              | Within 1 second, steadily display the Green1 bar.                                  | <img style="width:600px" src="/Design/Resources/Images/Clova-Client-Voice_Agent-Bar_Type-Attending.gif" /> |
| Hearing                | Expand the color zone from the center depending on the volume of the voice, starting with the color Warm White then Green2.      | <img style="width:600px" src="/Design/Resources/Images/Clova-Client-Voice_Agent-Bar_Type-Hearing.gif" /> |
| Processing & reporting | Move the Warm White zone sideways.                                        | <img style="width:600px" src="/Design/Resources/Images/Clova-Client-Voice_Agent-Bar_Type-ProcessingAndReporting.gif" /> |
| Mute on                | Display the Red bar and the mute or the microphone icon. The icon must then disappear after 2 seconds.       | <img style="width:600px" src="/Design/Resources/Images/Clova-Client-Voice_Agent-Bar_Type-MuteOn.gif" /> |
| Error                  | Display the Red bar and the error icon appears. The icon must then disappear after 2 seconds.                  | <img style="width:600px" src="/Design/Resources/Images/Clova-Client-Voice_Agent-Bar_Type-Error.gif" />  |

<div class="note">
  <p><strong>Note!</strong></p>
  <p>Note that the contents for bar-type UIs are scheduled to be updated in the future.</p>
</div>

#### A type Icon {#IconAType}

The voice agent of A type icons are displayed in the form of icons on the left as shown in the image below. It is comprised of an area to display voice as text, colors to express state, and a logo. Below is an example of an A type voice agent displayed on a screen.

![](/Design/Resources/Images/Clova-Client-Voice_Agent-Icon_A_Type.png)

The voice agent of A type icon must be expressed as follows for the corresponding situation:

| State                | Animation effect                                                                  | Example                                                                              |
|------------------------|------------------------------------------------------------------------------|---------------------------------------------------------------------------------|
| Loading                | Display the Green1 color around the circle.                                          | <img style="width:600px" src="/Design/Resources/Images/Clova-Client-Voice_Agent-Icon_A_Type-Loading.gif" /> |
| Attending              | Display the Green1 colored circle without any animation effect.                                   | <img style="width:600px" src="/Design/Resources/Images/Clova-Client-Voice_Agent-Icon_A_Type-Attending.png" /> |
| Hearing                | Expand the color zone starting with Warm White then Green2, from bottom of the circle to the top depending on the volume of the voice. | <img style="width:600px" src="/Design/Resources/Images/Clova-Client-Voice_Agent-Icon_A_Type-Hearing.gif" /> |
| Processing & reporting | Display the Green2 and Warm White colors around the circle.                                  | <img style="width:600px" src="/Design/Resources/Images/Clova-Client-Voice_Agent-Icon_A_Type-ProcessingAndReporting.gif" /> |
| Mute on                | Display the Red mute or microphone icons. It must be accompanied with the text "Mic is on mute." | <img style="width:600px" src="/Design/Resources/Images/Clova-Client-Voice_Agent-Icon_A_Type-MuteOn.gif" /> |
| Error                  | Display the Red error icon. It must be accompanied with a brief text explanation.            | <img style="width:600px" src="/Design/Resources/Images/Clova-Client-Voice_Agent-Icon_A_Type-Error.gif" /> |

<div class="note">
  <p><strong>Note!</strong></p>
  <p>The loading state refers to the state of preparing the <a href="#VoiceAgent">voice agent</a> in order to receive user input. This state is only applicable for devices with screens and such indication, that the preparation underway for expressing voice agent graphics, must be given to users.</p>
</div>

#### B type Icon {#IconBType}

The B type icons are used when expressing the voice agent from the app type clients, in other words, mobile devices. Below is an example of an B type voice agent displayed on a screen.

![](/Design/Resources/Images/Clova-Client-Voice_Agent-Icon_B_Type.png)

The voice agent of B type icon must be expressed as follows for the corresponding situation:

| State                  | Animation effect                                                                | Example       |
|--------------------------|----------------------------------------------------------------------------|-----------|
| Idle                     | Display the Warm White colored icon without any animation effect.                           | ![](/Design/Resources/Images/Clova-Client-Voice_Agent-Icon_B_Type-Idle.png) |
| Loading                  | Display the Green1 color around the icon.                            | ![](/Design/Resources/Images/Clova-Client-Voice_Agent-Icon_B_Type-Loading.gif) |
| Attending                | Display the Green1 colored icon without any animation effect.                                                      | ![](/Design/Resources/Images/Clova-Client-Voice_Agent-Icon_B_Type-Attending.png) |
| Hearing                  | Display the Warm White and Green2 color consecutively, spinning around the Green1 colored circle.                 | ![](/Design/Resources/Images/Clova-Client-Voice_Agent-Icon_B_Type-Hearing.gif) |
| Processing & reporting   | Display the Warm White and Green 2 color consecutively, spinning around the icon.                                     | ![](/Design/Resources/Images/Clova-Client-Voice_Agent-Icon_B_Type-ProcessingAndReporting.gif) |
| Mute on                  | Display the Red mute or microphone icon.                                                     | ![](/Design/Resources/Images/Clova-Client-Voice_Agent-Icon_B_Type-MuteOn.gif) |
| Error                    | Display the Red error icon.                                                                | ![](/Design/Resources/Images/Clova-Client-Voice_Agent-Icon_B_Type-Error.gif) |

<div class="note">
  <p><strong>Note!</strong></p>
  <p>The loading state refers to the state of preparing the <a href="#VoiceAgent">voice agent</a> in order to receive user input. This state is only applicable for devices with screens and such indication, that the preparation underway for expressing voice agent graphics, must be given to users.</p>
</div>
