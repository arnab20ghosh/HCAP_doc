---
title: External Configuration
---

## External Configuration

This feature allows the framework to use json configuration files from an external source.
The external source is usually a GIT repository (referred as `pipeline-config` below). The framework automatically clones the repository (i.e. makes a local copy of the files in the repository) in the `external_config_dir`, which defaults to `target/pipeline-config`.  
The external configuration files are combined into specific configurations.

The default values for Packer build is present in the `build.json` file. 

Packer is is a tool for creating machine images for multiple platforms from a single source configuration. 
This single source is in the form of a template file in JSON format and in this case we use a `build.json` file. To learn more about Packer and JSON templates, see <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-devsecops', viewPage: 'learn-the-concept', viewSection: 'devops'})" style="text-decoration:none">Learn the Concepts</a>. 

> The `build.json` file contains much of the variables and configurations for the packer build of the AMI you are building. In the build.json file you will find builders (contains what type of AMI is being built), variables, provisioners (processes and software to run after server is up and running) and post-process (tasks for what should be done after the AMI is built). 

### Contents

- <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-devsecops', viewPage: 'external-configuration', viewSection: 'example'})" style="text-decoration:none">External variables in config.rb</a>
- <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-devsecops', viewPage: 'external-configuration', viewSection: 'external'})" style="text-decoration:none">External Configuration environment variables </a>
- <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-devsecops', viewPage: 'external-configuration', viewSection: 'what'})" style="text-decoration:none">What does external configuration do</a>
- <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-devsecops', viewPage: 'external-configuration', viewSection: 'how'})" style="text-decoration:none">How to disable external configuration</a>
- <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-devsecops', viewPage: 'external-configuration', viewSection: 'how-to'})" style="text-decoration:none">How to use external configuration</a>
- <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-devsecops', viewPage: 'external-configuration', viewSection: 'how-external'})" style="text-decoration:none">How external configuration is used in the pipeline builds</a>
- <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-devsecops', viewPage: 'external-configuration', viewSection: 'external-con'})" style="text-decoration:none">External configuration key</a>
- <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-devsecops', viewPage: 'external-configuration', viewSection: 'searching'})" style="text-decoration:none">Searching external configuration files</a>
- <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-devsecops', viewPage: 'external-configuration', viewSection: 'sample'})" style="text-decoration:none">Sample External Configuration</a>
- <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-devsecops', viewPage: 'external-configuration', viewSection: 'directory'})" style="text-decoration:none">External Configuration Directory Structure </a>
- <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-devsecops', viewPage: 'external-configuration', viewSection: 'JSON'})" style="text-decoration:none">External JSON files and config pull</a> 

The default values for Packer build is present in the `build.json` file.

### <a id="example" name="example"></a>Example of build.json

```
# code truncated for brevity
"builders": [
    {
      "ssh_bastion_host": "<Bastion_public_ip>",
      "ssh_bastion_private_key_file": "<path_of_SSH_key>",
      "ssh_bastion_username": "ec2-user",
...
```

### <a id="variables" name="variables"></a>Variables in config.rb
All external configuration parameters are defined in *config.rb* with variable names starting with **external_config**  

| Parameter               | Description                                                  | Required                    |
| ----------------------- | ------------------------------------------------------------ | --------------------------- |
| :external_config_url    | The URL of the external configuration source. It is used when `external_config_type` is not set to `:none`. | Yes                         |
| :external_config_ref    | The external configuration GIT branch                        | Must be set for GIT sources |
| :external_config_dir    | The external configuration directory                         | Yes                         |
| :external_config_prefix | The base configuration directory under `:external_config_dir`. If this parameter is not set, the base configuration directory is `:external_config_dir`. | No                          |
| :external_config_key    | Determine all possible directories to load configuration from the least specific to the most specific | No                          |
| :external_config_type   | External configuration type. Defaults to `:git` for AMIs     | No                          |

The GIT repository is pulled when the **config:pull** task is executed.

### <a id="external" name="external"></a>External Configuration environment variables

The framework will read certain external configuration values from environment variables

| Parameter            | Environment Variable | Default  |
| -------------------- | -------------------- | -------- |
| :external_config_url | PIPELINE_CONFIG_URL  |          |
| :external_config_ref | PIPELINE_CONFIG_REF  | `master` |

### <a id="what" name="what"></a>What does external configuration do

The framework pulls the external configuration files from GIT (where the git repository is :external_config_url and the branch is :external_config_ref ) to the :external_config_dir directory.  The framework can use the external configuration feature to pull configuration files for a given project (i.e. base rhel7 AMI) and for a given AWS region (i.e. us-east-1).  

### <a id="how" name="how"></a>How to disable external configuration

