# 릴리즈 노트

이 페이지는 Clova 플랫폼과 문서의 릴리즈 노트를 제공합니다.

## 2017-11-06

## 플랫폼 변경 사항

* CIC
  - [`SpeechRecognizer.KeepRecording`](/CIC/References/CICInterface/SpeechRecognizer.md#KeepRecording) 지시 메시지 추가
  - 클라이언트의 디스플레이 장치 정보를 공유하기 위한 [`Device.Display`](/CIC/References/Context_Objects.md#Display) 맥락 정보 추가
  - [`ActionTimer`](/CIC/References/ContentTemplates/ActionTimer.html), [`ActionTimerList`](/CIC/References/ContentTemplates/ActionTimerList.html), [`Alarm`](/CIC/References/ContentTemplates/Alarm.html), [`AlarmList`](/CIC/References/ContentTemplates/AlarmList.html), [`Memo`](/CIC/References/ContentTemplates/Memo.html), [`MemoList`](/CIC/References/ContentTemplates/MemoList.html), [`Reminder`](/CIC/References/ContentTemplates/Reminder.html), [`ReminderList`](/CIC/References/ContentTemplates/ReminderList.html), [`Schedule`](/CIC/References/ContentTemplates/Schedule.html), [`ScheduleList`](/CIC/References/ContentTemplates/ScheduleList.html), [`Timer`](/CIC/References/ContentTemplates/Timer.html), [`TimerList`](/CIC/References/ContentTemplates/TimerList.html) 템플릿에 `token` 필드 추가

* CEK
  - [Custom extension 메시지](/CEK/References/CEK_API.html#CustomExtMessage) 중 요청 메시지에서 `context.System.device.displayType` 필드의 이름을 `context.System.device.display`로 바꾸고 하위 필드 구성을 변경

## 2017-10-30

### 문서 변경 사항

* Clova developer console 문서 추가
  - [Clova developer console 개요](/DevConsole/ClovaDevConsole_Overview.md) 설명 추가
  - [Extension 등록하기](/DevConsole/Guides/CEK/Register_Extension.md) 가이드 추가
  - [Interaction 모델 정의하기](/DevConsole/Guides/CEK/Define_Interaction_Model.md) 가이드 추가
  - [Extension 배포하기](/DevConsole/Guides/CEK/Deploy_Extension.md) 가이드 추가

## 2017-10-23

### 플랫폼 변경 사항

* CIC
  - [Text](/CIC/References/ContentTemplates/Text.md) 템플릿에 `emotionCode` 필드와 `motionCode` 필드를 추가
  - [`Alerts.SetAlert`](/CIC/References/CICInterface/Alerts.md#SetAlert) 지시 메시지의 `assets[].url` 필드 변경
  - [Custom extension 메시지](/CEK/References/CEK_API.md#CustomExtMessage) 중 요청 메시지에 `context.System.device.displayType` 필드 추가

### 문서 변경 사항

* CIC
  - [`AudioPlayer.StreamRequested`](/CIC/References/CICInterface/AudioPlayer.md#StreamRequested) 이벤트 메시지의 예제 오류 수정

## 2017-10-16

### 플랫폼 변경 사항

* CIC
  - [`PlaybackController`](/CIC/References/CICInterface/PlaybackController.md) 네임스페이스에 [`Replay`](/CIC/References/CICInterface/PlaybackController.md#Replay) 지시 메시지 추가
  - `content` 필드를 [`Alert.AlertsState`](/CIC/References/Context_Objects.md#AlertsState) 문맥 정보의 [`AlertInfoObject`](/CIC/References/Context_Objects.md#AlertInfoObject)에서 제거

### 문서 변경 사항

* CIC
  - 알람 동기화에 대한 보충 설명을 [알람 동작 구조](/CIC/References/CICInterface/Alerts.md#AlertsWorkFlow) 절에 추가
* 공통
  - 일부 문서 이미지 수정 및 문서 오류 교정

## 2017-10-02

### 플랫폼 변경 사항

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

### 문서 변경 사항

* CIC
  - [ImageText](/CIC/References/ContentTemplates/ImageText.md) 템플릿의 일부 코드 예제 수정
  - [Clova access token 생성하기](/CIC/Guides/Interact_with_CIC.md#CreateClovaAccessToken)와 [Authorization code 요청](/CIC/References/Clova_Auth_API.md#RequestAuthorizationCode)에 서비스 이용 약관에 대한 내용 추가

## 2017-09-25

### 플랫폼 변경 사항

* CIC
  - [`PlaybackController`](/CIC/References/CICInterface/PlaybackController.md) API에 음악 재생 제어용 [`PlaybackController.NextCommandIssued`](/CIC/References/CICInterface/PlaybackController.md#NextCommandIssued) 이벤트 메시지와 [`PlaybackController.PreviousCommandIssued`](/CIC/References/CICInterface/PlaybackController.md#PreviousCommandIssued) 이벤트 메시지 추가
  - [`SpeechRecognizer.ExpectSpeech`](/CIC/References/CICInterface/SpeechRecognizer.md#ExpectSpeech) 지시 메시지에 `expectSpeechId` 필드를 [`SpeechRecognizer.Recognize`](/CIC/References/CICInterface/SpeechRecognizer.md#Recognize) 이벤트 메시지에 `speechId`와 `explicit` 필드를 각각 추가
  - [Popup 템플릿](/CIC/References/ContentTemplates/Popup.md) 추가
* CEK
  - Clova Home API에 ChargeConfirmation 외 33건의 [Control API](/CEK/References/ClovaHomeInterface/Control_Interfaces.md) 추가
  - Clova Home API [지원 기기](/CEK/References/ClovaHomeInterface/Shared_Objects.md#ApplianceInfoObject) 6종 추가 및 `location` 필드 추가

## 2017-09-18

### 플랫폼 변경 사항

* CIC
  - DeviceControl API에 [`DeviceControl.ExpectReportState`](/CIC/References/CICInterface/DeviceControl.md#ExpectReportState) 지시 메시지, [`DeviceControl.ReportState`](/CIC/References/CICInterface/DeviceControl.md#ReportState) 이벤트 메시지, [`DeviceControl.RequestStateSynchronization`](/CIC/References/CICInterface/DeviceControl.md#RequestStateSynchronization) 이벤트 메시지 추가
  - `DeviceControl.UpdateDeviceState` 지시 메시지를 [`DeviceControl.SynchronizeState`](/CIC/References/CICInterface/DeviceControl.md#SynchronizeState)로 이름 변경
  - [Text](/CIC/References/ContentTemplates/Text.md) 템플릿에 `item3` 필드 추가
  - [`AudioPlayer.Play`](/CIC/References/CICInterface/AudioPlayer.md#Play) 지시 메시지에 출처 정보 관련 `source` 필드 추가
  - [`AudioStreamInfoObject`](/CIC/References/CICInterface/AudioPlayer.md#AudioStreamInfoObject)에 `durationInMilliseconds` 필드 추가
  - Notifier 네임스페이스 및 [`ClearIndicator`](/CIC/References/CICInterface/Notifier.md#ClearIndicator), [`SetIndicator`](/CIC/References/CICInterface/Notifier.md#SetIndicator) 지시 메시지 추가
  - [대기 정보(Atmosphere) 템플릿](/CIC/References/ContentTemplates/Atmosphere.md) 추가

### 문서 변경 사항
* CIC
  - 라이선스 이슈에 따른 날씨 템플릿의 `bgClipURL` 필드 사용 불가 문구 추가

## 2017-09-11

### 플랫폼 변경 사항

* CIC
  - [`SpeechRecognizer.ExpectSpeech`](/CIC/References/CICInterface/SpeechRecognizer.md#ExpectSpeech) 지시 메시지에 `explicit` 필드 추가
  - [Content template](/CIC/References/Content_Templates.md)에 [공통 필드](/CIC/References/ContentTemplates/Common_Fields.md) 스펙 추가

## 2017-09-04

### 플랫폼 변경 사항

* CIC
  - [`Clova.Help`](/CIC/References/CICInterface/Clova.md#Help) 지시 메시지 추가
  - [`DeviceControl.LaunchApp`](/CIC/References/CICInterface/DeviceControl.md#LaunchApp) 지시 메시지 추가
  - `TextRecognizer` 네임스페이스 및 [`TextRecognizer.Recognize`](/CIC/References/CICInterface/TextRecognizer.md) 이벤트 메시지 추가

### 문서 변경 사항

* [CIC API](/CIC/References/CIC_API.md), [CEK API](/CEK/References/CEK_API.md)의 목차, 설명 재작성
* CIC API 내용 업데이트: 요청/응답 헤더의 Status code 추가, REST API reference 문서 포맷 적용
* 일부 문서 오류 수정

## 2017-08-28

### 플랫폼 변경 사항

* CIC
  - 셋톱박스용 TV 채널 정보 스펙과 전원 상태 정보 스펙을 [`Device.DeviceState`](/CIC/References/Context_Objects.md#DeviceState)와 [`DeviceControl`](/CIC/References/CICInterface/DeviceControl.md) API에 추가
  - [D`eviceControl`](/CIC/References/CICInterface/DeviceControl.md) API에서 `target`으로 사용되는 값 일부 추가 및 변경: `power`, `energysave`, `screenbrightness`
  - [`DeviceControl`](/CIC/References/CICInterface/DeviceControl.md) API의 `SetPoint`를 [`SetValue`](/CIC/References/CICInterface/DeviceControl.md#SetValue)로 이름 변경
  - [`ValueOutOfRangeError`](/CEK/References/ClovaHomeInterface/Error_Interfaces.md#ValueOutOfRangeError)를 Clova Home의 Error 인터페이스에 추가

### 문서 변경 사항

* CIC
  - [Clova 인증 API](/CIC/References/Clova_Auth_API.md) 내용 업데이트 - 요청/응답 헤더와 Status code 추가, REST API reference 문서 포맷 적용

## 2017-08-21

### 문서 변경 사항

* CIC
  - [Access token 갱신](/CIC/Guides/Interact_with_CIC.md#ManageConnection)절 추가 및 /token API 내용 업데이트

## 2017-08-14

### 플랫폼 변경 사항

* CIC
  - [`DeviceControl`](/CIC/References/CICInterface/DeviceControl.md) API 추가
  - [`Device.DeviceState`](/CIC/References/Context_Objects.md) `payload` 필드 추가: `airplane`, `battery`, `bluetooth`, `brightness`, `flashLight`, `gps`, `powerSavingMode`, `soundMode`, `volume`, `wifi`

### 문서 변경 사항

* CIC
  - [대화 모델](/CIC/CIC_Overview.md#DialogModel) 설명 추가

* CEK
  - [Multi-turn 대화 수행하기](/CEK/Guides/Build_Custom_Extension.md#DoMultiturnDialog)절 추가 및 `sessionAttributes` 필드 설명 업데이트

## 2017-08-04

### 플랫폼 변경 사항

* CIC
  - [`Clova.Hello`](/CIC/References/CICInterface/Clova.md#Hello) 지시 메시지 추가
  - [`AudioPlayer.Play`](/CIC/References/CICInterface/AudioPlayer.md#Play) 지시 메시지의 `AudioItem` 객체에 `type` 필드 추가
  - [`AudioStreamInfoObject`](/CIC/References/CICInterface/AudioPlayer.md#AudioStreamInfoObject) 객체에 `urlPlayable` 필드 추가
  - [CIC 오류 메시지](/CIC/References/CIC_API.md#Error) 스펙 추가

* CEK
  - Clova Home [지원 기기](/CEK/References/ClovaHomeInterface/Shared_Objects.md#ApplianceInfoObject) 추가: 공기청정기, 가습기, 셋톱박스, 난방기기
  - Clova Home [지원 기기](/CEK/References/ClovaHomeInterface/Shared_Objects.md#ApplianceInfoObject) 제외: 도어락

### 문서 변경 사항

* CIC
  - [Multipart 메시지](/CIC/References/CIC_API.md#MultipartMessage) 내용 재작성

## 2017-07-28

### 플랫폼 변경 사항

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

### 플랫폼 변경 사항

* CIC
  - [`AudioStreamInfoObject`](/CIC/References/CICInterface/AudioPlayer.md#AudioStreamInfoObject) 객체 `beginAtInMilliseconds` 필드 추가

## 2017-07-07

### 플랫폼 변경 사항

* CEK
  - [Custom extension 응답 메시지](/CEK/References/CEK_API.md#CustomExtResponseMessage)의 [`outputSpeech`](/CEK/References/CEK_API.md#CustomExtResponseMessage) 객체 구성 변경

### 문서 변경 사항

* CEK
  - CEK 메시지 포맷 파트의 목차 업데이트
  - 이미지 업데이트

* 공통
  - [용어집 추가](/Terms.md)

## 2017-06-19

* CEK 문서 파트 추가
* CIC 문서 파트 추가
