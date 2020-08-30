#  TryHackMe - Vulnversity (Room 009)

<details><summary>Task 2 - Reconnaissance</summary>
<p>

## Task 2.2

### Q: Scan the box, how many ports are open?

A: 6

Walkthrough: Simply scan the machine using the `nmap -A -T4 <IP>` command to reveal open ports

![](/Vulnversity/images/nmap_scan.png)

## Task 2.3

### Q: What version of the Squid Proxy is running on the machine?

A: 3.5.12

Walkthrough: Found in the output of the nmap scan detailed above

## Task 2.4

### Q: How many ports will nmap scan if the flag -p-400 was used?

A: 400

Walkthrough: The `-p-` flag indicates a range of ports to scan. With 400 given at the end, this indicates it will scan port 1-400

## Task 2.5

### Q: Using the nmap flag -n, what will it not resolve?

A: DNS 

Walkthrough: Using the `nmap -h` command, we can see other flags. Scroll down and you will see the `-n` flag

![](/Vulnversity/images/nmap.png)

## Task 2.6

### Q: What is the most likely OS this machine is running

A: Ubuntu

Walkthrough: In SSH, it willt tell us the version of the package installed (Ubuntu). It also indicates Ubuntu through multiple other services such as HTTP as well

![](/Vulnversity/images/ubuntu.png)

## Task 2.7

### Q: What port is the web server running on?

A: 3333

Walkthrough: Scrolling down we can see that port 3333 is running the HTTP service. HTTP is used for websites and web servers

</p>
</details>

<details><summary>Task 3 - Locating Directories using GoBuster</summary>
<p>

## Task 3.1 - no answer needed

Run GoBuster with a wordlist using the `gobuster dir -u http://10.10.76.37:3333 -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt` command

## Task 3.2

### Q: What is the directory that has an upload form page?

A: /internal/

Walkthrough: Going through the GoBuster results and navigating to each page reveals that the /internal/ directory has an upload form

![](/Vulnversity/images/upload.png)

</p>
</details>

<details><summary>Task 4 - Compromise the Web Server</summary>
<p>
	
## Task 4.1

### Q: Try uploading a few file types to the server, what common extension seems to be blocked?

A: .php

Walkthrough: Since we know this is an Apache server thanks to the Nmap scan, we know that Apache typically works with .php files. There are multiple file extensions for PHP:

* .php
* .phtml
* .php3
* .php4
* .php5
* .phps

We can try uploading simple text documents modified to have these extensions and see what one is possibly blocked

![](/Vulnversity/images/php_tests.png)

Uploading the `.php` extension file presents a message stating that the extension is not allowed

![](/Vulnversity/images/banned.png)

## Task 4.2

To identify which extensions are not blocked, we can fuzz the upload form. To do this, use Burp Suite

## Task 4.3

### Q: What extension is allowed?

A: .phtml

Walkthrough: To begin, make a wordlist with the extensions presented earlier

![](/Vulnversity/images/phpext.png)

Next, upload a file and capture the request via Burp Suite and send it to Intruder. Click on `Payloads` and select the wordlist we created to load into it

Click the `Positions` tab, find the filename and `Add` to the extension

![](/Vulnversity/images/burp.png)

Run the attack and look at the results. The `.phtml` response will have a different length and include a different response than before

![](/Vulnversity/images/success.png)

## Task 4.4

We can use a PHP reverse shell as our payload. A reverse shell works by being called on the remote host and forcing this host to make a connection to us

We listen for incoming connections, upload and have our shell executed which will beacon out back to our listener

A good PHP reverse shell is located [here](https://github.com/pentestmonkey/php-reverse-shell/blob/master/php-reverse-shell.php)

To gain remote access to this machine, follow these steps:

1. Edit the PHP reverse shell file and edit the IP to be our VPN IP
2. Rename this file to php-reverse-shell.phtml
3. Listen for incoming connections using netcat via `nc -nvlp 1234`
4. Upload the shell and navigate to http://MACHINE_IP:3333/internal/uploads/php-reverse-shell.phtml and execute the payload
5. Get a connection back via netcat

![](/Vulnversity/images/changeip.png)

![](/Vulnversity/images/shell.png)

## Task 4.5

### Q: What is the name of the user who manages the webserver?

A: bill

Walkthrough: Navigate to the /home directory and have a look at the users. There is only one user

![](/Vulnversity/images/bill.png)

## Task 4.6

### Q: What is the user flag?

A: 8bd7992fbe8a6ad22a63361004cfcedb

Walkthrough: The `user.txt` flag in most CTFs is located on the Desktop of the user. Simply navigate to the Desktop and cat the .txt file. In this case, it is located inside `/home/bill/user.txt`

![](/Vulnversity/images/flag.png)

</p>
</details>