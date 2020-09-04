#  TryHackMe - Nessus (Room 012)

<details><summary>Installation</summary>
<p>

To install Nessus, first register for a Nessus Home License. This license can be used to scan up to 16 IP addresses at a time. Here is the registration [link](https://www.tenable.com/products/nessus-home)

![](/Nessus/images/reg.png)

Next, follow the installation instructions on Tenable's website. Once Nessus is set up, connect the machine that it lives on to the network using your VPN file

![](/Nessus/images/install.png)

After installing, it will take some time to initialize

![](/Nessus/images/downloading.png)

</p>
</details>

<details><summary>Nessus Essentials</summary>
<p>
	
As we launch Nessus, we are greeted with a button to launch a scan called `New Scan`. Nessus allows us to create custom templates that can be used during the scan selection as additional scan types inside the `Policies` menu

Nessus also allows us to change plugin properties such as hiding them or changing their severity via the `Plugin Rules`

We can also run through multiple `Scanners` where multiple installations can work together to complete scans or run scans on remote networks via the `Scanners` menu

There are various different scan types inside of Nessus. One of the most popular ones is the `Host Discovery` scan which simply lets us see what hosts are alive on the network. Another useful scan type is the `Basic Network Scan` which is considered suitable for any host

In Nessus, it is often useful to run a scan wherein the scanner can authenticate to systems and evaluate their patching level. The `Credentialed Patch Audit` scan allows us to do exactly that

When performing Web App tests, it is often useful to run the `Web Application Tests` scan. This can be incredibly useful when also using Nikto, ZAP, and Burp to gain a full picture of an application

</p>
</details>