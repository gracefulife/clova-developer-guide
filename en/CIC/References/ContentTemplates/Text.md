# Text template

The Text template is used in providing text for the client to display on the client's screen.
The name of the template fields provides style information as to how the text is composed or displayed.
For example, the given text may consist of a number of paragraphs or is to be displayed as a series of tables.

<div class="note">
<p><strong>Note!</strong></p>
<p>See <a href="#UIExample">UI example</a>s of the Text template used in display.</p>
</div>

## Template fields

| Field name       | Type    | Description                     |
|---------------|---------|-----------------------------|
| `bgUrl`                  | [URLObject](/CIC/References/ContentTemplates/Shared_Objects.md#URLObject)       | The URL of the image to display in the background. An empty string (`""`) indicates that background image information is unavailable.             |
| `emotionCode`            | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject) | The code for Clova's emotion for the client to _"express"_. If the client does not support emotional expression, ignore this field. <div class="note"><p><strong>Note!</strong></p><p>Contact us to find more about the emotion code specification.</p></div> |
| `highlightText`          | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject) or [NumberObject](/CIC/References/ContentTemplates/Shared_Objects.md#NumberObject) | Contains a text or number to be displayed with an emphasis. The number may contain commas as thousand separators. An empty string (`""`) or `null` indicates that there is no text or number to display with an emphasis. |
| `imageUrl`               | [URLObject](/CIC/References/ContentTemplates/Shared_Objects.md#URLObject)       | The URL of the image. An empty string (`""`) indicates that image is unavailable.               |
| `linkUrl`                | [URLObject](/CIC/References/ContentTemplates/Shared_Objects.md#URLObject)  | The URL to a Web map, _if_ this template contains an image of a map. An empty string (`""`) indicates that a URL to a Web map is unavailable. |
| `mainText`               | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject) | Contains the main text to display. An empty string (`""`) indicates that this information is unavailable.                     |
| `motionCode`             | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject) | The code for a motion for the client to perform. If the client does not support motions, ignore this field. <div class="note"><p><strong>Note!</strong></p><p>Contact us to find more about the motion code specification.</p></div> |
| `paragraphText`          | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject) | Contains paragraphs to display. An empty string (`""`) indicates that paragraphical text is unavailable. |
| `referenceText`          | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject) | The name or description of the source of the content. An empty string (`""`) indicates that source information is unavailable.                               |
| `referenceURL`           | [URLObject](/CIC/References/ContentTemplates/Shared_Objects.md#URLObject)       | The URL of the content source. An empty string (`""`) indicates that source information is unavailable.                      |
| `sentenceText`           | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject) | Contains a sentence to display. |
| `subText`                | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject) | Contains supplementary text to display. An empty string (`""`) indicates that supplementary text is unavailable. |
| `tableList[]`           | object array                                                                    | Contains text units to be displayed in tables. All tables consist of a single column and two or three rows.    |
| `tableList[].item1`     | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject) | The text for the first row. An empty string (`""`) indicates that the first row is empty or no text is to be presented in a table.   |
| `tableList[].item2`     | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject) | The text for the second row. An empty string (`""`) indicates that the second row is empty or no text is to be presented in a table.  |
| `tableList[].item2Link` | [URLObject](/CIC/References/ContentTemplates/Shared_Objects.md#URLObject) or [PhoneNumberObject](/CIC/References/ContentTemplates/Shared_Objects.md#PhoneNumberObject) | The link or phone number for the text in the second row. An empty string (`""`) indicates that this information is unavailable. |
| `tableList[].item3`     | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject) | The text for the third row. This field is omissible. |
| `type`                   | string                                                                          | The type of this template. The value is always `"Text"`.             |

## Template example

{% raw %}

