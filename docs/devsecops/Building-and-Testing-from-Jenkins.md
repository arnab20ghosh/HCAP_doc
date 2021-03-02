---
title: Build and test from Jenkins
---
# Build and test from Jenkins

#### Contents

- <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-devsecops', viewPage: 'building-jenkins', viewSection: 'jen-fold'})" style="text-decoration:none">Jenkins Folder Structure</a>
- <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-devsecops', viewPage: 'building-jenkins', viewSection: 'config'})" style="text-decoration:none">Configuring AMI Pipelines</a>
  - <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-devsecops', viewPage: 'building-jenkins', viewSection: 'seed-job'})" style="text-decoration:none">About Seed Jobs</a>
  - <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-devsecops', viewPage: 'building-jenkins', viewSection: 'config-seed'})" style="text-decoration:none">Initial Jenkins Configuration for Seed Jobs</a>
  - <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-devsecops', viewPage: 'building-jenkins', viewSection: 'ami-build'})" style="text-decoration:none">Running AMI build</a>
- <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-devsecops', viewPage: 'building-jenkins', viewSection: 'jen-config'})" style="text-decoration:none">Jenkins Configuration</a>

## <a id="jen-fold" name="jen-fold"></a>Jenkins Folder Structure

This section explains how to configure the platform Jenkins instance for running AMI jobs. The platform Jenkins is created and configured by the platform installation process.  

To add these capabilities to other Jenkins instances, see <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-devsecops', viewPage: 'building-jenkins', viewSection: 'jen-config'})" style="text-decoration:none">Jenkins Configuration</a>.   

### Jobs Structure

```tree
.
└── Seed Jobs                         - Folder containing all seed jobs
    ├── baseAmis                      - Platform provided AMIs seed job
    └── amis                          - Standard AMI seed job
```


## <a id="config" name="config"></a>Configuring AMI pipelines

AMI pipelines are used to build, test, and deliver AMIs in an automated way. The pipelines abstracts away the logic and processes required to Build, Test, and Deliver AMIs.

### <a id="seed-job" name="seed-job"></a>About Seed jobs

Seed jobs are Jenkins jobs that create one or more Jenkins jobs. Seeds jobs execute Jenkins Job DSL code.

There are two types of seed jobs available for image pipelines:

#### <a id="platform" name="platform"></a>Platform Seed Jobs

Platform seed jobs are already existing AMI jobs provided by the platform. They include the hardened BaseOS and other AMIs to run the platform. The Platform Seed jobs creates the required pipelines to build, test, and deliver the platform images.

#### <a id="seed" name="seed"></a>Standard Seed Jobs

Standard seed jobs are used to create customer image pipelines. **Pipeline-generator** creates skeleton projects. The standard seed job then creates pipelines for each of the pipeline projects created with the help of the **pipeline-generator** gem.

### <a id="config-seed" name="config-seed"></a>Initial Jenkins Configuration for Seed Jobs

It is necessary to complete the initial Jenkins configuration before creating the Seed jobs. For more information, see <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-devsecops', viewPage: 'building-jenkins', viewSection: 'jen-config'})" style="text-decoration:none">Jenkins Configuration</a>. 

**Following is the list of required Jenkins Plugins:**

- Folders Plugin
- Job DSL
- Environment Injector
- Credentials Binding
- Git
- Pipeline: Job (workflow-job)
- Pipeline

### <a id="plugin" name="plugin"></a>Installing the required plugins

1. Login to Jenkins.

2. On the Jenkins homepage, click **Manage Jenkins**.

   ![jenkins-1](/images/rean-devsecops/jenkins-1.png)

3. Click **Manage Plugins**.

   ![jenkins-34](/images/rean-devsecops/jenkins-34.png)

4. Click **Available** and wait for it to finish loading.

   ![jenkins-35](/images/rean-devsecops/jenkins-35.png)

5. Type the name of the plugin in the search bar **Filter** (e.g.  *environment injector*). Select the plugin in the list of results and click the check mark to the left of the plugin name. Similarly, search for the other plugins and select the check boxes. After installing all required plugins, click on **Download now and install after restart**. 

   ![jenkins-36](/images/rean-devsecops/jenkins-36.png)

