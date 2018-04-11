# README
This document is a developer guide and API reference for the CIC and CEK platforms. The target audiences of this document are client developers using CIC to develop electronic devices and apps that link with Clova services and extension developers using CEK to provide online content and services.

<div class="note">
  <p><strong>Note!</strong></p>
  <p>Clova is under continuous development.  Thus, the information in this document is subject to change at any time.</p>
</div>

## Contacts
Contact the Clova partnership team for any inquiries about this document.

## Document version and revision history

The current version of this document is {{ book.DocVersion }} and the revision history is as follows:

<table>
  <thead>
    <tr>
      <th style="width:10%">Version</th><th style="width:15%">Release Date</th><th style="width:75%">History</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>v3.6</td><td>2018-04-02</td>
      <td>
        <ul>
          <li>[CIC] Added message specifications to the <a href="/CIC/References/CICInterface/AudioPlayer.html">AudioPlayer</a> namespace and updated some fields
            <ul>
              <li>Added the <a href="/CIC/References/CICInterface/AudioPlayer.html#ExpectReportPlaybackState">AudioPlayer.ExpectReportPlaybackState</a> directive message, <a href="/CIC/References/CICInterface/AudioPlayer.html#ReportPlaybackState">AudioPlayer.ReportPlaybackState event message</a> {% if book.TargetReaderType == "Internal" %}, <a href="/CIC/References/CICInterface/AudioPlayer.html#RequestPlaybackState">AudioPlayer.RequestPlaybackState</a> event message, and <a href="/CIC/References/CICInterface/AudioPlayer.html#SynchronizePlaybackState">SynchronizePlaybackState directive message</a> {% endif %}</li>
              <li>Updated the payload field of the <a href="/CIC/References/CICInterface/AudioPlayer.html#Play">AudioPlayer.Play</a> directive message</li>
              <li>Added a mandatory token field value to the event field in the name formats of ProgressReportXXX and PlayXXX</li>
            </ul>
          </li>
          <li>[CIC] Added a repeatMode to the <a href="/CIC/References/Context_Objects.html#PlaybackState">AudioPlayer.PlaybackState</a> context object</li>
          <li>[CIC] Added a total of 12 message specifications to the <a href="/CIC/References/CICInterface/PlaybackController.html">PlaybackController</a> namespace
            <ul>
              <li>Added <a href="/CIC/References/CICInterface/PlaybackController.html#PauseCommandIssued">PlaybackController.PauseCommandIssued</a>, <a href="/CIC/References/CICInterface/PlaybackController.html#PlayCommandIssued">PlaybackController.PlayCommandIssued</a>, <a href="/CIC/References/CICInterface/PlaybackController.html#ResumeCommandIssued">PlaybackController.ResumeCommandIssued</a>, <a href="/CIC/References/CICInterface/PlaybackController.html#SetRepeatModeCommandIssued">PlaybackController.SetRepeatModeCommandIssued</a>, and <a href="/CIC/References/CICInterface/PlaybackController.html#StopCommandIssued">PlaybackController.StopCommandIssued</a> event messages</li>
              <li><a href="/CIC/References/CICInterface/PlaybackController.html#ExpectNextCommand">PlaybackController.ExpectNextCommand</a>, <a href="/CIC/References/CICInterface/PlaybackController.html#ExpectPauseCommand">PlaybackController.ExpectPauseCommand</a>, <a href="/CIC/References/CICInterface/PlaybackController.html#ExpectPlayCommand">PlaybackController.ExpectPlayCommand</a>, <a href="/CIC/References/CICInterface/PlaybackController.html#ExpectPreviousCommand">PlaybackController.ExpectPreviousCommand</a>,
