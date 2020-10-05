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