7. Select the check box for **Restart Jenkins when installation is complete and no jobs are running**.  Wait for all the plugins to install. The Jenkins will restart itself automatically once all plugins are installed.

   ![jenkins-37](/images/rean-devsecops/jenkins-37.png)

### <a id="config-jen" name="config-jen"></a>Configure Jenkins environment variables

1. On the Jenkins homepage, click **Manage Jenkins**.

   ![jenkins-1](/images/rean-devsecops/jenkins-1.png)

2. Click **Configure System**.

   ![jenkins-2](/images/rean-devsecops/jenkins-2.png)

3. Under **Global Properties**, select the **Environment variables** checkbox and click **Add**.

   ![jenkins-3](/images/rean-devsecops/jenkins-3.png)

   ![jenkins-4](/images/rean-devsecops/jenkins-4.png)

4. Add the **Name** to what is shown in the image below but the value should be your own artifactory values (these values are merely examples). After adding all the values, scroll to the bottom of the page and click **Save**.
   Additionally, STIGTOOL_S3_BUCKET should have the bucket created during installation.

   ![jenkins-global-properties](/images/rean-devsecops/jenkins-global-properties.png)

#### <a id="plat-seed" name="plat-seed"></a>Creating Platform Seed Jobs

1. On the Jenkins homepage, click **New Item**.

   ![jenkins-6](/images/rean-devsecops/jenkins-6.png)

2. Enter the name as **Seed Jobs**, select type **Folder** and click **OK**.

   ![jenkins-7](/images/rean-devsecops/jenkins-7.png)

3. Enter the **Display Name**, **Description** and then click **Save**.

   ![jenkins-8](/images/rean-devsecops/jenkins-8.png)

4. On the Jenkins homepage, click **New Item**.

   ![jenkins-9](/images/rean-devsecops/jenkins-9.png)

5. Enter the data as shown in the image below and click **OK**.

   ![jenkins-10](/images/rean-devsecops/jenkins-10.png)

6. Fill in the **Description**, then select the **This project is parameterized** checkbox, and from the drop-down select **String Parameter**.

   ![jenkins-11](/images/rean-devsecops/jenkins-11.png)

7. Enter the following entries as shown below:

   ![jenkins-12](/images/rean-devsecops/jenkins-12.png)

8. Under **Source Code Management**, enter the details as shown in the image below.

   **Note:** The Git Credentials must be configured as part of Jenkins initial configuration. The **Repository URL** must be updated to the repo URL of **platform-jenkins-customerjobs** in your Git Server

   ![jenkins-13](/images/rean-devsecops/jenkins-13.png)

9. Under the **Build** section, click on **Add build step**, select **Process Job DSLs**.

   ![jenkins-14](/images/rean-devsecops/jenkins-14.png)

10. Select **Look on Filesystem**, under **DSL Scripts**, provide the path as shown below:

    ![jenkins-15](/images/rean-devsecops/jenkins-15.png)

11. Click **Advanced**, the view will expand. Fill in *src/main/jobs* under **Additional classpath** and then click on **Save**.
    _Make sure that **Script Security** is disabled for Job DSL under Jenkins Global Security_

    ![jenkins-16](/images/rean-devsecops/jenkins-16.png)

#### <a id="run-seed" name="run-seed"></a>Running Platform Seed jobs

1. On the Jenkins homepage, click **Seed Jobs**.

   ![jenkins-17](/images/rean-devsecops/jenkins-17.png)

2. Click **baseAMIs**.

   ![jenkins-18](/images/rean-devsecops/jenkins-18.png)

3. Click **Build with Parameters**.

   ![jenkins-19](/images/rean-devsecops/jenkins-19.png)

4. Enter the following details:

   - **extraEnvVars** - Any extra environmental variables to be added to the created jobs, keep empty if not needed.
   - **configRepo** - *External configuration repository* in your Git server.
   - **branch** - The branch to pull the seed job logic from.

5. Click **Build**.

   ![jenkins-20](/images/rean-devsecops/jenkins-20.png)

6. On the Jenkins UI, there should be a folder named **AMIs**.

   ![jenkins-21](/images/rean-devsecops/jenkins-21.png)

#### <a id="stan-seed" name="stan-seed"></a>Creating standard Seed Job

