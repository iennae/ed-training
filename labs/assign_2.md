# Adding Collaboration


## Have one person in your team create a repo called ed-lab2.

* Elect one person from your group to create a repo called ed-lab2. Follow the process from Lab 1.

## Grant privileges to the ed-lab2 repo to your team.

* Share your github identity with the team
* Click on the gear to access the Settings tab

![Click on the gear to access the Settings tab](images/assign_2/1-click_on_Settings.png "Click on Settings")

* Click on Collaborators

![Click on Collaborators](images/assign_2/2-click_on_Collaborators.png "Click on Collaborators")

* Add Collaborators based on github name

![Add Collaborators based on github name](images/assign_2/3-add_collaborators_from_team.png "Add Collaborators based on github name")

* If you have successfully added, they will show up as a Collaborator. 

![If you have successfully added, they will show up as a Collaborator](images/assign_2/4-confirm_collaborators.png "If you have successfully added, they will show up as a Collaborator")

## Clone the ed-lab2 repo to your node

Clone your teams repo to your node. Add a file to the repo with your firstname as the file name. 

```
   cd ~/wd
   git clone git@github.com:USERNAME/ed-lab2.git
   cd ~/wd/ed-lab2
   touch FIRSTNAME.txt
   git add FIRSTNAME.txt
   git commit -m "adding my first name"
```

## Sync the remote repo

Push your changes to the remote repository.

```
git push origin master
```

As individuals add their name to the repo, you will run into conflicts. This is due to your local repo not being up to date with the remote repo as your team makes changes. 

Example Merge Conflict output:

```
[chef@ip-172-31-11-246 ed-lab2]$ touch jennifer.txt
[chef@ip-172-31-11-246 ed-lab2]$ git add jennifer.txt
[chef@ip-172-31-11-246 ed-lab2]$ git commit -m "adding my first name"
[master 00a017a] adding my first name
 1 file changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 jennifer.txt
[chef@ip-172-31-11-246 ed-lab2]$ git push origin master
To git@github.com:sparklydevops/ed-lab2.git
 ! [rejected]        master -> master (fetch first)
error: failed to push some refs to 'git@github.com:sparklydevops/ed-lab2.git'
hint: Updates were rejected because the remote contains work that you do
hint: not have locally. This is usually caused by another repository pushing
hint: to the same ref. You may want to first integrate the remote changes
hint: (e.g., 'git pull ...') before pushing again.
hint: See the 'Note about fast-forwards' in 'git push --help' for details.
```

Work with your team to plan your updates into the repo so that you don't have to repeat this process multiple times. Do a `git pull` to sync your local repo to the to the remote repo.

```
git pull origin master
git push origin master
```

Example output:

```
Merge branch 'master' of github.com:sparklydevops/ed-lab2

# Please enter a commit message to explain why this merge is necessary,
# especially if it merges an updated upstream into a topic branch.
#
# Lines starting with '#' will be ignored, and an empty message aborts
# the commit.

[chef@ip-172-31-11-246 ed-lab2]$ git pull origin master
remote: Counting objects: 3, done.
remote: Compressing objects: 100% (2/2), done.
remote: Total 3 (delta 0), reused 3 (delta 0), pack-reused 0
Unpacking objects: 100% (3/3), done.
From github.com:sparklydevops/ed-lab2
 * branch            master     -> FETCH_HEAD
   8451292..0d5f3db  master     -> origin/master
Merge made by the 'recursive' strategy.
 jay.txt | 0
 1 file changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 jay.txt

 $ git push origin master
 Warning: Permanently added the RSA host key for IP address '192.30.252.129' to the list of known hosts.
 Counting objects: 4, done.
 Compressing objects: 100% (4/4), done.
 Writing objects: 100% (4/4), 591 bytes | 0 bytes/s, done.
 Total 4 (delta 0), reused 0 (delta 0)
 To git@github.com:sparklydevops/ed-lab2.git
    0d5f3db..fdde3d1  master -> master

```

## Outcomes 

* Creation of ed-lab2 repo
* Firstname.txt files created for each of your group within the ed-lab2 repo.
