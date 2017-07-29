## Preparation {#Preparation}
To connect your client with CIC using the HTTP/2 protocol, prepare the following.

* [Libraries](#RequiredLibrary) for HTTP/2 protocol connection
* [Client credentials](#ClientAuthInfo) necessary for Clova access token creation


### Required library {#RequiredLibrary}
You are recommended to use the following libraries when developing the client part to enable communications over the HTTP/2 protocol connection.

| Programming language | Library                            |
|---------|------------------------------------|
| C/C++   | [nghttp2](https://nghttp2.org/), [libcurl](https://curl.haxx.se/libcurl/) |
| Java    | [OkHttp](http://square.github.io/okhttp/), [Netty](http://netty.io/), [Jetty](http://www.eclipse.org/jetty/) |


### Client credentials {#ClientAuthInfo}
To use any services provided by Clova, a user must authenticate his or her {{ book.ko.TargetServiceForClientAuth }} account on your client. Using the {{ book.ko.TargetServiceForClientAuth }} account information provided from the user, your client obtains an access token for the {{ book.ko.TargetServiceForClientAuth }} account. The token is in turn sent to a Clova authorization server, then the server issues a Clova access token (See [Creating Clova access token](#CreateClovaAccessToken)).

When sending a {{ book.ko.TargetServiceForClientAuth }} account access token to an authorization server, you must send client credentials as well, which you've obtained in Clova Developer Console (using [Clova Auth API](/CIC/References/Clova_Auth_API.md)). Therefore, you must obtain client credentials in Clova Developer Console and have them ready in advance. Client credentials include the following.

| Credentials                   | Description                                              |
|---------------------------|--------------------------------------------------|
| CLOVA_OAUTH_CLIENT_ID     | The client ID registered in Clova Developer Console        |
| CLOVA_OAUTH_CLIENT_SECRET | The client authentication key obtained in Clova Developer Console |

<div class="note">
  <p><strong>Note!</strong></p>
  <p>Clova Developer Console is still under development. Contact your counterpart contact personnel to ask for help with obtaining client credentials.</p>
</div>