1. On the Jenkins homepage, click **Seed Jobs**.

   ![jenkins-17](/images/rean-devsecops/jenkins-17.png)

2. Click **New Item**.

   ![jenkins-22](/images/rean-devsecops/jenkins-22.png)

3. Enter an item name, select **Freestyle** **project** and click **OK**.

   ![jenkins-23](/images/rean-devsecops/jenkins-23.png)

4. Fill in the job **Description** and fill in the job parameters as shown in the image below.

   ![jenkins-24](/images/rean-devsecops/jenkins-24.png)

5. Scroll down to the **Source Code Management** section and fill in the details as shown below:

6. **Note**: _The Git Credentials must be configured as part of Jenkins initial configuration. The **Repository URL** needs to be updated to the repo URL of **platform-jenkins-customerjobs** from your Git Server._

   ![jenkins-25](/images/rean-devsecops/jenkins-25.png)

7. Under the **Build** section, click **Add build step****, select **Process Job DSLs**.

   ![jenkins-14](/images/rean-devsecops/jenkins-14.png)

8. Fill in the config as below and then click **Advanced**.

   ![jenkins-26](/images/rean-devsecops/jenkins-26.png)

9. Add the **Additional classpath** as *src/main/jobs*. Scroll to the bottom of the page and click **Save**.

   ![jenkins-27](/images/rean-devsecops/jenkins-27.png)

#### <a id="run-seed" name="run-seed"></a>Running standard Seed Job

1. On the Jenkins homepage, click **Seed Jobs**.

   ![jenkins-17](/images/rean-devsecops/jenkins-17.png)

2. Click **ami**.

   ![jenkins-28](/images/rean-devsecops/jenkins-28.png)

3. Click **Build with Parameters**.

   ![jenkins-29](/images/rean-devsecops/jenkins-29.png)

4. Enter the following details that are applicable to the build:

   - **application** - The name of the application. Can be separated into folders by using `/`
   - **appName** - Human readable application name
   - **sourceCodeRepo** - The Git repository that holds the application source code
   - **sourceCodeCredsId** - Jenkins credentials id that has the remote git user credentials
   - **configRepo** - *External configuration repository* in your Git server.
   - **extraEnvVars** - extra environmental variables to be added to the created jobs, keep empty if not needed.
   - **branch** - The branch to pull the seed job logic from.

5. Click **Build**.

   ![jenkins-30](/images/rean-devsecops/jenkins-30.png)

6. On the Jenkins homepage, click **AMIs**.

   ![jenkins-21](/images/rean-devsecops/jenkins-21.png)

7. Click the**Rhel7** folder.

   ![jenkins-31](/images/rean-devsecops/jenkins-31.png)

8. Click the **ColdFusion** folder.

   ![jenkins-32](/images/rean-devsecops/jenkins-32.png)

   The ColdFusion folder must contain three sub-folders AdHoc, Develop, and Release.

   ![jenkins-33](/images/rean-devsecops/jenkins-33.png)

### <a id="ami-build" name="ami-build"></a>Running AMI builds

#### <a id="folder" name="folder"></a>AMI jobs folder structure

```tree
.
└── amis                              - Top level folder containing all AMIs jobs.
    └── rhel7                         - OS specific images
        └── baseos                    - A version of the OS specific image pipeline supporting different environments
            ├── adhoc                 - Adhoc AMI jobs
            │   └── Build             - Adhoc has only build, this is purely for testing purposes before pull requests are merged to develop
            ├── dev                   - Development AMI jobs (daily CI and development purposes).
            │   ├── Build             - Builds an image, optionally running tests and compliance scans.
            │   └── Deliver           - Creates encrypted copies of the image and copies to workload accounts.
            └── prod                  - Production AMI jobs (production AMIs releases).
                ├── Start             - Cuts a release branch from develop
                ├── Build             - Build the source code of release branch and rollback if anything fails
                ├── Finish            - Finish the release process by merging the release branch to master and publishing source code and manifests to artifactory
                └── Deliver           - Creates encrypted copies of the image in workload accounts
```

#### <a id="ami-job" name="ami-job"></a>Running AMI jobs

1. On the Jenkins homepage, click **AMIs**.

   ![jenkins-38](/images/rean-devsecops/jenkins-38.png)

