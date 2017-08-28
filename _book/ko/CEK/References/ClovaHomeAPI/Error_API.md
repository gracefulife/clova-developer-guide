## Error API {#ErrorAPI}
Clova Home extension이 CEK에게 오류를 반환할 때 사용되는 API입니다.


| 메시지 이름         | 메시지 타입  | 메시지 설명                                   |
|------------------|-----------|---------------------------------------------|
| [`DriverInternalError`](#DriverInternalError) | Error Response | 내부적인 오류가 발생하면 CEK에게 이 메시지를 응답으로 보냅니다.             |
| [`TargetOfflineError`](#TargetOfflineError)   | Error Response | 대상 기기에 접속할 수 없으면(offline) CEK에게 이 메시지를 응답으로 보냅니다. |
| [`ValueOutOfRangeError`](#ValueOutOfRangeError) | Error Resposne | 사용자가 대상 기기가 처리할 수 없는 범위의 동작을 요청한 경우 CEK에게 이 메시지를 응답으로 보냅니다. |

<div class="note">
<p><strong>Note!</strong></p>
<p>오류 메시지 종류를 계속 추가할 예정입니다.</p>
</div>

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

### TargetOfflineError {#TargetOfflineError}
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

### ValueOutOfRangeError {#ValueOutOfRangeError}
사용자가 대상 기기가 처리할 수 없는 범위의 동작을 요청한 경우 CEK에게 이 메시지를 응답으로 보냅니다. 예를 들면, 에어컨에 설정할 수 있는 희망 온도 값이 18에서 28 사이인데 사용자가 16이나 30과 같은 값을 설정하도록 요청한 상황에 이 메시지가 사용될 수 있습니다. `payload` 필드에 대상 기기가 처리할 수 있는 최대치와 최소치를 전달해야 합니다.

#### Payload field

| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|---------|
| `maximumValue` | number | 대상 기기가 허용하는 설정 값의 최대치 | 필수    |
| `minimumValue` | number | 대상 기기가 허용하는 설정 값의 최소치 | 필수    |

#### Remarks
`payload`에 입력한 값은 사용자 안내에 사용될 수 있습니다.

#### Message example

{% raw %}
```json
{
  "header": {
    "messageId": "fef949b7-eb94-4bda-a417-2cfb604194c3",
    "namespace": "ClovaHome",
    "name": "ValueOutOfRangeError",
    "payloadVersion": "1.0"
  },
  "payload": {
    "minimumValue":18.0,
    "maximumValue":30.0
  }
}
```
{% endraw %}

#### See also
* [`DriverInternalError`](#DriverInternalError)
