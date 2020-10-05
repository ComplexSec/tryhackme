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