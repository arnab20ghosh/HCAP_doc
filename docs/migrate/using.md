---
title: Discover and migrate resources
---

# Discover and migrate resources

Hitachi Cloud Accelerator Platform - Migrate (Migrate Accelerator) helps you to migrate applications that are running in your existing data centers to the cloud. It brings in data from Discovery tools, enables you to pick and choose the servers for each application group, uses a migration tool for server replication, and then creates server images. This topic describes how you can use Migrate Accelerator to migrate discovered servers from your data centers to the cloud and show the migrated resources in Hitachi Cloud Accelerator Platform - Deploy (Deploy Accelerator).<br>

_**Important:** Migrate Accelerator currently supports the migration of servers from your data center to Amazon Web Services (AWS) only._

## <a id="Content" name="Content"></a>Contents

- <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-migrate', viewPage: 'discover-and-migrate-resources', viewSection: 'how'})" style="text-decoration:none">How Migrate Accelerator works</a>
- <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-migrate', viewPage: 'discover-and-migrate-resources', viewSection: 'scenario'})" style="text-decoration:none">End-to-end scenario for migrating servers from a data center to the cloud</a>
- <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-migrate', viewPage: 'discover-and-migrate-resources', viewSection: 'supported-tools'})" style="text-decoration:none">Supported discovery and migration tools</a>
- <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-migrate', viewPage: 'discover-and-migrate-resources', viewSection: 'logon'})" style="text-decoration:none">Signing in to Migrate Accelerator</a>
- <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-migrate', viewPage: 'discover-and-migrate-resources', viewSection: 'prepare'})" style="text-decoration:none">Preparing to discover and migrate servers</a>
- <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-migrate', viewPage: 'discover-and-migrate-resources', viewSection: 'endtoend'})" style="text-decoration:none">Discovering and migrating servers</a>
- <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-migrate', viewPage: 'discover-and-migrate-resources', viewSection: 'view'})" style="text-decoration:none">Viewing the overall migration status for application groups</a>

## <a id="how" name="how"></a>How Migrate Accelerator works

Migrate Accelerator enables you to pick and choose what you migrate and track at the Data Center level. You can add these migrated servers on the Deploy Accelerator canvas and then build and deploy the infrastructure.<br>

The following image shows the end-to-end steps for using Migrate Accelerator to create resources in Deploy Accelerator.

![](/images/rean-migrate/rm_endtoendprocess.PNG)

_**Note:** When you deploy Migrate Accelerator on an AWS EC2 instance, you must ensure that the Migrate Accelerator instance can connect to servers in your data center._  

## <a id="scenario" name="scenario"></a>End-to-end scenario for migrating servers from a data center to the cloud

Consider a scenario in which you want to migrate your application from a data center to the cloud. You can use Migrate Accelerator, the <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-migrate', viewPage: 'discover-and-migrate-resources', viewSection: 'supported-tools'})" style="text-decoration:none">supported discovery and migration tools</a>, and Deploy Accelerator to perform the following end-to-end steps: 

1. Use the supported discovery tool to discover servers in your data center.
   Alternatively, manually create a CSV file that contains an inventory of the servers in your data center.
2. Bring in this discovered data into Migrate Accelerator and create logical application groups that include all servers that are required to run the application. 
   For example, you can add the database server and web server used by an application into a logical application group.
3. Use the supported migration tool to initiate server replication and test that all servers in the application group have been successfully replicated.
4. Use Migrate Accelerator to create images of the target test servers. 
   Launch an instance from this image to confirm that the server is replicated correctly. 
5. Plan and announce the downtime for your application.
6. Use the supported migration tool to cutover the servers in the application group to stop further server replication.
7. After the cutover servers are launched successfully, use Migrate Accelerator to create final images of all servers in the application group.
8. Launch instances from the final images in the subnet in which you want to host your application.
9. Point users to the migrated application in the cloud before the end of the planned downtime.      

## <a id="supported-tools" name="supported-tools"></a>Supported discovery and migration tools

Migrate Accelerator supports the following tools for discovering servers in your data center and migrating them to the cloud.

- **Discovery**: [RISC Networks CloudScape](https://www.riscnetworks.com/)

  _**Note:** If you do not want to use CloudScape, you can also manually create a CSV file that contains an inventory of the servers in your data center._

- **Migration**: [CloudEndure](https://www.cloudendure.com)

## <a id="logon" name="logon"></a>Signing in to Migrate Accelerator

The Migrate Accelerator and Admin Console deployment process creates a default administrator who can perform all required actions. This administrator can then create additional users or other users can <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-platform-common', viewPage: 'createAndAccessAccount', viewSection: 'create'})" style="text-decoration:none">create their own Hitachi Cloud Accelerator Platform account</a>.

1. In a browser, type **https://*ipAddress***.

   ***ipAddress*** refers to the IP address of the instance on which Migrate Accelerator is deployed. 

2. Enter your user name or email address and your password.

   ![](/images/rean-platform-common/console_signin.PNG)

3. Click **SIGN IN**.

   Until you create at least one discovery job, you are prompted to create a new discovery job each time you sign in to Migrate Accelerator.<br>

   When you sign in to Migrate Accelerator after you have created one or more discovery jobs, the discovery job that you had previously opened appears by default.


_**Note:**_

- _You can perform various actions in Migrate Accelerator only if your administrator has granted you the appropriate permissions._
- _You can access only the jobs, connections, and migration credentials that you have created._

## <a id="prepare" name="prepare"></a>Preparing to migrate servers

Before you create discovery and migration jobs in Migrate Accelerator, you must perform the following actions:

- <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-migrate', viewPage: 'discover-and-migrate-resources', viewSection: 'server-dc'})" style="text-decoration:none">Discover servers</a> in your data center.

- <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-migrate', viewPage: 'discover-and-migrate-resources', viewSection: 'configure-ce'})" style="text-decoration:none">Configure CloudEndure</a> to migrate servers from your data center to AWS.

- <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-migrate', viewPage: 'discover-and-migrate-resources', viewSection: 'provider'})" style="text-decoration:none">Configure providers</a> to store authentication details of the cloud service provider account in which Migrate Accelerator must create images of the migrated servers. 

- <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-migrate', viewPage: 'discover-and-migrate-resources', viewSection: 'migration'})" style="text-decoration:none">Create  migration service credentials</a> to store the user name and password that Migrate Accelerator must use to connect to a migration service, such as CloudEndure. For each migration job, Migrate Accelerator communicates with the selected migration service to initiate server migration, track migration status, and perform other actions.

- <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-migrate', viewPage: 'discover-and-migrate-resources', viewSection: 'mig-config'})" style="text-decoration:none">Create migration configurations</a> to store a predefined set of migration service, credentials to access that migration service, and the appropriate cloud service provider. While <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-migrate', viewPage: 'discover-and-migrate-resources', viewSection: 'migrate'})" style="text-decoration:none">creating a migration job</a>, you must select the appropriate migration configuration.

