# Popup template

The Popup template is used in providing popup information for the client to display on the client's screen. Various popup types are supported including toast and alert. Depending on the popup type, valid fields of the template vary.

| Popup Type       | Description                      | Valid fields                         |
|---------------|-----------------------------|-----------------------------|
| Toast         | A toast consisting of links and text.    | `toastLinkText`, `toastLinkUrl`, `toastText`                  |
| Alert         | An alert consisting of text and a confirmation button.   | `alertText`                                                   |
| Popup (Single button) | A popup consisting of a title, text and a button (link). | `mainText`, `positiveButtonText`, `positiveButtonUrl`, `titleText`   |
| Popup (Two buttons) | A popup consisting of a title, text and two buttons. | `negativeButtonText`, `negativeButtonUrl`, `mainText`, `positiveButtonText`, `positiveButtonUrl`, `titleText` |

<div class="note">
<p><strong>Note!</strong></p>
<p>See <a href="#UIExample">UI examples</a> of the Popup template used in display.</p>
</div>

## Template fields

| Field name       | Type    | Description                     |
|---------------|---------|-----------------------------|
| `alertText`        | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject) | The warning message for an alert. An empty string (`""`) indicates that the popup is not an alert. |
| `displayType`      | string                                                                          | The type of this popup. Available types  are:<ul><li><code>"POPUP"</code></li><li><code>"ALERT"</code></li><li><code>"TOAST"</code></li></ul>  |
| `negativeButtonText`   | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject) | The button label which carries a negative meaning such as `"No"`. An empty string (`""`) indicates that this popup has no "negative button" to display.  |
| `negativeButtonUrl`    | [URLObject](/CIC/References/ContentTemplates/Shared_Objects.md#URLObject)  | The URL to open when the "negative button" is tapped. An empty string (`""`) indicates that this information is unavailable. |
|  `mainText`        | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject) | The main text to display on this popup. An empty string (`""`) indicates that this information is unavailable.  |
| `positiveButtonText`  | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject) | The button label which carries a positive meaning such as `"Yes"` or `"Confirm"`. An empty string (`""`) indicates that this information is unavailable. |
| `positiveButtonUrl`   | [URLObject](/CIC/References/ContentTemplates/Shared_Objects.md#URLObject)       | The URL to open when the "positive button" is tapped. An empty string (`""`) indicates that this popup has no "positive button" to display.  |
| `title`            | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject) | The title of this popup. An empty string (`""`) indicates that this popup has no title.  |
| `toastLinkText`    | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject) | The link text to display on this toast. An empty string (`""`) indicates that this toast has no link text to display.  |
| `toastLinkUrl`     | [URLObject](/CIC/References/ContentTemplates/Shared_Objects.md#URLObject)       | The URL of the link to display on this toast. An empty string (`""`) indicates that this toast has no link to display. |
| `toastText`        | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject) | The text to display on this toast. An empty string (`""`) indicates that this toast has no text to display.  |
| `type`             | string                                                                          | The type of this template. The value is always `"Popup"`.     |

## Template example

{% raw %}
```json
// Example 1. Toast type
{
  "type": "Popup",
  "displayType": "TOAST",
  "toastText": {
    "type": "string",
    "value": "The 1 minute service is on. Teach Clova about your music taste and get a coupon for 100 songs on NAVER Music!"
  },
  "toastLinkText": {
    "type": "string",
    "value": "Learn more >"
  },
  "toastLinkUrl": {
    "type": "url",
    "value": "https://..."
  },
  "alertText": {
    "type": "string",
    "value": ""
  },
  "titleText": {
    "type": "string",
    "value": ""
  },
  "mainText": {
    "type": "string",
    "value": ""
  },
  "negativeButtonText": {
    "type": "string",
    "value": ""
  },
  "negativeButtonUrl": {
    "type": "url",
    "value": ""
  },
  "positiveButtonText": {
    "type": "string",
    "value": ""
  },
  "positiveButtonUrl": {
    "type": "url",
    "value": ""
  }
}

// Example 2. Alert type
{
  "type": "Popup",
  "displayType": "ALERT",
  "toastText": {
    "type": "string",
    "value": ""
  },
  "toastLinkText": {
    "type": "string",
    "value": ""
  },
  "toastLinkUrl": {
    "type": "url",
    "value": ""
  },
  "alertText": {
    "type": "string",
    "value": "Terminating the music. Another client has started playing the music."
  },
  "titleText": {
    "type": "string",
    "value": ""
  },
  "mainText": {
    "type": "string",
    "value": ""
  },
  "negativeButtonText": {
    "type": "string",
    "value": ""
  },
  "negativeButtonUrl": {
    "type": "url",
    "value": ""
  },
  "positiveButtonText": {
    "type": "string",
    "value": ""
  },
  "positiveButtonUrl": {
    "type": "url",
    "value": ""
  }
}

// Example 3. Popup type with a single button
{
  "type": "Popup",
  "displayType": "POPUP",
  "toastText": {
    "type": "string",
    "value": ""
  },
  "toastLinkText": {
    "type": "string",
    "value": ""
  },
  "toastLinkUrl": {
    "type": "url",
    "value": ""
  },
  "alertText": {
    "type": "string",
    "value": ""
  },
  "titleText": {
    "type": "string",
    "value": "Clova now knows your music taste!"
  },
  "mainText": {
    "type": "string",
    "value": "Enjoy Clova's recommendations with the NAVER Music coupon for 100 free songs!"
  },
  "negativeButtonText": {
    "type": "string",
    "value": ""
  },
  "negativeButtonUrl": {
    "type": "url",
    "value": ""
  },
  "positiveButtonText": {
    "type": "string",
    "value": "Get Music coupon"
  },
  "positiveButtonUrl": {
    "type": "url",
    "value": "https://..."
  }
}

// Example 4. Popup type with two buttons
{
  "type": "Popup",
  "displayType": "POPUP",
  "toastText": {
    "type": "string",
    "value": ""
  },
  "toastLinkText": {
    "type": "string",
    "value": ""
  },
  "toastLinkUrl": {
    "type": "url",
    "value": ""
  },
  "alertText": {
    "type": "string",
    "value": ""
  },
  "titleText": {
    "type": "string",
    "value": "Clova now knows your music taste!"
  },
  "mainText": {
    "type": "string",
    "value": "I can give you better recommendations now that I know your taste"
  },
  "negativeButtonText": {
    "type": "string",
    "value": "Continue"
  },
  "negativeButtonUrl": {
    "type": "url",
    "value": "https://..."
  },
  "positiveButtonText": {
    "type": "string",
    "value": "OK"
  },
  "positiveButtonUrl": {
    "type": "url",
    "value": "https://..."
  }
}
```
{% endraw %}

## UI example {#UIExample}

The following examples show how the Popup template is used on the Clova app distributed by {{ book.OrientedService }}.

| Toast | Alert |
|:-----------:|:-----------:|
| ![Type1](/CIC/Resources/Images/Content-Template-Toast.png) | ![Type2](/CIC/Resources/Images/Content-Template-Alert.png) |

| Popup (Single button) | Popup (Two buttons) |
|:-------------------:|:--------------------:|
| ![Type3](/CIC/Resources/Images/Content-Template-Popup_with_One_Button.png) | ![Type](/CIC/Resources/Images/Content-Template-Popup_with_Two_Buttons.png) |

## See also

* [CardList](/CIC/References/ContentTemplates/CardList.md)
* [ImageList](/CIC/References/ContentTemplates/ImageList.md)
* [ImageText](/CIC/References/ContentTemplates/ImageText.md)
* [Text](/CIC/References/ContentTemplates/Text.md)
