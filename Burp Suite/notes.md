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