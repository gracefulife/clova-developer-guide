# 시작하기 전에

<a target="_blank" href="http://clova.ai">Clova</a>는 NAVER가 개발 및 서비스하고 있는 인공지능 플랫폼입니다. Clova 사용자의 음성이나 이미지를 인식하고 이를 분석하여 사용자가 원하는 정보나 서비스를 제공합니다. Clova 플랫폼을 이용하는 3rd party 개발자는 다음과 같이 두 그룹으로 나뉠 수 있습니다.

* [CIC 플랫폼](/CIC/CIC_Overview.md#WhatisCIC) 사용자: Clova 인공 지능 서비스를 제공하는 전자 기기, 앱을 개발하려는 클라이언트 개발자
* [CEK 플랫폼](/CEK/CEK_Overview.md#WhatisCEK) 사용자: Clova를 통해 보유하고 있는 온라인 콘텐츠나 서비스를 제공하려는 확장 기능(Extension) 개발자

<div class="note">
  <p><strong>Note!</strong></p>
  <p>클라이언트나 금전 거래나 결제를 포함하는 extension 또는 IoT 서비스를 제공하는 extension을 개발하려는 회사나 개인은 사전에 <a target="_blank" href="https://www.navercorp.com/ko/company/proposalRegister.nhn">NAVER 제휴 제안</a> 페이지를 방문하여 미리 제휴를 맺어야 합니다.</p>
</div>

클라이언트 개발자와 extension 개발자를 위해 Clova 플랫폼은 Clova Interface Connection(CIC), Clova Extension Kit(CEK) 그리고 Clova developer console을 제공하고 있습니다. 개발자는 필요에 따라 다음과 같은 문서를 참조하면 됩니다.

<table>
  <thead>
    <tr>
      <th width="12%">구분</th>
      <th width="44%">클라이언트 개발자</th>
      <th width="44%">Extension 개발자</th>
    </tr>
  </thead>
<<<<<<< HEAD
  <tbody style="vertical-align: top;">
=======
  <tbody>
  <tr>
    <td>v4.1</td><td>2018-05-07</td>
    <td>
      <ul>
        <li>[CIC] <a href="/CIC/References/CICInterface/DeviceControl.html">DeviceControl</a> 네임스페이스에 <a href="/CIC/References/CICInterface/DeviceControl.html#LaunchURI">LaunchURI</a> 지시 메시지 추가</li>
        <li>[CIC] <a href="/CIC/References/CICInterface/DeviceControl.html">DeviceControl</a> 네임스페이스의 <a href="/CIC/References/CICInterface/DeviceControl.html#LaunchApp">LaunchApp</a> 지시 메시지와 <a href="/CIC/References/CICInterface/DeviceControl.html#OpenScreen">OpenScreen</a> 지시 메시지의 지원을 중지(Deprecated)</li>
      </ul>
    </td>
  </tr>
  <tr>
    <td>v4.0</td><td>2018-04-30</td>
    <td>
      <ul>
        <li>[CEK] Clova Home extension API에 <a href="/CEK/References/ClovaHomeInterface/Control_Interfaces.html#GetOpenStateRequest">GetOpenStateRequest</a>, <a href="/CEK/References/ClovaHomeInterface/Control_Interfaces.html#GetOpenStateResponse">GetOpenStateResponse</a> 추가</li>
      </ul>
    </td>
  </tr>
  <tr>
    <td>v3.9</td><td>2018-04-23</td>
    <td>
      <ul>
        <li>[CEK] Clova Home extension API에 <a href="/CEK/References/ClovaHomeInterface/Control_Interfaces.html#ReleaseModeConfirmation">ReleaseModeConfirmation</a>, <a href="/CEK/References/ClovaHomeInterface/Control_Interfaces.html#ReleaseModeRequest">ReleaseModeRequest</a> 추가</li>
      </ul>
    </td>
  </tr>
  <tr>
    <td>v3.8</td><td>2018-04-16</td>
    <td>
      <ul>
        <li>[CIC] <a href="/CIC/References/CICInterface/SpeechRecognizer.html#Recognize">SpeechRecognizer.Recognize</a> 이벤트 메시지의 wakeWord 필드 설명 및 Audio data 설명 업데이트</li>
        <li>[CIC] <a href="/CIC/References/CICInterface/DeviceControl.html">DeviceControl</a> 네임스페이스에 <a href="/CIC/References/CICInterface/DeviceControl.html#Open">Open</a> 지시 메시지 추가</li>
        <li>[CEK] Clova Home extension API <a href="/CEK/References/ClovaHomeInterface/Control_Interfaces.html#GetLockStateResponse">GetLockStateResponse</a>에 openState 필드 추가</li>
        <li>[CEK] Clova Home extension API에 <a href="/CEK/References/ClovaHomeInterface/Control_Interfaces.html#GetCleaningCycleRequest">GetCleaningCycleRequest</a>, <a href="/CEK/References/ClovaHomeInterface/Control_Interfaces.html#GetCleaningCycleResponse">GetCleaningCycleResponse</a> 추가</li>
      </ul>
    </td>
  </tr>
  <tr>
    <td>v3.7</td><td>2018-04-09</td>
    <td>
      <ul>
        <li>[CIC] 클라이언트 기기 디자인 가이드라인에서 <a href="Design/Design_Guideline_For_Client_Hardware.html#BootingScreen">부팅 화면</a> 관련 설명 및 예제 이미지를 업데이트</li>
        <li>[CEK] Clova Home extension API <a href="/CEK/References/ClovaHomeInterface/Shared_Objects.html#ColorInfoObject">ColorInfoObject</a>의 brightness 필드의 설명 및 필수/포함 여부 변경</li>
      </ul>
    </td>
  </tr>
    <tr>
      <td>v3.6</td><td>2018-04-02</td>
      <td>
        <ul>
          <li>[CIC] <a href="/CIC/References/CICInterface/AudioPlayer.html">AudioPlayer</a> 네임스페이스에 메시지 스펙 추가 및 일부 필드 업데이트
            <ul>
              <li><a href="/CIC/References/CICInterface/AudioPlayer.html#ExpectReportPlaybackState">AudioPlayer.ExpectReportPlaybackState</a> 지시 메시지, <a href="/CIC/References/CICInterface/AudioPlayer.html#ReportPlaybackState">AudioPlayer.ReportPlaybackState 이벤트 메시지</a>{% if book.TargetReaderType == "Internal" %}, <a href="/CIC/References/CICInterface/AudioPlayer.html#RequestPlaybackState">AudioPlayer.RequestPlaybackState</a> 이벤트 메시지, <a href="/CIC/References/CICInterface/AudioPlayer.html#SynchronizePlaybackState">SynchronizePlaybackState 지시 메시지</a>{% endif %} 추가</li>
              <li><a href="/CIC/References/CICInterface/AudioPlayer.html#Play">AudioPlayer.Play</a> 지시 메시지의 payload 필드 내용 업데이트</li>
              <li>ProgressReportXXX, PlayXXX 형식의 이름을 가진 이벤트 필드에 token 필드 값 필수로 추가</li>
            </ul>
          </li>
          <li>[CIC] <a href="/CIC/References/Context_Objects.html#PlaybackState">AudioPlayer.PlaybackState</a> 맥락 객체에 repeatMode 추가</li>
          <li>[CIC] <a href="/CIC/References/CICInterface/PlaybackController.html">PlaybackController</a> 네임스페이스에 총 12건의 메시지 스펙 추가
            <ul>
              <li><a href="/CIC/References/CICInterface/PlaybackController.html#PauseCommandIssued">PlaybackController.PauseCommandIssued</a>, <a href="/CIC/References/CICInterface/PlaybackController.html#PlayCommandIssued">PlaybackController.PlayCommandIssued</a>, <a href="/CIC/References/CICInterface/PlaybackController.html#ResumeCommandIssued">PlaybackController.ResumeCommandIssued</a>, <a href="/CIC/References/CICInterface/PlaybackController.html#SetRepeatModeCommandIssued">PlaybackController.SetRepeatModeCommandIssued</a>, <a href="/CIC/References/CICInterface/PlaybackController.html#StopCommandIssued">PlaybackController.StopCommandIssued</a> 이벤트 메시지 추가</li>
              <li><a href="/CIC/References/CICInterface/PlaybackController.html#ExpectNextCommand">PlaybackController.ExpectNextCommand</a>, <a href="/CIC/References/CICInterface/PlaybackController.html#ExpectPauseCommand">PlaybackController.ExpectPauseCommand</a>, <a href="/CIC/References/CICInterface/PlaybackController.html#ExpectPlayCommand">PlaybackController.ExpectPlayCommand</a>, <a href="/CIC/References/CICInterface/PlaybackController.html#ExpectPreviousCommand">PlaybackController.ExpectPreviousCommand</a>,
<a href="/CIC/References/CICInterface/PlaybackController.html#ExpectResumeCommand">PlaybackController.ExpectResumeCommand</a>, <a href="/CIC/References/CICInterface/PlaybackController.html#ExpectStopCommand">PlaybackController.ExpectStopCommand</a>, <a href="/CIC/References/CICInterface/PlaybackController.html#SetRepeatMode">PlaybackController.SetRepeatMode</a> 지시 메시지 추가</li>
              <li><a href="/CIC/References/CICInterface/PlaybackController.html#TurnOnRepeatMode">PlaybackController.TurnOnRepeatMode</a> 지시 메시지와 <a href="/CIC/References/CICInterface/PlaybackController.html#TurnOffRepeatMode">PlaybackController.TurnOffRepeatMode</a>는 사라질 예정</li>
            </ul>
          </li>
          <li>[CIC] 미디어 스트림을 위한 정보와 재생 목록을 표시하기 위한 재생 메타 정보를 분리하기 위해 <a href="/CIC/References/CICInterface/TemplateRuntime.html">TemplateRuntime</a> 네임스페이스 추가</li>
          <li>[CIC] <a href="/CIC/References/Context_Objects.html#DeviceState">Device.DeviceState</a>의 <a href="/CIC/References/Context_Objects.html#BluetoothInfoObject">BluetoothInfoObject</a>에 scanlist 필드 추가</li>
          <li>[CIC] PIN 코드를 사용하는 외부 블루투스 기기와 연결할 수 있도록 <a href="/CIC/References/CICInterface/DeviceControl.html">DeviceControl</a> 네임 스페이스에 <a href="/CIC/References/CICInterface/DeviceControl.html#BtConnectByPINCode">BtConnectByPINCode</a> 지시 메시지와 <a href="/CIC/References/CICInterface/DeviceControl.html#BtRequestForPINCode">BtRequestForPINCode</a>, <a href="/CIC/References/CICInterface/DeviceControl.html#BtRequestToCancelPinCodeInput">BtRequestToCancelPinCodeInput</a> 이벤트 메시지 추가</li>
          <li>[CIC] <a href="/CIC/References/CICInterface/DeviceControl.html">DeviceControl</a> 네임 스페이스의 <a href="/CIC/References/CICInterface/DeviceControl.html#BtConnect">BtConnect</a> 지시 메시지에 payload 추가</li>
          <li>[CEK] Clova Home extension API에 GetSleepStartTimeRequest 외 9건의 <a href="/CEK/References/ClovaHomeInterface/Control_Interfaces.html">Control API</a>와 4건의 <a href="/CEK/References/ClovaHomeInterface/Shared_Objects.html">공유 객체</a> 추가</li>
          <li>[CEK] Clova Home extension API의 <a href="/CEK/References/ClovaHomeInterface/Discovery_Interfaces.html#DiscoverAppliancesResponse">DiscoverAppliancesResponse</a>에 <a href="/CEK/References/ClovaHomeInterface/Shared_Objects.html#CustomCommandInfoObject">CustomCommandInfoObject</a> 추가</li>
          <li>[CEK] Clova Home extension API에서 TimeAmountInfoObject <a href="/CEK/References/ClovaHomeInterface/Shared_Objects.html">공유 객체</a> 제거 및 이에 따른 <a href="/CEK/References/ClovaHomeInterface/Control_Interfaces.html">Control API</a>의 일부 내용 변경</li>
          <li>[CEK] Clova Home extension API의 <a href="/CEK/References/ClovaHomeInterface/Shared_Objects.html#ApplianceInfoObject">ApplianceInfoObject</a>에 tags 필드 추가 및 location 필드 설명 변경</li>
          <li>[Dev. Console] Clova developer console의 일부 UI 업데이트 적용</li>
        </ul>
      </td>
    </tr>
    <tr>
      <td>v3.5</td><td>2018-03-19</td>
      <td>
        <ul>
          <li>[CIC] <a href="/CIC/References/Context_Objects.html#DeviceState">Device.DeviceState</a>에 <a href="/CIC/References/Context_Objects.html#SoundOutputInfoObject">SoundOutputInfoObject</a> 추가</li>
          <li>[CIC] 사용자가 설정한 임의의 명령을 실행할 수 있는 <a href="/CIC/References/CICInterface/PlaybackController.html#CustomCommandIssued">CustomCommandIssued</a> 이벤트 메시지를 <a href="/CIC/References/CICInterface/PlaybackController.html#CustomCommandIssued">PlaybackController</a> 네임스페이스에 추가</li>
          <li>[CEK] Clova Home API에 CloseConfirmation 외 47건의 <a href="/CEK/References/ClovaHomeInterface/Control_Interfaces.html">Control API</a>와 약 10종의 <a href="/CEK/References/ClovaHomeInterface/Shared_Objects.html">공유 객체</a> 추가</li>
          <li>[CEK] Clova Home API <a href="/CEK/References/ClovaHomeInterface/Shared_Objects.html#ApplianceInfoObject">지원 기기</a> 30종 추가</li>
        </ul>
      </td>
    </tr>
    <tr>
      <td>v3.4</td><td>2018-03-05</td>
      <td>
        <ul>
          <li>[CIC] <a  href="/CIC/References/CICInterface/SpeechRecognizer.html#Recognize">SpeechRecognizer.Recognize</a> 이벤트 메시지 initiator 필드의 설명을 수정</li>
          <li>[CIC] <a href="/Design/Design_Guideline_For_Client_Hardware.html">클라이언트 기기 디자인 가이드라인</a>에서 클라이언트 상태 중 Hearing 상태의 이름을 Listening으로 수정</li>
          <li>[CIC] 클라이언트 기기 디자인 가이드라인의 <a href="/Design/Design_Guideline_For_Client_Hardware.html#Audio">소리</a>에서 오디오 콘텐츠 타입으로 Feedback 타입을 추가하고 설명에 관련 규칙을 추가</li>
          <li>[CEK] <a href="/CEK/Tutorials/Introduction.html">튜토리얼</a> 페이지에 <a href="/CEK/Tutorials/Use_Builtin_Type_Slots.html">사용자가 입력한 정보 활용하기</a> 페이지 추가</li>
        </ul>
      </td>
    </tr>
    <tr>
      <td>v3.3</td><td>2018-02-26</td>
      <td>
        <ul>
          <li>[CIC] <a href="/CIC/References/CICInterface/SpeechRecognizer.html#Recognize">SpeechRecognizer.Recognize</a> 이벤트 메시지 initiator 필드에 deviceUUID 필드를 추가</li>
          <li>[CIC] 알람 동기화와 관련된 <a href="/CIC/References/CICInterface/Alerts.html#RequestSynchronizeAlert">RequestSynchronizeAlert</a> 이벤트 메시지와 <a href="/CIC/References/CICInterface/Alerts.html#SynchronizeAlert">SynchronizeAlert</a> 지시 메시지를 <a href="/CIC/References/CICInterface/Alerts.html">Alerts</a> 네임스페이스에 추가</li>
          <li>[CIC] System 네임스페이스에서 알람 동기화와 관련된 일부 필드를 제거할 예정</li>
        </ul>
      </td>
    </tr>
    <tr>
      <td>v3.2</td><td>2018-02-19</td>
      <td>
        <ul>
          <li>[CIC] 사용자의 호출을 정확히 판단하기 위해 <a href="/CIC/References/CICInterface/SpeechRecognizer.html#Recognize">SpeechRecognizer.Recognize</a> 이벤트 메시지에 initiator 필드를 추가</li>
          <li>[CIC] 리마인더 및 동작 예약의 내용을 확인하기 위해 <a href="/CIC/References/CICInterface/Alerts.html#SetAlert">Alerts.SetAlert</a> 지시 메시지에 label 필드를 추가</li>
          <li>[CIC] 리마인더 및 동작 예약의 내용을 표시하기 위해 <a href="/CIC/References/ContentTemplates/ActionTimer.html">ActionTimer</a>, <a href="/CIC/References/ContentTemplates/ActionTimerList.html">ActionTimerList</a>, <a href="/CIC/References/ContentTemplates/Reminder.html">Reminder</a>, <a href="/CIC/References/ContentTemplates/ReminderList.html">ReminderList</a> 템플릿에 label 필드를 추가</li>
        </ul>
      </td>
    </tr>
    <tr>
      <td>v3.1</td><td>2018-02-05</td>
      <td>
        <ul>
          <li>[CIC] <a href="/CIC/References/CICInterface/AudioPlayer.html#AudioStreamInfoObject">AudioStreamInfoObject</a>의 durationInMilliseconds 필드에 대한 설명 수정</li>
          <li>[CIC] <a href="/CIC/References/ContentTemplates/Atmosphere.html">Atmosphere</a>, <a href="/CIC/References/ContentTemplates/CardList.html">CardList</a>, <a href="/CIC/References/ContentTemplates/Humidity.html">Humidity</a>, <a href="/CIC/References/ContentTemplates/TodayWeather.html">TodayWeather</a>, <a href="CIC/References/ContentTemplates/TomorrowWeather.html">TomorrowWeather</a>, <a href="/CIC/References/ContentTemplates/WeeklyWeather.html">WeeklyWeather</a>, <a href="CIC/References/ContentTemplates/WindSpeed.html">WindSpeed</a> 템플릿에 출처 관련 필드 등 내용 추가</li>
          <li>[CEK] Extension 시작 호출(<a href="CEK/Guides/Build_Custom_Extension.html#HandleLaunchRequest">LaunchRequest</a>)에 대한 설명 수정 및 <a href="/Design/Design_Guideline_For_Extension.html">Extension 디자인 가이드라인 문서 반영</a></li>
          <li>[CEK] CEK와 extension간 통신에 사용되는 <a href="/CEK/CEK_Overview.html#WhatisCEK">HTTP 프로토콜 버전</a> 명시</li>
          <li>[CEK] <a href="/CEK/Tutorials/Introduction.html">튜토리얼</a> 페이지에 <a href="/CEK/Tutorials/Handle_Builtin_Intents.html">기본적인 의사 표현 처리하기</a> 페이지 추가</li>
          <li>[Dev. Console] Extension 서버에서 사용해야 할 <a href="/DevConsole/Guides/CEK/Register_Extension.html#SetServerConnection">포트</a>를 명시</li>
          <li>[Common] 일부 문서 오류 교정</li>
        </ul>
      </td>
    </tr>
    <tr>
      <td>v3.0</td><td>2018-01-29</td>
      <td>
        <ul>
          <li>[Design] <a href="/Design/Design_Guideline_For_Client_Hardware.html">클라이언트 기기 디자인 가이드라인</a>에 <a href="/Design/Design_Guideline_For_Client_Hardware.html#SoundEffect">Reminder용 효과음</a> 추가</li>
          <li>[CIC] <a href="/CIC/References/CICInterface/Notifier.html">Notifier</a> 네임스페이스에 <a href="/CIC/References/CICInterface/Notifier.html#Notify">Notifier.Notify</a> 이벤트 메시지 추가 및 해당 네임스페이스 메시지의 payload 필드 업데이트</li>
          <li>[CIC] <a href="/CIC/References/ContextObjects/SpeechState.html">SpeechSynthesizer.SpeechState</a> 및 <a href="/CIC/References/CICInterface/SpeechSynthesizer.html">SpeechSynthesizer</a> 네임스페이스에 <a href="/CIC/References/CICInterface/SpeechSynthesizer.html#SpeechFinished">SpeechFinished</a>, <a href="/CIC/References/CICInterface/SpeechSynthesizer.html#SpeechStarted">SpeechStarted</a>, <a href="/CIC/References/CICInterface/SpeechSynthesizer.html#SpeechStopped">SpeechStopped</a> 이벤트 메시지 추가</li>
          <li>[CIC] Multi-turn 대화를 위해 <a href="/CIC/References/CICInterface/TextRecognizer.html">TextRecognizer.Recognize</a> 이벤트 메시지에 speechId, explicit 필드 추가</li>
          <li>[CEK] Clova Home extension 메시지 레퍼런스 중 <a href="/CEK/References/ClovaHomeInterface/Error_Interfaces.html">Error 인터페이스</a>에 <a href="/CEK/References/ClovaHomeInterface/Error_Interfaces.html#NoSuchTargetError">NoSuchTargetError</a>, <a href="/CEK/References/ClovaHomeInterface/Error_Interfaces.html#NotSupportedInCurrentModeError">NotSupportedInCurrentModeError</a>, <a href="/CEK/References/ClovaHomeInterface/Error_Interfaces.html#UnsupportedOperationError">UnsupportedOperationError</a> 그리고 <a href="/CEK/References/ClovaHomeInterface/Error_Interfaces.html#ValueOutOfRangeError">ValueOutOfRangeError</a> 추가</li>
          <li>[Dev. Console] <a href="/DevConsole/Guides/CEK/Register_Extension.html#SetServerConnection">Extension 서버 연동 설정</a> 전 연결 확인하는 방법 추가 및 <a href="/DevConsole/Guides/CEK/Test_Extension.html#TestOnClovaApp">테스터 ID 적용 자동화</a>에 대한 안내 추가</li>
          <li>[Dev. Console] Clova developer console의 일부 UI 업데이트 적용</li>
        </ul>
      </td>
    </tr>
    <tr>
      <td>v2.9</td><td>2018-01-22</td>
      <td>
        <ul>
          <li>[Design] 플랫폼 지원 오디오 압축 포맷 내용을 <a href="/Design/Design_Guideline_For_Client_Hardware.html#SupportedAudioCompressionFormat">클라이언트 기기 디자인 가이드라인</a>과 <a href="/Design/Design_Guideline_For_Extension.html#SupportedAudioCompressionFormat">extension 디자인 가이드라인</a>에 각각 추가</li>
          <li>[CEK] <a href="/CEK/Tutorials/Introduction.html">튜토리얼</a> 페이지와 <a href="/CEK/Tutorials/Build_Simple_Extension.html">기초적인 extension 만들기</a> 페이지 추가</li>
          <li>[Dev. Console] <a href="/DevConsole/Guides/CEK/Register_Interaction_Model.html#AddCustomSlotType">Built-in intent 목록 표시</a>, <a href="/DevConsole/Guides/CEK/Deploy_Extension.html#InputComplianceInfo">심사 신청</a> 시 심사 요청 메시지 작성을 위한 UI 추가</li>
          <li>[Common] UML 다이어그램의 이미지 포맷 변경</li>
        </ul>
      </td>
    </tr>
    <tr>
      <td>v2.8</td><td>2018-01-15</td>
      <td>
        <ul>
          <li>[Design] <a href="/Design/Design_Guideline_For_Client_Hardware.html">클라이언트 기기 디자인 가이드라인</a>에 알람, 리마인더, 타이머에 대한 조명 효과 및 효과음 가이드라인 설명 추가 </li>
        </ul>
      </td>
    </tr>
    <tr>
      <td>v2.7</td><td>2018-01-08</td>
      <td>
        <ul>
          <li>[Design] 플랫폼 구현 상황에 맞게 <a href="/Design/Design_Guideline_For_Extension.html#DefineInteractionModel">built-in intent</a>에 대한 설명 수정</li>
          <li>[CIC] <a href="/CIC/Guides/Interact_with_CIC.html#HandleDelegation">위임된 사용자 요청 처리하기</a> 절 추가 및 <a href="/CIC/References/CICInterface/Clova.html#HandleDelegatedEvent">Clova.HandleDelegatedEvent</a> 지시 메시지와 <a href="/CIC/References/CICInterface/Clova.html#ProcessDelegatedEvent">Clova.ProcessDelegatedEvent</a> 이벤트 메시지 추가</li>
          <li>[CIC] <a href="/CIC/References/CICInterface/PlaybackController.html#NextCommandIssued">PlaybackController.NextCommandIssued</a>와 <a href="/CIC/References/CICInterface/PlaybackController.html#PreviousCommandIssued">PlaybackController.PreviousCommandIssued</a> 이벤트 메시지에 <a href="/CIC/References/Context_Objects.html#PlaybackState">AudioPlayer.PlaybackState</a> 맥락 정보를 포함하도록 설명 추가</li>
          <li>[CIC] <a href="/CIC/References/CICInterface/Alerts.html">Alerts</a> API의 <a href="/CIC/References/CICInterface/Alerts.html#AlertsWorkFlow">동작 구조</a>에 대한 설명 개선</li>
          <li>[CIC] <a href="/CIC/References/CICInterface/DeviceControl.html">DeviceControl</a> API의 <a href="/CIC/References/CICInterface/DeviceControl.html#DeviceContorlWorkFlow">동작 구조</a>에 대한 설명 추가</li>
          <li>[CIC] 일부 content template 및 공유 객체에 대한 오류 교정 내용 수정</li>
          <li>[CEK] <a href="/CEK/Examples/Extension_Examples.html">Extension 예제</a> 페이지 추가</li>
          <li>[Dev. Console] <strong>테스터 ID</strong> 필드 추가에 따른 <a href="/DevConsole/Guides/CEK/Test_Extension.html">Extension 테스트하기</a> 설명 업데이트</li>
        </ul>
      </td>
    </tr>
    <tr>
      <td>v2.6</td><td>2018-01-02</td>
      <td>
        <ul>
          <li>[CIC] <a href="/CIC/References/CIC_API.html#EstablishDownchannel">Downchannel 구성</a>절 내용에 429 오류 코드 및 관련 설명 Remarks 항목에 추가</li>
          <li>[CIC] 길찾기 템플릿(CarRoute, TransportationRoute) 제거, 길찾기에 대한 UI 표현이 ImageText 템플릿으로 대체됨.</li>
          <li>[Common] 일부 문서 오류, 오타 수정</li>
        </ul>
      </td>
    </tr>
    <tr>
      <td>v2.5</td><td>2017-12-18</td>
      <td>
        <ul>
          <li>[Design] <a href="/DevConsole/Guides/CEK/Register_Interaction_Model.html">Interaction 모델 등록하기</a>에서 <a href="/Design/Design_Guideline_For_Extension.html#DefineInteractionModel">interaction 모델 정의</a> 절 내용을 <a href="/Design/Design_Guideline_For_Extension.html">Extension 디자인 가이드라인</a> 문서로 이동</li>
          <li>[Design] <a href="/Design/Design_Guideline_For_Extension.html#DefineInteractionModel">Interaction 모델 정의</a> 절 내용에 <a href="/Design/Design_Guideline_For_Extension.html#UtteranceExample">발화 예시</a>문 작성 가이드라인 추가</li>
          <li>[CIC] <a href="/CIC/References/CICInterface/SpeechRecognizer.html">SpeechRecognizer</a> 인터페이스에서 ExpectSpeechTimedOut 이벤트 메시지 제거</li>
          <li>[CIC] <a href="/CIC/References/Context_Objects.html">맥락 정보(context)</a>에서 Clova.FreetalkState 개체 제거</li>
          <li>[Dev. console] <a href="/DevConsole/Guides/CEK/Test_Extension.html">Extension 테스트하기</a>에 테스트 모드 사용하기 추가</li>
          <li>[Dev. console] UI 개선에 따른 이미지 및 설명 수정</li>
          <li>[Dev. console] <a href="/DevConsole/Guides/CEK/Update_Extension.html">Extension 업데이트하기</a>, <a href="/DevConsole/Guides/CEK/Remove_Extension.html">Extension 중지 및 삭제하기</a> 추가</li>
        </ul>
      </td>
    </tr>
    <tr>
      <td>v2.4</td><td>2017-12-11</td>
      <td>
        <ul>
          <li>[Design] <a href="/Design/Design_Guideline_For_Extension.html">Extension 디자인 가이드라인</a> 추가</li>
          <li>[CIC] <a href="/CIC/References/CICInterface/AudioPlayer.html">AudioPlayer</a> 인터페이스에 <a href="/CIC/References/CICInterface/AudioPlayer.html#ClearQueue">ClearQueue</a> 지시 메시지 추가</li>
        </ul>
      </td>
    </tr>
    <tr>
      <td>v2.3</td><td>2017-12-04</td>
      <td>
        <ul>
          <li>[Design] <a href="/Design/Design_Guideline_For_Client_Hardware.html#AudioInterruptionRule">오디오 재생 규칙(audio interruption rule)</a>을 <a href="/Design/Design_Guideline_For_Client_Hardware.html">클라이언트 기기 디자인 가이드라인</a>에 추가</li>
          <li>[Design] <a href="/Design/Design_Guideline_For_Client_Hardware.html">클라이언트 기기 디자인 가이드라인</a>의 이미지 개선</li>
          <li>[CIC] CIC 연동하기의 사전 준비사항에 <a href="/CIC/Guides/Interact_with_CIC.html#UserAgentString">User-Agent string</a>을 추가</li>
          <li>[CIC] <a href="/CIC/References/CIC_API.html">CIC API 레퍼런스</a>의 <a href="/CIC/References/CIC_API.html#SendEvent">이벤트 메시지 전송</a> 절에 412 Precondition Failed 상태 코드 설명 추가</li>
          <li>[CEK] 사용자 multi-turn 대화를 위해 reprompt 필드를 <a href="/CEK/References/CEK_API.html#CustomExtResponseMessage">응답 메시지</a>에 추가</li>
          <li>[CEK] 일부 문서 오류 수정</li>
        </ul>
      </td>
    </tr>
    <tr>
      <td>v2.2</td><td>2017-11-20</td>
      <td>
        <ul>
          <li>[Design] <a href="/Design/Design_Guideline_For_Client_Hardware.html">클라이언트 기기 디자인 가이드라인</a> 추가</li>
          <li>[CIC] 오디오 콘텐츠 및 이미지 썸네일 표시를 위해 <a href="/CIC/References/ContentTemplates/CardList.html">CardList 템플릿</a>의 subType 값에 Type5, Type6를 추가</li>
          <li>[CEK] Clova Home extension 메시지의 <a href="/CEK/References/ClovaHomeInterface/Shared_Objects.html">공유 객체</a> HeatingModeInfoObject를 <a href="/CEK/References/ClovaHomeInterface/Shared_Objects.html#ModeInfoObject">ModeInfoObject</a>로 이름을 변경하고 범용적인 기기의 운전 모드를 나타내는데 사용하는 객체로 설명을 수정</li>
          <li>[CEK] Clova Home extension 메시지의 <a href="/CEK/References/ClovaHomeInterface/Control_Interfaces.html">Control</a> 인터페이스에 <a href="/CEK/References/ClovaHomeInterface/Control_Interfaces.html#GetCurrentTemperatureRequest">GetCurrentTemperatureRequest</a> 메시지와 <a href="/CEK/References/ClovaHomeInterface/Control_Interfaces.html#GetCurrentTemperatureResponse">GetCurrentTemperatureResponse</a> 메시지 추가</li>
          <li>[CEK] Clova Home extension 메시지의 <a href="/CEK/References/ClovaHomeInterface/Error_Interfaces.html">Error</a> 인터페이스에 <a href="/CEK/References/ClovaHomeInterface/Error_Interfaces.html#UnsupportedOperationError">UnsupportedOperationError</a> 메시지 추가</li>
        </ul>
      </td>
    </tr>
    <tr>
      <td>v2.1</td><td>2017-11-13</td>
      <td>
        <ul>
          <li>[CIC] 볼륨 제어 관련 지시 메시지(<a href="/CIC/References/CICInterface/DeviceControl.html#Decrease">DeviceControl.Decrease</a>, <a href="/CIC/References/CICInterface/DeviceControl.html#Increase">DeviceControl.Increase</a>, <a href="/CIC/References/CICInterface/DeviceControl.html#SetValue">DeviceControl.SetValue</a>, <a href="/CIC/References/CICInterface/PlaybackController.html#Mute">PlaybackController.Mute</a>, <a href="/CIC/References/CICInterface/PlaybackController.html#Unmute">PlaybackController.Unmute</a>)의 Remarks 항목에 UX 관련 내용 추가</li>
          <li>[CEK] <a href="/CEK/References/ClovaHomeInterface/Shared_Objects.html#ApplianceInfoObject">ApplianceInfoObject</a>에서 에어컨 타입(AIRCONDITIONER)에 DecrementFanSpeed, IncrementFanSpeed, SetFanSpeed, SetMode actioin을 가습기 타입(HUMIDIFIER)에 SetFanSpeed를 추가 </li>
        </ul>
      </td>
    </tr>
    <tr>
      <td>v2.0</td><td>2017-11-06</td>
      <td>
        <ul>
          <li>[CIC] <a href="/CIC/References/CICInterface/SpeechRecognizer.html#KeepRecording">SpeechRecognizer.KeepRecording</a> 지시 메시지 추가</li>
          <li>[CIC] <a href="/CIC/References/Context_Objects.html#Display">Device.Display</a> 맥락 정보 추가</li>
          <li>[CIC] <a href="/CIC/References/ContentTemplates/ActionTimer.html">ActionTimer</a>, <a href="/CIC/References/ContentTemplates/ActionTimerList.html">ActionTimerList</a>, <a href="/CIC/References/ContentTemplates/Alarm.html">Alarm</a>, <a href="/CIC/References/ContentTemplates/AlarmList.html">AlarmList</a>, <a href="/CIC/References/ContentTemplates/Memo.html">Memo</a>, <a href="/CIC/References/ContentTemplates/MemoList.html">MemoList</a>, <a href="/CIC/References/ContentTemplates/Reminder.html">Reminder</a>, <a href="/CIC/References/ContentTemplates/ReminderList.html">ReminderList</a>, <a href="/CIC/References/ContentTemplates/Schedule.html">Schedule</a>, <a href="/CIC/References/ContentTemplates/ScheduleList.html">ScheduleList</a>, <a href="/CIC/References/ContentTemplates/Timer.html">Timer</a>, <a href="/CIC/References/ContentTemplates/TimerList.html">TimerList</a> 템플릿에 token 필드 추가</li>
          <li>[CEK] <a href="/CEK/References/CEK_API.html#CustomExtMessage">Custom extension 메시지</a> 중 요청 메시지에서 context.System.device.displayType 필드의 이름을 context.System.device.display로 바꾸고 하위 필드 구성을 변경</li>
        </ul>
      </td>
    </tr>
    <tr>
      <td>v1.9</td><td>2017-10-30</td>
      <td>
        <ul>
          <li>[Dev. console] <a href="/DevConsole/ClovaDevConsole_Overview.html">Clova developer console 개요</a> 설명 추가</li>
          <li>[Dev. console] <a href="/DevConsole/Guides/CEK/Register_Extension.html">Extension 등록하기</a> 가이드 추가</li>
          <li>[Dev. console] <a href="/DevConsole/Guides/CEK/Register_Interaction_Model.html">Interaction 모델 등록하기</a> 가이드 추가</li>
          <li>[Dev. console] <a href="/DevConsole/Guides/CEK/Deploy_Extension.html">Extension 배포하기</a> 가이드 추가</li>
        </ul>
      </td>
    </tr>
    <tr>
      <td>v1.8</td><td>2017-10-23</td>
      <td>
        <ul>
          <li>[CIC] <a href="/CIC/References/ContentTemplates/Text.html">Text</a> 템플릿에 emotionCode 필드와 motionCode 필드를 추가</li>
          <li>[CIC] <a href="/CIC/References/CICInterface/Alerts.html#SetAlert">Alerts.SetAlert</a> 지시 메시지의 assets[].url 필드 내용 변경</li>
          <li>[CIC] <a href="/CIC/References/CICInterface/AudioPlayer.html#StreamRequested">AudioPlayer.StreamRequested</a> 이벤트 메시지의 예제 오류 수정</li>
          <li>[CEK] <a href="/CEK/References/CEK_API.html#CustomExtMessage">Custom extension 메시지</a> 중 요청 메시지에 context.System.device.displayType 필드 추가</li>
        </ul>
      </td>
    </tr>
    <tr>
      <td>v1.7</td><td>2017-10-16</td>
      <td>
        <ul>
          <li>[CIC] <a href="/CIC/References/CICInterface/PlaybackController.html">PlaybackController</a> 네임스페이스에 <a href="/CIC/References/CICInterface/PlaybackController.html#Replay">Replay</a> 지시 메시지 추가</li>
          <li>[CIC] 알람 동기화에 대한 보충 설명을 <a href="/CIC/References/CICInterface/Alerts.html#AlertsWorkFlow">알람 동작 구조</a> 절에 추가</li>
          <li>[CIC] content 필드를 <a href="/CIC/References/Context_Objects.html#AlertsState">Alert.AlertsState</a> 문맥 정보의 <a href="/CIC/References/Context_Objects.html#AlertInfoObject">AlertInfoObject</a>에서 제거</li>
          <li>[공통] 일부 문서 이미지 수정 및 문서 오류 교정</li>
        </ul>
      </td>
    </tr>
    <tr>
      <td>v1.6</td><td>2017-10-02</td>
      <td>
        <ul>
          <li>[CIC] <a href="/CIC/References/CICInterface/Alerts.html">Alerts</a> 네임스페이스 및 알람 관련 인터페이스 추가</li>
          <li>[CIC] <a href="/CIC/References/CICInterface/System.html">System</a> 네임스페이스 및 알람 관련 인터페이스 추가</li>
          <li>[CIC] <a href="/CIC/References/CICInterface/SpeechRecognizer.html#ExpectSpeech">SpeechRecognizer.ExpectSpeech</a> 지시 메시지에 expectContentType 필드 추가</li>
          <li>[CIC] <a href="/CIC/References/Context_Objects.html#DeviceState">Device.DeviceState</a>의 <a href="/CIC/References/Context_Objects.html#VolumeInfoObject">VolumeInfoObject</a>에 warning 필드 추가</li>
          <li>[CIC] <a href="/CIC/References/ContentTemplates/ActionTimer.html">ActionTimer</a>, <a href="/CIC/References/ContentTemplates/ActionTimerList.html">ActionTimerList</a>, <a href="/CIC/References/ContentTemplates/Alarm.html">Alarm</a>, <a href="/CIC/References/ContentTemplates/AlarmList.html">AlarmList</a>, <a href="/CIC/References/ContentTemplates/Memo.html">Memo</a>, <a href="/CIC/References/ContentTemplates/MemoList.html">MemoList</a>, <a href="/CIC/References/ContentTemplates/Reminder.html">Reminder</a>, <a href="/CIC/References/ContentTemplates/ReminderList.html">ReminderList</a>, <a href="/CIC/References/ContentTemplates/Schedule.html">Schedule</a>, <a href="/CIC/References/ContentTemplates/ScheduleList.html">ScheduleList</a>, <a href="/CIC/References/ContentTemplates/Timer.html">Timer</a>, <a href="/CIC/References/ContentTemplates/TimerList.html">TimerList</a> 템플릿 추가</li>
          <li>[CIC] <a href="/CIC/References/ContentTemplates/ImageText.html">ImageText</a> 템플릿의 일부 코드 예제 수정</li>
          <li>[CIC] <a href="/CIC/References/ContentTemplates/Popup.html">Popup 템플릿</a> 일부 필드 수정</li>
          <li>[CIC] <a href="/CIC/Guides/Interact_with_CIC.html#CreateClovaAccessToken">Clova access token 생성하기</a>와 <a href="/CIC/References/Clova_Auth_API.html#RequestAuthorizationCode">Authorization code 요청</a>에 서비스 이용 약관에 대한 내용 추가</li>
        </ul>
      </td>
    </tr>
    <tr>
      <td>v1.5</td><td>2017-09-25</td>
      <td>
        <ul>
          <li>[CIC] <a href="/CIC/References/CICInterface/PlaybackController.html">PlaybackController API</a>에 음악 재생 제어용 <a href="/CIC/References/CICInterface/PlaybackController.html#NextCommandIssued">PlaybackController.NextCommandIssued</a> 이벤트 메시지와 <a href="/CIC/References/CICInterface/PlaybackController.html#PreviousCommandIssued">PlaybackController.PreviousCommandIssued</a> 이벤트 메시지 추가</li>
          <li>[CIC] <a href="/CIC/References/CICInterface/SpeechRecognizer.html#ExpectSpeech">SpeechRecognizer.ExpectSpeech</a> 지시 메시지에 expectSpeechId 필드를 <a href="/CIC/References/CICInterface/SpeechRecognizer.html#Recognize">SpeechRecognizer.Recognize</a> 이벤트 메시지에 speechId와 explicit 필드를 각각 추가</li>
          <li>[CIC] <a href="/CIC/References/ContentTemplates/Popup.html">Popup 템플릿</a> 추가</li>
          <li>[CEK] Clova Home API에 ChargeConfirmation 외 33건의 <a href="/CEK/References/ClovaHomeInterface/Control_Interfaces.html">Control API</a> 추가</li>
          <li>[CEK] Clova Home API <a href="/CEK/References/ClovaHomeInterface/Shared_Objects.html#ApplianceInfoObject">지원 기기</a> 6종 추가 및 location 필드 추가</li>
        </ul>
      </td>
    </tr>
    <tr>
      <td>v1.4</td><td>2017-09-18</td>
      <td>
        <ul>
          <li>[CIC] DeviceControl API에 <a href="/CIC/References/CICInterface/DeviceControl.html#ExpectReportState">DeviceControl.ExpectReportState</a> 지시 메시지, <a href="/CIC/References/CICInterface/DeviceControl.html#ReportState">DeviceControl.ReportState</a> 이벤트 메시지, <a href="/CIC/References/CICInterface/DeviceControl.html#RequestStateSynchronization">DeviceControl.RequestStateSynchronization</a> 이벤트 메시지 추가 및 DeviceControl.UpdateDeviceState 지시 메시지를 <a href="/CIC/References/CICInterface/DeviceControl.html#SynchronizeState">DeviceControl.SynchronizeState</a>로 이름 변경</li>
          <li>[CIC] <a href="/CIC/References/ContentTemplates/Text.html">Text</a> 템플릿에 item3 필드 추가</li>
          <li>[CIC] <a href="/CIC/References/CICInterface/AudioPlayer.html#Play">AudioPlayer.Play</a> 지시 메시지에 출처 정보 관련 source 필드 추가</li>
          <li>[CIC] <a href="/CIC/References/CICInterface/AudioPlayer.html#AudioStreamInfoObject">AudioStreamInfoObject</a>에 durationInMilliseconds 필드 추가 </li>
          <li>[CIC] Notifier 네임스페이스 및 <a href="/CIC/References/CICInterface/Notifier.html#ClearIndicator">ClearIndicator</a>, <a href="/CIC/References/CICInterface/Notifier.html#SetIndicator">SetIndicator</a> 지시 메시지 추가</li>
          <li>[CIC] <a href="/CIC/References/ContentTemplates/Atmosphere.html">대기 정보(Atmosphere) 템플릿</a> 추가</li>
          <li>[CIC] 라이선스 이슈에 따른 날씨 템플릿의 bgClipURL 필드 사용 불가 문구 추가</li>
        </ul>
      </td>
    </tr>
    <tr>
      <td>v1.3</td><td>2017-09-11</td>
      <td>
        <ul>
          <li>[CIC] <a href="/CIC/References/CICInterface/SpeechRecognizer.html#ExpectSpeech">SpeechRecognizer.ExpectSpeech</a> 지시 메시지에 explicit 필드 추가</li>
          <li>[CIC] <a href="/CIC/References/Content_Templates.md">Content template</a>에 <a href="/CIC/References/ContentTemplates/Common_Fields.md">공통 필드</a> 스펙 추가</li>
        </ul>
      </td>
    </tr>
>>>>>>> doc-KR-Partner
    <tr>
      <td style="text-align: center;">개념 이해</td>
      <td>
        <ul>
          <li><a href="/CIC/CIC_Overview.md#WhatisCIC">CIC란?</a></li>
          <li><a href="/CIC/CIC_Overview.md#DialogModel">대화 모델</a></li>
        </ul>
      </td>
      <td>
        <ul>
          <li><a href="/CEK/CEK_Overview.md#WhatisCEK">CEK란?</a></li>
          <li><a href="/Design/Design_Guideline_For_Extension.md#DefineInteractionModel">Interaction 모델 이해하기</a></li>
        </ul>
      </td>
    </tr>
    <tr>
      <td style="text-align: center;">디자인</td>
      <td>
        <ul>
          <li><a href="/Design/Design_Guideline_For_Client_Hardware.md">클라이언트 기기 디자인 가이드라인</a></li>
        </ul>
      </td>
      <td>
        <ul>
          <li><a href="/Design/Design_Guideline_For_Extension.md">Extension 디자인 가이드라인</a></li>
        </ul>
      </td>
    </tr>
    <tr>
      <td style="text-align: center;">개발</td>
      <td>
        <ul>
          <li>가이드</li>
          <ul>
            <li><a href="/CIC/Guides/Interact_with_CIC.md">CIC 연동하기</a></li>
          </ul>
          <li>레퍼런스</li>
          <ul>
            <li><a href="/CIC/References/CIC_API.md">CIC API 레퍼런스</a></li>
            <li><a href="/CIC/References/CIC_API.md#CICInterface">CIC 메시지 인터페이스</a></li>
            <li><a href="/CIC/References/Content_Templates.md">Content template</a></li>
            <li><a href="/CIC/References/Clova_Auth_API.md">CIC 인증 API 레퍼런스</a></li>
          </ul>
        </ul>
      </td>
      <td>
        <ul>
          <li>튜토리얼</li>
          <ul>
            <li><a href="/CEK/Tutorials/Build_Simple_Extension.md">기초적인 Extension 만들기</a></li>
            <li><a href="/CEK/Tutorials/Handle_Builtin_Intents.md">기본적인 의사 표현 처리하기</a></li>
            <li><a href="/CEK/Tutorials/Use_Builtin_Type_Slots.md">사용자가 입력한 정보 활용하기</a></li>
          </ul>
          <li>가이드</li>
          <ul>
            <li><a href="/CEK/Guides/Build_Custom_Extension.md">Custom extension 만들기</a></li>
            <li><a href="/CEK/Guides/Build_Clova_Home_Extension.md">Clova Home extension 만들기</a></li>
            <li><a href="/CEK/Guides/Link_User_Account.md">사용자 계정 연결하기</a></li>
            <li><a href="/DevConsole/Guides/CEK/Register_Extension.md">Extension 등록하기</a></li>
            <li><a href="/DevConsole/Guides/CEK/Register_Interaction_Model.md">Interaction 모델 등록하기</a></li>
          </ul>
          <li>레퍼런스</li>
          <ul>
            <li><a href="/CEK/References/CEK_API.md#CustomExtMessage">Custom extension 메시지</a></li>
            <li><a href="/CEK/References/CEK_API.md#ClovaHomeExtMessage">Clova Home extension 메시지</a></li>
          </ul>
          <li>Extension 예제</li>
          <ul>
            <li><a href="/CEK/Examples/Extension_Examples.md#MagicBall">마법 구슬(Magic ball)</a></li>
            <li><a href="/CEK/Examples/Extension_Examples.md#RainSound">빗소리(Rain sound)</a></li>
            <li><a href="/CEK/Examples/Extension_Examples.md#DiceDrawer">주사위 놀이(Dice drawer)</a></li>
            <li><a href="/CEK/Examples/Extension_Examples.md#CoinHelper">코인 헬퍼(Coin helper)</a></li>
          </ul>
        </ul>
      </td>
    </tr>
    <tr>
      <td style="text-align: center;">배포</td>
      <td>
        <ul>
          <li>클라이언트 등록하기(추가 예정)</li>
        </ul>
      </td>
      <td>
        <ul>
          <li><a href="/DevConsole/Guides/CEK/Deploy_Extension.md">Extension 배포하기</a></li>
        </ul>
      </td>
    </tr>
  </tbody>
</table>

<div class="note">
  <p><strong>Note!</strong></p>
  <p>Clova는 현재 개발이 계속 진행되고 있습니다. 따라서, 문서의 내용은 언제든지 변경될 수 있습니다.</p>
</div>
