---
title: Administer Deploy Accelerator
---

# Administer Deploy Accelerator

Hitachi Cloud Accelerator Platform - Deploy (Deploy Accelerator) is a deployment automation platform that is used to deploy and configure environments reliably and consistently. This topic describes how to configure Deploy Accelerator.

## <a id="Content" name="Content"></a>Contents
* <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-deploy', viewPage: 'administer', viewSection: 'bp-configure'})" style="text-decoration:none">Configuring the Blueprint Gallery</a>
* <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-deploy', viewPage: 'administer', viewSection: 'package-type'})" style="text-decoration:none">Configuring the environment package types</a>
* <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-deploy', viewPage: 'administer', viewSection: 'access-token'})" style="text-decoration:none">Configuring the default access token for the packages repository</a>
* <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-deploy', viewPage: 'administer', viewSection: 'chef-server'})" style="text-decoration:none">Registering a Chef Server in Deploy Accelerator</a>
* <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-deploy', viewPage: 'administer', viewSection: 'package-share'})" style="text-decoration:none">Sharing Chef Server packages and roles</a>
* <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-deploy', viewPage: 'administer', viewSection: 'chef-sync'})" style="text-decoration:none">Synching with a registered Chef Server</a>
* <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-deploy', viewPage: 'administer', viewSection: 'configuration'})" style="text-decoration:none">Configuring Deploy Accelerator</a>
* <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-deploy', viewPage: 'administer', viewSection: 'customize-email'})" style="text-decoration:none">Customizing Deploy Accelerator email messages</a>

## <a id="bp-configure" name="bp-configure"></a>Configuring the Blueprint Gallery

The Blueprint Gallery is a repository of blueprints that can be templates of industry-standard cloud or IT infrastructure architectures or custom solutions. Users can leverage blueprints to quickly create infrastructure for solutions. For more information, see <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-deploy', viewPage: 'deploy-and-manage-environments', viewSection: 'blueprint'})" style="text-decoration:none">Creating new environments from blueprints</a>.<br>

Users can <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-deploy', viewPage: 'deploy-and-manage-environments', viewSection: 'export-blueprint'})" style="text-decoration:none">export their environments as blueprints</a> and <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-deploy', viewPage: 'deploy-and-manage-environments', viewSection: 'bp-gallery'})" style="text-decoration:none">add the blueprints in the Blueprint Gallery</a>.<br>

**To configure the Blueprint Gallery, perform the following actions:**

1. Connect to the EC2 instance on which Hitachi Cloud Accelerator Platform is deployed.

2. Locate the **${PLATFORM_HOME}/rean-deploy/conf** folder.

3. If the **dnow.properties** file is not available in this folder, create the file.

4. To display the **Blueprint Gallery** option when users click the **More options** icon (![](/images/rean-platform-common/icon_more.PNG)) icon in the top-right corner of the Deploy Accelerator Home page, add the **com.reancloud.platform.show_blueprints** property and set its value to **true**, as shown below.

   **com.reancloud.platform.show_blueprints=true**

   _**Note:** To once again hide the **Blueprint Gallery** option, you must update the value of the **com.reancloud.platform.show_blueprints** property to **false**._

5. To configure the Blueprint Gallery repository in the Artifactory that is used for Deploy Accelerator, add the **dnow.blueprintsGallery.artifactory_repo_name** property and set its value to the appropriate repository name.

   Only blueprints that are uploaded to the specified repository appear in the Blueprint Gallery. For more information, see <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-deploy', viewPage: 'deploy-and-manage-environments', viewSection: 'bp-gallery'})" style="text-decoration:none">adding blueprints in the Blueprint Gallery</a>.

   _**Note:** You must ensure that Deploy Accelerator users who are allowed to add blueprints in the Blueprint Gallery have access to the Artifactory and the specified repository._

