Clova는 사용자의 음성 입력을 분석하여 판단한 intent와 slot을 extension 서버에 전송하며, 서버는 이 요청에 대해 응답하도록 구현해야 합니다.

* **사용자의 입력을 분석한 결과가 등록한 intent이면,**

	Clova는 extension 실행, intent 실행, extension 종료 등 세 가지 타입 중 하나의 요청을 전송하며, 서버는 각각의 요청에 따라 extension 시작, intent로 지정된 명령 실행, extension 종료를 처리한 후 그 결과를 반환하면 됩니다.

* **사용자의 입력을 분석한 결과가 Clova가 기본적으로 제공하는 요청(**[Built-in intent](/Design/Design_Guideline_For_Extension.md#Intent)**)이면,**

	Clova는 그에 따라 도움말 안내, 긍정, 부정, 실행 취소 등의 요청을 전송하며, 서버는 이 요청에 따른 일반적인 응답을 하면 됩니다.
