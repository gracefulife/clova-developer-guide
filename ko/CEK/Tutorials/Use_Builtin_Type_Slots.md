# 사용자가 입력한 정보 활용하기
이 튜토리얼에서는 [기초적인 extension 만들기](/CEK/Tutorials/Build_Simple_Extension.md)에서 만든 샘플 주사위 extension이 사용자의 요청에 따라 주사위를 1개 이상 던지도록 하는 법을 알아봅니다. 

사용자의 음성 명령에는 extension이 수행할 동작 외에 그 동작에 필요한 추가적인 정보가 들어있을 수 있습니다. [튜토리얼 개요](/CEK/Tutorials/Introduction.md)에서 기술한 샘플 주사위 extension을 사용법을 다시 봅시다.

{% include "/CEK/Tutorials/BasicInformation/DICE_Sample_Dialog.md" %}

두 번째 대화에서 사용자는 "주사위 **2개** 던져줘"라고 요청했고, 여기서 "2개"가 바로 "주사위 던지기"라는 동작에 필요한 추가적인 정보입니다.

Interaction 모델에서는 이런 추가 정보를 [slot](/Design/Design_Guideline_For_Extension.md#Slot)이라고 부릅니다. Extension에서 추가 정보를 사용하려면, interaction 모델을 정의할 때 어떤 추가 정보가 들어올지 미리 파악한 뒤 알맞은 slot을 등록해야 합니다. Clova는 이렇게 등록된 slot을 기반으로 사용자 요청에 포함된 추가 정보를 알아낼 수 있습니다.

추가 정보를 처리하는 방법은 다음과 같습니다.
* 1단계. Interaction 모델에 slot 등록 (Clova developer console에서 작업)
* 2단계. Slot 처리 구현 (Extension 서버에서 작업)
* 3단계. Slot 동작 테스트 (Clova developer console에서 작업)

## 1단계. Interaction 모델에 slot 등록 {#Step1}
{% include "/CEK/Tutorials/UseBuiltinTypeSlots/Add_Builtin_Slot.md" %}

## 2단계. Slot 처리 구현 {#Step2}
{% include "/CEK/Tutorials/UseBuiltinTypeSlots/Implement_Slot_Handler.md" %}

## 3단계. Slot 동작 테스트 {#Step3}
{% include "/CEK/Tutorials/UseBuiltinTypeSlots/Test_Builtin_Type_Slots.md" %}

이제 샘플 주사위 extension은 주사위를 1개 이상 던질 수 있게 되었습니다.
같은 방법으로 주사위를 1번 이상 던지게 하거나 숫자가 아닌 다른 값을 가진 주사위를 던지게 할 수 있습니다.
