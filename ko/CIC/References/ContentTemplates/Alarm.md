# Alarm Template
CIC는 사용자가 알람을 생성하면 생성한 알람의 정보를 Alarm 템플릿 형태로 클라이언트에게 전달합니다. 클라이언트는 이 템플릿을 사용하여 사용자가 생성한 알람 정보를 화면에 표시해야 합니다.

<div class="note">
<p><strong>Note!</strong></p>
<p>Alarm 템플릿은 현재 다음과 같은 제약 사항이 있습니다.</p>
<ul>
  <li>사용자는 음성으로 알람 등록과 알람 목록 조회만 요청할 수 있습니다.</li>
  <li>사용자가 알람를 수정하거나 삭제하려면 Clova 앱을 이용해야 합니다.</li>
</ul>
</div>

## Template fields

| 필드 이름       | 자료형    | 필드 설명                     |
|---------------|---------|-----------------------------|
| `repeatDay[]`     | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject) array | 매주 반복되는 알람일 경우 반복할 요일 정보를 가지고 있는 객체 배열     |
| `repeatPeriod`  | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject)     | 반복 주기 정보를 가지는 객체입니다. 이 객체의 `value` 필드는 다음과 같은 값을 가집니다. <ul><li>빈 문자열(<code>""</code>): 일회성 알람 </li><li><code>"daily"</code>: 매일 반복되는 알람</li><li><code>"weekly"</code>: 매주 반복되는 알람</li></ul> |
| `scheduledTime` | [DateTimeObject](/CIC/References/ContentTemplates/Shared_Objects.md#DateTimeObject) | 알람이 울릴 날짜와 시간 정보를 가지는 객체                         |
| `token`         | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject)     | 추가한 알람의 식별자 정보가 담긴 객체                            |
| `type`          | string                                                                              | Content template 구분자. `"Alarm"` 값을 가집니다.             |

## Template example

{% raw %}

```json

// 일회성 알람
{
  "type": "Alarm",
  "token": {
    "type": "string",
    "value": "072c72b9-cfc5-4127-b4fe-557a10457232"
  },
  "scheduledTime": {
    "type": "datetime",
    "value": "2017-10-09T09:00:00Z"
  },
  "repeatPeriod": {
    "type": "string",
    "value": ""
  },
  "repeatDay": []
}

// 매일 반복되는 알람
{
  "type": "Alarm",
  "token": {
    "type": "string",
    "value": "b5403bd0-1598-495b-a466-9385c2b1103a"
  },
  "scheduledTime": {
    "type": "datetime",
    "value": "2017-10-09T09:00:00Z"
  },
  "repeatPeriod": {
    "type": "string",
    "value": "daily"
  },
  "repeatDay": []
}

// 매주 반복되는 알람
{
  "token": {
    "type": "string",
    "value": "da740e2a-01cd-4f2e-aedf-6c4285bae785"
  },
  "type": "Alarm",
  "scheduledTime": {
    "type": "datetime",
    "value": "2017-10-09T09:00:00Z"
  },
  "repeatPeriod": {
    "type": "string",
    "value": "weekly"
  },
  "repeatDay": [
    {
      "type": "string",
      "value": "monday"
    }
  ]
}
```

{% endraw %}

## UI example {#UIExample}

다음은 NAVER가 배포한 모바일용 Clova 앱에서 Alarm 템플릿의 내용을 표현한 UI 예제입니다.

![](/CIC/Resources/Images/Content_Template-Alarm.png)

## See also
* [AlarmList](/CIC/References/ContentTemplates/AlarmList.md)
* [Alerts](/CIC/References/CICInterface/Alerts.md) 인터페이스
