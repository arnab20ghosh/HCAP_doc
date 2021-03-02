---
title: Build and test from your workstation
---
# Build and test from your workstation

## Preparing to build

The process of building an AMI (Amazon Machine Image) uses various tools such as Chef, Packer, Direnv, and Git.
If you are unfamiliar with any of these DevOps tools please take time to read the <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-devsecops', viewPage: 'learn-the-concept', viewSection: 'devops'})" style="text-decoration:none">Learn the Concepts</a>. 

## Building an Amazon Machine Image (AMI) using the Projector Generator

### Overview

The image build/test/deliver stage is responsible for building an AMI, testing it against baseline specifications, running compliance scans against them and then sharing it to multiple workload accounts and creating encrypted copies of the AMI.

Machine image pipelines are set of rake tasks defined by the framework. For more information, in the Learn the Concepts topic, see <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-devsecops', viewPage: 'learn-the-concept', viewSection: 'rake'})" style="text-decoration:none">Running builds with Rake</a>.

  These Rake tasks can be used either in local machine or on Jenkins with appropriate settings and configurations. Before starting we need to set up the machine with appropriate tools. For this please refer the topics <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-devsecops', viewPage: 'configure-workstation', viewSection: 'dev'})" style="text-decoration:none">Configure a DevSecOps Workstation </a> and <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-devsecops', viewPage: 'learn-the-concept', viewSection: 'devops'})" style="text-decoration:none">Learn the Concepts</a>. Here are the rake tasks in the order:

  1. `bundle exec rake config`:pull This task creates a `pipeline-config` directory under `target` directory with the content from external configuration repository.

  2. `bundle exec rake build` will build an AMI using the provided packer template. Note this task actually creates an un-encrypted AMI.

  3. `bundle exec rake test` will launch an instance using the AMI built in previous step and run server tests and compliance tests.

  4. `bundle exec rake deliver` will create encrypted copies of the previously created un-encrypted images.

    NOTE: The Core account is where we will bake the images. We will actually use the AMIs to spin up instances and run the required application related services in Workload accounts.

> Before starting this tutorial of building an AMI locally; make sure to first read through the <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-devsecops', viewPage: 'create-projects', viewSection: 'proj'})" style="text-decoration:none">Create Projects</a>, <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-devsecops', viewPage: 'customizing-projects', viewSection: 'cust'})" style="text-decoration:none">Customize projects</a>, and <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-devsecops', viewPage: 'configure-projects', viewSection: 'con-pro'})" style="text-decoration:none">Configure Projects</a> sections.
It is **critically important** to understand the information presented in those sections before proceeding in this tutorial.

### Setting up the Build

