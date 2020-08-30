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

GoBuster is a tool used to brute-force URLs (directories and files), DNS subdomains and virtual host names

Download GoBuster [here](https://github.com/OJ/gobuster) or on Kali simply type `sudo apt-get install gobuster`

![](/Vulnversity/images/gobuster.png)

To get started you need a wordlist for GoBuster. If you are using Kali, you can find many wordlists under `/usr/share/wordlists` directory