6. <a id="bp-syncconfig" name="bp-syncconfig"></a>_(Optional)_ To modify the default interval between two successive syncs of the blueprint metadata that is shown in the Blueprint Gallery with the Artifactory, add the **dnow.blueprintsGallery.sync.interval** property and specify the appropriate value in minutes.

   The default interval between two successive syncs is 30 minutes. 

   **Example:** To modify the sync interval to an hour, you must update the property value to 60 (unit of measurement for this property is minutes), as shown in the example below:

   **dnow.blueprintsGallery.sync.interval=60**

   _**Note:**_

   - _The blueprint metadata that is synchronized contains the blueprint name, description, version, and image name._
   - _Updated image files with the same name are not synchronized. Therefore, the old image continues to be shown in the Blueprint Gallery._

7. Save the **dnow.properties** file.

8. Restart the **rean-deploy** service.

## <a id="package-type" name="package-type"></a>Configuring the environment package types

Deploy Accelerator provides out-of-the-box support for Chef Solo, Chef Server, Ansible, and Puppet. However, only Chef Solo and Chef Server are configured as the default environment package types. While creating an environment, users can select either Ansible Solo, Chef Solo, or Chef Server as the environment package type.<br>

Based on the requirements, administrators can choose to individually configure Chef Solo, Chef Server, Ansible Solo, Puppet, or a combination of these three as the environment package types.<br>

_**Important:** To configure the environment package types, you must have administrative access to the instance on which Cloud Accelerator Platform is deployed._

**To configure the environment package type, perform the following actions:**

1. Connect to the EC2 instance on which Cloud Accelerator Platform is deployed.

2. Locate the **${PLATFORM_HOME}/rean-deploy/conf** folder.

3. If the **dnow.properties** file is not available in this folder, create the file.

4. If the **com.reancloud.platform.deploy.environment.configuration_types** property is not available in the **dnow.properties** file, add the property.

5. Set the value of the **com.reancloud.platform.deploy.environment.configuration_types** property to the appropriate environment package types, as shown in the example below:

   *Example for Chef package:*

   **com.reancloud.platform.deploy.environment.configuration_types=chef-solo,chef-server**

   *Example for Ansible package:*

   **com.reancloud.platform.deploy.environment.configuration_types=ansible-solo**

   The supported values for this property are **chef-solo**, **chef-server**, **ansible-solo** and **puppet**. By default, Deploy Accelerator supports Ansible Solo, Chef Solo and Chef Server as the environment package types.

6. _(Optional)_ If Chef Server is configured as the environment package type, update the following additional properties.

   - To access the Chef Server without self-signed SSL certificates, add the **chefserver.no_verify_ssl** property and set its value to **true**, as shown below:

      **chefserver.no_verify_ssl=true**

      _**Note:** To once again enable access to the Chef Server with self-signed SSL certificates, you must update the value of the **chefserver.no_verify_ssl** property to **false**._

   - To modify the interval between two successive syncs with the Chef Server, add the **hcap.chefserver.sync.interval** property and set its value (in minutes), as shown in the example below:

     **hcap.chefserver.sync.interval=30**

     The default interval between two successive syncs is 10 minutes. After each successful sync, any cookbooks, roles, and groups that are added or updated in the Chef Server become available in Deploy Accelerator.

7. Save the **dnow.properties** file.

8. Restart the **rean-deploy** service.

## <a id="access-token" name="access-token"></a>Configuring the default access token for the packages repository

Users can add their own custom (or user-defined) packages based on the environment package types that are configured. In the package definition, they have to define the repository type, package download URL, and the access token for the repository.<br>

Administrators must define the default access token for the packages repository (GitHub or GitLab). If users do not specify an access token while adding a user-defined package, Deploy Accelerator uses this default access token to download the package.<br>

**To configure the default access token for the packages repository, perform the following actions:**

1. Connect to the EC2 instance on which Cloud Accelerator Platform is deployed.

2. Locate the **${PLATFORM_HOME}/rean-deploy/conf** folder.

