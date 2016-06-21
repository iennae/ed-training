#  Scaling

## Adding complexity

Bump the metadata version information of your cookbook. 

Update the `.kitchen.yml` in our app cookbook. 

To platforms section, add 

  - name: ubuntu-16.04

Note: We are not mapping local port 80 as we've already done that. You could map another port locally, or just use kitchen login to verify the setup.

* Converge kitchen

* kitchen converge default-ubuntu-1604

Error seen:

```

           Chef::Exceptions::Package
           -------------------------
           httpd is a virtual package provided by multiple packages, you must explicitly select one
```

Packages on debian systems will be different than on other systems.

How can we solve this?

* One mechanism is attribute driven

In app cookbook, 

```
$ chef generate attribute default
$  vi attributes/default.rb
```

Add to the file

```
case node['platform']
when 'redhat', 'centos', 'scientific', 'fedora', 'oracle'
  default['app']['apache2'] = 'httpd'
when 'debian', 'ubuntu'
  default['app']['apache2'] = 'apache2'
else
  default['app']['apache2'] = 'httpd'
end
```

Update the install_apache.rb recipe.

```
package node['app']['apache2']

service node['app']['apache2'] do
  action [ :enable, :start ]
end
```

Repeat this process for the mongodb cookbook. Check the [installation guide](https://docs.mongodb.com/manual/tutorial/install-mongodb-on-ubuntu/) for mongodb to see what requirements there are.




