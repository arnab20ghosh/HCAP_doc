---
title: Configure Projects
---
# <a id="con-pro" name="con-pro"></a>Configure Projects

#### Contents

- <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-devsecops', viewPage: 'configure-projects', viewSection: 'working'})" style="text-decoration:none">Working with config.rb</a>
  - <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-devsecops', viewPage: 'configure-projects', viewSection: 'variable'})" style="text-decoration:none">Variables in config.rb</a>
  - <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-devsecops', viewPage: 'configure-projects', viewSection: 'config-value'})" style="text-decoration:none">Configuring Values for Variables in the config.rb file</a>
  - <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-devsecops', viewPage: 'configure-projects', viewSection: 'purpose'})" style="text-decoration:none">Purpose of image_build_vars, image_build, and var_files with build.json</a>
  - <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-devsecops', viewPage: 'configure-projects', viewSection: 'example'})" style="text-decoration:none">Example of config.rb for an AMI project</a>
- <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-devsecops', viewPage: 'configure-projects', viewSection: 'inspec-terr'})" style="text-decoration:none">InSpec, Terraform and Compliance testing settings</a>
  - <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-devsecops', viewPage: 'configure-projects', viewSection: 'test-inspec'})" style="text-decoration:none">Testing with InSpec</a>
  - <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-devsecops', viewPage: 'configure-projects', viewSection: 'test-terr'})" style="text-decoration:none">Testing with Terraform</a>

## <a id="working" name="working"></a>Working with config.rb

The configuration of a local image build is done in the `config.rb` file. This file is available in the projects root directory. In the `config.rb` file, you can set various mandatory project variables, and also provide custom values relevant for the image build.  


### <a id="variable" name="variable"></a>Variables in config.rb

These values in the table below relevant only for AMI (image/packer) projects. 

| Variable            | Usage                                                        | Required | Default Value                   |
| ------------------- | ------------------------------------------------------------ | -------- | ------------------------------- |
| :application        | The application name                                         | yes      | name from project generator cli |
| :application_type   | The application_type sets what type of the project you are creating | yes      | 'ami'                           |
| :compliance_tool    | Tool to be used for compliance scanning                      | yes      | :stigtool                       |
| :compliance_options | Options that can be passed into the compliance tool          | no       | {}                              |
| :stigtool_options   | Options that be be passed into the stigtool                  | no       | {}                              |

### <a id="config-value" name="config-value"></a>Configuring Values for Variables in the config.rb file

#### About set method

In the **config.rb** file, variables are configured using the `set` method, which adds the key-value pair to the hash of globally defined values. 

The format for using the `set` method is `set :variable_symbol_name, 'value'`.

> For additional information on using the `set` method, in the Customizing project topic, see the Adding Configuration Settings.
>

#### Using Lambdas and function blocks with the set method

The set method can also use Ruby lambdas and blocks for values. 
Using this is equivalent to an anonymous function or closure similar to other languages.

Similar to any method in Ruby, the set method does not need a declared `return` statement and the lambda method will return the last line of the function block.

Following is an example of using a Lambda:

```ruby
set :image_build_vars, lambda {
  vars = fetch(:default_image_build_vars)
  vars[:source_ami] = ENV['SOURCE_AMI'] if ENV['SOURCE_AMI']
  vars[:build_url] = ENV['BUILD_URL'] if ENV['BUILD_URL']
  vars[:ca_cert_bundle] = target('ca-certs.tar')
  vars
}
```

In the code example above, the lambda provides a useful method to set the aggregated vars array 
(last line returned) to the global hash key of `:image_build_vars`.

In Ruby, you can also set a `:symbol` hash value using the shorter stabby lambda syntax as in the example below:

```ruby
set :image_build_var_files, -> {
  fetch(:default_image_build_var_files)
}
```

### <a id="purpose" name="purpose"></a>Purpose of image_build_vars, image_build, and var_files with build.json

#### build.json and vars.json
Any of the variables defined in `build.json` under variables key can be overridden by the local `vars.json`. 
Furthermore, any variables set in the `config.rb` file will override the `vars.json` values of the same variable name.

