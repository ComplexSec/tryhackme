#  TryHackMe - OWASP Juice Shope (Room 007)

<details><summary>Introduction</summary>
<p>

![](/OWASP%20Juice%20Shop/images/juice_shop.png)

Within this room, we will look at OWASP's Top 10 vulnerabilities in web applications. You will find these in all types of web applications.

This room will cover the following topics:

* [Injection](https://owasp.org/www-project-top-ten/OWASP_Top_Ten_2017/Top_10-2017_A1-Injection)
* [Broken Authentication](https://owasp.org/www-project-top-ten/OWASP_Top_Ten_2017/Top_10-2017_A2-Broken_Authentication)
* [Sensitive Data Exposure](https://owasp.org/www-project-top-ten/OWASP_Top_Ten_2017/Top_10-2017_A3-Sensitive_Data_Exposure)
* [Broken Access Control](https://owasp.org/www-project-top-ten/OWASP_Top_Ten_2017/Top_10-2017_A5-Broken_Access_Control)
* [Cross-site Scripting (XSS)](https://owasp.org/www-project-top-ten/OWASP_Top_Ten_2017/Top_10-2017_A7-Cross-Site_Scripting_(XSS))

</p>
</details>

<details><summary>Let's Go on an Adventure</summary>
<p>

## Let's Go on an Adventure

Before getting into the actual hacking part, it's good to have a look around.

In Burp, set the Intercept mode to off and then browse the site. This allows Burp to log different requests from the server that may be helpful later

This is called __walking through__ the application.

</p>
</details>

<details><summary>Inject the Juice</summary>
<p>
	
## Inject the Juice

![](/OWASP%20Juice%20Shop/images/sql_injection.png)

This task will focus on injection vulnerabilities. Injection vulnerabilities are quite dangerous to a company as they can potentially cause downtime and/or loss of data. 

Identifying injection points within a web application is usually quite simple, as most of them will return an error

There are many types of injection attacks, some of them are:

* SQL Injection - is when an attacker enters a malicious or malformed query to either retrieve or tamper data from a database. And in some cases, log into accounts
* Command Injection - is when web apps take input or user-controlled data and run them as system commands. An attacker may tamper with this data to execute their own system commands. This can be seen in applications that perform misconfigured ping tests
* Email injection - is a security vulnerability that allows malicious users to send email messages without prior authorization by the email server. These occur when the attacker adds extra data to fields which are not interpreted by the server correctly

In this case, we will use SQL Injection

For more information, check [here](https://owasp.org/www-project-top-ten/OWASP_Top_Ten_2017/Top_10-2017_A1-Injection)

</p>
</details>

<details><summary>Who Broke My Lock?</summary>
<p>

![](/OWASP%20Juice%20Shop/images/broken_auth.png)

In this task, we will look at exploiting authentication through different flaws. When talking about flaws within authentication, we include mechanisms that are vulnerable to manipulation. These mechanisms are what we will be exploiting:

* Weak passwords in high privileged accounts
* Forgotten password pages

For more information, check [here](https://owasp.org/www-project-top-ten/OWASP_Top_Ten_2017/Top_10-2017_A2-Broken_Authentication)

</p>
</details>

<details><summary>AH! Don't Look!</summary>
<p>

## AH! Don't Look!

![](/OWASP%20Juice%20Shop/images/sens_data.png)

A web app should store and transmit sensitive data safely and securely. In some cases, the developer may not correctly protect their sensitive data, making it vulnerable

Most of the time, data protection is not applied consistently across the web app making certain pages accessible to the public. Other times information is leaked to the public without the knowledge of the developer, making the web app vulnerable to an attack

For more information, check [here](https://owasp.org/www-project-top-ten/OWASP_Top_Ten_2017/Top_10-2017_A3-Sensitive_Data_Exposure)

</p>
</details>

<details><summary>Who's Flying This Thing?</summary>
<p>

## Who's Flying This Thing?

Modern day systems allows for multiple users to have access to different pages. Administrators most commonly use an administration page to edit, add and remove different elements of a website. You might use these when building a website via Weebly or Wix

When Broken Access Control exploits or bugs are found, it will be categorized into one of two types:

Categories | Description
------------ | -------------
Horizontal Privilege Escalation | Occurs when a user can perform an action or access data of another user with the __same__ level of permission
Vertical Privilege Escalation | Occurs when a user can perform an action or access data of another user with a __higher__ level of permission

