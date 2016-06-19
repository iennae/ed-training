
# Translate a runbook for installing MongoDB into chef

MongoDB is an open-source, document-oriented database designed for ease of development and scaling.  The MongoDB documentation site includes a [installation guide on how to install MongoDB on Red Hat Enterprise Linux, CentOS Linux, Fedora Linux, or a related system](http://docs.mongodb.org/manual/tutorial/install-mongodb-on-red-hat-centos-or-fedora-linux/). 

* [Chef Resource Documentation](https://docs.chef.io/resources.html)

Read the [installation guide](http://docs.mongodb.org/manual/tutorial/install-mongodb-on-red-hat-centos-or-fedora-linux/), identify the resources you need, and create a mongodb cookbook populated with an appropriate recipe. 

* What users do you need? What groups?
* What packages do you need?
* What configurations do you need?
* Where is data stored?
* What directories do you need to create?
* What services do you need?

Hints:

## Use the yum community cookbook

The yum community cookbook provides resource *yum_repository* that allows us to make individual yum repositories available for use. 

In the [installation guide](http://docs.mongodb.org/manual/tutorial/install-mongodb-on-red-hat-centos-or-fedora-linux/), we see that we need to configure a yum repo in order to install mongodb packages using yum. 


```
[mongodb-org-3.2]
name=MongoDB Repository
baseurl=https://repo.mongodb.org/yum/redhat/$releasever/mongodb-org/3.2/x86_64/
gpgcheck=1
enabled=1
gpgkey=https://www.mongodb.org/static/pgp/server-3.2.asc
```

translates to chef dsl as: 

```
    yum_repository 'mongodb-org-3.2' do
      description 'MongoDB Repository'
      baseurl 'https://repo.mongodb.org/yum/redhat/$releasever/mongodb-org/3.2/x86_64/'
      gpgcheck true
      gpgkey 'https://www.mongodb.org/static/pgp/server-3.2.asc'
      enabled true
      action :create
```

## Outcome 

* mongodb running on the node
* code checked into repository