# クライアントデバイスのデザインガイドライン

Clovaが搭載されたクライアントデバイスを使用するユーザーに一貫したUI/UXを提供することで、ユーザーは混乱することなく便利に製品を使用することができます。そのため、Clovaに接続するクライアントデバイスを制作する際、以下の項目についてデザインガイドラインが提供されています。

* [クライアントの状態およびイベント](#ClientStateAndEvent)
* [ボタン](#Button)
* [ライト](#Light)
* [オーディオ](#Audio)
* [画面](#Screen)

<div class="note">
  <p><strong>Note!</strong></p>
  <p>ここで言及されていないガイドラインや仕様は、メーカーの判断またはポリシーに基づいて実装してください。判断が難しい場合には、提携担当者までお問合せください。</p>
</div>

## クライアントの状態およびイベント {#ClientStateAndEvent}

ユーザーの音声入力、Clovaの音声出力、マイクの状態、エラーの発生(Clovaサービスのエラー、ネットワークエラーなど)などをユーザーが容易に認知したり操作できるように、クライアントデバイスを設計・実装する必要があります。そのために、クライアントデバイスの状態、状態の遷移およびその流れをよく知っている必要があります。以下は、クライアントの状態を表した状態ダイアグラムです。

![](/Design/Resources/Images/Clova-Client-State_Diagram.png)

クライアントの各状態についての説明は以下の通りです。

| 状態                | 説明                                                            |
|------------------------|--------------------------------------------------------------------|
| Attending              | クライアントがユーザーの音声入力を受信するために待機している                        |
| Error                  | システムエラーが発生している                                                |
| Listening              | クライアントがユーザーの音声入力を受信している                            |
| Idle                   | クライアントで何の処理も行われていない                             |
| Mute on                | マイクがミュートに設定されている                                               |
| Processing & reporting | Clovaがユーザーの音声リクエストを処理しているか、またはスピーカーでClovaの音声を出力している |

上記で言及されている状態は、[ライト](#Light)、[効果音](#SoundEffect)、[画面](#Screen)などで表されます。状態の遷移は、ユーザーの音声や[ボタン](#Button)の操作、環境要因などによって実行されたり、発生したりします。

また、クライアントでは以下のイベントが発生することがあり、そのイベントも音声やライトで表現される必要があります。

| 名前               | 説明                                                           |
|------------------------|--------------------------------------------------------------------|
| アラーム(Alarm)             | 指定された日付と時間に鳴るアラーム                                           |
| リマインダー(Reminder)       | 指定された日付と時間に、ユーザーが入力した内容を表示したり、音声で再生しながら鳴るアラーム         |
| タイマー(Timer)            | 指定された時間が経過してから鳴るアラーム                                        |

## ボタン {#Button}

クライアントデバイスは、ユーザーが音声の代わりにデバイスを直接コントロールできるように、ボタンを提供する必要があります。クライアントがユーザーに提供できるボタンの種類と、実装する際に順守する内容を説明します。

* [ボタンの種類](#Buttons)
* [ボタンのガイドライン](#ButtonGuideline)

### ボタンの種類 {#Buttons}

クライアントデバイスは、以下のボタンを提供する必要があります。

| 名称                        | 説明                                                     | 必須/任意 |
|----------------------------|-------------------------------------------------------------|:---------:|
| 電源ボタン(Power)             | デバイスの電源をオン/オフします。                                        | 必須      |
| マイクボタン(Mic mute)    | マイクを有効/無効にします。                                | 必須      |
| ボリュームアップボタン(Volume up)       | スピーカーの音量を上げます。                                         | 必須      |
| ボリュームダウンボタン(Volume down)   | スピーカーの音量を下げます。                                          | 必須      |
| 再生/一時停止ボタン(Play/Pause) | オーディオを一時停止/再生します。または、処理中の作業を中止します。         | 必須      |
| 音声入力の聞き取りボタン(Wake up)   | ユーザーの音声入力を聞き取るモード(attending状態)に切り替わります。ユーザーが「クローバー」と話しかけるのと同じ動作です。 | 任意      |
| Wi-Fiボタン(Wi-Fi)          | Wi-Fiネットワークに接続したり、接続を解除します。                                 | 任意      |
| Bluetoothボタン(Bluetooth)     | Bluetoothデバイスとペアリング/接続/解除します。                              | 任意      |
| リセットボタン(Reset)          | デバイスをリセットします。                                              | 任意      |

### ボタンのガイドライン {#ButtonGuideline}

ボタンを提供する際に、以下の内容を順守する必要があります。

* 電源ボタンとマイクボタンは、物理ボタンで提供することを推奨します。
* 電源ボタンとマイクボタン以外のボタンは、物理ボタンまたはタッチ式のUIボタンなど、メーカーのポリシーに合わせてさまざまな形で提供することができます。
* 頻繁に操作する主要ボタンは、操作のしやすさのために、前面または上部に配置することを推奨します。
* タッチ式のUIボタンを提供する場合、ユーザーが手を離すとき(touch release)に、定義されたアクションを行う必要があります。
* あらかじめ定義されたボタンの組み合わせがない場合、2つ以上のボタン入力が同時に行われると、先に認識されたボタン入力の機能のみを処理する必要があります。
* ボタン入力ですでに作業を処理しているときに新規のボタン入力がある場合、前の作業に対するフィードバック効果を中止し、新規のボタン入力に対するフィードバック効果を提供する必要があります。
* UI画面が提供されているデバイスに限って、再生/一時停止ボタンをGUIボタンで提供することが可能です。
* ボタンは、以下の方法で提供できます。
  - 1つの機能のための単独のボタンを提供する(例、Bluetoothボタンを単独で提供する)
  - ボタンの長押し操作を利用して機能を提供する(例、電源ボタンを長押ししてリセットする機能を提供する)
  - 2つ以上のボタンの組み合わせを利用して機能を提供する(例、電源ボタンと再生ボタンを同時に押してリセットする機能を提供する)

## ライト {#Light}

クライアントデバイスは、[クライアントの状態およびイベント](#ClientStateAndEvent)や、ユーザーのリクエストに対するフィードバックなどを表現するためにライトを提供する必要があります。クライアントがユーザーに提供すべきライトについて説明します。

* [ライトの色](#LightColor)
* [照明効果](#LightEffect)
* [ライトのガイドライン](#LightGuideline)

### ライトの色 {#LightColor}

クライアントは、次のようなライトの色を使用する必要があります。

| ライトの色     | RGB値                | 説明                                   | 必須/任意 |
|-------------|----------------------|---------------------------------------|:--------:|
| Green       | <span style="color:#32C864; font-size:150%; vertical-align:middle;">&#9724;</span> 50、200、100(#32C864)   | ユーザーの音声入力を聞き取っている                                  | 必須  |
| Yellow Green | <span style="color:#B4FF00; font-size:150%; vertical-align:middle;">&#9724;</span> 180、255、0(#B4FF00)    | Clova通知(Notification)                             | 必須  |
| Red         | <span style="color:#FF0000; font-size:150%; vertical-align:middle;">&#9724;</span> 255、0、0(#FF0000)      | マイクのミュート、ネットワーク接続エラー、バッテリー不足などのエラー状況     | 必須  |
| Warm White   | <span style="color:#EDE9E5; font-size:150%; vertical-align:middle;">&#9724;</span> 237、233、229(#EDE9E5)  | スピーカーによるClovaの音声出力、アラーム/リマインダー/タイマーイベントの受信                             | 必須  |

以下は、Waveのライトの事例です。

| Green       | Yellow Green | Red         | Warm White   |
|-------------|-------------|-------------|-------------|
| ![](/Design/Resources/Images/Clova-Client-Light-Wave_Green.png) | ![](/Design/Resources/Images/Clova-Client-Light-Wave_Yellow_Green.png) | ![](/Design/Resources/Images/Clova-Client-Light-Wave_Red.png) | ![](/Design/Resources/Images/Clova-Client-Light-Wave_Warm_White.png) |

### 照明効果 {#LightEffect}

照明効果は、[ライトの色](#LightColor)が伝える意味に基づいて、もっと詳しい意味や状態を伝えるために使用されます。

以下の表は、クライアントデバイスを実装するときに、ライトが表すべきライト効果と、それについての説明およびサンプルを提供します。

| 照明効果                            | 説明                                      | サンプル                                                               |
|------------------------------------|------------------------------------------|-------------------------------------------------------------------|
| 点灯する(Lights up)                     | 特別な効果なしに、ライトを点灯した状態に切り替わります。   | ![](/Design/Resources/Images/Clova-Client-Light-Wave_Sustain.gif)              |
| ゆっくりと点滅を繰り返す(Repeat pulse)         | ライトの照度をゆっくりと上げたり下げたりすることを繰り返します。 | ![](/Design/Resources/Images/Clova-Client-Light-Wave_Repeat_Blink_Slowly.gif)  |
| ゆっくりと消灯する(Fade out)                 | ライトの照度をゆっくりと下げて、最後にライトを消します。 | ![](/Design/Resources/Images/Clova-Client-Light-Wave_Fade_Out.gif)             |
| 波の表現を繰り返す(Repeat Splash)          | ライトが左右に波を打つような効果を繰り返します。 | ![](/Design/Resources/Images/Clova-Client-Light-Wave_Splash.gif)         |

以下の表は、クライアントの[状態およびイベント](#ClientStateAndEvent)をライトで表現する方法を示します。

| 状態またはイベント               | 照明効果適用                | 必須/任意 |
|----------------------------|----------------------------|:---------:|
| Attending、listening状態     | Greenのライトを点灯する              | 必須     |
| End状態                    | Warm Whiteのライトをゆっくりと消灯する     | 必須     |
| Error状態                  | Redのライトの点滅をゆっくりと繰り返す       | 必須     |
| Mute on状態                | Redのライトを点灯する                | 必須     |
| Processing & reporting状態 | Warm Whiteのライトの点滅をゆっくりと繰り返す | 必須     |
| Mute on状態の解除            | Redのライトをゆっくりと消灯する           | 必須     |
| 待機時間が超過した直後           | Greenのライトをゆっくりと消灯する         | 必須     |
| アラーム、リマインダー、タイマーの開始      | Warm Whiteのライトが波の表現を繰り返す  | 任意     |

### ライトのガイドライン {#LightGuideline}

ライトを提供する際に、以下の内容を順守する必要があります。
  - 1メートル以内の距離で、0.7の視力を持つ人が[ライトの色](#LightColor)を区別できる必要があります。
  - ライトの色に定義されている意味以外の状態や意味を適用しないことを推奨します。
  - ライトの色は、ユーザーがRGB値と同一の色であると認知できるように適用する必要があります。
  - 必ず表現すべき[照明効果](#LightEffect)以外にも、デバイスの起動、スピーカーの音量調節、充電状態、ボタンのフィードバックなど、状況に合わせて、またメーカーのUXポリシーに合わせて、ライトの色と効果を追加することができます。
  - 1つのライトの色や効果で、あまり多くの意味や状態を表現しないことを推奨します。
  - 画面が提供されないデバイスは、ライトの明るさなどでデバイスのスピーカー音量のレベルを表示することを推奨します。
  - 移動できるバッテリー搭載のモデルは、バッテリーの充電状態をライトで把握できるように実装することを推奨します。

## オーディオ {#Audio}

クライアントデバイスでオーディオコンテンツ、効果音などを出力する際に順守するべき内容を説明します。

* [オーディオ再生の基本ルール](#AudioInterruptionRule)
* [ユーザー発話時のオーディオ再生ルール](#AudioInterruptionRuleForUserUtterance)
* [効果音](#SoundEffect)
* [プラットフォームでサポートされている音声圧縮形式](#SupportedAudioCompressionFormat)

### オーディオ再生の基本ルール {#AudioInterruptionRule}

クライアントは、オーディオコンテンツの再生中に、別のオーディオコンテンツの再生を要求される場合があります。そのとき、クライアントは、オーディオ再生ルールに従ってオーディオコンテンツを再生する必要があります。オーディオ再生ルールは、オーディオコンテンツのタイプを基準に作成されています。なので、再生ルールの前に、まずオーディオコンテンツのタイプについて知る必要があります。オーディオコンテンツのタイプは、以下のように分類されます。

| オーディオコンテンツのタイプ | 説明                                                                          |
|---------------|-------------------------------------------------------------------------------|
| Alert         | アラーム音、タイマー音、リマインダー音、リマインダー発話、緊急の警報音などのオーディオコンテンツ             |
| Content       | ユーザーのリクエストに対する音楽、動画、ニュース、ポッドキャストなどのオーディオコンテンツ                            |
| Dialogue      | ユーザーのリクエストに対するTTSオーディオコンテンツ                                                  |
| Feedback      | リセット音、着信音(ring tone)、呼び出し音(ringback tone)                              |
| Notification  | 発信音、システム状態の発話(バッテリー不足の通知、Bluetooth接続解除の通知など)、通知音、通知発話         |

<div class="note">
  <p><strong>Note!</strong></p>
  <p>Alertとnotificationタイプは、効果音と発話をまとめて1つのオーディオコンテンツとして認識します。例えば、リマインダーの場合、リマインダー音とリマインダー発話が1つのalertオーディオコンテンツとして認識されます。バッテリー不足の通知の場合、発信音と「バッテリーが不足しています」のようなシステム状態の発話が1つのnotificationオーディオコンテンツになります。</p>
</div>

以下のオーディオ再生ルールがあります。

* 物理ボタンの効果音はすぐに再生される必要があります。そのために、ミキシング方式で効果音を出力します。
* オーディオコンテンツは、すぐに再生される必要があります。再生中のオーディオコンテンツがある場合、それをバックグラウンドに処理し、新規のオーディオコンテンツを再生する必要があります。
* ただし、再生中のオーディオコンテンツと新規のオーディオ[コンテンツのタイプ](#AudioInterruptionRule)が同じ場合には、次のように処理します。
  - **Alert、Content、Dialogue、Feedbackタイプ**：再生中のオーディオコンテンツを中断(cancel)し、新規のオーディオコンテンツを再生します。
  - **Notificationタイプ**：現在再生中のオーディオコンテンツを引き続き再生し、新規のオーディオコンテンツを再生キューに追加します。再生中のオーディオコンテンツの再生を完了してから、再生キューに入っている順序通りにオーディオコンテンツを再生します。
* オーディオ再生を中断するときには、現在再生中のオーディオコンテンツから再生を中断します。

以下は、上記のルールに基づいて、オーディオコンテンツのタイプによって再生中のオーディオコンテンツを処理する方法を示します。

<table style="text-align:center">
  <thead>
    <tr>
      <th rowspan="2">再生中のタイプ</th><th colspan="5">新規に再生するタイプ</th><th rowspan="2">物理ボタンの効果音</th>
    </tr>
    <tr>
      <th>Alert</th><th>Content</th><th>Dialogue</th><th>Feedback</th><th>Notification</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Alert</th>
      <td><span class="audioInterruptionRule cancelPlayback">再生中断</span></td>
      <td><span class="audioInterruptionRule backgroundPlay">バックグラウンド処理</span></td>
      <td><span class="audioInterruptionRule backgroundPlay">バックグラウンド処理</span></td>
      <td><span class="audioInterruptionRule backgroundPlay">バックグラウンド処理</span></td>
      <td><span class="audioInterruptionRule backgroundPlay">バックグラウンド処理</span></td>
      <td rowspan="5"><span class="audioInterruptionRule">ミキシング処理</span></td>
    </tr>
    <tr>
      <th>Content</th>
      <td><span class="audioInterruptionRule backgroundPlay">バックグラウンド処理</span></td>
      <td><span class="audioInterruptionRule cancelPlayback">再生中断</span></td>
      <td><span class="audioInterruptionRule backgroundPlay">バックグラウンド処理</span></td>
      <td><span class="audioInterruptionRule backgroundPlay">バックグラウンド処理</span></td>
      <td><span class="audioInterruptionRule backgroundPlay">バックグラウンド処理</span></td>
    </tr>
    <tr>
      <th>Dialogue</th>
      <td><span class="audioInterruptionRule backgroundPlay">バックグラウンド処理</span></td>
      <td><span class="audioInterruptionRule backgroundPlay">バックグラウンド処理</span></td>
      <td><span class="audioInterruptionRule cancelPlayback">再生中断</span></td>
      <td><span class="audioInterruptionRule backgroundPlay">バックグラウンド処理</span></td>
      <td><span class="audioInterruptionRule backgroundPlay">バックグラウンド処理</span></td>
    </tr>
    <tr>
      <th>Feedback</th>
      <td><span class="audioInterruptionRule backgroundPlay">バックグラウンド処理</span></td>
      <td><span class="audioInterruptionRule backgroundPlay">バックグラウンド処理</span></td>
      <td><span class="audioInterruptionRule backgroundPlay">バックグラウンド処理</span></td>
      <td><span class="audioInterruptionRule cancelPlayback">再生中断</span></td>
      <td><span class="audioInterruptionRule backgroundPlay">バックグラウンド処理</span></td>
    </tr>
    <tr>
      <th>Notification</th>
      <td><span class="audioInterruptionRule backgroundPlay">バックグラウンド処理</span></td>
      <td><span class="audioInterruptionRule backgroundPlay">バックグラウンド処理</span></td>
      <td><span class="audioInterruptionRule backgroundPlay">バックグラウンド処理</span></td>
      <td><span class="audioInterruptionRule backgroundPlay">バックグラウンド処理</span></td>
      <td><span class="audioInterruptionRule continuePlayback">引き続き再生(キューに追加)</span></td>
    </tr>
  </tbody>
</table>

### ユーザー発話時のオーディオ再生ルール {#AudioInterruptionRuleForUserUtterance}

クライアントがオーディオコンテンツを再生している途中に、ユーザーが音声入力をしようとする場合、以下のルールに従う必要があります。

* 再生中のオーディオコンテンツがある場合、attending状態からprocessing & reporting状態まで、そのオーディオをバックグラウンドで処理します。
* 音声入力の待機時間を超過したり、ユーザーのリクエストを正常に処理できなかった場合、バックグラウンド処理したオーディオコンテンツを元通りに再生します。
* リクエストの処理結果によって、再生するオーディオコンテンツが異なる場合、[オーディオ再生の基本ルール](#AudioInterruptionRule)に従ってオーディオコンテンツを再生します。
* マルチターンの対話を行う際、追加的にlistening、processing & reportingとなる状態でも上記のルールに従います。

ユーザーの音声入力を聞き取るattending、listening状態で、新規のオーディオコンテンツ再生のリクエストが入ると、次のように処理します。

* **Alert/dialogue/content**タイプのオーディオコンテンツを新規に再生する場合、ユーザーの音声入力の聞き取りをキャンセルして、そのオーディオコンテンツを再生します。
* **Notification**タイプや**Feedback**タイプのオーディオコンテンツを新規に再生する場合、そのオーディオコンテンツをバックグラウンドで再生します。

### 効果音 {#SoundEffect}

クライアントは、デバイスの状態やユーザーのリクエストに対するフィードバックなどを表現するために、[ライト](#Light)と一緒に効果音を提供する必要があります。クライアントがユーザーに提供すべき効果音の種類と状況を説明します。

* [効果音の種類](#SoundEffects)
* [効果音のガイドライン](#SoundEffectGuideline)

#### 効果音の種類 {#SoundEffects}

クライアントの[状態およびイベント](#ClientStateAndEvent)を表現するために、以下のような効果音を提供する必要があります。

| 状態またはイベント              | 効果音のサンプル                     | 必須/任意 |
|---------------------------|------------------------------|:---------:|
| Attending状態になる         | <audio title="Attending" controls><source src="./Resources/Sounds/Clova-Client-Soundeffect-Attending.wav" type="audio/wav" /></audio> | 必須     |
| Error状態になる             | <audio title="Error" controls><source src="./Resources/Sounds/Clova-Client-SoundEffect-Error.wav" type="audio/wav" /></audio>         | 必須     |
| Mute on状態になる           | <audio title="Mute on" controls><source src="./Resources/Sounds/Clova-Client-SoundEffect-Mute_On.wav" type="audio/wav" /></audio>     | 必須     |
| Mute on状態の解除           | <audio title="Mute off" controls><source src="./Resources/Sounds/Clova-Client-SoundEffect-Mute_Off.wav" type="audio/wav" /></audio>   | 必須     |
| アラーム(イベントが発生したときに、効果音をリピート再生する) | <audio title="Alarm" controls><source src="./Resources/Sounds/Clova-Client-SoundEffect-Alarm.wav" type="audio/wav" /></audio>         | 必須     |
| リマインダー(イベントが発生したときに、効果音とリマインダー内容のTTSの順序にリピート再生する) | <audio title="Reminder" controls><source src="./Resources/Sounds/Clova-Client-SoundEffect-Reminder.wav" type="audio/wav" /></audio>         | 必須     |
| タイマー(イベントが発生したときに、効果音をリピート再生する)      | <audio title="Timer" controls><source src="./Resources/Sounds/Clova-Client-SoundEffect-Timer.wav" type="audio/wav" /></audio>         | 必須     |

#### 効果音のガイドライン {#SoundEffectGuideline}

効果音を提供する際に、以下の内容を順守する必要があります。

* 提供されている効果音をそのまま使用することを推奨します。
* 提供されている効果音以外にも、状況またはメーカーのUXポリシーに合わせて、効果音を追加することができます。
* ユーザーが音だけで状況を認知できるようにする必要があります。
* 照明効果や画面の状況に合わせて、一貫した効果音を提供する必要があります。
* ボタンのフィードバックに対する効果音を提供する場合、ボタンの物性と感触にマッチする効果音を提供する必要があります。

### プラットフォームでサポートされている音声圧縮形式 {#SupportedAudioCompressionFormat}

クライアントはClovaから送信されるストリームを再生するので、Clovaでサポートされている音声圧縮形式を再生できる必要があります。

{% include "/Design/SupportedMediaFormat/Supported_Audio_Compression_Format.md" %}

## 画面 {#Screen}

クライアントのディスプレイ装置で、画面に以下のUI項目を提供する必要があります。

* [起動画面](#BootingScreen)
* [ロゴの表示](#DisplayingLogo)
* [Voice agent](#VoiceAgent)

### 起動画面 {#BootingScreen}

デバイスをオンにして、起動が完了するまで表示される画面です。起動画面には主にロゴが表示されます。Clovaのロゴは、他のロゴと組み合わせることなく、単独で画面に表示します。また、ロゴは同じサイズと比率で表示する必要があります。

<ul>
  <li>
    <p><strong>適切な例</strong></p>
    <img src="/Design/Resources/Images/Clova-Client-Partner_Logo_on_Loading_Screen.png" /> <img src="/Design/Resources/Images/Clova-Client-Clova_Logo_on_Loading_Screen.png" />
  </li>
  <li>
    <p><strong>不適切な例</strong></p>
    <img src="/Design/Resources/Images/Clova-Client-Logo_on_Loading_Screen_Bad_Example1.png" /> <img src="/Design/Resources/Images/Clova-Client-Logo_on_Loading_Screen_Bad_Example2.png" /><br/>
    <img src="/Design/Resources/Images/Clova-Client-Logo_on_Loading_Screen_Bad_Example3.png" /> <img src="/Design/Resources/Images/Clova-Client-Logo_on_Loading_Screen_Bad_Example4.png" />
  </li>
</ul>

### ロゴの表示 {#DisplayingLogo}

UI画面に、Clovaのロゴを以下のレイアウトで配置します。

* [ロゴのレイアウトA](#LogoLayoutA)
* [ロゴのレイアウトB](#LogoLayoutB)
* [ロゴのレイアウトC](#LogoLayoutC)

#### ロゴのレイアウトA {#LogoLayoutA}

画面下の一部や全体を覆うUI画面で、Clovaのロゴが左上に配置されます。

![](/Design/Resources/Images/Clova-Client-Logo_Display-Layout_A-Bottom_Overlay.png) ![](/Design/Resources/Images/Clova-Client-Logo_Display-Layout_A-Full_Screen_Overlay.png)

* Clovaのロゴは、左上に配置される必要があります。
* Clovaのロゴは、透明にしない必要があります。

#### ロゴのレイアウトB {#LogoLayoutB}

[ロゴのレイアウトA](#LogoLayoutA)と似たようなレイアウトです。画面下の一部や全体を覆うUI画面で、Clovaのロゴが右上に配置されます。

![](/Design/Resources/Images/Clova-Client-Logo_Display-Layout_B-Bottom_Overlay.png) ![](/Design/Resources/Images/Clova-Client-Logo_Display-Layout_B-Full_Screen_Overlay.png)

* Clovaのロゴは、右上に配置される必要があります。
* Clovaのロゴは、透明にしない必要があります。

#### ロゴのレイアウトC {#LogoLayoutC}

テキスト形式の結果を表現する画面で、Clovaのロゴが上部に配置されるレイアウトです。

![](/Design/Resources/Images/Clova-Client-Logo_Display-Layout_C.png)

* Clovaのロゴは、上部に配置される必要があります。
* コンテンツの提供元は、コンテンツの下に表示される必要があります。


### Voice agent {#VoiceAgent}

Voice agentは、ユーザーの音声入力の聞き取り、Clovaの音声出力など、Clovaの音声動作に関連する状態を表示するUIです。画面を持つクライアントデバイスは、voice agentを表現する必要があります。Voice agentで使用する色と、voice agentのタイプごとに動作および状態を表現する方法を説明します。

* [Voice agentの色](#VoiceAgentColor)
* [バータイプ](#BarType)
* [アイコンAタイプ](#IconAType)
* [アイコンBタイプ](#IconBType)

#### Voice agentの色 {#VoiceAgentColor}

クライアントは、次の色を使用してvoice agentで[クライアントの状態](#ClientStateAndEvent)を表現できる必要があります。

| 色の名称      | RGB値             | 色の名称      | RGB値             |
|--------------|-------------------|--------------|-------------------|
| Green1       | <span style="color:#12D5B2; font-size:150%; vertical-align:middle;">&#9724;</span> 18, 213, 178(#12D5B2)   | Green2       | <span style="color:#05D484; font-size:150%; vertical-align:middle;">&#9724;</span> 5, 212, 132 (#05D484)   |
| Red          | <span style="color:#FF0000; font-size:150%; vertical-align:middle;">&#9724;</span> 255, 0, 0(#FF0000)      | Warm White    | <span style="color:#EEFFFC; font-size:150%; vertical-align:middle;">&#9724;</span> 238, 255, 252(#EEFFFC)  |

#### バータイプ {#BarType}

バータイプのvoice agentは、以下のように長いバーの形で表示され、音声をテキストで表示する領域、状態を表現する色、そしてロゴで構成されます。状況によってアイコンが含まれることがあります。以下は、バータイプのvoice agentが表示された例です。

![](/Design/Resources/Images/Clova-Client-Voice_Agent-Bar_Type.png)

バータイプのvoice agentは、状況によって以下のように表現される必要があります。

| 状態                | アニメーション効果                                                                  | サンプル                                                                             |
|------------------------|------------------------------------------------------------------------------|---------------------------------------------------------------------------------|
| Attending              | Green1のバーが1秒以内にゆっくりと表示されます。                                  | <img style="width:600px" src="/Design/Resources/Images/Clova-Client-Voice_Agent-Bar_Type-Attending.gif" /> |
| Listening                | 声の大きさによって、Warm White、Green2の順に色の領域が拡張されます。      | <img style="width:600px" src="/Design/Resources/Images/Clova-Client-Voice_Agent-Bar_Type-Listening.gif" /> |
| Processing & reporting | Warm Whiteの色の領域が左右に動きます。                                        | <img style="width:600px" src="/Design/Resources/Images/Clova-Client-Voice_Agent-Bar_Type-ProcessingAndReporting.gif" /> |
| Mute on                | Redのバーとミュートまたはマイクアイコンが現れ、2秒後にアイコンが消えます。       | <img style="width:600px" src="/Design/Resources/Images/Clova-Client-Voice_Agent-Bar_Type-MuteOn.gif" /> |
| Error                  | Redのバーとエラーアイコンが現れ、2秒後にアイコンが消えます。                  | <img style="width:600px" src="/Design/Resources/Images/Clova-Client-Voice_Agent-Bar_Type-Error.gif" />  |

<div class="note">
  <p><strong>Note!</strong></p>
  <p>バータイプのUIは、今後内容が更新される予定です。</p>
</div>

#### アイコンAタイプ {#IconAType}

アイコンAタイプのvoice agentは、以下のように左にアイコンの形で表示されます。音声をテキストで表示する領域、状態を表現する色、そしてロゴで構成されます。以下は、アイコンAタイプのvoice agentが表示されたサンプルです。

![](/Design/Resources/Images/Clova-Client-Voice_Agent-Icon_A_Type.png)

アイコンAタイプのvoice agentは、状況によって以下のように表現される必要があります。

| 状態                | アニメーション効果                                                                  | サンプル                                                                              |
|------------------------|------------------------------------------------------------------------------|---------------------------------------------------------------------------------|
| Loading                | Green1の色の円を描いて表示されます。                                          | <img style="width:600px" src="/Design/Resources/Images/Clova-Client-Voice_Agent-Icon_A_Type-Loading.gif" /> |
| Attending              | アニメーション効果のないGreen1の色の円が表示されます。                                   | <img style="width:600px" src="/Design/Resources/Images/Clova-Client-Voice_Agent-Icon_A_Type-Attending.png" /> |
| Listening                | 声の大きさによって、円の下から上に向かってWarm White、Green2の順に色の領域が拡張されます。 | <img style="width:600px" src="/Design/Resources/Images/Clova-Client-Voice_Agent-Icon_A_Type-Listening.gif" /> |
| Processing & reporting | Green2、Warm Whiteの色が円に沿って動きます。                                  | <img style="width:600px" src="/Design/Resources/Images/Clova-Client-Voice_Agent-Icon_A_Type-ProcessingAndReporting.gif" /> |
| Mute on                | Redのミュートまたはマイクアイコンが現れ、「マイクがミュートになっています。」というテキストが表示されます。 | <img style="width:600px" src="/Design/Resources/Images/Clova-Client-Voice_Agent-Icon_A_Type-MuteOn.gif" /> |
| Error                  | Redのエラーアイコンが現れ、エラーを説明する簡単なテキストが表示されます。            | <img style="width:600px" src="/Design/Resources/Images/Clova-Client-Voice_Agent-Icon_A_Type-Error.gif" /> |

<div class="note">
  <p><strong>Note!</strong></p>
  <p>Loading状態は、ユーザーの入力を聞き取るために<a href="#VoiceAgent">voice agent</a>を準備する状態です。画面を持つデバイスにのみ適用される状態で、voice agentのグラフィックを表現するために準備する状況を表現する必要があります。</p>
</div>

#### アイコンBタイプ {#IconBType}

アイコンBタイプは、アプリタイプのクライアント、つまりモバイルデバイスでvoice agentを表現するときに使用されます。以下は、アイコンBタイプのvoice agentが表示されたサンプルです。

![](/Design/Resources/Images/Clova-Client-Voice_Agent-Icon_B_Type.png)

アイコンBタイプのvoice agentは、状況によって以下のように表現される必要があります。

| 状態                  | アニメーション効果                                                                | サンプル       |
|--------------------------|----------------------------------------------------------------------------|-----------|
| Idle                     | アニメーション効果のないWarm Whiteの色のアイコンを表示します。                           | ![](/Design/Resources/Images/Clova-Client-Voice_Agent-Icon_B_Type-Idle.png) |
| Loading                  | Green1の色がアイコンを囲む円を描いて表示されます。                            | ![](/Design/Resources/Images/Clova-Client-Voice_Agent-Icon_B_Type-Loading.gif) |
| Attending                | アニメーション効果のないGreen1の円が表示されます。                                                      | ![](/Design/Resources/Images/Clova-Client-Voice_Agent-Icon_B_Type-Attending.png) |
| Listening                  | Warm White、Green2の色の順に表示された領域が、Green1の色の円の上で、円を描いて表示されます。                 | ![](/Design/Resources/Images/Clova-Client-Voice_Agent-Icon_B_Type-Listening.gif) |
| Processing & reporting   | Warm White、Green2の色の順に、アイコンを囲む円を描いて表示されます。                                     | ![](/Design/Resources/Images/Clova-Client-Voice_Agent-Icon_B_Type-ProcessingAndReporting.gif) |
| Mute on                  | Redのミュートまたはマイクアイコンが表示されます。                                                     | ![](/Design/Resources/Images/Clova-Client-Voice_Agent-Icon_B_Type-MuteOn.gif) |
| Error                    | Redのエラーアイコンが表示されます。                                                                | ![](/Design/Resources/Images/Clova-Client-Voice_Agent-Icon_B_Type-Error.gif) |

<div class="note">
  <p><strong>Note!</strong></p>
  <p>Loading状態は、ユーザーの入力を聞き取るために<a href="#VoiceAgent">voice agent</a>を準備する状態です。画面を持つデバイスにのみ適用される状態で、voice agentのグラフィックを表現するために準備する状況を表現する必要があります。</p>
</div>