2. To build *RHEL* based images, click **RHEL 7.x**. (The steps for any other images types are similar.)

   ![jenkins-39](/images/rean-devsecops/jenkins-39.png)

3. To build a baseOS image, click **BaseOS**.

   ![jenkins-40](/images/rean-devsecops/jenkins-40.png)

4. Select one of the three pipelines:

   - **Ad-Hoc**: Used for testing changes in image builds without delivering them from an arbitrary SCM branch and from any arbitrary external configuration SCM branch.
   - **Develop**: Used for building and delivering images from the develop branch of SCM.
   - **Release**: Used for creating a release branch, building from that branch and releasing a new version and then delivering the image.

> The folder structure for these folders is explained at [Image jobs folder structure](#ami-jobs-folder-structure).

#### <a id="ad-hoc" name="ad-hoc"></a>Running Ad-Hoc pipeline

1. Click **Ad-Hoc**.

   ![jenkins-41](/images/rean-devsecops/jenkins-41.png)

2. Click **Build**.

   ![jenkins-44](/images/rean-devsecops/jenkins-44.png)

3. Click **Build with Parameters**.

   ![jenkins-45](/images/rean-devsecops/jenkins-45.png)

4. Enter the following details, and click **Build**.

   | Value             | Description                                           |
   | ----------------- | ----------------------------------------------------- |
   | branch            | The SCM branch for the pipeline repository            |
   | pipelineEnv       | The environment tag to use for the launched instances |
   | pipelineConfigRef | The SCM branch for the external config repository     |

   ![jenkins-46](/images/rean-devsecops/jenkins-46.png)

##### <a id="develop" name="develop"></a>Running Develop Pipeline

1. Click **Develop**.

   ![jenkins-42](/images/rean-devsecops/jenkins-42.png)

2. Click **Build**.

   ![jenkins-47](/images/rean-devsecops/jenkins-47.png)

3. Click **Build Now**. This will build the image and after a successful run it will automatically trigger the **Deliver** job.

   ![jenkins-48](/images/rean-devsecops/jenkins-48.png)

##### <a id="release" name="release"></a>Running Release Pipeline

1. Click **Release**.

   ![jenkins-43](/images/rean-devsecops/jenkins-43.png)

2. Click **Start**.

   ![jenkins-49](/images/rean-devsecops/jenkins-49.png)

3. Click **Build Now**.

   ![jenkins-50](/images/rean-devsecops/jenkins-50.png)

4. After a successful run of the **Start** job, the subsequent jobs will be started automatically.

   | Job     | Description                                                  |
   | ------- | ------------------------------------------------------------ |
   | Start   | Creates a release branch from the develop branch             |
   | Build   | Builds the image from the created release branch             |
   | Finish  | Finishes the release and merges the release branch into master and bumps the version in develop branch |
   | Deliver | Delivers the images to respective accounts                   |

## <a id="jen-config" name="jen-config"></a>Jenkins Configuration

> The below steps only needs to be performed if your Jenkins is not configured using the Jenkins bootstrap.

This section provides instructions how to enhance existing Jenkins with the platform capabilities.

**Prerequisites**:

JENKINS_HOME directory is used to provide disk space for builds and archives. JENKINS_HOME is an environment variable.
The value of JENKINS_HOME is available in the Jenkins configuration screen (`Manage Jenkins\Configure System`).

**Artifactory**

- Artifactory DNS: This is the URL of artifactory where you will download and install packages from.
- Artifactory UserName: This is the username to authenticate artifactory.
- Artifactory Password: This is the Password to authenticate artifactory.

**Git Server**

- Git server DNS
- Git server credentials

**Installation and configuration instructions**:

1. Configuring REAN Platform Artifactory repo to download packages

   To resolve _.rpm_ files using the YUM client, edit or create the _artifactory.repo_ file with root privileges:

   `sudo vi /etc/yum.repos.d/artifactory.repo`

   update file with following contents:

   ```bash
   [Artifactory]
   name=Artifactory
   baseurl=https://<URL_ENCODED_USERNAME>:<PASSWORD>@<Artifactory DNS>/artifactory/virtual-yum-rhel7
   enabled=1
   gpgcheck=0
   ```

2. Installing necessary yum packages

   1. Some yum packages are pre-requisites for jenkins.
   2. command to install package wget `sudo yum -y install wget`
   3. command to install package git `sudo yum -y install git`
   4. command to install package jq `sudo yum -y install jq`
   5. command to install package maven `sudo yum -y install maven`

3. Python

   If you don't have Python 3, please use instructions below to install it

   ```bash
   sudo yum update
   sudo yum install -y python36u python36u-libs python36u-devel python36u-pip
   python3.6 -V
   ```

4. python-pip

   pip is the standard package manager for Python.

   ```bash
   curl -O https://bootstrap.pypa.io/get-pip.py
   # if you are using python2.X
   python get-pip.py --user
   # if you are using python 3.X
   python3 get-pip.py --user
   export PATH=~/.local/bin:$PATH
   source ~/.bash_profile
   ```

   Now you can test to verify that `pip` is installed correctly.

   ```bash
   pip3 --version
   ```

5. AWS CLI

   This is required for executing AWS commands.

   ```bash
   pip3 install awscli --upgrade --user
   ```

   When you use the `--user` switch, `pip` installs the AWS CLI to `~/.local/bin`.

   Verify that the AWS CLI installed correctly.

   ```bash
   $ aws --version
   aws-cli/1.16.116 Python/3.6.8 Linux/4.14.77-81.59-amzn2.x86_64 botocore/1.12.106
   ```

   AWS CLI configuration after AWS CLI is installed, configure AWS credentials using the command below.

   ```bash
   # Command to configure AWS credentials
   aws configure --profile <account-name>
   AWS Access Key ID [None]: <your access key ID>
   AWS Secret Access Key [None]: <your secret key>
   Default region: <Region of AWS>
   Default output format [None]: < we prefer `json` >
   ```

6. Installing necessary jenkins plugins.

   Please see below for the list of required Jenkins plugins. You should have Jenkins admin permissions to install the plugins.
   You have to navigate to `Manage Jenkins` and then select `Manage Plugins`. On the menu tab, please select `Available`. You will see a small filter on the top right below the username (not the filter to the lest of the username). Paste the plugins one by one and then install them. Some plugins need Jenkins restarts (make sure no jobs are running). You may find some plugins are already installed just skip them or update them if you think they are old.

   ```bash
   ansicolor
   build-name-setter
   build-with-parameters
   cloudbees-folder
   config-file-provider
   configuration-as-code
   configuration-as-code-support
   copyartifact
   credentials
   credentials-binding
   doclinks
   envinject
   git
   github
   greenballs
   htmlpublisher
   htmlresource
   job-dsl
   jobConfigHistory
   matrix-auth
   multiple-scms
   parameterized-trigger
   plain-credentials
   role-strategy
   RubyMetrics
   rvm
   ssh-agent
   ssh-credentials
   workflow-aggregator
   workflow-aggregator
   ws-cleanup
   ```

7. Installing Terraform.

   ```bash
   wget https://<Artifactory DNS>/artifactory/virtual-misc/terraform/0.11.8/terraform_0.11.8_linux_amd64.zip
   tar -zxvf terraform_0.11.8_linux_amd64.zip
   chmod +x terraform
   sudo mv terraform /usr/bin
   ```

8. Installing Terraform Providers.

   ```bash
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

9. Installing Packer

   ```bash
   wget https://<Artifactory DNS>/artifactory/virtual-misc/packer/1.4.3/packer_1.4.3_linux_amd64.zip
   tar -zxvf packer_1.4.3_linux_amd64.zip
   chmod +x packer
   sudo mv packer /usr/bin
   ```

10. Installing RVM

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
       ```

11. Configuring RubyGems

       ```bash
    # add new gem source as artifactory
    gem source -a https://<USERNAME>:<API_KEY>@<Artifactory DNS>/artifactory/api/gems/virtual-rubygems/
    
    # remove community gem server
    gem sources -r https://rubygems.org
    
    # Configure jenkins to release gems into artifactory
    curl -u<USERNAME>:<API_KEY> https://<Artifactory DNS>/artifactory/api/gems/virtual-rubygems/api/v1/api_key.yaml > ~/.gem/credentials
    
    #  Configure bundle to use artifactory gem repo
    bundle config mirror.https://rubygems.org https://<USERNAME>:<API_KEY>@<Artifactory DNS>/artifactory/api/gems/virtual-rubygems/
    
       ```

12. Installing ChefDk

       ```bash
       sudo yum -y install chefdk
       ```

13. Configure Knife

    Knife is a command-line tool providing communications between the local chef-repo and the Chef server.

       ```bash
       sudo su tomcat -
       cd $TOMCAT_HOME
       mkdir .chef
       touch ./.chef/knife.rb
       # update following env vars and update it
       export $ARTIFACTORY_USER='< update with your artifactory user account >'
       export $ARTIFACTORY_KEY='< update with you artifactory password >'
       export $ARTIFACTORY_DNS='< update with artifactory dns eg.. artifactory.reancloud.com >'
       export $SUPERMARKET_REPO='< virtual supermarket repo name >'
       echo "knife[:supermarket_site]="https://$ARTIFACTORY_USER:$ARTIFACTORY_KEY@$ARTIFACTORY_DNS/api/chef/$SUPERMARKET_REPO" > ./.chef/knife.rb
       echo "knife[:cookbook_path]= ['.', '..', './cookbooks', '~/cookbooks']" >> ./.chef/knife.rb
       ```

14. Configure Git

       ```bash
       # create a .gitconfig file in the Jenkins Home
    
       cd $JENKINS_HOME
       touch .gitconfig
    
       # add content below to that file
       # This is Git's per-user configuration file.
       [user]
       name = < Jenkins Git User Name >
       email = < Jenkins Email Account >
       ```

15. Install REAN-platform CLI

       ```bash
       gem install reanplatform-tools
       ```

16. Install Radar publisher

       ```bash
       wget $ArtifactoryURL/virtual-misc/<PATH to RADAR Publisher>/radar-publisher.hpi
       cp radar-publisher.hpi $JENKINS_HOME/plugins/radar-publisher.hpi
    
       # restart tomcat or jenkins service
    
       # restart tomcat service
       sudo systemctl tomcat restart
    
       # If jenkins is installed with embedded tomcat
       sudo systemctl jenkins restart
       ```

17. Installing kubernetes client.

       ```bash
    # download kubectl CLI tools from Artifactory
    wget $ARTIFACTORY_URL/virtual-misc/KUBECTL-PATH/kubectl_<insert latest VERSION>
    sudo cp kubectl_<insert latest VERSION> /usr/local/bin/kubectl
       ```

18. Installing HELM Package

       ```bash
    # download desired version of HELM
    wget  $ArtifactoryURL/virtual-misc/<HELM Path>/helm-v<insert latest VERSION>-linux-amd64.tgz 
    
    tar -zxvf helm-v<insert latest VERSION>-linux-amd64.tgz
    
    mv linux-amd64/helm /usr/local/bin/helm
       ```

19. Post Install configuration credentials setup

    Git Credentials Setup, add your GIT credentials for your GIT server with the global scope.

    ![git-creds](/images/rean-devsecops/git-creds-image.png)

20. Setup ENV Vars for Jenkins Global Properties.

       ```bash
       ARTIFACTORY_ENDPOINT
       ARTIFACTORY_INSPEC_URL
       ARTIFACTORY_USERNAME
       AWS_DEFAULT_REGION
       AWS_REGION
       ENABLE_NESSUS
       PIPELINE_COLORS
       RUBYGEMS_PUSH_URL
       STIGTOOL_S3_BUCKET   
       ```

    > STIGTOOL_S3_BUCKET should have the bucket created during installation.

    _*ARTIFACTORY_ENDPOINT*, *ARTIFACTORY_INSPEC_URL*, *ARTIFACTORY_USERNAME*, *RUBYGEMS_PUSH_URL* should be configured with values from the customer artifactory._

    > The variable jenkins-global-propertiess should be configured like below.

    **Note: The artifactory values in the image below should be replaced with your artifactory URL**.

    ![](/images/rean-devsecops/jenkins-global-properties.png)

21. Configuring the Jenkins shared library.

22. You have to upload the Jenkins shared library into your version control system (git server).

23. Then you have to configure Jenkins to use it like below.

24. Navigate to **Manage Jenkins --> Configure System**.

25. Update the Global Pipeline Libraries, as shown below.

    ![jenkins-shared-library](/images/rean-devsecops/jenkins-shared-library.png)