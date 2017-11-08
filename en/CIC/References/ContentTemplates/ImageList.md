# ImageList template
Displays one or more images with description on a screen. It is used to display a list of thumbnails or a large image when a user selects one of the thumbnails.

<div class="note">
<p><strong>Note!</strong></p>
<p>See <a href="#UIExample">Screen UI example</a> for available display formats of the ImageList template.</p>
</div>

## Template field

| Field name       | Type    | Field description                     |
|---------------|---------|-----------------------------|
| `ImageList[]`                | object array | An object array that displays a list of images                        |
| `ImageList[].imageReference` | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject) | An object containing the source of the image. The `value` field of this object can have an empty string (`""`).      |
| `ImageList[].imageTitle`     | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject) | An object containing the title of the image. The `value` field of this object can have an empty string (`""`).           |
| `ImageList[].imageUrl`       | [URLObject](/CIC/References/ContentTemplates/Shared_Objects.md#URLObject)       | An object containing the URL of the image. The `value` field of this object can have an empty string (`""`).      |
| `ImageList[].referenceText`  | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject) | An object containing text information of the source. The `value` field of this object can have an empty string (`""`).      |
| `ImageList[].referenceURL`   | [URLObject](/CIC/References/ContentTemplates/Shared_Objects.md#URLObject)       | An object containing the URL of the source. The `value` field of this object can have an empty string (`""`).      |
| `ImageList[].thumbImageUrl`  | [URLObject](/CIC/References/ContentTemplates/Shared_Objects.md#URLObject)       | An object containing the URL of the thumbnail image. The `value` field of this object can have an empty string (`""`).      |
| `type`                       | string       | A content template delimiter. It has an `"ImageList"` value.        |

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
The following example shows how the ImageList template is presented in the Clova mobile app distributed by {{ book.OrientedService }}.

| Thumbnail list | Selected image |
|-------|-------|
| ![Thumbnail](/CIC/Resources/Images/Content_Template-Thumbnail_List.png) | ![Original](/CIC/Resources/Images/Content_Template-Original_Image.png) |

## See also
* [CardList](/CIC/References/ContentTemplates/ImageList.md)
* [ImageText](/CIC/References/ContentTemplates/ImageText.md)
* [Popup](/CIC/References/ContentTemplates/Popup.md)
* [Text](/CIC/References/ContentTemplates/Text.md)
