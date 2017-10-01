# ScheduleList Template
CIC는 사용자가 캘린더 일정의 목록을 요청하면 사용자에게 등록된 일정의 목록을 ScheduleList 템플릿 형태로 클라이언트에게 전달합니다. 클라이언트는 이 템플릿을 사용하여 사용자가 등록한 일정 목록을 화면에 표시해야 합니다.

<div class="note">
<p><strong>Note!</strong></p>
<p>ScheduleList 템플릿은 현재 다음과 같은 제약 사항이 있습니다.</p>
<ul>
  <li>사용자가 캘린더 계정을 등록, 수정, 삭제하려면 Clova 앱을 이용해야 합니다.</li>
  <li>사용자는 음성으로 캘린더의 일정 등록과 일정 목록 조회만 요청할 수 있습니다.</li>
  <li>사용자가 캘린더의 일정을 수정하거나 삭제하려면 Clova 앱을 이용해야 합니다.</li>
</ul>
</div>

## Template field

| 필드 이름       | 자료형    | 필드 설명                     |
|---------------|---------|-----------------------------|
| `scheduledList[]`        | object array | 사용자가 등록한 일정 목록을 가지는 객체 배열   |
| `scheduledList[].content`       | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject)     | 추가한 일정에 사용자가 입력한 내용이 담긴 객체 |
| `scheduledList[].end`           | [DateTimeObject](/CIC/References/ContentTemplates/Shared_Objects.md#DateTimeObject) 또는 [DateObject](/CIC/References/ContentTemplates/Shared_Objects.md#DateObject)  | 추가한 일정의 종료 날짜와 시간. 종일 일정의 경우 DateObject 형태의 자료형을 가지며, 날짜 정보만 가집니다. |
| `scheduledList[].start`         | [DateTimeObject](/CIC/References/ContentTemplates/Shared_Objects.md#DateTimeObject) 또는 [DateObject](/CIC/References/ContentTemplates/Shared_Objects.md#DateObject)  | 추가한 일정의 시작 날짜와 시간. 종일 일정의 경우 DateObject 형태의 자료형을 가지며, 날짜 정보만 가집니다. |
| `scheduledList[].repeatDay`     | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject) array | 매주 반복되는 일정일 경우 반복할 요일 정보를 가지고 있는 객체 배열 |
| `scheduledList[].repeatPeriod`  | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject)     | 반복 주기 정보를 가지는 객체입니다. 이 객체의 `value` 필드는 다음과 같은 값을 가집니다. <ul><li>빈 문자열(<code>""</code>) : 일회성 일정 </li><li><code>"daily"</code> : 매일 반복되는 일정</li><li><code>"weekly"</code> : 매주 반복되는 일정</li></ul> |
| `type`        | string                                                                              | Content template 구분자. `"ScheduleList"`로 고정             |

## Template Example

{% raw %}

```json
{
  "type": "ScheduleList",
  "scheduledList": [
    {
      "type": "Schedule",
      "start": {
        "type": "datetime",
        "dateTime": "2017-09-30T12:00:00+09:00"
      },
      "end": {
        "type": "datetime",
        "dateTime": "2017-09-30T13:00:00+09:00"
      },
      "content": {
        "type": "string",
        "value": "친구 결혼식"
      },
      "repeatPeriod": {
        "type": "string",
        "value": ""
      },
      "repeatDay": []
    },
    {
      "type": "Schedule",
      "start": {
        "type": "datetime",
        "dateTime": "2017-08-02T10:00:00+09:00"
      },
      "end": {
        "type": "datetime",
        "dateTime": "2017-08-02T11:00:00+09:00"
      },
      "content": {
        "type": "string",
        "value": "데일리 스크럼"
      },
      "repeatPeriod": {
        "type": "string",
        "value": "daily"
      },
      "repeatDay": []
    },
    {
      "type": "Schedule",
      "start": {
        "type": "datetime",
        "dateTime": "2017-08-02T10:00:00+09:00"
      },
      "end": {
        "type": "datetime",
        "dateTime": "2017-08-02T11:00:00+09:00"
      },
      "content": {
        "type": "string",
        "value": "주간 회의"
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
    },
    {
      "type": "Schedule",
      "start": {
        "type": "date",
        "dateTime": "2017-09-29"
      },
      "end": {
        "type": "datetime",
        "dateTime": "2017-09-29"
      },
      "content": {
        "type": "string",
        "value": "플레이숍"
      },
      "repeatPeriod": {
        "type": "string",
        "value": ""
      },
      "repeatDay": []
    }
  ]
}
```

{% endraw %}

## Screen UI example {#UIExample}

<div>
<p><strong>Note!</strong></p>
<p>ScheduleList 템플릿이 사용된 화면 예제를 준비하고 있습니다.</p>
</div>

## See also
* [Alerts](/CIC/References/CICInterface/Alerts.md) 인터페이스
* [ScheduleListList](/CIC/References/ContentTemplates/ScheduleListList.md)