- <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-migrate', viewPage: 'discover-and-migrate-resources', viewSection: 'connection'})" style="text-decoration:none">Configure connections</a> to store the user name and password that Migrate Accelerator can use to connect to the servers in your data center and install the CloudEndure agent. While <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-migrate', viewPage: 'discover-and-migrate-resources', viewSection: 'migrate'})" style="text-decoration:none">creating a migration job</a>, you can select the appropriate connections.

  _**Note:** You have to configure connections only if you want Migrate Accelerator to auto-install CloudEndure agents on the servers in your data center._

### <a id="server-dc" name="server-dc"></a>Discover servers in your datacenter

Before you create a discovery job in Migrate Accelerator, you must generate an inventory of the servers (or assets) in your data center by using one of the following methods.

- <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-migrate', viewPage: 'discover-and-migrate-resources', viewSection: 'cs'})" style="text-decoration:none">Bring in server data from CloudScape</a>
- <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-migrate', viewPage: 'discover-and-migrate-resources', viewSection: 'csv'})" style="text-decoration:none">Manually create an inventory of server data</a> 

_**Important:** The CSV file that you import into Migrate Accelerator can include servers of any operating system. However, you can successfully run a migration job only for Microsoft Windows and Linux servers._

#### <a id="cs" name="cs"></a>Bring in server data from CloudScape

If you are using CloudScape to discover servers in your data center, you can bring in this discovered data into Migrate Accelerator in one of the following ways:

- **Use RISC APIs:** While <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-migrate', viewPage: 'discover-and-migrate-resources', viewSection: 'discovery'})" style="text-decoration:none">creating a RISC discovery job</a>, specify the CloudScape account credentials, API endpoint and key, and the assessment. Migrate Accelerator brings in discovered data inventory directly from CloudScape.
- **Import data in a CSV format:** While <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-migrate', viewPage: 'discover-and-migrate-resources', viewSection: 'discovery'})" style="text-decoration:none">creating a RISC_EXPORTED_DISCOVERY discovery job</a>, specify the CSV file that you want to import into Migrate Accelerator. To export the discovered data from CloudScape in a CSV format, use the **Consume Intelligence > Foundation > Assets** option.

