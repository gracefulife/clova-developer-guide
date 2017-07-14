## Preparation {#Preparation}
Your client should connect with CIC using the HTTP/2 protocol. To do so, you need to prepare the following.

* [Libraries](#RequiredLibrary) for HTTP/2 protocol connection
* [Client credentials](#ClientAuthInfo) for creation of a Clova access token


### Required library {#RequiredLibrary}
You are recommended to use the following libraries for client development to allow communications over the HTTP/2 protocol connection.

| Programming language | Library  |
|---------|------------------------------------|
| C/C++  | [nghttp2](https://nghttp2.org/), [libcurl](https://curl.haxx.se/libcurl/) |
| Java  | [OkHttp](http://square.github.io/okhttp/), [Netty](http://netty.io/), [Jetty](http://www.eclipse.org/jetty/) |


### Client credentials {#ClientAuthInfo}
To use any services provided by Clova, the user must authenticate his or her {{ book.TargetServiceForClientAuth }} account in your client. With the {{ book.TargetServiceForClientAuth }} account information provided by the user, your client can obtain an access token for the {{ book.TargetServiceForClientAuth }} account. Following that, the token is delivered to the Clova authorization server, from where a Clova access token is issued (See [Creating Clova access token](#CreateClovaAccessToken)).

When the {{ book.TargetServiceForClientAuth }} account access token is sent to the authorization server, client credentials obtained in the Clova Developer Console should be provided together (use [Clova Auth API](/CIC/References/Clova_Auth_API.md)). As such, make sure to obtain client credentials in the Clova Developer Console and have it ready in advance. Client credentials include the following.

| Credentials  | Description  |
|---------------------------|--------------------------------------------------|
| CLOVA_OAUTH_CLIENT_ID  | The client ID registered in the Clova Developer Console  |
| CLOVA_OAUTH_CLIENT_SECRET | The client authentication key obtained in the Clova Developer Console |

<div class="note">
  <p><strong>Note!</strong></p>
  <p>Clova Developer Console is still under development. Please contact your counterpart contact personnel to ask for help with obtaining client credentials.</p>
</div>
