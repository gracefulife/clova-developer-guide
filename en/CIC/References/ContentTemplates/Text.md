# Text Template
This template is used to display text data. It can display highlighted text, paragraph text, or table text.

<div class="note">
<p><strong>Note!</strong></p>
<p>See <a href="#UIExample">Screen UI example</a> for the available display formats of the Text template.</p>
</div>

## Template field

| Field name  | Type  | Field description  | Required |
|---------------|---------|-----------------------------|---------|
| bgUrl  | [URLObject](/CIC/References/ContentTemplates/Shared_Objects.md#URLObject)  | The object containing the URL of the image to display in background  | No |
| highlightText  | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject) or [NumberObject](/CIC/References/ContentTemplates/Shared_Objects.md#NumberObject) | When the object contains text or number to highlight, you may add a digit grouping symbol to the number.  | No |
| imageUrl  | [URLObject](/CIC/References/ContentTemplates/Shared_Objects.md#URLObject)  | The object containing the URL of the image  | No |
| linkUrl  | [URLObject](/CIC/References/ContentTemplates/Shared_Objects.md#URLObject)  | The object containing the URL which redirects to a web map when a map image is included | No |
| mainText  | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject) | The object containing the main text  | No |
| paragraphText  | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject) | The object containing the paragraph-type text  | No |
| referenceText  | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject) | The object containing the text information of the source  | No |
| referenceURL  | [URLObject](/CIC/References/ContentTemplates/Shared_Objects.md#URLObject)  | The object containing the URL of the source  | No |
| sentenceText  | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject) | The object containing the sentence-type text  | No |
| subText  | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject) | The object containing the sub text  | No |
| tablieList[]  | object array  | The object array containing the table-type text. The table has two columns.  | No |
| tablieList[].item1  | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject) | The object containing the text to be displayed in the first column  | No |
| tablieList[].item2  | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject) | The object containing the text to be displayed in the second column  | No |
| tablieList[].item2Link | [URLObject](/CIC/References/ContentTemplates/Shared_Objects.md#URLObject) or [PhoneNumberObject](/CIC/References/ContentTemplates/Shared_Objects.md#PhoneNumberObject) | The object containing the link URL of the text or phone number to be displayed in the second column | No |
| type  | string  | Content Template identifier. Fixed to "ImageText".  | Yes |

## Template Example

{% raw %}
```json
// Example 1.
// User request: 1달러 지금 얼마야? (The user asks how much 1 dollar is worth now. Highlighted text is displayed)
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
    "value": "원"
  },
  "paragraphText": {
    "type": "string",
    "value": ""
  },
  "referenceText": {
    "type": "string",
    "value": "KEB하나은행"
  },
  "referenceUrl": {
    "type": "url",
    "value": "https://m.search.naver.com/search.naver?where=m&sm=mob_lic&query=1%eb%8b%ac%eb%9f%ac+%ed%99%98%ec%9c%a8"
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
  "type": "Text"
}

// Example 2.
// User request: 토트넘 감독이 누구야? (The user asks who's the director of Tottenham. Paragraph text is displayed.)
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
    "value": "토트넘 홋스퍼 FC 감독\n 마우리시오 포체티노"
  },
  "referenceText": {
    "type": "string",
    "value": "네이버 검색결과"
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
  "type": "Text"
}

// Example 3.
// User request: 꽃집 전화번호 알려줘 (The user requests flower shop phone numbers. Table text is displayed.)
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
    "value": "네이버 검색결과"
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
        "value": "터지머지플라워 분당 정자점"
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
        "value": "서머셋플라워"
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
  "type": "Text"
}

```
{% endraw %}

## Screen UI example {#UIExample}
The following examples show how the Text template is presented on a screen of the Clova mobile app for mobile provided by NAVER.

| Highlighted text | Paragraph text | Table text |
|-------|-------|-------|
| <div class="midAlign"><img src="/CIC/Resources/Images/Content_Template-Highlight_Text.png" /></div> | <div class="midAlign"><img src="/CIC/Resources/Images/Content_Template-Paragragh_Text.png" /></div> | <div class="midAlign"><img src="/CIC/Resources/Images/Content_Template-Table_Text.png" /></div> |

## See also
* [CardList](/CIC/References/ContentTemplates/CardList.md)
* [ImageList](/CIC/References/ContentTemplates/ImageList.md)
* [ImageText](/CIC/References/ContentTemplates/ImageText.md)