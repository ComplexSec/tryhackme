#  TryHackMe - Vulnversity (Room 009)

<details><summary>Reconnaissance</summary>
<p>

![](/Vulnversity/images/vuln.png)

Nmap is a free open-source and powerful tool used to discover hosts and services on a computer network

Nmap has many capabilities. Some common functionalities are:

Nmap Flag | Description
------------ | -------------
__-sV__ | Attempts to determine the version of services running
__-p <x>__ or __-p-__ | Port scan for port <x> or scan all ports
__-Pn__ | Disable host discovery and just scan for open ports
__-A__ | Enable OS and version detection, executes in-build scripts for further enumeration
__-sC__ | Scan with the default nmap scripts
__-v__ | Verbose mode
__-sU__ | UDP port scan
__-sS__ | TCP SYN port scan

</p>
</details>

<details><summary>Locating Directories using GoBuster</summary>
<p>

![](/Vulnversity/images/gob.png)

GoBuster is a tool used to brute-force URLs (directories and files), DNS subdomains and virtual host names

Download GoBuster [here](https://github.com/OJ/gobuster) or on Kali simply type `sudo apt-get install gobuster`

![](/Vulnversity/images/gobuster.png)

Some common GoBuster flags are:

GoBuster flag | Description
------------ | -------------
__-e__ | Print the full URLs in your console
__-u__ | The target URL
__-w__ | Path to your wordlist
__-U and -P__ | Username and Password for Basic Auth
__-p <x>__ | Proxy to use for requests
__-c <http_cookies>__ | Specify a cookie for simulating your auth

</p>
</details>

<details><summary>Compromise the Web Server</summary>
<p>

Now you have found a form to upload files, we can leverage this to upload and execute our payload which will lead to compromising the server

Check out the [answers](https://github.com/ComplexSec/tryhackme/blob/master/Vulnversity/answers.md) for a walkthrough

</p>
</details>
