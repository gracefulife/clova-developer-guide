# ImageText Template
화면에 표시해야 할 이미지와 텍스트 데이터를 함께 제공하는 템플릿입니다. 썸네일 이미지와 텍스트를 표시하거나 지도와 텍스트를 함께 표시할 때 사용됩니다.

<div class="note">
<p><strong>Note!</strong></p>
<p>ImageText 템플릿의 표시 형태는 <a href="#UIExample">Screen UI example</a>을 참조합니다.</p>
</div>

## Template field

| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|---------|
| `appLinkUrl`     | [URLObject](/CIC/References/ContentTemplates/Shared_Objects.md#URLObject)             | 지도 이미지가 포함되었을 때 지도 앱으로 이동하는 URL 정보가 담긴 객체  | 선택 |
| `imageUrl`       | [URLObject](/CIC/References/ContentTemplates/Shared_Objects.md#URLObject)             | 이미지의 URL 정보가 담긴 객체                                | 선택 |
| `linkUrl`        | [URLObject](/CIC/References/ContentTemplates/Shared_Objects.md#URLObject)             | 지도 이미지가 포함되었을 때 웹 지도로 이동하는 URL 정보가 담긴 객체   | 선택 |
| `mainText`       | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject)       | 메인 문구가 담긴 객체                                       | 선택 |
| `referenceText`  | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject)       | 출처의 텍스트 정보가 담긴 객체                                | 선택 |
| `referenceURL`   | [URLObject](/CIC/References/ContentTemplates/Shared_Objects.md#URLObject)             | 출처의 URL 정보가 담긴 객체                                  | 선택 |
| `subTextList`    | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject) array | 보조 문구가 담긴 배열                                       | 선택 |
| `thumbImageUrl`  | [URLObject](/CIC/References/ContentTemplates/Shared_Objects.md#URLObject)             | 썸네일 이미지의 URL 정보가 담긴 객체                           | 선택 |
| `thumbImageType` | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject)       | 썸네일 이미지의 유형 정보가 담긴 객체이며, 다음과 같은 값을 가집니다. <ul><li><strong>"인물"</strong></li><li><strong>"책"</strong></li><li><strong>"앨범"</strong></li></ul> | 선택 |
| `type`           | string  | Content template 구분자. **"ImageText"**로 고정      | 필수      |

## Template Example

{% raw %}
```json
// 예제 1.
// 사용자 요청: 리오넬 메시의 소속팀은? (썸네일 이미지와 텍스트 표시)
{
  "type": "ImageText",
  "imageUrl": {
    "type": "url",
    "value": ""
  },
  "mainText": {
    "type": "string",
    "value": "리오넬 메시"
  },
  "referenceText": {
    "type": "string",
    "value": "네이버 검색결과"
  },
  "referenceUrl": {
    "type": "url",
    "value": "https://m.search.naver.com/search.naver?where=m&sm=mob_lic&query=%eb%a6%ac%ec%98%a4%eb%84%ac+%eb%a9%94%ec%8b%9c+%ec%86%8c%ec%86%8d%ed%8c%80"
  },
  "subTextList": [
    {
      "type": "string",
      "value": "FC 바르셀로나"
    }
  ],
  "thumbImageType": {
    "type": "string",
    "value": "인물"
  },
  "thumbImageUrl": {
    "type": "url",
    "value": "http://sstatic.naver.net/people/3/201607071816066361.jpg"
  }
}

// 예제 2.
// 사용자 요청: 현재 위치 알려줘 (지도 이미지와 텍스트 표시)
{
  "type": "ImageText",
  "imageUrl": {
    "type": "url",
    "value": "https://simg.pstatic.net/static.map/image?caller=mw_search&crs=EPSG:4326&scale=2&format=jpg&dataversion=163.2&version=1.1&baselayer=default&center=127.1047745,37.3594589&markers=type,default2_s,127.1047745,37.3594589&level=10&h=402&w=515"
  },
  "mainText": {
    "type": "string",
    "value": "경기도 성남시 분당구 정자1동"
  },
  "referenceText": {
    "type": "string",
    "value": "네이버 검색결과"
  },
  "referenceUrl": {
    "type": "url",
    "value": "https://m.search.naver.com/search.naver?where=m&sm=mob_lic&query=%ed%98%84%ec%9e%ac+%ec%9c%84%ec%b9%98"
  },
  "subTextList": [
    {
      "type": "string",
      "value": ""
    }
  ],
  "thumbImageType": {
    "type": "string",
    "value": ""
  },
  "thumbImageUrl": {
    "type": "url",
    "value": ""
  }
}
```
{% endraw %}

## Screen UI example {#UIExample}
다음은 {{ book.OrientedService }}가 배포한 모바일용 Clova 앱에서 ImageText 템플릿의 내용을 표현한 UI 예제입니다.

| 썸네일 이미지와 텍스트 | 지도 이미지와 텍스트 |
|-------|-------|
| <div class="midAlign"><img src="/CIC/Resources/Images/Content_Template-Thumbimage_and_Text.png" /></div> | <div class="midAlign"><img src="/CIC/Resources/Images/Content_Template-Mapimage_and_Text.png" /></div> |

## See also
* [CardList](/CIC/References/ContentTemplates/CardList.md)
* [ImageList](/CIC/References/ContentTemplates/ImageList.md)
* [Text](/CIC/References/ContentTemplates/Text.md)
