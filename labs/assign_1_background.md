# Verify Local Environment

## Connect to Node 

SSH is a generic term used for the SSH protocol. ssh is the client command for connecting to remote nodes. sshd is the server program that runs on the remote node that must be up and running to allow for connections. 

ssh, Secure Shell is a way to connect to remote nodes. There are clients available on multiple operating systems. It is not a true shell like bash and tcsh. You need a username and password, or passphrase if using ssh keys.  

We have pre-established a privileged account on the remote node, and providing you with a username and password. When you use the ssh client, whether ssh on Mac or a GUI like putty on Windows, you are connecting to that node. 

## Basic Unix Commands

This is not an exhaustive set of commands. If you are not familiar with the unix command line, this will help you understand what the commands we are asking to use do throughout the day.

Some of these commands have optional or required arguments. You can find out more about any command using the `man COMMAND`. 

* man - Access the manual page about a command.
* pwd - present working directory. It gives you information about the current location on the file system.
* cd - change your current directory.
* ls - lists the files and directories in the current working directory
* mkdir - create a directory
* touch - 
* mv - can move a file into a directory, or rename a file/directory to a new name
* rm - remove files and directories
* cp - copies files and directories.
* cat - concatenates and prints file to standard output

There is a tutorial available at [Linuxcommand.org](http://linuxcommand.org/).

## Introduction to Version Control

* [Background for Version Control](https://git-scm.com/book/en/v2/Getting-Started-About-Version-Control)

## Introduction to Git

* [git basics](https://git-scm.com/book/en/v2/Getting-Started-Git-Basics)
* [Windows or Mac git GUI client](https://www.sourcetreeapp.com/)

## Git configuration

* [More information about git configuration](https://git-scm.com/book/en/v2/Getting-Started-First-Time-Git-Setup)


## Set your preferred git editor

If you don't have a preferred editor, use nano. nano is an easy editor to get started with. The basic commands:

Open a file for editing
```
$ nano FILENAME
```

Save a file after editing
```
CTRL+x, "y", ENTER
```

Exit a file
```
CTRL+x
```

## Sharing updates to remote repository

Basic git commands: push, pull, fetch

* [Git Push](http://git-scm.com/docs/git-push)
* [Git Pull](http://git-scm.com/docs/git-pull)
* [Git Fetch](http://git-scm.com/docs/git-fetch)


