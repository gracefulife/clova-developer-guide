# Text Template
화면에 표시해야 할 텍스트 데이터를 제공하는 템플릿입니다. 강조하는 형태의 텍스트, 문단 형태의 텍스트, 표 형태의 텍스트를 표시할 때 사용됩니다.

<div class="note">
<p><strong>Note!</strong></p>
<p>Text 템플릿의 표시 형태는 <a href="#UIExample">UI example</a>을 참조합니다.</p>
</div>

## Template fields

| 필드 이름       | 자료형    | 필드 설명                     |
|---------------|---------|-----------------------------|
| `bgUrl`                  | [URLObject](/CIC/References/ContentTemplates/Shared_Objects.md#URLObject)       | 백그라운드로 표시할 이미지의 URL 정보가 담긴 객체. 이 객체의 `value` 필드는 빈 문자열(`""`)을 가질 수도 있습니다.               |
| `emotionCode`            | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject) | 감정 표현이 정의된 코드. 감정 코드를 활용하여 클라이언트 기기에서 미리 정의된 감정 표현을 표시할 수 있습니다. 기기에 감정 표현하는 기능이 존재하지 않으면 이 코드를 무시하면 됩니다. <div class="note"><p><strong>Note!</strong></p><p>감정 코드에 대한 자세한 스펙은 관련 제휴 담당자에게 별도 문의하시기 바랍니다.</p></div> |
| `highlightText`          | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject) 또는 [NumberObject](/CIC/References/ContentTemplates/Shared_Objects.md#NumberObject) | 강조할 텍스트 또는 숫자 정보가 담긴 객체. 숫자 정보의 경우 구분 단위 기호를 넣어 표현할 수 있습니다. 이 객체의 `value` 필드는 빈 문자열(`""`) 또는 `null` 값을 가질 수도 있습니다. |
| `imageUrl`               | [URLObject](/CIC/References/ContentTemplates/Shared_Objects.md#URLObject)       | 이미지의 URL 정보가 담긴 객체. 이 객체의 `value` 필드는 빈 문자열(`""`)을 가질 수도 있습니다.                              |
| `linkUrl`                | [URLObject](/CIC/References/ContentTemplates/Shared_Objects.md#URLObject)       | 지도 이미지가 포함되었을 때 웹 지도로 이동하는 URL 정보가 담긴 객체. 이 객체의 `value` 필드는 빈 문자열(`""`)을 가질 수도 있습니다. |
| `mainText`               | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject) | 메인 문구가 담긴 객체. 이 객체의 `value` 필드는 빈 문자열(`""`)을 가질 수도 있습니다.                                     |
| `motionCode`             | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject) | 동작이 정의된 코드. 동작 코드를 활용하여 클라이언트 기기에서 미리 정의된 움직임을 수행할 수 있습니다. 기기에 동작을 표현하는 기능이 존재하지 않으면 이 코드를 무시하면 됩니다. <div class="note"><p><strong>Note!</strong></p><p>동작 코드에 대한 자세한 스펙은 관련 제휴 담당자에게 별도 문의하시기 바랍니다.</p></div> |
| `paragraphText`          | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject) | 문단 형태의 문구가 담긴 객체. 이 객체의 `value` 필드는 빈 문자열(`""`)을 가질 수도 있습니다.                                |
| `referenceText`          | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject) | 참조한 서비스의 정보가 담긴 객체. 이 객체의 `value` 필드는 빈 문자열(`""`)을 가질 수도 있습니다.  |
| `referenceUrl`           | [URLObject](/CIC/References/ContentTemplates/Shared_Objects.md#URLObject)       | 참조한 서비스의 이용 결과 URL 정보가 담긴 객체. 이 객체의 `value` 필드는 빈 문자열(`""`)을 가질 수도 있습니다.   |
| `sentenceText`           | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject) | 문장 형태의 문구가 담긴 객체. 이 객체의 `value` 필드는 빈 문자열(`""`)을 가질 수도 있습니다.                                |
| `subText`                | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject) | 보조 문구가 담긴 객체. 이 객체의 `value` 필드는 빈 문자열(`""`)을 가질 수도 있습니다.                                     |
| `tableList[]`           | object array                                                                    | 표 형태의 문구가 담긴 객체 배열. 행이 두 개 또는 세 개인 표를 구성합니다.     |
| `tableList[].item1`     | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject) | 첫 번째 행에 표시할 텍스트 정보를 담은 객체. 이 객체의 `value` 필드는 빈 문자열(`""`)을 가질 수도 있습니다.                    |
| `tableList[].item2`     | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject) | 두 번째 행에 표시할 텍스트 정보를 담은 객체. 이 객체의 `value` 필드는 빈 문자열(`""`)을 가질 수도 있습니다.                    |
| `tableList[].item2Link` | [URLObject](/CIC/References/ContentTemplates/Shared_Objects.md#URLObject) 또는 [PhoneNumberObject](/CIC/References/ContentTemplates/Shared_Objects.md#PhoneNumberObject) | 두 번째 행에 표시된 텍스트의 링크 URL 또는 전화 번호를 담은 객체. 이 객체의 `value` 필드는 빈 문자열(`""`)을 가질 수도 있습니다. |
| `tableList[].item3`     | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject) | 세 번째 행에 표시할 텍스트 정보를 담은 객체. 이 필드는 생략될 수 있습니다. |
| `type`                   | string                                                                          | Content template 구분자. `"Text"` 값을 가집니다.             |

## Template example

{% raw %}

```json
// 예제 1.
// 사용자 요청: 1달러 지금 얼마야? (강조하는 형태의 텍스트 표시)
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

// 예제 2.
// 사용자 요청: 토트넘 감독이 누구야? (문단 형태의 텍스트 표시)
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

// 예제 3.
// 사용자 요청: 꽃집 전화번호 알려줘 (표 형태의 텍스트 표시)
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

// 예제 4.
// 사용자 요청: 미안해. (감정 표현)

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
    "value": "전혀 미안해 할 거 없어요."
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

// 예제 5.
// 사용자 요청: 춤춰줘. (동작 표현)

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
    "value": "제 능력 밖의 일입니다."
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
다음은 NAVER가 배포한 모바일용 Clova 앱에서 Text 템플릿의 내용을 표현한 UI 예제입니다.

| 강조하는 형태의 텍스트 | 문단 형태의 텍스트 | 표 형태의 텍스트 |
|-------|-------|-------|
| ![Highlight](/CIC/Resources/Images/Content_Template-Highlight_Text.png) | ![Paragraph](/CIC/Resources/Images/Content_Template-Paragragh_Text.png) | ![Table](/CIC/Resources/Images/Content_Template-Table_Text.png) |

## See also
* [CardList](/CIC/References/ContentTemplates/CardList.md)
* [ImageList](/CIC/References/ContentTemplates/ImageList.md)
* [ImageText](/CIC/References/ContentTemplates/ImageText.md)
* [Popup](/CIC/References/ContentTemplates/Popup.md)
