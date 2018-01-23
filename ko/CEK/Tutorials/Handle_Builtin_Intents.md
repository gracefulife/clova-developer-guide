# 기본적인 의사 표현 처리하기
이 튜토리얼에서는 [기초적인 extension 만들기](/CEK/Tutorials/Build_Simple_Extension.md)에서 만든 샘플 주사위 extension을 통해 예, 아니오 등의 기본적인 의사 표현을 처리하는 법을 알아봅니다.

Clova는 빈번하게 발생하는 사용자의 기본적인 의사 표현을 모든 extension에서 공통으로 사용할 수 있도록 [built-in intent](/Design/Design_Guideline_For_Extension.md#BuiltinIntent)로 미리 정의해 놓았습니다. 예, 아니오를 포함하여 extension 사용법을 알려달라는 요청이나 처리 중인 작업을 취소하는 요청 등이 built-in intent에 포함됩니다.

Built-in intent를 처리하는 과정은 다음과 같습니다.
* 1단계. Built-in intent 처리 구현 (Extension 서버에서 작업)
* 2단계. Built-in intent 동작 테스트 (Clova developer console에서 작업)

## 1단계. Built-in intent 처리 구현 {#Step1}
{% include "/CEK/Tutorials/HandleBuiltinIntents/Implement_Builtin_Handler.md" %}

## 2단계. Built-in intent 동작 테스트 {#Step2}
{% include "/CEK/Tutorials/HandleBuiltinIntents/Test_Builtin_Intent.md" %}
