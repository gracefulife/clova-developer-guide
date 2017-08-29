# 문서 정보
이 문서는 Clova가 제공하는 CIC와 CEK 플랫폼에 대한 개발 가이드 및 API 레퍼런스를 제공합니다. 대상 독자는 CIC를 사용하여 Clova 서비스와 연동되는 전자 기기, 앱을 개발하려는 클라이언트 개발자와 CEK를 사용하여 온라인 콘텐츠 및 서비스를 제공하려는 Extension 개발자입니다.

<div class="note">
  <p><strong>Note!</strong></p>
  <p>Clova는 현재 개발이 계속 진행되고 있습니다. 따라서, 이 문서의 내용은 언제든지 변경될 수 있습니다.</p>
</div>

## 연락처
문서와 관련하여 궁금한 사항은 지정된 Clova 협업 담당자에게 문의합니다.

## 문서 이력

현재 이 문서의 버전은 v1.1 이며, 변경 이력은 다음과 같습니다.

| 버전 | 배포 일자 | 이력 사항                              |
|-----|---------|-------------------------------------|
| v1.1  | 2017-08-28   | <ul><li>[CIC] 셋톱박스용 TV 채널 정보 스펙과 전원 상태 정보 스펙을 <a href="/CIC/References/Context_Objects.html#DeviceState">Device.DeviceState</a>와 <a href="/CIC/References/APIs/DeviceControl.html">DeviceControl API</a>에 추가</li><li>[CIC] <a href="/CIC/References/APIs/DeviceControl.html">DeviceControl API</a>에서 target으로 사용되는 값 일부 추가 및 변경 : power, energysave, screenbrightness</li><li>[CIC] <a href="/CIC/References/APIs/DeviceControl.html">DeviceControl API</a>의 SetPoint를 <a href="/CIC/References/APIs/DeviceControl.html#SetValue">SetValue</a>로 이름 변경</li><li>[CIC] <a href="/CIC/References/Clova_Auth_API.html">Clova 인증 API</a> 내용 업데이트 - 요청/응답 헤더와 Status code 추가, REST API reference 문서 포맷 적용</li><li>[CEK] <a href="/CEK/References/Clova_Home_API.html#ValueOutOfRangeError">ValueOutOfRangeError</a>를 Clova Home API에 추가</li></ul> |
| v1.0  | 2017-08-21   | [CIC] <a href="/CIC/Guides/Interact_with_CIC.html#ManageConnection">Access token 갱신</a>절 추가 및 <a href="CIC/References/Clova_Auth_API.html#token">/token</a> 내용 업데이트 |
| v0.9  | 2017-08-14   | <ul><li>[CIC] <a href="/CIC/CIC_Overview.html#DialogModel">대화 모델</a> 설명 추가</li><li>[CIC] <a href="/CIC/References/APIs/DeviceControl.html">DeviceControl</a> API 추가</li><li>[CIC] <a href="/CIC/References/Context_Objects.html">Device.DeviceState</a> payload 필드 추가 : airplane, battery, bluetooth, brightness, flashLight, gps, powerSavingMode, soundMode, volume, wifi</li><li>[CEK] <a href="/CEK/Guides/Build_Custom_Extension.html#DoMultiturnDialog">Multi-turn 대화 수행하기</a>절 추가 및 sessionAttributes 필드 설명 업데이트</li></ul> |
| v0.8 | 2017-08-04 | <ul><li>[CIC] <a href="/CIC/References/APIs/Clova.html#Hello">Clova.Hello</a> 지시 메시지 추가</li><li>[CIC] <a href="/CIC/References/APIs/AudioPlayer.html#Play">AudioPlayer.Play</a> 지시 메시지의 AudioItem 객체에 type 필드 추가</li><li>[CIC] <a href="/CIC/References/APIs/AudioPlayer.html#AudioStreamObject">AudioStreamObject</a> 객체에 urlPlayable 필드 추가</li><li>[CIC] <a href="/CIC/References/CIC_Message_Format.html#Error">CIC 오류 메시지</a> 스펙 추가</li><li>[CIC] <a href="/CIC/References/HTTP2_Message_Format.html#Request">Multipart 메시지</a> 내용 재작성</li><li>[CEK] Clova Home <a href="/CEK/References/Clova_Home_API.html#ApplianceObject">지원 기기</a> 추가 : 공기청정기, 가습기, 셋톱박스, 난방기기</li><li>[CEK] Clova Home <a href="/CEK/References/Clova_Home_API.html#ApplianceObject">지원 기기</a> 제외 : 도어락</li></ul>  |
| v0.7 | 2017-07-28 | <ul><li>[CIC] <a href="/CIC/References/APIs/AudioPlayer.html">AudioPlayer</a>의 PlayNext, Stop 제거 (<a href="/CIC/References/APIs/PlaybackController.html">PlaybackController</a>에 병합)</li><li>[CIC]  <a href="/CIC/References/APIs/PlaybackController.html">PlaybackController</a>의 메시지 이름 변경(Mute, Next, Pause, Previous, Resume, Stop, Unmute, VolumeDown, VolumeUp </li><li>[CIC] 길찾기 템플릿 추가 : <a href="/CIC/References/ContentTemplates/CarRoute.html">CarRoute</a>, <a href="/CIC/References/ContentTemplates/TransportationRoute.html">TransportationRoute</a></li><li>[CIC] 날씨 템플릿 추가 : <a href="/CIC/References/ContentTemplates/Humidity.html">Humidity</a>, <a href="/CIC/References/ContentTemplates/TodayWeather.html">TodayWeather</a>, <a href="/CIC/References/ContentTemplates/TomorrowWeather.html">TomorrowWeather</a>, <a href="/CIC/References/ContentTemplates/WeeklyWeather.html">WeeklyWeather</a>, <a href="/CIC/References/ContentTemplates/WindSpeed.html">WindSpeed</a></li></ul> |
| v0.6 | 2017-07-14 | [CIC] <a href="/CIC/References/APIs/AudioPlayer.html#AudioStreamObject">AudioStreamObject</a> 객체 beginAtInMilliseconds 필드 내용 추가 |
| v0.5 | 2017-07-07 | <ul><li>[CEK] <a href="/CEK/References/Custom_Extension_Message_Format.html#ResponseMessage">Custom extension 응답 메시지</a>의 <a href="/CEK/References/Custom_Extension_Message_Format.html#SpeechObject">outputSpeech</a> 객체 구성 업데이트 반영</li><li>[공통] <a href="/Terms.html">용어집 추가</a></li><li>CEK 메시지 포맷 파트의 목차 업데이트</li></ul> |
| v0.4 | 2017-07-03 | <ul><li>[CEK] CEK 문서 이미지 내용 업데이트</li><li>[공통] 문서 리뷰 결과 반영</li></ul> |
| v0.3 | 2017-06-19 | <ul><li>[CEK] CEK 문서 파트 작성</li><li>[CIC] <a href="/CIC/Guides/Interact_with_CIC.html#ManageConnection">연결 관리하기</a> 업데이트 (HTTP Ping 프레임을 사용할 수 없을 경우)</li></ul> |
| v0.2 | 2017-06-08 | [CIC] [CIC 연동하기](/CIC/Guides/Interact_with_CIC.html)에 [연결 관리하기](/CIC/Guides/Interact_with_CIC.md#ManageConnection) 추가 (HTTP Ping) |
| v0.1 | 2017-05-29 | [CIC] CIC 문서 파트 작성 |
