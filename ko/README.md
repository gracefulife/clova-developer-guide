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
  <tbody style="vertical-align: top;">
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
