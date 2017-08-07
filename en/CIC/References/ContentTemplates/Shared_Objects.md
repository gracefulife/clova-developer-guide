# Shared Objects
Content templates use the following shared objects.

| Object name  | Object description  |
|--------------------|---------------------------------------------------|
| [CurrencyObject](#CurrencyObject)  | An object that contains currency and amount data  |
| [DateObject](#DateObject)  | An object that contains weather data  |
| [DateTimeObject](#DateTimeObject)  | An object that contains date and time data  |
| [LocationObject](#LocationObject)  | An object that contains coordinate data (UTMK) on a map  |
| [NumberObject](#NumberObject)  | An object that contains number data separated by thousands |
| [PercentageObject](#PercentageObject)  | An object that contains percentage data  |
| [PhoneNumberObject](#PhoneNumberObject)  | An object that contains phone number data  |
| [StringObject](#StringObject)  | An object that contains text data  |
| [TemperatureCObject](#TemperatureCObject) | An object that contains temperature data (Celsius)  |
| [URLObject](#URLObject)  | An object that contains URL data  |

# CurrencyObject {#CurrencyObject}
An object that contains currency and amount data.

### Object field
| Field name  | Type  | Field description  | Required |
|---------------|---------|-----------------------------|---------|
| type  | string  | The value is always "currency".  | Yes  |
| value  | string  | Data in combination of currency and amount  | Yes  |

### Object Example
{% raw %}
```json
{
    "type": "date",
    "value": "KRW500000"
}
```
{% endraw %}

## DateObject {#DateObject}
An object that contains date data.

### Object field
| Field name  | Type  | Field description  | Required |
|---------------|---------|-----------------------------|---------|
| type  | string  | The value is always "date".  | Yes  |
| value  | string  | Date (YYYY-MM-DD format)  | Yes  |

### Object Example
{% raw %}
```json
{
    "type": "date",
    "value": "2017-05-29"
}
```
{% endraw %}

## DateTimeObject {#DateTimeObject}
An object that contains date and time data.

### Object field
| Field name  | Type  | Field description  | Required |
|---------------|---------|-----------------------------|---------|
| type  | string  | The value is always "datetime".  | Yes  |
| value  | string  | Date and time (YYYY-MM-DDThh:mm:ssZ format) | Yes  |

### Object Example
{% raw %}
```json
{
    "type": "date",
    "value": "2017-07-26T18:00:00Z"
}
```
{% endraw %}

## LocationObject {#LocationObject}
An object that contains coordinate data on a map.

### Object field
| Field name  | Type  | Field description  | Required |
|---------------|---------|-----------------------------|---------|
| type  | string  | The value is always "location".  | Yes  |
| value  | string  | Coordinate data on a map ({{book.OrientedService}} UTMK). The value is a pair of latitude and longitude.  | Yes  |

### Object Example
{% raw %}
```json
{
    "type": "location",
    "value": "349652984,149297371"
}
```
{% endraw %}

## NumberObject {#NumberObject}
An object that contains number data separated by thousands.

### Object field
| Field name  | Type  | Field description  | Required |
|---------------|---------|-----------------------------|---------|
| type  | string  | The value is always "number".  | Yes  |
| value  | string  | Number data separated by thousands | Yes  |

### Object Example
{% raw %}
```json
{
    "type": "number",
    "value": "19,304,213"
}
```
{% endraw %}

## PercentageObject {#PercentageObject}
An object that contains percentage data.

### Object field
| Field name  | Type  | Field description  | Required |
|---------------|---------|-----------------------------|---------|
| type  | string  | The value is always "percentage". | Yes  |
| value  | number  | Percentage  | Yes  |

### Object Example
{% raw %}
```json
{
    "type": "percentage",
    "value": 20.2341
}
```
{% endraw %}

## PhoneNumberObject {#PhoneNumberObject}
An object that contains phone number data.

### Object field
| Field name  | Type  | Field description  | Required |
|---------------|---------|-----------------------------|---------|
| type  | string  | The value is always "phoneNum". | Yes  |
| value  | string  | Phone number  | Yes  |

### Object Example
{% raw %}
```json
{
    "type": "phoneNum",
    "value": "031-784-1000"
}
```
{% endraw %}

## StringObject {#StringObject}
An object that contains text data.

### Object field
| Field name  | Type  | Field description  | Required |
|---------------|---------|-----------------------------|---------|
| type  | string  | The value is always "string".  | Yes  |
| value  | string  | Text  | Yes  |

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

## TemperatureCObject {#TemperatureCObject}
An object that contains temperature data in Celsius.

### Object field
| Field name  | Type  | Field description  | Required |
|---------------|---------|-----------------------------|---------|
| type  | string  | The value is always "temperature-c".  | Yes  |
| value  | number  | Temperature data in Celsius  | Yes  |

### Object Example
{% raw %}
```json
{
    "type": "temperature-c",
    "value": 31
}
```
{% endraw %}

## TemperatureFObject {#TemperatureFObject}
An object that contains temperature data in Fahrenheit.

### Object field
| Field name  | Type  | Field description  | Required |
|---------------|---------|-----------------------------|---------|
| type  | string  | The value is always "temperature-f".  | Yes  |
| value  | number  | Temperature data in Fahrenheit  | Yes  |

### Object Example
{% raw %}
```json
{
    "type": "temperature-f",
    "value": 75
}
```
{% endraw %}

## URLObject {#URLObject}
An object that contains URL data.

### Object field
| Field name  | Type  | Field description  | Required |
|---------------|---------|-----------------------------|---------|
| type  | string  | The value is always "url".  | Yes  |
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
