# 튜토리얼
여러분의 서비스를 Clova와 연동하려면 extension을 개발해야 합니다. 이 튜토리얼은 extension을 개발하는 기본적인 과정을 순서대로 짚어보면서 Clova를 처음 접하는 개발자가 개발 방법을 익힐 수 있도록 도와줍니다.

이 튜토리얼을 따라하면 다음과 같은 것을 익힐 수 있습니다.
* [첫 번째 튜토리얼: 기초적인 extension 만들기](/CEK/Tutorials/Build_Simple_Extension.md)
* 두 번째 튜토리얼(추가 예정): 사용자가 입력한 정보를 활용하는 interaction 모델 적용하기
* 세 번째 튜토리얼(추가 예정): 예, 아니오 등과 같은 기본적인 의사 표현 처리하기

## Custom Extension 필수 요소 {#Requisite}

{% include "./BasicInformation/Mandatory_Components.md" %}

이 튜토리얼은 [주사위 놀이](/CEK/Examples/Extension_Examples.md#DiceDrawer)라는 샘플 extension을 통해 위 두 요소를 만들고 등록하는 방법을 설명합니다.

## 주사위 놀이 Extension 기능 {#DiceExtension}
주사위 놀이 extension은 이름처럼 주사위를 굴려 그 결과를 알려주는 extension 입니다.
여기서는 서비스되고 있는 '주사위 놀이'와 중복되지 않도록 '샘플 주사위'라는 이름으로 만듭니다.

{% include "./BasicInformation/DICE_Sample_Dialog.md" %}