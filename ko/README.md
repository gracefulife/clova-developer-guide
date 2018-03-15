# 문서 정보
이 문서는 Clova가 제공하는 CIC와 CEK 플랫폼에 대한 개발 가이드 및 API 레퍼런스를 제공합니다. 대상 독자는 CIC를 사용하여 Clova 서비스와 연동되는 전자 기기, 앱을 개발하려는 클라이언트 개발자와 CEK를 사용하여 온라인 콘텐츠 및 서비스를 제공하려는 Extension 개발자입니다.

<div class="note">
  <p><strong>Note!</strong></p>
  <p>Clova는 개발이 계속 진행되고 있습니다. 따라서, 문서의 내용은 언제든지 변경될 수 있습니다.</p>
</div>

## 연락처
문서와 관련하여 궁금한 사항은 지정된 Clova 제휴 담당자에게 문의합니다.

## 문서 버전 및 변경 이력

이 문서의 버전은 {{ book.DocVersion }}이며, 변경 이력은 다음과 같습니다.

<table>
  <thead>
    <tr>
      <th style="width:5%">버전</th><th style="width:15%">배포 일자</th><th style="width:80%">이력 사항</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>v3.5</td><td>2018-03-19</td>
      <td>
        <ul>
          <li>[CIC] <a href="/CIC/References/Context_Objects.html#DeviceState">Device.DeviceState</a>에 <a href="/CIC/References/Context_Objects.html#SoundOutputInfoObject">SoundOutputInfoObject</a> 추가</li>
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

    <tr>
      <td>v1.2</td><td>2017-09-04</td>
    <td>
      <ul>
        <li>[CIC] <a href="/CIC/References/CICInterface/Clova.html#Help">Clova.Help</a> 지시 메시지 추가</li>
        <li>[CIC] <a href="/CIC/References/CICInterface/DeviceControl.html#LaunchApp">DeviceControl.LaunchApp</a> 지시 메시지 추가</li>
        <li>[CIC] TextRecognizer 네임스페이스 및 <a href="/CIC/References/CICInterface/TextRecognizer.html">TextRecognizer.Recognize</a> 이벤트 메시지 추가</li>
        <li>[CIC] <a href="/CIC/References/CIC_API.html">CIC API</a>, <a href="/CEK/References/CEK_API.html">CEK API</a>의 목차, 설명 재작성</li>
        <li>[CIC] CIC API 내용 업데이트: 요청/응답 헤더의 Status code 추가, REST API reference 문서 포맷 적용</li>
        <li>[기타] 일부 문서 오류 수정</li>
      </ul>
    </td>
    </tr>

    <tr>
      <td>v1.1</td>
    <td>2017-08-28</td>
    <td>
      <ul>
        <li>[CIC] 셋톱박스용 TV 채널 정보 스펙과 전원 상태 정보 스펙을 <a href="/CIC/References/Context_Objects.html#DeviceState">Device.DeviceState</a>와 <a href="/CIC/References/CICInterface/DeviceControl.html">DeviceControl API</a>에 추가</li>
        <li>[CIC] <a href="/CIC/References/CICInterface/DeviceControl.html">DeviceControl API</a>에서 target으로 사용되는 값 일부 추가 및 변경: power, energysave, screenbrightness</li>
        <li>[CIC] <a href="/CIC/References/CICInterface/DeviceControl.html">DeviceControl API</a>의 SetPoint를 <a href="/CIC/References/CICInterface/DeviceControl.html#SetValue">SetValue</a>로 이름 변경</li>
        <li>[CIC] <a href="/CIC/References/Clova_Auth_API.html">Clova 인증 API</a> 내용 업데이트 - 요청/응답 헤더와 Status code 추가, REST API reference 문서 포맷 적용</li>
        <li>[CEK] <a href="/CEK/References/ClovaHomeInterface/Error_Interfaces.html#ValueOutOfRangeError">ValueOutOfRangeError</a>를 Clova Home의 Error 인터페이스에 추가</li>
      </ul>
    </td>
    </tr>

    <tr>
      <td>v1.0</td><td>2017-08-21</td>
      <td>[CIC] <a href="/CIC/Guides/Interact_with_CIC.html#ManageConnection">Access token 갱신</a>절 추가 및 /token API 내용 업데이트</td>
    </tr>

    <tr>
      <td>v0.9</td><td>2017-08-14</td>
      <td>
        <ul>
          <li>[CIC] <a href="/CIC/CIC_Overview.html#DialogModel">대화 모델</a> 설명 추가</li>
          <li>[CIC] <a href="/CIC/References/CICInterface/DeviceControl.html">DeviceControl</a> API 추가</li>
          <li>[CIC] <a href="/CIC/References/Context_Objects.html">Device.DeviceState</a> payload 필드 추가: airplane, battery, bluetooth, brightness, flashLight, gps, powerSavingMode, soundMode, volume, wifi</li>
          <li>[CEK] <a href="/CEK/Guides/Build_Custom_Extension.html#DoMultiturnDialog">Multi-turn 대화 수행하기</a>절 추가 및 sessionAttributes 필드 설명 업데이트</li>
        </ul>
      </td>
    </tr>

    <tr>
      <td>v0.8</td><td>2017-08-04</td>
      <td>
        <ul>
          <li>[CIC] <a href="/CIC/References/CICInterface/Clova.html#Hello">Clova.Hello</a> 지시 메시지 추가</li>
          <li>[CIC] <a href="/CIC/References/CICInterface/AudioPlayer.html#Play">AudioPlayer.Play</a> 지시 메시지의 AudioItem 객체에 type 필드 추가</li>
          <li>[CIC] <a href="/CIC/References/CICInterface/AudioPlayer.html#AudioStreamInfoObject">AudioStreamInfoObject</a> 객체에 urlPlayable 필드 추가</li>
          <li>[CIC] <a href="/CIC/References/CIC_API.html#Error">CIC 오류 메시지</a> 스펙 추가</li>
          <li>[CIC] <a href="/CIC/References/CIC_API.html#MultipartMessage">Multipart 메시지</a> 내용 재작성</li>
          <li>[CEK] Clova Home <a href="/CEK/References/ClovaHomeInterface/Shared_Objects.html#ApplianceInfoObject">지원 기기</a> 추가: 공기청정기, 가습기, 셋톱박스, 난방기기</li>
          <li>[CEK] Clova Home <a href="/CEK/References/ClovaHomeInterface/Shared_Objects.html#ApplianceInfoObject">지원 기기</a> 제외: 도어락</li>
        </ul>
      </td>
    </tr>

    <tr>
      <td>v0.7</td><td>2017-07-28</td>
      <td>
        <ul>
          <li>[CIC] <a href="/CIC/References/CICInterface/AudioPlayer.html">AudioPlayer</a>의 PlayNext, Stop 제거 (<a href="/CIC/References/CICInterface/PlaybackController.html">PlaybackController</a>에 병합)</li>
          <li>[CIC]  <a href="/CIC/References/CICInterface/PlaybackController.html">PlaybackController</a>의 메시지 이름 변경(Mute, Next, Pause, Previous, Resume, Stop, Unmute, VolumeDown, VolumeUp </li>
          <li>[CIC] 길찾기 템플릿 추가: CarRoute, TransportationRoute</li>
          <li>[CIC] 날씨 템플릿 추가: <a href="/CIC/References/ContentTemplates/Humidity.html">Humidity</a>, <a href="/CIC/References/ContentTemplates/TodayWeather.html">TodayWeather</a>, <a href="/CIC/References/ContentTemplates/TomorrowWeather.html">TomorrowWeather</a>, <a href="/CIC/References/ContentTemplates/WeeklyWeather.html">WeeklyWeather</a>, <a href="/CIC/References/ContentTemplates/WindSpeed.html">WindSpeed</a></li>
        </ul>
      </td>
    </tr>

    <tr>
      <td>v0.6</td><td>2017-07-14</td>
      <td>[CIC] <a href="/CIC/References/CICInterface/AudioPlayer.html#AudioStreamInfoObject">AudioStreamInfoObject</a> 객체 beginAtInMilliseconds 필드 내용 추가</td>
    </tr>

    <tr>
      <td>v0.5</td><td>2017-07-07</td>
      <td>
        <ul>
          <li>[CEK] <a href="/CEK/References/CEK_API.html#CustomExtResponseMessage">Custom extension 응답 메시지</a>의 <a href="/CEK/References/CEK_API.html#CustomExtResponseMessage">outputSpeech</a> 객체 구성 업데이트 반영</li>
          <li>[공통] <a href="/Terms.html">용어집 추가</a></li>
          <li>CEK 메시지 포맷 파트의 목차 업데이트</li>
        </ul>
      </td>
    </tr>
    <tr>
      <td>v0.4</td><td>2017-07-03</td>
      <td>
        <ul>
          <li>[CEK] CEK 문서 이미지 내용 업데이트</li>
          <li>[공통] 문서 리뷰 결과 반영</li>
        </ul>
      </td>
    </tr>
    <tr>
      <td>v0.3</td><td>2017-06-19</td>
      <td>
        <ul>
          <li>[CEK] CEK 문서 파트 작성</li>
          <li>[CIC] <a href="/CIC/Guides/Interact_with_CIC.html#ManageConnection">연결 관리하기</a> 업데이트 (HTTP Ping 프레임을 사용할 수 없을 경우)</li>
        </ul>
      </td>
    </tr>
    <tr>
      <td>v0.2</td><td>2017-06-08</td>
      <td>[CIC] <a href="/CIC/Guides/Interact_with_CIC.html">CIC 연동하기</a>에 <a href="/CIC/Guides/Interact_with_CIC.md#ManageConnection">연결 관리하기</a> 추가 (HTTP Ping)</td>
    </tr>
    <tr>
      <td>v0.1</td><td>2017-05-29</td>
      <td>[CIC] CIC 문서 파트 작성</td>
    </tr>
  </tbody>
</table>