3. If the **dnow.properties** file is not available in this folder, create the file.

4. In the **dnow.properties** file, locate one of the following properties based on the repository type in which packages are stored:

   - dnow.git.access.token
   - dnow.gitlab.access.token

   If the property is not available in the **dnow.properties** file, add the property.

5. Set the value of the property to the default access token for accessing the packages repository.

6. Save the **dnow.properties** file.

7. Restart the **rean-deploy** service.

## <a id="chef-server" name="chef-server"></a>Registering a Chef Server in Deploy Accelerator

By default, Deploy Accelerator supports Chef Solo and Chef Server as the environment package types. While creating an environment, users can choose whether they want to use Chef Solo or Chef Server packages to configure compute instances.<br>

While users can add their own custom (or user-defined) Chef Solo packages, only administrators can register a Chef Server in Deploy Accelerator. When you register a Chef Server, cookbooks (along with all the recipes it contains) and roles from that Chef Server become available in Deploy Accelerator. In addition, groups from the selected Chef Server organization are automatically created in Cloud Accelerator Platform. You can then manually share each package (or cookbook) and role with these groups and assign appropriate permissions.<br>

When users select the Chef Server package type while creating an environment, they also have to select the registered Chef Server. For that environment, the **Packages** tab displays packages (or cookbooks) and roles from the selected Chef Server only. However, users can see only the packages and roles that are shared with a group to which they belong. While adding a Chef Server package (or cookbook) to a resource, users can select multiple recipes in the order in which they must be run on the resource. If no recipe is selected, Deploy Accelerator runs the default recipe defined in the cookbook.<br>

_**Note:** Deploy Accelerator polls the registered Chef Server every 10 minutes for new and updated cookbooks and roles. However, new groups that are added in the registered Chef Server are not automatically shown in Cloud Accelerator Platform. To view the latest cookbooks, roles, and groups at any given time, you can manually <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-deploy', viewPage: 'administer', viewSection: 'chef-sync'})" style="text-decoration:none">sync with the registered Chef Server</a>._<br>

**Before you begin**

Before you register a Chef Server, you must map the IP address and host name of that Chef Server in the **/etc/hosts** file of the Deploy Accelerator docker container.  

1. Connect to the EC2 instance on which Deploy Accelerator is deployed.

2. To connect to the Deploy Accelerator docker container, run the following command:

    `docker exec -it containerID bash`

   In this command, specify the ID of the Deploy Accelerator docker container.

3. To open the **etc/hosts** file, run the following command 

   `vi /etc/hosts`

4. In the **etc/hosts** file, add an entry that maps the IP address and hostname of the Chef Server.

   _**Note:** If you have configured a load balancer for the Chef Server, you must map the IP address and host name of that load  balancer._

**To register a Chef Server in Deploy Accelerator, perform the following actions:**

1. In the Chef Server organization that you want to configure in Deploy Accelerator, ensure that the  **clients** group is a member of all other groups in that organization.

   If you do not perform this action, groups are not automatically created in Deploy Accelerator. 

2. On the Home page, click the **More options** icon (![](/images/rean-platform-common/icon_more.PNG)) icon in the top-right corner and then click **Chef Servers**.

3. On the Chef Server page, click **NEW**.

   ![](/images/rean-deploy/chefserver_add.PNG)

4. Enter the following details about the Chef Server that you want to configure in Deploy Accelerator:

   | Field        | Description                                                  |
   | ------------ | ------------------------------------------------------------ |
   | Name         | Enter a unique name for the Chef Server.                     |
   | Type         | Select the type of Chef Server that you want to configure. The available options are **Chef**, **OpsWorks**, and **Enterprise Chef**. |
   | Host Name    | Enter the host name of the Chef Server that you want to configure in Deploy Accelerator.<br>**Example:** chef-server.example.com |
   | Description  | Enter details about the Chef Server that you are configuring. |
   | Organization | Enter the organization from which you want to display packages in Deploy Accelerator. |
   | Client       | Enter the name of the Chef client that Deploy Accelerator must use to connect to the Chef Server. This client must be installed on the Chef Server. |
   | Client Key   | Enter the key that Deploy Accelerator must use to connect to the Chef client that you have specified. |

