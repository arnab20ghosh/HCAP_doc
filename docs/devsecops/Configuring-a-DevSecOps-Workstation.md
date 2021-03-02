---
title: Configure a DevSecOps Workstation 
---
# <a id="dev" name="dev"></a>Configure a DevSecOps Workstation 

You must first configure a machine for creating a DevSecOps project, and then building and testing the pipelines created in that project. 

The configuration of a DevSecOps workstation can be done on a Linux/ Unix, or a Mac machine, and for a Windows machine you need to install a Linux Virtual Machine(VM).

## <a id="pre" name="pre"></a>Prerequisites

Before you start with the configuration of the workstation, following are the prerequisites:

1. You have access to an active AWS Account.
2. You know how to launch an EC2 instance in AWS.
3. You have the following details of your AWS Account:
   - AWS Account ID
   - AWS Access Key
   - AWS Secret Key
   - VPC-ID
   - Subnet-ID
   - Security Groups for SSH and egress
   - SSH key to login
   - Bastion host (if key is deployed on a private subnet)
   - Bastion key
4. You have an Artifactory account created for you. 
5. You have the following Artifactory details:
   - Artifactory URL
   - Artifactory user name
   - Artifactory API key

> Notes
>
> - You need an Artifactory API Key and Artifactory username for configuring your system to use artifactory.
> - You need an Artifactory DNS for downloading packages from the artifactory and installing them on your workstation.

##  <a id="overview" name="overview"></a>Configure your workstation: Linux or Unix

The Linux configuration can be done using in one of the following options:

1. <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-devsecops', viewPage: 'configure-workstation', viewSection: 'dock'})" style="text-decoration:none">Using the **dev_env** docker container</a>
2. <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-devsecops', viewPage: 'configure-workstation', viewSection: 'con-scrtch'})" style="text-decoration:none">Configuring workstation from scratch</a>

### <a id="dock" name="dock"></a>Using the **dev_env** docker container

The dev_env docker container contains all the prerequisites setup required for the DevSecOps workstation. This configuration process has the following steps:

1. <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-devsecops', viewPage: 'configure-workstation', viewSection: 'docker'})" style="text-decoration:none">Download and install docker engine</a>
2. <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-devsecops', viewPage: 'configure-workstation', viewSection: 'set-env'})" style="text-decoration:none">Setup environment variable for private docker repository</a>
3. <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-devsecops', viewPage: 'configure-workstation', viewSection: 'dev-env'})" style="text-decoration:none">Download the dev_env docker image</a>
4. <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-devsecops', viewPage: 'configure-workstation', viewSection: 'doc-img'})" style="text-decoration:none">Launch the docker image</a>
5. <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-devsecops', viewPage: 'configure-workstation', viewSection: 'gem-src'})" style="text-decoration:none">Update gem sources an`d bundle configuration</a>

#### <a id="docker" name="docker"></a>Download and install docker engine 

