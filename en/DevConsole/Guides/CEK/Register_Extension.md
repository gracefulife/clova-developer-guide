# Registering an extension
If you are developing or have developed a [custom extension](/CEK/Guides/Build_Custom_Extension.md) or a [Clova Home extension](/CEK/Guides/Build_Clova_Home_Extension.md), you must register it on the Clova developer console. To register a new extension, press the **{{ book.DevConsole.cek_builder_new_extension_create }}** button on the bottom of the CEK menu page.

![](/DevConsole/Resources/Images/DevConsole-First_Look_of_Extension_List.png)

To register an extension, you must typically complete the following steps in order:

1. [Agreeing to the terms and conditions and privacy policy](#AgreeTermsOfUse)
2. [Entering basic extension information](#InputExtensionInfo)
3. [Setting up a server connection](#SetServerConnection)
  * [Setting up account linking](#SetAccountLinking)

## Agreeing to the terms and conditions and privacy policy {#AgreeTermsOfUse}

In order to register an extension, you must first agree to the terms and conditions of the CEK API service and the privacy policy. The details on the terms and conditions and privacy policy is displayed only once and will not be displayed after you agree.

![](/DevConsole/Resources/Images/DevConsole-Agree_Terms_of_Use_and_Collecting_Personal_Info.png)

## Entering basic extension information {#InputExtensionInfo}

The first thing to do when registering an extension is to enter the basic extension information. The basic information of the extension is the first and essential information required for creating the extension on the Clova developer console. After you enter the basic extension information, you can access or edit the created extension on the CEK menu at any time.

Follow the steps below to register the extension:

![](/DevConsole/Resources/Images/DevConsole-Create_New_Extension.png)

<ol>
  <li>Select the type of extension to register from the <strong>{{ book.DevConsole.cek_type }}</strong> item. Once you select an extension type, an input field corresponding to the type is displayed.</li>
  <li>Select a language supported from the <strong>{{ book.DevConsole.cek_lang }}</strong> item. Currently, only <strong>{{ book.DevConsole.ko_KR }}</strong> is supported.</li>
  <li>Enter the extension's ID, name, and call name in the following fields:
    <ol>
      <li><strong>{{ book.DevConsole.cek_id }}</strong>: The unique ID of the extension. Use the reverse domain name notation for the ID. (e.g.: com.yourdomain.extension.pizzabot)</li>
      <li><strong>{{ book.DevConsole.cek_name }}</strong>: The name of the extension. The name is shown later on the Clova Extension Store.</li>
      <li><strong>{{ book.DevConsole.cek_invocation_name }}</strong>: The name of the extension that can be used by users to call the extension. The name can be a general name of an owned service, company, or organization, but it is more preferable to use a concise and unique name to increase user convenience. A universal word, or names of another company or its service, cannot be used. The <strong>{{ book.DevConsole.cek_invocation_name }}</strong> will be evaluated during the extension review process.</li>
      <li><strong>{{ book.DevConsole.cek_provider }}</strong>: The name or alias of the extension manufacturer (company or individual). This will be reviewed in the extension approval process and is shown later in the extension store.</li>
    </ol>
  </li>
  <li>If the extension uses the directive messages of the <a href="/CIC/References/CICInterface/AudioPlayer.html">AudioPlayer</a>, select <strong>{{ book.DevConsole.cek_yes }}</strong> from the <strong>{{ book.DevConsole.cek_audioplayer }}</strong> item. The extension uses the directive messages when it provides a music streaming service.</li>
  <li>Enter an email address for contact in the <strong>{{ book.DevConsole.cek_email }}</strong> item.</li>
  <li>Enter the {{ book.OrientedService }} account for testing the extension under development in the <strong>{{ book.DevConsole.cek_tester }}</strong> item. You do not need to enter the account information when registering the extension, but can enter it in this field when <a href="/DevConsole/Guides/CEK/Test_Extension.html">testing the extension</a> later on.</li>
  <li>After filling out the basic extension information, press the <strong>{{ book.DevConsole.cek_create }}</strong> button.</li>
</ol>

When you complete entering the basic extension information, you are directed to the screen to edit this information. From this point, you can press the **{{ book.DevConsole.cek_save }}** button at the bottom of the page at any time to save the changed details. You can also find the list of registered extensions in the CEK menu as shown below.

![](/DevConsole/Resources/Images/DevConsole-Extension_list_after_Creation.png)

## Setting up a server connection {#SetServerConnection}

The extension will make an HTTPS connection to CEK. Here, CEK sends an HTTP request to the extension and the extension sends an HTTP response to CEK. In order for CEK to send an HTTP request to the extension, you must set up a server connection from the Clova developer console. You can set up a server connection after you [enter the basic extension information](#InputExtensionInfo) for the created extension.

Make sure to check whether a connection with the extension server is available before registering the extension server. You can check the connection state using a simple curl command as shown in the example below.

{% raw %}
```bash
$ curl "https://yourdomain.com/pizzabot" -X POST
```
{% endraw %}

Follow the steps below to set up a connection with the server.

![](/DevConsole/Resources/Images/DevConsole-Extension_Server_Settings.png)

<ol>
  <li>Press the <strong>{{ book.DevConsole.cek_configuration }}</strong> tab above the extension information input UI.</li>
  <li>Enter the endpoint URL of the extension server in the <strong>{{ book.DevConsole.cek_service_endpoint_url }}</strong> item.
    <div class="note">
    <p><strong>Note!</strong></p>
    <p>An HTTP connection can be used for testing but an HTTPS connection is required for the official service. The extension server must use port 80 and 443 for HTTP and HTTPS connection respectively.</p>
  </div>
  </li>
  <li>If there is a need for linking the user account of the extension service and the Clova user account, select <strong>{{ book.DevConsole.cek_yes }}</strong> from the <strong>{{ book.DevConsole.cek_account_linking }}</strong> item. For more information on account linking, see <a href="#SetAccountLinking">Setting up account linking</a>.</li>
  <li>Press the radio button of the <strong>{{ book.DevConsole.cek_ssl_certificate }}</strong> item. The extension server must use the certificate of an authorized certificate agency.  (Self-signed certificates cannot be used.)</li>
  <li>Fill out the details for setting up the server connection and press the <strong>{{ book.DevConsole.cek_save }}</strong> button.</li>
</ol>

### Setting up account linking {#SetAccountLinking}

If a link between the user account of the extension service and the Clova user account is required, you must enter the [account linking](/CEK/Guides/Link_User_Account.md) information in [server connection settings](#SetServerConnection).

Follow the steps below to enter the [information required](/CEK/Guides/Link_User_Account.md#RegisterAccountLinkingInfo) to set up account linking.

<ol>
  <img src="/DevConsole/Resources/Images/DevConsole-Extension_Accoun_Linking_Settings_1.png" />
  <li>Select <strong>{{ book.DevConsole.cek_yes }}</strong> from the <strong>{{ book.DevConsole.cek_account_linking }}</strong> item.</li>
  <li>In the <strong>{{ book.DevConsole.cek_authorization_url }}</strong> item, enter the authorization URL where user can verify their account. The user is directed to this URL when the extension is activated.</li>
  <li>If you want to allow a user to set up their own account right away, enter the URL for the account setup page in the <strong>{{ book.DevConsole.cek_configuration_url }}</strong> item.</li>
  <li>Enter the <strong>{{ book.DevConsole.cek_client_id }}</strong> required for an HTTPS request when authenticating the user account. The client ID is the value created when <a href="/CEK/Guides/Link_User_Account.html#BuildAuthServer">building an authentication server</a>.</li>
  <li>In the <strong>{{ book.DevConsole.cek_privacy_policy_url }}</strong> item, enter the URL where privacy policy on the extension service is provided . The details on this page is shown later on the extension store.</li>
  <li>If the <strong>{{ book.DevConsole.cek_authorization_url }}</strong> or the page of the <strong>{{ book.DevConsole.cek_privacy_policy_url }}</strong> imports necessary resources from another domain, add the corresponding domain address in the <strong>{{ book.DevConsole.cek_domain_list }}</strong> item.</li>
  <li>If the usage scope of the access token—issued when linking user account—is predefined, add the predefined scope in the <strong>{{ book.DevConsole.cek_scope }}</strong> item.</li>
  <img src="/DevConsole/Resources/Images/DevConsole-Extension_Accoun_Linking_Settings_2.png" />
  <li>In the <strong>{{ book.DevConsole.cek_access_token_uri }}</strong> item, enter the URL to get the service access token. Currently, <strong>only the code grant method is supported for grant type</strong>.</li>
  <li>In the <strong>{{ book.DevConsole.cek_refresh_token_uri }}</strong> item, enter the URL to renew the service access token in.</li>
  <li>Enter the <strong>{{ book.DevConsole.cek_client_secret }}</strong> required for HTTPS requests when getting the service access token. The client secret is the value created when <a href="/CEK/Guides/Link_User_Account.html#BuildAuthServer">building an authentication server</a>.</li>
  <li>For <strong>{{ book.DevConsole.cek_client_authentication_scheme }}</strong>, set the value for implementing the authentication server interface.
    <ul>
      <li><strong>HTTP Basic (Recommended)</strong>: Select if the credentials are sent in the HTTP header data for getting the service access token.</li>
      <li><strong>Credentials in the request body</strong>: Select if the credentials are sent in HTTP body data for getting the service access token</li>
    </ul>
  </li>
</ol>

<div id="RedirectURI" class="note">
  <p><strong>Note!</strong></p>
  <p>The client URL (redirect URL) to be redirected after account authentication is <code>{{ book.RedirectURLforAccountLinking }}</code> and can be found in <strong>{{ book.DevConsole.cek_redirect_urls }}</strong>.</strong></p>
  <img src="/DevConsole/Resources/Images/DevConsole-Redirect_URL_for_Extension_Accoun_Linking.png" />
</div>