5. Click **SAVE**.

   A new Chef Server appears under the **Chef Server List** section.

   In addition, groups from the selected Chef Server organization are automatically created in Cloud Accelerator Platform. The naming convention used for these groups is **organizationName-groupName**.

6. Add users to the groups (from the Chef Server organization) that have been created in Cloud Accelerator Platform. 

   For more information, see <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-platform-common', viewPage: 'administer', viewSection: 'groups'})" style="text-decoration:none"> Managing groups</a>.

7. <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-deploy', viewPage: 'administer', viewSection: 'package-share'})" style="text-decoration:none">Share each Chef Server package and role with the appropriate groups</a>.

   By default, only administrators can view the Chef Server packages and roles. 

8. _(Optional)_ To configure access to the Chef Server without self-signed SSL certificates, add the **chefserver.no_verify_ssl** property in the **dnow.properties** file and set its value to **true**. 

   For more information, see <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-deploy', viewPage: 'administer', viewSection: 'package-type'})" style="text-decoration:none">Configuring the environment package types</a>.


## <a id="package-share" name="package-share"></a>**Sharing Chef Server packages** and roles

By default, Chef Server packages (or cookbooks) and roles are shared with only administrators. You can control access to Chef Server packages and roles by sharing them with specific groups and assigning appropriate permissions. 

