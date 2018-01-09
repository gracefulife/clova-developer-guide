# Extension 등록하기
[Custom extension](/CEK/Guides/Build_Custom_Extension.md) 또는 [Clova Home extension](/CEK/Guides/Build_Clova_Home_Extension.md)을 개발 중이거나 개발한 경우 이를 Clova developer console에 등록해야 합니다. CEK 메뉴 페이지에서 페이지 하단에 있는 **새로운 익스텐션 만들기** 버튼을 클릭하면 신규 extension을 등록할 수 있습니다.

![](/DevConsole/Resources/Images/DevConsole-First_Look_of_Extension_List.png)

Extension을 등록할 때 일반적으로 다음 항목을 순차적으로 수행해야 합니다.

1. [이용 약관 및 개인 정보 수집 동의](#AgreeTermsOfUse)
2. [Extension 기본 정보 입력](#InputExtensionInfo)
3. [서버 연동 설정](#SetServerConnection)
  * [계정 연결 설정](#SetAccountLinking)

## 이용 약관 및 개인 정보 수집 동의 {#AgreeTermsOfUse}

Extension을 등록하기 전에 우선 CEK API 서비스 이용 약관과 개인 정보 수집에 동의해야 합니다. 이용 약관 및 개인 정보 수집에 대한 내용 최초 한 번만 표시되며 동의한 이후에는 나타나지 않습니다.

![](/DevConsole/Resources/Images/DevConsole-Agree_Terms_of_Use_and_Collecting_Personal_Info.png)

## Extension 기본 정보 입력 {#InputExtensionInfo}

Extension을 등록하는 과정에서 가장 먼저 할 일은 등록할 extension의 기본 정보를 입력하는 것입니다. Extension의 기본 정보는 Clova developer console에 extension을 생성하기 위한 필수이자 최소 정보입니다. Extension의 기본 정보를 입력하고 나면 CEK 메뉴에서 생성한 extension을 언제든지 접근 또는 수정할 수 있게 됩니다.

다음 절차에 따라 extension을 등록합니다.

![](/DevConsole/Resources/Images/DevConsole-Create_New_Extension.png)

<ol>
  <li><strong>타입</strong> 항목에서 등록할 extension의 타입을 선택합니다. Extension 타입을 선택하면 그에 해당하는 입력 필드가 추가로 나타납니다.</li>
  <li><strong>사용 언어</strong> 항목에서 extension에서 사용할 언어를 선택합니다. 현재 <strong>한국어</strong>만 지원하고 있습니다.</li>
  <li>Extension의 ID, 이름, 호출 이름에 해당하는 정보를 다음 항목에 입력합니다.
    <ol>
      <li><strong>익스텐션 아이디</strong>: Extension의 고유 ID입니다. Reversed FQDN 형식으로 입력합니다. (예: com.yourdomain.extension.pizzabot)</li>
      <li><strong>이름</strong>: Extension의 이름입니다. 추후 Clova extension 스토어에 노출됩니다.</li>
      <li><strong>호출 이름</strong>: 사용자가 extension을 호출할 때 부르는 이름입니다. 일반적으로 보유하고 있는 서비스, 회사 또는 조직의 이름이 될 수 있으나 사용자의 편의 등을 위해 간결하고 특색있는 단어를 지정하는 것이 좋습니다. 범용적인 단어나 타사의 이름이나 서비스에 해당하는 용어는 사용할 수 없습니다. <strong>호출 이름</strong>은 extension 심사 시 검수받게 됩니다.</li>
      <li><strong>제작사</strong>: Extension의 제작 주체(회사나 개인)의 이름 또는 별칭을 입력합니다. 추후 Clova extension 스토어에 노출되며, extension 승인 과정에서 심사를 받게 됩니다.</li>
    </ol>
  </li>
  <li>(Extension이 <a href="/CIC/References/CICInterface/AudioPlayer.html">AudioPlayer</a> 지시 메시지를 이용할 경우)<strong>오디오 플레이어 사용</strong> 항목을 <strong>네</strong>로 선택합니다. Extension이 음악 스트리밍 서비스를 제공할 때 사용됩니다.</li>
  <li><strong>서비스 담당자 정보</strong> 항목에 연락 가능한 이메일 주소를 입력합니다.</li>
  <li><strong>테스트 아이디</strong> 항목에 개발 중인 extension을 테스트할 때 이용할 {{ book.OrientedService }} 계정을 입력하면 됩니다. 당장 입력하지 않아도 되며 추후 <a href="/DevConsole/Guides/CEK/Test_Extension.html">extension을 테스트</a>해야 할 때 이 필드에 값을 입력할 수 있습니다.</li>
  <li>Extension 기본 정보를 모두 입력한 후 <strong>만들기</strong> 버튼을 클릭합니다.</li>
</ol>

Extension 기본 정보 입력이 끝나면 생성된 Extension의 정보를 수정하는 화면으로 전환됩니다. 이때부터 페이지 하단에 있는 **저장** 버튼을 클릭하여 중간 내용을 언제든지 저장할 수 있으며, 다음과 같이 CEK 메뉴에서 등록된 Extension 목록을 확인할 수 있습니다.

![](/DevConsole/Resources/Images/DevConsole-Extension_list_after_Creation.png)

## 서버 연동 설정 {#SetServerConnection}

Extension은 CEK와 HTTPS 통신을 수행하게 되니다. 이때, CEK는 Extension쪽으로 HTTP 요청를 보내고, Extension은 HTTP 응답을 CEK에게 보냅니다. CEK가 extension으로 HTTP 요청을 보내려면 Clova developer console에서 서버 연동 설정을 수행해야 합니다. [Extension 기본 정보를 입력](#InputExtensionInfo)한 후 생성된 extension에 대해 서버 연동 설정을 수행할 수 있습니다.

다음 절차에 따라 서버 연동 설정을 수행합니다.

![](/DevConsole/Resources/Images/DevConsole-Extension_Server_Settings.png)

<ol>
  <li>Extension 정보 입력 UI에서 위쪽에 있는 <strong>서버 연동 설정</strong> 탭을 클릭합니다.</li>
  <li>Extension의 서버 URL(endpoint) 정보를 <strong>서비스 서버 URL</strong> 항목에 입력합니다.</li>
  <li>(Extension이 제공하는 서비스의 사용자 계정과 Clova의 사용자 계정 간에 연결이 필요한 경우 <strong>계정 연결 여부</strong> 항목을 <strong>네</strong>로 선택합니다. 계정 연결에 대한 자세한 설명은 <a href="#SetAccountLinking">계정 연결 설정</a>을 참조합니다.</li>
  <li><strong>SSL 인증</strong> 항목의 라디오 버튼을 클릭합니다. Extension을 제공하는 서버는 반드시 공인된 인증 기관의 인증서를 사용해야 합니다. (Self-signed 인증서 사용 불가)</li>
  <li>서버 연동 설정과 관련된 내용을 입력한 후 <strong>저장</strong> 버튼을 클릭합니다.</li>
</ol>

### 계정 연결 설정 {#SetAccountLinking}

Extension으로 제공하려는 서비스의 사용자 계정이 Clova의 사용자 계정과 연결이 필요한 경우 [서버 연동 설정](#SetServerConnection) 중에 [계정 연결(account linking)](/CEK/Guides/LinkUserAccount.md)에 관련된 정보를 입력해야 합니다.

다음 절차에 따라 계정 연결 설정에 [필요한 정보](/CEK/Guides/LinkUserAccount.md#RegisterAccountLinkingInfo)를 입력합니다.

<ol>
  <img src="/DevConsole/Resources/Images/DevConsole-Extension_Accoun_Linking_Settings_1.png" />
  <li><strong>계정 연결 여부</strong> 항목에서 <strong>네</strong>를 선택합니다.</li>
  <li>사용자가 계정 인증을 할 수 있도록 UI를 제공하는 Authorization URL을 <strong>로그인 URL</strong> 항목에 입력합니다. 사용자가 extension을 활성화하면 이 페이지로 이동됩니다.</li>
  <li>(만야, 사용자가 본인 계정을 바로 설정할 수 있도록 하고 싶은 경우) <strong>계정 설정 페이지 URL</strong> 항목에 계정 설정 페이지의 URL을 입력합니다.</li>
  <li>사용자 계정 인증 시 HTTPS 요청에 필요한 <strong>클라이언트 ID</strong>를 입력합니다. 클라이언트 ID는 <a href="/CEK/Guides/LinkUserAccount.html#BuildAuthServer">인증 서버를 구축</a>할 때 생성한 값입니다.</li>
  <li><strong>개인 정보 정책 URL</strong> 항목에 extension이 제공하는 서비스의 개인 정보 보호 정책과 관련된 내용이 제공되는 페이지의 URL을 입력합니다. 이 페이지의 내용은 추후 스토어에 노출됩니다.</li>
  <li>(만약, <strong>로그인 URL</strong>이나 <strong>개인 정보 정책 제공 URL</strong>에서 제공하는 페이지가 다른 도메인에서 필요한 자원을 가져오는 경우) <strong>도메인 리스트</strong> 항목에 필요한 도메인을 추가합니다.</li>
  <li>(만약, 사용자 계정 연결 시 발급되는 access token의 사용 범위(scope)를 미리 정의한 경우) <strong>권한 범위</strong> 항목에 미리 정의한 범위를 추가합니다.</li>
  <img src="/DevConsole/Resources/Images/DevConsole-Extension_Accoun_Linking_Settings_2.png" />
  <li><strong>Access token URI</strong> 항목에 서비스의 access token을 발급 받을 수 있는 URL을 입력합니다. 현재 <strong>허가 승인 타입(grant type)은 code grant 방식만 지원</strong>하고 있습니다.</li>
  <li><strong>Access token 재발급 URI</strong> 항목에 서비스의 access token을 갱신할 수 있는 URL을 입력합니다.</li>
  <li>서비스의 access token을 획득 시 HTTPS 요청에 필요한 <strong>클라이언트 secret</strong>을 입력합니다. 클라이언트 secret은 <a href="/CEK/Guides/LinkUserAccount.html#BuildAuthServer">인증 서버를 구축</a>할 때 생성한 값입니다.</li>
  <li><strong>클라이언트 인증 정보 전송 방식</strong>은 다음 중 인증 서버의 인터페이스 구현에 맞는 값을 설정합니다.
    <ul>
      <li><strong>HTTP Basic (Recommended)</strong>: 서비스 access token을 획득하기 위해 인증 정보(Credentials)를 헤더에 입력받는 경우</li>
      <li><strong>Credentials in request body</strong>: 서비스 access token을 획득하기 위해 인증 정보를 본문(body)에 입력받는 경우</li>
    </ul>
  </li>
</ol>

<div id="RedirectURI" class="note">
  <p><strong>Note!</strong></p>
  <p>계정 인증 후 이동할 클라이언트가 URL(redirect URL)은 <code>{{ book.RedirectURLforAccountLinking }}</code>이며, <strong>리다이렉트 URL</strong> 항목에서 확인할 수 있습니다.</strong></p>
  <img src="/DevConsole/Resources/Images/DevConsole-Redirect_URL_for_Extension_Accoun_Linking.png" />
</div>