```json
// Example 1
// User asks the rate for a US dollar (The text is to be displayed as emphasized)
{
  "actionList": [
    {
      "type": "action",
      "value": ""
    }
  ],
  "bgUrl": {
    "type": "url",
    "value": ""
  },
  "highlightText": {
    "type": "number",
    "value": "1,119"
  },
  "mainText": {
    "type": "string",
    "value": "Won"
  },
  "paragraphText": {
    "type": "string",
    "value": ""
  },
  "referenceText": {
    "type": "string",
    "value": "LINE Bank"
  },
  "referenceUrl": {
    "type": "url",
    "value": "https://m.search.naver.com/search.naver?where=m&sm=mob_lic&query=2%3%9&34"
  },
  "sentenceText": {
    "type": "string",
    "value": ""
  },
  "subText": {
    "type": "string",
    "value": "-0.13%"
  },
  "tableList": [
    {
      "item1": {
        "type": "string",
        "value": ""
      },
      "item2": {
        "type": "string",
        "value": ""
      },
      "item2Link": {
        "type": "",
        "value": ""
      }
    }
  ],
  "emotionCode": {
    "type": "string",
    "value": ""
  },
  "motionCode": {
    "type": "string",
    "value": ""
  },
  "type": "Text"
}

// Example 2
// User asks who the Tottenham manager is. (The text is to be displayed as paragraphs)
{
  "actionList": [
    {
      "type": "action",
      "value": ""
    }
  ],
  "bgUrl": {
    "type": "url",
    "value": ""
  },
  "highlightText": {
    "type": "string",
    "value": ""
  },
  "mainText": {
    "type": "string",
    "value": ""
  },
  "paragraphText": {
    "type": "string",
    "value": "Tottenham Hotspur FC Manager\n Mauricio Pochettino"
  },
  "referenceText": {
    "type": "string",
    "value": "NAVER search result"
  },
  "referenceUrl": {
    "type": "url",
    "value": "https://m.search.naver.com/search.naver?where=m&sm=mob_lic&query=%ed%86%a0%ed%8a%b8%eb%84%98+%ea%b0%90%eb%8f%85%ec%9d%b4+%eb%88%84%ea%b5%ac%ec%95%bc?"
  },
  "sentenceText": {
    "type": "string",
    "value": ""
  },
  "subText": {
    "type": "string",
    "value": ""
  },
  "tableList": [
    {
      "item1": {
        "type": "string",
        "value": ""
      },
      "item2": {
        "type": "string",
        "value": ""
      },
      "item2Link": {
        "type": "",
        "value": ""
      }
    }
  ],
  "emotionCode": {
    "type": "string",
    "value": ""
  },
  "motionCode": {
    "type": "string",
    "value": ""
  },
  "type": "Text"
}

// Example 3
// User requests for phone numbers for flower shops. (The text is to be displayed tables)
{
  "actionList": [
    {
      "type": "action",
      "value": ""
    }
  ],
  "bgUrl": {
    "type": "url",
    "value": ""
  },
  "highlightText": {
    "type": "string",
    "value": ""
  },
  "mainText": {
    "type": "string",
    "value": ""
  },
  "paragraphText": {
    "type": "string",
    "value": ""
  },
  "referenceText": {
    "type": "string",
    "value": "NAVER search result"
  },
  "referenceUrl": {
    "type": "url",
    "value": "https://m.search.naver.com/search.naver?where=m&sm=mob_lic&query=%ea%bd%83%ec%a7%91"
  },
  "sentenceText": {
    "type": "string",
    "value": ""
  },
  "subText": {
    "type": "string",
    "value": ""
  },
  "tableList": [
    {
      "item1": {
        "type": "string",
        "value": "Sally Flowers Shinjuku branch"
      },
      "item2": {
        "type": "string",
        "value": "03-1234-5678"
      },
      "item2Link": {
        "type": "phoneNum",
        "value": "03-1234-5678"
      }
    },
    {
      "item1": {
        "type": "string",
        "value": "Super Brown's Super Flowers"
      },
      "item2": {
        "type": "string",
        "value": "03-9876-5432"
      },
      "item2Link": {
        "type": "phoneNum",
        "value": "03-9876-5432"
      }
    },
    ...
  ],
  "emotionCode": {
    "type": "string",
    "value": ""
  },
  "motionCode": {
    "type": "string",
    "value": ""
  },
  "type": "Text"
}

// Example 4
// User apologizes. (Client is to display the text and express emotion)
{
  "actionList": [
    {
      "type": "action",
      "value": ""
    }
  ],
  "bgUrl": {
    "type": "url",
    "value": ""
  },
  "highlightText": {
    "type": "string",
    "value": ""
  },
  "mainText": {
    "type": "string",
    "value": ""
  },
  "paragraphText": {
    "type": "string",
    "value": "You have nothing to be sorry about."
  },
  "referenceText": {
    "type": "string",
    "value": ""
  },
  "referenceUrl": {
    "type": "url",
    "value": ""
  },
  "sentenceText": {
    "type": "string",
    "value": ""
  },
  "subText": {
    "type": "string",
    "value": ""
  },
  "tableList": [
    {
      "item1": {
        "type": "string",
        "value": ""
      },
      "item2": {
        "type": "string",
        "value": ""
      },
      "item2Link": {
        "type": "",
        "value": ""
      }
    }
  ],
  "emotionCode": {
    "type": "string",
    "value": "EmotionCode7"
  },
  "motionCode": {
    "type": "string",
    "value": ""
  },
  "type": "Text"
}

// Example 5
// User asks the client to dance. (Motion)
{
  "actionList": [
    {
      "type": "action",
      "value": ""
    }
  ],
  "bgUrl": {
    "type": "url",
    "value": ""
  },
  "highlightText": {
    "type": "string",
    "value": ""
  },
  "mainText": {
    "type": "string",
    "value": ""
  },
  "paragraphText": {
    "type": "string",
    "value": "It's out my scope."
  },
  "referenceText": {
    "type": "string",
    "value": ""
  },
  "referenceUrl": {
    "type": "url",
    "value": ""
  },
  "sentenceText": {
    "type": "string",
    "value": ""
  },
  "subText": {
    "type": "string",
    "value": ""
  },
  "tableList": [
    {
      "item1": {
        "type": "string",
        "value": ""
      },
      "item2": {
        "type": "string",
        "value": ""
      },
      "item2Link": {
        "type": "",
        "value": ""
      }
    }
  ],
  "emotionCode": {
    "type": "string",
    "value": ""
  },
  "motionCode": {
    "type": "string",
    "value": "MotionDance"
  },
  "type": "Text"
}
```

{% endraw %}

## UI example {#UIExample}

The following examples show how the Text template is used on the Clova app distributed by {{ book.OrientedService }}.

| Text with emphasis | Paragraph | Table |
|:-------:|:-------:|:-------:|
| ![Highlight](/CIC/Resources/Images/Content_Template-Highlight_Text.png) | ![Paragraph](/CIC/Resources/Images/Content_Template-Paragragh_Text.png) | ![Table](/CIC/Resources/Images/Content_Template-Table_Text.png) |

## See also

* [CardList](/CIC/References/ContentTemplates/CardList.md)
* [ImageList](/CIC/References/ContentTemplates/ImageList.md)
* [ImageText](/CIC/References/ContentTemplates/ImageText.md)
* [Popup](/CIC/References/ContentTemplates/Popup.md)
