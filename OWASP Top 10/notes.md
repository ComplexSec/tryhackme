#  TryHackMe - OWASP Top 10 (Room 008)

<details><summary>1 - Injection</summary>
<p>

![](/OWASP%20Top%2010/images/command_inj.png)

<details><summary>Day 1 - Injection</summary>
<p>

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

<details><summary>Day 1 - OS Command Injection</summary>
<p>

Command Injection occures when server-side code in a web application makes a system call on the hosting machine

It is a web vulnerability that allows an attacker to take advantage of that made system call to execute OS commands on the server. Sometimes this won't always end in something malicious, like a `whoami` or just reading files

Command Injection opens up many options for the attacker. The worst thing they could do would be to spawn a reverse shell to become the user that the web server is running as. A simple `;nc -e /bin/bash` is all that is needed and they own the server

Some variants of netcat do not support the `-e` option. You can use a list of [these](http://pentestmonkey.net/cheat-sheet/shells/reverse-shell-cheat-sheet) reverse shells as an alternative

Once the attacker has a foothold on the server, they can start the usual enumeration of your systems and start looking for ways to pivot around

</p>
</details>

<details><summary>Day 1 - Command Injection Practical</summary>
<p>

