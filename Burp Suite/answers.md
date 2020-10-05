#  TryHackMe - Burp Suite (Room 006)

Please try and answer all questions before looking at the answers to test your knowledge :)

<details><summary>Task 4.1 to 4.9 - Overview of Features</summary>
<p>

## Task 4.1

### Q: Which tool in Burp Suite can we use to perform a `diff` on responses and other pieces of data?

<details><summary>Answer</summary>
<p>

__Comparer__	

</p>
</details>


## Task 4.2

### Q: What tool could we use to analyze randomness in different pieces of data such as password reset tokens?

<details><summary>Answer</summary>
<p>
	
Sequencer

</p>
</details>

## Task 4.3

### Q: Which tool can we use to set the scope of our project?

<details><summary>Answer</summary>
<p>
	
Target

</p>
</details>

## Task 4.4

### Q: While only available in the premium version, which tool can we use to automatically identify different vulnerabilities in the application we are examining?

<details><summary>Answer</summary>
<p>
	
Scanner

</p>
</details>

## Task 4.5

### Q: Encoding or decoding data can be particularly useful when examining URL parameters or protections on a form. Which tool allows us to do just that?

<details><summary>Decoder</summary>
<p>
	
Decoder

</p>
</details>

## Task 4.6

### Q: Which tool allows us to redirect our web traffic into Burp for further examination?

<details><summary>Answer</summary>
<p>
	
Proxy

</p>
</details>

## Task 4.7

### Q: Simple in concept, but powerful in execution, which tool allows us to reissue requests?

<details><summary>Answer</summary>
<p>
	
Repeater

</p>
</details>

## Task 4.8

### Q: With four modes, which tool in Burp can we use for a variety of purposes such as field fuzzing?

<details><summary>Answer</summary>
<p>
	
Intruder

</p>
</details>

## Task 4.9

### Q: Which tool allows us to modify Burp Suite via the addition of extensions?

<details><summary>Answer</summary>
<p>
	
Extender

</p>
</details>

</p>
</details>

<details><summary>Task 6.1 to 6.9 - Proxy</summary>
<p>

## Task 6.1 - no answer needed

Deploy the VM

## Task 6.2

### Q: By default, the Burp proxy listens on only one interface. What is it?

<details><summary>Answer</summary>
<p>
	
127.0.0.1:8080

</p>
</details>

## Task 6.3 - no answer needed

### Q: In Burp, navigate to the Intercept sub-tab of Proxy section and turn Intercept on

## Task 6.4

### Q: Return to the browser and navigate to the web app hosted on machine in the lab. Note that the page appears to be continuously loading. In Burp, we have a request that is waiting in our Intercept tab. 
### Take a look at the actions. Which shortcut allows us to forward the request to Repeater?

<details><summary>Answer</summary>
<p>
	
CTRL+R

</p>
</details>

<details><summary>Walkthrough</summary>
<p>

Walkthrough: Right click inside Intercept tab and you will see various options

![](/Burp%20Suite/images/repeater.png)

</p>
</details>

## Task 6.5

### Q: How about if we wanted to forward our request to Intruder?

<details><summary>Answer</summary>
<p>
	
CTRL+I

</p>
</details>

<details><summary>Walkthrough</summary>
<p>

Walkthrough: Right click inside Intercept tab and you will see various options

![](/Burp%20Suite/images/intruder.png)

</p>
</details>

## Task 6.6

### Q: Burp Suite saves the history of requests sent through the proxy along their varying details. Useful when we need to have proof of our actions in a pentest or we want to modify and resend a request sent before. 

### What is the name of the first section wherein general web requests (GET/POST) are saved?

<details><summary>Answer</summary>
<p>
	
HTTP History

</p>
</details>

<details><summary>Walkthrough</summary>
<p>
	
Walkthrough: In the Proxy tab, the first option after the Intercept sub-tab is HTTP History. Looking through here, we see all general web requests sent via Proxy

![](/Burp%20Suite/images/http_history.png)

</p>
</details>

## Task 6.7

### Q: Defined in RFC 6455 as a low-latency communication protocol that does not require HTTP encapsulation, what is the name of the second section of our saved history in Burp Suite? These are commonly used in collaborate application which require real-time updates

<details><summary>Answer</summary>
<p>
	
WebSockets history

</p>
</details>

<details><summary>Walkthrough</summary>
<p>
	

Walkthrough: In the Proxy tab, the second option after the Intercept sub-tab is WebSockets History. Looking through here, we see WebSockets requests sent via Proxy

![](/Burp%20Suite/images/websockets_history.png)

</p>
</details>

## Task 6.8

### Move over to the Options section of the Proxy tab and scroll down to `Intercept Client Requests`. Here, we can apply further fine-grained rules to define which requests we would like to intercept. Perhaps the most useful out of the default rules is our only AND rule. What is it's match type?

