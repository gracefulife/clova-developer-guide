# Popup template
Provides texts or buttons displaying toast, alert and popup. Depending on the display format, valid fields may vary.

| Display format       | Description                      | Valid fields                         |
|---------------|-----------------------------|-----------------------------|
| Toast         | A toast comprised of links related to sentences.     | `toastLinkText`, `toastLinkUrl`, `toastText`                  |
| Alert         | An alert comprised of sentences and a check button.    | `alertText`                                                   |
| Popup(One button) | A popup comprised of a title, sentences and a button (link). | `mainText`, `positiveButtonText`, `positiveButtonUrl`, `titleText`   |
| Popup (Two buttons) | A popup comprised of a title, sentences and two buttons. | `negativeButtonText`, `negativeButtonUrl`, `mainText`, `positiveButtonText`, `positiveButtonUrl`, `titleText` |

<div class="note">
<p><strong>Note!</strong></p>
<p>See <a href="#UIExample">Screen UI example</a> for available display formats of the Popup template.</p>
</div>

## Template field

| Field name       | Type    | Field description                     |
|---------------|---------|-----------------------------|
| `alertText`        | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject) | An object containing a warning message displayed on the Alert. The `value` field of this object can have an empty string (`""`). |
| `displayType`      | string                                                                          | Types of display. Available values are:<ul><li><code>"POPUP"</code></li><li><code>"ALERT"</code></li><li><code>"TOAST"</code></li></ul>  |
| `negativeButtonText`   | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject) | An object containing negative texts such as **No** displayed on the Popup. The `value` field of this object can have an empty string (`""`). |
| `negativeButtonUrl`    | [URLObject](/CIC/References/ContentTemplates/Shared_Objects.md#URLObject)       | An object containing URL connected to a button with negative texts such as **No** displayed on the Popup. The `value` field of this object can have an empty string (`""`). |
|  `mainText`        | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject) | An object containing texts displayed on the Popup. The `value` field of this object can have an empty string (`""`). |
| `positiveButtonText`  | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject) | An object containing positive texts such as **Yes** displayed on the Popup. Use this object to display texts such as **Check** on the button in case it is the Popup with a single button. The `value` field of this object can have an empty string (`""`). |
| `positiveButtonUrl`   | [URLObject](/CIC/References/ContentTemplates/Shared_Objects.md#URLObject)       | An object containing URL connected to a button with positive texts such as **Yes** displayed on the Popup. Use this object to URL connected to a button meaning **Check** in case it is the Popup with a single button. The `value` field of this object can have an empty string (`""`). |
| `title`            | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject) | An object containing a title displayed on the Popup. The `value` field of this object can have an empty string (`""`). |
| `toastLinkText`    | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject) | An object containing link texts displayed on the Toast. The `value` field of this object can have an empty string (`""`). |
| `toastLinkUrl`     | [URLObject](/CIC/References/ContentTemplates/Shared_Objects.md#URLObject)       | An object containing URL link displayed on the Toast. The `value` field of this object can have an empty string (`""`). |
| `toastText`        | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject) | An object containing texts displayed on the Toast. The `value` field of this object can have an empty string (`""`). |
| `type`             | string                                                                          | A content template delimiter. It has an `"Popup"` value.     |

## Template example