Install the **Docker Engine - Community** for CentOS. For information on how to install Docker, see [Docker Engine Documentation](https://docs.docker.com/install/linux/docker-ce/centos/).

#### <a id="set-env" name="set-env"></a>Set environment variable for private docker repository

After downloading and installing the docker engine, set the private artifactory URL to an environment variable.

To create environment variables, it is recommended to use `direnv`, which can provide project specific functionality. To learn more about `direnv`, in the Learn the Concepts section, see <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-devsecops', viewPage: 'learn-the-concept', viewSection: 'direnv'})" style="text-decoration:none">Managing Environment Variables with direnv</a>

If you have not installed `direnv`, then use the `export  VARIABLE_NAME=value` command to get the private docker registry repository. Add the registry location with the repository name. The docker environment variable `DOCKER-REPO` will be based off the Artifactory DNS.

Example of using this format for an artifactory URL is shown below:

```
export DOCKER-REPO=virtual-docker-reanplatform.<Artifactory DNS>
```

#### <a id="dev-env" name="dev-env"></a>Download the dev_env docker image

Use your artifactory credentials to download the docker image (dev_env) from the artifactory

- Login to the artifactory-based docker registry with the artifactory credentials:

```bash
# login into to docker registry with read-only credentials
  docker login $DOCKER-REPO
```

- Enter your artifactory username and password after running the login command.

- Pull the docker image

```bash
# pull the dev_env image
docker pull $DOCKER-REPO/reanplatform-builder_image:latest
```

#### <a id="loc-dir" name="loc-dir"></a>Mount the local directories

Before running the docker image you have to mount the directories.

We recommend using two locations. All binaries and any other install related files are in one location and all platform repos are in another location.
   In the example below we are mounting the binaries to `/opt/scratch` and the platform repos to `/opt/media`.

```
docker run -it -d -v <local-directory>/opt/media:Z -v <local-directory>/opt/scratch:Z $DOCKER-REPO/reanplatform-builder_image:latest /bin/bash --login
```


#### <a id="doc-img" name="doc-img"></a>Launch the docker image

Once you start the container you can login anytime using following command:

```bash
# to get the list of running container
docker ps

# get the container-id of the dev_env and then login into it
docker exec -it <container-id> /bin/bash
```

All required DevOps tools are already installed in the `dev_env` docker image.

#### <a id="gem-src" name="gem-src"></a>Update your gem sources and bundle config

The following steps must be followed inside the docker container:

- Configure Gem sources to use the Artifactory **rubygems** repo

```
gem source -a https://<USERNAME>:<API_KEY>@<Artifactory DNS>/artifactory/api/gems/virtual-rubygems/
```

- Remove the community gem repo

```
gem sources -r https://rubygems.org
```

- Run the command to setup your gem tool

```
curl -u<USERNAME>:<API_KEY> https://<Artifactory DNS>/artifactory/api/gems/virtual-rubygems/api/v1/api_key.yaml > ~/.gem/credentials	
```

- Configure bundler

```
bundle config mirror.https://rubygems.org https://<USERNAME>:<API_KEY>@<Artifactory DNS>/artifactory/api/gems/virtual-rubygems/
```

### <a id="con-scrtch" name="con-scrtch"></a>Configuring workstation from scratch

The following instructions are applicable to RedHat compatible Linux distributions.

To configure the Linux workstation from scratch use the following steps:

1. <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-devsecops', viewPage: 'configure-workstation', viewSection: 'yum'})" style="text-decoration:none">Update Yum configuration</a>
2. <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-devsecops', viewPage: 'configure-workstation', viewSection: 'pip'})" style="text-decoration:none">Install Python-pip</a>
3. <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-devsecops', viewPage: 'configure-workstation', viewSection: 'cli'})" style="text-decoration:none">Install AWS CLI</a>
4. <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-devsecops', viewPage: 'configure-workstation', viewSection: 'aws-cli'})" style="text-decoration:none">Configure AWS CLI</a>
5. <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-devsecops', viewPage: 'configure-workstation', viewSection: 'chefdk'})" style="text-decoration:none">Install ChefDK</a>
6. <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-devsecops', viewPage: 'configure-workstation', viewSection: 'packer'})" style="text-decoration:none">Install Packer</a>
7. <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-devsecops', viewPage: 'configure-workstation', viewSection: 'terr'})" style="text-decoration:none">Install Terraform </a>
8. <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-devsecops', viewPage: 'configure-workstation', viewSection: 'git'})" style="text-decoration:none">Install Git</a>
9. <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-devsecops', viewPage: 'configure-workstation', viewSection: 'bun-bash'})" style="text-decoration:none">Configure bundle and bash profile</a>
10. <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-devsecops', viewPage: 'configure-workstation', viewSection: 'rvm'})" style="text-decoration:none">Install Ruby with RVM</a>
11. <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-devsecops', viewPage: 'configure-workstation', viewSection: 'gem-src'})" style="text-decoration:none">Configure Gem sources</a>
12. <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-devsecops', viewPage: 'configure-workstation', viewSection: 'bundler'})" style="text-decoration:none">Configure Bundler</a>
13. <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-devsecops', viewPage: 'configure-workstation', viewSection: 'python'})" style="text-decoration:none">Configure Python</a>

#### <a id="yum" name="yum"></a>Update Yum Configuration	

You must use the Artifactory to install the yum packages.

To resolve _.rpm_ files using the yum client, edit or create the _artifactory.repo_ file with root privileges:

```
sudo vi /etc/yum.repos.d/artifactory.repo
```

update file with following contents:

```bash
[Artifactory]
name=Artifactory
baseurl=https://<URL_ENCODED_USERNAME>:<PASSWORD>@<Artifactory DNS>/artifactory/virtual-yum-rhel7
enabled=1
gpgcheck=0
```

#### <a id="pip" name="pip"></a>Install Python-pip

Python-pip is the standard package manager for Python. If you don't have Python 3, please use instructions below to install:

- Python Installation in CentOS/RHEL:

```bash
sudo yum update
sudo yum install -y python36u python36u-libs python36u-devel python36u-pip
python3.6 -V
```

- Installation of Python-pip:

```bash
curl -O https://bootstrap.pypa.io/get-pip.py
# if you are using python2.X
python get-pip.py --user

# if you are using python 3.X
python3 get-pip.py --user
export PATH=~/.local/bin:$PATH
source ~/.bash_profile
```

- Test to verify if `pip` is installed correctly.

```bash
pip3 --version
```

#### <a id="cli" name="cli"></a>Install AWS CLI 

AWS CLI is required to execute AWS commands. Use the following command to install AWS CLI:

```bash
pip3 install awscli --upgrade --user
```

When you use the `--user` switch, `pip` installs the AWS CLI to `~/.local/bin`.

Verify that the AWS CLI installed correctly.

```bash
$ aws --version
aws-cli/1.16.116 Python/3.6.8 Linux/4.14.77-81.59-amzn2.x86_64 botocore/1.12.106
```

#### <a id="aws-cli" name="aws-cli"></a>Configure AWS CLI

After AWS CLI is installed, configure AWS credentials using the command below.


```bash
# Command to configure AWS credentials
aws configure --profile <account-name>
AWS Access Key ID [None]: <your access key ID>
AWS Secret Access Key [None]: <your secret key>
Default region: <Region of AWS>
Default output format [None]: < we prefer `json` >
```

#### <a id="chefdk" name="chefdk"></a>Install ChefDK

```bash
 sudo yum -y install chefdk	
```

#### <a id="packer" name="packer"></a>Install Packer

To Learn more about Packer, in the Learn the Concepts topic, see <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-devsecops', viewPage: 'learn-the-concept', viewSection: 'packer'})" style="text-decoration:none">Building with Packer</a>

- Use wget to install packer:

```bash
wget https://<Artifactory DNS>/artifactory/virtual-misc/packer/1.4.3/packer_1.4.3_linux_amd64.zip
tar -zxvf packer_1.4.3_linux_amd64.zip
chmod +x packer
sudo mv packer /usr/bin
```

#### <a id="terr" name="terr"></a>Install Terraform

To Learn more about Terraform, in the Learn the Concepts topic, see <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-devsecops', viewPage: 'learn-the-concept', viewSection: 'inspec'})" style="text-decoration:none">Testing with Terraform and InSpec</a>.

Use the following commands to install Terraform:

```bash
wget https://<Artifactory DNS>/artifactory/virtual-misc/terraform/0.11.8/terraform_0.11.8_linux_amd64.zip
tar -zxvf terraform_0.11.8_linux_amd64.zip
chmod +x terraform
sudo mv terraform /usr/bin

# installing terraform providers
wget https://<Artifactory DNS>/artifactory/virtual-misc/terraform-provider-aws/2.25.0/terraform-provider-aws_v2.25.0_x4
wget https://<Artifactory DNS>/artifactory/virtual-misc/terraform-provider-external/1.0.0_x4/terraform-provider-external_v1.0.0_x4
wget https://<Artifactory DNS>/artifactory/virtual-misc/terraform-provider-helm/0.10.2/terraform-provider-helm_v0.10.2_x4
wget https://<Artifactory DNS>/artifactory/virtual-misc/terraform-provider-kubernetes/1.8.1/terraform-provider-kubernetes_v1.8.1_x4
wget https://<Artifactory DNS>/artifactory/virtual-misc/terraform-provider-local/1.3.0/terraform-provider-local_v1.3.0_x4
wget https://<Artifactory DNS>/artifactory/virtual-misc/terraform-provider-null/1.0.0_x4/terraform-provider-null_v1.0.0_x4
wget https://<Artifactory DNS>/artifactory/virtual-misc/terraform-provider-template/1.0.0_x4/terraform-provider-template_v1.0.0_x4
chmod +x terraform-provider-*
mv terraform-provider-* /usr/local
```

#### <a id="git" name="git"></a>Install Git

Git is used for version control. To install git, run the command:

```
sudo yum -y install git
```

#### <a id="bun-bash" name="bun-bash"></a>Configure bundler and bash profile

Configure bundler and bash profiles with Artifactory credentials. Configure the bash profile with (file: ~/.bash_profile) Supermarket URL, Artifactory API KEY, Artifactory Username

```bash
export supermarket_url=<Artifactory DNS>/artifactory/webapp/api/chef/virtual-supermarket
export artifactory_username=<Artifactory Username>
export artifactory_api_key=<Artifactory API Key>
```

#### <a id="rvm" name="rvm"></a>Install Ruby with RVM

```bash
wget https://<Artifactory DNS>/artifactory/virtual-misc/rvm/1.29.3/rvm-1.29.3.tar
mkdir rvm && cd rvm
tar --strip-components=1 -xzf ../rvm-stable.tar.gz
./install --auto-dotfiles
source ~/.rvm/scripts/rvm
wget https://<Artifactory DNS>/artifactory/virtual-misc/ruby/2.5.7/ruby-2.5.7.tar.bz2

# Save these packages for offline use by storing them in the rvm archive folder
$rvm_path/archives/

# An alternate archive folder can be specified in the .rvmrc file
echo rvm_archives_path=/path/to/tarballs/ >> ~/.rvmrc

# Disable automatic dependencies ("requirements") fetching: rvm autolibs read-fail
# Clean default gems:
echo "" > ~/.rvm/gemsets/default.gems

# Clean global gems:
echo "" > ~/.rvm/gemsets/global.gems

rvm install 2.5.7 #  (this may require sudo password for autolibs)

# Set default Ruby version:
rvm use 2.5.7 --default

# Restart your terminal for RVM to work
```

#### <a id="gem-src" name="gem-src"></a>Configure Gem sources

- Configuring Gem sources to use Artifactory.

```
gem source -a https://$artifactory_username:$artifactory_api_key@<Artifactory DNS>/artifactory/api/gems/virtual-rubygems/
```

- To remove the community gem repo, use:

```
gem sources -r https://rubygems.org
```

- If you want to setup the credentials for your gem tool either include your API*KEY in the `~/.gem/credentials` file, or run the following command:

```
curl -u$artifactory_username:$artifactory_api_key https://<Artifactory DNS>/artifactory/api/gems/virtual-rubygems/api/v1/api_key.yaml > ~/.gem/credentials
```


#### <a id="bundler" name="bundler"></a>Configure Bundler

Execute the command in the terminal to mirror the system to use real-artifactory

```
bundle config mirror.https://rubygems.org https://$artifactory_username:$artifactory_api_key@supermarket_url
```


#### <a id="python" name="python"></a>Configure Python

Add the following configuration to `~/.pip/pip.conf`

```bash
[global]
index-url = https://$artifactory_username:$artifactory_api_key@<artifactory DNS>/artifactory/api/pypi/virtual-pypi/simple
```

##  <a id="macos" name="macos"></a>Configure your workstation: macOS

### Option 1: Using the dev_env docker container

Download and install [Docker engine](https://hub.docker.com/editions/community/docker-ce-desktop-mac) on your system.

Follow the instructions at <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-devsecops', viewPage: 'configure-workstation', viewSection: 'dock'})" style="text-decoration:none">Using the **dev_env** docker container</a>.

### Option 2: Configuring your workstation from scratch

Install the following tools:

* ChefDK
* Packer
* Terraform
* Brew
* git
* envrc
* AWS-cli
* Python-pip
* AWS-Vault

You must have **administrator** computer privileges to install Brew.

-  **Install Brew by pasting below command in a macOS Terminal prompt**

```
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

- **Install `wget` using homebrew**

```
brew install wget
```

   Installation of packages can be done by using the command or by downloading from official websites of respective packages

- **Download ChefDK from the below link and install it**

   To Install the package go the Downloads folder and double click on the chefdk-3.11.3-1.dmg file. Provide credentials if necessary.

   ```bash
   wget https://<artifactory DNS>/artifactory/virtual-misc/chefdk/3.18.14-1/chefdk-3.11.3-1.dmg ~/Downloads/
   ```

- **Configure version of Ruby that is included in ChefDK**

```bash
# Lets use chef version of ruby and gems for development. It is not compulsory if you know how to play with ruby please use your own methods.
echo 'export PATH="/opt/chefdk/embedded/bin:\$PATH"' >> ~/.bash_profilee && source ~/.bash_profile
```

- **Install AWS CLI to do API calls to AWS**

```bash
# Installing AWS CLI to do API calls to AWS
brew install awscli
```

- **Check if AWS CLI is installed using**

  ```
  aws -—version
  ```

- **Configure AWS credentials using command**

```bash
# Get your AWS access key and secret key from the AWS console
# Command to configure AWS credentials
aws configure --profile <account-name>
AWS Access Key ID [None]: <your access key ID>
AWS Secret Access Key [None]: <your secret key>
Default region name [None]: <select a region ie.. `us-east-1`>
Default output format [None]: < we prefer `json` >
```

*AWS credentials:* _(Put in access key, secret access key, region and format)_

-  **Install packer using brew using the command line**

```bash
# Installing packer which is used to build AMI's
brew install packer
```

-  **Download and install Terraform**


```bash
#download terraform
wget https://releases.hashicorp.com/terraform/0.11.8/terraform_0.11.8_darwin_amd64.zip ~/Downloads/
unzip ~/Downloads/terraform_0.11.8_darwin_amd64.zip
sudo mv ~/Downloads/terraform /usr/local/bin/terraform
# To verify the installation
terraform version
```

- **Install direnv using the brew command**

```bash
# use brew to install direnv
# if you need more information please refer to https://direnv.net/
brew install direnv
```

   Add the following line at the end of the `~/.bash_profile` file and use `direnv allow` to load environment variables for that particular session

```
bash 
eval "$(direnv hook bash)
```

- **Install git**

```bash
brew install git
```
- **Install aws-vault** 

   A better way to login into AWS console and generation of temporary credentials. for more information pleas visit https://github.com/99designs/aws-vault
   
   ```
   brew cask install aws-vault 
   ```
   
   **Configure bundler and bash profile with artifactory credentials**
   
   Configure the bash_profile with (file: ~/.bash_profile) Supermarket url, Artifactory password API, Artifactory Username

```bash
export ARTIFACTORY_USERNAME=<artifactory-username>
export ARTIFACTORY_API_KEY=<artifactory-api-key>
export ARTIFACTORY_ENDPOINT=<artifactory DNS>
export ARTIFACTORY_SUPERMARKET_URL="https://$ARTIFACTORY_USERNAME:$ARTIFACTORY_API_KEY@$ARTIFACTORY_ENDPOINT/artifactory/virtual-supermarket/"
```

> After the Artifactory credentials are added above, you either need to reload the bash_profile or move a directory up and back into the project and type `direnv allow` to load the new ENV variables.

- **Execute the command in the terminal to configure the bundler to use artifactory**

```bash
bundle config mirror.https://rubygems.org "https://$ARTIFACTORY_USERNAME:$ARTIFACTORY_API_KEY@$ARTIFACTORY_ENDPOINT/artifactory/api/gems/virtual-rubygems/"
bundle config mirror.http://rubygems.org "http://$ARTIFACTORY_USERNAME:$ARTIFACTORY_API_KEY@$ARTIFACTORY_ENDPOINT/artifactory/api/gems/virtual-rubygems/"
```

Check if bundler is configured correctly with `bundle config`

- **Configure gems upload and download from the artifactory**

```bash
#For your gem client to upload and download Gems from this repository you need to add it to your ~/.gemrc file using the following command:
gem source -a https://$ARTIFACTORY_USERNAME:$ARTIFACTORY_API_KEY@$ARTIFACTORY_ENDPOINT/artifactory/api/gems/virtual-rubygems/

curl -u$ARTIFACTORY_USERNAME:$ARTIFACTORY_API_KEY https://$ARTIFACTORY_ENDPOINT/artifactory/api/gems/virtual-rubygems/api/v1/api_key.yaml > ~/.gem/credentials

# install framework gems using the command below--note this may take awhile to run
gem install pipeline-tasks
```

- **Install the Python and pip**

```
brew install python
```

- **Configure Python pip**

Add the following configuration to `~/.pip/pip.conf`.


```bash
[global]
index-url = https://<ARTIFACTORY_USERNAME>:<ARTIFACTORY_API_KEY>@<artifactory DNS>/artifactory/api/pypi/virtual-pypi/simple
```

## Configure your workstation: Windows

### <a id="win-doc" name="win-doc"></a>Option 1: Using the dev_env docker container

Download and install [Docker engine](https://hub.docker.com/editions/community/docker-ce-desktop-windows) on your system.

Follow the instructions at <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-devsecops', viewPage: 'configure-workstation', viewSection: 'dock'})" style="text-decoration:none">Configure the dev_env container</a>.

### <a id="overview" name="overview"></a>Option 2: Using a Linux virtual machine

The configuration of DevSecOps can be done on a Linux/ Unix, or a Mac machine, and for a Windows machine you need to install a Linux Virtual Machine(VM). For more information on installation of Linux VM, see <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-devsecops', viewPage: 'linux-virtual', viewSection: 'win-lin'})" style="text-decoration:none">Windows Linux Virtual Machine</a>.

### Configure your Linux workstation

In the **Configure your Workstation** section, follow the instructions in <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-devsecops', viewPage: 'configure-workstation', viewSection: 'con-scrtch'})" style="text-decoration:none">Configuring workstation from scratch</a>.

### Additional resources

- [VirtualBox](https://www.virtualbox.org)
- [How to install CentOS on VirtualBox](https://www.avoiderrors.com/install-centos-7-virtual-box/)
- [VMware workstation](https://www.vmware.com/products/personal-desktop-virtualization.html)
- [VirtualBox Images](https://www.osboxes.org/virtualbox-images/)
- [VMware Images](https://www.osboxes.org/vmware-images/)
