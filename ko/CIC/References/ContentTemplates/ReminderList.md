# ReminderList Template
CIC는 사용자가 리마인더의 목록을 요청하면 사용자에게 등록된 리마인더의 목록을 ReminderList 템플릿 형태로 클라이언트에게 전달합니다. 클라이언트는 이 템플릿을 사용하여 사용자가 등록한 리마인더 목록을 화면에 표시해야 합니다.

<div class="note">
<p><strong>Note!</strong></p>
<p>ReminderList 템플릿은 현재 다음과 같은 제약 사항이 있습니다.</p>
<ul>
  <li>사용자는 음성으로 리마인더 등록과 리마인더 목록 조회만 요청할 수 있습니다.</li>
  <li>사용자가 리마인더를 수정하거나 삭제하려면 Clova 앱을 이용해야 합니다.</li>
</ul>
</div>

## Template field

| 필드 이름       | 자료형    | 필드 설명                     |
|---------------|---------|-----------------------------|
| `reminderList[]`               | object array  | 사용자가 등록한 리마인더 목록을 가지는 객체 배열.                                                                                          |
| `reminderList[].content`       | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject)     | 리마인더에 사용자가 입력한 내용이 담긴 객체 |
| `reminderList[].repeatDay`     | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject) array | 매주 반복되는 리마인더일 경우 반복할 요일 정보를 가지고 있는 객체 배열 |
| `reminderList[].repeatPeriod`  | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject)     | 반복 주기 정보를 가지는 객체입니다. 이 객체의 `value` 필드는 다음과 같은 값을 가집니다. <ul><li>빈 문자열(<code>""</code>) : 일회성 리마인더</li><li><code>"daily"</code> : 매일 반복되는 리마인더</li><li><code>"weekly"</code> : 매주 반복되는 리마인더</li></ul> |
| `reminderList[].status`        | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject)     | 리마인더의 처리 여부를 나타내는 객체입니다. 이 객체의 `value` 필드는 다음과 같은 값을 가집니다. <ul><li><code>"TODO"</code> : 미완료된 리마인더</li><li><code>"DONE"</code> : 완료된 리마인더</li></ul> |
| `reminderList[].scheduledTime` | [DateTimeObject](/CIC/References/ContentTemplates/Shared_Objects.md#DateTimeObject) | 리마인더가 울릴 날짜와 시간 정보를 가지는 객체      |
| `type`        | string                                                                                                | Content template 구분자. `"ReminderList"` 값을 가집니다.             |

## Template Example

{% raw %}

```json
{
  "type": "ReminderList",
  "reminderList": [
    {
      "scheduledTime": {
        "type": "datetime",
        "value": "2017-10-01T14:00:00Z"
      },
      "content": {
        "type": "string",
        "value": "입금하기"
      }
    },
    {
      "scheduledTime": {
        "type": "datetime",
        "value": "2017-10-01T14:00:00Z"
      },
      "content": {
        "type": "string",
        "value": "소개팅 준비"
      }
    }
  ]
}
```

{% endraw %}

## Screen UI example {#UIExample}

<div>
<p><strong>Note!</strong></p>
<p>ReminderList 템플릿이 사용된 화면 예제를 준비하고 있습니다.</p>
</div>

## See also
* [Alerts](/CIC/References/CICInterface/Alerts.md) 인터페이스
* [Reminder](/CIC/References/ContentTemplates/Reminder.md)
