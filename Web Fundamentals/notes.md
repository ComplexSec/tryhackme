#  TryHackMe - Web Fundamentals (Room 005)

## How Do We Load Websites?

Initially, a DNS request is made. DNS takes a URL and turns it into an IP address

The IP address uniquely identifies each internet connected device. IP addresses are formed of 4 groups of numbers, each 0-255 and called an __octet__

### Loading Content

Once the browser knows the server's IP address, it asks the server for the web page. This is done via an __HTTP GET__ request

__GET__ is an example of an HTTP verb which are different types of requests

The server responds to __GET__ requests with the web page content. If the web page is loading extra resources like JavaScript, images, or CSS files, those are retrieved in __separate GET requests__

### Wireshark Showing the HTTP requests that load a website

![](/Web%20Fundamentals/images/wireshark.png)

For most websites, the requests will use HTTPS. HTTPS is an encrypted version of HTTP. It uses TLS 1.3

### Web Server

A webserver is software that receives and responds to HTTP(S) requests. Examples are Apache, Nginx, and Microsoft IIS

### HTTP

HTTP runs on port 80 and HTTPS runs on port 443

### Content

Content of web page is normally a combination of HTML, CSS & JavaScript.

* `HTML` defines the structure of the page and the content
* `CSS` changes how the page looks
* `JavaScript` makes pages interactive & loads extra content

## More HTTP - Verbs and Request Formats

There are 9 different HTTP "verbs" - also known as __methods__

Two main ones used in web servers:

* GET - used to retrieve content
* POST - used to send data like commenting or logging in

### HTTP Request Broken Down

First line is a verb and path for the server

* `GET /index.html`

Next section is headers which give web server more information about the request. Cookies are sent in __request headers__

Finally, the body of the request. 

* For __POST__ requests, this is the content that is sent to the server
* For __GET__ requests, a body is allowed but will mostly be ignored

Example of GET request retrieving a JS file:

`GET /main.js HTTP/1.1`

`Host: 192.168.170.129:8081`

`Connection: keep-alive`

`User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 
(KHTML, like Gecko) Chrome/80.0.3987.122 Safari/537.36`

`Accept: */*`

`Referer: http://192.168.170.129:8081/`

`Accept-Encoding: gzip, deflate`

`Accept-Language: en-GB,en-US;q=0.9,en;q=0.8`

### Responses

Server replies with a response. Responses follow a similiar structure to the request

First line describes the status rather than a verb & path. Status normally a code like 404

Basic breakdown of status codes or [click here](https://developer.mozilla.org/en-US/docs/Web/HTTP/Status):

* 100-199: Information
* 200-299: Successes (200 OK is the "normal" response for a GET)
* 300-399: Redirects (information you want is elsewhere)
* 400-499: Client errors (user did something wrong)
* 500-599: Server errors (server tried & something went wrong)

