# Maintainable Chef

## Linting 

```
cd ~/wd/ed-lab3/cookbooks
```

Run _foodcritic_, chef linting tool 

```
foodcritic app
```

Run _rubocop_, ruby linting tool

```
rubocop app
```


```
rubocop app
Inspecting 11 files
CCC.C......


```

### Add exclusions to Rubocop config file 

Update `.rubocop.yml` to ignore the Style/SingleSpaceBeforeFirstArg violation :

```
nano .rubocop.yml
```


```
Style/SingleSpaceBeforeFirstArg:
    Enabled: false

```

```
rubocop app
```

Check the available cops.

```
rubocop --show-cops
```

Based on the errors, determine which cops you want to ignore, or fix. 

## Integration Tests 

Modify the contents of test/integration/default/serverspec/default_spec.rb

```
cd ~/wd/ed-lab3/cookbooks/app
nano test/integration/default/serverspec/install_apache_spec.rb
```



Add contents to file `test/integration/default/serverspec/install_apache_spec.rb`:

```
require 'spec_helper'

describe 'app::default' do
  it "httpd service is running" do
   expect(service 'httpd').to be_running
 end
end
```

Run the integration test

```
kitchen verify
```


Expected Output:

```
[chef@ip-172-31-11-246 app]$ kitchen verify
-----> Starting Kitchen (v1.4.2)
-----> Using experimental policyfile mode for chef-client
$$$$$$ The Policyfile feature is under active development.
$$$$$$ For best results, always use the latest chef-client version
-----> Verifying <default-centos-65>...
$$$$$$ Running legacy verify for 'Docker' Driver
       Preparing files for transfer
       Removing /tmp/verifier/suites/serverspec
       Transferring files to <default-centos-65>
-----> Running serverspec test suite
       /opt/chef/embedded/bin/ruby -I/tmp/verifier/suites/serverspec -I/tmp/verifier/gems/gems/rspec-support-3.3.0/lib:/tmp/verifier/gems/gems/rspec-core-3.3.2/lib /opt/chef/embedded/bin/rspec --pattern /tmp/verifier/suites/serverspec/\*\*/\*_spec.rb --color --format documentation --default-path /tmp/verifier/suites/serverspec

       app::default
         does something (PENDING: Replace this with meaningful tests)

       app::default
         httpd service is running

       Pending: (Failures listed here are expected and do not affect your suite's status)

         1) app::default does something
            # Replace this with meaningful tests
            # /tmp/verifier/suites/serverspec/default_spec.rb:6


       Finished in 0.24267 seconds (files took 0.73668 seconds to load)
       2 examples, 0 failures, 1 pending

       Finished verifying <default-centos-65> (0m2.69s).
-----> Kitchen is finished. (0m5.10s)

```

