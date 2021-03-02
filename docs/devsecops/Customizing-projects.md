---
title: Customize Projects
---

# <a id="cust" name="cust"></a>Customize projects

Customize the projects by modifying `config.rb` and adding new rake tasks.

`config.rb` is automatically loaded by the framework. It is the best option for loading your configuration files and set up your custom variables.  

In the example below, the following variables are defined:`:application`, `:application_type`, `::custom_var`, and `:source_ami`. 

```ruby
# config.rb

# Set the application name.
set :application, 'custom-ami-123'

# Set the application type to AMI.
set :application_type, :ami

# Set the custom variable
set :custom_var, '12345'

# Set the source AMI. This AWS AMI will be used to build the custom AMI.
# This code block will
#   read the 'SOURCE_IMAGE_FILE' environment variable to get the file name
#   read the JSON file returning the 'ami_id' value
set :source_ami, lambda {
  ENV.fetch('SOURCE_IMAGE') do
    ami_file = ENV.fetch('SOURCE_IMAGE_FILE') { raise 'Either SOURCE_IMAGE or SOURCE_IMAGE_FILE env var must be set!' }
    read_json(ami_file)['ami_id']
  end
}
```

#### Contents

- <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-devsecops', viewPage: 'customizing-projects', viewSection: 'Add'})" style="text-decoration:none">Adding configuration settings </a>
- <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-devsecops', viewPage: 'customizing-projects', viewSection: 'Reading'})" style="text-decoration:none">Read JSON and YAML files</a>
- <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-devsecops', viewPage: 'customizing-projects', viewSection: 'Initializing'})" style="text-decoration:none">Initializing AWS clients </a>
- <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-devsecops', viewPage: 'customizing-projects', viewSection: 'server'})" style="text-decoration:none">Adding server and website objects</a>
- <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-devsecops', viewPage: 'customizing-projects', viewSection: 'Uploading'})" style="text-decoration:none">Uploading files </a>
- <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-devsecops', viewPage: 'customizing-projects', viewSection: 'rake'})" style="text-decoration:none">Using Rake Tasks</a>
- <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-devsecops', viewPage: 'customizing-projects', viewSection: 'hook'})" style="text-decoration:none">Adding before and after hooks</a>

## <a id="Add" name="Add"></a>Adding configuration settings

The framework stores current configuration in the global configuration hash.  It includes internally provisioned configuration values and values provisioned directly with setters. 

The global configuration hash should be accessed only via the helper methods.  

- `fetch(key, default=nil)`
  - Retrieves the value from the hash of globally defined values. If the key is not found, it will return the default value.  
- `set(key, value)` 
  - Adds the key-value pair to the hash of globally defined values.
- `set_if_empty(key, value)`
  - Adds the key-value pair to the globally defined values only if the key is not configured.   

### <a id="Setters" name="Setters"></a>Setters

The framework provides the following methods for setting configuration values.  

- `set`
- `set_if_empty`

Let's look at the `set` example:  

```ruby
# Sets :application to `not-my-application`
set :application, 'not-my-application'

# Sets :application to `my-application`, the older value is overwritten
set :application, 'my-application'
```

Let's look at the `set_if_empty` example:  

```ruby
# Sets :application to `my-application`
set :application, 'my-application'

# This set command has no effect because :application is already set
set_if_empty :application, 'the-greatest-application-ever-created'
```

### <a id="Getters" name="Getters"></a>Getters

The framework provides the following methods for getting the configuration values.  

```ruby
# In this example, we are retrieving the `:application` value
application =  fetch(:application)
```

## <a id="Reading" name="Reading"></a>Reading JSON and YAML files

JSON and YAML files are very popular ways of storing configuration and data.

The framework supports reading files in JSON and YAML formats. 

### <a id="Read" name="Read"></a>Read JSON files

The method `read_json` is used for reading JSON files.

`read_json(path)` 
    Returns the JSON file content, if the file exists
    Returns nil, if the file doesn't exits

```ruby
# if this example, we are reading the content of 'target/infra-core-bucket.json'
# and we are looking for the 'platform_bucket' element
config_bucket = read_json(target("infra-core-bucket.json"))['platform_bucket']
```

