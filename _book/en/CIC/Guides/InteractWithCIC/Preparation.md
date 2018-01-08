## Preparation {#Preparation}
Integrating your client and CIC requires you to connect the two over the HTTP/2 protocol. To make the connection, prepare the following:

* [Libraries](#RequiredLibrary) for HTTP/2 protocol connection
* [User-Agent string](#UserAgentString) for client
* [Client credentials](#ClientAuthInfo) for creating Clova access tokens


### Required library {#RequiredLibrary}

To support communication over the HTTP/2 protocol, you need to import the libraries that support the HTTP/2 protocol. We recommend you to use the following libraries.

| Programming language | Library               |
|---------|------------------------------------|
| C/C++   | [nghttp2](https://nghttp2.org/), [libcurl](https://curl.haxx.se/libcurl/) |
| Java    | [OkHttp](http://square.github.io/okhttp/), [Netty](http://netty.io/), [Jetty](http://www.eclipse.org/jetty/) |


### User-Agent string {#UserAgentString}

Add a user-agent string in the HTTP header when using Clova or Clova related Web services. Clients make HTTP connections for the following tasks, and the User-Agent string is required in all the tasks.

* [Communicating with the CIC server](#ConnectToCIC)
* Opening a page in a Webview on an app
* Downloading images required for a UI
* Requesting audio stream for a media player

<div class="danger">
  <p><strong>Caution!</strong></p>
  <p>If you miss out a user-agent string in an HTTP header, or if your user-agent string is not written according to the notation, your request or connection attempt may be rejected.
.</p>
</div>

Define your user-agent string based on the following [Backus-Naur form(BNF)](https://en.wikipedia.org/wiki/Backus%E2%80%93Naur_form).

```
letter     = "A" | "B" | "C" | "D" | "E" | "F" | "G" | "H" | "I" | "J" | "K" | "L" | "M"
           | "N" | "O" | "P" | "Q" | "R" | "S" | "T" | "U" | "V" | "W" | "X" | "Y" | "Z"
           | "a" | "b" | "c" | "d" | "e" | "f" | "g" | "h" | "i" | "j" | "k" | "l" | "m"
           | "n" | "o" | "p" | "q" | "r" | "s" | "t" | "u" | "v" | "w" | "x" | "y" | "z" ;
digit      = "0" | "1" | "2" | "3" | "4" | "5" | "6" | "7" | "8" | "9" ;
whitespace = " " ;
number     = digit , { digit } ;
character  = letter | digit | "_" | "-" | "." ;
word       = character , { character } ;
string     = word
           | word , { whitespace | word } , word ;
safe_char  = letter | digit | "_" ;
safe_word  = safe_char , { safe_char } ;

urlencoded_character = character | "%" ;
urlencoded_string    = urlencoded_character , { urlencoded_character } ;

slash               = "/" ;
slash_delimiter     = [ whitespace ] , slash , [ whitespace ] ;
semicolon           = ";" ;
semicolon_delimiter = [ whitespace ] , semicolon , [ whitespace ] ;

build      = safe_word
           | safe_word , "." , build ;
release    = safe_word
           | safe_word , "." , release ;
version    = number , "." , number , "." , "number"
           | number , "." , number , "." , "number" , "-" , release
           | number , "." , number , "." , "number" , "+" , build
           | number , "." , number , "." , "number" , "-" , release , "+" , build ;

Manufacturer_Identifier = string ;
Product_Identifier      = string ;
Firmware_Version        = version ;
OS_Information          = string ;
HW_Information          = string ;
property                = word , "=" , urlencoded_string ;
extra_information       = property , { semicolon_delimiter , property } ;

User_Agent = Manufacturer_Identifier , slash_delimiter ,
             Product_Identifier , slash_delimiter ,
             Firmware_Version ,
             [ whitespace ] , "(" ,
             OS_Information , semicolon_delimiter ,
             HW_Information ,
             [ semicolon_delimiter , extra_informations ] , ")" ;
```

The following is an example of a user-agent string written according to BNF. **For your information, you MUST follow [Semantic Versioning](https://semver.org/) for specifying the `Firmware_Version`**

```
MyCompanyName/MyProductName/1.0.1 (KindOfOS 0.9;CustomHardwareInfo;sampleKey1=sampleValue1;sampleKey2=sampleValue2)
MyOrganizationName/MyAppName/2.1.2-release (Android 7.0;SettopBox;target=KR;other=sample)
AbbreviationOfCompanyName/MyClient/0.8.2+build (Linux 7.0;Raspberry_pi;domain=Sample%40Clova;type=Test%20Type)
MCN/SampleClient/1.7.0 (SampleIoTOS 2.1;SmartHub)
```

<div class="danger">
  <p><strong>Note!</strong></p>
  <p>The user-agent string needs to be registered on the Clova developer console. Until the Clova developer console for CIC becomes available, contact your Clova representative to add the user-agent string.</p>
</div>

### Client credentials {#ClientAuthInfo}

To use a Clova service, users must authenticate their {{ book.TargetServiceForClientAuth }} account on the client and also [obtain a Clova access token](#CreateClovaAccessToken) for their account.
To obtain a Clova access token, you need to send the user's {{ book.TargetServiceForClientAuth }} access token obtained from user authentication, _and_  client credentials over to the Clova authorization server.
Client credentials can be obtained from the Clova Developer Console (using [Clova Auth API](/CIC/References/Clova_Auth_API.md)). Have the client credentials from the Clova Developer Console ready in advance. Client credentials provide following information.

| Credentials                   | Description                                              |
|---------------------------|--------------------------------------------------|
| `CLOVA_OAUTH_CLIENT_ID`     | The client ID registered on the Clova Developer Console         |
| `CLOVA_OAUTH_CLIENT_SECRET` | The client secret obtained from the Clova Developer Console |

<div class="note">
  <p><strong>Note!</strong></p>
  <p>The Clova Developer Console for CIC is currently under development. Contact your Clova representative personnel to ask for help with obtaining client credentials.</p>
</div>
