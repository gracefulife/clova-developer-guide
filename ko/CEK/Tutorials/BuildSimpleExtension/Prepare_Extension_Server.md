Extension 서버는 Clova와 통신하여 사용자 요청을 처리하는 REST API 서버로, extension을 서비스하기 위해 반드시 필요합니다.

Extension 서버를 만들려면 HTTP를 사용하여 메시지를 주고받는 코드를 작성해야 합니다.
여기서는 가능한 빨리 extension을 만들어 보기 위해 직접 서버를 구축하는 대신 이미 만들어진 extension을 사용합니다.

Clova가 서비스하는 '주사위 놀이'라는 extension은 소스 코드가 공개되어 있습니다.
소스 코드를 받아 실행해보려면 다음과 같은 것들이 필요합니다.

| 항목     | 설명                               | 필수 여부 |
|---------|-----------------------------------|:-------:|
| <a href="https://git-scm.com/" target="_blank">git</a>    | 소스 코드 다운로드에 필요합니다.          | 선택     |
| <a href="https://nodejs.org/" target="_blank">node.js</a> | Extension 서버 실행에 필요합니다.          | 필수     |
| <a href="https://chrome.google.com/webstore/detail/postman/fhbjgbiflinjbdggehcddcbncdddomop">Postman Chrome extension</a> | Extension 서버가 동작하는지 확인할 때 필요합니다. | 선택     |

필요한 소프트웨어를 설치한 후 아래처럼 주사위 놀이 extension 소스 코드를 다운로드 받고 실행합니다. `tutorial-dice` 브랜치를 사용합니다.

{% raw %}
```bash
git clone https://github.com/naver/clova-extension-sample-dice.git
cd clova-extension-sample-dice
git checkout tutorial-dice
npm install
node app.js
```
{% endraw %}

이렇게 실행한 extension 서버가 잘 동작하는지 확인하려면 Postman을 사용해 요청을 보내면 됩니다. 자세한 방법은 <a href="https://github.com/naver/clova-extension-sample-dice" target="_blank">주사위 놀이 extension github 페이지</a>에서 볼 수 있습니다.

위의 방식대로 잘 실행되는 것을 확인하면, 외부에서 접근 가능한 서버로 옮겨 실행합니다.

### Extension 서버 개발 팁 {#Tip}
{% include "/CEK/Tutorials/BuildSimpleExtension/Extension_Server_Development_Tip.md" %}
