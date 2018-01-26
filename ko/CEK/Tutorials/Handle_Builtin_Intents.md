# 기본적인 의사 표현 처리하기
이 튜토리얼에서는 [기초적인 extension 만들기](/CEK/Tutorials/Build_Simple_Extension.md)에서 만든 샘플 주사위 extension을 통해 예, 아니오 등의 기본적인 의사 표현을 처리하는 법을 알아봅니다.

Clova는 빈번하게 발생하는 사용자의 기본적인 의사 표현을 모든 extension에서 공통으로 사용할 수 있도록 [built-in intent](/Design/Design_Guideline_For_Extension.md#BuiltinIntent)로 미리 정의해 놓았습니다. 다음은 Clova가 제공하는 built-in intent입니다.

| Built-in intent 이름       | 의도               | 대응하는 사용자 발화 예시                                      |
|---------------------------|-------------------|----------------------------------------------------------|
| Clova.GuideIntent         | 도움말 요청          | "너 뭐 할 줄 알아?", "사용법 알려줘" |
| Clova.CancelIntent        | 실행 취소 요청        | "취소", "취소해줘"                                          |
| Clova.YesIntent           | 긍정 응답(예, Yes)   | "응", "그래", "알겠어", "알겠습니다", "오케이"                   |
| Clova.NoIntent            | 부정 응답(아니오, No) | "아니", "아니요", "싫어"                                     |

사용자가 도움말을 요청하거나 실행 취소를 요청할 때 이를 처리하기 위해 첫 번째 튜토리얼에서 했던 것처럼 intent와 예시 문장을 등록할 필요 없이 위 표에 있는 built-in intent를 사용하면 됩니다.

Built-in intent를 처리하는 과정은 다음과 같습니다.
* 1단계. Built-in intent 처리 구현 (Extension 서버에서 작업)
* 2단계. Built-in intent 동작 테스트 (Clova developer console에서 작업)

## 1단계. Built-in intent 처리 구현 {#Step1}
{% include "/CEK/Tutorials/HandleBuiltinIntents/Implement_Builtin_Handler.md" %}

## 2단계. Built-in intent 동작 테스트 {#Step2}
{% include "/CEK/Tutorials/HandleBuiltinIntents/Test_Builtin_Intent.md" %}

이렇게 하면 샘플 주사위 extension이 도움말 요청에 응답할 수 있게 됩니다.
이와 같은 방법으로 extension 서버가 `Clova.CancelIntent`, `Clova.YesIntent`, `Clova.NoIntent`을 처리하도록 구현하면, 실행 취소나 긍정 혹은 부정을 의미하는 요청에도 응답할 수 있습니다.