### <a id="YAML" name="YAML"></a>Read YAML files

The method `read_yaml` is used for reading YAML files.

`read_yaml(path)` 
    Returns the YAML file content, if the file exists
    Returns nil, if the file doesn't exits

```ruby
# if this example, we are reading the content of 'config/customer.yml'
customer = read_yaml('config/customer.yml')
```

## <a id="Initializing" name="Initializing"></a>Initializing AWS clients

The framework supports connections to multiple AWS accounts/regions at the same time by means of named AWS clients. 

AWS connections will always use the credentials that were used at the initialization time.  

If the credentials haven't been set, the AWS clients will use the credentials loaded from:  
  - AWS environment variables
  - AWS instance profile
  - `AWS_PROFILE` environment variable 
  - AWS profile

If the AWS region haven't been set, the AWS clients will use the default AWS region:  
  -  `AWS_REGION` environment variable
  -  `AWS_DEFAULT_REGION` environment variable
  -  The region associated with the AWS profile

The framework supports four methods of AWS client initialization: S3 Client, AWS Client, AWS Client Advanced, and Generic Cloud Client.

### <a id="S3" name="S3"></a>S3 Client

`s3_client` is a very simple method with a single argument. 
This method uses the default AWS credentials.

The parameter value for the `s3_client` is:

* **region:** [String] AWS Region. Defaults to nil.

```ruby
# In this example, we call the `s3_client` method to get an AWS S3 client in the 'us-east-1' region. 
s3_client = s3_client('us-east-1')
```

### <a id="AWS" name="AWS"></a>AWS Client

`aws_client` method creates an AWS client for the specific AWS API. 
This method uses the default AWS credentials.

The parameter values for the `aws_client` are:

* **api:** [String] AWS API
* **region:** [String] AWS Region. Defaults to nil.

```ruby
# In this example, we call the `aws_client` method to get an AWS S3 client in the 'us-east-1' region. 
s3_client = aws_client(:S3, 'us-east-1')
```

### <a id="Advanced" name="Advanced"></a>AWS Client Advanced

`aws_client_advanced` method creates an AWS client for the specific AWS API. 
This methods gives an option to use named clients allowing connections to multiple regions.
This method uses the default AWS credentials.

The parameter values for `aws_client_advanced` are:

* **name:** [String] client name. Defaults to :default.
* **client_type:** [Symbol] AWS API
* **region:** [String] AWS Region. Defaults to nil.

```ruby
# In this example, we call `aws_client_advanced` to get named AWS EC2 clients for calls to EC2 services in `us-east-1` and `us-west-1`.

ec2_useast1 = ::PipelineTasks::Dsl::CloudHelper.aws_client_advanced(name: :useast1, client_type: :EC2, region: 'us-east-1')

ec2_uswest1 = ::PipelineTasks::Dsl::CloudHelper.aws_client_advanced(name: :uswest1, client_type: :EC2, region: 'us-west-1')
```

### <a id="Generic" name="Generic"></a>Generic Cloud Client

The generic cloud client or `cloud_client` is called to create AWS or Azure cloud clients.  
This methods allows connections to multiple AWS regions using named clients and connections using multiple AWS accounts with the help of AWS profiles.

The basic parameter values passed into the `cloud_client` for AWS connections are:

* **client_type:** [Symbol] client API type (:EC2, :AutoScaling, :S3, etc.)
* **name:** [Symbol] client name, defaults to :default
* **provider**: [Symbol] cloud provider, :aws or :azure. Defaults to AWS.
* **region**: [String] AWS region 
* **aws_profile**: [String] Named AWS profile (in the config/credentials files)

```ruby
# In this example, we call the `cloud_client` method to get an AWS EC2 client in the default AWS region. 
ec2_client = ::PipelineTasks::Dsl::CloudHelper.cloud_client(client_type: :EC2)

# In this example, we call the `cloud_client` method to get an AWS EC2 client in the us-east-1 AWS region using the 'abc' profile
ec2_client = ::PipelineTasks::Dsl::CloudHelper.cloud_client(client_type: :EC2, region: 'us-east-1', aws_profile: 'abc')
```

