Once you have checked that the interaction model is working properly, you must check that speech recognition and responses are operating as intended on an actual device before requesting a review.

### Registering a tester ID
Register a tester ID to specify an account to execute the extension.

1. Access the <a href="https://developers.naver.com/console/clova/cek/#/list" target="_blank">Clova developer console</a>.
2. Click the **{{ book.DevConsole.cek_edit }}** button on the **{{ book.DevConsole.cek_skill_info }}** item of the Sample Dice extension.
3. Find **{{ book.DevConsole.cek_tester }}** on the displayed screen and enter your {{ book.OrientedService }} account ID.
4. Click the **{{ book.DevConsole.cek_save }}** button.

<div class="note">
  <p><strong>Note!</strong></p>
  <p>Wait a short while after registering the tester ID to test the extension. If you are unable to test the extension even after an hour, post your issue on the forum or contact the partnership team.</p>
</div>

<div class="danger">
	<p><strong>Caution!</strong></p>
  <p>To test on an actual device, you must register an externally accessible actual extension server URL in <strong>{{ book.DevConsole.cek_skill_info }}</strong>.</p></li>
</div>

### Running from the Clova app
Run the Sample Dice extension using the Clova app.

1. Install the Clova app on the testing device.
2. Log in using the {{ book.OrientedService }} account registered as your tester ID.
3. Make a voice command using the invocation name of the tested extension. For example, say "Clova, ask Sample Dice to roll a die."
4. Check whether the Clova app responds with "Throwing 1 die."

The extension is ready for service once it is confirmed to operate correctly on an actual device. You can now request a review on the Clova developer console and deploy the extension.