{% raw %}
```json
// Example 1. Toast type
{
  "type" : "Popup",
  "displayType" : "TOAST",
  "toastText" : {
    "type" : "string",
    "value" : "1분 미리듣기 중입니다. 음악 취향 길들이기에 참여하고 네이버 뮤직 100곡 이용권 받으세요!"
  },
  "toastLinkText" : {
    "type" : "string",
    "value" : "이벤트 참여 >"
  },
  "toastLinkUrl" : {
    "type" : "url",
    "value" : "https://..."
  },
  "alertText" : {
    "type" : "string",
    "value" : ""
  },
  "titleText" : {
    "type" : "string",
    "value" : ""
  },
  "mainText" : {
    "type" : "string",
    "value" : ""
  },
  "negativeButtonText" : {
    "type" : "string",
    "value" : ""
  },
  "negativeButtonUrl" : {
    "type" : "url",
    "value" : ""
  },
  "positiveButtonText" : {
    "type" : "string",
    "value" : ""
  },
  "positiveButtonUrl" : {
    "type" : "url",
    "value" : ""
  }
}

// Example 2. Alert type
{
  "type" : "Popup",
  "displayType" : "ALERT",
  "toastText" : {
    "type" : "string",
    "value" : ""
  },
  "toastLinkText" : {
    "type" : "string",
    "value" : ""
  },
  "toastLinkUrl" : {
    "type" : "url",
    "value" : ""
  },
  "alertText" : {
    "type" : "string",
    "value" : "다른 기기에서 재생을 시작하여 음악이 중지되었습니다."
  },
  "titleText" : {
    "type" : "string",
    "value" : ""
  },
  "mainText" : {
    "type" : "string",
    "value" : ""
  },
  "negativeButtonText" : {
    "type" : "string",
    "value" : ""
  },
  "negativeButtonUrl" : {
    "type" : "url",
    "value" : ""
  },
  "positiveButtonText" : {
    "type" : "string",
    "value" : ""
  },
  "positiveButtonUrl" : {
    "type" : "url",
    "value" : ""
  }
}

// Example 3. Popup type with one button
{
  "type" : "Popup",
  "displayType" : "POPUP",
  "toastText" : {
    "type" : "string",
    "value" : ""
  },
  "toastLinkText" : {
    "type" : "string",
    "value" : ""
  },
  "toastLinkUrl" : {
    "type" : "url",
    "value" : ""
  },
  "alertText" : {
    "type" : "string",
    "value" : ""
  },
  "titleText" : {
    "type" : "string",
    "value" : "취향파악 완료!"
  },
  "mainText" : {
    "type" : "string",
    "value" : "이제 네이버 뮤직 100곡 무료 이용권으로 클로바의 추천 음악을 즐기세요!"
  },
  "negativeButtonText" : {
    "type" : "string",
    "value" : ""
  },
  "negativeButtonUrl" : {
    "type" : "url",
    "value" : ""
  },
  "positiveButtonText" : {
    "type" : "string",
    "value" : "뮤직 이용권 받기"
  },
  "positiveButtonUrl" : {
    "type" : "url",
    "value" : "https://..."
  }
}

// Example 4. Popup type with two buttons
{
  "type" : "Popup",
  "displayType" : "POPUP",
  "toastText" : {
    "type" : "string",
    "value" : ""
  },
  "toastLinkText" : {
    "type" : "string",
    "value" : ""
  },
  "toastLinkUrl" : {
    "type" : "url",
    "value" : ""
  },
  "alertText" : {
    "type" : "string",
    "value" : ""
  },
  "titleText" : {
    "type" : "string",
    "value" : "취향파악 완료!"
  },
  "mainText" : {
    "type" : "string",
    "value" : "고객님의 음악 취향을 알게되어서 추천을 더 잘할 수 있겠어요."
  },
  "negativeButtonText" : {
    "type" : "string",
    "value" : "계속"
  },
  "negativeButtonUrl" : {
    "type" : "url",
    "value" : "https://..."
  },
  "positiveButtonText" : {
    "type" : "string",
    "value" : "종료"
  },
  "positiveButtonUrl" : {
    "type" : "url",
    "value" : "https://..."
  }
}
```
{% endraw %}

## Screen UI example {#UIExample}
The following example shows how the Popup template is presented in the Clova mobile app distributed by {{ book.OrientedService }}.

| Toast format | Alert format |
|-----------|-----------|
| ![Type1](/CIC/Resources/Images/Content-Template-Toast.png) | ![Type2](/CIC/Resources/Images/Content-Template-Alert.png) |

| Popup format (One button) | Popup format (Two buttons) |
|-------------------|--------------------|
| ![Type3](/CIC/Resources/Images/Content-Template-Popup_with_One_Button.png) | ![Type](/CIC/Resources/Images/Content-Template-Popup_with_Two_Buttons.png) |

## See also
* [CardList](/CIC/References/ContentTemplates/CardList.md)
* [ImageList](/CIC/References/ContentTemplates/ImageList.md)
* [ImageText](/CIC/References/ContentTemplates/ImageText.md)
* [Text](/CIC/References/ContentTemplates/Text.md)