1. On the Home page, click the **More options** icon (![](/images/rean-platform-common/icon_more.PNG) icon in the top-right corner and then click **Packages**.

   The Package List page displays packages and roles from the Chef Server that is registered in Deploy Accelerator. The **Package Type** column enables you to identify a Chef Server package or role and the **Chef Server** column enables you to identify the Chef Server from which the package or role is displayed.

2. To share one or more Chef Server packages or roles, select the check box next to those packages and roles and then click **SHARE**.

   ![](/images/rean-deploy/rd_packagelist.PNG)

3. In the Share Packages window, click the **Share** icon (![](/images/rean-deploy/icon_sharegroup.PNG)) icon for the **Group** with which you want to share the selected packages and roles.

   ![](/images/rean-deploy/rd_packagesharegroups.PNG)

   _**Note:**_

   - _When a Chef Server is registered, all groups in the selected Chef Server organization are also automatically created in Cloud Accelerator Platform. The naming convention used for these groups is **organizationName-groupName**. However, you can add new groups or manage users in these groups. For more information, see <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-platform-common', viewPage: 'administer', viewSection: 'groups'})" style="text-decoration:none">Managing groups</a>._
   - _New groups that are added in the registered Chef Server are not automatically displayed in Cloud Accelerator Platform. To view the new groups, you must manually <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-deploy', viewPage: 'administer', viewSection: 'chef-sync'})" style="text-decoration:none">sync with the registered Chef Server</a>._

4. Select the permissions that you want to grant to the group and click **DONE**.

   ![](/images/rean-deploy/rd_packagesharepermissions.PNG)

   _**Note:** If you have selected multiple packages and roles, any permissions that were previously assigned to the packages and roles are not displayed._

5. _(Optional)_ To share the packages and roles with additional groups, repeat steps 3 and 4.

6. Read the warning message and perform one of the following actions:

   - If you want to proceed with sharing the packages, select the Warning check box and click **SUBMIT**.

      All users who are members of the selected groups can now view the packages and roles in Deploy Accelerator. The actions that they can perform on the packages and roles are based on the selected permissions.

      _**Note:** Sharing of Chef Server packages and roles with the selected groups might take several minutes_

   - If you no longer want to share the packages, click **CANCEL**.

## <a id="chef-sync" name="chef-sync"></a>Synching with a registered Chef Server

When you register a Chef Server with Deploy Accelerator, cookbooks (along with all the recipes it contains) and roles from that Chef Server become available in Deploy Accelerator. In addition, groups from the selected Chef Server organization are automatically created in Cloud Accelerator Platform.<br>

Deploy Accelerator polls the registered Chef Server every 10 minutes for new and updated cookbooks and roles. However, new groups that are added in the selected Chef Server organization are not automatically shown in Cloud Accelerator Platform. To view the latest cookbooks, roles, and groups at any given time, you can manually sync with the registered Chef Server.<br>

Based on your requirements, you can also modify the default interval between two successive syncs with the Chef Server. For more information, see <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-deploy', viewPage: 'administer', viewSection: 'package-type'})" style="text-decoration:none">Configuring the environment package types</a>.<br>

_**Note:** Any new cookbooks, roles, and groups that are added in the Chef Server also become available when you manually update the Chef Server details in Deploy Accelerator._

**To sync with a registered Chef Server, perform the following actions:**

1. On the Home page, click the **More options** icon (![](/images/rean-platform-common/icon_more.PNG)) icon in the top-right corner and then click **Chef Servers**.

2. On the ChefServer List page, click the **Sync Chef Server** (![](/images/rean-deploy/icon_chefserverrefresh.PNG)) icon next to the Chef Server.

   In the Chef Server Last Sync window, you can view the start time, end time, and status (InProgress, Success, or Failed) of the most recent sync, as shown in the following image.

   ![](/images/rean-deploy/chefserversync.PNG)

3. Click **Sync Chef Server**.

   If the previous sync is in progress, you have to wait for it to complete before starting another sync with the registered Chef Server.

## <a id="configuration" name="configuration"></a>Configuring Deploy Accelerator

To update the Deploy Accelerator configuration properties, you must have administrative access to the instance on which Cloud Accelerator Platform is deployed.

1. Connect to the EC2 instance on which Cloud Accelerator Platform is deployed.
2. Locate the **${PLATFORM_HOME}/rean-deploy/conf** folder.
3. If the **dnow.properties** file is not available in this folder, create the file.
4. If the <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-deploy', viewPage: 'administer', viewSection: 'properties'})" style="text-decoration:none">configuration properties</a> that you want to update are not available in the **dnow.properties** file, add those properties.
5. Set the value of the appropriate properties in the **dnow.properties** file.
6. Save the **dnow.properties** file.
7. Restart the **rean-deploy** service.

### <a id="properties" name="properties"></a>Deploy Accelerator configuration properties

The following sections list the Deploy Accelerator configuration properties that you can update based on your requirements:

- <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-deploy', viewPage: 'administer', viewSection: 'general-properties'})" style="text-decoration:none">General properties</a>
- <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-deploy', viewPage: 'administer', viewSection: 'email-properties'})" style="text-decoration:none">Email properties</a>
- <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-deploy', viewPage: 'administer', viewSection: 'package-properties'})" style="text-decoration:none">Package properties</a>
- <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-deploy', viewPage: 'administer', viewSection: 'artifactory-properties'})" style="text-decoration:none">Artifactory properties</a>
- <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-deploy', viewPage: 'administer', viewSection: 'bpgallery-properties'})" style="text-decoration:none">Blueprint Gallery properties</a>
- <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-deploy', viewPage: 'administer', viewSection: 'helm-properties'})" style="text-decoration:none">Helm Provider properties</a>

#### <a id="general-properties" name="general-properties"></a>General properties

| Property | Description                                                  | Default value |
| -------- | ------------------------------------------------------------ | ------------- |
| dnow.url | Defines the URL to access Deploy Accelerator.<br><br>The URL specified must be https://*ipAddress*, where *ipAddress* refers to the public IP address of the instance on which Deploy Accelerator is installed. |               |

#### <a id="email-properties" name="email-properties"></a>Email properties

| Property                                           | Description                                                  | Default value                      |
| -------------------------------------------------- | ------------------------------------------------------------ | ---------------------------------- |
| send_status_mails                                  | Enables or disables the sending of status emails for an environment. | true                               |
| com.hcap.deploy.notification.deployment-initiation | Enables or disables the sending of destroy initiation email for all environments in Deploy Accelerator.<br><br>_**Note**: The environment-level setting has the highest precedence, followed by the user-level setting, and finally the application-level setting._ | true                               |
| com.hcap.deploy.notification.deployment-completion | Enables or disables the sending of deploy or destroy completion emails for all environments in Deploy Accelerator.<br><br>_**Note**: The environment-level setting has the highest precedence, followed by the user-level setting, and finally the application-level setting._ | true                               |
| smtp.host                                          | Defines the host name of the SMTP server from which deployment status emails must be sent to users. | email-smtp.us-east-1.amazonaws.com |
| smtp.port                                          | Defines the port on which the SMTP server can be accessed.   | 587                                |
| smtp.username                                      | Defines the user name that must be used to access the SMTP server from which emails are sent to users.<br><br>This property is required only if you have enabled authentication for your SMTP server. |                                    |
| smtp.password                                      | Defines the encrypted password for the user name that must be used to access the SMTP server.<br><br>This property is required only if you have enabled authentication for your SMTP server. |                                    |
| from.email                                         | Defines the From email address that is used in status emails that are sent to users. | rean.noreply@hitachivantara.com    |
| mail.destroying_started.subject                    | Defines the subject of the email that is sent when an environment starts being destroyed. | Environment destroying started     |
| mail.destroy_failed.subject                        | Defines the subject of the email that is sent when an environment is not destroyed successfully. | Environment deployment failed      |
| mail.deploy_successful.subject                     | Defines the subject of the email that is sent when an environment is successfully deployed. | Environment deployment successful  |
| mail.environment_status.subject                    | Defines the subject of the email that is sent to inform users about the deployment status of an environment. | Environment deployment status      |

#### <a id="package-properties" name="package-properties"></a>Package properties

| Property                                                     | Description                                                  | Default value         |
| ------------------------------------------------------------ | ------------------------------------------------------------ | --------------------- |
| com.reancloud.platform.deploy.environment.configuration_types | Defines the environment package types that are displayed when users create an environment.<br><br>The supported values for this property are **chef-server**, **chef-solo**, and **puppet**. | chef-solo,chef-server |
| chefserver.no_verify_ssl                                     | To disable SSL certificate validation when a self-signed certificate is configured for the registered Chef Server, set the value of this property as **true**. | false                 |
| hcap.chefserver.sync.interval                                | Defines the interval (in minutes) between two successive syncs with the registered Chef Server.<br><br>Defines the interval (in minutes) between two successive syncs with the registered Chef Server.<br><br>After each successful sync, any new cookbooks, roles, and groups that are added in the Chef Server become available in Deploy Accelerator. | 10                    |
| dnow.git.access.token                                        | Defines the access token for the GitHub repository from which Deploy Accelerator must download packages.<br>If users do not provide an access token while adding user-defined packages, Deploy Accelerator uses this default access token to download the packages from the GitHub repository. |                       |
| dnow.gitlab.access.token                                     | Defines the access token for the Git Lab repository from which Deploy Accelerator must download packages.<br><br>If users do not provide an access token while adding user-defined packages, Deploy Accelerator uses this default access token to download the packages from the Git Lab repository. |                       |

#### <a id="artifactory-properties" name="artifactory-properties"></a>Artifactory properties

| Property                                     | Description                                                  | Default value       |
| -------------------------------------------- | ------------------------------------------------------------ | ------------------- |
| com.reancloud.platform.artifactory_support   | Defines whether a repository is configured for Deploy Accelerator. | true                |
| com.reancloud.platform.artifactory_repo_type | Defines the type of repository that is configured for Deploy Accelerator. | Jfrog               |
| com.reancloud.platform.artifactory_url       | Defines the URL to access the artifactory.                   |                     |
| com.reancloud.platform.artifactory_username  | Defines the username to access the artifactory.              |                     |
| com.reancloud.platform.artifactory_api_key   | Defines the API key of the username that you have specified. This API key must have all required permissions to access the artifactory. |                     |
| com.reancloud.platform.super_market_repo     | Defines the repository in which Chef cookbooks are stored. In an offline deployment, Deploy Accelerator downloads Chef cookbooks from this repository. | virtual-supermarket |

#### <a id="bpgallery-properties" name="bpgallery-properties"></a>Blueprint Gallery properties

| Property                                     | Description                                                  | Default value |
| -------------------------------------------- | ------------------------------------------------------------ | ------------- |
| com.reancloud.platform.show_blueprints       | Shows or hides the **Blueprint Gallery** option when users click the **More options** icon (![](/images/rean-platform-common/icon_more.PNG)) icon in the top-right corner of the Deploy Accelerator Home page. | false         |
| dnow.blueprintsGallery.artifactory_repo_name | Defines the repository in which blueprints are stored. Deploy Accelerator shows blueprints from this repository in the Blueprint Gallery. |               |
| dnow.blueprintsGallery.sync.interval         | Defines the interval (in minutes) between two successive syncs of the blueprint metadata that is shown in the Blueprint Gallery with the Artifactory.<br><br>The blueprint metadata that is synchronized contains the blueprint name, description, version, and image name. | 30            |

#### <a id="helm-properties" name="helm-properties"></a>Helm Provider properties

These properties are for the default helm repository from which Deploy Accelerator downloads helm charts while deploying environments with the <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-deploy', viewPage: 'deploy-and-manage-environments', viewSection: 'helm-details'})" style="text-decoration:none">Helm provider type</a>. Users do not have to add the **Helm Repository** data source in their environment if their helm chart is available in this repository.

| Property                                       | Description                                                  | Default value |
| ---------------------------------------------- | ------------------------------------------------------------ | ------------- |
| com.reancloud.deploy.helm.repository.name      | Chart repository name                                        | true          |
| com.reancloud.deploy.helm.repository.url       | Chart repository URL                                         | true          |
| com.reancloud.deploy.helm.repository.key_file  | Identify HTTPS client using this SSL key file                | false         |
| com.reancloud.deploy.helm.repository.cert_file | Identify HTTPS client using this SSL certificate file        | false         |
| com.reancloud.deploy.helm.repository.ca_file   | Verify certificates of HTTPS-enabled servers using this CA bundle | false         |
| com.reancloud.deploy.helm.repository.username  | Username for HTTP basic authentication                       | false         |
| com.reancloud.deploy.helm.repository.password  | Password for HTTP basic authentication                       | false         |

## <a id="customize-email" name="customize-email"></a>Customizing Deploy Accelerator email messages

When the deployment of an environment has succeeded or failed, an email is sent to the user whose email address is specified at the time of deploying the environment. Similarly, when an environment starts being destroyed, an email is sent to the specified email address.<br>

All emails related to an environment are also sent to the registered email address of the user who has created the environment, also known as the owner of the environment. You can choose to <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-deploy', viewPage: 'administer', viewSection: 'email-owner'})" style="text-decoration:none">configure the sending of status emails for environments</a>.<br>

The content of these emails is based on the default email templates that are selected. You can choose to <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-deploy', viewPage: 'administer', viewSection: 'email'})" style="text-decoration:none">create custom email templates</a> and even <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-deploy', viewPage: 'administer', viewSection: 'subject'})" style="text-decoration:none">customize the subject of status emails</a>.

