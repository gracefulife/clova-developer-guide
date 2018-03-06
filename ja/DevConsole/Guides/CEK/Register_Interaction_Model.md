# 対話モデルを登録する

CEKがExtensionにユーザーのリクエストを送る際、ユーザーの発話をどう解析し、どんな形式で送るかを決めるために、[あらかじめinteraction modelを定義](/Design/Design_Guideline_For_Extension.md#DefineInteractionModel)する必要があります。対話モデルは、[Custom Extension](/CEK/Guides/Build_Custom_Extension.md)に渡されるリクエストを標準化したスキーマです。

対話モデルを登録するには、先にClova Developer Centerで[Extensionを登録](/DevConsole/Guides/CEK/Register_Extension.md)する必要があります。CEKのメニューで次のように、interaction modelを登録するExtensionの**{{ book.DevConsole.cek_edit }}**ボタンをクリックします。

![](/DevConsole/Resources/Images/DevConsole-Interaction_Model_Menu.png)

以下のような*{{ book.DevConsole.cek_interaction_model }}：{{ book.DevConsole.Dashboard }}**画面が表示されます。

![](/DevConsole/Resources/Images/DevConsole-Interaction_Model_Dashboard.png)

Extensionを設計する段階で[定義したinteraction model](/Design/Design_Guideline_For_Extension.md#DefineInteractionModel)は、次の順で登録します。

1.[Built-in slotタイプを追加する](#AddBuiltinSlotType)
2.[Custom slotタイプを追加する](#AddCustomSlotType)
3.[Built-in intentを追加する](#AddBuiltinIntent)
4.[Custom intentを追加する](#AddCustomIntent)

<div class="note">
  <p><strong>メモ</strong></p>
  <p>Custom intentを追加してから必要なslotタイプを追加することもできますが、Clova Developer Centerの提供するUIの特性上、先にslotタイプを追加してからintentを追加することをお勧めします。</p>
</div>

## Built-in slotタイプを追加する {#AddBuiltinSlotType}

サービスを提供するExtensionがどの[built-in slotタイプ](/Design/Design_Guideline_For_Extension.md#Slot)を使用するか決めたなら、そのExtensionのinteraction modelにbuilt-in slotタイプを追加する必要があります。例えば、ピザの宅配Extensionを作成する場合、ユーザーの発話に、ピザの数量に関する情報の表現が含まれることが予想されます。従って、関連するbuilt-in slotタイプをExtensionで使用する必要があります。その場合、次の順でbuilt-in slotタイプをExtensionに追加します。

<ol>
  <li><strong>{{ book.DevConsole.cek_builder_list_title_slottype }}</strong>パネルの右上、または左側のサイドメニューの<strong>{{ book.DevConsole.cek_builder_list_title_slottype }}</strong>メニューの右上にある<img class="inlineImage" src="/DevConsole/Resources/Images/DevConsole-Plus_Button.png" />ボタンをクリックします。ボタンをクリックすると、<strong>{{ book.DevConsole.cek_interaction_model }}：{{ book.DevConsole.SlotType }}</strong>画面が表示されます。</li>
  <li><strong>{{ book.DevConsole.UseBuiltInSlotType }}</strong>項目で必要なbuilt-in slotタイプのチェックボックスをクリックします。</li>
  <img src="/DevConsole/Resources/Images/DevConsole-Add_Built-in_Slot_Type.png" />
  <li>必要なbuilt-in slotタイプにチェックを入れ、右上の<strong>{{ book.DevConsole.cek_save }}</strong>ボタンをクリックします。</li>
</ol>

すると、**{{ book.DevConsole.cek_interaction_model }}：{{ book.DevConsole.Dashboard }}**画面の**{{ book.DevConsole.cek_builder_list_title_slottype }}**パネルに、次のようにbuilt-in slotタイプが追加されたことを確認できます。

![](/DevConsole/Resources/Images/DevConsole-Added_Built-in_Slot_Type.png)

## Custom slotタイプを追加する {#AddCustomSlotType}

次に、Extensionで使用する[custom slotタイプ](/Design/Design_Guideline_For_Extension.md#Slot)を定義します。[Built-in slotタイプを追加する](#AddBuiltinSlotType)に続き、ピザの宅配Extensionを作成すると仮定します。ユーザーの発話のうち、ピザの種類に当たる部分をcustom slotタイプとして定義する必要があります。以下の表のような代表語と同義語を持つ、「PIZZA_TYPE」というcustom slotタイプを追加すると仮定します。

| 代表語           | 同義語                                        |
|----------------|----------------------------------------------|
| ペパロニ          | ペパロニピザ                                  |
| バーベキュー           | バーベキューピザ、BBQピザ                           |
| チーズ             | チーズピザ                                     |
| 野菜             | 野菜ピザ、ベジピザ、ベジタリアンピザ               |
| シュリンプゴールドクラスト | シュリンプゴールドクラストピザ、シュリンプゴルクラピザ、シュリンプゴルクラ |

次の順でcustom slotタイプを追加します。

<ol>
  <li><strong>{{ book.DevConsole.cek_builder_list_title_slottype }}</strong>パネルの右上、または左側のサイドメニューの<strong>{{ book.DevConsole.cek_builder_list_title_slottype }}</strong>メニューの右上にある<img class="inlineImage" src="/DevConsole/Resources/Images/DevConsole-Plus_Button.png" />ボタンをクリックします。ボタンをクリックすると、<strong>{{ book.DevConsole.cek_interaction_model }}：{{ book.DevConsole.SlotType }}</strong>画面が表示されます。</li>
  <li><strong>{{ book.DevConsole.CreateSlotType }}</strong>の入力フィールドに、追加するcustom slotタイプの名前を入力し、<strong>{{ book.DevConsole.cek_create }}</strong>ボタンをクリックします。Custom slotタイプが生成されると、そのcustom slotタイプの詳細を確認できる画面が表示されます。</li>
  <img src="/DevConsole/Resources/Images/DevConsole-Add_Custom_Slot_Type_1.png" />
  <li><img class="inlineImage" src="/DevConsole/Resources/Images/DevConsole-Plus_Button.png" />ボタンをクリックして、<strong>{{ book.DevConsole.cek_builder_slottype_dictionary_title }}</strong>に代表語を追加します。</li>
  <img src="/DevConsole/Resources/Images/DevConsole-Add_Custom_Slot_Type_2.png" />
  <li>追加した代表語に、同義語や類義語を追加します。</li>
  <img src="/DevConsole/Resources/Images/DevConsole-Add_Custom_Slot_Type_3.png" />
  <li>最後に、右上の<strong>{{ book.DevConsole.cek_save }}</strong>ボタンをクリックします。</li>
</ol>

右の<strong>ダッシュボード</strong>メニューで**{{ book.DevConsole.cek_interaction_model }}：{{ book.DevConsole.Dashboard }}**に移動すると、custom slotタイプが追加されたことを確認できます。

![](/DevConsole/Resources/Images/DevConsole-Added_Custom_Slot_Type.png)

定義するcustom slotタイプに大量の情報を入力する必要がある場合、TSV(タブ区切りの値、.tsv)形式のファイルをアップロードすることもできます。TSVファイルの各行の1番目の値が代表語となります。それに続くタブ区切りの値は、その代表語の同義語または類義語になります。次は、「PIZZA_TYPE」というcustom slotタイプの定義を、TSV形式で表現したものです。

```
ペパロニ　　　　　　ペパロニピザ
バーベキュー　　　バーベキューピザ　　　BBQピザ
チーズ　　　　　　　　チーズピザ
野菜　　　　　　野菜ピザ　　　　　　　　ベジピザ　　　　　　　　ベジタリアンピザ
シュリンプゴールドクラスト　　シュリンプゴールドクラストピザ　　シュリンプゴルクラピザ　　シュリンプゴルクラ
```

Clova Developer Centerは、以下のように**アップロード**ボタンと**ダウンロード**ボタンを提供します。**アップロード**ボタンをクリックすると、あらかじめTSVファイルで定義したcustom slotタイプをアップロードできます。**ダウンロード**ボタンをクリックすると、現在Clova Developer Centerで作成中のcustom slotタイプをTSV形式でダウンロードできます。

![](/DevConsole/Resources/Images/DevConsole-Custom_Slot_Upload_and_Download_Button.png)

## Built-in intentを追加する {#AddBuiltinIntent}

[Built-in intent](/Design/Design_Guideline_For_Extension.md#Intent)は、Clovaプラットフォームで一部の共通したユーザーリクエストのカテゴリを決め、それを共有して使用するために宣言したintentです。例えば、頻繁に発生すると予想されるユーザーの肯定・否定、キャンセルなどのリクエストを、intentとしてあらかじめ定義したものです。現在、すべてのExtensionは、Clovaの提供するbuilt-in intentをすべて処理できる必要があります。次のbuilt-in intentがデフォルトで登録されています。

![](/DevConsole/Resources/Images/DevConsole-Built-in_Intent_List.png)

<div class="note">
  <p><strong>メモ</strong></p>
  <p>今後、Extensionごとに必要なbuilt-in intentのみ使用できるように変更される予定です。</p>
</div>

## Custom intentを追加する {#AddCustomIntent}
Extensionが使用する[built-in slotタイプ](#AddBuiltinSlotType)と[custom slotタイプ](#AddCustomSlotType)を追加したら、次はcustom intentを追加します。続けて、ピザを注文するユーザーのリクエストを仮定します。次の順で「OrderPizza」という名前のintentを追加します。

<ol>
  <li><strong>{{ book.DevConsole.cek_builder_list_title_intent }}</strong>パネルの右上か、左側のサイドメニューの<strong>{{ book.DevConsole.cek_builder_list_title_intent }}</strong>メニューの右上の<img class="inlineImage" src="/DevConsole/Resources/Images/DevConsole-Plus_Button.png" />ボタンをクリックします。ボタンをクリックすると、<strong>{{ book.DevConsole.cek_interaction_model }}：{{ book.DevConsole.NewIntent }}</strong>画面が表示されます。</li>
  <li><strong>{{ book.DevConsole.CreateCustomIntent }}</strong>の入力フィールドに、追加するcustom intentの名前を入力し、<strong>{{ book.DevConsole.cek_create }}</strong>ボタンをクリックします。Custom intentが生成されると、そのcustom intentの詳細を確認する画面が表示されます。</li>
  <img src="/DevConsole/Resources/Images/DevConsole-Add_Custom_Intent_1.png" />
  <li><strong>{{ book.DevConsole.cek_builder_intent_slot_title }}</strong>の入力フィールドに、追加するslotの名前を入力し、右の<img class="inlineImage" src="/DevConsole/Resources/Images/DevConsole-Plus_Button.png" />ボタンをクリックしてslotを追加します。</li>
  <img src="/DevConsole/Resources/Images/DevConsole-Add_Custom_Intent_2.png" />
  <li>Slotを追加し、そのslotのタイプを指定します。</li>
  <img src="/DevConsole/Resources/Images/DevConsole-Add_Custom_Intent_3.png" />
  <li>次に、<strong>{{ book.DevConsole.cek_builder_intent_expression_title }}</strong>にサンプル発話を入力し、右の<img class="inlineImage" src="/DevConsole/Resources/Images/DevConsole-Plus_Button.png" />ボタンをクリックしてそのサンプル発話を追加します。</li>
  <img src="/DevConsole/Resources/Images/DevConsole-Add_Custom_Intent_4.png" />
  <li>追加したサンプル発話で、slotとして処理される部分をドラッグしてslotを指定します。</li>
  <img src="/DevConsole/Resources/Images/DevConsole-Add_Custom_Intent_5.png" />
  <li>ステップ5、6を繰り返して、intentにサンプル発話を必要なだけ追加します。</li>
  <li>最後に、右上の<strong>{{ book.DevConsole.cek_save }}</strong>ボタンをクリックします。</li>
</ol>

<div class="note">
  <p><strong>メモ</strong></p>
  <p>Slotタイプとslotの名前は、集合の名前か、または複数の値を代入できる、抽象的な概念を持つ名前である必要があります。</p>
</div>

Custom slotタイプと同じく、TSV(タブ区切りの値、.tsv)形式のファイルをアップロードして定義することもできます。TSVファイルは、intentのslotを定義する部分と、サンプル発話を列挙する部分の2つに分けられます。Intentのslot定義がファイルの先頭にあり、`[INTENT SLOT]`ヘッダの次の行でslotが列挙されます。タブで区切られた最初の列はintentで使用されるslotの名前で、2番目の列はslotタイプです。

Intentのサンプル発話の列挙がそれに続きます。`[INTENT EXPRESSION]`ヘッダの次の行でサンプル発話が列挙されます。サンプル発話でslotを区別するために、該当する表現をslot名のタグで囲む必要があります。以下は、intentを定義したTSVファイルの例です。

```
[INTENT SLOT]
pizzaType	PIZZA_TYPE
pizzaAmount	CLOVA.NUMBER

[INTENT EXPRESSION]
<pizzaType>ペパロニ</pizzaType><pizzaAmount>2枚</pizzaAmount>注文して。
<pizzaType>BBQピザ</pizzaType><pizzaAmount>2枚</pizzaAmount>出前取ってくれる?
<pizzaType>コンビネーションピザ</pizzaType><pizzaAmount>2つ</pizzaAmount>頼んで。
<pizzaType>シュリンプゴルクラ</pizzaType><pizzaAmount>1個</pizzaAmount>お願い。
...
```

Clova Developer Centerは、以下のように**アップロード**ボタンと**ダウンロード**ボタンを提供します。**アップロード**ボタンをクリックすると、あらかじめTSVファイルで定義したcustom intentをアップロードできます。**ダウンロード**ボタンをクリックすると、現在Clova Developer Centerで作成しているcustom intentをTSV形式でダウンロードできます。

![](/DevConsole/Resources/Images/DevConsole-Utterance_Example_Upload_and_Download_Button.png)

<div class="danger">
  <p><strong>注意</strong></p>
  <p>1つのinteraction modelでは、intentに関わらず、slotタイプに同じ名前を宣言することをお勧めします。例えば、「OrderPizza」intentで、ピザの種類(「PIZZA_TYPE」)に関するslot名を「pizzaType」にしたとすると、他のintentで同じslotタイプを宣言する際、同じく「pizzaType」にする必要があります。ただし、「ソウルからプサンまで時間がどれぐらいかかるか教えて」のように、「ソウル」と「プサン」が同じslotタイプであっても、目的によって区別される必要のある場合、slot名を区別して作成します。</p>
</div>

これまで、1つのintentをinteraction modelに追加する方法を説明しました。ここで説明されている方法を繰り返して、Extensionにintentを必要なだけ追加すると、以下のようにinteraction modelを完成できます。

![](/DevConsole/Resources/Images/DevConsole-Added_Interaction_Model.png)
