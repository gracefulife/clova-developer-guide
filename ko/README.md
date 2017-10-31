# 시작하기 전에

[Clova](http://clova.ai)는 {{ book.TargetServiceForClientAuth }}가 개발 및 서비스하고 있는 인공지능 플랫폼입니다. Clova 사용자의 음성이나 이미지를 인식하고 이를 분석하여 사용자가 원하는 정보나 서비스를 제공합니다. Clova 플랫폼을 이용하는 3rd party 개발자는 다음과 두 범주로 나뉠 수 있습니다.

* Clova 인공 지능 서비스를 제공하는 전자 기기, 앱을 개발하려는 클라이언트 개발자
* Clova를 통해 보유하고 있는 온라인 콘텐츠나 서비스를 제공하려는 확장 기능(Extension) 개발자

위와 같이 나뉜 클라이언트 개발자와 extension 개발자를 위해 Clova는 Clova Interface Connection(CIC), Clova Extension Kit(CEK) 그리고 Clova developer console라는 것을 제공하고 있습니다. 각 개발자는 필요에 따라 다음과 같이 Clova 플랫폼이 제공하는 문서를 참조하면 됩니다.

<table>
  <thead>
    <tr>
      <th width="50%">클라이언트 개발자</th>
      <th width="50%">Extension 개발자</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>
        <ul>
          <li>개념 설명 및 가이드</li>
          <ul>
            <li><a href="/CIC/CIC_Overview.html">CIC 개요</a></li>
            <li>하드웨어 설계 가이드라인(작성 예정)</li>
            <li><a href="/CIC/Guides/Interact_with_CIC.html">CIC 연동하기</a></li>
            <li>클라이언트 등록하기(작성 예정)</li>
          </ul>
          <li>레퍼런스</li>
          <ul>
            <li><a href="/CIC/References/CIC_API.html">CIC API 레퍼런스</a></li>
            <li><a href="/CIC/References/CIC_API.html#CICInterface">CIC 메시지 인터페이스</a></li>
            <li><a href="/CIC/References/Content_Templates.html">Content template</a></li>
            <li><a href="/CIC/References/Clova_Auth_API.html">CIC 인증 API 레퍼런스</a></li>
          </ul>
          <li><a href="/Release_Notes.html">릴리즈 노트</a></li>
        </ul>
      </td>
      <td>
        <ul>
          <li>개념 설명 및 가이드</li>
          <ul>
            <li><a href="/CEK/CEK_Overview.html">CEK 개요</a></li>
            <li>Extension 설계 가이드라인(작성 예정)</li>
            <li><a href="/DevConsole/Guides/CEK/Register_Extension.md">Extension 등록하기</a></li>
            <li><a href="/DevConsole/Guides/CEK/Define_Interaction_Model.md">Interaction 모델 정의하기</a></li>
            <li><a href="/CEK/Guides/Build_Custom_Extension.html">Custom extension 만들기</a></li>
            <li><a href="/CEK/Guides/Build_Clova_Home_Extension.html">Clova Home extension 만들기</a></li>
            <li><a href="/CEK/Guides/LinkUserAccount.md">사용자 계정 연결하기</a></li>
            <li><a href="/DevConsole/Guides/CEK/Deploy_Extension.html">Extension 배포하기</a></li>
          </ul>
          <li>레퍼런스</li>
          <ul>
            <li><a href="/CEK/References/CEK_API.html#CustomExtMessage">Custom extension 메시지</a></li>
            <li><a href="/CEK/References/CEK_API.md#ClovaHomeExtMessage">Clova Home extension 메시지</a></li>
          </ul>
          <li><a href="/Release_Notes.html">릴리즈 노트</a></li>
        </ul>
      </td>
    </tr>
  </tbody>
</table>

<div class="note">
  <p><strong>Note!</strong></p>
  <p>Clova 플랫폼은 계속 확장/개선되고 있기 때문에 문서의 구조와 내용이 수시로 추가 및 업데이트될 수 있습니다.</p>
</div>
