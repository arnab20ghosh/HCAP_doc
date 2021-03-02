---
title: Deploy and configure Cloud Accelerator Platform
---

# <a id="deploy"></a>Deploy and configure Cloud Accelerator Platform 
Hitachi Cloud Accelerator Platform can be deployed and configured using bootstrap in both online and offline modes. In the offline mode, Cloud Accelerator Platform does not require Internet connectivity to perform various operations.

For more information about deploying and configuring Cloud Accelerator Platform, contact the Cloud Accelerator Platform team.

<!-- directive
#<a id="summary" name="summary"></a>The containerized deployment of REAN Accelerator Platform includes the following high-level steps:

- <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-platform-common', viewPage: 'deployAndConfigure', viewSection: 'step1'})" style="text-decoration:none">Step 1</a>: Create an AWS EC2 instance and install other required tools, such as Docker, Docker Compose, and AWS CLI.

- <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-platform-common', viewPage: 'deployAndConfigure', viewSection: 'step2'})" style="text-decoration:none">Step 2</a>: Create an EBS volume file, attach it to the EC2 instance, and format the EBS volume file.

- <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-platform-common', viewPage: 'deployAndConfigure', viewSection: 'step3'})" style="text-decoration:none">Step 3</a>: *(Optional)* Create and configure an AWS Relational Database Service (RDS) database instance. 

  Alternatively, you can choose to configure REAN Accelerator Platform to use MySQL in a container.

- <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-platform-common', viewPage: 'deployAndConfigure', viewSection: 'step4'})" style="text-decoration:none">Step 4</a>: Get and extract the REAN Accelerator Platform deployment code.

- <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-platform-common', viewPage: 'deployAndConfigure', viewSection: 'step5'})" style="text-decoration:none">Step 5</a>: Configure the deployment of REAN Accelerator Platform.

- <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-platform-common', viewPage: 'deployAndConfigure', viewSection: 'step6'})" style="text-decoration:none">Step 6</a>: *(Optional)* Configure REAN Deploy.

- <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-platform-common', viewPage: 'deployAndConfigure', viewSection: 'step7'})" style="text-decoration:none">Step 7</a>: *(Optional)* Configure SSL.

- <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-platform-common', viewPage: 'deployAndConfigure', viewSection: 'step8'})" style="text-decoration:none">Step 8</a>: *(Optional)* Configure CA certificates.

- <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-platform-common', viewPage: 'deployAndConfigure', viewSection: 'step9'})" style="text-decoration:none">Step 9</a>: Pull REAN Accelerator Platform Docker images on the EC2 instance.

- <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-platform-common', viewPage: 'deployAndConfigure', viewSection: 'step10'})" style="text-decoration:none">Step 10</a>: Deploy the REAN Accelerators (REAN Deploy, REAN Assess, and REAN Test).

_**Note:** If you update any containers after deploying the REAN Accelerators, you must restart REAN Accelerator Platform. For more information, see <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-platform-common', viewPage: 'administer', viewSection: 'stop-platform'})" style="text-decoration:none">Stopping and restarting REAN Accelerator Platform</a>._

## <a id="step1" name="step1"></a>Step 1: Create an EC2 instance and install other required tools

1. Use the AWS Management Console or the AWS CLI tool to create an IAM role that includes the following permissions:

   ```
   {
      "Version": "2012-10-17",
      "Statement": [
          {
              "Effect": "Allow",
              "Action": [
                  "logs:CreateLogGroup",
                  "logs:CreateLogStream",
                  "logs:PutLogEvents",
                  "logs:DescribeLogGroups",
                  "logs:DescribeLogStreams"
              ],
              "Resource": [
                  "arn:aws-us-gov:logs:*:*:*"
              ]
          }
      ]
   }
   ```

   For information about creating an IAM role, see the [AWS documentation](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_create_for-user.html).

2. Use the AWS Management Console or the AWS CLI tool to create an EC2 instance of the **t2.xlarge** type and attach the role that you have created to this instance.

   The operating system of this instance must be either **RHEL-7 or later (64-bit)** or **Amazon Linux**.

