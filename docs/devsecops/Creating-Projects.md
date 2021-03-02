---
title: Create Projects
---

# <a id="proj" name="proj"></a>Create Projects

The project generator creates a Ruby-based project providing AMI creation capabilities.
In the further sections of this document we will explain how to customize the project to successfully create AMIs.

#### Contents

- <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-devsecops', viewPage: 'create-projects', viewSection: 'prereq'})" style="text-decoration:none">Prerequisites</a>
- <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-devsecops', viewPage: 'create-projects', viewSection: 'prereq'})" style="text-decoration:none">Step by step guide</a>
- <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-devsecops', viewPage: 'create-projects', viewSection: 'generate'})" style="text-decoration:none">Generating a Project</a>

## <a id="prereq" name="prereq"></a>Prerequisites

Before you start creating a project, ensure that you have:

1. An access to Artifactory that has all the required artifacts for the project.
2. An access to Git server. 
3. AWS credentials for Packer. For more information on how to use AWS credentials with Packer, visit Packer Documentation, and see [AWS Authentication](https://www.packer.io/docs/builders/amazon.html#authentication).

## <a id="step" name="step"></a>Step-by-step guide

The following steps are required for creating AMI pipelines:

- <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-devsecops', viewPage: 'create-projects', viewSection: 'generate'})" style="text-decoration:none">Generate project using project generator </a>
- <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-devsecops', viewPage: 'create-projects', viewSection: 'work-config'})" style="text-decoration:none">Set Basic Configuration in Config.rb</a>
- <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-devsecops', viewPage: 'create-projects', viewSection: 'packer'})" style="text-decoration:none">Creating a Packer template</a>
- <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-devsecops', viewPage: 'create-projects', viewSection: 'chef'})" style="text-decoration:none">Add required server configuration using chef cookbooks </a>
- <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-devsecops', viewPage: 'create-projects', viewSection: 'inspec'})" style="text-decoration:none">Add Inspec tests to validate server configuration </a>
- <!-- <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-devsecops', viewPage: 'create-projects', viewSection: 'compliance'})" style="text-decoration:none">Add Compliance scans to check for security guidelines given by IASE DISA </a> -->
- <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-devsecops', viewPage: 'create-projects', viewSection: 'git'})" style="text-decoration:none">Commit to Git </a>
- <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-devsecops', viewPage: 'create-projects', viewSection: 'additional'})" style="text-decoration:none">Additional Commands </a>

## <a id="generate" name="generate"></a>Generating a project

The project creation depends on the **pipeline-generator** ruby gem

To install the gem locally, use the command:

`gem install pipeline-generator`

To generate the custom project on your local machine, use the command:

`generate pipeline [APP_NAME] [DIR] --style=[STYLE]`

- `pipeline`: indicates that we're creating a new pipeline codebase
- [APP_NAME] : name of the pipeline For example, clientname-app-pipeline.
- [DIR] : directory with the generated output. It can be any directory in the file system.
- --style (-s) : allows us to specify the type of pipeline we're creating, for AMIs this should be set to `image/packer`

#### Examples

- **Generating project in a parent directory**

  In this example, the project generator creates files with the application name `base-rhel7` in the `companyxyz-rhel7` directory in the parent directory.

  `generate pipeline base-rhel7 ../companyxyz-rhel7 -s image/packer`

  ```tree
    .
    └── parent directory
      ├── current directory     - the command is executed here
      └── companyxyz-rhel7      - this is the directory with generated files
  ```

- **Generate project in a subdirectory**

  In this example, the project generator creates files with the application name `base-rhel7` in the `companyabc-rhel7` subdirectory of the current directory.

  `generate pipeline base-rhel7 companyabc-rhel7 -s image/packer`

  ```tree
    .
    └── parent directory
        └── current directory     - the command is executed here
            └── companyabc-rhel7  - this is the directory with generated files
  ```

### <a id="understand" name="understand"></a>Understanding the generated files

The `generate pipeline` command for `image/packer` creates the following files:

| File name               | File type   | Purpose                                                      | Requires customizations               |
| ----------------------- | ----------- | ------------------------------------------------------------ | ------------------------------------- |
| Rakefile                | Rake        | Loads the AMI rake tasks                                     | No                                    |
| config.rb               | Ruby        | Configures the AMI pipeline                                  | Yes  (when changing generated values) |
| build.json              | JSON        | The AMI packer template                                      | Yes                                   |
| jenkins/Build           | Jenkinsfile | Builds AMI in the core account                               | No                                    |
| jenkins/Deliver         | Jenkinsfile | Delivers AMI to the workload accounts                        | No                                    |
| jenkins/Release/Start   | Jenkinsfile | Starts the release process                                   | No                                    |
| jenkins/Release/Build   | Jenkinsfile | Builds the AMI in the context of the release process         | No                                    |
| jenkins/Release/Deliver | Jenkinsfile | Delivers the built AMI in the context of the release process | No                                    |
| jenkins/Release/Finish  | Jenkinsfile | Finishes the release process                                 | No                                    |
| test.tf                 | Terraform   | Creates EC2 instance for server and compliance scanning      | No                                    |

The Jenkins files define Jenkins pipelines using the provided shared Jenkins library. These pipelines execute underlying rake tasks defined for AMI projects.

> Note: The framework also creates `Gemfile` and `Gemfile.lock`. These files describe the Ruby gem dependencies.
>

## <a id="work-config" name="work-config"></a>Working with the Configuration files

The **config.rb** file in the project directory contains the project configuration details. The framework automatically loads **config.rb** by default.
The framework requires the `:application` configuration setting.

The project generator automatically sets `:application` to the value passed in application name.
To change your application name, set `:application` to a new value.

The framework also support loading additional configuration data from other configuration files based on `PIPELINE_ENV` environment variable. This allows different configuration for different environments, for example development vs production.

The additional configuration files must be located under `config` directory in the project root and the file names have to consist of **PIPELINE_ENV** values and the `.rb` file extension.

The values in the additional configuration files overrides the values in `config.rb`. For example, if the same parameter `:iamaparameter` is set in both `config.rb` and `config/dev.rb` and `PIPELINE_ENV` is set to `dev`, the value of `:iamaparameter` in `config/dev.rb` will be used.

In this example, we have three additional configuration files.

```tree
  .
  └── project           - project directory
      └── config        - config directory
          ├──  dev.rb   - this file is loaded when PIPELINE_ENV is dev
          ├──  qa.rb    - this file is loaded when PIPELINE_ENV is qa
          └──  prod.rb  - this file is loaded when PIPELINE_ENV is prod
```

`PIPELINE_ENV` defaults to `dev` if it hasn't been set.

For more information on the parameters in the config.rb file, in the Configuring Projects topic, see <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-devsecops', viewPage: 'configure-projects', viewSection: 'working'})" style="text-decoration:none">Working with config.rb</a>.

## <a id="packer" name="packer"></a>Creating a Packer template

Packer uses a template JSON file to create the Amazon Machine Images (AMIs). In the project generator framework, this template file is `build.json` and this file is located in the project root folder.
To learn more about Packer and the various features this tool offers, in the Learn the Concepts topic, <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-devsecops', viewPage: 'learn-the-concept', viewSection: 'packer'})" style="text-decoration:none">Building with Packer</a>.

### Overriding config.rb values with build.json values

To modify or provide values for the variables that are null in the `variables` section of `build.json`; we can add these variables and values to the `config.rb` file.
Any values provided in the `config.rb` file for a packer build will override values in the **build.json** and **local vars.json** files. 

For example, you can set a region variable in the config.rb file using the following command:

```ruby
set :aws_region, 'us-east-1'
```

This value of `us-east-1` will be used by the packer template during the build process.

### Mandatory Packer variables

When using the project generator, a `build.json` template is available by default.
Following are the basic mandatory parameters for an AMI packer build:

| variable      | purpose                                                                                  | build.json template location                          |
| ------------- | ---------------------------------------------------------------------------------------- | ----------------------------------------------------- |
| name          | Name of the builder such as EBS 1-- only needed if multiple builders are used            | builders                                              |
| type          | Type of builder being used such as `amazon-ebs`                                          | builders                                              |
| ami_name      | Name of the AMI being built, a combination of user supplied name, env name and timestamp | variables as null, user function variable in builders |
| instance_type | The EC2 instance type to use when building the AMI such as t2.small                      | variables                                             |
| source_ami    | The source AMI whose root volume will be copied and used to provision                    | variables as null, user function variable in builders |

## <a id="chef" name="chef"></a>Adding Chef cookbooks

Packer provisioners use built-in and third-party software to install and configure the machine image after booting. For more information see, [Packer docs](https://www.packer.io/docs/provisioners).

### Installing Chef

This step should be done only if the image being built does not have Chef already installed. Packer will automatically attempt to install Chef by default. For more information, in Packer documentation, see [Chef Solo Provisioner](https://www.packer.io/docs/provisioners/chef-solo.html#skip_install).

If Chef is not installed by default, use the custom script to install Chef. For more information, in Packer documentation, see [Chef Solo Install Commands](https://www.packer.io/docs/provisioners/chef-solo.html#install-command).

### Creating a Berksfile

If a [Berksfile](https://docs.chef.io/berkshelf.html#the-berksfile) is present in the project root the framework assumes that the project uses Chef to provision the image.

For more information on how to add Chef cookbook dependencies, in Chef documentation, see [About Berksfile](https://docs.chef.io/berkshelf.html).

When `build` task in invoked, the framework cleans any existing cookbooks already vendored, then vendors all the dependent cookbooks to the `vendor-cookbooks` directory.

### Adding a Chef solo provisioner

Chef-Solo is an open source tool that runs locally and allows to provision guest machines using Chef cookbooks without any Chef configuration. For more information on adding Chef templates for Packer provisioners, in Packer documentation, see [Chef Solo Provisioner](https://www.packer.io/docs/provisioners/chef-solo.html) .

The only change that needs to be done for the *chef-solo* provisioner is to point it to the local folder containing the cookbooks, in this case `vendor-cookbooks` directory.

```json
{
  "type": "chef-solo",
  "cookbook_paths": ["vendor-cookbooks"]
}
```

> To learn more about Chef, in the Learn the Concepts section, see <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-devsecops', viewPage: 'learn-the-concept', viewSection: 'chef'})" style="text-decoration:none">Provisioning with Chef</a>.

After these provisioners and files are created, the packer template AMI can be built by running the rake build command.

`rake build`

This command will create an AMI template that will install ChefDK on the image and run the cookbooks.

## <a id="inspec" name="inspec"></a>Adding InSpec tests

InSpec is a framework for testing and auditing applications and infrastructure. To learn more about InSpec, in the Learn the Concepts section, see <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-devsecops', viewPage: 'learn-the-concept', viewSection: 'inspec'})" style="text-decoration:none">Testing with Terraform and Inspec</a>.

The InSpec testing profiles are located in the `test` folder of the project.

### Inspec profile settings

When InSpec profiles are used for server testing, set `:test_suite` to the directory with the InSpec profile. If `:test_suite` is not set, it defaults to `:application`.

```ruby
# in this example, we should have our InSpec profile in "test/my-inspec-profile"
set :test_suite, 'my-inspec-profile'
```

#### Create a local InSpec profile

Add InSpec profiles to your project by creating your own profiles or including profiles from the Chef Supermarket repository in the Artifactory.
To learn more about creating or adding inSpec profiles, visit the [Chef InSpec documentation](https://www.inspec.io/docs/)

The InSpec profile contains the **inspec.yml** file, which includes the required name key, and other optional keys such as description, title, summary, and other parameters.
The InSpec profile also contains `controls` files. These directories contains all the tests. The InSpec tests are  stored in its respective repository and released to artifactory to be pulled down to the project.

When you execute a local profile, the **inspec.yml** file will be read in order to source any profile dependencies. It will then cache the dependencies locally and generate an **inspec.lock** file.

- In the project root folder, create a folder named `test`
- In the `test` folder create another folder for the InSpec profile. The folder name must match `:test_suite` in config.rb.
- Add the **inspec.yml** file.

In this example, we have a sample `inspec.yml`:

```yaml
# test/<test_suite>/inspec.yml
name: 'example-application-name'
title: Inspec for azure application
maintainer: John Doe
copyright: ABC Corp
copyright_email: john.doe@abccorp.com
license: All Rights Reserved
summary: An InSpec Compliance Profile
version: 0.1.0
supports:
  - os-family: redhat
  - os-family: centos
```

### Adding local controls to an InSpec profile

Controls added directly to the InSpec profile are local to a project/pipeline and are not globally available to other pipelines.
To use a common set of InSpec controls that can be shared by multiple pipelines, see the next topic Adding shared controls to an InSpec profile.

After the local InSpec profile is created inside the `test` directory with appropriate `inspec.yml` file, add another folder called `controls` to the profile. Now create a `<control_file>.rb` and start writing InSpec tests.

In this example, we have InSpec control `properties.rb` checking for the file presence:

```ruby
# test/<test_suite>/controls/properties.rb
title '/tmp/properties profile'

# you add controls here
control "properties" do

  describe file('/tmp') do
    it { should be_directory }
  end

  describe file('/tmp/properties') do
    it { should exist }
    its('mode') { should cmp '00755' }

  end
end
```

For information on different resources like the `file` resource mentioned above, in the InSpec documentation, see [Inspec resources](https://www.inspec.io/docs/reference/resources).

#### Adding shared controls to an InSpec profile

We can add shared profiles under `depends` section of inspec.yml, so that they can be fetched and used at runtime. For example,

```yaml
name: 'example-application-name'
title: Inspec for azure application
maintainer: John Doe
copyright: ABC Corp
copyright_email: john.doe@abccorp.com
license: All Rights Reserved
summary: An InSpec Compliance Profile
version: 0.1.0
inspec_version:
  - '> 4.0'
supports:
  - os-family: redhat
  - os-family: centos
  - os-family: bsd
depends:
  - name: generic-app
    git: https://github.com/abccorp/inspec-generic-app.git
```

In our local profile we can use the dependent profile controls. For example,

```ruby
# test/<test_suite>/controls/shared_controls.rb
include_controls 'generic-app' do
end
```

#### Passing Inputs to InSpec

For more information Chef InSpec Input, see [InSpec Documentation](https://www.inspec.io/docs/reference/inputs/)

InSpec profiles can optionally have inputs values passed at runtime. We can set them up in a local file `test/<test_suite>/inspec_inputs.yml`.
An example InSpec Inputs file is below:

```yaml
---
# test/<test_suite>/inspec_inputs.yml
chefdk_version: 3.3.23                                # ChefDK version
chef_bins:                                            # Installed chef binaries
  - chef
  - chef-client
  - berks
  - inspec
ca: true
```

The framework will automatically use `inspec_inputs.yml` as the InSpec Inputs data.

## <a id="git" name="git"></a>Committing to Git

### Commit and Push the Code

A Git repository is a virtual storage of your project.

- If you need to setup authentication with the Git server
  - Run `git config --global user.name <name>` to set up your Git username for all commits
  - Run `git config --global user.email <email>` to set up your Git email for all commits
  - Run `ssh-keygen -t rsa -C "<email>" -P "" -q -f ~/.ssh/git_rsa` to generate a ssh key pair
    - It generates two keys:
      - Private key `~/.ssh/git_rsa`
      - Public key `~/.ssh/git_rsa.pub`
  - Register the public key `~/.ssh/git_rsa.pub` in the Git server
  - Update the local `~/.ssh/config` file with this section

  ```sh
    Host <the Git host>
      AddKeysToAgent yes
      PreferredAuthentications publickey
      IdentityFile ~/.ssh/git_rsa
  ```

- Create a private Git repository on the Git server
  - The repository name should match the generated application name (e.g. `clientname-myapp-pipeline`)
  - The remote URL will be used in one of the steps below as `<remote_repo_url>`
  - Open a shell prompt in the newly-generated code directory
  - Run `git init` It will create an empty Git repository
  - Run `git add .` it will stage all files in the directory
  - Run `git commit -m "Initial Commit"` it will commit all staged files
  - Run `git remote add origin <remote_repo_url>` it will set up the upstream branch for the local branches
  - Run `git push -u origin develop` it will push the local commit to the remote develop branch

## <a id="additional" name="additional"></a>Additional Commands

Following are some additional commands that you can use in the project:

- To Check your configuration, use `rake -T`
- To create an unencrypted AMI, use `rake build` 
- To run InSpec test suite and compliance scans, use `rake test` 
- To create the encrypted AMI,use `rake deliver` 