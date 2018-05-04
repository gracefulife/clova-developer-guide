# Text Template
The Text template is used in providing text for the client to display on the client screen. The name of the template fields provides style information about how the text is composed or displayed. For example, the given text may consist of a number of paragraphs or is to be displayed as a series of tables.

<div class="note">
<p><strong>Note!</strong></p>
<p>See <a href="#UIExample">UI examples</a> of the Text template used in display.</p>
</div>

## Template fields

| Field name       | Data type    | Description                     |
|---------------|---------|-----------------------------|
| `bgUrl`                  | [URLObject](/CIC/References/ContentTemplates/Shared_Objects.md#URLObject)       | The URL of the image to display in the background. An empty string (`""`) indicates that no content is to be displayed.               |
| `emotionCode`            | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject) | The code of Clova emotions for the client to "express." You can display the emotions predefined on the client device using emotion code. If the client does not support emotional expression, ignore this field. <div class="note"><p><strong>Note!</strong></p><p>For more information on the specification of the emotion codes, contact your Partnership Manager.</p></div> |
| `highlightText`          | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject) or [NumberObject](/CIC/References/ContentTemplates/Shared_Objects.md#NumberObject) | The text or a number to be displayed with an emphasis. The number may contain commas as thousand separators. The `value` field of this object array element may have an empty string (`""`) or a `null` value. |
| `imageUrl`               | [URLObject](/CIC/References/ContentTemplates/Shared_Objects.md#URLObject)       | The URL of the image. An empty string (`""`) indicates that no content is to be displayed.                              |
| `linkUrl`                | [URLObject](/CIC/References/ContentTemplates/Shared_Objects.md#URLObject)       | The URL to a web map, if a map image is included. An empty string (`""`) indicates that no content is to be displayed. |
| `mainText`               | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject) | The main text to display. An empty string (`""`) indicates that no content is to be displayed.                                     |
| `motionCode`             | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject) | The code for the action of the client to perform. You can make the client perform predefined actions using the action codes. If the client does not support an action feature, ignore this field. <div class="note"><p><strong>Note!</strong></p><p> For more information on the specification of the action codes, contact your Partnership Manager.</p></div> |
| `paragraphText`          | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject) | The text to display in a paragraph format. An empty string (`""`) indicates that no content is to be displayed.                                |
| `referenceText`          | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject) | The information of the referred service. An empty string (`""`) indicates that no content is to be displayed.  |
| `referenceUrl`           | [URLObject](/CIC/References/ContentTemplates/Shared_Objects.md#URLObject)       | The information on the usage result URL of the referred service. An empty string (`""`) indicates that no content is to be displayed.   |
| `sentenceText`           | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject) | The text to display in a sentence format. An empty string (`""`) indicates that no content is to be displayed.                                |
| `subText`                | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject) | The supplementary text to display. An empty string (`""`) indicates that no content is to be displayed.                                     |
| `tableList[]`           | object array                                                                    | The text to display in a table format. All tables consist of a single column and two or three rows.     |
| `tableList[].item1`     | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject) | The text to display in the first row. An empty string (`""`) indicates that no content is to be displayed.                    |
| `tableList[].item2`     | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject) | The text to display in the second row. An empty string (`""`) indicates that no content is to be displayed.                    |
| `tableList[].item2Link` | [URLObject](/CIC/References/ContentTemplates/Shared_Objects.md#URLObject) or [PhoneNumberObject](/CIC/References/ContentTemplates/Shared_Objects.md#PhoneNumberObject) | The URL link for the text displayed in the second row or phone number. An empty string (`""`) indicates that no content is to be displayed. |
| `tableList[].item3`     | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject) | The text to display in the third row. This field is omissible. |
| `type`                   | string                                                                          | The type of this template. The value is always `"Text"`.             |

## Template example

{% raw %}

```json
// Example 1.
// User request: How much does one dollar worth now? (The text is to be displayed as emphasized)
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
    "value": "https://m.search.contentproviderdomain.com/search?where=m&sm=mob_lic&query=1%eb%8b%ac%eb%9f%ac+%ed%99%98%ec%9c%a8"
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

// Example 2.
// User request: Who is the manager of Tottenham? (The text is to be displayed as paragraphs)
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
    "value": "Tottenham Hotspur F.C. Manager\n Mauricio Pochettino"
  },
  "referenceText": {
    "type": "string",
    "value": "NAVER search result"
  },
  "referenceUrl": {
    "type": "url",
    "value": "https://m.search.contentproviderdomain.com/search?where=m&sm=mob_lic&query=%ed%86%a0%ed%8a%b8%eb%84%98+%ea%b0%90%eb%8f%85%ec%9d%b4+%eb%88%84%ea%b5%ac%ec%95%bc?"
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

// Example 3.
// User request: Tell me the phone numbers for flower shops. (The text is to be displayed tables)
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
    "value": "https://m.search.contentproviderdomain.com/search?where=m&sm=mob_lic&query=%ea%bd%83%ec%a7%91"
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
        "value": "031-716-6676"
      },
      "item2Link": {
        "type": "phoneNum",
        "value": "031-716-6676"
      }
    },
    {
      "item1": {
        "type": "string",
        "value": "Super Brown's Super Flowers"
      },
      "item2": {
        "type": "string",
        "value": "031-712-3310"
      },
      "item2Link": {
        "type": "phoneNum",
        "value": "031-712-3310"
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

// Example 4.
// User request: Sorry. (Client is to display the text and express emotion)

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

// Example 5.
// User request: Dance for me. (Motion)

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
    "value": "MotionDance"
  },
  "motionCode": {
    "type": "string",
    "value": ""
  },
  "type": "Text"
}
```

{% endraw %}

## UI example {#UIExample}
The following examples show how the Text template is used on the Clova app distributed by {{ book.OrientedService }}.

| Text with emphasis | Text in paragraphs | Text in a table |
|-------|-------|-------|
| ![Highlight](/CIC/Resources/Images/Content_Template-Highlight_Text.png) | ![Paragraph](/CIC/Resources/Images/Content_Template-Paragragh_Text.png) | ![Table](/CIC/Resources/Images/Content_Template-Table_Text.png) |

## See also
* [CardList](/CIC/References/ContentTemplates/CardList.md)
* [ImageList](/CIC/References/ContentTemplates/ImageList.md)
* [ImageText](/CIC/References/ContentTemplates/ImageText.md)
* [Popup](/CIC/References/ContentTemplates/Popup.md)