<details><summary>Answer</summary>
<p>
	
URL

</p>
</details>

<details><summary>Walkthrough</summary>
<p>

Walkthrough: Going into the `Intercept Client Requests` options, we can see the `Match Type` field says URL for our AND rule

![](/Burp%20Suite/images/and_rule.png)

</p>
</details>

## Task 6.9

### Q: How about it's 'Relationship'? 

### In this situation, enabling this match rule can be incredibly useful following target definition as we can effectively leave intercept on permanently (unless we need to navigate without intercept) as it won't disturb sites which are outside of our scope - something which is particularly nice if we need to Google something in the same browser.

<details><summary>Answer</summary>
<p>
	
Is in target scope

</p>
</details>

<details><summary>Walkthrough</summary>
<p>

Walkthrough: Going into the `Intercept Client Requests` options, we can see the `Relationship` field says Is in target scope for our AND rule 

![](/Burp%20Suite/images/relationship.png)

</p>
</details>

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

<details><summary>Answer</summary>
<p>
	
Site Map

![](/Burp%20Suite/images/sitemap.png)

</p>
</details>

## Task 7.6

### Q: What is the term for browsing the application as a normal user prior to examining it further?

<details><summary>Answer</summary>
<p>
	
Happy Path

</p>
</details>

## Task 7.7 - no answer needed

### Q: One last thing before moving on. Within the target tab, you may have noticed a sub-tab for issue definitions. Click into that now

## Task 7.8

### Q: The issue definitions found here are how Burp Suite defines issues within reporting. While getting started, these issue definitions can be particularly helpful for understanding and categorizing various findings we might have

### Which poisoning issue arises when an application behind a cache process input that is not included in the cache key?

<details><summary>Answer</summary>
<p>
	
Web Cache Poisoning

![](/Burp%20Suite/images/webcache_poisoning.png)

</p>
</details>

</p>
</details>

<details><summary>Task 8.1 to 8.9 - Putting it on Repeat[er]</summary>
<p>

## Task 8.1 - no answer needed

To start, click `Account` or `Login` in the top right corner to navigate to the login page

## Task 8.2

### Q: Try logging in with invalid credentials. What error is generated when login fails?

A: Invalid email or password

![](/Burp%20Suite/images/invalid_creds.png)

## Task 8.3 - no answer needed

### Q: Even though we did not send it to Repeater initially, we can still find the request in our history. Switch over to the HTTP sub-tab of Proxy, look through the requests to find it, right click and send it to Repeater and Intruder

## Task 8.4

### Q: Now that is it in Repeater, let's try adjusting the request such that we are sending a single quote (') as both the email and password. What error is generated from this request?

A: SQLITE_ERROR

Walkthrough: Replace the `email` and `password` content with a single quote in Repeater and send it

![](/Burp%20Suite/images/sqlite_error.png)

## Task 8.5 & 8.6 - no answer needed

Now that we leveraged Repeater to gain POC that Juice Shop's login is vulnerable to SQLi, let's try something a little more mischievous and attempt to leave a devastating zero-star review

First, click on the `Contact Us` tab and then `Customer Feedback`

## Task 8.7 - no answer needed

With the Burp proxy turned on, submit feedback. Once this is done, find the POST request in your HTTP History and send it to Repeater

![](/Burp%20Suite/images/website_sucks.png)

## Task 8.8 

### Q: What field do we have to modify in order to submit a zero-star review?

A: rating

Walkthrough: The `rating` field indicates how many stars are posted in the review

## Task 8.9

Submit a zero star review and complete the challenge

![](/Burp%20Suite/images/zerostar.png)

</p>
</details>

<details><summary>Task 9.1 to 9.12 - Intruder</summary>
<p>

## Task 9.1

### Q: Which attack type allows us to select multiple payload sets (one per position) and iterate through them simulatenously?

A: Pitchfork

## Task 9.2

### Q: How about the attack type which allows us to use one payload set in every single position we have selected simultaneously?

A: Battering ram

## Task 9.3

### Q: Which attack type allows us to select multiple payload sets (one per position) and iterate through all possible combinations?

A: Cluster Bomb

## Task 9.4

### Q: Perhaps the most commonly used, which attack type allows us to cycle through our payload set, putting the next available payload in each position in turn?

A: Sniper

## Task 9.5 - no answer needed

### Download the wordlist attached to this room, this is a shortened version of the [fuzzbd SQLi platform detection list](https://github.com/fuzzdb-project/fuzzdb/blob/master/attack/sql-injection/detect/xplatform.txt)

## Task 9.6 - no answer needed

### Return to the Intruder in Burp. Open up the Positions sub-tab and verify that `Sniper` is selected as our attack type

## Task 9.7 - no answer needed

### Burp attempts to automatically highlight possible fields of interest for Intruder, however, it does not have it correct. Hit `Clear` on the right hand side to clear all selected fields

