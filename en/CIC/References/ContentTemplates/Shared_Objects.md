# Shared Objects
Content templates use the following shared objects to display repetitive data types.

| Object name            | Object description                                            |
|--------------------|---------------------------------------------------|
| [ActionObject](#ActionObject)             | An object containing possible action information of the client.          |
| [CurrencyObject](#CurrencyObject)         | An object containing currency and amount                   |
| [DateObject](#DateObject)                 | An object containing a date                         |
| [DateTimeObject](#DateTimeObject)         | An object containing date and time                    |
| [LocationObject](#LocationObject)         | An object containing coordinates (UTMK) of a map           |
| [NumberObject](#NumberObject)             | An object containing a number, separated by thousands |
| [PercentageObject](#PercentageObject)     | An object containing a percentage                        |
| [PhoneNumberObject](#PhoneNumberObject)   | An object containing a phone number                     |
| [StringObject](#StringObject)             | An object containing text                        |
| [TemperatureCObject](#TemperatureCObject) | An object containing a temperature (Celsius)                    |
| [TemperatureFObject](#TemperatureFObject) | An object containing a temperature (Fahrenheit)                    |
| [URLObject](#URLObject)                   | An object containing a URL                         |


# ActionObject {#ActionObject}
| An object containing possible action information of the client.

### Object field
| Field name       | Type    | Field description                     | Required |
|---------------|---------|-----------------------------|---------|
| `type`          | string  | The value is always `"action"`.  | Yes     |
| `value`         | string  | [Action URL scheme](/CIC/References/ContentTemplates/Common_Fields.md#ActionURLScheme) Action information of the format | Yes     |

### Object Example
{% raw %}

```json
{
    "type": "action",
    "value": "clova://naverSearch?query=이태원맛집"
}
```

{% endraw %}

# CurrencyObject {#CurrencyObject}
An object containing currency and amount.

### Object field
| Field name       | Type    | Field description                     | Required |
|---------------|---------|-----------------------------|---------|
| `type`          | string  | The value is always `"currency"`.  | Yes     |
| `value`         | string  | Data in combination of currency and amount               | Yes     |

### Object Example
{% raw %}

```json
{
    "type": "currency",
    "value": "KRW500000"
}
```

{% endraw %}

## DateObject {#DateObject}
An object containing a date.

### Object field
| Field name       | Type    | Field description                     | Required |
|---------------|---------|-----------------------------|---------|
| `type`          | string  | The value is always `"date"`.  | Yes     |
| `value`         | string  | A date (YYYY-MM-DD format)     | Yes     |

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
An object containing date and time.

### Object field
| Field name       | Type    | Field description                     | Required |
|---------------|---------|-----------------------------|---------|
| `type`          | string  | The value is always `"datetime"`.   | Yes     |
| `value`         | string  | Date and time (YYYY-MM-DDThh:mm:ssZ format) | Yes     |

### Object Example
{% raw %}

```json
{
    "type": "datetime",
    "value": "2017-07-26T18:00:00Z"
}
```

{% endraw %}

## LocationObject {#LocationObject}
An object containing map coordinates.

### Object field
| Field name       | Type    | Field description                     | Required |
|---------------|---------|-----------------------------|---------|
| `type`          | string  | The value is always `"location"`.                  | Yes     |
| `value`         | string  | Map coordinates ({{book.OrientedService}} UTMK). The value is a pair of latitude and longitude.  | Yes     |

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
An object containing a number separated by thousands.

### Object field
| Field name       | Type    | Field description                     | Required |
|---------------|---------|-----------------------------|---------|
| `type`          | string  | The value is always `"number"`.    | Yes     |
| `value`         | string  | A number separated by thousands | Yes     |

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
An object containing a percentage.

### Object field
| Field name       | Type    | Field description                     | Required |
|---------------|---------|-----------------------------|---------|
| `type`          | string  | The value is always `"percentage"`. | Yes     |
| `value`         | number  | A percentage                         | Yes     |

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
An object containing a phone number.

### Object field
| Field name       | Type    | Field description                     | Required |
|---------------|---------|-----------------------------|---------|
| `type`          | string  | The value is always `"phoneNum"`. | Yes     |
| `value`         | string  | A phone number                    | Yes     |

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
An object containing text.

### Object field
| Field name       | Type    | Field description                     | Required |
|---------------|---------|-----------------------------|---------|
| `type`          | string  | The value is always `"string"`.  | Yes     |
| `value`         | string  | Text                      | Yes     |

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
    "value": "Search Result"
}
```

{% endraw %}

## TemperatureCObject {#TemperatureCObject}
An object containing a temperature in Celsius.

### Object field
| Field name       | Type    | Field description                     | Required |
|---------------|---------|-----------------------------|---------|
| `type`          | string  | The value is always `"temperature-c"`.   | Yes     |
| `value`         | number  | A temperature in Celsius                      | Yes     |

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
An object containing a temperature in Fahrenheit.

### Object field
| Field name       | Type    | Field description                     | Required |
|---------------|---------|-----------------------------|---------|
| `type`          | string  | The value is always `"temperature-f"`.   | Yes     |
| `value`         | number  | A temperature in Fahrenheit                      | Yes     |

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
An object containing a URL.

### Object field
| Field name       | Type    | Field description                     | Required |
|---------------|---------|-----------------------------|---------|
| `type`          | string  | The value is always `"url"`.   | Yes     |
| `value`         | string  | A URL                        | Yes     |

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
