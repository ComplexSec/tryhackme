#  TryHackMe - OWASP Top 10 (Room 008)

<details><summary>Day 1 - Injection</summary>
<p>

![](/OWASP%20Top%2010/images/command_inj.png)

<details><summary>Injection</summary>
<p>

## Injection

Injection flaws are very common. These flaws occur because the user controlled input is interpreted as actual commands or parameters by the application. Injection attacks depend on what technologies are being used and how exactly the input is interpreted by these technologies

Some common exmaples include:

* SQL Injection: This occures when user controlled input is passed to SQL queries. As a result, an attacker can pass in SQL queries to manipulate the outcome of such queries
* Command Injection: This occurs when user input is passed to system commands. As a result, an attacker is able to execute arbitrary system commands on application servers

If an attacker is able to successfully pass input that is interpreted correctly, they would be able to do the following:

* Access, Modify and delete information in a database when this input is passed into database queries. This would mean that an attacker can steal sensitive information such as personal details and credentials
* Execute Arbitrary system commands on a server that would allow an attacker to gain access to users' systems. This would enable them to steal sensitive data and carry out more attacks against infrastructure linked to the server on which the command is executed

The main defence for preventing injection attacks is ensuring that user controlled input is not interpreted as queries or commands. There are different ways of doing this:

* Using an allow list: when input is sent to the server, this input is compared to a list of safe input or characters. If the input is marked as safe, then it is processed. Otherwise, it is rejected and the application throws an error
* Stripping input: If the input contains dangerous characters, these characters are removed before they are processed

Dangerous characters or input is classified as any input that can change how the underlying data is processed. Instead of manually constructing allow lists or even just stripping input, there are various libraries that perform these actions for you

</p>
</details>

<details><summary>OS Command Injection</summary>
<p>

## OS Command Injection

Command Injection occures when server-side code in a web application makes a system call on the hosting machine

It is a web vulnerability that allows an attacker to take advantage of that made system call to execute OS commands on the server. Sometimes this won't always end in something malicious, like a `whoami` or just reading files

Command Injection opens up many options for the attacker. The worst thing they could do would be to spawn a reverse shell to become the user that the web server is running as. A simple `;nc -e /bin/bash` is all that is needed and they own the server

