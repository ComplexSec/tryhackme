#  TryHackMe - Burp Suite (Room 006)

<details><summary>Task 4.1 to 4.9 - Overview of Features</summary>
<p>

## Task 4.1

### Q: Which tool in Burp Suite can we use to perform a `diff` on responses and other pieces of data?

A: Comparer

## Task 4.2

### Q: What tool could we use to analyze randomness in different pieces of data such as password reset tokens?

A: Sequencer

## Task 4.3

### Q: Which tool can we use to set the scope of our project?

A: Target

## Task 4.4

### Q: While only available in the premium version, which tool can we use to automatically identify different vulnerabilities in the application we are examining?

A: Scanner

## Task 4.5

### Q: Encoding or decoding data can be particularly useful when examining URL parameters or protections on a form. Which tool allows us to do just that?

A: Decoder

## Task 4.6

### Q: Which tool allows us to redirect our web traffic into Burp for further examination?

A: Proxy

## Task 4.7

### Q: Simple in concept, but powerful in execution, which tool allows us to reissue requests?

A: Repeater

## Task 4.8

### Q: With four modes, which tool in Burp can we use for a variety of purposes such as field fuzzing?

A: Intruder

## Task 4.9

### Q: Which tool allows us to modify Burp Suite via the addition of extensions?

A: Extender

</p>
</details>

<details><summary>Task 6.1 to 6.9 - Proxy</summary>
<p>

## Task 6.1 - no answer needed

Deploy the VM

## Task 6.2

### Q: By default, the Burp proxy listens on only one interface. What is it?

A: 127.0.0.1:8080

## Task 6.3 - no answer needed

### Q: In Burp, navigate to the Intercept sub-tab of Proxy section and turn Intercept on

## Task 6.4

### Q: Return to the browser and navigate to the web app hosted on machine in the lab. Note that the page appears to be continuously loading. In Burp, we have a request that is waiting in our Intercept tab. 
### Take a look at the actions. Which shortcut allows us to forward the request to Repeater?

A: CTRL+R

Walkthrough: Right click inside Intercept tab and you will see various options

![](/Burp%20Suite/images/repeater.png)

## Task 6.5

### Q: How about if we wanted to forward our request to Intruder?

A: CTRL+I

Walkthrough: Right click inside Intercept tab and you will see various options

![](/Burp%20Suite/images/intruder.png)

## Task 6.6

### Q: Burp Suite saves the history of requests sent through the proxy along their varying details. Useful when we need to have proof of our actions in a pentest or we want to modify and resend a request sent before. 

### What is the name of the first section wherein general web requests (GET/POST) are saved?

A: HTTP History

Walkthrough: In the Proxy tab, the first option after the Intercept sub-tab is HTTP History. Looking through here, we see all general web requests sent via Proxy

![](/Burp%20Suite/images/http_history.png)

## Task 6.7

### Q: Defined in RFC 6455 as a low-latency communication protocol that does not require HTTP encapsulation, what is the name of the second section of our saved history in Burp Suite? These are commonly used in collaborate application which require real-time updates

A: WebSockets history

Walkthrough: In the Proxy tab, the second option after the Intercept sub-tab is WebSockets History. Looking through here, we see WebSockets requests sent via Proxy

![](/Burp%20Suite/images/websockets_history.png)

## Task 6.8

### Move over to the Options section of the Proxy tab and scroll down to `Intercept Client Requests`. Here, we can apply further fine-grained rules to define which requests we would like to intercept. Perhaps the most useful out of the default rules is our only AND rule. What is it's match type?

A: URL

Walkthrough: Going into the `Intercept Client Requests` options, we can see the `Match Type` field says URL for our AND rule

![](/Burp%20Suite/images/and_rule.png)

## Task 6.9

### Q: How about it's 'Relationship'? 

### In this situation, enabling this match rule can be incredibly useful following target definition as we can effectively leave intercept on permanently (unless we need to navigate without intercept) as it won't disturb sites which are outside of our scope - something which is particularly nice if we need to Google something in the same browser.

A: Is in target scope

Walkthrough: Going into the `Intercept Client Requests` options, we can see the `Relationship` field says Is in target scope for our AND rule 

![](/Burp%20Suite/images/relationship.png)

</p>
</details>

<details><summary>Task 7.1 to 7.8 - Target Definition</summary>
<p>

## Task 7.1 - no answer needed

### Before leaving the Proxy tab, switch Intercept off

## Task 7.2 - no answer needed

### Navigate to the Target tab in Burp. In the last task, we browsed to the website on our target machine. Find our target site in this list and right click on it. Select `Add to scope`

## Task 7.3 - no answer needed

### Clicking `Add to scope` will trigger a pop-up. This will stop Burp from sending out-of-scope items to our site map

## Task 7.4 - no answer needed

### Select `Yes` to close the popup

## Task 7.5

### Q: Browse around the rest of the application to build out our page structure in the target tab. Once you have visited most of the pages of the site, return to Burp Suite and expand the various levels of the application directory. What do we call this representation of the collective web application?

A: Site Map

![](/Burp%20Suite/images/sitemap.png)

## Task 7.6

### Q: What is the term for browsing the application as a normal user prior to examining it further?

A: Happy Path

## Task 7.7 - no answer needed

### Q: One last thing before moving on. Within the target tab, you may have noticed a sub-tab for issue definitions. Click into that now

## Task 7.8

### Q: The issue definitions found here are how Burp Suite defines issues within reporting. While getting started, these issue definitions can be particularly helpful for understanding and categorizing various findings we might have

### Which poisoning issue arises when an application behind a cache process input that is not included in the cache key?

A: Web Cache Poisoning

![](/Burp%20Suite/images/webcache_poisoning.png)