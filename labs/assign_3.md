# Setup a Chef Repository

## Have one person in your team create a repo called ed-lab3.

* Elect one person from your group to create a repo called `ed-lab3`. Follow the process from Lab 1 with one exception, don't create a readme.

## Grant privileges to the ed-lab3 repo to your team.

Follow the process from Lab 2 to grant access to your full team.

## Generate the chef repo.

In this exercise we are creating a monolithic chef-repo. The monolithic chef-repo will hold the global policy items as well as any cookbooks created in this workshop. Generally, when using with a Chef server you choose between one of two strategies. 

1. Monolithic Workflow - 1 chef-repo containing everything that maps to 1 repo in source control.
2. 1 cookbook per repo + policy only chef-repo. 

```
 cd ~/wd
 chef generate repo ed-lab3
 cd ~/wd/ed-lab3
 git init .
 git add .
 git commit -m "Initial creation of chef repo"
 save your changes and commit back to team's repo
 git remote add origin git@github.com:USERNAME/ed-lab3.git
 git push -u origin master
```

Example Output

```
[chef@ip-172-31-11-246 ed-lab3]$ git add .
[chef@ip-172-31-11-246 ed-lab3]$ git commit -m "initial creation of chef repo"
[master (root-commit) 763d4d8] initial creation of chef repo
 14 files changed, 316 insertions(+)
 create mode 100644 .gitignore
 create mode 100644 LICENSE
 create mode 100644 README.md
 create mode 100644 chefignore
 create mode 100644 cookbooks/README.md
 create mode 100644 cookbooks/example/attributes/default.rb
 create mode 100644 cookbooks/example/metadata.rb
 create mode 100644 cookbooks/example/recipes/default.rb
 create mode 100644 data_bags/README.md
 create mode 100644 data_bags/example/example_item.json
 create mode 100644 environments/README.md
 create mode 100644 environments/example.json
 create mode 100644 roles/README.md
 create mode 100644 roles/example.json
[chef@ip-172-31-11-246 ed-lab3]$ git remote add origin git@github.com:sparklydevops/ed-lab3.git
[chef@ip-172-31-11-246 ed-lab3]$ git push -u origin master
Counting objects: 24, done.
Compressing objects: 100% (20/20), done.
Writing objects: 100% (24/24), 5.71 KiB | 0 bytes/s, done.
Total 24 (delta 2), reused 0 (delta 0)
To git@github.com:sparklydevops/ed-lab3.git
 * [new branch]      master -> master
Branch master set up to track remote branch master from origin.

```

## Clone the ed-lab3 repo to your node

If you didn't generate the ed-lab3 chef-repo, clone your teams repo to your node. 




```
   cd ~/wd
   git clone git@github.com:USERNAME/ed-lab3.git
   cd ~/wd/ed-lab3
```


## Split your team up into pairs, max of 3 people per "pair"

* Driver - person working with keyboard
* Observer - person looking at the code 

Work with your team to plan your updates into the repo so that you can do the `git pull`, `git push` to sync your local repo to the to the remote repo as needed.

## Create application cookbook - Pair 1

The _driver_ will type out the commands. The _observer_ will verify for mistakes.

```
 cd ~/wd/ed-lab3/cookbooks
 chef generate cookbook app
 git add app
 git commit -m "creation of cookbook app"
 git push origin master
```

## Install Apache via a Recipe - Pair 1

The _driver_ and _observer_ should switch roles. The _driver_ will type out the commands. The _observer_ will verify for mistakes.


Generate the `install_apache` recipe in the `app` cookbook.

```
   chef generate recipe app install_apache
   nano app/recipes/install_apache.rb
```

Add the follow `resources` to the `install_apache` recipe.

```
package 'httpd'

service 'httpd' do
  action [ :enable, :start ]
end


Edit the default recipe:

```
   nano recipes/default.rb
```

This is a good practice of 
Update the contents of the `default.rb` recipe with the following contents:


```
include_recipe 'app::install_apache'

```

Update the `.kitchen.yml`. 

```
 cd ~/wd/ed-lab3/cookbooks/app
 nano .kitchen.yml
