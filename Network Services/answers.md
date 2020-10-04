#  TryHackMe - Network Services (Room 015)

<details><summary>Task 1 - Understanding SMB</summary>
<p>

## Task 1.1

### Q: What does SMB stand for?

A: Server Message Block Protocol

## Task 1.2

### Q: What type of protocol is SMB?

A: Response-Request

## Task 1.3

### Q: What do clients connect to servers using?

A: TCP/IP

## Task 1.4

### Q: What systems does Samba run on?

A: Unix

</p>
</details>

<details><summary>Task 2 - Enumerating SMB</summary>
<p>
	
## Task 2.1

### Q: Conduct an __nmap__ scan of your choosing. How many ports are open?

A: 3

![](/Network%20Services/images/nmap.png)

## Task 2.2

### Q: What port is SMB running on?

A: 139/445

## Task 2.3

### Q: Let's get started with Enum4Linux, conduct a full basic enumeration. For starters, what is the WORKGROUP name?

A: WORKGROUP

![](/Network%20Services/images/WORKGROUP.png)


## Task 2.4

### Q: What comes up as the __name__ of the machine?

A: POLOSMB

![](/Network%20Services/images/polosmb.png)

## Task 2.5

### Q: What operating system version is running?

A: 6.1

## Task 2.6

### Q: What share sticks out as something we might want to investigate?

A: profiles

![](/Network%20Services/images/profiles.png)

</p>
</details>