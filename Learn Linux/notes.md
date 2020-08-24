# Learn Linux (Room 001)

## SSH

About: SSH is the act of remotely accessing a machine. Allows you to run commands interactively on the remote machine - done through the use of a program on the target which allows the SSH client to interface with the target. SSH works with comand line

Connecting: Through the command line, type `ssh shiba1@10.10.32.230`

## Basic Command Execution - echo

About: The echo command returns whatever is inputted into it

Executing: Typing `echo hello`, you will see input echoed back to you

## Manual Pages and Flags

About: Most commands will have options called flags (<command> <flag> <input>). Flags learned using the man command (man <command>). Some commands support the `-h` flag as well

Executing: The `man echo` command shows options for echo command

## Basic File Operations - ls

About: ls commands lists information about every file/directory. The ls -a lists all hidden files aswell

Execution: `ls -a` outputs all entries, `ls -l` produces a long list format

## Basic File Operations - cat

About: cat outputs contents of files to the console. cat supports the `--help` flag

Execution: `cat -n` numbers all the output lines

## Basic File Operations - touch

About: touch creates files

Execution: `touch b.txt` creates a file called b.txt

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

## Advanced File Operators - Background

The `ls` command has different flags allowing you to view information about different types of files

![](/images/ls%20-al%20command.png)