## <a id="server" name="server"></a>Adding server and website objects

### <a id="About" name="About"></a>About servers

`server` is a Ruby object defining a logical server. The object contains all information necessary to connect to the underlying server.

#### <a id="Using" name="Using"></a>Using *server*

The ***server*** creation requires a name and a variety of options depending on the configuration details.

* **name:** [String/Symbol] server name
* **protocol**: [String] server protocol (winrm, winrms, wsman, wsmans, ssh, docker, local)
* **host**: [String] server host name or IP address
* **port**: [Integer/String] server port
* **user**: [String] server user name
* **password**: [String] server password. Either password or SSH keys is required.
* **keys**: [String] file path to the SSH key. Either password or SSH keys is required.
* **bastion_user**: [String] bastion user name. all bastion options are optional.
* **bastion_host**: [String] bastion host name or IP address. all bastion options are optional.
* **bastion_port**: [String] bastion port. all bastion options are optional.
* **test_profile**: [String] test profile. This is used for inspec tests. The value must be set if server_test_tool is :inspec.
  
```ruby
    # in this example, we are defining 'server_no_bastion'
    server 'server_no_bastion',
      protocol: "ssh",
      user: "ec2-user",
      port: 22,
      host: '1.1.1.1',
      keys: 'sshkey' 

    # in this example, we are defining 'server_with_bastion'
    server 'server_with_bastion',
      protocol: "ssh",
      user: "ec2-user",
      port: 22,
      host: '1.1.1.1',
      keys: 'sshkey',
      bastion_user: "ec2-user",
      bastion_host: '1.1.1.2',
      bastion_port: 22,
      test_profile: 'test'

    # in this example, we are defining 'server_efg' that is using server 'bastion_123'
    server 'bastion_123',
      protocol: 'ssh',
      user: 'ec2-user',
      port: 22,
      keys: 'ssh_key_path'

    server 'server_efg',
      protocol: "ssh",
      user: "ec2-user",
      port: 22,
      host: '1.1.1.1',
      keys: 'sshkey',
      bastion: 'bastion123'
      test_profile: 'test'
```

#### <a id="server_source" name="server_source"></a>Using *server_source*

The ***server*** creation requires a name, a provider, and a resource_type and a variety of properties depending on the configuration details.

If the resource type is `aws_instance`, the server name should be set to the value of either `tag:Name` or `instance_id` to allow the host to be fetched automatically.  

* **name:** [String/Symbol] server name
* **provider**: [String] should be set to `aws` for AWS pipelines
* **resource_type**: [String] should be either `aws_instance` or `aws_autoscaling_group`
* **protocol**: [String] server protocol (winrm, winrms, wsman, wsmans, ssh, docker, local)
* **host**: [String] server host name or IP address
* **port**: [Integer/String] server port
* **user**: [String] server user name
* **password**: [String] server password. Either password or SSH keys is required.
* **keys**: [String] file path to the server's SSH key. Either password or SSH keys is required.
  
```ruby
    # in this example, we are defining a new server 'my_server_123' that is using the bastion options
    bastion_options = {
      name: 'bastion_123',
      provider: 'aws',
      resource_type: 'aws_autoscaling_group',
      protocol: 'ssh',
      user: 'ec2-user',
      port: 22,
      keys: 'ssh_key_path'
    }

    server_source 'my_server_123',
      provider: 'aws',
      resource_type: 'aws_instance',
      protocol: 'ssh',
      user: 'ec2-user',
      port: 22,
      password: 'password',
      bastion: bastion_options,
      test_profile: 'common'

    # in this example, we are defining 'my_server_456' that is using server 'bastion_asg'
    server_source 'bastion_asg', 
      provider: 'aws',
      resource_type: 'aws_autoscaling_group',
      user: 'ec2-user', 
      protocol: 'ssh', 
      port: 22, 
      keys: 'ssh_key_path'

     server_source 'my_server_456',
      provider: 'aws',
      resource_type: 'aws_instance',
      protocol: 'ssh',
      user: 'ec2-user',
      port: 22,
      password: 'password',
      bastion: 'bastion_asg',
      test_profile: 'common' 
```

