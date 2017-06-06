# Shared Objects
Content Template은 다음과 같은 객체(Shared Objects)를 공유하여 사용합니다.

| 객체 이름            | 객체 설명                                            |
|--------------------|---------------------------------------------------|
| [DateObject](#DateObject)               | 날짜 정보를 가진 객체                         |
| [NumberObject](#NumberObject)           | 단위 구분자(1천 단위)가 처리된 숫자 정보를 가진 객체 |
| [PhoneNumberObject](#PhoneNumberObject) | 전화 번호 정보를 가진 객체                     |
| [StringObject](#StringObject)           | 텍스트 정보를 가진 객체                       |
| [URLObject](#URLObject)                 | URL 정보를 가진 객체                        |

## DateObject {#DateObject}
날짜 정보를 가진 객체입니다.

### Object field
| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|---------|
| type          | string  | "date" 값으로 고정되어 있습니다.  | 필수     |
| value         | string  | URL                         | 필수     |

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
없음

## NumberObject {#NumberObject}
단위 구분자(1천 단위)가 처리된 숫자 정보를 가진 객체입니다.

### Object field
| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|---------|
| type          | string  | "number" 값으로 고정되어 있습니다.    | 필수     |
| value         | string  | 단위 구분자(1천 단위)가 처리된 숫자 정보 | 필수     |

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
없음

## PhoneNumberObject {#PhoneNumberObject}
전화 번호 정보를 가진 객체입니다.

### Object field
| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|---------|
| type          | string  | "phoneNum" 값으로 고정되어 있습니다. | 필수     |
| value         | string  | 전화 번호 정보                    | 필수     |

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
없음

## StringObject {#StringObject}
텍스트 정보를 가진 객체입니다.

### Object field
| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|---------|
| type          | string  | "string" 값으로 고정되어 있습니다.  | 필수     |
| value         | string  | 텍스트 정보                      | 필수     |

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

### See also
없음

## URLObject {#URLObject}
URL 정보를 가진 객체입니다.

### Object field
| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|---------|
| type          | string  | "url" 값으로 고정되어 있습니다.   | 필수     |
| value         | string  | URL                         | 필수     |

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

### See also
없음