For information about using CloudScape to discover servers in your data center, see the [RISC Networks documentation](https://www.riscnetworks.com/).

#### <a id="csv" name="csv"></a>Manually create an inventory of server data

Create a CSV file that contains a manual inventory of the servers that need to be migrated. While <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-migrate', viewPage: 'discover-and-migrate-resources', viewSection: 'discovery'})" style="text-decoration:none">creating a CSV discovery job</a>, specify this CSV file to be imported into Migrate Accelerator.

The first row of your CSV file must contain the following data (or column headers):<br>**HostName,IPAddress,ServerId,OSType,Group**

_**Note:** The **Group** column enables you to group servers that belong to the same application._

### <a id="configure-ce" name="configure-ce"></a>Configure CloudEndure

Before you create a migration job in Migrate Accelerator, perform the following steps to configure CloudEndure:

1. Register for the CloudEndure Live Migration solution through the [AWS Marketplace](https://aws.amazon.com/marketplace/pp/B01MQCH96B) website with your AWS account.
   The license package that you select must cover the number of CloudEndure agents that you need to install on the servers in your data center. For more information, see the [CloudEndure documentation](https://docs.cloudendure.com/Content/Getting_Started_with_CloudEndure/Registering_to_CloudEndure_Solutions/Registering_to_CloudEndure_Solutions.htm#Migratio).

2. To migrate servers from your data center to AWS, create a Live Migration project in CloudEndure.
   For information about setting up a Live Migration project, see the [CloudEndure documentation](https://docs.cloudendure.com/#Getting_Started_with_CloudEndure/Working_with_Projects/Working_with_Projects.htm#Working_with_Projects%3FTocPath%3DNavigation%7CGetting%2520Started%2520with%2520CloudEndure%7CWorking%2520with%2520Projects%7C_____0).

   _**Note:** While <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-migrate', viewPage: 'discover-and-migrate-resources', viewSection: 'migrate'})" style="text-decoration:none">creating a migration job</a> in Migrate Accelerator, you must select this Live Migration project._

3. In the Live Migration project, configure the following details:

   - Configure the replication details and the credentials of the AWS account in which you want to create the infrastructure.

   - Ensure that the license that you select for the Live Migration project covers the number of CloudEndure agents that you need to install in your data center. 

     You can either manually install an agent on each server that you want to migrate or enable Migrate Accelerator to install agents on the servers.

   - Ensure that the appropriate [CloudEndure IAM policy](https://console.cloudendure.com/IAMPolicy.json) is attached to the AWS user whose credentials you have specified in the Live Migration project.

### <a id="provider" name="provider"></a>Configure providers

When you <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-migrate', viewPage: 'discover-and-migrate-resources', viewSection: 'migrate'})" style="text-decoration:none">start a migration job</a> for a group of servers in the data center, CloudEndure creates test instances in AWS and replicates data from these servers on the test instances. After the data replication has completed successfully, you can create images of the test instances by using the provider that is configured in the migration job.<br>

Providers enable you to specify the cloud provider and credentials for accessing the account in which the images must be created. You can <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-migrate', viewPage: 'discover-and-migrate-resources', viewSection: 'createprovider'})" style="text-decoration:none">create multiple providers</a> in the Admin Console and select the appropriate provider while creating a migration job. The providers that you create are accessible only to you by default. However, you can choose to <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-migrate', viewPage: 'discover-and-migrate-resources', viewSection: 'shareprovider'})" style="text-decoration:none">share your provider</a> with other users who belong to specific Migrate Accelerator groups.<br>

_**Important:** Migrate Accelerator can create images only in the same AWS account in which CloudEndure launches test instances. Therefore, the provider that you select in a migration job must contain credentials that match the credentials that are specified in the CloudEndure Live Migration project._

#### <a id="createprovider" name="createprovider"></a>Create a provider

1. On the Home page, click the **Accelerator** icon (![](/images/rean-platform-common/icon_accelerator.PNG) in the top-left corner and select **Admin Console**.

2. Click the **More options** icon (![](/images/rean-platform-common/icon_more.PNG)) in the top-right corner and then click **Providers**.

3. Under **Add Provider**, click **NEW**.

4. Enter the provider name and select the appropriate provider type (for example, AWS).

   _**Note:** Migrate Accelerator currently supports only AWS as a cloud provider._

5. In **Select Accelerator** list, select **Migrate Accelerator**. 

   This allows creating provider for Migrate Accelerator in the Admin console. 

6. In **Provider Details**, specify authentication details (in JSON format) of the AWS account in which Migrate Accelerator must create the server images.

   Consider the following points while selecting the option to specify authentication details.

   - **Instance Profile with Assume Role**

     This method provides a secure way for cross-account access. Consider a scenario  in which Migrate Accelerator is deployed in an AWS account that is different from the accounts in which Migrate Accelerator must create the server images. Instead of storing the access credentials for all these accounts in Migrate Accelerator, you can attach a role to the instance on which Migrate Accelerator is deployed. Migrate Accelerator can then assume a role in the other accounts and create images. For more information about assuming roles, see the [AWS documentation](https://docs.aws.amazon.com/cli/latest/userguide/cli-roles.html).<br>

     To use the **Instance Profile with Assume Role** method, you must attach a role to the instance on which Migrate Accelerator is deployed. For the other accounts, you must specify a role that Migrate Accelerator can assume to create the images. The role that you specify must have permissions to create images. It must also define the account in which Migrate Accelerator is deployed as a trusted entity.<br><br><u>Sample JSON</u>

     ```json
     {
         "region": "xx-xxxx-x",
         "assume_role": {
             "role_arn": "arn:aws:iam::xxxxxxxxxxx:role/assume_role",
             "session_name": "SESSION-NAME",
             "external_id": "assume_role" 
         }
     }
     ```

   - **Instance Profile**

     This method provides a secure way of accessing the account in which Migrate Accelerator must create the server images. However, you must use this method only if a role is attached to the instance on which Migrate Accelerator is deployed. This role must have the permissions to create images.<br><br>To use the **Instance Profile** method, you must specify the region in which the images must be created.

     <u>Sample JSON</u>

     ```json
     {
         "region": "xx-xxxx-x"
     }
     ```

   - **Basic Credentials with Assume Role**

     This method provides another way for cross-account access. Consider a scenario in which Migrate Accelerator is deployed in an AWS account that is different from the accounts in which Migrate Accelerator must create the server images. Instead of storing access credentials for all these accounts in Migrate Accelerator, you can specify long-term access credentials for only the parent account. Migrate Accelerator can then assume a role in the other accounts and create images. For more information about assuming roles, see the [AWS documentation](https://docs.aws.amazon.com/cli/latest/userguide/cli-roles.html).<br><br>To use the Basic Credentials with Assume Role method, you must specify the credentials for only the parent account. For all other accounts, you must specify a role that Migrate Accelerator can assume to create images. The role that you specify must have access to create images. It must also define the parent account as a trusted entity.<br><br><u>Sample JSON</u>

     ```json
     {
         "access_key": "xxxxxxxxxx",
         "secret_key": "xxxxxxxxxx",
         "region": "xx-xxxx-x",
         "assume_role": {
             "role_arn": "arn:aws:iam::xxxxxxxxxxx:role/assume_role",
             "session_name": "SESSION-NAME",
             "external_id": "assume_role"
         }
     }
     ```

   - **Basic Credentials**

     To use this method, you must specify the IAM user credentials for accessing the account in which Migrate Accelerator must create the server images. The IAM user whose credentials you specify must have access to create images.<br><br><u>Sample JSON</u> 

     ```json
     {
         "access_key": "XXXXXXXXXXXXXXX",
         "secret_key": "XXXXXXXXXXXXX",
         "region": "xx-xxxx-x"
     }
     ```

7. <a id="meta" name="meta"></a>In **Optional Metadata**, specify additional metadata for the provider. Make sure that you do not enter confidential data in the metadata as it is displayed in plain-text.

   ```
   {
     "description": "This provider is for 001 and 002 blueprints",
     "migration_name": "Migration 1"
   }
   ```

8. Click **SAVE**.

   A new provider appears under the **Provider List** section.

#### <a id="editprovider" name="editprovider"></a>Edit a provider

1. On the Home page, click the **Accelerator** icon (![](/images/rean-platform-common/icon_accelerator.PNG)) in the top-left corner and select **Admin Console**.

2. Click the **More options** icon (![](/images/rean-platform-common/icon_more.PNG)) in the top-right corner and then click **Providers**.

3. Under **Provider List**, in the **Actions** column for the provider that you want to edit, click **Edit** (![](/images/rean-migrate/edit.PNG)).

4. Under **Edit Provider**, update the provider name or provider details.

   _**Note:** If you edit a provider, you must re-enter all values in the provider details before you click **UPDATE**. Otherwise, an error message might be shown while using this provider to create images of migrated servers._

5. Click **UPDATE**.

#### <a id="shareprovider" name="shareprovider"></a>Share a provider

You can share a provider with a Migrate Accelerator user-group in the Admin console. Sharing a provider assigns that provider to all the users in the selected user-group. This action can reduce the need for users to create their own providers.

**To share a provider with a specific user group, perform the following actions:**

1. On the Home page, click the **Accelerator** icon (![](/images/rean-platform-common/icon_accelerator.PNG)) in the top-left corner and select **Admin Console**.

2. Click the **More options** icon (![](/images/rean-platform-common/icon_more.PNG)) in the top-right corner and then click **Providers**.

3. Under **Provider List**, in the **Actions** column for the provider that you want to share, click **Share Provider**  (![](/images/rean-migrate/share.PNG)).

    ![](/images/rean-migrate/shareprovider.PNG)

4. In the **Share Provider** dialog box, for a user group, click the **Add Permissions**  icon (![](/images/rean-migrate/addper.PNG)).

5. Select the permissions you want to assign, and click **DONE**. 

6. In the **Share Provider** dialog box, click **SUBMIT**. 

### <a id="migration" name="migration"></a>Create migration service credentials

Migrate Accelerator uses migration credentials to communicate with the migration service to initiate migration, track migration status, and perform other actions. While configuring migration credentials, you must specify the migration service and credentials that Migrate Accelerator must use to migrate application groups from the data center.<br>

While <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-migrate', viewPage: 'discover-and-migrate-resources', viewSection: 'mig-config'})" style="text-decoration:none">creating a migration configuration</a>, you must select the credentials that Migrate Accelerator must use to communicate with the selected migration service.

**To configure migration service credentials, perform the following actions:**

1. On the Home page of Migrate Accelerator, click the **More options** icon (![](/images/rean-platform-common/icon_more.PNG)) icon in the top right corner.

2. Click **Migration Configurations**.

3. Click the **MIGRATION SERVICE CREDENTIALS** tab.

4. Under **Add/Edit Migration Service Credentials**, click **NEW**.

   ![](/images/rean-migrate/rm_migrationcredentials.PNG)

5. Enter a unique name for the migration service credentials.

6. From the **Migration Service** list, select the appropriate migration service.

   _**Note:** Currently, Migrate Accelerator supports only CloudEndure as a migration service._

7. Enter the credentials (user and password) that Migrate Accelerator must use to access the selected migration service.

8. Click **SAVE**.

   The new migration service credentials appear under the **Migration Service Credentials List** section.

### <a id="mig-config" name="mig-config"></a> Create migration configurations

Migration configurations allow you to store a predefined set of configurations that are required while <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-migrate', viewPage: 'discover-and-migrate-resources', viewSection: 'migrate'})" style="text-decoration:none">creating a migration job</a>.  Each migration configuration comprises the following details:

- Migration service that Migrate Accelerator must use to migrate servers from the data center to the selected cloud service provider.
- Credentials to access the migration service.
- Authentication details for the cloud service provider account in which Migrate Accelerator must create images of the servers. 
- _(Only for the CloudEndure migration service)_ Live Migration project from which Migrate Accelerator must migrate servers.

You can specify a migration configuration once and use it in multiple migration jobs. Also, if your migration service credentials or cloud service provider authentication details change, you just need to update the appropriate migration configurations instead of editing multiple migration jobs.

**To create a migration configuration, perform the following actions:**

1. On the Home page of Migrate Accelerator, click the **More options** icon  (![](/images/rean-platform-common/icon_more.PNG))  icon in the top right corner.

2. Click **Migration Configurations**.

3. Click the **MIGRATION CONFIGURATION** tab.

4. Under **Add/Edit Migration Configuration**, click **NEW**.

5. Enter a unique name and description for the migration configuration.

   ![](/images/rean-migrate/rm_migrationconfig.PNG)

6. From the **Migration Service** list, select the appropriate migration service.

   _**Note:** Currently, Migrate Accelerator supports only CloudEndure as a migration service._

7. From the **Migration Service Credentials** list, select the appropriate credentials.

   All credentials for the selected migration service appear in the list.

   For information about creating the credentials, see <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-migrate', viewPage: 'discover-and-migrate-resources', viewSection: 'migration'})" style="text-decoration:none">Create migration service credentials</a>.

8. To fetch all projects from the CloudEndure migration service, perform the following actions:

   - Click **GET PROJECTS**.

   - From the **Project** list, select the appropriate Live Migration project in CloudEndure.

     _**Important:** Ensure that the selected project includes the license to install agents on all servers in the application group._

9. From the **Cloud Service Provider** list, select the appropriate provider for creating images of the migrated servers.

   Ensure that the credentials in the selected provider are the same as the AWS credentials that are configured in the selected Live Migration project.

   For information about creating providers, see <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-migrate', viewPage: 'discover-and-migrate-resources', viewSection: 'provider'})" style="text-decoration:none">Configure providers</a>.

10. Click **SAVE**.

    The new migration configuration appears under the **Migration Configuration List** section.

### <a id="connection" name="connection"></a>Configure connections

Migrate Accelerator uses connections to connect to servers that are running in your data center so that it can install the CloudEndure agent on these servers. You must create an SSH connection to connect to servers that have the Linux operating system. Similarly, you must create a WinRM connection to connect to servers that have the Microsoft Windows operating system.<br>

_**Note:** You have to configure connections only if you want Migrate Accelerator to auto-install CloudEndure agents on the servers in your data center. When you select the **Auto install agent** option while <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-migrate', viewPage: 'discover-and-migrate-resources', viewSection: 'migrate'})" style="text-decoration:none">creating a migration job</a>, you must also specify the appropriate connection to connect to the servers in your data center._

**To configure a connection, perform the following actions:**

1. On the Home page of Migrate Accelerator, click the **More options** icon (![](/images/rean-platform-common/icon_more.PNG)) in the top-right corner.

2. Click **Connections**.

3. Under **Add/Edit Connection**, click **NEW**.

   ![](/images/rean-migrate/rm_connection.PNG)

4. Enter the connection name and select the appropriate connection type.

5. Based on the connection type that you have selected, perform the following actions:

   | Connection type | Actions to perform                                           |
   | --------------- | ------------------------------------------------------------ |
   | SSH             | Enter the user and password or SSH key that Migrate Accelerator must use to connect to the servers.<br><br>_**Note:** Ensure that the user that you specify has Read-Write access to the **/tmp** directory on the servers. Also, ensure that this user has root access or is in the sudoers list._ |
   | WinRM           | Enter the user and password that Migrate Accelerator must use to connect to the servers.<br><br>To set up a secure connection, select **Https**. Migrate Accelerator uses the CA certificates that were copied to the **/root/rean-platform/ca-certs** folder while deploying Migrate Accelerator. |

6. Click **SAVE**.

   A new connection appears under the **Connection List** section.

## <a id="endtoend" name="endtoend"></a>Discovering and migrating servers

The end-to-end process to bring in discovered servers into Migrate Accelerator, perform server replication, and migrate server images to the cloud includes multiple steps, as shown in the following image.

![](/images/rean-migrate/rm_flow.PNG)

1. <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-migrate', viewPage: 'discover-and-migrate-resources', viewSection: 'discovery'})" style="text-decoration:none">Discover servers</a>
2. <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-migrate', viewPage: 'discover-and-migrate-resources', viewSection: 'plan'})" style="text-decoration:none">Plan migration of servers</a>
3. <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-migrate', viewPage: 'discover-and-migrate-resources', viewSection: 'migrate'})" style="text-decoration:none">Migrate servers</a>
4. <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-migrate', viewPage: 'discover-and-migrate-resources', viewSection: 'migrate-resource'})" style="text-decoration:none">Use migrated resources in Deploy Accelerator</a>

### <a id="discovery" name="discovery"></a>Discover servers

![](/images/rean-migrate/rm_flow1.PNG)

#### <a id="create-disc-job" name="create-disc-job"></a>Create a discovery job

1. To create a discovery job, perform one of the following actions:

   - If you have not created any discovery job, in the dialog box that appears, click **ADD DISCOVERY**.
   - If you have previously created a discovery job, on the Home page of Migrate Accelerator, click the **Create Discovery** icon (![](/images/rean-migrate/icon_create.PNG)).

2. On the Create Discovery page, enter the discovery name and description.

3. From the **Discovery Tool** list, select the appropriate discovery tool.

4. If you have selected **RISC** as the discovery tool, perform the following actions:

   - Enter your CloudScape API endpoint, API key, user, and password.

   - Click **GET ASSESSMENTS**.

   - From the **CloudScape Assessments** list, select the assessment that contains the discovered servers that you want to migrate.

   - _(Optional)_ To retrieve asset data based on tags defined in RISC, perform the following actions:

     - Click **ADD TAG**.

       In RISC, a tag is represented by a key-value pair. A key can be associated with multiple values, but the key, in combination with each value, represents a distinct tag. The same tag can be applied to multiple assets and multiple tags can be applied to an asset. To bring in asset data in Migrate Accelerator based on tags defined in RISC, you must specify the key-value pairs representing those tags while creating a discovery job.

     - In **Tag Key**, type the tag key that is applied to assets that you want to bring into Migrate Accelerator.

       _**Important:** Ensure that the tag keys and values that you specify in Migrate Accelerator exactly match the tag keys and values defined in RISC. Otherwise, the discovery job will not complete successfully and no assets will be brought into Migrate Accelerator._

     - In **Tag values**, type the appropriate tag values that correspond to the tag key you have specified.

       For example, say the **OS** key in RISC has two values - **Windows** and **Linux**. And you want to bring in assets that have the **OS-Windows** and **OS-Linux** tags (key-value pairs) assigned to them. While creating a discovery job in Migrate Accelerator, you must specify **OS** as the **Tag key** and **Windows** and **Linux** as the corresponding **Tag values**, as shown in the following image.

       ![](/images/rean-migrate/rm_creatediscoveryrisc.PNG)

       _**Note:** Ensure that you specify a unique set of tag values for a tag key--you cannot type the same tag value twice for a tag key._

     - To add another tag, click **ADD TAG** and then type the tag key and corresponding tag values.

       You can add multiple tag keys and corresponding tag values for a discovery job.

   _**Important:** You cannot modify or delete tag key values once they are saved. However, you can later <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-migrate', viewPage: 'discover-and-migrate-resources', viewSection: 'edit-disc-job'})" style="text-decoration:none">edit the discovery job</a> to add more tag keys or tag values._


5. If you have selected **CSV** as the discovery tool, perform the following actions:

   - Click **Choose File**.

   - Select the CSV file from your local machine and click **Upload**.

     The first row of your CSV file must contain the following data (or column headers):<br>**HostName,IPAddress,ServerId,OSType,Group**

   The following image shows the Create Discovery page for the CSV discovery tool.

   ![](/images/rean-migrate/rm_creatediscoverycsv.PNG)

6. If you have selected **RISC_EXPORTED_DISCOVERY** as the discovery tool, perform the following actions:

   - Click **Choose File**, select the CSV file that you have exported from RISC CloudScape, and click **Upload**.

   - _(Optional)_ Click **MAP**.

      The **Discovery Field** column displays the fields in which Migrate Accelerator stores the discovered data. In **CSV Column**, the drop-down list displays all columns from the CSV file that you have uploaded. 

   - For each field in the **Discovery Field** column, select the CSV column from which the data must be imported, as shown in the following image.

      ![](/images/rean-migrate/rm_creatediscoveryrisccsv.PNG)

   - _(Optional)_ To view how the discovered data will be mapped to the Migrate Accelerator fields, move through to the end of the **Discovery Field** column and click **PREVIEW**.

7. Click **CREATE DISCOVERY**.

   Application groups within the discovery job appear in the left panel.

   _**Note:** After you create a **RISC** or **RISC_EXPORTED_DISCOVERY** discovery job, you can <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-migrate', viewPage: 'discover-and-migrate-resources', viewSection: 'connect-dataupload'})" style="text-decoration:none">manually upload the connectivity data</a> that RISC CloudScape has generated for your assessment._


#### <a id="risc-jobstatus" name="risc-jobstatus"></a>View the status of RISC discovery jobs

In the case of **RISC** discovery jobs, Migrate Accelerator fetches data incrementally from CloudScape. While the data retrieval is still in progress, you can see the already retrieved assets in the Migrate Accelerator UI.<br>The banner for RISC discovery jobs shows the status, timestamps (for last fetch, last new asset, and last updated assets), and impacted actions. Until all assets have been successfully retrieved, it is recommended that you *do not* perform the following actions:

- <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-migrate', viewPage: 'discover-and-migrate-resources', viewSection: 'connect-dataupload'})" style="text-decoration:none">Manually upload the connectivity data</a>
- <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-migrate', viewPage: 'discover-and-migrate-resources', viewSection: 're-group'})" style="text-decoration:none">Regroup servers in an application group</a>
- <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-migrate', viewPage: 'discover-and-migrate-resources', viewSection: 'build-plan'})" style="text-decoration:none">Download the build plan for an application group</a>
- <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-migrate', viewPage: 'discover-and-migrate-resources', viewSection: 'migrate'})" style="text-decoration:none">Migrate servers in an application group</a>

_**Note:** To view updates to the discovery job status in the banner, you must manually refresh your browser._

The following image shows an example of the banner that is shown for RISC discovery jobs. To hide the banner, click **X** in the top-right corner. To show the banner again, click the **Show RISC progress** icon (![](/images/rean-migrate/icon_showbanner.png)).

![](/images/rean-migrate/rm_discbanner.PNG)

#### <a id="connect-dataupload" name="connect-dataupload"></a>Manually upload connectivity data

The option to manually upload connectivity data is available only for **RISC** and **RISC_EXPORTED_CSV** discovery jobs. The connectivity data helps to identify the inter-dependencies between servers in an application group. For example, it can highlight the dependency between the web and database servers of an application.<br>

Migrate Accelerator includes this connectivity data in the build plan, which can be used to plan the migration of application infrastructure to the cloud.

**Before you begin**

1. Download the connectivity data for the appropriate assessment in CloudScape (use the **Add Intelligence > Available Reports** option and then export the **Detailed Application Dependency Data** report as a CSV file).

2. If required, customize the connectivity data in the CSV file based on the following considerations:

   - Ensure that all the servers listed in the CSV file are a part of the same application group in Migrate Accelerator. Otherwise, none of the connectivity data is saved in the Migrate Accelerator database. 

   - If the CSV file size is too large, you might get an error while uploading the file in Migrate Accelerator. In this case, you can break up the connectivity data into multiple files. Migrate Accelerator consolidates the connectivity data across these multiple files. 

     _**Important:** You must ensure that the same connectivity entry (which is a combination of source server, destination server, destination port, and connection protocol) is not listed in multiple files. Otherwise, duplicate connectivity entries are created in the database._

   - Migrate Accelerator requires data from only the following three columns in the CSV file that is downloaded from CloudScape:

     - destport
     - destaddr
     - scraddr

     To reduce the file size, you can choose to remove all other columns from the CSV file.

**To manually upload connectivity data, perform the following actions:**

1. In the **Pick Discovery Job** box at the top, locate the discovery job for which you want to upload the connectivity data.

2. Next to the appropriate discovery job, click the **Upload** icon (![](/images/rean-migrate/icon_uploaddata.PNG)).

3. In the Manual Upload RISC Connectivity Data window, click **Choose File**. 

4. Locate and select the CSV file that contains the connectivity data for the discovery job.

5. Click **SUBMIT**.

   The **Upload** icon for the discovery job is not available until the CSV file has been uploaded successfully. 

   _**Note:** In case of any error, none of the connectivity data in the CSV file is saved in the Migrate Accelerator database._

#### <a id="edit-disc-job" name="edit-disc-job"></a>Edit a discovery job

1. In the **Pick Discovery Job** box at the top, locate the discovery job that you want to edit.

2. Next to the appropriate discovery job, click the **Edit** icon (![](/images/rean-migrate/icon_discedit.PNG)).

3. In the Edit Discovery window, make the required updates to the discovery job.

   For **CSV** and **RISC_EXPORTED_CSV** discovery jobs, you can edit only the description.

   For **RISC** discovery jobs, you can edit the description, CloudScape API Endpoint, and CloudScape credentials (password and API key). You can also add a new tag key and corresponding tag values, or add new tag values to an existing tag key. For information about adding tag keys and tag values, see <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-migrate', viewPage: 'create-disc-job', viewSection: 'discovery'})" style="text-decoration:none">Create a discovery job</a>.

   _**Note:** To save any updates that you make to a **RISC** discovery job, you must specify the CloudScape password and API key again._

4. Click **SAVE**.

   If you have added a new tag key or tag value to a completed **RISC** discovery job, its status changes to **In Progress** again. If you have added a tag key or tag value to an in-progress **RISC** discovery job, Migrate Accelerator waits for the job to complete and then again changes its status to **In Progress**.

   In both these cases, the discovery job retrieves asset data that corresponds to the new tag keys and tag values. It also retrieves any new asset data that corresponds to existing tag keys and tag values. 

### <a id="plan" name="plan"></a>Plan migration of servers

![](/images/rean-migrate/rm_flow2.PNG)

Migrate Accelerator migrates servers as a part of an application group. An application group is a logical grouping of discovered servers that can be migrated to the cloud at the same time. A few discovery tools logically group servers as a part of the discovery process. For example, the database server and the web server used by an application can be a part of one logical application group.<br>

By default, Migrate Accelerator groups the servers in an application group based on the discovery tool that you have selected. However, you can change the default grouping of servers based on your requirements.<br>

As a part of planning the migration of application groups, you can perform the following tasks:

- <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-migrate', viewPage: 'discover-and-migrate-resources', viewSection: 'server-details'})" style="text-decoration:none">View details of discovered servers</a>
- <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-migrate', viewPage: 'discover-and-migrate-resources', viewSection: 'new-group'})" style="text-decoration:none">Create a new application group</a>
- <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-migrate', viewPage: 'discover-and-migrate-resources', viewSection: 're-group'})" style="text-decoration:none">Regroup servers in an application group</a>
- <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-migrate', viewPage: 'discover-and-migrate-resources', viewSection: 'build-plan'})" style="text-decoration:none">Download the build plan for an application group</a>

#### <a id="supported-os" name="supported-os"></a>Supported operating systems

Migrate Accelerator supports the migration of servers that use the following operating systems:

| Operating system | Supported versions         |
| ---------------- | -------------------------- |
| Windows          | - 2016<br>- 2012<br>- 2008 |
| Ubuntu           | - 16.04<br>- 14.04         |
| Red Hat Linux    | 7.6                        |

_**Note:** Migrate Accelerator does not support auto-installation of the CloudEndure agent on Windows 2008._

#### <a id="server-details" name="server-details"></a>View details of discovered servers

1. On the Home page, from the left panel, select an application group.

   All servers that are a part of the selected application group appear in the Servers for Group panel.

   _**Note:** The **Ungrouped** group contains servers that are not a part of any application group._

2. Click the server whose details you want to view.

   A panel with details of the selected server appears on the right, as shown in the image below. 

   ![](/images/rean-migrate/rm_serverdetails.PNG)

3. _(Optional)_ To hide the panel, click **X** in the top-right corner.

#### <a id="new-group" name="new-group"></a>Create a new application group

1. Ensure that the discovery job for which you want to create a new application group is selected in the **Pick Discovery Job** box at the top.

2. On the Home page, click **Create Group**.

3. In the Create Group panel, enter the group name.

   The group name that you specify must be unique for the selected discovery job.

4. To move servers to the new group, perform the following actions:

   - In the Groups panel, select an existing application group.

      Servers in the selected application group appear in the Servers for Group panel.

   - In the Servers for Group panel, select the servers that you want to move to the new group.

      The selected servers also appear in the Create Group panel.

      _**Note:** The Search option in the Servers for Group panel filters servers listed on the current page only._

   - _(Optional)_ Repeat the above actions to move servers from other existing groups to the new group.

      The **Ungrouped** group contains servers that are not a part of any application group.

   To create a new application group, you must add at least one server in that group. Each server can be a part of only one group.

   ![](/images/rean-migrate/RM_addgroup.PNG)

5. Click **CREATE GROUP**.

6. In the confirmation box, click **YES**.

   A new application group appears in the left panel on the Home page.

#### <a id="re-group" name="re-group"></a>Regroup servers in an application group

1. Ensure that the appropriate discovery job is selected in the **Pick Discovery Job** box at the top.

2. On the Home page, click **Regroup**.

3. In the Regroup panel, from the **Group Name** list, select the application group to which you want to add servers.

   Only application groups that contain at least one server appear in the list.

4. To add servers to the selected application group, perform the following actions:

   - In the Groups panel, select an existing application group.

      Servers in the selected application group appear in the Servers for Group panel.

   - In the Servers for Group panel, select the servers that you want to move to the group selected in the Regroup panel.

      The selected servers also appear in the Regroup panel.

      _**Note:** The Search option in the Servers for Group panel filters servers listed on the current page only._

   - _(Optional)_ Repeat the above actions to move servers from other existing groups.

   ![](/images/rean-migrate/rm_regroup.PNG)

   Each server can be a part of only one group.

5. Click **REGROUP**.

6. In the confirmation box, click **YES**. 

#### <a id="build-plan" name="build-plan"></a>Download the build plan for an application group

Migrate Accelerator generates a build plan for each application group. This build plan is a specification document that you can download and use to plan the migration of your application infrastructure to the cloud. 

1. Ensure that the appropriate discovery job is selected in the **Pick Discovery Job** box at the top.

2. On the Home page, from the left panel, select the application group for which you want to download the build plan.

3. Click the **Download Build Plan** icon (![](/images/rean-migrate/icon_buildplan.PNG)).

   The build plan is downloaded to your local machine. Migrate Accelerator automatically populates data in a few columns across multiple tabs in the build plan. You can identify these columns based on the green background color.

   _**Note:** By default, Migrate Accelerator generates a generic build plan that is not customized for any specific cloud provider. However, your administrator can configure Migrate Accelerator to generate a build plan that is customized for AWS._

4. _(Optional)_ Enter details in the other sheets based on your requirements, add your existing application architecture diagram, and capture the dependencies for the various resources of the application that you are migrating.

   A cloud engineer can use this build plan to create the application infrastructure in Deploy Accelerator.

### <a id="migrate" name="migrate"></a>Migrate servers

![](/images/rean-migrate/rm_flow3.PNG)

You must perform the following steps for each application group that you want to migrate to the cloud.

1. Ensure that the appropriate discovery job is selected in the **Pick Discovery Job** box at the top.

2. On the Home page, from the left panel, select the application group that you want to migrate.

3. To start the migration process, click the **Migrate** icon (![](/images/rean-migrate/icon_migrate.PNG)).

4. On the Create Migration Job page, perform the following actions:

   - Enter the migration name and description.

      ![](/images/rean-migrate/rm_createmigration.PNG)

   - From the **Migration Service** list, select the appropriate migration service.

      _**Note:** Migrate Accelerator currently supports only **CloudEndure** as a migration service._

   - From the **Migration Configuration** list, select the appropriate configuration.

      The migration configuration is a predefined set of credentials to access the selected migration service and the authentication details for the cloud service provider in which Migrate Accelerator must create images of the servers. For the CloudEndure migration service, it also defines the Live Migration project from which Migrate Accelerator must migrate servers.

      For information about creating migration configurations, see <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-migrate', viewPage: 'discover-and-migrate-resources', viewSection: 'mig-config'})" style="text-decoration:none">Create migration configurations</a>.

   - _(Optional)_ To enable Migrate Accelerator to install CloudEndure agents on the servers that need to be migrated, perform the following actions:

      - Select **Auto install agents**.

         Ensure that the servers in the data center meet the following requirements for installing the CloudEndure agent.

         | Operating system | Supported versions | Software requirements                 |
         | ---------------- | ------------------ | ------------------------------------- |
         | Windows          | - 2016<br>- 2012   | .NET framework 4.5                    |
         | Ubuntu           | - 16.04<br>- 14.04 | - Python 2.4 or higher<br>- GNU Wget  |
         | Red Hat Linux    | 7.6                | - Python 2.4 or higher<br/>- GNU Wget |

         _**Note:** Consider the following points if Migrate Accelerator is unable to auto install the CloudEndure agent on the servers in the data center:_

         - _Ensure that the folder that was specified in the **com.reancloud.migration.server.windows.agent_folder** property in the **application.properties** file while deploying Migrate Accelerator exists on the Windows servers in the data center._

         - _For secure connection to Windows servers, ensure that the thumbprint of the certificates that were copied to the **ca-certs** folder while deploying Migrate Accelerator matches the WinRM HTTPS Listener certificate thumbprint._

         - _Ensure that the Linux servers in the data center have access to a valid YUM repository._

         - _For Ubuntu 16.04 servers, run the following command to set the symbolic link for the appropriate version of Python:_

           ```
           ln -s python<Version> python
           ```

           _**For example:** To set the symbolic link for Python 2.7, run the following command:_

           ```
           ln -s python2.7 python
           ```

         - To enable Migrate Accelerator to connect to Ubuntu and Red Hat Linux servers with the user name and key (instead of password) that is specified in the selected connection, ensure that the user has sudo access with NOPASSWD.

           To set the PASSWD for the user, run the following command on the Ubuntu or Red Hat Linux server:

           ```
           sudo visudo
           ```

           In the file that opens, enter the following property:

           <USERNAME> ALL = NOPASSWD: ALL

      - _(To connect to Linux servers in the data center)_ From the **Linux Connection** list, select the appropriate SSH migration connection.

      - _(To connect to Windows servers in the data center)_ From the **Windows Connection** list, select the appropriate WinRM migration connection.

         For information about creating connections, see <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-migrate', viewPage: 'discover-and-migrate-resources', viewSection: 'connection'})" style="text-decoration:none">Configure connections</a>.

      When you start the migration job, Migrate Accelerator connects to the servers in the application group by using the SSH or WinRM connection that you have specified and installs the CloudEndure agent on the servers.

      _**Note:** If you do not select the **Auto install agents** check box, ensure that you have manually installed the CloudEndure agents on the servers in the data center. For more information about installing the CloudEndure agents, see the [CloudEndure documentation](https://docs.cloudendure.com/#Installing_the_CloudEndure_Agents/Installing_the_CloudEndure_Agents.htm)._

   - To start the migration process, click **CREATE MIGRATION**.

      You can view the status of your migration job on the following page:

      ![](/images/rean-migrate/rm_migrationstatus.PNG)

      To view the status of the agent installation process for a server, click the **Action** icon (![](/images/rean-migrate/icon_action.PNG))  next to that server in the Server List panel and then select **Logs**.

      The **Migration Tool Status** column displays the CloudEndure status for each server in the application group. You can also view the overall migration status in Migrate Accelerator in the chart on the right panel.

      After the server replication is successful, the **Migration Tool Status** column displays the **Ready for Test** status.

5. Perform the following actions for each server in the application group:

   - To launch a test instance for the server, click the **Action** icon (![](/images/rean-migrate/icon_action.PNG)) and select **Launch Test Instance**.

   - After the test instance is successfully launched, create an image from the test instance by clicking the **Action** icon and selecting **Create Image**. 

      Migrate Accelerator uses the provider that is configured in the migration job to create the images. The image ID appears in **Image ID** the column.

   - To confirm that the server data has been successfully replicated, perform the following actions:

      - Sign in to the AWS Management Console.
      - Launch an EC2 instance by using the image ID (AMI) that you have created through Migrate Accelerator.
      - Connect to the EC2 instance and confirm that the server data has been successfully replicated.

   - After confirming that the server data has been successfully replicated, stop the server data replication by clicking the **Action** icon and selecting **Launch Cutover Instance**.

      This action also uninstalls the agent from the server in your data center.

   - To create the final image of the server, click the **Action** icon and select **Create Image**.

      Migrate Accelerator uses the provider that is configured in the migration job to create the images.  The new image ID is updated in the **Image ID** column.

6. _(Optional)_ <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-migrate', viewPage: 'discover-and-migrate-resources', viewSection: 'migrate-resource'})" style="text-decoration:none">Use migrated resources in Deploy Accelerator</a>.

### <a id="migrate-resource" name="migrate-resource"></a>Use migrated resources in Deploy Accelerator

![](/images/rean-migrate/rm_flow4.PNG)

1. In a browser, type your Cloud Accelerator Platform URL.

2. Sign in to Cloud Accelerator Platform.

3. On the Home page of Deploy Accelerator, create a new environment for one of the migrated applications.

   Ensure that you select the same provider and region as your target environment in the Live Migration project in CloudEndure.

4. From the **Resources** tab in the left panel, drag an EC2 Instance resource to the canvas.

5. Click the resource you have created and in the right panel, enter the AMI ID of your migrated server and other attribute details.

6. Repeat steps 4 and 5 for each migrated server that is a part of the application that you want to deploy.

7. To build your environment, drag additional network and other resources to the canvas. 

8. Create appropriate dependencies between these resources.

9. Save the environment.

10. Start a deployment of this environment.

For more information about creating and deploying environments in Deploy Accelerator, see the _<a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-deploy', viewPage: 'deploy-and-manage-environments', viewSection: 'Content'})" style="text-decoration:none">Deploy and manage environments</a>_.

## <a id="view" name="view"></a>Viewing the overall migration status for application groups

You can view the overall migration status for one or more application groups in a discovery job.

1. Ensure that the appropriate discovery job is selected in the **Pick Discovery Job** box at the top.

2. In the icon panel, click **DISCOVERY VIEW**.

3. From the left panel, select the application groups for which you want to view the dashboard.

   ![](/images/rean-migrate/rm_dashboard.PNG)

   You can view the following information on the dashboard:

   | Panel         | Description                                                  |
   | ------------- | ------------------------------------------------------------ |
   | DISCOVERED    | This panel displays the total number of discovered servers in your data center. |
   | AGENTS        | This panel displays the total number of servers on which Migrate Accelerator is currently installing the CloudEndure agents, the total number of servers on which the agents are successfully installed, and the total number of servers on which the agents failed to be installed.<br><br>_**Note:** When the agent installation process starts, the Discovered panel displays 0 discovered servers. Instead, these servers are displayed as INSTALLING, COMPLETE, or FAILED in the AGENTS panel._ |
   | MIGRATIONS    | This panel displays the total number of servers that are being currently migrated, total number of servers that were successfully migrated, and total number of servers that failed to be migrated.<br><br>_**Note:** When the migration process starts, the AGENTS panel displays 0 COMPLETE servers. Instead, these servers are displayed as MIGRATING, COMPLETE, or FAILED in the MIGRATIONS panel._ |
   | Migrated jobs | This panel displays the migration jobs that were run for the selected application group. You can view the job name, job description, job start time, and the migration tool that was used. |