#### image_build_vars and image_build_var_files

Additionally, `:image_build_vars` can be set to add additional values in addition to the build.json variables from the `config.rb`.
`:image_build_var_files` fetches the various image files where the configuration values are stored. 

Examples of the `:image_build_vars` and `:image_build_var_files` are shown in the example `config.rb` file below. 

### <a id="example" name="example"></a>Example of config.rb for an AMI project

```ruby
set :application, 'baseos-rhel7'

# Using defaults to set :image_build_var_files, adding :source_ami and :build_url
set :image_build_vars, lambda {
  vars = fetch(:default_image_build_vars) # this default value is set by the framework
  vars[:source_ami] = ENV['SOURCE_AMI'] if ENV['SOURCE_AMI']
  vars[:build_url] = ENV['BUILD_URL'] if ENV['BUILD_URL']
  vars
}

# Using defaults to set :image_build_var_files
set :image_build_var_files, lambda {
  fetch(:default_image_build_var_files) # this default value is set by the framework
}
```
## <a id="inspec-terr" name="inspec-terr"></a>InSpec, Terraform and Compliance testing settings

### <a id="test-inspec" name="test-inspec"></a>Testing with Inspec

InSpec is a free and open-source framework for testing and auditing applications and infrastructure. 
To learn more about InSpec, in the Learn the Concepts section, see <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-devsecops', viewPage: 'learn-the-concept', viewSection: 'inspec'})" style="text-decoration:none">Testing with Terraform and Inspec</a>.

#### <a id="step" name="step"></a>InSpec server testing

InSpec uses test and compliance **profiles**, which organize controls to support dependency management and code reuse. 
Each profile is a standalone structure with its own distribution and execution flows.

InSpec uses the testing profile which are located in the `inspec.yml` file. A testing profile should be defined under the `test` directory under the `:application` name sub-folder (by default). The sub-folder can be overwritten by setting `:test_suite` (see below).

An example **inspec.yml** file is shown below--also note only the `name` value is required at a minimum to be set in profiles.

```yaml
name: REAN-baseos-RHEL7
title: InSpec Profile for REAN RHEL7
maintainer: John Doe
copyright: REAN Cloud
copyright_email: john.doe@hitachivantara.com
license: All Rights Reserved
summary: An InSpec Compliance Profile
version: 0.1.3
supports:
  - os-family: redhat
```

Individual **local InSpec tests** can then be added under the `controls` sub-folder that resides under the `:application` name sub-folder. 

When InSpec profiles are used for server testing, we can customize the sub-folder by setting `:test_suite` to the directory with the InSpec profile.

If `:test_suite` is not set, it defaults to `:application` for the subfolder under test as noted above.

```ruby
# in this example, we should have our InSpec profile in "test/my-inspec-profile"
set :test_suite, 'my-inspec-profile'
```

The InSpec executions generate HTML, JSON, and XML reports in `target/reports/*<test_profile>*/`.

The file names are `validation.html`, `validation.json`, `validatiion.xml`, and `validatiion.txt`.

#### <a id="step" name="step"></a>InSpec options

InSpec `attributes` can be overridden by `<server_name>_inspec_attributes` and `<server_name>_inspec_attributes_files`.

In the example below, `:my_server_name` is a name of a defined server, this of course would be named as the server name you are testing.

To see how to create servers with servers names, please see the documentation on <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-devsecops', viewPage: 'customizing-projects', viewSection: 'server'})" style="text-decoration:none">Adding server and website objects</a>

```ruby
    #config.rb
    set :my_server_name_inspec_attributes_files, 'test/my_server_name/inspec_attributes.yml'

    set :my_server_name_inspec_attributes, -> {
      {
        {
          "attr1" : 'attr1Value',
          "attr2" : 'attr2Value'
        }
      }

    }
```
-----
### <a id="test-terr" name="test-terr"></a>Testing with Terraform 

A `test.tf` is automatically added to the AMI project and this file is used by Terraform to create a temporary infrastructure (servers) for testing.

#### Compliance testing settings

