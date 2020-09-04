#  TryHackMe - Web Scanning (Room 011)

<details><summary>Task 1 - Nikto</summary>
<p>

## Task 1.1

### Q: What switch do we use to set the target host?

A: -h

Notes: Nowhere in the Nikto manual or help page does it say that `-h` lets you specify the target host. Both the manual and help page show this for host. The `-h` can be used however as a shortcut

![](Web%20Scanning/images/h.png)

## Task 1.2

### Q: Websites do not always properly redirect to their secure transport port and can sometimes have different issues depending on the manner in which they are scanned. How do we disable secure transport?

A: -nossl

![](Web%20Scanning/images/nossl.png)

## Task 1.3

### Q: How about the opposite, how do we force secure transport?

A: -ssl

![](Web%20Scanning/images/ssl.png)

## Task 1.4

### Q: What if we want to set a specific port to scan?

A: -p

![](Web%20Scanning/images/port.png)

## Task 1.5

### Q: As the web is constantly evolving, so is Nikto. A database of vulnerabilities represents a core component to this web scanner. How do we verify that this database is working and free from error?

A: -dbcheck

![](Web%20Scanning/images/dbcheck.png)

## Task 1.6

### Q: If instructed to, Nikto will attempt to guess and test both files within directories as well as usernames. Which switch and numerical value do we use to set Nikto to enumerate usernames in Apache? Keep in mind this option is deprecated in favour of plugins, however, it is still a great option to be aware of

A: -mutate 3

![](Web%20Scanning/images/mutate3.png)

## Task 1.7

### Q: Suppose we know the username and password for a web forum, how do we set Nikto to do a credentialed check? Suppose the username is admin and the password is PrettyAwesomePassword1234

A: -id admin:PrettyAwesomePassword1234

![](Web%20Scanning/images/id.png)

## Task 1.8

### Q: Scan the target machine, what web server do we discover and what version is it?

A: Apache/2.4.7

![](Web%20Scanning/images/apache.png)

## Task 1.9

### Q: This box is vulnerable to very poor directory control due to it's web server version. What directory is indexed that really shouldn't be?

A: config

![](Web%20Scanning/images/config.png)

## Task 1.10

### Q: Nikto scans can take a while to fully complete, which switch do we set in order to limit the scan to end at a certain time?

A: -until

![](Web%20Scanning/images/until.png)

## Task 1.11

### Q: How do we list all of the plugins that are available?

A: -list-plugins

![](Web%20Scanning/images/listplugins.png)

## Task 1.12

### Q: On the flip-side of the database, plugins represent another core component to Nikto. Which switch do we use to instruct Nikto to use plugin checks to find out of data software on the target host? Keep in mind that when testing this command, we need to specify the host we intend to run this against. For submitting the answer, use only the base command with the out of data option

A: -Plugins outdated

Notes: Running the command `nikto -list-plugins` lists all avaiable plugins

![](Web%20Scanning/images/listplugins.png)

## Task 1.13

### Q: Finally, what if we would like to use our plugins to run a series of standard tests against the target host?

A: -Plugins tests

![](Web%20Scanning/images/tests.png)

</p>
</details>

<details><summary>Task 2 - OWASP ZAP</summary>
<p>
	
## Task 2.2

### Q: Launch ZAP, what option do we set in order to specify what we are attacking?

A: URL to attack

![](Web%20Scanning/images/attack.png)

## Task 2.3

### Q: Launch the attack against our target

Note: During this attack, you may notice this is very similiar to Nikto. Similiar to Nessus vs. OpenVAS, Nikto and ZAP both offer different perspectives on a host and, as such, it is useful to know how to leverage both scanning tools in order to maximize your own visibility in a situation wherein 'noise' does not particularly matter

## Task 2.4

### Q: ZAP will discover a file that typically contains pages which well-behaved web indexing engines will read in order to know which sections of a site to avoid. What is the name of this file?

A: robots.txt

![](Web%20Scanning/images/robots.png)

## Task 2.5

### Q: One entry is included in the disallow section of this file, what is it?

A: /

![](Web%20Scanning/images/disallow.png)

## Task 2.6

### Q: ZAP will find a directory that contains images for our applications, what is the path for that directory? 

A: /dvwa/images

![](Web%20Scanning/images/images.png)

## Task 2.7

### Q: This website does not force a secure connection by default and ZAP is not pleased with it. Which related cookie is ZAP upset about?

A: HttpOnly

![](Web%20Scanning/images/httponly.png)

## Task 2.8

### Q: Featured in various rooms on TryHackMe, XSS is a vicious attack that is becoming ever more common on the open web. What alert does ZAP produce to let us know that this site is vulnerable to XSS? 

A: Web Browser XSS Protection Not Enabled

![](Web%20Scanning/images/xss.png)

## Task 2.9

### Q: The ZAP proxy spider represents the component responsible for 'crawling' the site. What site is found to be out of scope?

A: http://www.dvwa.co.uk

![](Web%20Scanning/images/outscope.png)

## Task 2.10

### Q: ZAP will use primarily two methods in order to scan a website, which of these two HTTP methods requests content?

A: GET

## Task 2.11

### Q: Which option attempts to submit content to the website?

A: POST

</p>
</details>