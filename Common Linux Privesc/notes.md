#  TryHackMe - Common Linux Privesc (Room 004)

## Understanding Privesc

Privilege escalation involves going from a lower permission to a higher permission. It's the exploitation of a vulnerability, design flaw or configuration oversight in an operating system or app to gain unauthorized access to resources that are usually restricted from users

Priv esc lets you gain system administrator levels of access. Being admin allows you to:

* Reset passwords
* Bypass access controls to compromise protected data
* Edit software configurations
* Enable persistence, so you can access the machine again later
* Change privilege of users

## Direction of Privilege Escalation

![](/Common%20Linux%20Privesc/images/typesofprivesc.png)

There are two main privilege escalation variants:

#### Horizontal Privilege Escalation

This is where you expand your reach over the compromised system by taking over a different user who is on the same privilege level as you. Allows you to inherit whatever files and access that user has. 

Can be used to gain access to another normal privileged user that happens to have an SUID file attached to their home directory which can be used to get super user access

#### Vertical Privilege Escalation

This is where you attempt to gain higher privileges or access, with an existing compromised account. For local priv esc attacks, this might mean hijacking an account with admin privileges or root privileges

## Enumeration

