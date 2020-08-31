#  TryHackMe - ToolsRUs (Room 010)

<details><summary>Task 1</summary>
<p>

## Task 1.1

### What directory can you find that begins with "g"?

A: guidelines

Walkthrough: First step in any CTF is doing a simple `nmap` command to find information such as open ports, version detection and OS detection if possible. Achieved through the `nmap -A -T4 -p- <ip>` command

![](/ToolsRUs/images/nmap_scan.png)

We now know that there is a webserver located on port 80. Navigating to the web page reveals a simple page. Looking at the source code, nothing jumps out at us either

![](/ToolsRUs/images/tosrus.png)

We can brute force directories now to see if any hidden directories are revealed using Gobuster

![](/ToolsRUs/images/301.png)

## Task 1.2

### Q: Whose name can you find from this directory?

A: bob

Walkthrough: Simply navigating to this page reveals a question directed to `Bob`

## Task 1.3

### Q: What directory has basic authentication?

A: protected

Walkthrough: Navigating to the page pops up a login prompt. This indicates very basic authentication for this page

![](/ToolsRUs/images/basic.png)

## Task 1.4

### Q: What is bob's password to the protected part of the website?

A: bubbles

Walkthrough: Using `hydra` - the password cracking tool - we can brute force the password with the typical `rockyou.txt` wordlist to try and get the password successfully

![](/ToolsRUs/images/hydra.png)

In this command:

* `hydra` is the tool
* `-l bob` indicates the username we want to try
* `-P /opt/rockyou.txt` is the wordlist we want to use
* `-f` indicates to exit once a result is found
* `10.10.46.187` is the IP
* `http-get` is the method we want to use
* `/protected` is the protected URL
* `-t 4` indicates the number of threads
* `-V` shows each username:password combination

After a second or two, you will get a positive result for a correct password

![](/ToolsRUs/images/bubbles.png)

Navigating to this page reveals some interesting information. It reveals that the protected page has moved to a different port

![](/ToolsRUs/images/different.png)

## Task 1.5

### Q: What other port that serves a web service is open on the machine?

A: 1234

Walkthrough: Looking back through our Nmap scan, we can see that there is an HTTP service running Apache Tomcat/Coyote JSP engine 1.1 on port 1234

## Task 1.6

### Q: Going to the service running on that port, what is the name and version of the software?

A: Apache Tomcat/7.0.88

Walkthrough: Navigating to that page, we get an Apache tomcat page. At the top, it reveals the version and name of the service running

![](/ToolsRUs/images/apache.png)

## Task 1.7

### Q: Use Nikto with the credentials you have found and scan the /manager/html directory on port 1234. How many documentation files did Nikto identify?

A: 5

Walkthrough: Using Nikto with the following parameters:

* `nikto` is the tool
* `-h http://10.10.46.187:1234/manager/html` specifies the URL we want to scan
* `-id bob:bubbles` indicates the credentials we want to use
* `-o /home/complexity/tryhackme/niktoscan.txt` indicates the output file

Going through the Nikto scan results, we can see some documentation files it found

## Task 1.8

### Q: What is the server version (run the scan against port 80)

A: Apache/2.4.18

Walkthrough: Look through the results of the initial Nmap scan and check port 80 details

## Task 1.9

### Q: What version of Apache-Coyote is this service using?

A: 1.1

Walkthrough: Again, simply look through the results of the same nmap scan performed earlier

## Task 1.10

### Q: Use Metasploit to exploit the service and get a shell on the system. What user did you get a shell as?

A: root

Walkthrough: Using Searchsploit and searching for Tomcat and grepping for ".rb" extensions for Metasploit modules, we find a couple of interesting exploits

![](/ToolsRUs/images/tomcat.png)

We are only interested in remote exploits. This means we do not need to be local and can execute from our own computer.

After going through a couple, you will reach the one titled `multiple/remote/31433.rb` - this one requires authentication which we have due to the credentials we cracked earlier

![](/ToolsRUs/images/searchsploit.png)

Loading this module up in Metasploit, we can start to set the options

![](/ToolsRUs/images/options.png)

After setting the options, we can simply run the module and we should get a meterpreter session back. Running the `getuid` command inside Meterpreter reveals that we are the root user

![](/ToolsRUs/images/root.png)

## Task 1.11

### Q: What text is in the file /root/flag.txt?

A: ff1fc4a81affcc7688cf89ae7dc6e0e1

Walkthrough: Simply navigate to the directory and `cat` out the file to reveal its contents

![](/ToolsRUs/images/flag.png)

</p>
</details>