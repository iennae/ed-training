# Maintainable Chef and Collaboration

## Overview

In this exercise, every team will update their cookbooks, and add tests for recipes. Generally when pairing, one person will write the test, and then the other person will write the code that repairs the test.


## Customize website via a Recipe 


### Write a failing test for content

Make sure you base your failing test based on the content you expect to see. 

Two different methods for testing, what's different between them and which do you choose to use to test?

Update `test/integration/default/serverspec/default_spec.rb`:

```ruby
describe file('/var/www/html/index.html') do
  it { should contain('Hello World')}
end
```

OR

Update `test/integration/default/serverspec/default_spec.rb`:

```ruby
describe command('curl -s http://localhost') do
  its(:stdout) { should_not contain('Centos') }
  its(:stdout) { should contain('Hello World') }
end
```

### Verify Test

```
kitchen converge
kitchen verify

```

### Write the Code

Update `app/recipes/default.rb` with

```ruby
file '/var/www/html/index.html' do
  content "<h1>Hello, World</h1>"
end
```


## Add tests for earlier features (1 per team)


### Identify what tests you should add for mysql and apache

Need help? [Serverspec docs](http://serverspec.org/) and [Examples from mysql cookbook](https://github.com/chef-cookbooks/mysql/tree/master/test/integration)

* Update `test/integration/default/serverspec/install_apache_spec.rb`:
* Update `test/integration/default/serverspec/mysql_service_spec.rb`:

### Verify Test


```
kitchen converge
kitchen verify

```


### Extra Credit: Replace file with template resource

Read up on the template resource on the [Chef Docs site](http://docs.chef.io/resources.html#template) if you don't remember what a template is.

Update `app/recipes/install_apache.rb` with

```ruby
template '/var/www/html/index.html' do
  .....
end
```

Requirements
* Create template with the _chef generate_ command
* Add template resource in _install_apache.rb_ recipe
* Update _app/metadata.rb_ with a new version.
* Commit your changes back to the repo.

