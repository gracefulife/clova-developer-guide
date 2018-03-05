사용자가 던질 주사위의 개수를 지정할 수 있도록 interaction 모델을 수정해야 합니다.

이를 위해 우선 slot에 담을 정보 유형을 결정하여 interaction 모델에 slot 타입을 선언하고, 이 타입을 사용할 slot을 intent에 등록한 뒤, 추가 정보가 포함된 사용자 발화 예시를 입력하여 Clova가 slot을 인식할 수 있도록 해줍니다.

### 사용할 slot 타입 선언하기
Slot에 담을 추가 정보의 유형에 따라 slot의 타입을 정해야 합니다. 예를 들어, 주사위의 개수는 숫자로 나타낼 수 있습니다.

Clova는 모든 extension이 범용적으로 사용할 수 있도록 일반적으로 쓰이는 정보 유형을 미리 정의해두었고, 이를 [built-in slot 타입](/Design/Design_Guideline_For_Extension.md#BuiltinSlotType)이라고 합니다. 숫자 타입은 `CLOVA.NUMBER`라는 built-in slot 타입으로 정의되어 있으므로, 주사위의 개수를 처리하기 위한 별도의 유형을 만들지 않아도 됩니다.

<div class="note">
  <p><strong>Note!</strong></p>
  <p>Built-in slot 타입으로 정의되지 않은 extension 고유의 정보 유형은 <a href="/Design/Design_Guideline_For_Extension.md#CustomSlotType">custom slot 타입</a>을 정의하여 처리할 수 있습니다.</p>
</div>

<a href="https://developers.naver.com/console/clova/cek/#/list" target="_blank">Clova developer console</a>에 접속하여 다음과 같이 샘플 주사위 extension에서 사용할 slot 타입을 선언합니다.

1. 샘플 주사위의 **{{ book.DevConsole.cek_interaction_model }}** 항목 내 **{{ book.DevConsole.cek_edit }}** 버튼을 누릅니다.
2. **{{ book.DevConsole.cek_builder_list_title_slottype }}** 오른쪽에 있는 <img class="inlineImage" src="/CEK/Resources/Images/DevConsole_Plus_Button.png" /> 버튼을 누릅니다.
3. **{{ book.DevConsole.cek_builder_new_slottype_builtin_title }}** 아래의 테이블에서 `CLOVA.NUMBER`의 체크박스를 선택합니다.

  <img src="/CEK/Resources/Images/CEK_Tutorial_Builtin_Type_Slots_Register_Slot_Type.png" style="max-width:800px;"/>

4. **{{ book.DevConsole.cek_builder_new_slottype_builtin_title }}** 오른쪽의 **{{ book.DevConsole.cek_save }}** 버튼을 누릅니다.

### Intent에 slot 등록하기
던질 주사위의 개수는 주사위를 던지는 동작에 필요한 추가 정보입니다. 주사위를 던지는 동작은 첫 번째 튜토리얼에서 `ThrowDiceIntent`라는 intent로 등록했으므로, 이 intent에 주사위의 개수를 의미하는 slot을 등록해야 합니다.
앞서 slot 타입을 선언했던 화면에서 다음과 같이 slot을 등록합니다.

1. **{{ book.DevConsole.cek_builder_list_title_intent }}** 아래에 있는 custom intent인 `ThrowDiceIntent`를 선택합니다.
2. **{{ book.DevConsole.cek_builder_intent_slot_title }}** 아래의 입력란에 "diceCount"라고 입력합니다.
3. 엔터키 또는 오른쪽에 있는 <img class="inlineImage" src="/CEK/Resources/Images/DevConsole_Plus_Button.png" /> 버튼을 누릅니다.
4. 등록한 "diceCount" 오른쪽 **{{ book.DevConsole.cek_builder_utterance_select_slot }}** 콤보박스를 누릅니다.
5. 나타난 목록 중에서 앞서 등록한 **{{ book.DevConsole.cek_builder_select_slottype_builtin }}**의 `CLOVA.NUMBER`를 선택합니다.

  <img src="/CEK/Resources/Images/CEK_Tutorial_Builtin_Type_Slots_Add_Slot.png" style="max-width:800px;"/>

6. 화면 오른쪽 상단의 **{{ book.DevConsole.cek_save }}** 버튼을 누릅니다.

### 발화 예시 입력하기
첫 번째 튜토리얼에서는 단순히 주사위를 던져달라는 문장만 예시로 입력했으나, 이제는 slot을 이용하여 주사위 개수를 지정하는 새로운 문장을 예시로 입력해야 합니다.

앞서 slot을 등록했던 화면에서 다음과 같이 발화 예시 문장을 입력합니다.

1. **{{ book.DevConsole.cek_builder_intent_expression_title }}** 아래의 입력란에 "주사위 두 개 굴려"라고 입력합니다.

  <img src="/CEK/Resources/Images/CEK_Tutorial_Builtin_Type_Slots_Sample_Utterance.png" style="max-width:800px;"/>

2. 엔터키 또는 <img class="inlineImage" src="/CEK/Resources/Images/DevConsole_Plus_Button.png" /> 버튼을 누릅니다.
3. 등록된 문장에서 "두 개"라는 단어를 마우스로 드래그하여 선택합니다.
4. **{{ book.DevConsole.cek_builder_slot_layer_select_slot }}** 밑에 있는 "diceCount"를 선택합니다.

  <img src="/CEK/Resources/Images/CEK_Tutorial_Builtin_Type_Slots_Set_Slot.png" style="max-width:800px;"/>
5. "하나 던져봐", "다섯 개의 주사위 굴려"라는 문장으로 1-4를 반복합니다.
