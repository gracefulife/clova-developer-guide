Once you have checked that the interaction model is working properly, you must check that speech recognition and response is operating as intended on a real device before requesting a review.

### Registering a tester ID
Register a tester ID to specify an account to execute the extension.

1. Access the <a href="https://developers.naver.com/console/clova/cek/#/list" target="_blank">Clova developer console</a>.
2. Click the **{{ book.DevConsole.cek_edit }}** button on the **{{ book.DevConsole.cek_skill_info }}** item of the Sample Dice extension.
3. Find **{{ book.DevConsole.cek_tester }}** on the displayed screen and enter your {{ book.OrientedService }} account ID.
4. Click the **{{ book.DevConsole.cek_save }}** button.

<div class="note">
  <p><strong>Note!</strong></p>
  <p>Wait for a short while after registering the tester ID to test the extension. If you are unable to test the extension even after an hour, inquire on the forum or contact the partnership team.</p>
</div>

<div class="danger">
	<p><strong>Caution!</strong></p>
  <p>To test on a real device, you must register an actual extension server URL that can be accessed externally in <strong>{{ book.DevConsole.cek_skill_info }}</strong>.</p></li>
</div>

### Running from the Clova app
Run the Sample Dice extension using the Clova app.

1. Install the Clova app on the testing device.
2. Log in using the {{ book.OrientedService }} account registered as your tester ID.
3. Make a voice command using the invocation name of the tested extension. For example, say “Clova, ask Sample Dice to roll a dice."
4. Check whether the Clova app responds with "Throwing 1 dice."

If the extension operates well on the real device, then it is ready to be serviced. You can now request a review on the Clova developer console and deploy the extension.

