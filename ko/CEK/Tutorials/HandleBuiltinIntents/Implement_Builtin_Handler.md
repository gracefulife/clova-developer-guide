샘플 주사위 extension이 built-in intent를 받았을 때 처리할 수 있도록 extension 서버를 구현해야 합니다.

Clova가 제공하는 built-in intent에는 도움말 요청, 긍정 또는 부정, 취소 요청 등이 있는데, 샘플 주사위는 기본적인 처리 방법을 알아보기 위해 도움말 요청 intent만 처리하도록 합니다.
도움말 요청 intent는 사용자가 "어떻게 사용해", "도움말 알려줘" 같은 말을 할 때 전송되는 intent로, `Clova.GuideIntent`라는 이름을 사용합니다.

이 intent를 처리하기 위해 다음과 같이 [첫 번째 튜토리얼](/CEK/Tutorials/Build_Simple_Extension.md)의 저장소를 재사용합니다.
다음과 같이 로컬 저장소로 이동하여 `tutorial/step2` 브랜치로 전환합니다.

{% raw %}
```bash
cd /path/to/your_sample_dice_directory
git fetch
git checkout tutorial/step2
```
{% endraw %}

샘플 주사위 extension은 `clova/index.js` 파일의 `intentRequest()`에서 도움말 요청을 처리합니다.

{% raw %}
```javascript
intentRequest(cekResponse) {
  const intent = this.request.intent.name

  switch (intent) {
    ...
    case 'Clova.GuideIntent':
      cekResponse.appendSpeechText("주사위 한 개 던져줘, 라고 시도해보세요.")
      break
    ...
  }
  ...
}
```
{% endraw %}

위 코드에서 보는 것처럼, Clova로부터 받은 요청 메시지에서 intent를 추출하여 그 이름이 `Clova.GuideIntent`일 때 "주사위 한 개 던져줘"라고 시도하도록 알려줍니다.
