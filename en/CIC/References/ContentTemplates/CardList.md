# CardList Template
This template lets your client display data on a screen using a card list format. CardList has several card types as follows. Each card type consists of different *card* objects.

| Card type  | Type description  | Fields of *card* object  |
|---------------|-----------------------------|-----------------------------|
| Type1  | Displays image, title, and description of the content.  | description, imageUrl, referenceText, referenceUrl, title  |
| Type2  | Displays image, title, description, and link of the content. | description, imageUrl, linkUrl, referenceText, referenceUrl, title  |
| Type3  | Displays video content.  | description, imageUrl, referenceText, referenceUrl, title, videoUrl |
| Type4  | Displays news content.  | description, press, pressIconUrl, publishDate, title  |

<div class="note">
<p><strong>Note!</strong></p>
<p>See <a href="#UIExample">Screen UI example</a> for the available display formats of each type.</p>
</div>

## Template field

| Field name  | Type  | Field description  | Required |
|---------------|---------|-----------------------------|---------|
| cardList[]  | object array | The object array that displays the card list | Yes  |
| cardList[].description  | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject) array | The object array containing the description of the content  | No |
| cardList[].imageUrl  | [URLObject](/CIC/References/ContentTemplates/Shared_Objects.md#URLObject)  | The object containing the URL of the image to display  | No |
| cardList[].linkUrl  | [URLObject](/CIC/References/ContentTemplates/Shared_Objects.md#URLObject)  | The object containing the URL of the content  | No |
| cardList[].press  | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject)  | The object containing the name of the press  | No |
| cardList[].pressIconUrl  | [URLObject](/CIC/References/ContentTemplates/Shared_Objects.md#URLObject)  | The object containing the URL of the press icon  | No |
| cardList[].publishDate  | [DateObject](/CIC/References/ContentTemplates/Shared_Objects.md#DateObject)  | The object containing the publishing date of the article  | No |
| cardList[].referenceText  | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject)  | The object containing the text information of the source  | No |
| cardList[].referenceURL  | [URLObject](/CIC/References/ContentTemplates/Shared_Objects.md#URLObject)  | The object containing the URL of the source  | No |
| cardList[].title  | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject)  | The object containing the title of the content  | No |
| cardList[].videoUrl  | [URLObject](/CIC/References/ContentTemplates/Shared_Objects.md#URLObject)  | The object containing the URL of the video to play  | No |
| subType  | string  | Card type identifier. You may specify four types as follows. <ul><li>Type1</li><li>Type2</li><li>Type3</li><li>Type4</li></ul><div class="note"><p><strong>Note!</strong></p><p>Type1, Type2, Type3 are represented as an empty string at the moment. You need to determine which type to use based on the available fields of each <em>card</em> object.</p></div> | Yes  |
| type  | string  | Content Template identifier. Fixed to "CardList".  | Yes |

## Template Example

{% raw %}
```json
// Type1, Type2 example:
// User request: 공포 영화 추천해줘 (Request to recommend a horror movie).

{
  "subType": "",
  "type": "CardList",
  "cardList": [
    {
      "description": [
        {
          "type": "string",
          "value": "공포, 스릴러"
        },
        {
          "type": "string",
          "value": "아론 에크하트, 데이비드 매주즈, 캐리스 밴 허슨, 카타리나 산디노 모레노, 키어 오도넬, 매트 네이블, 존 피루첼로, 엠제이 안소니, 카롤리나 위드라, 마크 스테거, 토마스 아라나, 페트라 스프레처, 마크 헨리, 애슐리 그린 엘리자베스"
        },
        {
          "type": "string",
          "value": ""
        }
      ],
      "imageUrl": {
        "type": "url",
        "value": "http://movie.phinf.naver.net/20170410_12/1491786049305s4W0n_JPEG/movie_image.jpg?type=w640_2"
      },
      "linkUrl": {
        "type": "url",
        "value": "http://movie.naver.com/movie/bi/mi/basic.nhn?code=118965"
      },
      "press": {
        "type": "string",
        "value": ""
      },
      "publishDate": {
        "type": "date",
        "value": ""
      },
      "referenceText": {
        "type": "string",
        "value": "네이버 검색결과"
      },
      "referenceUrl": {
        "type": "url",
        "value": "https://m.search.naver.com/search.naver?where=m&sm=mob_lic&query=+%ec%98%81%ed%99%94"
      },
      "title": {
        "type": "string",
        "value": "인카네이트"
      },
      "videoUrl": {
        "type": "url",
        "value": ""
      }
    },
    {
      "description": [
        {
          "type": "string",
          "value": "공포"
        },
        {
          "type": "string",
          "value": "마틸다 안나 잉그리드 루츠, 알렉스 로, 자니 갈렉키, 빈센트 도노프리오, 에이미 티가든, 보니 모건, 로라 위긴스, 잭 로어리그, 리지 브로체르"
        },
        {
          "type": "string",
          "value": ""
        }
      ],
      "imageUrl": {
        "type": "url",
        "value": "http://movie.phinf.naver.net/20170317_53/1489741954272MquSW_JPEG/movie_image.jpg?type=w640_2"
      },
      "linkUrl": {
        "type": "url",
        "value": "http://movie.naver.com/movie/bi/mi/basic.nhn?code=137909"
      },
      "press": {
        "type": "string",
        "value": ""
      },
      "publishDate": {
        "type": "date",
        "value": ""
      },
      "referenceText": {
        "type": "string",
        "value": "네이버 검색결과"
      },
      "referenceUrl": {
        "type": "url",
        "value": "https://m.search.naver.com/search.naver?where=m&sm=mob_lic&query=+%ec%98%81%ed%99%94"
      },
      "title": {
        "type": "string",
        "value": "링스"
      },
      "videoUrl": {
        "type": "url",
        "value": ""
      }
    },
    ...
  ]
}

// Type3 example
// User request: 축구 동영상 보여줘 (Request to play football video clips.)
{
  "subType": "",
  "type": "CardList",
  "cardList": [
    {
      "description": [
        {
          "type": "string",
          "value": "04:14"
        },
        {
          "type": "string",
          "value": ""
        },
        {
          "type": "string",
          "value": ""
        }
      ],
      "imageUrl": {
        "type": "url",
        "value": "http://hol.phinf.naver.net/00/587/820/58782072_0.jpg"
      },
      "linkUrl": {
        "type": "url",
        "value": ""
      },
      "press": {
        "type": "string",
        "value": ""
      },
      "publishDate": {
        "type": "date",
        "value": ""
      },
      "referenceText": {
        "type": "string",
        "value": "네이버 검색결과"
      },
      "referenceUrl": {
        "type": "url",
        "value": "https://m.search.naver.com/search.naver?where=m&sm=mob_lic&query=%ec%b6%95%ea%b5%ac+%eb%8f%99%ec%98%81%ec%83%81+%eb%b3%b4%ec%97%ac%ec%a4%98"
      },
      "title": {
        "type": "string",
        "value": "[해외반응] U20 월드컵, 이탈리아 일본, 해외네티즌 \"최악의 더러운 경기\" - 해외네티즌반응"
      },
      "videoUrl": {
        "type": "url",
        "value": "http://m.tv.naver.com/v/1720910"
      }
    },
    {
      "description": [
        {
          "type": "string",
          "value": "06:31"
        },
        {
          "type": "string",
          "value": ""
        },
        {
          "type": "string",
          "value": ""
        }
      ],
      "imageUrl": {
        "type": "url",
        "value": "http://hol.phinf.naver.net/00/587/815/58781581_0.jpg"
      },
      "linkUrl": {
        "type": "url",
        "value": ""
      },
      "press": {
        "type": "string",
        "value": ""
      },
      "publishDate": {
        "type": "date",
        "value": ""
      },
      "referenceText": {
        "type": "string",
        "value": "네이버 검색결과"
      },
      "referenceUrl": {
        "type": "url",
        "value": "https://m.search.naver.com/search.naver?where=m&sm=mob_lic&query=%ec%b6%95%ea%b5%ac+%eb%8f%99%ec%98%81%ec%83%81+%eb%b3%b4%ec%97%ac%ec%a4%98"
      },
      "title": {
        "type": "string",
        "value": "FA컵 결승: 아스널 v 첼시 경기 후 인터뷰"
      },
      "videoUrl": {
        "type": "url",
        "value": "http://m.sports.naver.com/video.nhn?id=310230"
      }
    },
    ...
  ]
}


// Type4 example
// User request: 최신 뉴스 보여줘 (Request to view the latest news.)
{
  "subType": "Type4",
  "type": "CardList",
  "cardList": [
    {
      "description": [
        {
          "type": "string",
          "value": "다음 달이면 말 많고 탈 많았던 '4대강'의 보 수문이 열립니다. 문재인 대통령이 지난 22일 '4대강 사업'에 대한 감사 지시를 하면서 이뤄진 결정입니다. 이를 계기로 4대강 사업 논란이 다시 수면 위로 떠올랐습니"
        },
        {
          "type": "string",
          "value": ""
        },
        {
          "type": "string",
          "value": ""
        }
      ],
      "imageUrl": {
        "type": "url",
        "value": ""
      },
      "linkUrl": {
        "type": "url",
        "value": "http://news.naver.com/main/read.nhn?mode=LSD&mid=sec&sid1=001&oid=025&aid=0002720454"
      },
      "press": {
        "type": "string",
        "value": "중앙일보"
      },
      "publishDate": {
        "type": "date",
        "value": "2017-05-28"
      },
      "referenceText": {
        "type": "string",
        "value": ""
      },
      "referenceUrl": {
        "type": "url",
        "value": ""
      },
      "title": {
        "type": "string",
        "value": "[시민마이크]'녹차라떼 4대강' 감사, 시민들의 생각은?"
      },
      "videoUrl": {
        "type": "url",
        "value": ""
      }
    },
    {
      "description": [
        {
          "type": "string",
          "value": "5월 마지막 주말 나들이객 줄이어더위 식히고 모래작품 보고(부산=연합뉴스) 조정호 기자 = 초여름 날씨를 보인 28일 부산 해운대 모래축제가 열린 해운대해수욕장에서 나들이객들이 가로 25ｍ, 높이 5ｍ 크기의 대형 모래작품을 구경하고 있습니다. 2017.5.28(전국종합=연합뉴스) 5월의 마지막 주말인 28일 초여름 날씨가..."
        },
        {
          "type": "string",
          "value": ""
        },
        {
          "type": "string",
          "value": ""
        }
      ],
      "imageUrl": {
        "type": "url",
        "value": ""
      },
      "linkUrl": {
        "type": "url",
        "value": "http://news.naver.com/main/read.nhn?mode=LSD&mid=sec&sid1=001&oid=001&aid=0009297247"
      },
      "press": {
        "type": "string",
        "value": "연합뉴스"
      },
      "publishDate": {
        "type": "date",
        "value": "2017-05-28"
      },
      "referenceText": {
        "type": "string",
        "value": ""
      },
      "referenceUrl": {
        "type": "url",
        "value": ""
      },
      "title": {
        "type": "string",
        "value": "단오제 등 전국 곳곳 축제…초여름 날씨에 때이른 피서 행렬"
      },
      "videoUrl": {
        "type": "url",
        "value": ""
      }
    },
    ...
  ]
}

```
{% endraw %}

## Screen UI example {#UIExample}
The following examples show how each type's CardList template is presented on a screen of the Clova mobile app provided by NAVER.

| Type1 | Type2 |
|-------|-------|
| <div class="midAlign"><img src="/CIC/Resources/Images/Content_Template-Content_Card_Type.png" /></div> | <div class="midAlign"><img src="/CIC/Resources/Images/Content_Template-Content_Card_with_Link_Type.png" /></div> |

| Type3 | Type4 |
|-------|-------|
| <div class="midAlign"><img src="/CIC/Resources/Images/Content_Template-Video_Card_Type.png" /></div> | <div class="midAlign"><img src="/CIC/Resources/Images/Content_Template-News_Card_Type.png" /></div> |

## See also
* [ImageList](/CIC/References/ContentTemplates/ImageList.md)
* [ImageText](/CIC/References/ContentTemplates/ImageText.md)
* [Text](/CIC/References/ContentTemplates/Text.md)