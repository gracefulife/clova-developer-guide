<a href="{{ book.DeveloperConsoleURL }}/cek/#/list" target="_blank">Clova developer console</a>에 접속하여 extension의 기본 정보를 등록합니다.
주요 항목은 아래와 같습니다.

* Extension 정보
	* **{{ book.DevConsole.cek_id }}**: extension의 고유한 ID 값으로, 일반적으로 패키지 이름과 extension 이름의 조합으로 작성합니다. 샘플 주사위 extension의 ID는 'my.clova.extension.sampledice'로 입력합니다.
	* **{{ book.DevConsole.cek_invocation_name }}**: extension을 실행할 때 부르는 이름으로 Clova 앱이나 스피커 형태의 기기에서 음성 인식이 잘 되는 단어를 선택합니다. 샘플 주사위 extension의 호출 이름은 '샘플 주사위' 입니다.

* 서버 연동 설정
	* **{{ book.DevConsole.cek_service_endpoint_url }}**: Clova와 통신할 extension의 REST API 서버로, 외부에서 접근할 수 있는 URL이어야 합니다.
		1단계에서 샘플 주사위 소스 코드를 실행한 서버의 주소를 입력합니다.

		<div class="note">
	    <p><strong>Note!</strong></p>
	    <p>테스트 단계에서는 HTTP도 가능하나 정식 서비스를 위해서는 HTTPS여야 합니다. Extension 서버는 HTTP일 때 80번 포트를 HTTPS일 때 443번 포트를 사용해야 합니다.</p>
		</div>

	* **{{ book.DevConsole.cek_account_linking }}**: 인증 서버(OAuth 2.0기반)를 사용해 3rd party의 회원정보와 연동할 경우에만 사용합니다.
		샘플 주사위 extension은 **{{ book.DevConsole.cek_no }}**로 설정합니다.
* 배포 정보 및 개인 정보 보호 및 규정 준수

	Extension 배포와 심사에 필요한 정보입니다. 이 튜토리얼의 내용을 수행할 때는 입력하지 않아도 됩니다.
