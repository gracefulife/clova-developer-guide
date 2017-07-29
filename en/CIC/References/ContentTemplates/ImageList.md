# ImageList Template
Displays one or more images with description for each. It displays a list of thumbnails, or, when a user selects one of the thumbnails, displays a large image.

<div class="note">
<p><strong>Note!</strong></p>
<p>See <a href="#UIExample">Screen UI example</a> for available display formats of the ImageList template.</p>
</div>

## Template field

| Field name       | Type    | Field description                     | Required |
|---------------|---------|-----------------------------|---------|
| ImageList[]                | object array | An object array that displays a image list                        | Yes |
| ImageList[].imageReference | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject) | An object that contains image source information      | No |
| ImageList[].imageTitle     | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject) | An object that contains an image title           | No |
| ImageList[].imageUrl       | [URLObject](/CIC/References/ContentTemplates/Shared_Objects.md#URLObject)       | An object that contains an image URL      | No |
| ImageList[].referenceText  | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject) | An object that contains source text information      | No |
| ImageList[].referenceURL   | [URLObject](/CIC/References/ContentTemplates/Shared_Objects.md#URLObject)       | An object that contains a source URL        | No |
| ImageList[].thumbImageUrl  | [URLObject](/CIC/References/ContentTemplates/Shared_Objects.md#URLObject)       | An object that contains a thumbnail image URL | No |
| type                       | string       | Content Template delimiter. The value is always "ImageList".        | Yes |

## Template Example

{% raw %}
```json
// Example 1.
// User request: 자동차 사진 보여줘 (Request to show pictures of cars)
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

## Screen UI example {#UIExample}
The following examples show how the ImageList template is presented on a screen of the Clova mobile app provided by NAVER.

| Thumbnail list | Displaying a selected image |
|-------|-------|
| <div class="midAlign"><img src="/CIC/Resources/Images/Content_Template-Thumbnail_List.png" /></div> | <div class="midAlign"><img src="/CIC/Resources/Images/Content_Template-Original_Image.png" /></div> |

## See also
* [CardList](/CIC/References/ContentTemplates/ImageList.md)
* [ImageText](/CIC/References/ContentTemplates/ImageText.md)
* [Text](/CIC/References/ContentTemplates/Text.md)