# Memo Template

The Memo template is used in providing memo information for the client to display on the client's screen.
When the user creates a memo, CIC sends the memo to the client, in the form of the Memo template.

<div class="note">
<p><strong>Note!</strong></p>
<p>The following is the restrictions in using memo:</p>
<ul>
  <li>Voice requests can be used only to add a memo or to check a list of memos.</li>
  <li>To modify or delete a memo, the user must use the Clova app.</li>
</ul>
</div>

## Template fields

| Field name       | Type    | Description                     |
|---------------|---------|-----------------------------|
| `content`     | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject)     | Contains the memo.  |
| `timestamp`   | [DateTimeObject](/CIC/References/ContentTemplates/Shared_Objects.md#DateTimeObject) | The time at which this memo was created. |
| `token`       | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject)     | The ID of this memo. |
| `type`        | string                                                                              | The type of this template. The value is always `"Memo"`.             |

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
    "value": "My WiFi password: 12345678"
  },
  "timestamp": {
    "type": "datetime",
    "value": "2017-12-24T00:00:00Z"
  }
}
```

{% endraw %}

## UI example {#UIExample}

<div class="note">
<p><strong>Note!</strong></p>
<p>An example for the Memo template is in preparation.</p>
</div>

## See also

* [MemoList](/CIC/References/ContentTemplates/MemoList.md)
