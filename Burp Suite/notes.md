#  TryHackMe - Burp Suite (Room 006)

## Introduction

Burp Suite is widely regarded as the de facto tool to use when performing web app testing

## Installation

Burp Suite is already installed in Kali Linux. If installing Burp from scratch, download from [here](https://portswigger.net/burp/communitydownload)

Burp Suite also requires [Java JRE](https://www.java.com/en/download/) to run successfully

## Getting CA Certified

Before using Burp, installation of a CA certificate is necessary as Burp acts as a proxy between your browser and sending it through the internet - this allows it to read and send HTTPS data

Download it from `http:://localhost:8080` while Burp is running and import it into Firefox via the settings

![](/Burp%20Suite/images/ca_certificate.png)

## Overview of Features

Quick overview of each section:

* __Proxy__ - allows us to funnel traffic through Burp for further analysis
* __Target__ - how we set the scope of the project. Also used to effectively create a site map of the app
* __Intruder__ - powerful tool for everything from field fuzzing to credential stuffing and more
* __Repeater__ - allows us to repeat requests with or without modification.  Often used as a precursor to fuzzing with Intruder
* __Sequencer__ - analyzes the "randomness" present in parts of the app which are intended to be unpredictable. Commonly used for testing session cookies
* __Decoder__ - tool that allows us to perform various transforms on pieces of data. These transforms vary from decoding/encoding to various bases or URL encoding
* __Comparer__ - tool used to compare different responses or other pieces of data like site maps or proxy histories. Similiar to `diff` tool in Linux
* __Extender__ - allows us to add components such as tool integration, additional scan definitions and more
* __Scanner__ - automated web vulnerability scanner that can highlight areas of the app for further investigation. Not in community edition of Burp

## Dark Mode

To use Dark Mode in Burp Suite, navigate to `User options` --> `Display` -->  `Look and feel` and choose the __Darcula__ mode

![](/Burp%20Suite/images/darcula.png)

## Proxy

Proxy servers by definition allow us to relay our traffic through an alternative route to the internet. Done for educational filtering to accessing content region locked

Using a proxy for web pentesting allows us to view and modify traffic inline at a granular level

![](/Burp%20Suite/images/proxy.png)

By default Burp will be set to 'intercept' traffic:

* Requests will by default require our authorization to be sent
* We can modify our requests in-line similiar to what you might see in a MitM attack and then send them on
* Can drop requests as well. Useful to see the request attempt after clicking a button or performing another action
* Can send requests to other tools like Repeater or Intruder for modification and manipulation to induce vulnerabilities

For more information about proxies, read [here](https://portswigger.net/burp/documentation/desktop/tools/proxy)

