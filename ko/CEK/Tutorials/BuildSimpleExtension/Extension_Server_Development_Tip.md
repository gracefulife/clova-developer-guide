Clova는 사용자의 음성 입력을 분석한 결과를 extension 서버에 전송하며, 서버는 수신한 내용에 맞게 응답하도록 구현해야 합니다.

* **분석한 결과가 별도로 등록한 사용자 의도(**[Custom intent](/Design/Design_Guideline_For_Extension.md#CustomIntent)**)이면,**

	Clova는 extension 실행, 등록한 의도 실행, extension 종료 등 세 가지 타입 중 하나의 요청 메시지를 전송하며, 서버는 각각의 메시지에 따라 extension 시작, 지정된 의도 처리, extension 종료를 처리한 후 그 결과를 반환하면 됩니다.

* **분석한 결과가 Clova가 기본적으로 제공하는 의도(**[Built-in intent](/Design/Design_Guideline_For_Extension.md#BuiltinIntent)**)이면,**

	Clova는 그에 따라 도움말 안내, 긍정, 부정, 실행 취소 등의 요청 메시지를 전송하며, 서버는 이에 따른 일반적인 응답을 하면 됩니다.
