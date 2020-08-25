# Learn Linux (Room 001)

## SSH

About: SSH is the act of remotely accessing a machine. Allows you to run commands interactively on the remote machine - done through the use of a program on the target which allows the SSH client to interface with the target. SSH works with comand line

Connecting: Through the command line, type `ssh shiba1@10.10.32.230`

![](/images/ssh_command.png)

## Basic Command Execution - echo

About: The echo command returns whatever is inputted into it

Executing: Typing `echo hello`, you will see input echoed back to you

![](/images/echo_hello.png)

## Manual Pages and Flags

About: Most commands will have options called flags (<command> <flag> <input>). Flags learned using the man command (man <command>). Some commands support the `-h` flag as well

Executing: The `man echo` command shows options for echo command

![](/images/man_echo.png)

## Basic File Operations - ls

About: ls commands lists information about every file/directory. The ls -a lists all hidden files aswell

Execution: `ls -a` outputs all entries, `ls -l` produces a long list format

![](/images/ls_commands.png)

## Basic File Operations - cat

About: cat outputs contents of files to the console. cat supports the `--help` flag

Execution: `cat -n` numbers all the output lines

![](/images/cat_-n.png)

## Basic File Operations - touch

About: touch creates files

Execution: `touch b.txt` creates a file called b.txt

![](/images/touch_command.png)

## Basic File Operations - Running a Binary

About: To run programs, provide the full path to the binary. Binary is executable code. Can use relative paths to execute binaries

Executing: 

Running a binary using directory shortcut `./hello`. 

Running a binary in your home directory using ~ `~/hello`.

Running a binary called hello in previous directory `../hello`


## su

About: su allows you to change the user, without logging out and logging back in 

Usage: 	

`su shiba2` logs in as shiba2 user
        
`su` logs in as root by default	

## Linux Operators - `>`

About: `>` is the operator for output redirection. Can redirect output of any command to a file

Usage: `echo hello > file.txt` writes hello to file.txt

Additional notes: Using this operator on an existing file erases the content of the file and replaces it

## Linux Operators - `>>`

About: `>>` does the same thing as `>` but appends the output to a file instead of erasing

Usage: `echo noot >> file.txt` appends noot to file.txt

## Linux Operators - `&&`

About: `&&` means AND. Allows execution of second command after first one executed successfully

Usage: `ls & echo hello` - lists files and prints hello

Additional notes: Can use something created in the first command in the second command

## Linux Operators - `&`

About: `&` is a background operator. Can run commands in the background

Usage: `sleep 5 &` - sleeps for 5 seconds in the background

## Linux Operators - `$`

About: `$` is used to denote environment variables. Variables set by the computer that are used to affect different processes and how they work. Current user is always stored in a variable called $USER

Usage: `echo $USER` - prints the current user value of $USER

Additional notes: Environment variables can be used as input for other commands

Additional Usage: `touch $USER` - creates file called the current user

## Linux Operators - `|`

About: `|` allows you to take the output of a command and use it as input for another. Not all commands support piping.

Usage: `cat test | grep 123` - prints content of test and searches for 123 inside the output

## Linux Operators - `;`

About: `;` works similiar to && but does not require the first command to execute successfully

Usage: `fakecommand; ls` - executes ls command

## Advanced File Operators - chmod

About: The `chmod` command allows you to set different permissions for a file. Set using a three digit number where each digit controls a specific permission

Digit | Meaning
------------ | -------------
1 | That file can be executed
2 | That file can be written to
3 | That file can be executed and written to
4 | That file can be read
5 | That file can be read and executed
6 | That file can be written to and read
7 | That file can be read, written to and executed

File permissions are divided into three sections

* User
* Group
* Everyone

## Advanced File Operators - chown

About: The `chown` allows us to change the user and group for any file.  Syntax is `chown user:group <filename>`. Can only use chown if you have higher privileges than the other user

Usage: `chown shiba2:shiba2 file` changes owner and group of file to shiba2

![](/images/chown_command.png)

Additional notes: Can use chown without specifying a group

![](/images/chown2_command.png)

## Advanced File Operators - rm

About: The `rm` command removes files. Need write permissions to the file to delete it

Usage: `rm file` deletes the file called file

![](/images/rm_command.png)

## Advanced File Operators - mv

About: The `mv` command allows you to move files from one place to another. Syntax is `mv <file> <destination>`

Usage: `mv file ~` moves file into the home directory

![](/images/mv_command.png)

Additional notes: Can use `mv` command to change the name of a file

Usage: `mv file ~ghfds` will rename file to ghfds

![](/images/mv2_command.png)

## Advanced File Operators - cp

About: The `cp` command does the same thing as mv except instead of moving the file, it duplicates it. Syntax is `cp <file> <destination>`

## Advanced File Operators - cd && mkdir

About (cd): The `cd` command allows you to change directory. Relative paths are supported as well as absolute paths. Syntax is `cd <directory>`

Usage: `cd aa` moves us into the `aa` directory

![](/images/cd_command.png)

About (mkdir): The `mkdir` command allows us to make a new directory to store files in. Syntax is `mkdir <directory_name>`

## Advanced File Operators - ln

About: The `ln` command has two different uses. One is what is known as hard linking, which duplicates the file and links the duplicate to the original - whatever happens to the created link, is also done to the original file. Syntax is `ln <source> <destination>`

![](/images/lnhard_command.png)

About: The next form of linking is symbolic linking (symlink). A symbolic link is a glorified reference, meaning that the actual symbolic link has no data in it at all - just a reference to another file. Syntax is `ln -s <file> <destination>`

![](/images/lnsym_command.png)

Additional notes: The permissions on the symblink has 777, but since it is just a reference, it still has the same perms as the original file

## Advanced File Operators - find

About: The `find` command allows us to find files. Lists every file in the current directory. Is recursive. Only lists files in directories you have permission to access

Usage: 

* `find dir -user` would list every file owned by a specific user
* `find dir -group` would list every file owned by a specific group

![](/images/find_command.png)

## Advanced File Operators - grep

About: The `grep` command allows us to find data inside of data. Syntax is `grep <string> <file>`. Can use it in piping

Usage: `find /* | grep test1234` would find all files on the system and grep would narrow it down to just files containing test1234 in the name

![](/images/grep_command.png)

Additional usage: `grep hello test -n` would grep for the string hello in the file test while printing numbered lines

![](/images/grep2_command.png)

Additional notes: The `grep` command supports regular expressions