The build task spins up an instance using **Packer**, runs the Packer provisioners as mentioned in the **build.json** file of Packer. For more information, see [**Packer docs**](https://www.packer.io/intro/getting-started/build-image.html)

#### Overview of the build.json file

The *build.json* file contains much of the variables and configurations for the packer AMI build. The *build.json* contains mainly these sections:

* [variables](https://www.packer.io/docs/templates/user-variables.html) - Default packer variables that can be overridden while building
* [builders](https://www.packer.io/docs/builders/index.html) - contains what type of AMI is being built and the cloud provider type
* [provisioners](https://www.packer.io/docs/provisioners/index.html) - Configuration and scripts that needs to be applied on the AMI
* [post-processors](https://www.packer.io/docs/post-processors/index.html) - Tasks that needs to be run after the AMI is built

For more information on configuring **build.json**, in the Learn the Concepts topic, <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-devsecops', viewPage: 'learn-the-concept', viewSection: 'packer'})" style="text-decoration:none">Building with Packer</a>.

Multiple <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-devsecops', viewPage: 'learn-the-concept', viewSection: 'cloud'})" style="text-decoration:none">AWS Settings</a> also need to be configured as Environmental variables and configuring the profile being used to create this image.

The required ENV settings are shown below in step 2.

##### **Step 1: Create an AMI project with the project generator using the packer style template.**

Use the project generator gem to create a new AMI pipeline.

```bash
generate pipeline my-project ../my-ami -s image/packer
```

> Here *my-project* is the name of the application and *my-ami* is the folder in which the image pipeline project is generated.

> All steps below assume that the commands/steps are performed in **the my-ami project directory created** in the project generator script used above.

##### **Step 2: Configure Environment (ENV) Variables**

> It is recommended to use <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-devsecops', viewPage: 'learn-the-concept', viewSection: 'direnv'})" style="text-decoration:none">direnv</a>. tool to set the environment variables using the **.envrc** file.

If direnv is not installed, the ENV variables can be set using the `export VARIABLE_NAME=value` in the terminal. To see all the Environment available variables and their values, in the terminal, type `printenv` . The benefit of using the direnv tool is that it allows you to create a project level file for ENV variables without cluttering up the global ENV variables or having naming conflicts and/or conflicting values.

The following ENV (Environment Variables) values (see table below) should be set when building a local AMI from your workstation. As you can see, the only required one
is the AWS_PROFILE which is includes the AWS_REGION within the profile needed for this pipeline.


| Variable            | Usage                                                                           | Optional |
| ------------------- | ------------------------------------------------------------------------------- | -------- |
| AWS_PROFILE         | Set this to the same profile as the account in which the AMI is being built     | true     |
| AWS_REGION          | Region in which the image is being built, if it's not set will read from config | false    |
| VAR_FILE            | Set this if using a local override JSON file for packer variables               | true     |
| PACKER_LOG          | Set to 1 to enable *packer* debug logs                                          | true     |
| PACKER_LOG_PATH     | File to save the build logs to                                                  | true     |
| PIPELINE_CONFIG_REF | External Configuration's GIT Branch                                             | false    |
| PIPELINE_CONFIG_URL | External configuration URL                                                      | false    |
| SOURCE_AMI          | BASE AMI using used for AMI baking process                                      | false    |
| STIGTOOL_S3_BUCKET  | Required only if you need publishing STIG state to S3                           | true     |

> Note: The external configuration can be disabled by setting :external_config_type to :none.

An example **.envrc** file

```bash
export PIPELINE_CONFIG_REF=develop
export PIPELINE_CONFIG_URL=git@github.com/reancloud/rean-pipeline-config.git
export AWS_PROFILE=rean-pldev
export VAR_FILE=vars.json
export SOURCE_AMI=ami-053f6d5d4cb2dbae7
```

Environment variables are used to configure values that the framework passes into the packer builder. 


##### **Step 3: Modifying config.rb**

This file should be modified with all user specific configurations.

The default variables in the table below are always passed to the packer command.

| Value       | Description                                                              |
| ----------- | ------------------------------------------------------------------------ |
| expiry_date | Calculated as the current date plus 1 day                                |
| aws_region  | Value of *AWS_REGION* or *AWS_DEFAULT_REGION* environment variables      |
| build_url   | Value of *BUILD_URL* environment variable if it is set, defaults to None |

The framework sets *:default_image_build_vars* configuration variable which consists of the following values:

| Value       | Description                                                  |
| ----------- | ------------------------------------------------------------ |
| environment | Value of *PIPELINE_ENV* environment variable, defaults to dev. |
| version     | Current project version in the VERSION file                  |
| name        | *AMI_NAME* environment variable if set                       |
| source_ami  | Checks for *SOURCE_IMAGE* environment variable fallback to *SOURCE_IMAGE_FILE* |
| ami_users   | Comma separated value of accounts to which to share the image, get's auto-generated from workload_account*.json from external pipeline repository data |

> The **source_ami** key specifies the source AMI to be used while building an AMI. When building a base AMI this can either come from the external pipeline repository or the local **vars.json** or the **SOURCE_IMAGE** environment variable which has the AMI id. When building a dependent AMI based on an already built AMI, either use the **SOURCE_IMAGE** or **SOURCE_IMAGE_FILE** environment variable. The **SOURCE_IMAGE_FILE** environment variable points to a JSON file containing the AMI info in a format as mentioned below:


```json
{
  "ami_id": "ami-0f18387ab543f07be"
}

```

The framework sets the variables that are passed to packer command as *image_build_vars* which initially points to the *default_image_build_vars*

```ruby
# using the default values
set_if_empty :image_build_vars, lambda {
  fetch(:default_image_build_vars)
}
```

The user can add additional variables as shown below:

```ruby
# using the default values and adding one variable
set :image_build_vars, lambda {
  vars = fetch(:default_image_build_vars)
  vars[:source_ami] = ENV['SOURCE_AMI'] if ENV['SOURCE_AMI']
  vars
}
```

The following configuration values are used for AMI server and compliance testing.

`:compliance_tool`: This is the tool used for compliance scanning of STIGs. For more information, in the Learn the Concepts topic, see <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-devsecops', viewPage: 'learn-the-concept', viewSection: 'security'})" style="text-decoration:none">Security Technical Implementation Guides</a>. 

Defaults to `:stigtool`.

When using `:stigtool`, the state publisher s3 bucket can be configured using the environment variable `STIGTOOL_S3_BUCKET`.

To disable the compliance checking, set the value to `:none` in the config.rb.

```ruby
# disable the compliance checking
set :compliance_tool, :none
```

> `:server_test_tool`: The tools used for server testing. Defaults to `:inspec`.

##### **Step 4: Modify the build.json file**

The project generator sets the Packer build  default values in the build.json created in the root project directory.
Any value of `null` in the variables section must either be defined via external configuration repository json files, local var.json file or provided in the **config.rb**. For more information, in the Create Project, see <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-devsecops', viewPage: 'create-projects', viewSection: 'work-config'})" style="text-decoration:none">Set Basic Configuration in Config.rb</a>.

All values defined in upper case in *build.json* in the *variables* section should be updated with user specified values.

| Values              | Description                                                  |
| ------------------- | ------------------------------------------------------------ |
| MY_AMI              | A meaningful name for the packer builder                     |
| MY_OWNER            | Propagates as *Owner* tag for the image                      |
| MY_PRODUCT          | Propagates as *Product* tag for the image                    |
| MY_PROJECT          | Propagates as *Project* tag for the image                    |
| MY_SG_ID            | Comma separated list of security groups                      |
| MY_SOURCE_AMI       | The source image to be used, can be over-ridden by SOURCE_AMI environment variable |
| MY_SSH_USERNAME     | The SSH username used to connect to the launched machine     |
| MY_SUBNET_ID        | The subnet id to use                                         |
| MY_VPC_ID           | The VPC id to use                                            |
| MY_INSTANCE_PROFILE | It is in the generated build.json                            |
| MY_INSTANCE_SIZE    | It is in the generated build.json                            |

Any values defined as *null* in the *variables* section of *build.json* are auto-generated by the framework.

| Value       | Description                                                                                                                                            |
| ----------- | ------------------------------------------------------------------------------------------------------------------------------------------------------ |
| ami_users   | Comma separated value of accounts to which to share the image, get's auto-generated from workload_account*.json from external pipeline repository data |
| aws_region  | Value of *AWS_REGION* or *AWS_DEFAULT_REGION* environment variables                                                                                    |
| build_url   | Value of *BUILD_URL* environment variable if set, defaults to None.                                                                                    |
| environment | Value of *PIPELINE_ENV* environment variable, defaults to dev.                                                                                         |
| expiry_date | Calculated as the current date plus 1 day                                                                                                              |
| version     | Current project version in the VERSION file                                                                                                            |

> The *public_ip* variable can be set to *true* if required.

> Any of the *variables* defined in **build.json** under **variables** key can be overridden by the local **vars.json**. If we are not using VPC infrastructure or we haven't been bootstrapped by the framework, the variables *vpc_id* (Virtual Private Cloud Id), *sg_ids* (Security Group Ids), *subnet_id* (Network Subnet Id), etc. should be added to the local **vars.json**

For more information, in the Learn the Concepts topic, see <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-devsecops', viewPage: 'learn-the-concept', viewSection: 'aws-img'})" style="text-decoration:none">Network Connectivity: AWS image pipeline</a>. 

### Running the build

This steps generate Packer inputs from multiple sources (config.rb, external configuration, environment variables etc) and then runs packer to build an initial un-encrypted AMI, creates details of built AMI under **target/image.json**, **target/image-\<region\>.json** files and then verifies the AMI is available for further use.

Run the following command which will download all the gems and dependencies:

```bash
bundle install
```

Then run  **config:pull**. It actually creates a `pipeline-config` directory under `target` directory with the content from external configuration repository and checkouts the reference branch. The directory `target/pipeline-config` will have configuration information for all pipelines.

```bash
  bundle exec rake config:pull
```


```bash
bundle exec rake build
```

This `build` rake task above will run the actual AMI build using **packer** and creates the un-encrypted AMI, then creates **target/image.json**, **target/image-us-east-1.json** with the built AMI info and verifies the AMI is available.


**Below are examples of generated files from the AMI build: **

   > **target/image.json**

```json
{
    "ami_ids": {
        "us-east-1": "ami-XXXXXXXXXXXXXXXX"
    }
}
```

> **target/image-us-east-1.json**

```json
{
  "ami_id": "ami-XXXXXXXXXXXXXXXXXXXX"
}
```

#### **build** rake task dependencies

If this is your first time using Rake tasks for task management or if you want to learn more about Ruby Rake task management. For more information, in the Learn the Concepts topic, see <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-devsecops', viewPage: 'learn-the-concept', viewSection: 'rake'})" style="text-decoration:none">Running builds with Rake</a>. 

```tree
.
└── build                                               - Top level build task
    ├── vendor_clean                                    - Cleans the existing vendor-cookbooks folder
    ├── vendor-cookbooks                                - Downloads the cookbook dependencies
    │   └── target                                      - Creates the target folder if missing
    ├── target                                          - Creates the target folder if missing
    └── build:build                                     - Task to runs the image build
        ├── build:inputs                                - Generates the packer inputs(`target/image-inputs.json`) from multiple sources
        │   └── target                                  - Creates the target folder if missing
        └── build:prereq_json                           - Backwards compatibility for builds that uses json_updater packer plugin
```

### Running tests and compliance scans

The test task is responsible for spinning up a temporary EC2 machine instance based on the created AMI, running baseline tests, running compliance scanning tests, and finally destroying the temporary infrastructure.

This uses **terraform** to launch the temporary infrastructure. The configuration for the terraform is standard across all projects and is stored as **test.tf**.

> To learn more about terraform as well as InSpec which are used for the testing, refer to <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-devsecops', viewPage: 'learn-the-concept', viewSection: 'inspec'})" style="text-decoration:none">Testing with Terraform and Inspec</a>. 

> The compliance scans are run according to STIG guidelines; to learn more about STIGS--what they are and how they are used, see <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-devsecops', viewPage: 'learn-the-concept', viewSection: 'security'})" style="text-decoration:none">Security Technical Implementation Guides</a>. 

The high level **overview** consists of the following:

1. Create a temporary infrastructure (EC2 machine) using terraform from the previously created AMI
2. Wait for the instance to be available (status checks to pass)
3. Fetch the password for WinRM connection in case of Windows machines
4. Wait for the connection to be available (SSH in case of Linux machines and WinRM in case of Windows machines)
5. Run Inspec scans to test the EC2 instance against baseline configuration
6. Run compliance scans using Nessus/Inspec if compliance scanning is enabled
7. Generate/Record the results if compliance scanning is enabled
8. Destroy the temporary infrastructure using terraform, independent of the status of the test/compliance scanning

#### Running Test

> Run tests on an AMI that was built during the previous steps.

> This assumes that the **target/image.json** file is created as part of the AMI build process.

##### **Option 1**

Runs the whole test process mentioned above from the overview in a single command.

```bash
bundle exec rake test
```

> If any task/stage fails the AMI get de-registered

##### **Option 2**

Runs each stage of the test process individually

> This helps to run baseline tests/compliance scans over and over again without having to create/destroy temporary EC2 machine every single time. **This method should be used while running scans/tests locally.**

**Test Option 2 > Step 1**

```bash
bundle exec rake test:pre
```

This task will first generate a temporary SSH keypair and launches the EC2 using **terraform**

**Test Option 2 > Step 2**

```bash
bundle exec rake test:integration
```

This task runs the baseline scans on the AMI as per the test profiles present under the **test** directory.

This task can be re-run after fixing any failing tests to confirm they are working without having to re-create the EC2 instance.

**Test Option 2 > Step 3**

```bash
bundle exec rake test:compliance
```

This task runs the compliance scans on the AMI as per the compliance profiles present under the **audit** directory.

This task can be re-run after fixing any failing compliance tests to confirm they are working without having to re-create the EC2 instance.

**Test Option 2 > Step 4**

```bash
bundle exec rake test:post
```

This task is used to destroy the temporary EC2 that was spun up to run tests/compliance scans.

> **Make sure to run this task always after running tests/compliance scans locally**.

#### **Test** rake task dependencies listing

If any stage/task in the *test* stage fails the framework will call the **expire** or **destroy** task as per the configuration.
The default action is to **destroy**

> Note: See in the **tree below** if you call `test` at the outer level, it will call all the subsequent tasks within this task. However, you can also call `test:pre`, `test:integration`, `test:compliance`, and `test:post` separately which allows more flexibility and not needing to re-create the EC2 instance when re-running tests.

```tree
.
└── test                                                - Top level test task
    ├── test:pre                                        - Creates temporary infrastructure for the tests
    │   └── test:infra:deploy:test                      - Infra task which deploys a server internally named **test** server
    │       ├── target                                  - Creates the target folder if missing
    │       ├── test:infra:deploy:test:init             - Task to run **terraform init**
    │       │   ├── test:infra:deploy:test:inputs       - Generates terraform inputs
    │       │   │   └── target                          - Creates the target folder if missing
    │       │   ├── build:inputs                        - Generates the packer inputs from multiple sources
    │       │   │   └── target                          - Creates the target folder if missing
    │       │   └── test:infra:keypair                  - Generates temporary keypair for standing up the ec2 and for connecting to the launched instance
    │       │       └── target                          - Creates the target folder if missing
    │       ├── test:infra:deploy:test:apply            - Task to run **terraform apply**
    │       │   └── test:infra:deploy:test:inputs       - Generates terraform inputs
    │       │       └── target                          - Creates the target folder if missing
    │       └── test:infra:deploy:test:outputs          - Task to run **terraform output**
    ├── test:all                                        - Task to run the integration and compliance scans
    │   ├── test:integration                            - Task to run inspec scans
    │   │   └── test:integration:test                   - Task to run inspec against the internally named **test** server
    │   │       └── test:integration:test:prepare       - Task to check if the ec2 is up and running and is able connect to that
    │   └── test:compliance                             - Task to run STIG compliance scan
    │       ├── test:compliance:test                    - task to run STIG compliance scan against the internally named **test** server
    │       └── test:integration:test:prepare           - Task to check if the ec2 is up and running and is able connect to that
    └── test:post                                       - Task to destroy the temporary infrastructure
        └── test:infra:destroy:test                     - Infra task to destroy the internally named **test** server
            ├── target                                  - Creates the target folder if missing
            ├── test:infra:deploy:test:init             - Task to run **terraform init**
            │   └── test:infra:deploy:test:inputs       - Generates terraform inputs
            │       └── target                          - Creates the target folder if missing
            └── test:infra:destroy:test:destroy         - Task to run **terraform destroy**
                ├── test:infra:deploy:test:inputs       - Generates terraform inputs
                │   └── target                          - Creates the target folder if missing
                ├── build:inputs                        - Generates the packer inputs from multiple sources
                │   └── target                          - Creates the target folder if missing
                └── test:infra:keypair                  - Generates temporary keypair for standing up the ec2
                    └── target                          - Creates the target folder if missing
```

### Manually inspecting a server

To manually inspect a server, a server or server_source object needs to be configured / initialized in config.rb, see <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-devsecops', viewPage: 'configure-projects', viewSection: 'con-pro'})" style="text-decoration:none">Configure Projects</a>.

To inspect an AMI, you may also choose to manually create the test infrastructure (EC2 instance) and inspect the server brought up by the image.
However if testing manually using this method; remember the infrastructure will not automatically be destroyed and you must destroy after inspecting it.

<!-- Arnab: No topic present in learn the concepts///////
To inspect an server, you may also want to connect to a **remote test system**. To learn more about network connectivity and remote logins for remote test system see the Learn the Concepts [Network Connectivity](../learn-the-concepts.md#network-connectivity-aws-image-pipelines) and [Remote Logins](../learn-the-concepts.md#remote-logins-linux-images) sections. -->

### Destroying an image

When inside the project directory of the AMI image your are working on; you can use a Rake command to destroy the AMI.
Again to do this, you need to be inside the AMI project directory as you have been working for all previous sections.

If you run the following command as mentioned previously you will see all the rake tasks available:

> `bundle exec rake -T`

You will see one called `destroy` and this is the command we will use to target the AMI of the project folder we are in.

Run the following command to destroy the current AMI within the directory we are working:

> `bundle exec rake destroy`

### Publishing an image

The deliver task optionally shares the already created un-encrypted AMI to the workload accounts--workload accounts are where tasks and builds can happen; however the deployment would take place using the core account--and creates encrypted copies of the AMI in the same account
where it was built (core account) and optionally to the external workload accounts.

1. If the Image type is Windows and Sysprep is enabled, an EC2 instance is used for copy using the AWS Instance launch API.

1. If the image type is Windows and Sysprep is disabled and if the image does not have BillingCode EC2 CopyImage API is used.

1. If the image type is Windows and Sysprep is disabled, and if the image have BillingCode packer is used for copy.

1. If the image type is Linux and if the image does not have billing code enabled EC2 CopyImage API is used.

1. If the image type is Linux and if the image have BillingCode packer is used for copy. 

   Fore more information on Sysprep, see [Microsoft docs](https://docs.microsoft.com/en-us/windows-hardware/manufacture/desktop/sysprep--generalize--a-windows-installation).

#### **deliver** rake task dependencies
The **deliver** task copies the unencrypted image built at the build stage to various workload accounts. The external configuration should define the workload_accounts.

```ruby
  # the workload accounts in `us-gov-west-1` AWS region
  # the workload account codes are "rean-sd", "pldev", and "plwl"
  #workload_accounts.us-gov-west-1.json
  {
    "rean-sd" : {
       "subnet_id" : "subnet-87e34ce3",
       "account_id" : "XXXXX",
       "vpc_id" : "vpc-95691df0",
       "sg_id" : "sg-492fd32d"
    },
    "pldev" : {
       "subnet_id" : "subnet-36add540",
       "account_id" : "XXXXXXXXX",
       "vpc_id" : "vpc-6e4ff30a",
       "sg_id" : "sg-4e6f5329"
    },
    "plwl" : {
       "subnet_id" : "subnet-61e90d05",
       "account_id" : "XXXXXXXX",
       "sg_id" : "sg-bd29d5d9",
       "vpc_id" : "vpc-4c6b1f29"
    }
 }

 # the workload accounts in `us-east-1.` AWS region
 # the workload account codes are "product", "trainee", and "reanms"
 #workload_accounts.us-east-1.json
 {
    "product" : { #core account
        "account_id": "XXXXXXXXX",
        "vpc_id": "vpc-0181557b",
        "subnet_id": "subnet-29cb4f75",
        "sg_id":"sg-6f18e222",
        "owner" : "engineer1"
    },
    "trainee": {
        "account_id": "XXXXXXXXX",
        "vpc_id": "vpc-07ced0d080a8f9419",
        "sg_id": "sg-0ab199d93a6328210",
        "subnet_id": "subnet-04bab323ac37ee117",
        "owner" : "engineer1"
    },
    "reanms" : {
        "account_id": "XXXXXXXXX",
        "vpc_id": "vpc-0998d5622512e678e",
        "subnet_id": "subnet-0b7c153ee6773191d",
        "sg_id":"sg-03429fd7a87beff63",
        "owner" : "engineer1"
    }
}
```

```tree
.
└── deliver                                             - Top level deliver tasks
    └── deliver:all                                     - Task to call all deliver copies
        └── deliver:copy                                - Task which calls the copy
            ├── deliver:copy:<workload-account-1>       - Copy to workload account 1
            ├── deliver:copy:<workload-account-2>       - Copy to workload account 2
            ├── deliver:copy:<workload-account-.>       - ..........................
            ├── deliver:copy:<workload-account-.>       - ..........................
            └── deliver:copy:<workload-account-n>       - Copy to workload account **n**
```

The workload accounts ***deliver*** tasks dynamically generated based on workload accounts data. By default the framework looks for a JSON file at *target/pipeline-config/amis/workload_account.\<region\>.json*


> The AWS CLI needs to be configured with all workload account credentials. The framework expects one AWS profile per the workload account. The AWS profile names should match the workload accounts. The framework passes in the profile name when running the workload account copy task, so the AWS CLI needs to be configured for each workload account in the workload_accounts.<region>.json.


```sh
  #example config ~/.aws/config
  [pldev] #AWS_PROFILE as referrenced in the work load accounts
  region=us-gov-west-1 # Default region
  aws_access_key_id = AKIAZNNNNNNNNNNNNN
  aws_secret_access_key = 1234567890

```

**Note**: One of work load accounts could actually be a core account in which the AMI is built at the build stage. It is added to workload accounts so that it can be copied as an encrypted AMI. During the build phase, the unencrypted AMI is shared across all workload accounts but due to AWS licensing issues, some AMIs can not be copied using the AWS copy AMI API unless it is in the same account. So the deliver task will have to rebuild the AMI by launching an AMI using unencrypted AMIs and then encrypt the resulting AMI.

If our `AWS_REGION` is `us-east-1` and the workload accounts are `product`, `trainee`, and `reanms`, we will have the following *deliver* tasks.
- rake deliver
  - rake deliver:all - This task uses already shared AMI during build task.
    - rake deliver:copy - This is a combination of tasks below
      - rake deliver:copy:product - This task uses AWS AMI copy API as it runs in a core account. This task also validates if the AMI is already copied by using name tags. If it is already copied, then it will not create another AMI (this rule also applies for the other two tasks).
      - rake deliver:copy:trainee - This task rebuilds AMI using the unencrypted AMI built at the build stage and encrypts it
      - rake deliver:copy:reanms - This task rebuilds AMI using the unencrypted AMI built at the build stage and encrypts it
