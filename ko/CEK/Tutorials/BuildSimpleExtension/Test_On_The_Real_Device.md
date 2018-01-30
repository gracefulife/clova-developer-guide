Interaction 모델이 잘 동작하는 것을 확인했다면, 심사 요청 전에 실제 기기에서 테스트하여 음성 인식과 응답이 기대한대로 동작하는지 확인해야 합니다.

### 테스터 아이디 등록하기
특정 계정에서만 이 extension을 실행해볼 수 있도록 테스터 아이디를 등록합니다.

1. <a href="https://developers.naver.com/console/clova/cek/#/list" target="_blank">Clova developer console</a>에 접속합니다.
2. 샘플 주사위의 **Extension 정보** 항목 내 **수정** 버튼을 누릅니다.
3. 나타난 화면에서 **테스터 아이디**를 찾아 여러분의 {{ book.OrientedService }} 계정 아이디를 입력합니다.
4. **저장** 버튼을 누릅니다.

<div class="note">
  <p><strong>Note!</strong></p>
  <p>테스터 아이디를 등록한 후 조금 기다리면 extension을 테스트해 볼 수 있습니다. 만약, 1시간 정도가 지나도 extension을 테스트할 수 없을 경우 포럼이나 제휴 담당자를 통해 문의하시기 바랍니다.</p>
</div>

<div class="danger">
	<p><strong>Caution!</strong></p>
  <p>실제 기기에서 테스트 하려면 <strong>extension 정보</strong>에 반드시 외부에서 접속 가능한 실제 extension 서버 주소를 등록해야 합니다.</p></li>
</div>

### Clova 앱에서 실행하기
Clova 앱을 통해 샘플 주사위 extension을 실행합니다.

1. 테스트할 기기에 Clova 앱을 설치합니다.
2. 테스터 아이디로  입력한 {{ book.OrientedService }} 계정으로 로그인합니다.
3. 테스트용 extension 호출 이름으로 음성 명령을 내립니다. 예를 들어, "클로바, 샘플 주사위에 주사위 던지라고 해"라고 명령해봅니다.
4. Clova 앱이 "주사위를 1개 던집니다"라고 응답하는지 확인합니다.

Extension이 실제 기기에서도 잘 동작하면 서비스할 준비가 된 것입니다. 이제 Clova developer console에서 심사를 요청하여 extension을 배포할 수 있습니다.
