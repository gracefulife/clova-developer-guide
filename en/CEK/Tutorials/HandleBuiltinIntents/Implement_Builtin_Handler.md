You must change the code so that the Sample Dice extension can handle built-in intents.

To help you understand the basic handling method, this section of the tutorial will have you set your extension to handle the help request built-in intent only.
The help request built-in intent is sent when user utterances contain phrases such as "How do I use this?" or "I need help." It uses the name, `Clova.GuideIntent`.

In order to handle this built-in intent, we will reuse the repository from the [first tutorial](/CEK/Tutorials/Build_Simple_Extension.md).
Go to the local repository and check out the `tutorial2` branch as shown below:

{% raw %}
```bash
cd /path/to/your_sample_dice_directory
git fetch
git checkout tutorial2
```
{% endraw %}

The Sample Dice extension handles the help request in the `intentRequest()` of the `clova/index.js` file.

{% raw %}
```javascript
intentRequest(cekResponse) {
  const intent = this.request.intent.name

  switch (intent) {
    ...
    case 'Clova.GuideIntent':
    default:
      cekResponse.setSimpleSpeechText (Try saying "Throw one die.")
  }
  ...
}
```
{% endraw %}

As shown from the codes above, the intent is extracted from the request message sent from Clova. If the intent name is `Clova.GuideIntent`, it prompts the user to try saying "Throw one die."