Looking at the `server_source` example, we are not providing the host parameter for the bastion. The framework uses AWS APIs to get host(s) at the execution time based on `provider`, `resource_type`, and the server name. 

### <a id="website" name="website"></a>website

`website` is a Ruby object defining a logical web site. The object contains all necessary information to produce the URL.

The ***website*** creation requires a name and a variety of options depending on the configuration details.

* **name:** [String/Symbol] web site name
* **protocol**: [String] web site protocol (http, https). `http` is the default.
* **host**: [String] web site host name
* **port**: [Integer/String] web site port
* **user**: [String] web site user name
* **password**: [String] web site password
* **path**: [String] web site path

```ruby
# in this example, we are creating a web site, which will be reachable by https://www.iamawebsite.com/
website :classic, protocol: :https, host: 'www.iamawebsite.com'
```

## <a id="Uploading" name="Uploading"></a>Uploading  files

### <a id="Uploading-server" name="Uploading-server"></a>Uploading files to servers

***scp_upload***

Upload local files to a remote server, using ***scp***.

 `scp_upload` parameters are:

* **server:** [String] server
* **locals:** [Array<String>] array of local files
* **remote**: [String] remote path

```ruby
# in this example, we are uploading the file at local_file_path to server123 at remote_path
scp_upload server123, ['local_file_path'], 'remote_path'
```

***train_upload***

Upload local files to a remote server, using ***train***. We recommend using `scp_upload` instead of this method.  

 `train_upload` parameters are:

* **server:** [String] server
* **locals:** [Array<String>] array of local files
* **remote**: [String] remote path

```ruby
# in this example, we are uploading the file at local_file_path to server123 at remote_path
train_upload server123, ['local_file_path'], 'remote_path'
```

### <a id="Uploading-s3" name="Uploading-s3"></a>Uploading files to S3

***s3_folder_upload!*** uploads a folder to an S3 bucket. This method uses the default AWS region.

 `s3_folder_upload!` parameters are:

* **bucket:** [String] S3 bucket
* **local_folder:** [String] local folder (source)
* **remote_folder**: [String] remote path
* **thread_count**: [Integer] Maximum number of simultaneous threads. Defaults to 5.

```ruby
# in this example, we are uploading the content of the /opt/options/config-files directory 
# to the s3_destination_bucket under 'config-files' 
s3_folder_upload!('s3_destination_bucket', '/opt/options/config-files', 'config-files')
```

## <a id="rake" name="rake"></a>Using Rake Tasks

