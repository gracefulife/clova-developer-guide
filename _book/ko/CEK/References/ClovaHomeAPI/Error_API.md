## Error API {#ErrorAPI}
Clova Home extension이 CEK에게 오류를 반환할 때 사용되는 API입니다.


| 메시지 이름         | 메시지 타입  | 메시지 설명                                   |
|------------------|-----------|---------------------------------------------|
| [`DriverInternalError`](#DriverInternalError)                                 | Error Response | 내부적인 오류가 발생하면 CEK에게 이 메시지를 응답으로 보냅니다.             |
| [`TargetOfflineError`](#TargetOfflineError)                                   | Error Response | 대상 기기에 접속할 수 없으면(offline) CEK에게 이 메시지를 응답으로 보냅니다. |

### DriverInternalError {#DriverInternalError}
내부적인 오류가 발생하면 CEK에게 이 메시지를 응답으로 보냅니다. CEK가 이 메시지를 전달받으면 미리 준비된 오류 메시지를 클라이언트에 전달합니다.

#### Payload field

없음

#### Remarks
* 오류 메시지도 정상적인 HTTPS 응답(200 OK)으로 CEK에게 메시지를 전달해야 합니다.
* 오류 메시지의 이름으로 상황을 판단하기 때문에 별도의 본문(payload)이 필요하지 않습니다.

#### Message example

{% raw %}
```json
{
  "header": {
    "messageId": "fef949b7-eb94-4bda-a417-2cfb604194c3",
    "namespace": "ClovaHome",
    "name": "DriverInternalError",
    "payloadVersion": "1.0"
  },
  "payload": {
  }
}
```
{% endraw %}

#### See also
* [`TargetOfflineError`](#TargetOfflineError)

### TargetOfflineError{#TargetOfflineError}
대상 기기에 접속할 수 없으면(offline) CEK에게 이 메시지를 응답으로 보냅니다. CEK가 이 메시지를 전달받으면 미리 준비된 오류 메시지를 클라이언트에 전달합니다.

#### Payload field

없음

#### Remarks
* 오류 메시지도 정상적인 HTTPS 응답(200 OK)으로 CEK에게 메시지를 전달해야 합니다.
* 오류 메시지의 이름으로 상황을 판단하기 때문에 별도의 본문(payload)이 필요하지 않습니다.

#### Message example

{% raw %}
```json
{
  "header": {
    "messageId": "fef949b7-eb94-4bda-a417-2cfb604194c3",
    "namespace": "ClovaHome",
    "name": "TargetOfflineError",
    "payloadVersion": "1.0"
  },
  "payload": {
  }
}
```
{% endraw %}

#### See also
* [`DriverInternalError`](#DriverInternalError)
