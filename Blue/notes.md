#  TryHackMe - Blue (Room 017)

<details><summary>What is EternalBlue?</summary>
<p>

![](/Blue/images/msf.jpg)

EternalBlue is the name given to a series of Microsoft software vulnerabilities and the exploit created by the NSA as a cyberattack tool. Although the EternalBlue exploit - MS17-010 - affects only Windows operating systems, anything that uses the SMBv1 file-sharing protocol is technically at risk of being targeted

</p>
</details>

<details><summary>How was EternalBlue developed?</summary>
<p>
	
![](/Blue/images/msf2.jpg)

The origins of the SMB vulnerability are what spy stories are made of - dangerous NSA hacking tools leaked, a notorious group called Shadow Brokers on the hunt for common vulnerabilities and exposures, and a massively popular operating system

According to [condemning statements made by Microsoft](https://blogs.microsoft.com/on-the-issues/2017/05/14/need-urgent-collective-action-keep-people-safe-online-lessons-last-weeks-cyberattack/) EternalBlue was developed by the NSA as part of their controversial program of stockpiling and weaponizing cybersecurity vulnerabilities rather than flagging them to the appropriate vendor

</p>
</details>

<details><summary>How Does EternalBlue Work?</summary>
<p>
	
![](/Blue/images/msf3.jpg)

The EternalBlue exploit works by taking advantage of SMBv1 vulnerabilities present in older versions of Microsoft operating systems. SMBv1 was first developed in 1983 as a network communication protocol to enable shared access to files, printers and ports. It was essentially a way for Windows machines to talk to one another and other devices for remote services

The exploit makes use of the way Microsoft Windows handles or mishandles specially crafted packets from malicious attackers. All the attacker needs to do is send a maliciously-crafted packet to the target server and the malware propogates and a cyberattack ensues

Microsoft's patch closes the security vulnerability completely thus preventing attempts. But a key problem remains - for many versions of Windows, the software update must be installed in order to provide protection

It is THIS key problem that gives EternalBlue such a long shelf life - many people and even businesses fail to update their software regularly, leaving their OS's unpatched and vulnerable

If you want more in-depth information about how it works, check out [this article](https://research.checkpoint.com/2017/eternalblue-everything-know/)

</p>
</details>