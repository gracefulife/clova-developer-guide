Access the <a href="https://developers.naver.com/console/clova/cek/#/list" target="_blank">Clova developer console</a> and register the basic information of the extension.
The main items are as follows:

* Extension information
	* **{{ book.DevConsole.cek_id }}**: The unique ID value of the extension. Generally uses a combination of the package name and extension name. Enter the ID of the Sample Dice extension as "my.clova.extension.sampledice."
	* **{{ book.DevConsole.cek_invocation_name }}**: The name used to call the extension. Select a word that can be easily recognized by the Clova app or speaker devices. The invocation name used for the Sample Dice extension is "Sample Dice."

* Server connection settings
	* **{{ book.DevConsole.cek_service_endpoint_url }}**: The REST API server of the extension to communicate with Clova. It must be a publicly accessible URL.
		In Step 1, enter the URL of the server that executed the Sample Dice code.

		<div class="note">
	    <p><strong>Note!</strong></p>
			<p>An HTTP connection can be used for testing, but an HTTPS connection is required for the official service. The extension server must use ports 80 and 443 for HTTP and HTTPS connections respectively.</p>
		</div>

	* **{{ book.DevConsole.cek_account_linking }}**: Only use when connecting with membership information of a 3rd party using an authorization server (based on OAuth 2.0).
		Set the Sample Dice extension as **{{ book.DevConsole.cek_no }}**.
* Deployment information and privacy and compliance information

	This information is required for extension review and deployment. You do not need to enter this information when following the tutorial.
