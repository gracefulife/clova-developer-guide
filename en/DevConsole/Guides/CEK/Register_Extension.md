# Registering extensions
If developing or developed a [custom extension](/CEK/Guides/Build_Custom_Extension.md) or a [Clova Home extension](/CEK/Guides/Build_Clova_Home_Extension.md), it should be registered on the Clova developer console. You may register a new extension by clicking **Create new extension** button at the bottom of the CEK menu page.

![](/DevConsole/Resources/Images/DevConsole-First_Look_of_Extension_list.png)

Process the below entries in order to register extensions.

1. [Enter basic information of your extension](#InputExtensionInfo)
2. [Server configuration](#SetServerConnection)
  * [Configure account linking](#SetAccountLinkning)

## Enter basic information of your extension {#InputExtensionInfo}

The first thing that must take place to register an extension is to enter basic information of your extension. The basic information is the most fundamental and essential data to register the extension. Registered extensions on the CEK menu can always be accessed and modified once they are registered with the basic information.

Register extensions following the below procedure

![](/DevConsole/Resources/Images/DevConsole-Create_New_Extension.png)

<ol>
  <li>Select extension type from the <strong>Type</strong> field. If the extension type is selected, a relevant input field will appear.</li>
  <li>From <strong>Select Language</strong> field, select a language to be used from your extension. Only <strong>Korean</strong> is supported at the moment.</li>
  <li>Enter Extension ID, name, call name data on the following entries.
    <ol>
      <li><strong>Extension ID</strong>: A unique ID of your extension. Enter in reversed FQDN format (Ex. com.yourdomain.extension.weathernotifier).</li>
      <li><strong>Name</strong>: A name of your extension. The name will be exposed to the Clova extension store.</li>
      <li><strong>Call name</strong>: A name for a user to call your extension. Common words cannot be used.</li>
    </ol>
  </li>
  <li>Select <strong>Audio Player Use</strong> field as <strong>Yes</strong> (if your extension is using a <a href="/CIC/References/CICInterface/AudioPlayer.html">AudioPlayer</a> directive message). The audio player will be used to serve music streaming service.</li>
  <li>Click <strong>Create</strong> button after inputting all the basic information.</li>
</ol>

Upon clicking the button, the page will be navigated to a modification page where created extension information can be modified. Added information can be saved at anytime by clicking **Save** button at the bottom of the page. The extension list registered on the CEK menu can be viewed as below.

![](/DevConsole/Resources/Images/DevConsole-Extension_list_after_Creation.png)

## Server configuration {#SetServerConnection}

Your extension communicate with CEK by using HTTPS. CEK will dispatch HTTP request to the extension and the extension will return HTTP response to CEK. For CEK to send HTTP request to the extension, the server configuration has to be performed from the Clova developer console. After [entering basic information of your extension](#InputExtensionInfo), the server configuration can be performed at the created extension.

Process the server configuration by following the procedure.

![](/DevConsole/Resources/Images/DevConsole-Extension_Server_Settings.png)

<ol>
  <li>Click <strong>server configuration</strong> tab located at the top of Entering extension information UI.</li>
  <li>Enter server URL (endpoint) of your extension data on the <strong>Service server URL</strong> field.</li>
  <li>Select <strong>Yes</strong> from <strong>Account connection</strong> field (if a user account of your extension service and a user account of Clova should be connected). To find more about account connection, see <a href="#SetAccountLinking">Configure account linking</a> </li>
  <li>Click the radio button from <strong>SSL authentication</strong> field. A server providing extensions must use a certificate officially approved from certificate authority. (Self-signed certificate is not allowed)</li>
  <li>Click <strong>Save</strong> after entering server configuration.</li>
</ol>

### Configure account linking {#SetAccountLinkning}

Enter [account linking](/CEK/Guides/Link_User_Account.md) information on the [Server configuration](#SetServerConnection) precedure if a user account of your extension service and a user account of Clova should to be connected.

Enter [information required](/CEK/Guides/Link_User_Account.md#RegisterAccountLinkingInfo) to configure account linking according to the following procedure.

<ol>
  <img src="/DevConsole/Resources/Images/DevConsole-Extension_Accoun_Linking_Settings_1.png" />
  <li>Select <strong>Yes</strong> from the <strong>Account linking</strong> field. </li>
  <li>Enter an Authorization URL providing a UI page for users to authorize account on <strong>Login URL</strong>. If users activate the extension, it will navigate to this page. </li>
  <li>Enter <strong>Client ID</strong> required for HTTPS request when authorizing user account. The client ID is a value created when <a href="/CEK/Guides/Link_User_Account.html#BuildAuthServer">building authorization server</a>.</li>
  <li>Enter a URL of the page with personal information policy of extension services on <strong>Personal information policy URL</strong>. This page will be exposed to the Clova extension store.</li>
  <li>Add a domain required from the <strong>Domain list field</strong> (if bringing resources for domains besides the domain with <strong>Login URL</strong> or <strong>Personal information policy URL</strong> pages).</li>
  <li>Add the predesignated scope on <strong>Scope</strong> field (if the scope of an access token issued by user account linking is predesignated).</li>
  <img src="/DevConsole/Resources/Images/DevConsole-Extension_Accoun_Linking_Settings_2.png" />
  <li>Enter URL which acquires a service access token on <strong>Access token URI</strong> field. As of now, the <strong>grant type supports the code grant method only.</li>
  <li>Enter <strong>Client secret</strong> required for HTTPS request to acquire the service access token. The client secret is a value created when <a href="/CEK/Guides/Link_User_Account.html#BuildAuthServer">building authorization server</a>.</li>
  <li><strong>Client verification schema</strong> configures a value that matches to the authorization server interface from the following.
    <ul>
      <li><strong>HTTP Basic (Recommended)</strong>: If entering the authorization credential to the header to acquire a service access token.</li>
      <li><strong>Credentials in request body</strong>: If entering the authorization credential to the body to acquire a service access token.</li>
    </ul>
  </li>
</ol>

<div id="RedirectURI" class="note">
  <p><strong>Note!</strong></p>
  <p>A URL (redirect URL) to be accessed for a client after the account authorization is <code>{{ book.RedirectURLforAccountLinking }}</code>. The URL can be verified from <strong>Redirect URL</strong> field.</strong></p>
  <img src="/DevConsole/Resources/Images/DevConsole-Redirect_URL_for_Extension_Accoun_Linking.png" />
</div>
