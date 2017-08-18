# ImageText template
Displays an image with text on a screen. It is used to display a thumbnail image with text or a map with text.

<div class="note">
<p><strong>Note!</strong></p>
<p>See <a href="#UIExample">Screen UI example</a> for available display formats of the ImageText template.</p>
</div>

## Template field

| Field name  | Type  | Field description  | Required |
|---------------|---------|-----------------------------|---------|
| `appLinkUrl`  | [URLObject](/CIC/References/ContentTemplates/Shared_Objects.md#URLObject)  | An object containing a URL which directs users to a map app when a map image is included  | No |
| `imageUrl`  | [URLObject](/CIC/References/ContentTemplates/Shared_Objects.md#URLObject)  | An object containing the URL of the image  | No |
| `linkUrl`  | [URLObject](/CIC/References/ContentTemplates/Shared_Objects.md#URLObject)  | An object containing a URL which directs users to a web map when a map image is included  | No |
| `mainText`  | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject)  | An object containing main text  | No |
| `referenceText`  | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject)  | An object containing text data of the source  | No |
| `referenceURL`  | [URLObject](/CIC/References/ContentTemplates/Shared_Objects.md#URLObject)  | An object containing the URL of the source  | No |
| `subTextList`  | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject) array | An array containing sub text  | No |
| `thumbImageUrl`  | [URLObject](/CIC/References/ContentTemplates/Shared_Objects.md#URLObject)  | An object containing the URL of the thumbnail image  | No |
| `thumbImageType` | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject)  | An object containing the type of the thumbnail image. Available values are: <ul><li><strong>"인물"</strong></li><li><strong>"책"</strong></li><li><strong>"앨범"</strong></li></ul> | No |
| `type`  | string  | A content template delimiter. The value is always **"ImageText"**.  | Yes  |

## Template Example

{% raw %}
```json
// Example 1.
// User request: 리오넬 메시의 소속팀은? (User asks which team Lionel Messi is in. Thumbnail image and text are displayed)
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

// Example 2.
// User request: 현재 위치 알려줘 (User asks the current location. Map image and text are displayed)
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
The following example shows how the ImageText template is presented in the Clova mobile app distributed by {{ book.OrientedService }}.

| Thumbnail image with text | Map image with text |
|-------|-------|
| <div class="midAlign"><img src="/CIC/Resources/Images/Content_Template-Thumbimage_and_Text.png" /></div> | <div class="midAlign"><img src="/CIC/Resources/Images/Content_Template-Mapimage_and_Text.png" /></div> |

## See also
* [CardList](/CIC/References/ContentTemplates/CardList.md)
* [ImageList](/CIC/References/ContentTemplates/ImageList.md)
* [Text](/CIC/References/ContentTemplates/Text.md)
