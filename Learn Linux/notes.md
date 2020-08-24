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

Usage: 	`su shiba2` logs in as shiba2 user
	`su` logs in as root by default	


## Linux Operators - Intro

