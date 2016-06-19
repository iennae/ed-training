
### chef generate


* [Creating your own Chef Cookbook Generator](https://www.chef.io/blog/2014/12/09/guest-post-creating-your-own-chef-cookbook-generator/)
* [Policyfiles](https://www.chef.io/blog/2014/10/02/chefdk-0-3-0-released-introducing-policyfiles/) - Older blog post. 


### Docker

[Docker Cheat sheet](https://github.com/wsargent/docker-cheat-sheet)

### (Optional) Translate a runbook for installing MongoDB into chef

#### Creation of MongoDB cookbook

```
 cd ~/wd/ed-lab3/cookbooks
 git pull origin master
 chef generate cookbook mongodb
 cd ~/wd/ed-lab3/cookbooks/mongodb
 ```

#### Update kitchen.yml to use centos 6.5, docker

#### Create template to hold the mongodb repo location

 ```
 chef generate template mongodb.repo
 ```

#### Commit cookbook to source control

 ```
 git add ~/wd/ed-lab3/cookbooks/mongodb
 git commit -m "creation of cookbook mongodb"
 git push origin master
```

#### Creation of install_mongo.rb recipe

Determine the package(s) needed.

#### Update default.rb to include install_mongo.rb recipe

#### Update mongodb.repo.erb template 

From [Mongo Installation guide](http://docs.mongodb.org/manual/tutorial/install-mongodb-on-red-hat/):

```
For the latest stable release of MongoDB
Use the following repository file:

[mongodb-org-3.0]
name=MongoDB Repository
baseurl=https://repo.mongodb.org/yum/redhat/$releasever/mongodb-org/3.0/x86_64/
gpgcheck=0
enabled=1
```

If you need further hints, you can check out this [working example](https://github.com/nathenharvey/install_mongo) of minimal requirements to install mongodb.