## Task 9.8 - no answer needed

### Highlight the email field between the double quotes (")

## Task 9.9 - no answer needed

### Click `Add` to select the email field as a position for our payloads

![](/Burp%20Suite/images/email.png)

## Task 9.10 - no answer needed

### Switch to the payloads sub-tab of Intruder. Once there, hit `Load` and select the wordlist you previously downloaded

![](/Burp%20Suite/images/payload.png)

## Task 9.11 - no answer needed

### Scroll down and uncheck `URL-encode these characters`. We do not want to have the characters sent to be encoded as they otherwise won't be recognized by SQL

![](/Burp%20Suite/images/urlencode.png)

## Task 9.12

### Finally, click `Start attack`. What is the first payload that returns a 200 status code, showing that we have successfully bypassed authentication?

A: a' OR 1=1--

Walkthrough: Look through the results and check the status codes

![](/Burp%20Suite/images/200OK.png)

</p>
</details>

<details><summary>Task 10.1 to 10.7 - Sequencer</summary>
<p>

## Task 10.1 - no answer needed

### Switch over to the HTTP History sub-tab of Proxy

## Task 10.2 - no answer needed

### We are going to dig for a response which issues a cookie. Parse through the various responses we have received from Juice Shop until you find one that includes a `Set-Cookie` header

![](/Burp%20Suite/images/setcookie.png)

## Task 10.3 - no answer needed

### Once a request is found, right-click on it and `Send to Sequencer`

## Task 10.4 - no answer needed

### Change over to Sequencer and select `Start live capture`

## Task 10.5 - no answer needed

### Let Sequencer run and collect 10,000 requests. Once it hits that amount, hit  `Pause` and then `Analyze now`

## Task 10.6 

### Parse through the results. What is the effective estimated entrop measured in?

A: bits

Walkthrough: Learnt through the summary tab under `Overall result`

![](/Burp%20Suite/images/bits.png)

## Task 10.7

### In order to find the usable bits of entropy, we often have to make some adjustments to have a normalized dataset. What item is converted in this process?

A: token

Walkthrough: Learnt through the `Bit level analysis` and `Bit conversion` section

![](/Burp%20Suite/images/token.png)

</p>
</details>

<details><summary>Task 11.1 to 11.6 - Decoder & Comparer</summary>
<p>

## Task 11.1 - no answer needed

Return to the Target tab and find the API endpoint highlighted in the following request

![](/Burp%20Suite/images/scoreboard.png)

## Task 11.2 - no answer needed

Copy the first line of that request and paste it into Decoder then select `Decode as URL`

## Task 11.3

### Q: What character does the %20 in the request we copied into Decoder come out as?

A: Space

Walkthrough: There is a space between Score and Board

![](/Burp%20Suite/images/space.png)

## Task 11.4

### Q: Similiar to CyberChef, Decoder also has a `Magic` mode where it will automatically attempt to decode the input it is provided. What is this mode called?

A: Smart Decode

Walkthrough: Look through the options to Decode as

![](/Burp%20Suite/images/smartdecode.png)

## TAsk 11.5 

### Q: What can we load into Comparer to see differences in what various user roles can access? This is very useful to check for access control issues

A: Site maps

## Task 11.6 

### Q: Comparer can perform a diff against two different metrics, which one allows us to examine the data loaded in as-is rather than breaking it down into bytes?

A: Words

Walkthrough: Located at the bottom right of Comparer tab

![](/Burp%20Suite/images/words.png)

</p>
</details>

<details><summary>Task 12.1 to 12.6 - Extensions</summary>
<p>

## Task 12.1 - no answer needed

### Switch over to the Options sub-tab of the Extender tab

## Task 12.2 - no answer needed

### Scroll down until you reach the `Python Environment` section. Burp requires the standalone edition of Jython

## Task 12.3 - no answer needed

### Download the standalone version of Jython from [here](https://www.jython.org/download.html)

## Task 12.4 - no answer needed

### Return to Burp and hit `Select file` under the Python environment subsection for Jython standalone. Navigate to where you just downloaded this file and select it

![](/Burp%20Suite/images/jython_standalone.png)

## Task 12.5 - no answer needed

### Burp is now set to go for installing extensions. Switch to the BApp Store sub-tab of Extender and look for extensions

## Task 12.6

### Q: Which extension allows us to bookmark various requests?

A: Bookmarks

![](/Burp%20Suite/images/bookmarks.png)

</p>
</details>

<details><summary>Task 13.1 to 13.2 - Burp Suite Pro</summary>
<p>

## Task 13.1

### Q: Download the report attached to this take. What is the only critical issue?

A: Cross-origin resource sharing: arbitrary origin trust

![](/Burp%20Suite/images/cors.png)

## Task 13.2

### Q: How many `certain` low issues did Burp find?

A: 12

![](/Burp%20Suite/images/low.png)
