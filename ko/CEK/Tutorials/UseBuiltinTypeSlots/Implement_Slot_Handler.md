샘플 주사위 extension이 slot을 처리할 수 있도록 코드를 변경해야 합니다.
여기서는 사전에 구현된 소스 코드를 참고하여 어떤 부분이 변경되었는지 살펴보기 위해 [첫 번째 튜토리얼](/CEK/Tutorials/Build_Simple_Extension.md)의 저장소를 재사용합니다.
다음과 같이 로컬 저장소로 이동하여 `tutorial3` 브랜치로 전환합니다.

{% raw %}
```bash
cd /path/to/your_sample_dice_directory
git fetch
git checkout tutorial3
```
{% endraw %}

샘플 주사위 extension은 `clova/index.js` 파일의 `intentRequest()`에서 slot을 처리합니다.

{% raw %}
```javascript
intentRequest(cekResponse) {
  const intent = this.request.intent.name
  const slots = this.request.intent.slots

  switch (intent) {
    case "ThrowDiceIntent":
      let diceCount = 1
      if (!!slots) {
        const diceCountSlot = slots.diceCount
        if (slots.length != 0 && diceCountSlot) {
          diceCount = parseInt(diceCountSlot.value)
        }

        if (isNaN(diceCount)) {
          diceCount = 1
        }
      }
      ...
  }
  ...
}
```
{% endraw %}

위 코드에서 보는 것처럼, Clova로부터 받은 요청 메시지에서 slot 정보를 추출(`this.request.intent.slots`)한 뒤 , 앞서 interaction 모델에 등록한 "diceCount"라는 slot(`slots.diceCount`)이 있으면 그 값을 정수 형태로 읽어옵니다. 이렇게 읽은 값이 던질 주사위의 개수이며, slot이 없거나 정수 형태의 값인 아닌 경우에는 기본값인 1로 판단합니다.

변경된 코드를 extension 서버에서 실행합니다.