3. On the EC2 instance that you have created, install the following tools:

   - Docker (Community Edition) 17.09-ce or later

     For more information, see [Install Docker](https://docs.docker.com/engine/installation/).

   - Docker Compose 1.21

     For more information, see [Install Docker Compose](https://docs.docker.com/compose/install/).

   - AWS CLI 1.11 or later

     For more information, see [Configure AWS CLI](http://docs.aws.amazon.com/cli/latest/userguide/cli-chap-getting-started.html).

4. For running **Elasticsearch** in a container, set the following system parameters:

   ```
   sudo sysctl -w vm.max_map_count=262144
   sudo sh -c "echo 'vm.max_map_count = 262144' >> /etc/sysctl.conf"
   ```

5. For running dnowcore on RHEL-based system, set the following parameters:

   ```
   grubby --args="namespace.unpriv_enable=1" --update-kernel="$(grubby --default-kernel)"
   cat /proc/cmdline | grep "namespace.unpriv_enable=1"
   echo "user.max_user_namespaces=15076" >> /etc/sysctl.conf
   reboot
   ```

## <a id="step2" name="step2"></a>Step 2: Create, attach, and format the EBS volume file

1. To create an EBS volume file, perform the following actions:

   - In a navigation pane,  Select **EBS volume**.

   - Choose **Create volume**.

   - For Volume type, select volume type as **General Purpose 2**. 

     For more information, see [AWS EBS volume type](http://docs.aws.amazon.com/AWSEC2/latest/UserGuide/EBSVolumeTypes.html).

   - For Size, type the size of the volume.

   - For  Availability zone, select the availability zone in which you have created the instance. 

   - Click on **Create volume**.

2. To attach the EBS volume to the EC2 instance that you have created in Step 1, perform the following actions:

   - In the AWS console, in the navigation pane, select **Volume**.

   - Select a volume and choose **Action** and then **Attach volume**.

   - In the Attach volume dialog box, enter the instance ID or the instance name.

     _**Note:** The availability zone for the instance and EBS volume must be the same._

   - Click on **Attach**.

3. *(Optional)* Format and mount the EBS volume.

   _**Note:** You must format the EBS volume only once. Repeating the formatting results in loss of all the data in the volume._

## <a id="step3" name="step3"></a>Step 3: Create and configure an AWS RDS database instance

This step is optional if you choose to configure REAN Accelerator Platform to use MySQL in a container.

1. Create an AWS RDS database instance.

   For more information, see [Create RDS DB instance](http://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/CHAP_Tutorials.WebServerDB.CreateDBInstance.html).

2. Create a database for the Admin Console (RBAC).

3. Create a database for REAN Deploy.

4. Create a database for REAN Test.

## <a id="step4" name="step4"></a>Step 4: Get and extract the REAN Accelerator Platform deployment code

1. Download the **download.zip** file from <https://github.com/reancloud/REAN-Platform/releases>.

   If you do not have access to this GitHub repository, contact the REAN Cloud team.

2. Extract the **download.zip** file on the EC2 instance.

## <a id="step5" name="step5"></a>Step 5: Configure the deployment of REAN Accelerator Platform

1. On the attached EBS volume, create a data directory for REAN Accelerator Platform.

2. On the EC2 instance, navigate to the extracted folder and open the **.env** file.

3. In the **.env** file, add the following code line:

   ```
   PLATFORM_HOME=<Data Directory>
   ```

4. In the **.env** file, edit the mandatory properties that are listed in the following table:

   | Variable               | Description                                             | Mandatory |
   | ---------------------- | ------------------------------------------------------- | --------- |
   | ARTIFACTORY            | AWS ECR repository                                      | True      |
   | ENVIRONMENT            | Type of release                                         | True      |
   | TAG                    | Version release                                         | True      |
   | PLATFORM_HOME          | Location to store the persistent data                   | False     |
   | ENDPOINT               | URL or DNS endpoint to access REAN Accelerator Platform | True      |
   | RT_REPORTS_BUCKET_NAME | S3 bucket for storing REAN-Test reports                 | True      |
   | ADMIN_EMAIL            | Admin email                                             | False     |
   | AUTHNZ_DB_ROOT_PASS    | authnz DB root password, local dev only                 | False     |
   | AUTHNZ_DB_HOST         | authnz DB host                                          | False     |
   | AUTHNZ_DB_NAME         | authnz DB name                                          | True      |
   | AUTHNZ_DB_USER         | authnz DB user                                          | True      |
   | AUTHNZ_DB_PASS         | authnz DB password                                      | True      |
   | RD_DB_ROOT_PASS        | REAN-Deploy DB root password, local dev only            | False     |
   | RD_DB_HOST             | REAN-Deploy DB host                                     | False     |
   | RD_DB_NAME             | REAN-Deploy DB name                                     | True      |
   | RD_DB_USER             | REAN-Deploy DB user                                     | True      |
   | RD_DB_PASS             | REAN-Deploy DB password                                 | True      |
   | RT_DB_ROOT_PASS        | REAN-Test DB root password, local dev only              | False     |
   | RT_DB_HOST             | REAN-Test DB host                                       | False     |
   | RT_DB_NAME             | REAN-Test DB name                                       | True      |
   | RT_DB_USER             | REAN-Test DB user                                       | True      |
   | RT_DB_PASS             | REAN-Test DB password                                   | True      |
   | JAVA_OPTIONS           | JAVA options                                            | False     |
   | CATALINA_OPTS          | Tomcat JAVA options                                     | False     |

5. <a id = "5ca" name="5ca"></a>*(Optional)* To configure REAN Accelerators to use SSL or CA certificates to connect to the database, set the database properties for each Accelerator as shown in the following example:

   ```
   RD_DB_NAME=reandeploy?verifyServerCertificate=true&useSSL=true&requireSSL=true
   RD_DB_HOST=<rds-endpoint>
   RD_DB_USER=<rds_db_user>
   RD_DB_PASS=<rds_db_pass>
   ```

   ```
   RD_DB_NAME=reandeploy?verifyServerCertificate=true&useSSL=true&requireSSL=true
   ```

   _**Note:** This step is applicable whether you are using an AWS RDS database instance or MySQL in a container. In addition to this step, you can also configure SSL or configure CA certificates._

## <a id="step6" name="step6"></a>*(Optional)* Step 6: Configure REAN Deploy

1. To create the **conf** directory, run the following command:

   ```
   mkdir -p ${PLATFORM_HOME}/rean-deploy/conf
   ```

2. In the **conf** directory, create the **dnow.properties** file.

3. In the **dnow.properties** file, add REAN Deploy properties that you want to update.

   For information about the different properties that you can update to configure REAN Deploy, see <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-deploy', viewPage: 'administer', viewSection: 'configuration'})">REAN Deploy configuration properties</a>.

4. To customize FIPS compliant encryption key (AES-256) in REAN Deploy to encrypt sensitive data, such as secret key and access key, perform the following actions:

   _**<font color="red">Warning:</font>**_

   *<font color="red">REAN Cloud recommends that you change the encryption key when you deploy REAN Deploy  1.6.0 or later for the first time.</font>*<br>

   *<font color="red">If you have already deployed REAN Deploy 1.6.0 or later, ensure that REAN Deploy does not have any existing data (for example: connections and providers) before you change the encryption key. Otherwise, all existing data becomes unusable and cannot be recovered.</font>*<br>

   *<font color="red">If you are upgrading from REAN Deploy 1.5.0 or earlier for the first time and you change the encryption key during the upgrade, any existing data is re-encrypted with the new encryption key that you have specified. However, you must not change the encryption key during any future upgrades; otherwise the existing data will become unusable.</font>*

   - Run the following command to generate the encryption key:

     ```
     keytool -genseckey -keystore platform-keystore.jck -storetype jceks -storepass platformstorepass -keyalg AES -keysize 256 -alias jceksaes -keypass platformkeypass
     ```

   - Copy the **Keystore** file that is generated, to the **conf** directory.

   - Open the **dnow.properties** file and add the following properties:

     ```
     com.reancloud.security.encrypt.keystore.path=/home/rean-cloud/Work/AES/platform-keystore.jck
     com.reancloud.security.encrypt.keystore.password=platformstorepass
     com.reancloud.security.encrypt.keystore.encrypt.alias=jceksaes
     com.reancloud.security.encrypt.keystore.encrypt.keypassword=platformkeypass
     ```

   - Save the **dnow.properties** file.

   _**Note:** If you do not configure the encryption key, REAN Deploy automatically configures the FIPS-compliant encryption key (AES-256) during the deployment._

## <a id="step7" name="step7"></a>*(Optional)* Step 7: Configure SSL

1. To create a directory to store SSL certificates, run the following command:

   ```
   mkdir -p ${PLATFORM_HOME}/ssl
   ```

2. In the **SSL** directory that you have created, add the following certificate file:

   | File name        | Description         |
   | ---------------- | ------------------- |
   | dh.pem           | Diffie-Hellman key  |
   | reanplatform.key | SSL certificate key |
   | reanplatform.pem | SSL certificate     |

   _**Note:** If the **dh.pem** file is not available in the **SSL** directory, it gets created by default._

## <a id="step8" name="step8"></a>*(Optional)* Step 8: Configure CA certificates

1. To create a directory to store CA certificates, run the following command:

   ```
   mkdir -p ${PLATFORM_HOME}/rean-deploy/ca-certs
   ```

2. In the **ca-certs** directory that you have created, add the CA certificate files.

_**Note:** In addition to this step, ensure that you have configured REAN Accelerators to use CA certificates to connect to the database._

## <a id="step9" name="step9"></a>Step 9: Pull REAN Accelerator Platform Docker images on the EC2 instance

1. To get the Docker images ZIP file, contact the REAN Cloud team.
2. Copy the ZIP file to your EC2 instance and then load the Docker images.

## <a id="step10" name="step10"></a>Step 10: Deploy the REAN Accelerators

1. To get the Docker Compose files for REAN Accelerators, contact the REAN Cloud team.

2. To deploy either all or only a few specific REAN Accelerators, perform one of the following actions:

   - If you are using an AWS RDS database instance, run one of the commands listed in the following table based on the REAN Accelerators that you want to deploy:

     | REAN Accelerator                                             | Command to deploy the REAN Accelerator                       |
     | ------------------------------------------------------------ | ------------------------------------------------------------ |
     | All REAN Accelerators (REAN Deploy, REAN Assess, and REAN Test) | docker-compose -f core.yml -f reandeploy.yml -f reanassess.yml -f reantest.yml up |
     | REAN Deploy                                                  | docker-compose -f core.yml -f reandeploy.yml up              |
     | REAN Test                                                    | docker-compose -f core.yml -f reantest.yml up                |
     | REAN Deploy and REAN Assess                                  | docker-compose -f core.yml -f  reandeploy.yml -f reanassess.yml up |

   - If you have configured REAN Accelerator Platform to use MySQL locally in a container, you must run the following command to deploy all REAN Accelerators:

     ```
     docker-compose -f core-db.yml -f reandeploy-db.yml -f reantest-db.yml -f core.yml -f reandeploy.yml -f reanassess.yml -f reantest.yml up
     ```

   The deployment process might take several minutes. After all the commands are successfully run, you get access to the REAN Accelerator Platform URL: **https://(EC2-Instance_Ip)**.

   You can <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-platform-common', viewPage: 'createAndAccessAccount', viewSection: 'logon'})" style="text-decoration:none">log on</a> as a REAN Accelerator Platform administrator by using the default credentials (**user name: admin** and **password: admin**). REAN Cloud recommends that you <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-platform-common', viewPage: 'createAndAccessAccount', viewSection: 'password'})" style="text-decoration:none">change the password</a> after you log on for the first time.

_**Note:** REAN Accelerator Platform uses Amazon CloudWatch Logs for all container logging. The **reanplatform** log group in CloudWatch contains log streams for each REAN Accelerator._

## Where to go next

After REAN Accelerator Platform is deployed successfully, you can use the Admin Console to create <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-platform-common', viewPage: 'administer', viewSection: 'groups'})" style="text-decoration:none">groups</a> and <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-platform-common', viewPage: 'administer', viewSection: 'users'})" style="text-decoration:none">users</a> and assign users to appropriate groups. Alternatively, you can choose to <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-platform-common', viewPage: 'administer', viewSection: 'active'})" style="text-decoration:none">integrate REAN Accelerator Platform with Microsoft Active Directory</a> and manage users and group membership in Active Directory.
-->