Compliance scanning is supported via InSpec profiles in the `audit` folder. Within this audit folder is a sub-folder based upon the value of the `:application` key. The InSpec profile verifies the STIG rules. 

With compliance scanning, the scans are run against STIGS (Security Technical Implementation Guides) which are basically security protocol rules. 

For more information on STIGS as well as POAM, Skip and Filter exclusions, see the <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-devsecops', viewPage: 'learn-the-concept', viewSection: 'security'})" style="text-decoration:none">Security and Compliance</a> section in the Learn the Concepts .

When running compliance scanning using the stigtool one can write `skip.yml`, `poam.yml` and `inspec_attributes.yml`; these files are pulled in via external configuration dependent on the project `:application` name. 

**An example InSpec profile for the audit folder is shown below.**

```yaml
name: REAN-baseos-RHEL7
title: Compliance Audit for REAN RHEL7
maintainer: John Doe
copyright: REAN Cloud
copyright_email: john.doe@hitachivantara.com
license: All Rights Reserved
summary: An InSpec Compliance Profile
version: 0.1.0
inspec_version:
  - "> 3.6.6"
  - "< 4.0"
supports:
  - os-family: redhat
depends:
- name: RHEL_7_STIG
  url: <artifactory_url>
  username: <artifactory_username>
  password: <artifactory_password>

```
> As you can see the `depends` section references the name of the STIG which to be downloaded from artifactory which is RHEL_7_STIG


##### Directory of the audit folder
```tree
├── audit
│   └── baseos-rhel7
│       ├── controls
│       │   └── RHEL_7_STIG.rb
│       ├── inspec.lock
│       └── inspec.yml

```

As you can see above, within the `controls` sub-folder under the application named sub-folder which is under the `audit` directory, is where the STIG files are to run with the same name(s) present within the depends block from the inspec profile. 

Hence from the inspec profile example above, there should be a file in the `controls` folder named `RHEL_7_STIG.rb`

Inside of this `RHEL_7_STIG.rb` file the code would look as below:

```ruby
include_controls 'RHEL_7_STIG' do
end
```

The above **include_controls** method calls the STIG downloaded from artifactory to execute and run the compliance scans. 

> However, the question might be 'what if we don't want to run certain security protocol rules to be scanned for various reasons?' This is where POAMs and Skips are used. 

#### POAM and Skip options

##### POAMs

A **POAM** is a *temporary* exclusion for an InSpec test. 

A POAM will have an expiration date and once that date passes; the compliance test will fail. 

An example of a POAM exclusion in a `POAM.yml` file is shown below:

```yaml
- benchmark: RHEL_7_STIG
  cookbook: STIG-RHEL-7
  profile: STIG-RHEL-7
  rules:
    RHEL-07-010500:
      reason: "We need a test environment, and LDAP server, and physical smart cards in order to implement and test this feature."
      requested_by: john.doe@hitachivantara.com
      requested_on: 2019-07-15 16:47:56
      approved_by:
      approved_on:
      days_allowed: 180
```

> Notice above the `RHEL-07-010500` is the specific name of the STIG rule to be excluded. The POAM also references the profile name.

----

##### Skip

InSpec also supports skipping tests entirely with a **Skip**. Unlike POAMs, Skips have no expiration date for the particular rule to be excluded. 

An example of a Skip rule in an `aws.<region>.skip.yml` is shown below:

```yaml
- benchmark: RHEL_7_STIG
  cookbook: STIG-RHEL-7
  profile: STIG-RHEL-7
  rules:
    RHEL-07-010480:
      reason: "AWS EC2 does not allow booting into single-user or maintenance mode, and does not expose the BIOS to the virtual machine."
      status: notapplicable
      requested_by: john.doe@hitachivantara.com
      requested_on: 2018-02-19 16:47:56
      approved_by:
      approved_on:
```

> Notice this is a similar structure to the POAM with the name of the STIG to be skipped under the rules block; however a major difference is the naming of the skip file. Skip files can include the aws region; **meaning skip rule exclusions can be written for specific regions**. 
