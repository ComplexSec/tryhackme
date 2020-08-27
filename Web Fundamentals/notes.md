#  TryHackMe - Web Fundamentals (Room 005)

## How Do We Load Websites?

Initially, a DNS request is made. DNS takes a URL and turns it into an IP address

The IP address uniquely identifies each internet connected device. IP addresses are formed of 4 groups of numbers, each 0-255 and called an __octet__

### Loading Content

Once the browser knows the server's IP address, it asks the server for the web page. This is done via an __HTTP GET__ request

__GET__ is an example of an HTTP verb which are different types of requests

The server responds to __GET__ requests with the web page content. If the web page is loading extra resources like JavaScript, images, or CSS files, those are retrieved in __separate GET requests__