Set `:external_config_type` to `:none` and make sure `:external_config_dir` is not set.

### <a id="how-to" name="how-to"></a>How to use external configuration

To use this feature directly, call `external_config_files` or `external_config_file` in your configuration files.   

```ruby
# this call will return the list of all vars.json files from the least specific to the most specific
set :customer_app_var_files, -> { external_config_files('vars.json') }
```

### <a id="how-external" name="how-external"></a>How external configuration is used in the pipeline builds

This feature allows image and application pipelines to use pipeline configuration files from `pipeline-config` and in the 
case of packer AMI image pipelines the configuration file is the `vars.json` file. 

Below shows an example of a `vars.json` file specific to an AMI project

```json
{
  "source_ami": "ami-6871a115",
  "chefdk_version": "3.3.23-1",
  "chefdk_rpm": "chefdk-3.3.23-1.el7.x86_64.rpm",
  "nessus_agent_package_name": "NessusAgent",
  "nessus_agent_package_version": "6.11.1-es7",
  "mcafee_package_name": "mcafee-epo-agent",
  "mcafee_package_version": "4.8.0",
  "aws_cli_package_name": "awscli-bundle",
  "aws_cli_package_version": "20180913"
}
```
### <a id="external-con" name="external-con"></a>External configuration key

The external configuration key (`:external_config_key`) is automatically created based on the the application name.   
The key is constructed by splitting `:application` on `-`, reversing it, and joining it back with a new separator `/`.  

For instance if the :application name is `baseos-rhel7` then the external configuration key would be `rhel7/baseos` for the location.

Or using another example with the **:application** value below:

```ruby
set :application, 'customer-app123'  # :external_config_key is set to `app123/customer`
```

The key can be overridden by setting the value directly in the application's `config.rb`.  

The key determines the directories where the framework will look for external configuration files. 

### <a id="searching" name="searching"></a>Searching external configuration files

The search is driven by the external configuration key. The search determines all configuration files matching the given name from the least specific to the most specific.  
The least specific configuration files are located in the top level directory and the most specific configuration files are located in the lowest level directory.  

Let's say the base configuration directory is `pipeline-config` and the external configuration key is set to `customer/app123`.  
The framework will start searching in the `pipeline-config` directory, moving on to the `pipeline-config/app123`, and finishing the search in the `pipeline-config/customer/app123` directory.  

### <a id="sample" name="sample"></a>Sample External Configuration

```ruby
set :external_config_dir, target('pipeline-config')
set :external_config_url, 'git@github.com:customer123/rean-pipeline-config.git'
set :external_config_ref, 'branch456'
set :external_config_prefix, 'pipelines'
set :external_config_type, :git
set :external_config_key, 'customerapp/jenkins'
```

This external configuration will cause the framework to get the external configuration files from the GIT branch 'branch456' and the GIT repository at 'git@github.com:customer123/rean-pipeline-config.git' into a directory under `./target/pipeline-config`.

### <a id="directory" name="directory"></a>External Configuration Directory Structure

Let's look at the example of `pipeline-config` directory structure.