Some variants of netcat do not support the `-e` option. You can use a list of [these](http://pentestmonkey.net/cheat-sheet/shells/reverse-shell-cheat-sheet) reverse shells as an alternative

Once the attacker has a foothold on the server, they can start the usual enumeration of your systems and start looking for ways to pivot around

</p>
</details>

<details><summary>Command Injection Practical</summary>
<p>

## What is Active Command Injection?

Blind command injection occurs when the system command made to the server does not return the response to the user in the HTML document. Active command injection will return the response to the user. It can be made visible through several HTML elements

Scenario: EvilCorp has started development on a web based shell but has accidentally left it exposed to the internet. It is nowhere near finished but contains the same command injection vulnerability as before but this time, the response from the system call can be seen on the page

Just like before, look at the sample code from evilshell.php and go over what it is doing and why it makes it active command injection. 

![](/OWASP%20Top%2010/images/evilshell.png)

In pseudocode, the above snippet is doing the following:

1. Checking if the parameter "commandString" is set
2. If it is, then the variable $command_string gets what was passed into the input field
3. The program then goes into a try block to execute the function `passthru($command_string)`. Read the docs on `passthru()` on [PHP's website](https://www.php.net/manual/en/function.passthru.php) but in general, it is executing what gets entered into the input then passing the output directly back to the browser
4. If the try does not succeed, output the error to the page. Generally, this won't output anything because you cannot output stderr but PHP does not let you have a try without a catch

## Ways to Detect Active Command Injection

We know that active command injection occurs when you can see the response from the system call. In the above code, the function `passthru()` is actually what is doing all the work. It is passing the response directly to the document so you can see the fruits of your labour right there.

Since we know that, we can go over some useful commands to try to enumerate the machine a bit further. The function call here to `passthru()` may not always be what is happening behind the scenes

## Commands to Try

### Linux

* whoami
* id
* ifconfig / ip a
* uname -a
* ps -ef

### Windows

* whoami
* vers
* ipconfig
* tasklist
* netstat -an

</p>
</details>

</p>
</details>

<details><summary>Day 2 - Broken Authentication</summary>
<p>

![](/OWASP%20Top%2010/images/broken_auth.png)

<details><summary>Broken Authentication</summary>
<p>

## Broken Authentication

Authentication and session management constitute core components of modern web apps. Authentication allows users to gain access to web applications by verifying their identities

The most common form of authentication is using a username and password mechanism. A user would enter these credentials and the server would verify them. If they were correct, the server would then provide the user's browser with a session cookie

A session cookie is needed because web servers use HTTP(S) to communicate which is stateless. Attaching session cookies means that the server will know who is sending what data

If an attacker is able to find flaws in an authentication mechanism, they would then successfully gain access to other user's accounts. This would allow the attacker to access sensitive data

Some common flaws in authentication mechanisms include:

* Brute force attacks: If a web app uses usernames and passwords, an attacker is able to launch brute force attacks that allow them to guess the username and passwords using multiple authentication attempts
* Use of weak credentials: Web applications should set strong password policies. If applications allow users to set passwords such as `password` or common passwords, then an attacker is able to easily guess them and access user accounts. They can do this without brute forcing and without multiple attempts
* Weak Session Cookies: session cookies are how the server keeps track of users. If session cookies contain predictable values, an attacker can set their own session cookies and access user's accounts

There can be various mitigation techniques for broken authentication mechanisms depending on the exact flaw

* To avoid password guessing attacks, ensure the app enforces a strong password policy
* To avoid brute force attacks, ensure the app enforces an automatic lockout after a certain number of attempts. This would prevent an attacker from launching more brute force attacks
* Implement Multi Factor Authentication - if a user has multiple methods of authentication it would be difficult to get access to both credentials to get access to their account

</p>
</details>

<details><summary>Broken Authentication Practical</summary>
<p>

## Broken Authentication Practical

A lot of times what happens is that developers forget to sanitize the input given by the user in the code of their application, which can make them vulnerable to attacks like SQLi. However, we are going to focus on a vulnerability that happens because of a developer's mistake but is very easy to exploit i.e. re-registration of an existing user

Say there is an existing user with the name __admin__ and now we want to get access to their account. We can re-register that username but with slight modification like "  admin"

Now when you enter that in the username field and enter other information, it will register a new user but that user will have the same right as normal admin. That new user will also be able to see all the content presented under the user __admin__

To see this in action, go to `http://<IP>:8888` and try to register a user name __darren__ you will see that user already exists so then try to register a user " darren" and you will see that you are now logged in and will be able to see the content present only in Darren's account which in our case is the flag that you need to retrieve

</p>
</details>

</p>
</details>

<details><summary>Day 3 - Sensitive Data Exposure</summary>
<p>

![](/OWASP%20Top%2010/images/sens.png)

<details><summary>Sensitive Data Exposure</summary>
<p>

## Sensitive Data Exposure

When a web app accidentally divulges sensitive data, we refer to it as "Sensitive Data Exposure". This is often data directly linked to customers (names, DoBs, financial information, etc...) but could also be more technical information such as usernames and passwords

At more complex levels, this often involves techniques such as a MitM attack where the attacker would force user connections through a device whcih they control, then take advantage of weak encryption on any transmitted data to gain access to the intercepted information

Many examples are much simpler and vulnerabilities can be found in web apps which can be exploited without any advanced networking knowledge

The web app in this box contains one such vulnerability

</p>
</details>

<details><summary>Sensitive Data Exposure - Supporting Material 1</summary>
<p>

## Sensitive Data Exposure - Supporting Material 1

The most common way to store a large amount of data in a format that is easily accessible from many locations at once is in a database. This is obviously perfect for something like a web app, as there may be many users interacting with the website at any one time

Database engines usually follow the Structured Query Language (SQL) synax; however, alternative formats (such as NoSQL) are rising in popularity

In a production environment, it is common to see databases set up on dedicated servers, running a database service such as MySQL, or MariaDB; however, databases can also be stored as files

These databases are referred to as __flat-file__ databases as they are stored as a single file on the computer. Commonly seen on smaller web apps

What happens if the database is stored underneath the root directory of the website (one of the files that a user connecting to the website is able to acecss?) Well, we can download it and query it on our own machine, with full access to everything in the database

The most common format of flag-file database is an __sqlite__ database. These can be interacted with in most programming languages, and have a dedicated client for querying them on the command line. This client is called __sqlite3__ and is installed by default on Kali

To access a local sqlite database, use the `sqlite3 <database_name>` command

From there, you can see the tables in the database by using the `.tables` command

![](/OWASP%20Top%2010/images/sens.png)

At this point, we can dump all of the data from the table, but we won't necessarily know what each column means unless we look at the table information

First, use the `PRAGMA table_info(<table_name>)` command to see the table information. After that, you can use the `SELECT * FROM customers;` to dump the information from the table

![](/OWASP%20Top%2010/images/customers.png)

We can see from the table information that there are four columns:

* custID
* custName
* creditCard
* password

</p>
</details>

<details><summary>Sensitive Data Exposure - Supporting Material 2</summary>
<p>

## Sensitive Data Exposure - Supporting Material 2

In the previous task we found a collection of password hashes. When it comes to hash cracking, Kali comes pre-installed with various tools

For this, we can use the online tool [Crackstation](https://crackstation.net/). This website is extremely good at cracking weak password hashes. For more complicated hashes, we would need more sophisticated tools

Simply paste the hashes we found earlier into the box and hit the `Crack Hashes` button and it should successfully break the password

![](/OWASP%20Top%2010/images/crackstation.png)

</p>
</details>

</p>
</details>