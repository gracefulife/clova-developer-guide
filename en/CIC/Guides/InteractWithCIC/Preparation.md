## Preparation {#Preparation}
Make your client connect with CIC using the HTTP/2 protocol. Before trying to connect with CIC, prepare the following.

* [Libraries](#RequiredLibrary) for HTTP/2 protocol connection
* [Client credentials](#ClientAuthInfo) necessary for creation of Clova access tokens


### Required library {#RequiredLibrary}
To enable communications over the HTTP/2 protocol, use the libraries recommended below.

| Programming language | Library  |
|---------|------------------------------------|
| C/C++  | [nghttp2](https://nghttp2.org/), [libcurl](https://curl.haxx.se/libcurl/) |
| Java  | [OkHttp](http://square.github.io/okhttp/), [Netty](http://netty.io/), [Jetty](http://www.eclipse.org/jetty/) |


### Client credentials {#ClientAuthInfo}
To use any services provided by Clova, users must authenticate their {{ book.TargetServiceForClientAuth }} account on your client. Using the {{ book.TargetServiceForClientAuth }} account information entered by a user, you can obtain an access token for the user's {{ book.TargetServiceForClientAuth }} account. Then, you send the token to the Clova authorization server and proceed to [creating Clova access tokens](#CreateClovaAccessToken).

When sending the {{ book.TargetServiceForClientAuth }} account access token to the authorization server, make sure to send client credentials as well, which you have obtained from the Clova Developer Console (using [Clova Auth API](/CIC/References/Clova_Auth_API.md)). Get client credentials from the Clova Developer Console and have them ready in advance. Client credentials provide following information.

| Credentials  | Description  |
|---------------------------|--------------------------------------------------|
| `CLOVA_OAUTH_CLIENT_ID`  | The client ID registered at the Clova Developer Console  |
| `CLOVA_OAUTH_CLIENT_SECRET` | The client authentication key obtained from the Clova Developer Console |

<div class="note">
  <p><strong>Note!</strong></p>
  <p>The Clova Developer Console is currently under development. Contact your counterpart contact personnel to ask for help with obtaining client credentials.</p>
</div>