```

Update the `.kitchen.yml` configuration. 

* Change the driver name to _docker_.
* Delete the ubuntu platform
* Add driver_config configuration to allow forwarding to the container.

The contents of your .kitchen.yml should look as follows

```
---
driver:
  name: docker

provisioner:
  name: chef_zero

platforms:
  - name: centos-7.1
    driver_config:
      forward:
      - 80:80

suites:
  - name: default
    run_list:
      - recipe[app::default]
    attributes:

```


```
   kitchen converge 

```

How do you know if your recipe worked? Kitchen converge finishes without errors, and you have a port up and running. You can check by browsing directly to the node because you have set up port forwarding!


```
cd ~/wd/ed-lab3/cookbooks
git add app
git commit -m "install and configure apache"
git push origin master
```
 


## Install MySQL via a Recipe (1 per team)

### Create feature branch or use your branching strategy

* git checkout -b install_mysql

### Include mysql cookbook from supermarket

[Supermarket](https://supermarket.chef.io) is the Chef community site. Before using community cookbooks in your environment, always inspect the cookbook. You run the code with root privileges!

* open `~/wd/TEAM-repo/chef-repo/cookbooks/app/recipes/default.rb` in editor
* add `include_recipe 'app::mysql_service'`
* save file

#### Using mysql cookbook

We will use the mysql cookbook. The [mysql cookbook](https://github.com/chef-cookbooks/mysql) is a library cookbook, and contains no recipes. It only has resources that we can use that extend the available resources to manage. We will use the mysql_service resource. You can also read the examples in the [mysql cookbook README](https://github.com/chef-cookbooks/mysql) to understand how to use the other available mysql resources.

* open `~/wd/TEAM-repo/chef-repo/cookbooks/app/recipes/mysql_service.rb` in editor
* add  

```
mysql_service 'joengo' do
  port '3306'
  version '5.5'
  initial_root_password 'banana'
  action [:create, :start]
end
```

* open `app/metadata.rb` in editor
* add 

```
depends 'mysql', '~> 6.0'
```
* save `app/metadata.rb` file

#### Use kitchen and docker to test your recipe

* cd ~/wd/TEAM-repo/chef-repo/cookbooks/app
* Update ~/wd/TEAM-repo/chef-repo/cookbooks/app/.kitchen.yml
 * Change driver name from `vagrant` to `docker`
 * Remove the line `- name: ubuntu-12.04`
 * Update the centos-6.5 line to include driver_config to forward port 80

```
platforms:
  - name: centos-6.5
    driver_config:
      forward:
      - 80:80
```
 * Save the file
* kitchen converge (This will take a few minutes!)

#### If all is well, Save your work!

How do you know if your recipe worked? Kitchen converge finishes without errors, and you have a port up and running. You can check by browsing directly to the node because you have set up port forwarding!

 * cd ~/wd/TEAM-repo/chef-repo/cookbooks/
 * git add app
 * git commit -m "install and configure mysql"
 * save your changes and commit back to team's repo

## Verify your development environment is consistent (Everyone)

Depending on which part of the work you did, you should make sure that your node is working as expected.

* git pull origin master
* cd ~/wd/TEAM-repo/chef-repo/cookbooks/app
* update your .kitchen.yml to match as above
* kitchen converge
* kitchen login 
 * Password: kitchen

## Outcome 

You should have an updated TEAM-repo with

* updated docs/branch.md, skills.md
* chef-repo
* app cookbook

 

### (Optional) Include apache2 cookbook from supermarket

[Supermarket](https://supermarket.chef.io) is the Chef community site. Before using community cookbooks in your environment, always inspect the cookbook. You run the code with root privileges!

The Apache2 cookbook will allow you to set up virtual hosts. You could use this cookbook instead of the simple recipe we have made to install apache.

[Apache2 Cookbook](https://supermarket.chef.io/cookbooks/apache2)

* open `~/wd/TEAM-repo/chef-repo/cookbooks/app/recipes/default.rb` in editor
* add `include_recipe 'apache2'`
* save file
* open `~/wd/TEAM-repo/chef-repo/cookbooks/app/metadata.rb` in editor
* add `depends 'apache2'`
* save file

