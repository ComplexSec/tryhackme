#  TryHackMe - Nessus (Room 012)

<details><summary>Task 3 - Nessus Quiz</summary>
<p>

## Task 3.1

### Q: As we log into Nessus, we are greeted with a button to launch a scan. What is the name of this button?

A: New Scan

## Task 3.2

### Q: Nessus allows us to create custom templates that can be used during the scan selection as additional scan types. What is the name of the menu where we can set these?

A: Policies

## Task 3.3

### Q: Nessus also allows us to change plugin properties such as hiding them or changing their severity. What menu allows us to change this?

A: Plugin Rules

## Task 3.4

### Q: Nessus can also be run through multiple "Scanners" where multiple installations can work together to complete scans or run scans on remote network. What menu allows us to see all of these installations?

A: Scanners

## Task 3.5

### What scan allows us to see simply what hosts are alive?

A: Host Discovery

## Task 3.6

### Q: One of the most useful scan types, what is considered to be 'suitable for any host'?

A: Basic Network Scan

## Task 3.7

### Q: Following a few basic scans, it is often useful to run a scan wherein the scanner can authenticate to systems and evaluate their patching level. What scan allows you to do this?

A: Credentialed Patch Audit

## Task 3.8

### Q: When performing web app tests, it is often useful to run which scan? This can be incredibly useful when also using Nikto, ZAP, and Burp to gain a full picture of an application

A: Web Application Tests

</p>
</details>

<details><summary>Task 4 - Scanning</summary>
<p>
	
## Task 4.2

### Q: Create a new 'Basic Network Scan' targeting the deployed VM. What option can we set under 'BASIC' to set a time for this scan to run? This can be very useful when network congestion is an issue

A: Schedule

## Task 4.3

### Q: Under discovery, set the scan to cover ports 1-65535. What is this type called?

A: Port scan (all ports)

## Task 4.4

### Q: As we are connected to the network via a VPN, it may be to our benefit to 'tone down' the scan a bit. What scan type can we change to under 'ADVANCED' for this lower bandwidth connection?

A: Scan low bandwidth links

## Task 4.6

### Q: After the scan completes, which vulnerability can we view the details of to see the open ports on this host?

A: Nessus SYN Scanner

## Task 4.7

### Q: There seems to be a chat server running on this machine, what port is it on?

A: 6667

## Task 4.8

### Q: Looks like we have a medium level vulnerability relating to SSH. What is this vulnerability named?

A: SSH Weak Algorithms Supported

## Task 4.9

### Q: What web server type and version is reported by Nessus?

A: Apache/2.4.99

</p>
</details>

<details><summary>Task 6 - Web App Scanning</summary>
<p>
	
## Task 6.1

### Q: What is the plugin ID of the plugin that determines the HTTP server type and version?

A: 10107

## Task 6.3

### Q: What authentication page is discovered by the scanner that transmits credentials in cleartext?

A: login.php

## Task 6.4

### Q: What is the file extension of the config backup?

A: .bak

## Task 6.5

### Q: Which directory contains example documents? 

A: /external/phpids/0.6/docs/examples/

## Task 6.6

### Q: What vulnerability is this application susceptible to that is associated with X-Frame-Options?

A: ClickJacking

## Task 6.7

### Q: What version of PHP is the server using?

A: 5.5.9-1ubuntu4.26

</p>
</details>