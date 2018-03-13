The extension server is a REST API server that handles user intents by communicating with Clova and is mandatory in order to service the extension.

To create an extension server, you must design the code to exchange messages over an HTTP connection.
In order to create an extension quickly, this tutorial uses a completed extension with a configured server.

The source code of the Clova extension, Dice Drawer, is publicly available.
Before executing the source code, check the following items:

| Item     | Description                               | Required |
|---------|-----------------------------------|:-------:|
| <a href="https://git-scm.com/" target="_blank">git</a>    | Necessary for downloading the source code.          | Optional     |
| <a href="https://nodejs.org/" target="_blank">node.js</a> | Necessary for running the extension server.          | Required     |
| <a href="https://chrome.google.com/webstore/detail/postman/fhbjgbiflinjbdggehcddcbncdddomop" target="_blank">Postman Chrome extension</a> | Necessary for checking whether the extension server is operating. | Optional     |

After you have installed the necessary software, download the source code of the Dice Drawer extension and run it as shown below: Use `tutorial1` branch.

{% raw %}
```bash
git clone https://github.com/naver/clova-extension-sample-dice.git
cd clova-extension-sample-dice
git checkout tutorial1
npm install
node app.js
```
{% endraw %}

To check whether the extension server is operating properly, use Postman to send a request. For more information, see <a href="https://github.com/naver/clova-extension-sample-dice" target="_blank">Dice Drawer extension on GitHub</a>.

Once you have confirmed that the server is operating properly according to the method above, move to a server that can be externally accessed to run it.