_**Important:** To customize Deploy Accelerator email messages, you must have administrative access to the instance on which Cloud Accelerator Platform is deployed._

### <a id="email-owner" name="email-owner"></a>Configure the sending of status emails for environments

1. Connect to the EC2 instance on which Cloud Accelerator Platform is deployed.

2. Locate the **${PLATFORM_HOME}/rean-deploy/conf** folder.

3. If the **dnow.properties** file is not available in this folder, create the file.

4. In the **dnow.properties** file, locate the **send_status_mails** property.

   If this property is not available in the **dnow.properties** file, add the property.

5. To stop sending status emails for environments, change the value of the **send_status_mails** property to **false**, as shown in the example below:

   **send_status_mails=false** 

6. Save the **dnow.properties** file.

7. Restart the **rean-deploy** service.

_**Note:** To once again send status emails for environments, update the value of the **send_status_mails** property to **true**._

### <a id="subject" name="subject"></a>Customize the subject of status emails

1. Connect to the EC2 instance on which Cloud Accelerator Platform is deployed.

2. Locate the **${PLATFORM_HOME}/rean-deploy/conf** folder.

3. If the **dnow.properties** file is not available in this folder, create the file.

4. In the **dnow.properties** file, locate the following properties:

   - **mail.destroying_started.subject**
   - **mail.destroy_failed.subject**
   - **mail.deploy_successful.subject**
   - **mail.environment_status.subject**

   If these properties are not available in the **dnow.properties** file, add the properties.