See the following link for additional information about Rake [Learn the tools: Running builds with Rake](learn-the-concepts.md#learn-the-tools-running-builds-with-rake). 

### <a id="add-rake" name="add-rake"></a>Adding new rake tasks

New rake tasks can be added directly to the Rakefile. Additional rake files (with the file extension .rake) can be added to the *rakelib* directory located at the top project level (i.e. the same directory that contains the main Rakefile).

In the following example, we are adding one new rake task.

```ruby
# in this example, we are adding a new rake task directly to Rakefile
load 'packer-tasks/rake/image/ami.rake'

task :do_something do
  # the task code goes here
end
```

In the following example, we are adding two new rake tasks in `do.rake` and another task in `qa.rake`. 

```ruby
# This is the file content of 'rakelib/do.rake'
# in this example, we are adding new rake tasks to a .rake file in rakelib
task :do_something do
  # the task code goes here
end

task :do_something_else do
  # the task code goes here
end

# This is the file content of 'rakelib/qa.rake'
# in this example, we are adding a new rake task to a .rake file in rakelib
task :qa do
  # the task code goes here
end
```

### <a id="rake-name" name="rake-name"></a>rake namespaces

Rake *namespaces* are used to avoid clashes between tasks with the same names. 

```ruby
# the build task in the main namespace
namespace 'main' do
  task :build do
    # the task code goes here
  end
end

# the build task in the samples namespace
namespace 'samples' do
  task :build do
    # the task code goes here
  end
end

# the top level build task now has dependencies on two other tasks
task build: %w[main:build samples:build]
```

We can call each task individually or we can use prerequisites to define another task (see the example above).

```sh
# calling the main:build task
rake main:build

# calling the samples:build task
rake samples:build

# calling the top level build task. the build task depends on main:build and samples:build
rake build
```

### <a id="enhance-rake" name="enhance-rake"></a>Enhancing rake tasks

A rake task may be defined more than once. Each definition adds its prerequisites and actions to the existing definition.

```ruby
# in this example, we are showing different ways to define the same task
# the following is equivalent to the single task specification given below
task :name
task name: :prereq1
task name: %w[prereq2]
task :name do |t|
  # actions
end

# the following is equivalent to the multiple task specifications given above
task name: [:prereq1, :prereq2] do |t|
  # actions (may reference t)
end
```

### <a id="dsl" name="dsl"></a>Using framework's DSL methods in rake tasks

If you want to use framework's DSL (Domain Specific Language) in your rake tasks, you just need to import the framework into your .rake files.

```ruby
# in this example, we are using the pipeline-task framework methods
require 'pipeline-tasks'

set :a_custom_variable, 'value_123'

set_if_empty :do_compex_test, false
```

## <a id="hook" name="hook"></a>Adding before and after hooks

### <a id="about-hook" name="about-hook"></a>About before and after hooks for Rake tasks

The *before* and *after* hooks allow customization by enabling any rake tasks to call a task (or code block) before or after its own execution. If you don't have much experience with Ruby Rake management, think of a rake task as implementation steps packaged into a `task` scope that can be called from the command line.  

As this may be obvious, *the order of the arguments matters* when methods such as before and after are called. In both the before and after hooks, the current task is first and then following by the prerequisite or post task and any additional arguments or do-end code blocks.  

#### *before* hook

The *before* hook should be created in the following way: `before(task, prerequisite, *args, &block)`.

 `before` parameters are:

* **task:** [String] task
* **prerequisite:** [String] this task should be executed before *task*
* **args**: [String] prerequisite task arguments
* **block**: [Object] optional code block

In the example below, `:starting` would be the task to be called and `:ensure_user` would be the task to run before `:starting` is invoked. 

```ruby
  # :ensure_user will be called before :starting
  before :starting, :ensure_user
```

```ruby
# in this example, 'infra:destroy:core-bucket-pre' will be executed before 'infra:destroy:core-bucket:destroy'
# the code block (the code between do-end) contains some additional code that we want to execute
before 'infra:destroy:core-bucket:destroy', 'infra:destroy:core-bucket-pre' do
  # Identify the bucket that will hold remote state.
  backend_bucket = fetch(:terraform_backend_bucket)
  
  # Build the TF args that target the core account.
  options = { environment: fetch(:accounts, {})[fetch(:core_vars, {})['account_code']] }
  
  # Remove the bucket from the TF state.
  status "Removing bucket:  #{backend_bucket} from terraform state"
  cd 'terraform/core-bucket' do
    terraform 'state', nil, 'rm', 'aws_s3_bucket.platform', options.merge(ignore_failure: true)
  end
end
```

#### *after* hook

The *after* hook should be created in the following way: `after(task, post_task, *args, &block)`.

 `after` parameters are:

* **task:** [String] task
* **post_task:** [String] this task should be executed after *task*
* **args**: [String] post_task task arguments
* **block**: [Object] optional code block

The **after hook** example below shows the after method name and then the arguments being passed with the first argument as `security:compliance` being the initial task to be called and the next argument `security:check_audit_results` being the post task to be called after the first task is completed. 

```ruby
  # in this example, `security:check_audit_results` will be called after `security:compliance`
  after "security:compliance", "security:check_audit_results"
```

```ruby
  # in this example, 'config:bootstrap:upload' will be called after 'infra:deploy:core-bucket:apply'
  # the code block will ensure we always upload generated configuration to the bucket by invoking task 'config:customer.yml:upload!'
  after 'infra:deploy:core-bucket:apply', 'config:bootstrap:upload' do
    begin invoke 'config:customer.yml:upload!'
    rescue RuntimeError => e
      error e.message
    end
  end
```

