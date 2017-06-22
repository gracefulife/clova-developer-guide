# Shared Objects
Content Template uses the following shared objects.

| Object name  | Object description  |
|--------------------|---------------------------------------------------|
| [DateObject](#DateObject)  | The object containing date data  |
| [NumberObject](#NumberObject)  | The object containing number data separated by thousands |
| [PhoneNumberObject](#PhoneNumberObject) | The object containing phone number data  |
| [StringObject](#StringObject)  | The object containing text data  |
| [URLObject](#URLObject)  | The object containing URL data  |

## DateObject {#DateObject}
This object contains date data.

### Object field
| Field name  | Type  | Field description  | Required |
|---------------|---------|-----------------------------|---------|
| type  | string  | The value is fixed to "date".  | Yes  |
| value  | string  | URL  | Yes  |

### Object Example
{% raw %}
```json
{
    "type": "date",
    "value": "2017.05.29"
}
```
{% endraw %}

### See also
None

## NumberObject {#NumberObject}
This object contains number data separated by thousands.

### Object field
| Field name  | Type  | Field description  | Required |
|---------------|---------|-----------------------------|---------|
| type  | string  | The value is fixed to "number".  | Yes  |
| value  | string  | The number data separated by thousands | Yes  |

### Object Example
{% raw %}
```json
{
    "type": "number",
    "value": "19,304,213"
}
```
{% endraw %}

### See also
None

## PhoneNumberObject {#PhoneNumberObject}
This object contains phone number data.

### Object field
| Field name  | Type  | Field description  | Required |
|---------------|---------|-----------------------------|---------|
| type  | string  | The value is fixed to "phoneNum". | Yes  |
| value  | string  | Phone number data  | Yes  |

### Object Example
{% raw %}
```json
{
    "type": "number",
    "value": "031-784-1000"
}
```
{% endraw %}

### See also
None

## StringObject {#StringObject}
This object contains text data.

### Object field
| Field name  | Type  | Field description  | Required |
|---------------|---------|-----------------------------|---------|
| type  | string  | The value is fixed to "string".  | Yes  |
| value  | string  | Text data  | Yes  |

### Object Example
{% raw %}
```json
// Example 1
{
    "type": "string",
    "value": "토트넘 입단 손흥민 “EPL 항상 꿈꿔왔던 무대”"
}

// Example 2
{
    "type": "string",
    "value": "네이버 검색결과"
}
```
{% endraw %}

### See also
None

## URLObject {#URLObject}
This object contains URL data.

### Object field
| Field name  | Type  | Field description  | Required |
|---------------|---------|-----------------------------|---------|
| type  | string  | The value is fixed to "url".  | Yes  |
| value  | string  | URL  | Yes  |

### Object Example
{% raw %}
```json
// Example 1
{
    "type": "url",
    "value": "https://m.search.naver.com/search.naver?where=m_image&mode=default&query=%EC%86%90%ED%9D%A5%EB%AF%BC%20%EC%9D%B4%EB%AF%B8%EC%A7%80#imgId=news4100000269062_1"
}

// Example 2
{
    "type": "url",
    "value": "https://search.pstatic.net/common/?src=http%3A%2F%2Fimgnews.naver.com%2Fimage%2F410%2F2015%2F08%2F31%2F20150831_1441012614_99_20150831181804.jpg&type=b360"
}
```
{% endraw %}

### See also
None