5. Update the value of these properties.

6. Save the **dnow.properties** file.

7. Restart the **rean-deploy** service.

### <a id="email" name="email"></a>Create a custom email template

1. *(Optional)* To add data about an environment in the email template, perform the following actions:

   - In Deploy Accelerator, open the environment for which you are creating a custom email template.

   - From the left panel, click the **Resources** tab, and drag the **Output** resource to the canvas.

   - Rename the resource and click it to open the right panel.

   - On the **RESOURCE** tab, select the **Set Json** link for the **output** attribute.

   - In the Set Json value for : output window, define the output variables that you want to use in the email template, as shown in the example below:

     ```json
     {
       "ip": {
         "value": "${output_1.public_ip}"
       },
       "privateip": {
         "value": "${output_1.private_ip}"
       },
       "first_name": {
         "value": "peter"
       },
       "last_name": {
         "value": "morgan"
       }
     }
     ```

   - Click **Set Value**.

   - To update your changes to the environment, click **Save**. 

2. Create a new HTML file.

3. In the HTML file, add the content to be included in the email.

4. *(Optional)* Based on your requirements, use the custom output variables that you defined in step 1. You can also use any of the following output variables in the email content:

   | Output variable | Description                                                  |
   | --------------- | ------------------------------------------------------------ |
   | $status         | Displays the status of the deployment                        |
   | $envName        | Displays the name of the environment for which an email is being sent to the user |
   | $url            | Displays the URL to access Deploy Accelerator                |

5. Save the HTML file.

   Ensure that the file name enables users to easily identify the purpose of the template. For example, you can use the name **customerName_deploysuccess.html**.

6. Connect to the EC2 instance on which Cloud Accelerator Platform is installed.

7. Locate the **${PLATFORM_HOME}/rean-deploy/dnow-data-dir/email-templates** folder.

   _**Note:** If the **email-templates** folder is not available, you must create the folder._

8. Copy the custom email template file that you have created to the **email-templates** folder.

_**Note:** The custom email templates are not displayed in the Deploy Accelerator UI. Therefore, you must share the list of custom email templates with other Deploy Accelerator users as required. Users have to manually enter the names of these email templates before <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-deploy', viewPage: 'deploy-and-manage-environments', viewSection: 'deploy'})" style="text-decoration:none">starting new deployments of an environment</a> . Alternatively, users can <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-deploy', viewPage: 'deploy-and-manage-environments', viewSection: 'config'})" style="text-decoration:none">configure an environment</a> to use these templates for all its deployments._
