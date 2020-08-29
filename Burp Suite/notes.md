#  TryHackMe - Burp Suite (Room 006)

<details><summary>Introduction</summary>
<p>

## Introduction

Burp Suite is widely regarded as the de facto tool to use when performing web app testing

</p>
</details>

<details><summary>Installation</summary>
<p>

## Installation

Burp Suite is already installed in Kali Linux. If installing Burp from scratch, download from [here](https://portswigger.net/burp/communitydownload)

Burp Suite also requires [Java JRE](https://www.java.com/en/download/) to run successfully

</p>
</details>

<details><summary>Getting CA Certified</summary>
<p>

## Getting CA Certified

Before using Burp, installation of a CA certificate is necessary as Burp acts as a proxy between your browser and sending it through the internet - this allows it to read and send HTTPS data

Download it from `http:://localhost:8080` while Burp is running and import it into Firefox via the settings

![](/Burp%20Suite/images/ca_certificate.png)

</p>
</details>

<details><summary>Overview of Features</summary>
<p>

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

</p>
</details>

<details><summary>Dark Mode</summary>
<p>

## Dark Mode

To use Dark Mode in Burp Suite, navigate to `User options` --> `Display` -->  `Look and feel` and choose the __Darcula__ mode

![](/Burp%20Suite/images/darcula.png)

</p>
</details>

<details><summary>Proxy</summary>
<p>

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

</p>
</details>

<details><summary>Target Definition</summary>
<p>

## Target Definition

![](/Burp%20Suite/images/target_definition.png)

The `Target` tab in Burp allows us to define the scope, view a site map and specify issue definitions

When starting a web app test, you will be provided a few things:

* The application URL
* A list of the different user roles within the app
* Various test accounts and associated credentials for those accounts
* A list of pieces/forms in the app which are out-of-scope for testing

From this information, we can start to build our scope within Burp. Typically done in a tiered approach wherein we work our way up from the lowest privileged account, browsing the site as a normal user would

Browsing normally to discover the full extent of the site is commonly referred to as the __happy path__

Following the creation of a site map, we can go through and start removing various items from the scope. These items typically fit one of these criteria:

* The item (page, form, etc) has been designated as out of scope
* Automated exploitation of the item would cause a huge mess
* Automated exploitation of the item would lead to damaging and potentially crashing the web app

</p>
</details>

<details><summary>Putting it on Repeat[er]</summary>
<p>

## Putting it on Repeat[er]

Repeater allows us to repeat requests. These requests can be re-issued as-is or with modifications. In contrast to Intruder, Repeater is typically used for the purposes of experimentation or more fine-tuned exploitation

![](/Burp%20Suite/images/repeater_header.png)

For more information on Repeater, click [here](https://portswigger.net/burp/documentation/desktop/tools/repeater)

</p>
</details>

<details><summary>Intruder</summary>
<p>

## Intruder

Intruder can be used from fuzzing to brute forcing. At its core, Intruder serves one purpose: automation

It is meant for repeat testing once a POC has been established

Some common uses are:

* Enunemerating identifiers such as usernames, cycling through predictable session/password recovery tokens, and attempting simple password guessing
* Harvesting useful data from user profiles or other pages of interest via grepping our responses
* Fuzzing for vulnerabilities such as SQL injection, XSS and file path traversal

![](/Burp%20Suite/images/intruder_header.png)

Intruder has [four](https://portswigger.net/burp/documentation/desktop/tools/intruder/positions) different attack types:

1. Sniper - the most popular attack type. Cycles through selected positions, putting the next available payload in each position in turn. Uses only one set of payloads
2. Battering ram - uses only one set of payloads. Puts every payload into every selected position
3. Pitchfork - allows us to use multiple payload sets and iterate through both payload sets simultaneously. If we selected two positions, we can provide a username and password payload list for example
4. Cluster Bomb - allows us to use multiple payload sets and iterate through all combinations of the payload lists we provide. If we selected two positions, we can provide a username and password payload list. Intruder then cycles through the combinations resulting in a total number of combinations equalling usernames * passwords

</p>
</details>

<details><summary>Sequencer</summary>
<p>

## Sequencer

![](/Burp%20Suite/images/sequencer.png)

Sequencer is a tool for analyzing the quality of randomness in an application's session tokens and other important data items that are otherwise intended to be unpredictable

Commonly analyzed items include:

* Session tokens
* Anti-CSRF (Cross-Site Request Forgery) Tokens
* Password reset tokens (sent with password resets that in theory uniquely tie user with their password reset requests)

For more information, check out Burp Suite [documentation](https://portswigger.net/burp/documentation/desktop/tools/sequencer)

</p>
</details>

<details><summary>Decoder and Comparer</summary>
<p>

## Decoder & Comparer

![](/Burp%20Suite/images/decoder.png)

Decoder is a tool that allows us to perform various transforms on pieces of data varying from decoding/encoding to various bases or URL encoding. We chain these transforms together and Decoder will automatically spawn an additional tier each time we select a decoder, encoder, or hash

Comparer is a tool used to compare different responses or other pieces of data such as site maps or proxy histories. Very similiar to the Linux tool `diff`

* When looking for username enumeration conditions, you can compare responses to failed logins using valid and invalid usernames, looking for subtle differences in responses
* When an Intruder attack has resulted in some very large responses with different lengths than the base response, you can compare these to quickly see where the differences lie
* When comparing the site maps or Proxy history entries generated by different types of users, you can compare pairs of similiar requests to see where the differences lie that give rise to different application behaviour. This may reveal possible access control issues in the application wherein lower privileged users can access pages they really shouldn't be able to
* When testing for blind SQL injection bugs using Boolean condition injection and other simiiar tests, you can compare two responses to see whether injecting different conditions has results in a relevant difference in responses

</p>
</details>

<details><summary>Installing Extensions</summary>
<p>

## Extender

![](/Burp%20Suite/images/extensions.png)

Extender allows us to add components such as tool integrations, additional scan definitions, and more. Some of the most popular extensions are:

* Logger++ - adds enhanced logging to all requests and responses from all Burp Suite tools
* Request Smuggler - allows you to attempt to smuggle requests to backend servers
* Autorize - useful for authentication testing in web app tests. These tests typically revolve around navigating to restricted pages or issuing restricted GET requests with the session cookies of low privileged users
* Burp Teams Server - allows for collaboration on a Burp project amongst team member. Project detials are shared in a chatroom-like format
* Retire.js - adds scanner checks for outdated JavaScript libraries that contain vulnerabilities
* J2EEScan - adds scanner test coverage for J2EE (Java platform for web developemnt) applications
* Request Timer - captures response times for requests made by all Burp tools: useful for discovering timing attack vectors

A pre-requisite for many extensions is Jython: the Java implementation of Python

![](/Burp%20Suite/images/jython.png)

For more information, check Burp Suite [documentation](https://portswigger.net/burp/documentation/desktop/tools/extender) on Extender or check out the [article](https://portswigger.net/testers/penetration-testing-tools) on some of the top extensions for Burp Suite

<details><summary>Burp Suite Pro Features</summary>
<p>

## Burp Suite Pro Features

![](/Burp%20Suite/images/pro.png)

The Burp Suite Scanner allows us to passively and actively scan and spider the website we are testing for vulnerabilities. In Burp 2.0's task-based model, we can launch these scans (Scanner and Spider) from the dashboard and let them run in the background while we continue to examine the web app

![](/Burp%20Suite/images/scanner.png)

Commonly used in manual tests, Burp Collaborator Client allows us to gain insight into issues that may otherwise seem to produce no output

Often during testing, we may come across items which - either due to timing/slowness or a lack of any reaction - are likely vulnerable but do not produce any sure-fire indicators. With Burp Collaborator, we can produce out-of-band alerts via generating payloads that reach back to Burp Suite's servers for us

For more information, check out the documentation for [Scanner](https://portswigger.net/burp/documentation/scanner) and [Collaborate Client](https://portswigger.net/burp/documentation/desktop/tools/collaborator-client)

</p>
</details>