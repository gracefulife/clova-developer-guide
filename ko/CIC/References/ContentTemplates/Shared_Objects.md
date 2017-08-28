# Shared Objects
Content template은 일부 반복되는 데이터 타입을 표현하기 위해 다음과 같은 객체(Shared Objects)를 공유하여 사용합니다.

| 객체 이름            | 객체 설명                                            |
|--------------------|---------------------------------------------------|
| [CurrencyObject](#CurrencyObject)         | 통화와 금액 정보를 가지는 객체                   |
| [DateObject](#DateObject)                 | 날짜 정보를 가지는 객체                         |
| [DateTimeObject](#DateTimeObject)         | 날짜와 시간 정보를 가지는 객체                    |
| [LocationObject](#LocationObject)         | 지도 상의 좌표 정보(UTMK)를 가지는 객체           |
| [NumberObject](#NumberObject)             | 단위 구분자(1천 단위)가 처리된 숫자 정보를 가지는 객체 |
| [PercentageObject](#PercentageObject)     | 백분율 정보를 가지는 객체                        |
| [PhoneNumberObject](#PhoneNumberObject)   | 전화 번호 정보를 가지는 객체                     |
| [StringObject](#StringObject)             | 텍스트 정보를 가지는 객체                        |
| [TemperatureCObject](#TemperatureCObject) | 온도 정보(섭씨)를 가지는 객체                    |
| [TemperatureFObject](#TemperatureFObject) | 온도 정보(화씨)를 가지는 객체                    |
| [URLObject](#URLObject)                   | URL 정보를 가지는 객체                         |

# CurrencyObject {#CurrencyObject}
통화와 금액 정보를 가지는 객체입니다.

### Object field
| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|---------|
| `type`          | string  | `"currency"` 값으로 고정되어 있습니다.  | 필수     |
| `value`         | string  | 통화와 금액이 조합된 정보             | 필수     |

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
날짜 정보를 가지는 객체입니다.

### Object field
| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|---------|
| `type`          | string  | `"date"` 값으로 고정되어 있습니다.  | 필수     |
| `value`         | string  | 날짜 정보(YYYY-MM-DD 포맷)     | 필수     |

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
날짜와 시간 정보를 가지는 객체입니다.

### Object field
| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|---------|
| `type`          | string  | `"datetime"` 값으로 고정되어 있습니다.   | 필수     |
| `value`         | string  | 날짜와 시간 정보(YYYY-MM-DDThh:mm:ssZ 포맷) | 필수     |

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
지도 상의 좌표 정보를 가지는 객체입니다.

### Object field
| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|---------|
| `type`          | string  | `"location"` 값으로 고정되어 있습니다.                  | 필수     |
| `value`         | string  | 지도 상의 좌표 정보({{book.OrientedService}} UTMK). 위도와 경도 값의 쌍으로 구성됩니다.  | 필수     |

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
단위 구분자(1천 단위)가 처리된 숫자 정보를 가지는 객체입니다.

### Object field
| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|---------|
| `type`          | string  | `"number"` 값으로 고정되어 있습니다.    | 필수     |
| `value`         | string  | 단위 구분자(1천 단위)가 처리된 숫자 정보 | 필수     |

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
백분율 정보를 가지는 객체입니다.

### Object field
| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|---------|
| `type`          | string  | `"percentage"` 값으로 고정되어 있습니다. | 필수     |
| `value`         | number  | 백분율 정보                         | 필수     |

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
전화 번호 정보를 가지는 객체입니다.

### Object field
| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|---------|
| `type`          | string  | `"phoneNum"` 값으로 고정되어 있습니다. | 필수     |
| `value`         | string  | 전화 번호 정보                    | 필수     |

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
텍스트 정보를 가지는 객체입니다.

### Object field
| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|---------|
| `type`          | string  | `"string"` 값으로 고정되어 있습니다.  | 필수     |
| `value`         | string  | 텍스트 정보                      | 필수     |

### Object Example
{% raw %}
```json
// 예제 1
{
    "type": "string",
    "value": "토트넘 입단 손흥민 “EPL 항상 꿈꿔왔던 무대”"
}

// 예제 2
{
    "type": "string",
    "value": "네이버 검색결과"
}
```
{% endraw %}

## TemperatureCObject {#TemperatureCObject}
섭씨 단위의 온도 정보를 가지는 객체입니다.

### Object field
| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|---------|
| `type`          | string  | `"temperature-c"` 값으로 고정되어 있습니다.   | 필수     |
| `value`         | number  | 섭씨 단위의 온도 정보                      | 필수     |

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
화씨 단위의 온도 정보를 가지는 객체입니다.

### Object field
| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|---------|
| `type`          | string  | `"temperature-f"` 값으로 고정되어 있습니다.   | 필수     |
| `value`         | number  | 화씨 단위의 온도 정보                      | 필수     |

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
URL 정보를 가지는 객체입니다.

### Object field
| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|---------|
| `type`          | string  | `"url"` 값으로 고정되어 있습니다.   | 필수     |
| `value`         | string  | URL 정보                        | 필수     |

### Object Example
{% raw %}
```json
// 예제 1
{
    "type": "url",
    "value": "https://m.search.naver.com/search.naver?where=m_image&mode=default&query=%EC%86%90%ED%9D%A5%EB%AF%BC%20%EC%9D%B4%EB%AF%B8%EC%A7%80#imgId=news4100000269062_1"
}

// 예제 2
{
    "type": "url",
    "value": "https://search.pstatic.net/common/?src=http%3A%2F%2Fimgnews.naver.com%2Fimage%2F410%2F2015%2F08%2F31%2F20150831_1441012614_99_20150831181804.jpg&type=b360"
}
```
{% endraw %}
