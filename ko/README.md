# 문서 정보
이 문서는 Clova가 제공하는 CIC와 CEK 플랫폼에 대한 개발 가이드 및 API 레퍼런스를 제공합니다. 대상 독자는 CIC를 사용하여 Clova 서비스와 연동되는 전자 기기, 앱을 개발하려는 클라이언트 개발자와 CEK 플랫폼을 사용하여 온라인 콘텐츠를 Clova를 통해 제공하려는 Extension 개발자입니다.

<div class="note">
  <p><strong>Note!</strong></p>
  <p>Clova는 현재 개발이 계속 진행되고 있습니다. 따라서, 이 문서의 내용은 언제든지 변경될 수 있습니다.</p>
</div>

## 연락처
문서와 관련하여 궁금한 사항은 지정된 Clova 협업 담당자에게 문의합니다.

## 문서 이력
| 버전 | 배포 일자         | 이력 사항                   | 작성자     | 승인자    |
|-----|----------------|---------------------------|----------|----------|
| v0.7 | 2017-07-28    | <ul><li>[CIC] <a href="/CIC/References/APIs/AudioPlayer.html">AudioPlayer</a>의 PlayNext, Stop 제거 (<a href="/CIC/References/APIs/PlaybackController.html">PlaybackController</a>에 병합)</li><li>[CIC]  <a href="/CIC/References/APIs/PlaybackController.html">PlaybackController</a>의 메시지 이름 변경(Mute, Next, Pause, Previous, Resume, Stop, Unmute, VolumeDown, VolumeUp </li><li>[CIC] 길찾기 템플릿 추가 : <a href="/CIC/References/ContentTemplates/CarRoute.html">CarRoute</a>, <a href="/CIC/References/ContentTemplates/TransportationRoute.html">TransportationRoute</a></li><li>[CIC] 날씨 템플릿 추가 : <a href="/CIC/References/ContentTemplates/Humidity.html">Humidity</a>, <a href="/CIC/References/ContentTemplates/TodayWeather.html">TodayWeather</a>, <a href="/CIC/References/ContentTemplates/TomorrowWeather.html">TomorrowWeather</a>, <a href="/CIC/References/ContentTemplates/WeeklyWeather.html">WeeklyWeather</a>, <a href="/CIC/References/ContentTemplates/WindSpeed.html">WindSpeed</a></li></ul> | <ul><li>pd1팀 김현준</li><li>pf1팀 권세영</li><li>pf1팀 강정일</li></ul> | <ul><li>pf1팀 정민영</li><li>pf1팀 권세영</li></ul> |
| v0.6 | 2017-07-14    | [CIC] <a href="/CIC/References/APIs/AudioPlayer.html#AudioStreamObject">AudioStreamObject</a> 객체 beginAtInMilliseconds 필드 내용 추가 | <ul><li>pf1팀 김현준</li><li>pf1팀 강정일</li></ul> | pf1팀 정민영 |
| v0.5 | 2017-07-07 | <ul><li>[CEK] <a href="/CEK/References/Custom_Extension_Message_Format.html#ResponseMessage">Custom extension 응답 메시지</a>의 <a href="/CEK/References/Custom_Extension_Message_Format.html#SpeechObject">outputSpeech</a> 객체 구성 업데이트 반영</li><li>[공통] <a href="/Terms.html">용어집 추가</a></li><li>CEK 메시지 포맷 파트의 목차 업데이트</li></ul> | <ul><li>pf1팀 임성순</li><li>pf1팀 강정일</li></ul> | <ul><li>pf1팀 정민영</li><li>pf1팀 권세영</li></ul> |
| v0.4 | 2017-07-03 | <ul><li>[CEK] CEK 문서 이미지 내용 업데이트</li><li>[공통] 문서 리뷰 결과 반영</li></ul> | <ul><li>pf1팀 임성순</li><li>pf1팀 강정일</li></ul> | <ul><li>pf1팀 정민영</li><li>pf1팀 권세영</li></ul> |
| v0.3 | 2017-06-19 | <ul><li>[CEK] CEK 문서 파트 작성</li><li>[CIC] <a href="/CIC/Guides/Interact_with_CIC.html#ManageConnection">연결 관리하기</a> 업데이트 (HTTP Ping 프레임을 사용할 수 없을 경우)</li></ul> | <ul><li>pf1팀 강윤신</li><li>pf1팀 박재현</li><li>pf1팀 김현준</li><li>pf1팀 임성순</li><li>pf1팀 강정일</li></ul> | <ul><li>pf1팀 정민영</li><li>pf1팀 권세영</li></ul> |
| v0.2 | 2017-06-08 | [CIC] [CIC 연동하기](/CIC/Guides/Interact_with_CIC.html)에 [연결 관리하기](/CIC/Guides/Interact_with_CIC.md#ManageConnection) 추가 (HTTP Ping) | <ul><li>pf1팀 김현준</li><li>pf1팀 강정일</li></ul> | pf1팀 정민영 |
| v0.1 | 2017-05-29 | [CIC] CIC 문서 파트 작성 | <ul><li>pf1팀 강윤신</li><li>pf1팀 박진영</li><li>pf1팀 김현준</li><li>pf1팀 임성순</li><li>pf1팀 강정일</li></ul> | <ul><li>pf1팀 정민영</li><li>pf1팀 권세영</li></ul> |