<a href="/CIC/References/CICInterface/PlaybackController.html#ExpectResumeCommand">PlaybackController.ExpectResumeCommand</a>, <a href="/CIC/References/CICInterface/PlaybackController.html#ExpectStopCommand">PlaybackController.ExpectStopCommand</a>, and <a href="/CIC/References/CICInterface/PlaybackController.html#SetRepeatMode">PlaybackController.SetRepeatMode</a> directive messages</li>
              <li><a href="/CIC/References/CICInterface/PlaybackController.html#TurnOnRepeatMode">PlaybackController.TurnOnRepeatMode</a> directive message and <a href="/CIC/References/CICInterface/PlaybackController.html#TurnOffRepeatMode">PlaybackController.TurnOffRepeatMode</a> are scheduled to be removed</li>
            </ul>
          </li>
          <li>[CIC] Added the <a href="/CIC/References/CICInterface/TemplateRuntime.html">TemplateRuntime</a> namespace to separate the information for streaming media and metadata for displaying the play list</li>
          <li>[CIC] Added a scanlist field to the <a href="/CIC/References/Context_Objects.html#BluetoothInfoObject">BluetoothInfoObject</a> of <a href="/CIC/References/Context_Objects.html#DeviceState">Device.DeviceState</a></li>
          <li>[CIC] Added the <a href="/CIC/References/CICInterface/DeviceControl.html#BtConnectByPINCode">BtConnectByPINCode</a> directive message and <a href="/CIC/References/CICInterface/DeviceControl.html#BtRequestForPINCode">BtRequestForPINCode</a> and <a href="/CIC/References/CICInterface/DeviceControl.html#BtRequestToCancelPinCodeInput">BtRequestToCancelPinCodeInput</a> event messages to the <a href="/CIC/References/CICInterface/DeviceControl.html">DeviceControl</a> namespace to connect with 3rd party Bluetooth devices which use PIN codes</li>
          <li>[CIC] Added a payload to the <a href="/CIC/References/CICInterface/DeviceControl.html#BtConnect">BtConnect</a> directive message of the <a href="/CIC/References/CICInterface/DeviceControl.html">DeviceControl</a> namespace</li>
          <li>[CEK] Added 10 <a href="/CEK/References/ClovaHomeInterface/Control_Interfaces.html">Control APIs</a>, including GetSleepStartTimeRequest and 4 <a href="/CEK/References/ClovaHomeInterface/Shared_Objects.html">shared objects</a> in the Clova Home extension API</li>
          <li>[CEK] Added the <a href="/CEK/References/ClovaHomeInterface/Shared_Objects.html#CustomCommandInfoObject">CustomCommandInfoObject</a> to the <a href="/CEK/References/ClovaHomeInterface/Discovery_Interfaces.html#DiscoverAppliancesResponse">DiscoverAppliancesResponse</a> of the Clova Home extension API</li>
          <li>[CEK] Removed TimeAmountInfoObject <a href="/CEK/References/ClovaHomeInterface/Shared_Objects.html">shared object</a> from the Clova Home extension API and revised some contents of the <a href="/CEK/References/ClovaHomeInterface/Control_Interfaces.html">Control API</a></li>
          <li>[CEK] Added a tags field and changed the description of the location field in the <a href="/CEK/References/ClovaHomeInterface/Shared_Objects.html#ApplianceInfoObject">ApplianceInfoObject</a> of the Clova Home extension API</li>
          <li>[Dev. console] Updated some UIs on the Clova developer console</li>
        </ul>
      </td>
    </tr>
    <tr>
      <td>v3.5</td><td>2018-03-19</td>
      <td>
        <ul>
          <li>[CIC] Added the <a href="/CIC/References/Context_Objects.html#SoundOutputInfoObject">SoundOutputInfoObject</a> to the <a href="/CIC/References/Context_Objects.html#DeviceState">Device.DeviceState</a></li>
          <li>[CIC] Added the <a href="/CIC/References/CICInterface/PlaybackController.html#CustomCommandIssued">CustomCommandIssued</a> event message, that can execute customized commands of a user, to the <a href="/CIC/References/CICInterface/PlaybackController.html#CustomCommandIssued">PlaybackController</a> namespace</li>
          <li>[CEK] Added 48 <a href="/CEK/References/ClovaHomeInterface/Control_Interfaces.html">Control APIs</a>, including CloseConfirmation and 10 types of <a href="/CEK/References/ClovaHomeInterface/Shared_Objects.html">shared objects</a> in the Clova Home API</li>
          <li>[CEK] Added 30 more Clova Home API <a href="/CEK/References/ClovaHomeInterface/Shared_Objects.html#ApplianceInfoObject">supported appliances</a></li>
        </ul>
      </td>
    </tr>
    <tr>
      <td>v3.4</td><td>2018-03-05</td>
      <td>
        <ul>
          <li>[CIC] Modified the description of the initiator field of the <a  href="/CIC/References/CICInterface/SpeechRecognizer.html#Recognize">SpeechRecognizer.Recognize</a> event message</li>
          <li>[CIC] Changed the name of the hearing state in client states to listening state in the <a href="/Design/Design_Guideline_For_Client_Hardware.html">design guidelines for client devices</a></li>
          <li>[CIC] Added a feedback type in the audio content type and rules on the description in <a href="/Design/Design_Guideline_For_Client_Hardware.html#Audio">audio</a> section in the design guidelines for client devices</li>
          <li>[CEK] Added the <a href="/CEK/Tutorials/Use_Builtin_Type_Slots.html">Utilizing user input information</a> page in the <a href="/CEK/Tutorials/Introduction.html">tutorial</a></li>
        </ul>
      </td>
    </tr>
    <tr>
      <td>v3.3</td><td>2018-02-26</td>
      <td>
        <ul>
          <li>[CIC] Added a deviceUUID field to the initiator field of the <a href="/CIC/References/CICInterface/SpeechRecognizer.html#Recognize">SpeechRecognizer.Recognize</a> event message</li>
          <li>[CIC] Added <a href="/CIC/References/CICInterface/Alerts.html#RequestSynchronizeAlert">RequestSynchronizeAlert</a> event message and <a href="/CIC/References/CICInterface/Alerts.html#SynchronizeAlert">SynchronizeAlert</a> directive message related to alarm synchronization to the <a href="/CIC/References/CICInterface/Alerts.html">Alerts</a> namespace</li>
          <li>[CIC] Scheduled to remove some fields related to alarm synchronization from the System namespace</li>
        </ul>
      </td>
    </tr>
    <tr>
      <td>v3.2</td><td>2018-02-19</td>
      <td>
        <ul>
          <li>[CIC] Added the initiator field to the <a href="/CIC/References/CICInterface/SpeechRecognizer.html#Recognize">SpeechRecognizer.Recognize</a> event message to accurately identify the user invocation</li>
          <li>[CIC] Added the label field to the <a href="/CIC/References/CICInterface/Alerts.html#SetAlert">Alerts.SetAlert</a> directive message to check details of reminders and scheduled actions</li>
          <li>[CIC] Added the label field to the <a href="/CIC/References/ContentTemplates/ActionTimer.html">ActionTimer</a>, <a href="/CIC/References/ContentTemplates/ActionTimerList.html">ActionTimerList</a>, <a href="/CIC/References/ContentTemplates/Reminder.html">Reminder</a>, and <a href="/CIC/References/ContentTemplates/ReminderList.html">ReminderList</a> templates to display the details of reminders and scheduled actions</li>
        </ul>
      </td>
    </tr>
    <tr>
      <td>v3.1</td><td>2018-02-05</td>
      <td>
        <ul>
          <li>[CIC] Modified the description of the durationInMilliseconds field of <a href="/CIC/References/CICInterface/AudioPlayer.html#AudioStreamInfoObject">AudioStreamInfoObject</a></li>
          <li>[CIC] Added information such as a field to state the source of the following templates: <a href="/CIC/References/ContentTemplates/Atmosphere.html">Atmosphere</a>, <a href="/CIC/References/ContentTemplates/CardList.html">CardList</a>, <a href="/CIC/References/ContentTemplates/Humidity.html">Humidity</a>, <a href="/CIC/References/ContentTemplates/TodayWeather.html">TodayWeather</a>, <a href="CIC/References/ContentTemplates/TomorrowWeather.html">TomorrowWeather</a>, <a href="/CIC/References/ContentTemplates/WeeklyWeather.html">WeeklyWeather</a>, and <a href="CIC/References/ContentTemplates/WindSpeed.html">WindSpeed</a></li>
          <li>[CEK] Modified the description of the request (<a href="CEK/Guides/Build_Custom_Extension.html#HandleLaunchRequest">LaunchRequest</a>) to invoke extension and applied the content of <a href="/Design/Design_Guideline_For_Extension.html">Design guidelines for extensions</a></li>
          <li>[CEK] Added a list of <a href="/CEK/CEK_Overview.html#WhatisCEK">HTTP versions</a> used for communicating between CEK and extensions</li>
          <li>[CEK] Added the <a href="/CEK/Tutorials/Handle_Builtin_Intents.html">Handling built-in intents</a> page to the <a href="/CEK/Tutorials/Introduction.html">tutorial</a></li>
          <li>[Dev. console] Specified the <a href="/DevConsole/Guides/CEK/Register_Extension.html#SetServerConnection">port</a> to be used by the extension server</li>
          <li>[Common] Emended some errors in the document</li>
        </ul>
      </td>
    </tr>
    <tr>
      <td>v3.0</td><td>2018-01-29</td>
      <td>
        <ul>
          <li>[Design] Added <a href="/Design/Design_Guideline_For_Client_Hardware.html#SoundEffect">sound effects for reminders</a> in the <a href="/Design/Design_Guideline_For_Client_Hardware.html">Design guidelines for client devices</a></li>
          <li>[CIC] Added a <a href="/CIC/References/CICInterface/Notifier.html#Notify">Notifier.Notify</a> event message to the <a href="/CIC/References/CICInterface/Notifier.html">Notifier</a> namespace and updated the payload field of the namespace</li>
          <li>[CIC] Added <a href="/CIC/References/CICInterface/SpeechSynthesizer.html#SpeechFinished">SpeechFinished</a>, <a href="/CIC/References/CICInterface/SpeechSynthesizer.html#SpeechStarted">SpeechStarted</a>, and <a href="/CIC/References/CICInterface/SpeechSynthesizer.html#SpeechStopped">SpeechStopped</a> event messages to the <a href="/CIC/References/ContextObjects/SpeechState.html">SpeechSynthesizer.SpeechState</a> and <a href="/CIC/References/CICInterface/SpeechSynthesizer.html">SpeechSynthesizer</a> namespaces</li>
          <li>[CIC] Added speechId and explicit fields to the <a href="/CIC/References/CICInterface/TextRecognizer.html">TextRecognizer.Recognize</a> event message for multi-turn dialogs</li>
          <li>[CEK] Added <a href="/CEK/References/ClovaHomeInterface/Error_Interfaces.html#NoSuchTargetError">NoSuchTargetError</a>, <a href="/CEK/References/ClovaHomeInterface/Error_Interfaces.html#NotSupportedInCurrentModeError">NotSupportedInCurrentModeError</a>, <a href="/CEK/References/ClovaHomeInterface/Error_Interfaces.html#UnsupportedOperationError">UnsupportedOperationError</a>, and <a href="/CEK/References/ClovaHomeInterface/Error_Interfaces.html#ValueOutOfRangeError">ValueOutOfRangeError</a> to the <a href="/CEK/References/ClovaHomeInterface/Error_Interfaces.html">error interface</a> among the Clova Home extension message references</li>
          <li>[Dev. console] Added the method to check the connection before <a href="/DevConsole/Guides/CEK/Register_Extension.html#SetServerConnection">setting an extension server connection</a> and added a guide on the <a href="/DevConsole/Guides/CEK/Test_Extension.html#TestOnClovaApp">automated application of tester IDs</a></li>
          <li>[Dev. console] Updated some UIs on the Clova developer console</li>
        </ul>
      </td>
    </tr>
    <tr>
      <td>v2.9</td><td>2018-01-22</td>
      <td>
        <ul>
          <li>[Design] Added the chapter on supported audio compression formats in the <a href="/Design/Design_Guideline_For_Client_Hardware.html#SupportedAudioCompressionFormat">design guidelines for client devices</a> and <a href="/Design/Design_Guideline_For_Extension.html#SupportedAudioCompressionFormat">design guidelines for extensions</a></li>
          <li>[CEK] Added a <a href="/CEK/Tutorials/Introduction.html">Tutorial</a> page and a page on<a href="/CEK/Tutorials/Build_Simple_Extension.html">Building a basic extension</a></li>
          <li>[Dev. console] Displayed the <a href="/DevConsole/Guides/CEK/Register_Interaction_Model.html#AddCustomSlotType">list of built-in intents</a> and added UI for writing messages for a <a href="/DevConsole/Guides/CEK/Deploy_Extension.html#InputComplianceInfo">review request</a></li>
          <li>[Common] Changed the image format of the UML diagram</li>
        </ul>
      </td>
    </tr>
    <tr>
      <td>v2.8</td><td>2018-01-15</td>
      <td>
        <ul>
          <li>[Design] Added the guideline descriptions on light and sound effects for alarms, reminders, and timers to the <a href="/Design/Design_Guideline_For_Client_Hardware.html">Design guidelines for client devices</a></li>
        </ul>
      </td>
    </tr>
    <tr>
      <td>v2.7</td><td>2018-01-08</td>
      <td>
        <ul>
          <li>[Design] Modified the description of the <a href="/Design/Design_Guideline_For_Extension.html#DefineInteractionModel">built-in intent</a> based on platform implementation</li>
          <li>[CIC] Added a section on <a href="/CIC/Guides/Interact_with_CIC.html#HandleDelegation">handling delegated user requests</a> and added a <a href="/CIC/References/CICInterface/Clova.html#HandleDelegatedEvent">Clova.HandleDelegatedEvent</a> directive message and a <a href="/CIC/References/CICInterface/Clova.html#ProcessDelegatedEvent">Clova.ProcessDelegatedEvent</a> event message</li>
          <li>[CIC] Added a description to include the <a href="/CIC/References/Context_Objects.html#PlaybackState">AudioPlayer.PlaybackState</a> context information in <a href="/CIC/References/CICInterface/PlaybackController.html#NextCommandIssued">PlaybackController.NextCommandIssued</a> and <a href="/CIC/References/CICInterface/PlaybackController.html#PreviousCommandIssued">PlaybackController.PreviousCommandIssued</a> event messages</li>
          <li>[CIC] Revised the description of the <a href="/CIC/References/CICInterface/Alerts.html#AlertsWorkFlow">interaction structure</a> of the <a href="/CIC/References/CICInterface/Alerts.html">Alerts</a> API</li>
          <li>[CIC] Added the description of the <a href="/CIC/References/CICInterface/DeviceControl.html#DeviceContorlWorkFlow">interaction structure</a> of the <a href="/CIC/References/CICInterface/DeviceControl.html">DeviceControl</a> API</li>
          <li>[CIC] Emended errors on some content templates and shared objects</li>
          <li>[CEK] Added the <a href="/CEK/Examples/Extension_Examples.html">Extension examples</a> page</li>
          <li>[Dev. console] Updated the description on <a href="/DevConsole/Guides/CEK/Test_Extension.html">testing an extension</a> due to the added <strong>tester ID</strong> field</li>
        </ul>
      </td>
    </tr>
    <tr>
      <td>v2.6</td><td>2018-01-02</td>
      <td>
        <ul>
          <li>[CIC] Added error code 429 and its description in the Remarks of the section <a href="/CIC/References/CIC_API.html#EstablishDownchannel">Establishing a downchannel</a></li>
          <li>[CIC] Removed route-finding templates (CarRoute, TransportationRoute) and the UI for route-finder was replaced with an ImageText template</li>
          <li>[Common] Emended some errors and typos in the document</li>
        </ul>
      </td>
    </tr>
    <tr>
      <td>v2.5</td><td>2017-12-18</td>
      <td>
        <ul>
          <li>[Design] Moved the section on <a href="/Design/Design_Guideline_For_Extension.html#DefineInteractionModel">Defining an interaction model</a> in <a href="/DevConsole/Guides/CEK/Register_Interaction_Model.html">Registering interaction model</a> to <a href="/Design/Design_Guideline_For_Extension.html">Design guidelines for extensions</a></li>
          <li>[Design] Added a guideline to prepare <a href="/Design/Design_Guideline_For_Extension.html#UtteranceExample">sample utterances</a> in the section on <a href="/Design/Design_Guideline_For_Extension.html#DefineInteractionModel">Defining an interaction model</a></li>
          <li>[CIC] Removed ExpectSpeechTimedOut event message from the <a href="/CIC/References/CICInterface/SpeechRecognizer.html">SpeechRecognizer</a> interface</li>
          <li>[CIC] Removed the Clova.FreetalkState object from the <a href="/CIC/References/Context_Objects.html">context information</a></li>
          <li>[Dev. console] Added a description on how to use the test mode in <a href="/DevConsole/Guides/CEK/Test_Extension.html">Testing an extension</a></li>
          <li>[Dev. console] Modified image and description due to UI improvements</li>
          <li>[Dev. console] Added sections <a href="/DevConsole/Guides/CEK/Update_Extension.html">Updating an extension</a> and <a href="/DevConsole/Guides/CEK/Remove_Extension.html">Disabling and deleting an extension</a></li>
        </ul>
      </td>
    </tr>
    <tr>
      <td>v2.4</td><td>2017-12-11</td>
      <td>
        <ul>
          <li>[Design] Added <a href="/Design/Design_Guideline_For_Extension.html">Design guidelines for extensions</a></li>
          <li>[CIC] Added <a href="/CIC/References/CICInterface/AudioPlayer.html#ClearQueue">ClearQueue</a> directive message to the <a href="/CIC/References/CICInterface/AudioPlayer.html">AudioPlayer</a> interface</li>
        </ul>
      </td>
    </tr>
    <tr>
      <td>v2.3</td><td>2017-12-04</td>
      <td>
        <ul>
          <li>[Design] Added <a href="/Design/Design_Guideline_For_Client_Hardware.html#AudioInterruptionRule">audio interruption rules</a> to the <a href="/Design/Design_Guideline_For_Client_Hardware.html">Design guidelines for client devices</a></li>
          <li>[Design] Improved the images in <a href="/Design/Design_Guideline_For_Client_Hardware.html">Design guidelines for client devices</a></li>
          <li>[CIC] Added the section on <a href="/CIC/Guides/Interact_with_CIC.html#UserAgentString">user-agent strings</a> for prerequisites before interacting with CIC</li>
          <li>[CIC] Added the description of the 412 Precondition failed code in the <a href="/CIC/References/CIC_API.html#SendEvent">Sending event messages</a> section of the <a href="/CIC/References/CIC_API.html">CIC API reference</a></li>
          <li>[CEK] Added a reprompt field in the <a href="/CEK/References/CEK_API.html#CustomExtResponseMessage">response message</a> to encourage multi-turn dialogs with the user</li>
          <li>[CEK] Emended errors in the document</li>
        </ul>
      </td>
    </tr>
    <tr>
      <td>v2.2</td><td>2017-11-20</td>
      <td>
        <ul>
          <li>[Design] Added <a href="/Design/Design_Guideline_For_Client_Hardware.html">Design guidelines for client devices</a></li>
          <li>[CIC] Added Type5 and Type6 to the subType value of the <a href="/CIC/References/ContentTemplates/CardList.html">CardList template</a> to display audio content and image thumbnails</li>
          <li>[CEK] Changed the name of a <a href="/CEK/References/ClovaHomeInterface/Shared_Objects.html">shared object</a>, HeatingModeInfoObject of the Clova Home extension message to <a href="/CEK/References/ClovaHomeInterface/Shared_Objects.html#ModeInfoObject">ModeInfoObject</a> and modified the description as an object indicating the operation mode of universal devices</li>
          <li>[CEK] Added the <a href="/CEK/References/ClovaHomeInterface/Control_Interfaces.html#GetCurrentTemperatureRequest">GetCurrentTemperatureRequest</a> message and the <a href="/CEK/References/ClovaHomeInterface/Control_Interfaces.html#GetCurrentTemperatureResponse">GetCurrentTemperatureResponse</a> message to the <a href="/CEK/References/ClovaHomeInterface/Control_Interfaces.html">Control</a> interface of the Clova Home extension message</li>
          <li>[CEK] Added the <a href="/CEK/References/ClovaHomeInterface/Error_Interfaces.html#UnsupportedOperationError">UnsupportedOperationError</a> message to the <a href="/CEK/References/ClovaHomeInterface/Error_Interfaces.html">error</a> interface of the Clova Home extension message</li>
        </ul>
      </td>
    </tr>
    <tr>
      <td>v2.1</td><td>2017-11-13</td>
      <td>
        <ul>
          <li>[CIC] Added UX details in the Remarks of directive messages for volume control (<a href="/CIC/References/CICInterface/DeviceControl.html#Decrease">DeviceControl.Decrease</a>, <a href="/CIC/References/CICInterface/DeviceControl.html#Increase">DeviceControl.Increase</a>, <a href="/CIC/References/CICInterface/DeviceControl.html#SetValue">DeviceControl.SetValue</a>, <a href="/CIC/References/CICInterface/PlaybackController.html#Mute">PlaybackController.Mute</a>, and <a href="/CIC/References/CICInterface/PlaybackController.html#Unmute">PlaybackController.Unmute</a>)</li>
          <li>[CEK] Added DecrementFanSpeed, IncrementFanSpeed, SetFanSpeed, and SetMode actions to the AIRCONDITIONER type, and added SetFanSpeed to the HUMIDIFIER type in the <a href="/CEK/References/ClovaHomeInterface/Shared_Objects.html#ApplianceInfoObject">ApplianceInfoObject</a></li>
        </ul>
      </td>
    </tr>
    <tr>
      <td>v2.0</td><td>2017-11-06</td>
      <td>
        <ul>
          <li>[CIC] Added the <a href="/CIC/References/CICInterface/SpeechRecognizer.html#KeepRecording">SpeechRecognizer.KeepRecording</a> directive message</li>
          <li>[CIC] Added <a href="/CIC/References/Context_Objects.html#Display">Device.Display</a> context information</li>
          <li>[CIC] Added a token field to the <a href="/CIC/References/ContentTemplates/ActionTimer.html">ActionTimer</a>, <a href="/CIC/References/ContentTemplates/ActionTimerList.html">ActionTimerList</a>, <a href="/CIC/References/ContentTemplates/Alarm.html">Alarm</a>, <a href="/CIC/References/ContentTemplates/AlarmList.html">AlarmList</a>, <a href="/CIC/References/ContentTemplates/Memo.html">Memo</a>, <a href="/CIC/References/ContentTemplates/MemoList.html">MemoList</a>, <a href="/CIC/References/ContentTemplates/Reminder.html">Reminder</a>, <a href="/CIC/References/ContentTemplates/ReminderList.html">ReminderList</a>, <a href="/CIC/References/ContentTemplates/Schedule.html">Schedule</a>, <a href="/CIC/References/ContentTemplates/ScheduleList.html">ScheduleList</a>, <a href="/CIC/References/ContentTemplates/Timer.html">Timer</a>, and <a href="/CIC/References/ContentTemplates/TimerList.html">TimerList</a> templates</li>
          <li>[CEK] Changed the name of the context.System.device.displayType to context.System.device.display from the request messages of <a href="/CEK/References/CEK_API.html#CustomExtMessage">custom extension messages</a> and changed the sub-field configuration</li>
        </ul>
      </td>
    </tr>
    <tr>
      <td>v1.9</td><td>2017-10-30</td>
      <td>
        <ul>
          <li>[Dev. console] Added the description for the <a href="/DevConsole/ClovaDevConsole_Overview.html">Clova developer console overview</a></li>
          <li>[Dev. console] Added the guide for <a href="/DevConsole/Guides/CEK/Register_Extension.html">Registering an extension</a></li>
          <li>[Dev. console] Added the guide for <a href="/DevConsole/Guides/CEK/Register_Interaction_Model.html">Registering an interaction model</a></li>
          <li>[Dev. console] Added the guide for <a href="/DevConsole/Guides/CEK/Deploy_Extension.html">Deploying an extension</a></li>
        </ul>
      </td>
    </tr>
    <tr>
      <td>v1.8</td><td>2017-10-23</td>
      <td>
        <ul>
          <li>[CIC] Added emotionCode and motionCode fields to the <a href="/CIC/References/ContentTemplates/Text.html">Text</a> template</li>
          <li>[CIC] Changed assets[].url field contents of <a href="/CIC/References/CICInterface/Alerts.html#SetAlert">Alerts.SetAlert</a> directive message</li>
          <li>[CIC] Revised an example error for the <a href="/CIC/References/CICInterface/AudioPlayer.html#StreamRequested">AudioPlayer.StreamRequested</a> event message</li>
          <li>[CEK] Added context.System.device.displayType field to the request message in the request message of <a href="/CEK/References/CEK_API.html#CustomExtMessage">custom extension messages</a></li>
        </ul>
      </td>
    </tr>
    <tr>
      <td>v1.7</td><td>2017-10-16</td>
      <td>
        <ul>
          <li>[CIC] Added <a href="/CIC/References/CICInterface/PlaybackController.html#Replay">Replay</a> directive message to the <a href="/CIC/References/CICInterface/PlaybackController.html">PlaybackController</a> namespace</li>
          <li>[CIC] Added supplementary information on alarm synchronization in the <a href="/CIC/References/CICInterface/Alerts.html#AlertsWorkFlow">Overall process</a> section</li>
          <li>[CIC] Removed the content field from the <a href="/CIC/References/Context_Objects.html#AlertsState">Alert.AlertsState</a> of <a href="/CIC/References/Context_Objects.html#AlertInfoObject">AlertInfoObject</a> context information</li>
          <li>[Common] Modified images and emended errors in the document</li>
        </ul>
      </td>
    </tr>
    <tr>
      <td>v1.6</td><td>2017-10-02</td>
      <td>
        <ul>
          <li>[CIC] Added the <a href="/CIC/References/CICInterface/Alerts.html">Alerts</a> namespace and alarm related interface</li>
          <li>[CIC] Added the <a href="/CIC/References/CICInterface/System.html">System</a> namespace and alarm related interface</li>
          <li>[CIC] Added the expectContentType field to the <a href="/CIC/References/CICInterface/SpeechRecognizer.html#ExpectSpeech">SpeechRecognizer.ExpectSpeech</a> directive message</li>
          <li>[CIC] Added a warning field to the <a href="/CIC/References/Context_Objects.html#VolumeInfoObject">VolumeInfoObject</a> of <a href="/CIC/References/Context_Objects.html#DeviceState">Device.DeviceState</a></li>
          <li>[CIC] Added templates: <a href="/CIC/References/ContentTemplates/ActionTimer.html">ActionTimer</a>, <a href="/CIC/References/ContentTemplates/ActionTimerList.html">ActionTimerList</a>, <a href="/CIC/References/ContentTemplates/Alarm.html">Alarm</a>, <a href="/CIC/References/ContentTemplates/AlarmList.html">AlarmList</a>, <a href="/CIC/References/ContentTemplates/Memo.html">Memo</a>, <a href="/CIC/References/ContentTemplates/MemoList.html">MemoList</a>, <a href="/CIC/References/ContentTemplates/Reminder.html">Reminder</a>, <a href="/CIC/References/ContentTemplates/ReminderList.html">ReminderList</a>, <a href="/CIC/References/ContentTemplates/Schedule.html">Schedule</a>, <a href="/CIC/References/ContentTemplates/ScheduleList.html">ScheduleList</a>, <a href="/CIC/References/ContentTemplates/Timer.html">Timer</a>, and <a href="/CIC/References/ContentTemplates/TimerList.html">TimerList</a></li>
          <li>[CIC] Modified some code examples of the <a href="/CIC/References/ContentTemplates/ImageText.html">ImageText</a> template</li>
          <li>[CIC] Modified some fields of the <a href="/CIC/References/ContentTemplates/Popup.html">Popup</a> template</li>
          <li>[CIC] Added the Terms and Conditions of Service on <a href="/CIC/Guides/Interact_with_CIC.html#CreateClovaAccessToken">Creating Clova access tokens</a> and <a href="/CIC/References/Clova_Auth_API.html#RequestAuthorizationCode">Requesting an authorization code</a></li>
        </ul>
      </td>
    </tr>
    <tr>
      <td>v1.5</td><td>2017-09-25</td>
      <td>
        <ul>
          <li>[CIC] Added <a href="/CIC/References/CICInterface/PlaybackController.html#NextCommandIssued">PlaybackController.NextCommandIssued</a> and <a href="/CIC/References/CICInterface/PlaybackController.html#PreviousCommandIssued">PlaybackController.PreviousCommandIssued</a> event messages for music playback control to the <a href="/CIC/References/CICInterface/PlaybackController.html">PlaybackController API</a></li>
          <li>[CIC] Added expectSpeechId field to the <a href="/CIC/References/CICInterface/SpeechRecognizer.html#ExpectSpeech">SpeechRecognizer.ExpectSpeech</a> directive message, and added speechId and explicit fields to the <a href="/CIC/References/CICInterface/SpeechRecognizer.html#Recognize">SpeechRecognizer.Recognize</a> event message</li>
          <li>[CIC] Added the <a href="/CIC/References/ContentTemplates/Popup.html">Popup template</a></li>
          <li>[CEK] Added 34 <a href="/CEK/References/ClovaHomeInterface/Control_Interfaces.html">Control APIs</a>, including ChargeConfirmation in the Clova Home API</li>
          <li>[CEK] Added 6 more Clova Home API <a href="/CEK/References/ClovaHomeInterface/Shared_Objects.html#ApplianceInfoObject">supported appliances</a> and added a location field</li>
        </ul>
      </td>
    </tr>
    <tr>
      <td>v1.4</td><td>2017-09-18</td>
      <td>
        <ul>
          <li>[CIC] Added <a href="/CIC/References/CICInterface/DeviceControl.html#ExpectReportState">DeviceControl.ExpectReportState</a> directive message, <a href="/CIC/References/CICInterface/DeviceControl.html#ReportState">DeviceControl.ReportState</a> event message, and <a href="/CIC/References/CICInterface/DeviceControl.html#RequestStateSynchronization">DeviceControl.RequestStateSynchronization</a> event message to DeviceControl API. Changed the name of the DeviceControl.UpdateDeviceState directive message to <a href="/CIC/References/CICInterface/DeviceControl.html#SynchronizeState">DeviceControl.SynchronizeState</a></li>
          <li>[CIC] Added the item3 field to the <a href="/CIC/References/ContentTemplates/Text.html">Text</a> template</li>
          <li>[CIC] Added a source field in the <a href="/CIC/References/CICInterface/AudioPlayer.html#Play">AudioPlayer.Play</a> directive message</li>
          <li>[CIC] Added the durationInMilliseconds field in <a href="/CIC/References/CICInterface/AudioPlayer.html#AudioStreamInfoObject">AudioStreamInfoObject</a> </li>
          <li>[CIC] Added the Notifier namespace. Added <a href="/CIC/References/CICInterface/Notifier.html#ClearIndicator">ClearIndicator</a> and <a href="/CIC/References/CICInterface/Notifier.html#SetIndicator">SetIndicator</a> directive messages</li>
          <li>[CIC] Added the <a href="/CIC/References/ContentTemplates/Atmosphere.html">Atmosphere</a> template</li>
          <li>[CIC] Added a guide text on prohibited use for the bgClipURL field of weather templates due to license issues</li>
        </ul>
      </td>
    </tr>
    <tr>
      <td>v1.3</td><td>2017-09-11</td>
      <td>
        <ul>
          <li>[CIC] Added the explicit field to the <a href="/CIC/References/CICInterface/SpeechRecognizer.html#ExpectSpeech">SpeechRecognizer.ExpectSpeech</a> directive message</li>
          <li>[CIC] Added a <a href="/CIC/References/ContentTemplates/Common_Fields.md">common fields</a> specification to the <a href="/CIC/References/Content_Templates.md">Content</a> template</li>
        </ul>
      </td>
    </tr>
    <tr>
      <td>v1.2</td><td>2017-09-04</td>
      <td>
        <ul>
          <li>[CIC] Added the <a href="/CIC/References/CICInterface/Clova.html#Help">Clova.Help</a> directive message</li>
          <li>[CIC] Added the <a href="/CIC/References/CICInterface/DeviceControl.html#LaunchApp">DeviceControl.LaunchApp</a> directive message</li>
          <li>[CIC] Added the TextRecognizer namespace and <a href="/CIC/References/CICInterface/TextRecognizer.html">TextRecognizer.Recognize</a> event message</li>
          <li>[CIC] Rewrote the table of contents and descriptions of the <a href="/CIC/References/CIC_API.html">CIC API</a> and <a href="/CEK/References/CEK_API.html">CEK API</a></li>
          <li>[CIC] Updated content on CIC API: Added status codes for the request and response header, and applied the format of the REST API reference to the document</li>
          <li>[Other] Emended errors in the document</li>
        </ul>
      </td>
    </tr>
    <tr>
      <td>v1.1</td><td>2017-08-28</td>
      <td>
        <ul>
          <li>[CIC] Added the set-top box specification on TV channels and specifications for the power state to <a href="/CIC/References/Context_Objects.html#DeviceState">Device.DeviceState</a> and <a href="/CIC/References/CICInterface/DeviceControl.html">DeviceControl API</a></li>
          <li>[CIC] Added and changed some target values in the <a href="/CIC/References/CICInterface/DeviceControl.html">DeviceControl API</a>: power, energysave, screenbrightness</li>
          <li>[CIC] Changed the name SetPoint of the <a href="/CIC/References/CICInterface/DeviceControl.html">DeviceControl API</a> to <a href="/CIC/References/CICInterface/DeviceControl.html#SetValue">SetValue</a></li>
          <li>[CIC] Updated <a href="/CIC/References/Clova_Auth_API.html">the Clova auth API</a>: Added request and response headers, and status codes. Applied the format of the REST API reference to the document</li>
          <li>[CEK] Added <a href="/CEK/References/ClovaHomeInterface/Error_Interfaces.html#ValueOutOfRangeError">the ValueOutOfRangeError </a> to the error interface of the Clova Home</li>
        </ul>
      </td>
    </tr>
    <tr>
      <td>v1.0</td><td>2017-08-21</td>
      <td>[CIC] Added the section on <a href="/CIC/Guides/Interact_with_CIC.html#ManageConnection">Renewing a Clova access token</a> and updated content on token APIs</td>
    </tr>
    <tr>
      <td>v0.9</td><td>2017-08-14</td>
      <td>
        <ul>
          <li>[CIC] Added description on <a href="/CIC/CIC_Overview.html#DialogModel">dialog model</a> </li>
          <li>[CIC] Added <a href="/CIC/References/CICInterface/DeviceControl.html">DeviceControl</a> API</li>
          <li>[CIC] Added payload fields in <a href="/CIC/References/Context_Objects.html">Device.DeviceState</a>: airplane, battery, bluetooth, brightness, flashLight, gps, powerSavingMode, soundMode, volume, and wifi</li>
          <li>[CEK] Added the section on <a href="/CEK/Guides/Build_Custom_Extension.html#DoMultiturnDialog">Engaging in multi-turn dialogs</a> and updated the description on the sessionAttributes field</li>
        </ul>
      </td>
    </tr>
    <tr>
      <td>v0.8</td><td>2017-08-04</td>
      <td>
        <ul>
          <li>[CIC] Added the <a href="/CIC/References/CICInterface/Clova.html#Hello">Clova.Hello</a> directive message</li>
          <li>[CIC] Added the type field to the AudioItem object of the <a href="/CIC/References/CICInterface/AudioPlayer.html#Play">AudioPlayer.Play</a> directive message</li>
          <li>[CIC] Added the urlPlayable field to the <a href="/CIC/References/CICInterface/AudioPlayer.html#AudioStreamInfoObject">AudioStreamInfoObject</a></li>
          <li>[CIC] Added specification on <a href="/CIC/References/CIC_API.html#Error">CIC error messages</a></li>
          <li>[CIC] Rewrote the contents of <a href="/CIC/References/CIC_API.html#MultipartMessage">multipart message</a></li>
          <li>[CEK] Added new Clova Home <a href="/CEK/References/ClovaHomeInterface/Shared_Objects.html#ApplianceInfoObject">supported appliances</a>: air purifier, humidifier, set-top box, and heater</li>
          <li>[CEK] Removed an existing Clova Home <a href="/CEK/References/ClovaHomeInterface/Shared_Objects.html#ApplianceInfoObject">supported appliance</a>: door lock</li>
        </ul>
      </td>
    </tr>
    <tr>
      <td>v0.7</td><td>2017-07-28</td>
      <td>
        <ul>
          <li>[CIC] Removed PlayNext and Stop from <a href="/CIC/References/CICInterface/AudioPlayer.html">AudioPlayer</a> (merged into <a href="/CIC/References/CICInterface/PlaybackController.html">PlaybackController</a>)</li>
          <li>[CIC] Changed the message names of <a href="/CIC/References/CICInterface/PlaybackController.html">PlaybackController</a> (Mute, Next, Pause, Previous, Resume, Stop, Unmute, VolumeDown, and VolumeUp</li>
          <li>[CIC] Added find-route templates: CarRoute and TransportationRoute</li>
          <li>[CIC] Added weather templates: <a href="/CIC/References/ContentTemplates/Humidity.html">Humidity</a>, <a href="/CIC/References/ContentTemplates/TodayWeather.html">TodayWeather</a>, <a href="/CIC/References/ContentTemplates/TomorrowWeather.html">TomorrowWeather</a>, <a href="/CIC/References/ContentTemplates/WeeklyWeather.html">WeeklyWeather</a>, and <a href="/CIC/References/ContentTemplates/WindSpeed.html">WindSpeed</a></li>
        </ul>
      </td>
    </tr>
    <tr>
      <td>v0.6</td><td>2017-07-14</td>
      <td>[CIC] Added  beginAtInMilliseconds field contents to <a href="/CIC/References/CICInterface/AudioPlayer.html#AudioStreamInfoObject">AudioStreamInfoObject</a></td>
    </tr>
    <tr>
      <td>v0.5</td><td>2017-07-07</td>
      <td>
        <ul>
          <li>[CEK] Updated the <a href="/CEK/References/CEK_API.html#CustomExtResponseMessage">outputSpeech</a> object configuration in the <a href="/CEK/References/CEK_API.html#CustomExtResponseMessage">response message of custom extensions</a></li>
          <li>[Common] Added the <a href="/Glossary.html">Glossary</a></li>
          <li>Updated the table of contents for the section on CEK message formats</li>
        </ul>
      </td>
    </tr>
    <tr>
      <td>v0.4</td><td>2017-07-03</td>
      <td>
        <ul>
          <li>[CEK] Updated images in the CEK document</li>
          <li>[Common] Applied changes according to the document review results</li>
        </ul>
      </td>
    </tr>
    <tr>
      <td>v0.3</td><td>2017-06-19</td>
      <td>
        <ul>
          <li>[CEK] Completed the first draft of the CEK document</li>
          <li>[CIC] Updated <a href="/CIC/Guides/Interact_with_CIC.html#ManageConnection">Managing connections</a> (if HTTP PING frame is not available)</li>
        </ul>
      </td>
    </tr>
    <tr>
      <td>v0.2</td><td>2017-06-08</td>
      <td>[CIC] Added the section on <a href="/CIC/Guides/Interact_with_CIC.md#ManageConnection">Managing connections</a> (HTTP PING) to <a href="/CIC/Guides/Interact_with_CIC.html">Interacting with CIC</a></td>
    </tr>
    <tr>
      <td>v0.1</td><td>2017-05-29</td>
      <td>[CIC] Completed the first draft of the CIC document</td>
    </tr>
  </tbody>
</table>
