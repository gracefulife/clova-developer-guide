# Memo Template
When the user creates a memo, CIC passes the memo detail in Memo template format to the client. The client should display the memo details on the screen using the received template.

<div class="note">
<p><strong>Note!</strong></p>
<p>Currently, there are limits to the Memo template as below.</p>
<ul>
  <li>With the voice command, the user can only request to add a memo and check the list.</li>
  <li>In order to modify or delete a memo, the user should use the Clova app.</li>
</ul>
</div>

## Template field

| Field name       | Type    | Field description                     |
|---------------|---------|-----------------------------|
| `content`     | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject)     | An object containing a memo  |
| `timestamp`   | [DateTimeObject](/CIC/References/ContentTemplates/Shared_Objects.md#DateTimeObject) | An object containing the time when the memo was added |
| `token`       | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject)     | An object containing identifier of an added memo.  |
| `type`        | string                                                                              | A content template delimiter. It has an `"Memo"` value.             |

## Template example

{% raw %}

```json
{
  "type": "Memo",
  "token": {
    "type": "string",
    "value": "072c72b9-cfc5-4127-b4fe-557a10457232"
  },
  "content": {
    "type": "string",
    "value": "내 와이파이 비밀번호: 12345678"
  },
  "timestamp": {
    "type": "datetime",
    "value": "2017-12-24T00:00:00Z"
  }
}
```

{% endraw %}

## Screen UI example {#UIExample}

<div class="note">
<p><strong>Note!</strong></p>
<p>Preparing for an example of a screen which applied a Memo template.</p>
</div>

## See also
* [MemoList](/CIC/References/ContentTemplates/MemoList.md)