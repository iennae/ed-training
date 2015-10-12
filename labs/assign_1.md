# Verify Local Environment

## Overview

In this exercise each participant configures and tests a local development environment.

## Connect to Node (Everyone)

* ssh chef@NODE 

If you don't have ssh available please downlowd an ssh client. For Windows, a good option is [putty](http://www.putty.org/).


## Introduction to Git

## Customize your workstation (Everyone)

```
   git config --global user.name "YOUR NAME"
   git config --global user.email "YOUR EMAIL ADDRESS"

```

Example: 

```
$ git config --global user.name "Jennifer Davis"
$ git config --global user.email "sparklydevops@gmail.com"
```

## Verify .gitconfig creation (Everyone)

```
   cat ~/.gitconfig
```

Example:

```
   cat ~/.gitconfig
[user]
   name = Jennifer Davis
   email = sparklydevops@gmail.com
```

## Set your preferred git editor (Everyone)

If you don't set your preferred editor, it will use the default text editor for the system.

* emacs
* nano
* vi/vim

```
   git config --global core.editor EDITORNAME
```

Example:
```
$ git config --global core.editor nano
```

## Verify the configuration (Everyone)

```
   git config --list
```

Example Output:

```
[chef@ip-172-31-11-246 hello_world]$ git config --list
user.name=Jennifer Davis
user.email=sparklydevops@gmail.com
core.editor=nano
core.repositoryformatversion=0
core.filemode=true
core.bare=false
```

## Create a project Directory (Everyone)

```
   mkdir wd
   cd wd
```

## Create initial project (Everyone)

```
   mkdir hello_world
   cd hello_world
   git init 
   git status
```

Expected Output
```
[chef@ip-172-31-11-246 hello_world]$ git status
On branch master

Initial commit

nothing to commit (create/copy files and use "git add" to track)
```

Create hello.txt file:

```
   echo "hello world" >> hello.txt
   git status
   git add hello.txt
   git status
   git commit -m "creation of hello.txt file"
   git status

```

Example of first status output:

```
 git status
On branch master

Initial commit

Untracked files:
  (use "git add <file>..." to include in what will be committed)

   hello.txt

nothing added to commit but untracked files present (use "git add" to track)
```

Example of second status output:

```
[chef@ip-172-31-11-246 hello_world]$ git status
On branch master

Initial commit

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)

   new file:   hello.txt
```

Example of third status output:

```
[chef@ip-172-31-11-246 hello_world]$ git status
On branch master
nothing to commit, working directory clean
```

## Create a GitHub identity (Everyone)

* If you don't already have a github account, create one.
* Browse to http://github.com. Supply a username, email address, and password.
* Free plan is fine. Other plans allow you to have private repositories.

## (Optional) Setting up your Github keys (Everyone)

If you want to skip the added burden of entering your username and password each time at the prompt with git, you can follow the steps here to set up your ssh keys:

https://help.github.com/articles/generating-ssh-keys/

Example output of successful setup of keys:

```
 [chef@ip-172-31-11-246 wd]$ ssh -T git@github.com
Hi sparklydevops! You've successfully authenticated, but GitHub does not provide shell access.
```



## Create a new remote repo

In a web browser, after logging into Github, you'll see an option to create a "New Repository" on the lower right.

Click on New Repository:

![Once logged in, click New repository](images/assign_1/1-click_new_repo.png "Once logged in, click New repository")

In the repository name field, enter `ed-lab1` and click the Initilize README option.: 

![In the Repository name field, ed-lab1](images/assign_1/2-name_ed-lab1.png "In the Repository name field, ed-lab1 ")
![Make sure to click the Initilize README](images/assign_1/3-init_with_readme.png "Make sure to click the Initilize README")

Once you have created the repo, you will see a screen like this:

![After clicking Create Repo](images/assign_1/4-after_create_repo.png "After clicking Create Repo")

On the lower right you will see the clone url. You can leave it with https and enter your credentials each time, or you can switch to ssh by clicking on SSH if you've set up your ssh keys.

![Click on SSH and grab the SSH clone url](images/assign_1/5-change_to_ssh_clone_url.png "Click on SSH and grab the SSH clone url")

## Clone new repo to node

On the node:

```
   cd ~/wd
   git clone git@github.com:YOURUSERNAME/ed-lab1.git
```

Example:
```
[chef@ip-172-31-11-246 wd]$ git clone git@github.com:sparklydevops/ed-lab1.git
Cloning into 'ed-lab1'...
remote: Counting objects: 3, done.
remote: Total 3 (delta 0), reused 0 (delta 0), pack-reused 0
Receiving objects: 100% (3/3), done.
Checking connectivity... done.
```

Check the contents of the repository you just cloned

```
  cd ~/wd/ed-lab1
  ls
  git remote -v
```

## Add hello.txt to your ed-lab1 repo

Copy the hello.txt file from the previous exercise into your ed-lab1 repository.

```
cp ~/wd/hello_world/hello.txt .
git status
git add hello.txt
git status
git commit -m "adding hello.txt to repository"
```

## Sharing updates to remote repository

At this point we have added the file to our local repository but not to our remote repository. 

```
git push origin master
```

Verify update to github, by reloading your repository

![Verify updates to github](images/assign_1/6-verify_updates_to_github.png "If you successfully pushed your change to github you should see a hello.txt file in your repository")


## Outcomes 

* git configured on your node
* ed-lab1 repo created on github, with local repo cloned
  
