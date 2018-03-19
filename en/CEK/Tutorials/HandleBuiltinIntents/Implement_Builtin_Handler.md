You must change the code so that the Sample Dice extension can handle the built-in intent.

To understand the basic handling method, set it to handle the built-in intent of the help request only.
The built-in intent of the help request is sent when the user says words, such as "How do I use it?" or "Give me help." It uses the name, `Clova.GuideIntent`.

In order to handle this built-in intent, we will reuse the repository of the [first tutorial](/CEK/Tutorials/Build_Simple_Extension.md).
Go to the local repository and switch to the `tutorial2` branch as shown below:

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
      cekResponse.setSimpleSpeechText (Try saying “Throw one dice.”)
  }
  ...
}
```
{% endraw %}

As shown from the codes above, the intent is extracted from the request message sent from Clova. If the intent name is `Clova.GuideIntent`, it prompts the user to try saying “Throw one dice.”

