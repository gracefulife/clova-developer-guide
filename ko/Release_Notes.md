# 릴리즈 노트

이 페이지는 Clova 플랫폼과 문서의 변경 이력을 제공합니다.

## 2018-05-28

* CEK
  * Clova Home extension API [ConditionsNotMetError](/CEK/References/ClovaHomeInterface/Error_Interfaces.md#ConditionsNotMetError)에 state 필드 추가
  * Clova Home extension API [TVChannelInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#TVChannelInfoObject)에 서브 채널 정보 추가

## 2018-05-21

* CIC
  * [Device.DeviceState](/CIC/References/Context_Objects.md#DeviceState) 맥락 객체의 [BluetoothInfoObject]/CIC/References/Context_Objects.md#BluetoothInfoObject에 빠진 필드(btlist[].role) 추가
* CEK
  * Clova Home extension API에 [ValueNotFoundError](/CEK/References/ClovaHomeInterface/Error_Interfaces.md#ValueNotFoundError) 추가

## 2018-05-14

* CIC
  * [LaunchURI](/CIC/References/CICInterface/Clova.md#LaunchURI) 지시 메시지를 DeviceControl 네임스페이스에서 [Clova](/CIC/References/CICInterface/Clova.md) 네임스페이스로 이전

* CEK
  * HTTP 요청 메시지에 헤더(SignatureCEK, SignatureCEKCertChainUrl) 추가 및 [요청 메시지 검증](/CEK/References/CEK_API.md#RequestMessageValidation)절 추가

## 2018-05-07
* CIC
  * DeviceControl 네임스페이스에 LaunchURI 지시 메시지 추가
  * [DeviceControl](/CIC/References/CICInterface/DeviceControl.md) 네임스페이스의 [LaunchApp](/CIC/References/CICInterface/DeviceControl.md#LaunchApp) 지시 메시지와 [OpenScreen](/CIC/References/CICInterface/DeviceControl.md#OpenScreen) 지시 메시지의 지원을 중지(Deprecated)

## 2018-04-30

* CEK
  * Clova Home extension API에 [GetOpenStateRequest](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#GetOpenStateRequest), [GetOpenStateResponse](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#GetOpenStateResponse)

## 2018-04-23

* CEK
  * Clova Home extension API에 [ReleaseModeConfirmation](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#ReleaseModeConfirmation), [ReleaseModeRequest](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#ReleaseModeRequest) 추가

## 2018-04-16

* CIC
  * [SpeechRecognizer.Recognize](/CIC/References/CICInterface/SpeechRecognizer.md#Recognize) 이벤트 메시지의 wakeWord 필드 설명 및 Audio data 설명 업데이트
  * [DeviceControl](/CIC/References/CICInterface/DeviceControl.md) 네임스페이스에 [Open](/CIC/References/CICInterface/DeviceControl.md#Open) 지시 메시지 추가

* CEK
  * Clova Home extension API [GetLockStateResponse](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#GetLockStateResponse)에 openState 필드 추가
  * Clova Home extension API에 [GetCleaningCycleRequest](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#GetCleaningCycleRequest), [GetCleaningCycleResponse](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#GetCleaningCycleResponse) 추가

## 2018-04-09

* CIC
  * 클라이언트 기기 디자인 가이드라인에서 [부팅 화면](/Design/Design_Guideline_For_Client_Hardware.md#BootingScreen) 관련 설명 및 예제 이미지를 업데이트

* CEK
  * Clova Home extension API [ColorInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#ColorInfoObject)의 brightness 필드의 설명 및 필수/포함 여부 변경

## 2018-04-02

* CIC
  * [AudioPlayer](/CIC/References/CICInterface/AudioPlayer.md) 네임스페이스에 메시지 스펙 추가 및 일부 필드 업데이트
    * [AudioPlayer.ExpectReportPlaybackState](/CIC/References/CICInterface/AudioPlayer.md#ExpectReportPlaybackState) 지시 메시지, [AudioPlayer.ReportPlaybackState 이벤트 메시지](/CIC/References/CICInterface/AudioPlayer.md#ReportPlaybackState){% if book.TargetReaderType == "Internal" %}, [AudioPlayer.RequestPlaybackState](/CIC/References/CICInterface/AudioPlayer.md#RequestPlaybackState) 이벤트 메시지, [SynchronizePlaybackState 지시 메시지](/CIC/References/CICInterface/AudioPlayer.md#SynchronizePlaybackState){% endif %} 추가
    * [AudioPlayer.Play](/CIC/References/CICInterface/AudioPlayer.md#Play) 지시 메시지의 payload 필드 내용 업데이트
    * ProgressReportXXX, PlayXXX 형식의 이름을 가진 이벤트 필드에 token 필드 값 필수로 추가
  * [AudioPlayer.PlaybackState](/CIC/References/Context_Objects.md#PlaybackState) 맥락 객체에 repeatMode 추가
  * [PlaybackController](/CIC/References/CICInterface/PlaybackController.md) 네임스페이스에 총 12건의 메시지 스펙 추가
    * [PlaybackController.PauseCommandIssued](/CIC/References/CICInterface/PlaybackController.md#PauseCommandIssued), [PlaybackController.PlayCommandIssued](/CIC/References/CICInterface/PlaybackController.md#PlayCommandIssued), [PlaybackController.ResumeCommandIssued](/CIC/References/CICInterface/PlaybackController.md#ResumeCommandIssued), [PlaybackController.SetRepeatModeCommandIssued](/CIC/References/CICInterface/PlaybackController.md#SetRepeatModeCommandIssued), [PlaybackController.StopCommandIssued](/CIC/References/CICInterface/PlaybackController.md#StopCommandIssued) 이벤트 메시지 추가
    * [PlaybackController.ExpectNextCommand](/CIC/References/CICInterface/PlaybackController.md#ExpectNextCommand), [PlaybackController.ExpectPauseCommand](/CIC/References/CICInterface/PlaybackController.md#ExpectPauseCommand), [PlaybackController.ExpectPlayCommand](/CIC/References/CICInterface/PlaybackController.md#ExpectPlayCommand), [PlaybackController.ExpectPreviousCommand](/CIC/References/CICInterface/PlaybackController.md#ExpectPreviousCommand), [PlaybackController.ExpectResumeCommand](/CIC/References/CICInterface/PlaybackController.md#ExpectResumeCommand), [PlaybackController.ExpectStopCommand](/CIC/References/CICInterface/PlaybackController.md#ExpectStopCommand), [PlaybackController.SetRepeatMode](/CIC/References/CICInterface/PlaybackController.md#SetRepeatMode) 지시 메시지 추가
    * [PlaybackController.TurnOnRepeatMode](/CIC/References/CICInterface/PlaybackController.md#TurnOnRepeatMode) 지시 메시지와 [PlaybackController.TurnOffRepeatMode](/CIC/References/CICInterface/PlaybackController.md#TurnOffRepeatMode)는 사라질 예정
  * 미디어 스트림을 위한 정보와 재생 목록을 표시하기 위한 재생 메타 정보를 분리하기 위해 [TemplateRuntime](/CIC/References/CICInterface/TemplateRuntime.md) 네임스페이스 추가
  * [Device.DeviceState](/CIC/References/Context_Objects.md#DeviceState)의 [BluetoothInfoObject](/CIC/References/Context_Objects.md#BluetoothInfoObject)에 scanlist 필드 추가
  * PIN 코드를 사용하는 외부 블루투스 기기와 연결할 수 있도록 [DeviceControl](/CIC/References/CICInterface/DeviceControl.md) 네임 스페이스에 [BtConnectByPINCode](/CIC/References/CICInterface/DeviceControl.md#BtConnectByPINCode) 지시 메시지와 [BtRequestForPINCode](/CIC/References/CICInterface/DeviceControl.md#BtRequestForPINCode), [BtRequestToCancelPinCodeInput](/CIC/References/CICInterface/DeviceControl.md#BtRequestToCancelPinCodeInput) 이벤트 메시지 추가
  * [DeviceControl](/CIC/References/CICInterface/DeviceControl.md) 네임 스페이스의 [BtConnect](/CIC/References/CICInterface/DeviceControl.md#BtConnect) 지시 메시지에 payload 추가
* CEK
  * Clova Home extension API에 GetSleepStartTimeRequest 외 9건의 [Control API](/CEK/References/ClovaHomeInterface/Control_Interfaces.md)와 4건의 [공유 객체](/CEK/References/ClovaHomeInterface/Shared_Objects.md) 추가
  * Clova Home extension API의 [DiscoverAppliancesResponse](/CEK/References/ClovaHomeInterface/Discovery_Interfaces.md#DiscoverAppliancesResponse)에 [CustomCommandInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#CustomCommandInfoObject) 추가
  * Clova Home extension API에서 TimeAmountInfoObject [공유 객체](/CEK/References/ClovaHomeInterface/Shared_Objects.md) 제거 및 이에 따른 [Control API](/CEK/References/ClovaHomeInterface/Control_Interfaces.md)의 일부 내용 변경
  * Clova Home extension API의 [ApplianceInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#ApplianceInfoObject)에 tags 필드 추가 및 location 필드 설명 변경
* Clova developer console
  * Clova developer console의 일부 UI 업데이트 적용

## 2018-03-19

* CIC
  * [Device.DeviceState](/CIC/References/Context_Objects.md#DeviceState)에 [SoundOutputInfoObject](/CIC/References/Context_Objects.md#SoundOutputInfoObject) 추가
  * 사용자가 설정한 임의의 명령을 실행할 수 있는 [CustomCommandIssued](/CIC/References/CICInterface/PlaybackController.md#CustomCommandIssued) 이벤트 메시지를 [PlaybackController](/CIC/References/CICInterface/PlaybackController.md#CustomCommandIssued) 네임스페이스에 추가

* CEK
  * Clova Home extension API에 CloseConfirmation 외 47건의 [Control API](/CEK/References/ClovaHomeInterface/Control_Interfaces.md)와 약 10종의 [공유 객체](/CEK/References/ClovaHomeInterface/Shared_Objects.md)
 추가
  * Clova Home extension API [지원 기기](/CEK/References/ClovaHomeInterface/Shared_Objects.md#ApplianceInfoObject) 30종 추가

## 2018-03-05

* CIC
  * [SpeechRecognizer.Recognize](/CIC/References/CICInterface/SpeechRecognizer.md#Recognize) 이벤트 메시지 initiator 필드의 설명을 수정
  * [클라이언트 기기 디자인 가이드라인](/Design/Design_Guideline_For_Client_Hardware.md)에서 클라이언트 상태 중 Hearing 상태의 이름을 Listening으로 수정
  * 클라이언트 기기 디자인 가이드라인의 [소리](/Design/Design_Guideline_For_Client_Hardware.md#Audio)에서 오디오 콘텐츠 타입으로 Feedback 타입을 추가하고 설명에 관련 규칙을 추가
  * [튜토리얼](/CEK/Tutorials/Introduction.md) 페이지에 [사용자가 입력한 정보 활용하기](/CEK/Tutorials/Use_Builtin_Type_Slots.md) 페이지 추가

## 2018-02-26

* CIC
  * [SpeechRecognizer.Recognize](/CIC/References/CICInterface/SpeechRecognizer.md#Recognize) 이벤트 메시지 initiator 필드에 deviceUUID 필드를 추가
  * 알람 동기화와 관련된 [RequestSynchronizeAlert](/CIC/References/CICInterface/Alerts.md#RequestSynchronizeAlert) 이벤트 메시지와 [SynchronizeAlert](/CIC/References/CICInterface/Alerts.md#SynchronizeAlert) 지시 메시지를 [Alerts](/CIC/References/CICInterface/Alerts.md) 네임스페이스에 추가
  * System 네임스페이스에서 알람 동기화와 관련된 일부 필드를 제거할 예정

## 2018-02-19

* CIC
  * 사용자의 호출을 정확히 판단하기 위해 [SpeechRecognizer.Recognize](/CIC/References/CICInterface/SpeechRecognizer.md#Recognize) 이벤트 메시지에 initiator 필드를 추가
  * 리마인더 및 동작 예약의 내용을 확인하기 위해 [Alerts.SetAlert](/CIC/References/CICInterface/Alerts.md#SetAlert) 지시 메시지에 label 필드를 추가
  * 리마인더 및 동작 예약의 내용을 표시하기 위해 [ActionTimer](/CIC/References/ContentTemplates/ActionTimer.md), [ActionTimerList](/CIC/References/ContentTemplates/ActionTimerList.md), [Reminder](/CIC/References/ContentTemplates/Reminder.md), [ReminderList](/CIC/References/ContentTemplates/ReminderList.md) 템플릿에 label 필드를 추가

## 2018-02-05

* CIC
  * [Atmosphere](/CIC/References/ContentTemplates/Atmosphere.md), [CardList](/CIC/References/ContentTemplates/CardList.md), [Humidity](/CIC/References/ContentTemplates/Humidity.md), [TodayWeather](/CIC/References/ContentTemplates/TodayWeather.md), [TomorrowWeather](CIC/References/ContentTemplates/TomorrowWeather.md), [WeeklyWeather](/CIC/References/ContentTemplates/WeeklyWeather.md), [WindSpeed](CIC/References/ContentTemplates/WindSpeed.md) 템플릿에 출처 관련 필드 등 추가
  * [AudioStreamInfoObject](/CIC/References/CICInterface/AudioPlayer.md#AudioStreamInfoObject)의 durationInMilliseconds 필드에 대한 설명 수정

* CEK
  * Extension 시작 호출([LaunchRequest](CEK/Guides/Build_Custom_Extension.md#HandleLaunchRequest))에 대한 설명 수정 및 [Extension 디자인 가이드라인 문서 반영](/Design/Design_Guideline_For_Extension.md)
  * CEK와 extension간 통신에 사용되는 [HTTP 프로토콜 버전](/CEK/CEK_Overview.md#WhatisCEK) 명시
  * [튜토리얼](/CEK/Tutorials/Introduction.md) 페이지에 [기본적인 의사 표현 처리하기](/CEK/Tutorials/Handle_Builtin_Intents.md) 페이지 추가

* Clova developer console
  * Extension 서버에서 사용해야 할 [포트](/DevConsole/Guides/CEK/Register_Extension.md#SetServerConnection)를 명시

## 2018-01-29

* Design
  * [클라이언트 기기 디자인 가이드라인](/Design/Design_Guideline_For_Client_Hardware.md)에 [Reminder용 효과음](/Design/Design_Guideline_For_Client_Hardware.md#SoundEffect) 추가

* CIC
  * [Notifier](/CIC/References/CICInterface/Notifier.md) 네임스페이스에 [Notifier.Notify](/CIC/References/CICInterface/Notifier.md#Notify) 이벤트 메시지 추가 및 해당 네임스페이스 메시지의 payload 필드 업데이트
  * [SpeechSynthesizer.SpeechState](/CIC/References/ContextObjects/SpeechState.md) 및 [SpeechSynthesizer](/CIC/References/CICInterface/SpeechSynthesizer.md) 네임스페이스에 [SpeechFinished](/CIC/References/CICInterface/SpeechSynthesizer.md#SpeechFinished), [SpeechStarted](/CIC/References/CICInterface/SpeechSynthesizer.md#SpeechStarted), [SpeechStopped](/CIC/References/CICInterface/SpeechSynthesizer.md#SpeechStopped) 이벤트 메시지 추가
  * Multi-turn 대화를 위해 [TextRecognizer.Recognize](/CIC/References/CICInterface/TextRecognizer.md) 이벤트 메시지에 speechId, explicit 필드 추가

* CEK
  * Clova Home extension 메시지 레퍼런스 중 [Error 인터페이스](/CEK/References/ClovaHomeInterface/Error_Interfaces.md)에 [NoSuchTargetError](/CEK/References/ClovaHomeInterface/Error_Interfaces.md#NoSuchTargetError), [NotSupportedInCurrentModeError](/CEK/References/ClovaHomeInterface/Error_Interfaces.md#NotSupportedInCurrentModeError), [UnsupportedOperationError](/CEK/References/ClovaHomeInterface/Error_Interfaces.md#UnsupportedOperationError) 그리고 [ValueOutOfRangeError](/CEK/References/ClovaHomeInterface/Error_Interfaces.md#ValueOutOfRangeError) 추가

* Clova developer console
  * [테스터 아이디 적용 자동화](/DevConsole/Guides/CEK/Test_Extension.md#TestOnClovaApp)
  * [Extension 서버 연동 설정](/DevConsole/Guides/CEK/Register_Extension.md#SetServerConnection) 전 연결 확인하는 방법 추가
  * Clova developer console의 일부 UI 업데이트 문서 적용

## 2018-01-22

* Design
  * 플랫폼 지원 오디오 압축 포맷 내용을 [클라이언트 기기 디자인 가이드라인](/Design/Design_Guideline_For_Client_Hardware.md#SupportedAudioCompressionFormat)과 [extension 디자인 가이드라인](/Design/Design_Guideline_For_Extension.md#SupportedAudioCompressionFormat)에 각각 추가

* CEK
  * [튜토리얼](/CEK/Tutorials/Introduction.md) 페이지와 [기초적인 extension 만들기](/CEK/Tutorials/Build_Simple_Extension.md) 페이지 추가

* Clova developer console
  - [Built-in intent 목록 표시](/DevConsole/Guides/CEK/Register_Interaction_Model.md#AddCustomSlotType), [심사 신청](/DevConsole/Guides/CEK/Deploy_Extension.md#InputComplianceInfo) 시 심사 요청 메시지 작성을 위한 UI 추가

* 공통 사항
  * UML 다이어그램의 이미지 포맷 변경

## 2018-01-15

* Design
  - [클라이언트 기기 디자인 가이드라인](/Design/Design_Guideline_For_Client_Hardware.md)에 알람, 리마인더, 타이머에 대한 조명 효과 및 효과음 가이드라인 설명 추가

## 2018-01-08

* Design
  - 플랫폼 구현 상황에 맞게 [built-in intent](/Design/Design_Guideline_For_Extension.md#DefineInteractionModel)에 대한 설명 수정

* CIC
  - 사용자 요청 위임 처리를 위한 [Clova.HandleDelegatedEvent](/CIC/References/CICInterface/Clova.md#HandleDelegatedEvent) 지시 메시지와 [Clova.ProcessDelegatedEvent](/CIC/References/CICInterface/Clova.md#ProcessDelegatedEvent) 이벤트 메시지 추가
  - [위임된 사용자 요청 처리하기](/CIC/Guides/Interact_with_CIC.md#HandleDelegation) 절 추가
  - [PlaybackController.NextCommandIssued](/CIC/References/CICInterface/PlaybackController.md#NextCommandIssued)와 [PlaybackController.PreviousCommandIssued](/CIC/References/CICInterface/PlaybackController.md#PreviousCommandIssued) 이벤트 메시지에 [AudioPlayer.PlaybackState](/CIC/References/CICInterface/PlaybackController.md#PlaybackState) 맥락 정보를 포함하도록 설명 추가
  - [Alerts](/CIC/References/CICInterface/Alerts.md) API의 [동작 구조](/CIC/References/CICInterface/Alerts.md#AlertsWorkFlow)에 대한 설명 개선
  - [DeviceControl](/CIC/References/CICInterface/DeviceControl.md) API의 [동작 구조](/CIC/References/CICInterface/DeviceControl.md#DeviceContorlWorkFlow)에 대한 설명 추가
  - 일부 [content template](/CIC/References/Content_Templates.md) 및 공유 객체에 대한 오류 교정 내용 수정

* CEK
  - [Extension 예제](/CEK/Examples/Extension_Examples.md) 페이지 추가

* Clova developer console
  - Extension 테스트 수행을 위해 **테스터 아이디** 필드를 extension 기본 정보 등록 메뉴에 추가
  - **테스터 아이디** 필드 추가에 따른 [Extension 테스트하기](/DevConsole/Guides/CEK/Test_Extension.md) 설명 업데이트

## 2018-01-02

* CIC
  - [Downchannel 구성](/CIC/References/CIC_API.md#EstablishDownchannel)에 429 오류 코드 추가 및 관련 설명을 Remarks 항목에 추가
  - 길찾기 템플릿(CarRoute, TransportationRoute) 제거, 길찾기에 대한 UI 표현을 위해 ImageText 템플릿을 사용하는 것으로 대체됨

## 2017-12-18

* Design
  - [Interaction 모델 등록하기](DevConsole/Guides/CEK/Register_Interaction_Model.md)에서 [interaction 모델 정의하기](/Design/Design_Guideline_For_Extension.md#DefineInteractionModel) 절 내용을 [Extension 디자인 가이드라인](/Design/Design_Guideline_For_Extension.md) 문서로 이동
  - [Interaction 모델 정의하기](/Design/Design_Guideline_For_Extension.md#DefineInteractionModel) 절 내용에 [발화 예시](/Design/Design_Guideline_For_Extension.md#UtteranceExample)문 작성 가이드라인 추가

* CIC
  - [SpeechRecognizer](/CIC/References/CICInterface/SpeechRecognizer.md) 인터페이스에서 ExpectSpeechTimedOut 이벤트 메시지 제거
  - [맥락 정보(context)](/CIC/References/Context_Objects.md)에서 Clova.FreetalkState 개체 제거

* Clova developer console
  - Clova developer console UI 개선
  - [Interaction 모델 정의하기](/DevConsole/Guides/CEK/Define_Interaction_Model.md)에 [발화 예시문](/DevConsole/Guides/CEK/Define_Interaction_Model.md#UtteranceExample) 작성 가이드라인 추가
  - [Extension 테스트하기](/DevConsole/Guides/CEK/Test_Extension.md)에 [테스트 모드 사용하기](/DevConsole/Guides/CEK/Test_Extension.md#UsingTestMode) 추가
  - [Extension 업데이트하기](/DevConsole/Guides/CEK/Update_Extension.md), [Extension 중지 및 삭제하기](/DevConsole/Guides/CEK/Remove_Extension.md) 추가

## 2017-12-10

* Design
  - [Extension 디자인 가이드라인](/Design/Design_Guideline_For_Extension.md) 추가

* CIC
  - [AudioPlayer](/CIC/References/CICInterface/AudioPlayer.md) 인터페이스에 [ClearQueue](/CIC/References/CICInterface/AudioPlayer.md#ClearQueue) 지시 메시지 추가

## 2017-12-04

* Design
  - [오디오 재생 규칙(audio interruption rule)](/Design/Design_Guideline_For_Client_Hardware.md#AudioInterruptionRule)을 [클라이언트 기기 디자인 가이드라인](/Design/Design_Guideline_For_Client_Hardware.md)에 추가
  - [클라이언트 기기 디자인 가이드라인](/Design/Design_Guideline_For_Client_Hardware.md)에 사용된 이미지 개선

* CIC
  - [CIC 연동하기](/CIC/Guides/Interact_with_CIC.md)의 사전 준비사항에 [User-Agent string](/CIC/Guides/Interact_with_CIC.md#UserAgentString)을 추가
  - [CIC API 레퍼런스](/CIC/References/CIC_API.md)>의 [이벤트 메시지 전송](/CIC/References/CIC_API.md#SendEvent) 절에 412 Precondition Failed 상태 코드 설명 추가

* CEK
  - 사용자 multi-turn 대화를 위해 reprompt 필드 설명을 [응답 메시지](/CEK/References/CEK_API.md#CustomExtResponseMessage)에 추가
  - 일부 문서 오류 수정

## 2017-11-20

* Design
  - [클라이언트 기기 디자인 가이드라인](/Design/Design_Guideline_For_Client_Hardware.md) 추가

* CIC
  - 오디오 콘텐츠 및 이미지 썸네일 표시를 위해 [CardList 템플릿](/CIC/References/ContentTemplates/CardList.md)의 subType 값에 Type5, Type6를 추가

* CEK
  - Clova Home extension 메시지의 [공유 객체](/CEK/References/ClovaHomeInterface/Shared_Objects.md) HeatingModeInfoObject를 [ModeInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#ModeInfoObject)로 이름을 변경하고 범용적인 기기의 운전 모드를 나타내는데 사용하는 객체로 설명을 수정
  - Clova Home extension 메시지의 [Control](/CEK/References/ClovaHomeInterface/Control_Interfaces.md) 인터페이스에 [GetCurrentTemperatureRequest](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#GetCurrentTemperatureRequest) 메시지와 [GetCurrentTemperatureResponse](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#GetCurrentTemperatureResponse) 메시지 추가
  - Clova Home extension 메시지의 [Error](/CEK/References/ClovaHomeInterface/Error_Interfaces.md) 인터페이스에 [UnsupportedOperationError](/CEK/References/ClovaHomeInterface/Error_Interfaces.md#UnsupportedOperationError) 메시지 추가

## 2017-11-13

* CIC
  - 볼륨 제어 관련 지시 메시지([DeviceControl.Decrease](/CIC/References/CICInterface/DeviceControl.md#Decrease), [DeviceControl.Increase](/CIC/References/CICInterface/DeviceControl.md#Increase), [DeviceControl.SetValue](/CIC/References/CICInterface/DeviceControl.md#SetValue), [PlaybackController.Mute](/CIC/References/CICInterface/PlaybackController.md#Mute), [PlaybackController.Unmute](/CIC/References/CICInterface/PlaybackController.md#Unmute))의 Remarks 항목에 UX 관련 내용 추가
  - [ReminderList](/CIC/References/ContentTemplates/ReminderList.md) 템플릿 예제 오류 수정


* CEK
  - [ApplianceInfoObject](/CEK/References/ClovaHomeInterface/Shared_Objects.md#ApplianceInfoObject)에서 에어컨 타입(AIRCONDITIONER)에 DecrementFanSpeed, IncrementFanSpeed, SetFanSpeed, SetMode actioin을 가습기 타입(HUMIDIFIER)에 SetFanSpeed를 추가

## 2017-11-06

* CIC
  - [`SpeechRecognizer.KeepRecording`](/CIC/References/CICInterface/SpeechRecognizer.md#KeepRecording) 지시 메시지 추가
  - 클라이언트의 디스플레이 장치 정보를 공유하기 위한 [`Device.Display`](/CIC/References/Context_Objects.md#Display) 맥락 정보 추가
  - [`ActionTimer`](/CIC/References/ContentTemplates/ActionTimer.md), [`ActionTimerList`](/CIC/References/ContentTemplates/ActionTimerList.md), [`Alarm`](/CIC/References/ContentTemplates/Alarm.md), [`AlarmList`](/CIC/References/ContentTemplates/AlarmList.md), [`Memo`](/CIC/References/ContentTemplates/Memo.md), [`MemoList`](/CIC/References/ContentTemplates/MemoList.md), [`Reminder`](/CIC/References/ContentTemplates/Reminder.md), [`ReminderList`](/CIC/References/ContentTemplates/ReminderList.md), [`Schedule`](/CIC/References/ContentTemplates/Schedule.md), [`ScheduleList`](/CIC/References/ContentTemplates/ScheduleList.md), [`Timer`](/CIC/References/ContentTemplates/Timer.md), [`TimerList`](/CIC/References/ContentTemplates/TimerList.md) 템플릿에 `token` 필드 추가

* CEK
  - [Custom extension 메시지](/CEK/References/CEK_API.md#CustomExtMessage) 중 요청 메시지에서 `context.System.device.displayType` 필드의 이름을 `context.System.device.display`로 바꾸고 하위 필드 구성을 변경

## 2017-10-30

* Clova developer console 문서 추가
  - [Clova developer console 개요](/DevConsole/ClovaDevConsole_Overview.md) 설명 추가
  - [Extension 등록하기](/DevConsole/Guides/CEK/Register_Extension.md) 가이드 추가
  - [Interaction 모델 정의하기](/DevConsole/Guides/CEK/Define_Interaction_Model.md) 가이드 추가
  - [Extension 배포하기](/DevConsole/Guides/CEK/Deploy_Extension.md) 가이드 추가

## 2017-10-23

* CIC
  - [Text](/CIC/References/ContentTemplates/Text.md) 템플릿에 `emotionCode` 필드와 `motionCode` 필드를 추가
  - [`Alerts.SetAlert`](/CIC/References/CICInterface/Alerts.md#SetAlert) 지시 메시지의 `assets[].url` 필드 변경
  - [Custom extension 메시지](/CEK/References/CEK_API.md#CustomExtMessage) 중 요청 메시지에 `context.System.device.displayType` 필드 추가
  - [`AudioPlayer.StreamRequested`](/CIC/References/CICInterface/AudioPlayer.md#StreamRequested) 이벤트 메시지의 예제 오류 수정

## 2017-10-16

* CIC
  - [`PlaybackController`](/CIC/References/CICInterface/PlaybackController.md) 네임스페이스에 [`Replay`](/CIC/References/CICInterface/PlaybackController.md#Replay) 지시 메시지 추가
  - `content` 필드를 [`Alert.AlertsState`](/CIC/References/Context_Objects.md#AlertsState) 문맥 정보의 [`AlertInfoObject`](/CIC/References/Context_Objects.md#AlertInfoObject)에서 제거
  - 알람 동기화에 대한 보충 설명을 [알람 동작 구조](/CIC/References/CICInterface/Alerts.md#AlertsWorkFlow) 절에 추가

* 공통
  - 일부 문서 이미지 수정 및 문서 오류 교정

## 2017-10-02

* CIC
  - [`Alerts`](/CIC/References/CICInterface/Alerts.md) 네임스페이스 및 알람 관련 인터페이스 추가
  - [`System`](/CIC/References/CICInterface/System.md) 네임스페이스 및 알람 관련 인터페이스 추가
  - [`SpeechRecognizer.ExpectSpeech`](/CIC/References/CICInterface/SpeechRecognizer.md#ExpectSpeech) 지시 메시지에 `expectContentType` 필드 추가
  - [`Device.DeviceState`](/CIC/References/Context_Objects.md#DeviceState)의 [`VolumeInfoObject`](/CIC/References/Context_Objects.md#VolumeInfoObject)에 warning 필드 추가
  - 개인 정보 관리 서비스(PIMS) 관련 템플릿 추가
    - [ActionTimer](/CIC/References/ContentTemplates/ActionTimer.md)
    - [ActionTimerList](/CIC/References/ContentTemplates/ActionTimerList.md)
    - [Alarm](/CIC/References/ContentTemplates/Alarm.md)
    - [AlarmList](/CIC/References/ContentTemplates/AlarmList.md)
    - [Memo](/CIC/References/ContentTemplates/Memo.md)
    - [MemoList](/CIC/References/ContentTemplates/MemoList.md)
    - [Reminder](/CIC/References/ContentTemplates/Reminder.md)
    - [ReminderList](/CIC/References/ContentTemplates/ReminderList.md)
    - [Schedule](/CIC/References/ContentTemplates/Schedule.md)
    - [ScheduleList](/CIC/References/ContentTemplates/ScheduleList.md)
    - [Timer](/CIC/References/ContentTemplates/Timer.md)
    - [TimerList](/CIC/References/ContentTemplates/TimerList.md)
  - [Popup 템플릿](/CIC/References/ContentTemplates/Popup.md) 일부 필드 수정
  - [ImageText](/CIC/References/ContentTemplates/ImageText.md) 템플릿의 일부 코드 예제 수정
  - [Clova access token 생성하기](/CIC/Guides/Interact_with_CIC.md#CreateClovaAccessToken)와 [Authorization code 요청](/CIC/References/Clova_Auth_API.md#RequestAuthorizationCode)에 서비스 이용 약관에 대한 내용 추가

## 2017-09-25

* CIC
  - [`PlaybackController`](/CIC/References/CICInterface/PlaybackController.md) API에 음악 재생 제어용 [`PlaybackController.NextCommandIssued`](/CIC/References/CICInterface/PlaybackController.md#NextCommandIssued) 이벤트 메시지와 [`PlaybackController.PreviousCommandIssued`](/CIC/References/CICInterface/PlaybackController.md#PreviousCommandIssued) 이벤트 메시지 추가
  - [`SpeechRecognizer.ExpectSpeech`](/CIC/References/CICInterface/SpeechRecognizer.md#ExpectSpeech) 지시 메시지에 `expectSpeechId` 필드를 [`SpeechRecognizer.Recognize`](/CIC/References/CICInterface/SpeechRecognizer.md#Recognize) 이벤트 메시지에 `speechId`와 `explicit` 필드를 각각 추가
  - [Popup 템플릿](/CIC/References/ContentTemplates/Popup.md) 추가

* CEK
  - Clova Home extension API에 ChargeConfirmation 외 33건의 [Control API](/CEK/References/ClovaHomeInterface/Control_Interfaces.md) 추가
  - Clova Home extension API [지원 기기](/CEK/References/ClovaHomeInterface/Shared_Objects.md#ApplianceInfoObject) 6종 추가 및 `location` 필드 추가

## 2017-09-18

* CIC
  - DeviceControl API에 [`DeviceControl.ExpectReportState`](/CIC/References/CICInterface/DeviceControl.md#ExpectReportState) 지시 메시지, [`DeviceControl.ReportState`](/CIC/References/CICInterface/DeviceControl.md#ReportState) 이벤트 메시지, [`DeviceControl.RequestStateSynchronization`](/CIC/References/CICInterface/DeviceControl.md#RequestStateSynchronization) 이벤트 메시지 추가
  - `DeviceControl.UpdateDeviceState` 지시 메시지를 [`DeviceControl.SynchronizeState`](/CIC/References/CICInterface/DeviceControl.md#SynchronizeState)로 이름 변경
  - [Text](/CIC/References/ContentTemplates/Text.md) 템플릿에 `item3` 필드 추가
  - [`AudioPlayer.Play`](/CIC/References/CICInterface/AudioPlayer.md#Play) 지시 메시지에 출처 정보 관련 `source` 필드 추가
  - [`AudioStreamInfoObject`](/CIC/References/CICInterface/AudioPlayer.md#AudioStreamInfoObject)에 `durationInMilliseconds` 필드 추가
  - Notifier 네임스페이스 및 [`ClearIndicator`](/CIC/References/CICInterface/Notifier.md#ClearIndicator), [`SetIndicator`](/CIC/References/CICInterface/Notifier.md#SetIndicator) 지시 메시지 추가
  - [대기 정보(Atmosphere) 템플릿](/CIC/References/ContentTemplates/Atmosphere.md) 추가
  - 라이선스 이슈에 따른 날씨 템플릿의 `bgClipURL` 필드 사용 불가 문구 추가

## 2017-09-11

* CIC
  - [`SpeechRecognizer.ExpectSpeech`](/CIC/References/CICInterface/SpeechRecognizer.md#ExpectSpeech) 지시 메시지에 `explicit` 필드 추가
  - [Content template](/CIC/References/Content_Templates.md)에 [공통 필드](/CIC/References/ContentTemplates/Common_Fields.md) 스펙 추가

## 2017-09-04

* CIC
  - [`Clova.Help`](/CIC/References/CICInterface/Clova.md#Help) 지시 메시지 추가
  - [`DeviceControl.LaunchApp`](/CIC/References/CICInterface/DeviceControl.md#LaunchApp) 지시 메시지 추가
  - `TextRecognizer` 네임스페이스 및 [`TextRecognizer.Recognize`](/CIC/References/CICInterface/TextRecognizer.md) 이벤트 메시지 추가
  - [CIC API](/CIC/References/CIC_API.md), [CEK API](/CEK/References/CEK_API.md)의 목차, 설명 재작성
  - CIC API 내용 업데이트: 요청/응답 헤더의 Status code 추가, REST API reference 문서 포맷 적용
  - 일부 문서 오류 수정

## 2017-08-28

* CIC
  - 셋톱박스용 TV 채널 정보 스펙과 전원 상태 정보 스펙을 [`Device.DeviceState`](/CIC/References/Context_Objects.md#DeviceState)와 [`DeviceControl`](/CIC/References/CICInterface/DeviceControl.md) API에 추가
  - [D`eviceControl`](/CIC/References/CICInterface/DeviceControl.md) API에서 `target`으로 사용되는 값 일부 추가 및 변경: `power`, `energysave`, `screenbrightness`
  - [`DeviceControl`](/CIC/References/CICInterface/DeviceControl.md) API의 `SetPoint`를 [`SetValue`](/CIC/References/CICInterface/DeviceControl.md#SetValue)로 이름 변경
  - [`ValueOutOfRangeError`](/CEK/References/ClovaHomeInterface/Error_Interfaces.md#ValueOutOfRangeError)를 Clova Home의 Error 인터페이스에 추가
  - [Clova 인증 API](/CIC/References/Clova_Auth_API.md) 내용 업데이트 - 요청/응답 헤더와 Status code 추가, REST API reference 문서 포맷 적용

## 2017-08-21

* CIC
  - [Access token 갱신](/CIC/Guides/Interact_with_CIC.md#ManageConnection)절 추가 및 /token API 내용 업데이트

## 2017-08-14

* CIC
  - [`DeviceControl`](/CIC/References/CICInterface/DeviceControl.md) API 추가
  - [`Device.DeviceState`](/CIC/References/Context_Objects.md) `payload` 필드 추가: `airplane`, `battery`, `bluetooth`, `brightness`, `flashLight`, `gps`, `powerSavingMode`, `soundMode`, `volume`, `wifi`
  - [대화 모델](/CIC/CIC_Overview.md#DialogModel) 설명 추가

* CEK
  - [Multi-turn 대화 수행하기](/CEK/Guides/Build_Custom_Extension.md#DoMultiturnDialog)절 추가 및 `sessionAttributes` 필드 설명 업데이트

## 2017-08-04

* CIC
  - [`Clova.Hello`](/CIC/References/CICInterface/Clova.md#Hello) 지시 메시지 추가
  - [`AudioPlayer.Play`](/CIC/References/CICInterface/AudioPlayer.md#Play) 지시 메시지의 `AudioItem` 객체에 `type` 필드 추가
  - [`AudioStreamInfoObject`](/CIC/References/CICInterface/AudioPlayer.md#AudioStreamInfoObject) 객체에 `urlPlayable` 필드 추가
  - [CIC 오류 메시지](/CIC/References/CIC_API.md#Error) 스펙 추가
  - [Multipart 메시지](/CIC/References/CIC_API.md#MultipartMessage) 내용 재작성

* CEK
  - Clova Home [지원 기기](/CEK/References/ClovaHomeInterface/Shared_Objects.md#ApplianceInfoObject) 추가: 공기청정기, 가습기, 셋톱박스, 난방기기
  - Clova Home [지원 기기](/CEK/References/ClovaHomeInterface/Shared_Objects.md#ApplianceInfoObject) 제외: 도어락

## 2017-07-28

* CIC
  - [`AudioPlayer`](/CIC/References/CICInterface/AudioPlayer.md)의 `PlayNext`, `Stop` 제거 ([`PlaybackController`](/CIC/References/CICInterface/PlaybackController.md)에 병합)
  - [`PlaybackController`](/CIC/References/CICInterface/PlaybackController.md)의 메시지 이름 변경(`Mute`, `Next`, `Pause`, `Previous`, `Resume`, `Stop`, `Unmute`, `VolumeDown`, `VolumeUp`
  - 길찾기 템플릿 추가:
    - [CarRoute](/CIC/References/ContentTemplates/CarRoute.md)
    - [TransportationRoute](/CIC/References/ContentTemplates/TransportationRoute.md)
  - 날씨 템플릿 추가:
    - [Humidity](/CIC/References/ContentTemplates/Humidity.md)
    - [TodayWeather](/CIC/References/ContentTemplates/TodayWeather.md)
    - [TomorrowWeather](/CIC/References/ContentTemplates/TomorrowWeather.md)
    - [WeeklyWeather](/CIC/References/ContentTemplates/WeeklyWeather.md)
    - [WindSpeed](/CIC/References/ContentTemplates/WindSpeed.md)

## 2017-07-14

* CIC
  - [`AudioStreamInfoObject`](/CIC/References/CICInterface/AudioPlayer.md#AudioStreamInfoObject) 객체 `beginAtInMilliseconds` 필드 추가

## 2017-07-07

* CEK
  - [Custom extension 응답 메시지](/CEK/References/CEK_API.md#CustomExtResponseMessage)의 [`outputSpeech`](/CEK/References/CEK_API.md#CustomExtResponseMessage) 객체 구성 변경
  - CEK 메시지 포맷 파트의 목차 업데이트
  - 이미지 업데이트

* 공통
  - [용어집 추가](/Terms.md)

## 2017-06-19

* CEK 문서 파트 추가
* CIC 문서 파트 추가