```sh
  pipeline-config/
    ├── amis   #:external_config_prefix
    │   ├── core_account.json
    │   ├── rhel7
    │   │   ├── artifactory #:external_config_key - 'rhel7/baseos'
    │   │   │   ├── audit #:audit_dir
    │   │   │   │   ├── filter.yml
    │   │   │   │   ├── inspec_attributes.yml #values for inspec attributes
    │   │   │   │   ├── poam.yml #Rules that should be skipped for a approved period of timeframe, reasons, request and approval
    │   │   │   │   └── skip.yml #Rules that should be skipped, reasons, request and approval
    │   │   │   ├── inspec_attributes.yml
    │   │   │   └── vars.json #packer vars for packer build task
    │   │   ├── baseos #:external_config_key - 'rhel7/baseos'
    │   │   │   ├── audit #:audit_dir
    │   │   │   │   ├── filter.yml
    │   │   │   │   ├── inspec_attributes.yml
    │   │   │   │   ├── poam.yml
    │   │   │   │   └── skip.yml
    │   │   │   └── vars.json #packer vars for packer build task
    │   │   ├── dockerhost
    │   │   │   ├── audit #:audit_dir
    │   │   │   │   ├── filter.yml
    │   │   │   │   ├── inspec_attributes.yml
    │   │   │   │   ├── poam.yml
    │   │   │   │   └── skip.yml
    │   │   │   └── vars.json #packer vars for packer build task
    │   │   ├── inspec_attributes.yml
    │   │   └── vars.json
    │   ├── vars.json #packer vars for packer build task
    │   ├── win2012r2
    │   │   ├── baseos ##:external_config_key - 'win2012r2/baseos'
    │   │   │   └── vars.json
    │   │   └── reantestclient ##:external_config_key - 'win2012r2/reantestclient'
    │   │       ├── inspec_attributes.yml
    │   │       ├── selenium
    │   │       │   ├── inspec_attributes.yml
    │   │       │   └── vars.json
    │   │       ├── testcomplete
    │   │       │   ├── inspec_attributes.yml
    │   │       │   └── vars.json
    │   │       ├── uft
    │   │       │   ├── inspec_attributes.yml
    │   │       │   └── vars.json
    │   │       └── vars.json
    │   └── workload_accounts.json
    ├── docker-images #:external_config_prefix
    │   └── rhel7
    │       ├── baseos #:external_config_key - 'rhel7/baseos'
    │       │   ├── audit #:audit_dir
    │       │   │   ├── filter.yml
    │       │   │   ├── inspec_attributes.yml
    │       │   │   ├── poam.yml
    │       │   │   └── skip.yml
    │       │   └── vars.json # vars for docker build task
    │       ├── bootstrap #:external_config_key - 'rhel7/bootstrap'
    │       │   ├── audit #:audit_dir
    │       │   │   ├── filter.yml
    │       │   │   ├── poam.yml
    │       │   │   └── skip.yml
    │       │   └── vars.json
    │       │ 
    │       ├── stigtool_inspec_attributes.yml
    │       └── tomcat
    │           ├── audit
    │           │   ├── filter.yml
    │           │   ├── inspec_attributes.yml
    │           │   ├── poam.yml
    │           │   └── skip.yml
    │           ├── inspec_attributes.yml
    │           └── vars.json
    └── pipelines #:external_config_prefix
        └── reanplatform
            └── bootstrap #:external_config_key - 'reanplatform/bootstrap'
                └── customer.yml
```

In the directory structure above, you may have noticed the file `workload_accounts.json`. 

**Workload accounts** are where tasks and builds can happen; however the deployment would take place using the core account.

 For AMIs and Docker Images the vars.json at the root folder i.e, the order in which a variable will be taken for 'baseos-rhel7' is
 1. ami/rhel7/baseos/vars.json
 2. ami/rhel7/vars.json

 The framework supports cloud provider and region specific vars. The variable `:aws_region` must be set in `config.rb`. In this example, the cloud provider is `aws`. 
  - ami/rhel7/vars.json
  - ami/rhel7/baseos/vars.json
  - ami/rhel7/baseos/aws.vars.json
  - ami/rhel7/baseos/aws.us-east-1.vars.json
  - ami/rhel7/baseos/aws.us-gov-west1.vars.json
  - ami/rhel7/baseos/aws.us-west2.vars.json

 If `:aws_region` or `AWS_REGION`  or `AWS_DEFAULT_REGION` is 'us-east-1', the order of preference is taken as :
 1. ami/rhel7/baseos/aws.us-east-1.vars.json
 2. ami/rhel7/baseos/aws.vars.json
 3. ami/rhel7/baseos/vars.json
 4. ami/rhel7/vars.json

 If the same variable is declared in all four files, the value in the most specific file (in the first file) will be used.

### <a id="JSON" name="JSON"></a>External JSON files and config pull

Extra variable files get passed to the AMI Packer build (in addition to the build.json) in the ***following order***, 
with each subsequent file overriding variables of the same name or adding new variables-

#### **Loaded First:**
> target/pipeline-config/amis/rhel7/baseos/vars-final.json: The relevant JSON files from the external pipeline configuration(target/pipeline-config/amis ) are combined into a vars-final.json file.

*the vars-final.json is created by the **`bundle exec rake config:pull`** command and pulls down json files from the remote repository based upon the `:application` name*

#### **Loaded Second:** 
> vars.json: local vars.json file for packer build

#### **Loaded Third:**
> target/image-inputs.json: contains data generated from config.rb, environment variables, etc.

#### Example for variable precedence
An example of this would be if the `config.rb` file had a configuration value set for `"aws_region"` as `"us-east-1"` and the `vars.json` file in the `pipeline-config/amis` had `"aws_region"` as a value of `"us-gov-west-1"`. 

The value set in `config.rb` for `"aws_region"` would override/replace the value set in the JSON file of the `pipeline-config/amis` because this would be loaded afterwards.

> The **key point** is here is the external `pipeline-config` repository is a central location for common configuration values of different AMI types. 
And these values can be overridden or added to **locally** when configuring the pipeline and only pulling down the values pertaining to the specific AMI based upon the :application value. 

## Related Topics

<a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-devsecops', viewPage: 'configure-projects', viewSection: 'con-pro'})" style="text-decoration:none">Configure Projects</a>