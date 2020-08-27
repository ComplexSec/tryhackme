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

## Content

Content of web page is normally a combination of HTML, CSS & JavaScript.

* `HTML` defines the structure of the page and the content
* `CSS` changes how the page looks
* `JavaScript` makes pages interactive & loads extra content