# ImageList Template
화면에 한 개 이상의 이미지와 각 이미지에 대한 설명을 제공하는 템플릿입니다. 썸네일의 목록을 표시하거나 사용자가 썸네일을 선택했을 때 큰 이미지를 표시하기 위해 사용합니다.

<div class="note">
<p><strong>Note!</strong></p>
<p>ImageList 템플릿의 표시 형태는 <a href="#UIExample">UI example</a>을 참조합니다.</p>
</div>

## Template fields

| 필드 이름       | 자료형    | 필드 설명                     |
|---------------|---------|-----------------------------|
| `ImageList[]`                | object array | 이미지 목록을 표현하는 객체 배열                        |
| `ImageList[].imageReference` | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject) | 이미지의 출처 정보가 담긴 객체. 이 객체의 `value` 필드는 빈 문자열(`""`)을 가질 수도 있습니다.      |
| `ImageList[].imageTitle`     | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject) | 이미지 제목이 담긴 객체. 이 객체의 `value` 필드는 빈 문자열(`""`)을 가질 수도 있습니다.           |
| `ImageList[].imageUrl`       | [URLObject](/CIC/References/ContentTemplates/Shared_Objects.md#URLObject)       | 이미지의 URL 정보가 담긴 객체. 이 객체의 `value` 필드는 빈 문자열(`""`)을 가질 수도 있습니다.      |
| `ImageList[].referenceText`  | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject) | 출처의 텍스트 정보가 담긴 객체. 이 객체의 `value` 필드는 빈 문자열(`""`)을 가질 수도 있습니다.      |
| `ImageList[].referenceURL`   | [URLObject](/CIC/References/ContentTemplates/Shared_Objects.md#URLObject)       | 출처의 URL 정보가 담긴 객체. 이 객체의 `value` 필드는 빈 문자열(`""`)을 가질 수도 있습니다.      |
| `ImageList[].thumbImageUrl`  | [URLObject](/CIC/References/ContentTemplates/Shared_Objects.md#URLObject)       | 썸네일 이미지의 URL 정보가 담긴 객체. 이 객체의 `value` 필드는 빈 문자열(`""`)을 가질 수도 있습니다.      |
| `type`                       | string       | Content template 구분자. `"ImageList"` 값을 가집니다.        |

## Template example

{% raw %}
```json
// 예제 1.
// 사용자 요청: 자동차 사진 보여줘
{
  "type": "ImageList",
  "thumbImageUrlList": [
    {
      "imageReference": {
        "type": "string",
        "value": ""
      },
      "imageTitle": {
        "type": "string",
        "value": "창원대리운전 번개처럼 빠르게"
      },
      "imageUrl": {
        "type": "url",
        "value": "https://m.search.naver.com/search.naver?where=m_image&mode=default&query=%EC%9E%90%EB%8F%99%EC%B0%A8%20%EC%9D%B4%EB%AF%B8%EC%A7%80#imgId=post7533909_3"
      },
      "referenceText": {
        "type": "string",
        "value": "네이버 검색결과"
      },
      "referenceUrl": {
        "type": "url",
        "value": "https://m.search.naver.com/search.naver?where=m&sm=mob_lic&query=%ec%9e%90%eb%8f%99%ec%b0%a8+%ec%82%ac%ec%a7%84+%eb%b3%b4%ec%97%ac%ec%a4%98"
      },
      "thumbImageUrl": {
        "type": "url",
        "value": "https://search.pstatic.net/common/?src=http%3A%2F%2Fpost.phinf.naver.net%2FMjAxNzA1MDZfMTg4%2FMDAxNDk0MDYyNDAwMDY3.C6LJCKXrha2u8dIqOOX0RhQNGrVVfkp3WbLO8U-xzRwg.IEYdykQp6xguEy4bnQ83JhDy1QZOtO4n1Lx5MBwivFwg.JPEG%2FIz2FmvAaRVzSf2Z-sNWzYQVU5z6Q.jpg&type=b360"
      }
    },
    {
      "imageReference": {
        "type": "string",
        "value": ""
      },
      "imageTitle": {
        "type": "string",
        "value": "자동차"
      },
      "imageUrl": {
        "type": "url",
        "value": "https://m.search.naver.com/search.naver?where=m_image&mode=default&query=%EC%9E%90%EB%8F%99%EC%B0%A8%20%EC%9D%B4%EB%AF%B8%EC%A7%80#imgId=gallery2004021016070294818_1"
      },
      "referenceText": {
        "type": "string",
        "value": "네이버 검색결과"
      },
      "referenceUrl": {
        "type": "url",
        "value": "https://m.search.naver.com/search.naver?where=m&sm=mob_lic&query=%ec%9e%90%eb%8f%99%ec%b0%a8+%ec%82%ac%ec%a7%84+%eb%b3%b4%ec%97%ac%ec%a4%98"
      },
      "thumbImageUrl": {
        "type": "url",
        "value": "https://search.pstatic.net/common/?src=http%3A%2F%2Fthumb.photo.naver.net%2Fdata15%2Fgallery%2F2004-02%2F10%2F07%2F18m2948m0.jpg&type=b360"
      }
    },
    ...
  ]
}

```
{% endraw %}

## UI example {#UIExample}
다음은 {{ book.OrientedService }}가 배포한 모바일용 Clova 앱에서 ImageList 템플릿의 내용을 표현한 UI 예제입니다.

| 썸네일 목록 | 선택한 이미지 표시 |
|-------|-------|
| ![Thumbnail](/CIC/Resources/Images/Content_Template-Thumbnail_List.png) | ![Original](/CIC/Resources/Images/Content_Template-Original_Image.png) |

## See also
* [CardList](/CIC/References/ContentTemplates/ImageList.md)
* [ImageText](/CIC/References/ContentTemplates/ImageText.md)
* [Popup](/CIC/References/ContentTemplates/Popup.md)
* [Text](/CIC/References/ContentTemplates/Text.md)
