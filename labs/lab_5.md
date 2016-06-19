# Translate our MongoDB cookbook from recipes into resources

## Custom Resources 12.5 Style 

* simple extension of Chef
* implemented as part of a cookbook
* follows easy, repeatable syntax patterns
* effectively leverages resources that are built into Chef
* is reusable in the same way as resources that are built into Chef

Defined as ruby file (.rb extension) located in cookbook's resources directory.

```
property :name, RubyType, default: 'value'

load_current_value do
  # some Ruby
end

action :name do
 # a mix of built-in Chef resources and Ruby
end

action :name do
 # a mix of built-in Chef resources and Ruby
end


```

In the following example, this resource would create a 
Example:

```
resource_name :httpd

property :homepage, String, default: '<h1>Hello world!</h1>'

load_current_value do
  if ::File.exist?('/var/www/html/index.html')
    homepage IO.read('/var/www/html/index.html')
  end
end

action :create do
  package 'httpd'

  service 'httpd' do
    action [:enable, :start]
  end

  file '/var/www/html/index.html' do
    content homepage
  end
end
```

Example of using this resource

```
httpd 'build website' do
  homepage '<h1>Welcome to the Example Co. website!</h1>'
  action :create
end

```

[Walk-through of creating custom resources.](https://docs.chef.io/decks/custom_resources.html)

## Outcome 

* custom resource file in resources directory of cookbook
* simplified recipe in cookbook