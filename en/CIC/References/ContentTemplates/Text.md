# Text Template
Provides text data to display. It is used to display text with highlights, paragraph text or table text.

<div class="note">
<p><strong>Note!</strong></p>
<p>See <a href="#UIExample">Screen UI example</a> for available display formats of the Text template.</p>
</div>

## Template field

| Field name  | Type  | Field description  | Required |
|---------------|---------|-----------------------------|---------|
| bgUrl  | [URLObject](/CIC/References/ContentTemplates/Shared_Objects.md#URLObject)  | An object that contains a URL to an image to be displayed in background  | No |
| highlightText  | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject) or [NumberObject](/CIC/References/ContentTemplates/Shared_Objects.md#NumberObject) | An object that contains highlighted text or number with digit grouping symbols.  | No |
| imageUrl  | [URLObject](/CIC/References/ContentTemplates/Shared_Objects.md#URLObject)  | An object that contains an image URL  | No |
| linkUrl  | [URLObject](/CIC/References/ContentTemplates/Shared_Objects.md#URLObject)  | An object that contains a URL which directs users to a web map when a map image is included | No |
| mainText  | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject) | An object that contains main text  | No |
| paragraphText  | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject) | An object that contains paragraph text  | No |
| referenceText  | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject) | An object that contains text information of a source  | No |
| referenceURL  | [URLObject](/CIC/References/ContentTemplates/Shared_Objects.md#URLObject)  | An object that contains a source URL  | No |
| sentenceText  | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject) | An object that contains sentence text  | No |
| subText  | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject) | An object that contain sub text  | No |
| tableList[]  | object array  | An object array that contains table text. The table has two columns.  | No |
| tableList[].item1  | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject) | An object that contains text to be displayed in the first column  | No |
| tableList[].item2  | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject) | An object that contains text to be displayed in the second column  | No |
| tableList[].item2Link | [URLObject](/CIC/References/ContentTemplates/Shared_Objects.md#URLObject) or [PhoneNumberObject](/CIC/References/ContentTemplates/Shared_Objects.md#PhoneNumberObject) | An object that contains link URL or phone number of the text in the second column | No |
| type  | string  | Content template delimiter. The value is always "ImageText".  | Yes |

## Template Example

{% raw %}
```json
// Example 1.
// User request: 1달러 지금 얼마야? (User asks how much 1 dollar is worth now. Text with highlights is displayed)
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
// User request: 토트넘 감독이 누구야? (User asks who's the director of Tottenham. Paragraph text is displayed)
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
// User request: 꽃집 전화번호 알려줘 (User asks flower shop phone numbers. Table text is displayed)
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
The following example shows how the Text template is presented in the Clova mobile app distributed by {{ book.OrientedService }}.

| Text with highlights | Paragraph text | Table text |
|-------|-------|-------|
| <div class="midAlign"><img src="/CIC/Resources/Images/Content_Template-Highlight_Text.png" /></div> | <div class="midAlign"><img src="/CIC/Resources/Images/Content_Template-Paragragh_Text.png" /></div> | <div class="midAlign"><img src="/CIC/Resources/Images/Content_Template-Table_Text.png" /></div> |

## See also
* [CardList](/CIC/References/ContentTemplates/CardList.md)
* [ImageList](/CIC/References/ContentTemplates/ImageList.md)
* [ImageText](/CIC/References/ContentTemplates/ImageText.md)
