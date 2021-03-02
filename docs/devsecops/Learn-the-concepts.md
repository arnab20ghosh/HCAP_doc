---
title: Learn the concepts
---

# Learn the concepts

## <a id="devops" name="devops"></a>DevOps Concepts

DevOps is the practice of operations and development engineers participating together in the entire service lifecycle, from design through the development process to production support. 

*Continuous Integration (CI)* Continuous Integration (CI) is a development practice that requires developers to integrate code into a shared repository several times a day. Each check-in is then verified by an automated build, allowing teams to detect problems early. 

*Continuous Delivery (CD)* Continuous Delivery is the ability to get changes of all types—including new features, configuration changes, bug fixes and experiments—into production, or into the hands of users, safely and quickly in a sustainable way.

DevOps learning resources:

- [What is DevOps](https://theagileadmin.com/what-is-devops/)
- [More about DevOps](https://aws.amazon.com/devops/what-is-devops/)
- [Continuous Integration](https://www.thoughtworks.com/continuous-integration)
- [Continuous Delivery](https://continuousdelivery.com/)

## <a id="devops" name="devops"></a>DevSecOps Concepts

DevSecOps is the philosophy of integrating security practices within the DevOps process. DevSecOps is about built-in security, not security that functions as a perimeter around apps and data. All people involved in the development process are accountable for security.  

[What is DevSecOps](https://www.redhat.com/en/topics/devops/what-is-devsecops)

## <a id="packer" name="packer"></a> Building with Packer

[Packer](https://packer.io/intro/#what-is-packer-) is a tool for creating machine images for multiple platforms from a single source configuration.

The JSON configuration file used to define what image we want built and how is called a *template* in Packer terminology. The template has one or more [*builders*](https://packer.io/docs/builders/index.html) which are Packer components that are able to create a machine image for a single platform (for example, `amazon-ebs` is the Amazon EC2 AMI builder that ships with Packer). Builders read in some configuration and use that to run and generate a machine image. A builder is invoked as part of a build in order to create the actual resulting images.

Packer learning resources:

- [Packer documentation](https://packer.io/docs/index.html)
- [Learn DevOps: Infrastructure Automation With Terraform](https://hitachivantara.udemy.com/learn-devops-infrastructure-automation-with-terraform/)

## <a id="chef" name="chef"></a> Provisioning with Chef

[Chef](https://docs.chef.io/) is a powerful automation platform that transforms infrastructure into code. You create and test your code on your workstation before you deploy it to other environments.

When you write your code, you use resources to describe your infrastructure. A resource corresponds to some piece of infrastructure, such as a file, a template, or a package. Each resource declares what state a part of the system should be in, but not how to get there. Chef handles these complexities for you. Chef provides many resources that are ready for you to use. You can also utilize resources shipped in community cookbooks, or write your own resources specific to your infrastructure.

Chef learning resources:

- [Basic Chef Fluency Badge](https://linuxacademy.com/cp/modules/view/id/224)
- [Chef Local Cookbook Development Badge](https://linuxacademy.com/cp/modules/view/id/122)
- [Chef Fundamentals: A Recipe for Automating Infrastructure](https://hitachivantara.udemy.com/chef-fundamentals-a-recipe-for-automating-infrastructure/)

## <a id="direnv" name="direnv"></a> Managing Environment Variables with direnv

[Direnv](https://direnv.net/) is an extension for your shell. It augments existing shells with a new feature that can load and unload environment variables depending on the current directory.

To see all the Environment variables available and their values--as well as the one you just created--you can type `printenv` in the terminal. 

If using direnv, you will most likely have to type `direnv allow` after creating the new variable. 

## <a id="inspec" name="inspec"></a> Testing with Terraform and InSpec

[Terraform](www.terraform.io) is a tool for building, changing, and versioning infrastructure safely and efficiently. 

Configuration files describe to Terraform the components needed to run a single application or your entire datacenter. Terraform generates an execution plan describing what it will do to reach the desired state, and then executes it to build the described infrastructure. As the configuration changes, Terraform is able to determine what changed and create incremental execution plans which can be applied.

[Chef InSpec](https://www.inspec.io/docs/) is a free and open-source framework for testing and auditing your applications and infrastructure. Chef InSpec works by comparing the actual state of your system with the desired state that you express in easy-to-read and easy-to-write Chef InSpec code. Chef InSpec detects violations and displays findings in the form of a report, but puts you in control of remediation.

For testing our images, we use Terraform to create temporary resources ([EC2 instances](https://www.terraform.io/docs/providers/aws/r/instance.html)) and [InSpec profiles](https://www.inspec.io/docs/reference/profiles/) to test the resources. 

<!--TODO: In case the user has not visited any other sections before this one, explain to them (briefly) how Terraform is used to create temporary systems to perform tests on, and how Inspec is used to test the contents of those systems.-->

<!--TODO: The user will not need to understand all Terraform concepts and resources in order to perform tests.  Instruct them about which resources we use,and link to documentation on those resources.  Also link to documentation on basic Terraform variable interpolation.-->

<!--TODO: The user will not need to understand basic Inspec testing concepts in order to use inspec tests with these pipelines.  Hyperlink to different documentation sections on the different concepts that they will need to learn.-->

Terraform and InSpec learning resources:

- [Terraform variable interpolation](https://www.terraform.io/docs/configuration-0-11/interpolation.html)
- [Using Terraform to Manage Applications and Infrastructure](https://linuxacademy.com/cp/modules/view/id/358)
- [Learn DevOps: Infrastructure Automation With Terraform](https://hitachivantara.udemy.com/learn-devops-infrastructure-automation-with-terraform/)
- [Compliance Automation with InSpec](https://learn.chef.io/tracks/compliance-automation#/)
- [How to create custom InSpec profiles](https://learn.chef.io/modules/create-a-custom-profile#/)
- [Example InSpec profile](https://github.com/inspec/inspec/tree/master/examples/profile)

## <a id="rake" name="rake"></a> Running builds with Rake

[Rake](https://ruby.github.io/rake/) is a make-like build utility for Ruby with tasks and dependencies specified in standard Ruby syntax.

To see the rake tasks run the following command on the command line.

```shell
bundle exec rake -T
```

We can use rake to execute individual pipeline tasks or to execute rake tasks which have dependencies on other tasks. 

In this example, we are executing one rake task.

```shell
bundle exec rake expire # This task expires machine images built by Packer
```

In this example, we are executing another rake task with a lot of dependencies.

```shell
bundle exec rake test # This task executes pre, post, and actual testing steps
```

In this example, we are executing a rake task in a namespace.

```shell
bundle exec rake build:validate # the namespace is build and the task is validate
```

<!--TODO: In case the user has not visited any other sections before this one, explain to them (briefly) how Rake is used to execute tasks in image pipelines.-->

<!--TODO: The user will not need to understand all Rake concepts and DSL methods in order to develop and run these pipelines.  Instruct them about which rake concepts we use, and link to documentation on those resources.  Also link to basic guides on how to use rake.-->

Rake learning resources:

- [Rake](https://ruby.github.io/rake/)
- [Rakefile](https://ruby.github.io/rake/doc/rakefile_rdoc.html)
- [Rake Namespaces](https://ruby.github.io/rake/doc/rakefile_rdoc.html#label-Namespaces)

## <a id="git-flow" name="git-flow"></a> Understanding git and git flow

[Git](https://git-scm.com/) is a free and open source distributed version control system. 

[Git flow](https://nvie.com/posts/a-successful-git-branching-model/)  is a Git workflow design which defines a strict branching model and it dictates what kind of branches to set up and how to merge them together.

Git flow uses two branches to record the history of the project. The `master` branch stores the official release history, and the `develop` branch serves as an integration branch for features. It's also convenient to tag all commits in the `master` branch with a version number. Each new feature should reside in its own branch, which can be pushed to the central repository for backup/collaboration. But, instead of branching off of `master`, `feature` branches use `develop` as their parent branch. When a feature is complete, it gets merged back into develop. Features should never interact directly with `master`.

![git flow model](/images/rean-devsecops/gitflow-model.png)

Git and Git Flow learning resources:

- [Git](https://git-scm.com/)
- [Git Flow](https://nvie.com/posts/a-successful-git-branching-model/)

## <a id="cloud" name="cloud"></a>Cloud credentials: AWS

The AWS Command Line Interface (AWS CLI) is an open source tool that interacts with AWS services using commands in your command-line shell. 

The easiest way to setup AWS credentials is to run the following command in your shell.

```shell
aws configure
```

TODO: Teach the user how to set up their AWS credentials INI file, and hyperlink them to external documentation about the topic.

TODO: Teach the user about the relevant AWS environment variables to select 

At the very least, the framework needs the following environment variables:

- *AWS_ACCESS_KEY_ID*  - an AWS access key associated with an IAM user or role
- *AWS_SECRET_ACCESS_KEY*  - the "password" for the access key
- *AWS_DEFAULT_REGION* - AWS will send requests to this AWS Region

AWS learning resources:

- [AWS Command Line Interface](https://docs.aws.amazon.com/cli/latest/userguide/cli-chap-welcome.html)
- [Configure the AWS CLI](https://docs.aws.amazon.com/cli/latest/userguide/cli-chap-configure.html#cli-quick-configuration)
- [AWS CLI environment variables](https://docs.aws.amazon.com/cli/latest/userguide/cli-configure-envvars.html)
- [AWS Region](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/using-regions-availability-zones.html#concepts-regions-availability-zones)

## <a id="security" name="security"></a>Security and Compliance: Security Technical Implementation Guide

The Security Technical Implementation Guides (STIGs) contain technical guidance to "lock down" information systems/software that might otherwise be vulnerable to a malicious computer attack.

The framework creates compliance reports by executing the InSpec profiles based on the STIG specifications.

For compliance scanning using stigtool one can write `skip.yml`, `poam.yml`, `filter.yml` and `inspec_attributes.yml`. 

Below we explain what the purpose of using POAM, Skip and Filter are using for when testing STIG specifications.

> **POAM** - Plan of Action and Milestones. A POAM is temporary exclusion in an inspec test.
For example, if Red Hat Linux introduces an error in the latest version of a software package, we may have to downgrade.
This will cause the compliance scan to fail validation because the STIG insists software should be updated.  In order to work around the issue, we would create a POAM for it with an expiration date.  Once the date in the POAM has passed, the InSpec test will fail. 

> **Skip** - InSpec also supports skipping tests entirely.  For example, we rely on Amazon to pass several STIGs regarding datacenter security.  These tests are skipped permanently, and the reason logged.

> **Filter** - Nessus does not support skips and POAMs, instead it uses a filter to exclude tests that are not applicable.

STIGs cover many topics, some of which we rely on Amazon's certification process to cover.  Some STIGs do not apply at all.  For example, we can't check bios settings on an EC2 instance, so we can't validate any bios settings called out in the STIG.  They will never apply, so they can be permanently skipped.   Rather than removing them from the code base and invalidating the comprehensive STIG list we generated, we skip them. 

There are also occasionally temporary conditions that force us to bypass an Inspec test.  If there's an issue with a RedHat package and we have to downgrade it until a patch comes out, the build would fail the Inspec test that mandates the most recent version.  In these situations, we want to skip the check, but we eventually want to run it again.  

In these situations, we create a POAM for it.  A poam looks similar to a skip, but it contains an expiration date.  Both contain approval information and an explanation of why it's in place, which are included in the output 

Skips and POAMs are stored as configuration files in the appropriate `audit` directory of the external configuration.  For example, the base OS RHEL7 packer job skips and POAMs are kept in `rean-pipeline-config/amis/rhel7/baseos/audit/` folder of the `rean-pipeline-config` repo.  

These files are required to skip STIGs if STIGs are not valid or STIGs cause application issues on the machine. 


STIGs learning resources:

- [STIGs](https://public.cyber.mil/stigs/)

## <a id="aws-img" name="aws-img"></a>Network connectivity: AWS image pipelines

If a subnet associated with a route table that has a route to an Internet Gateway, it is known as a *public* subnet. Otherwise, it is a *private* subnet.

AWS networking learning resources:

- [AWS VPCs and Subnets](https://docs.aws.amazon.com/vpc/latest/userguide/VPC_Subnets.html)

## <!-- Remote logins: Linux images -->

<!--TODO: The user will need to understand that remote management of Linux systems is done through SSH.-->

<!--TODO: The user will need to understand which settings in their config.rb and their packer build JSON are used to configure remote logins.-->

<!--TODO: The user will need to understand how remote login configuration is handled for testing phases: how keys are generated and created in the cloud, how the temporary VM is configured to use that configuration, and how the inspec tests use the same configuration.-->

## <!-- Remote logins: Windows images -->

<!--TODO: The user will need to understand that remote management of Linux systems is done through WinRM.  They should also understand the difference between HTTP WinRM (no encryption), and HTTPS WinRM (encryption).-->

<!--TODO: The user will need to understand which settings in their config.rb and their packer build JSON are used to configure remote logins.  They should also understand how the system is able to automatically collect the Administrator password in some cloud setups.-->

<!--TODO: The user will need to understand how EC2 userdata must be used to configure remote management capability for Windows systems on bootup, so that the system is accessible by packer over WinRM.-->

<!--TODO: The user will need to understand how remote login configuration is handled for testing phases: how keys are generated and created in the cloud, how the temporary VM is configured to use that configuration, and how the inspec tests use the same configuration.-->

