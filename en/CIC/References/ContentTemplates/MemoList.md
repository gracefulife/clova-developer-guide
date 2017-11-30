# MemoList Template
When the user requests for a list of memo, CIC passes the memo list registered to the user in MemoList template format to the client. The client should display the memo list registered by the user on the screen using the received template.

<div class="note">
<p><strong>Note!</strong></p>
<p>Currently, there are limits to the MemoList template as below.</p>
<ul>
  <li>With the voice command, the user can only request to add a memo and check the list.</li>
  <li>In order to modify or delete a memo, the user should use the Clova app.</li>
</ul>
</div>

## Template field

| Field name       | Type    | Field description                     |
|---------------|---------|-----------------------------|
| `memoList[]`              | object array  | An object array containing the memo list registered by the user.                                       |
| `memoList[].content`      | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject)     | An object containing a memo  |
| `memoList[].lastModified` | [DateTimeObject](/CIC/References/ContentTemplates/Shared_Objects.md#DateTimeObject) | An object containing the latest time when the memo was modified |
| `memoList[].token`        | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject)     | An object containing identifier of a memo.  |
| `type`                    | string                                                                              | A content template delimiter. It has an `"MemoList"` value.             |

## Template example

{% raw %}

```json
{
  "type": "MemoList",
  "memoList": [
    {
      "token": {
        "type": "string",
        "value": "072c72b9-cfc5-4127-b4fe-557a10457232"
      },
      "content": {
        "type": "string",
        "value": "내 와이파이 비밀번호: 12345678"
      },
      "lastModified": {
        "type": "datetime",
        "value": "2017-12-24T00:00:00Z"
      }
    },
    {
      "token": {
        "type": "string",
        "value": "b5403bd0-1598-495b-a466-9385c2b1103a"
      },
      "content": {
        "type": "string",
        "value": "할 일 목록: 숙제하기, 여친 만들기"
      },
      "lastModified": {
        "type": "datetime",
        "value": "2017-12-24T01:00:00Z"
      }
    },
    {
      "token": {
        "type": "string",
        "value": "da740e2a-01cd-4f2e-aedf-6c4285bae785"
      },
      "content": {
        "type": "string",
        "value": "버킷 리스트: 100억 써보기, 아무것도 안하기, 72시간 잠자기"
      },
      "lastModified": {
        "type": "datetime",
        "value": "2017-12-24T02:00:00Z"
      }
    }
  ]
}
```

{% endraw %}

## Screen UI example {#UIExample}

<div class="note">
<p><strong>Note!</strong></p>
<p>Preparing for an example of a screen which applied a MemoList template.</p>
</div>

## See also
* [Memo](/CIC/References/ContentTemplates/Memo.md)