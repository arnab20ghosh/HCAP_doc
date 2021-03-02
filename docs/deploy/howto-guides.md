---
title: How-to guides for Deploy Accelerator
---

# <a id="deploy-howto" name="deploy-howto"></a>How-to guides for Deploy Accelerator

The How-to guides for Deploy Accelerator focus on achieving specific goals, performing common tasks, or resolving specific issues. These guides include high-levels steps or detailed procedures with examples to help you to quickly accomplish your goals.<br>

For step-by-step instructions on performing various tasks in Deploy Accelerator, see <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-deploy', viewPage: 'deploy-and-manage-environments', viewSection: 'Content'})" style="text-decoration:none">Deploy and manage environments</a>.

## Contents

- <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-deploy', viewPage: 'how-to-guides-deploy', viewSection: 'env-import-existing'})" style="text-decoration:none">How do I import a new version of an existing environment?</a>
- <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-deploy', viewPage: 'how-to-guides-deploy', viewSection: 'env-upgrade'})" style="text-decoration:none">How do I upgrade an existing environment?</a>
- <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-deploy', viewPage: 'how-to-guides-deploy', viewSection: 'collaborate'})" style="text-decoration:none">How do I collaborate with other users?</a>
- <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-deploy', viewPage: 'how-to-guides-deploy', viewSection: 'access-entities'})" style="text-decoration:none">How do I access entities of a user who has left the organization?</a>
- <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-deploy', viewPage: 'how-to-guides-deploy', viewSection: 'template-file'})" style="text-decoration:none">How do I create a template file?</a>
- <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-deploy', viewPage: 'how-to-guides-deploy', viewSection: 'generate-keypair'})" style="text-decoration:none">How do I dynamically generate a key pair for an EC2 instance?</a>

## <a id="env-import-existing" name="env-import-existing"></a>How do I import a new version of an existing environment?

Deploy Accelerator allows you to import a blueprint as a new version of an existing environment. For example, say that you created a new environment in Deploy Accelerator by importing a blueprint from the Blueprint Gallery or your computer. And an updated version of this blueprint is now available. Deploy Accelerator allows you to import this updated blueprint as a new version of the existing environment.<br>

While you can import a blueprint with the same name as an existing environment, the version must be unique.<br>

_**Important:** Importing a blueprint as a new version of an existing environment does not affect any of the existing deployments of the environment._<br>

**High-level steps to import a new version of an existing environment**

1. Open the existing environment and note the name and existing version numbers of this environment.

2. Based on your requirements, perform one of the following actions:

   - To import a blueprint from your computer, click the **More** icon (![](/images/rean-deploy/icon_more_bar.PNG)) on the canvas and then click **Import**.
   - To import a blueprint from the Blueprint Gallery, click the **More options** icon (![](/images/rean-platform-common/icon_more.PNG)) in the top-right corner of the Home page and then click **Blueprint Gallery**. On the Blueprint Gallery page, click **IMPORT** for the new blueprint version that you want to import.

   For detailed information about the different ways in which you can import a blueprint in Deploy Accelerator see, <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-deploy', viewPage: 'deploy-and-manage-environments', viewSection: 'blueprint'})" style="text-decoration:none">Creating new environments from blueprints</a>.

3. In the Import Environments window, perform the following actions:

   - Enter the same name as your existing environment.

   - Enter a unique version up to a maximum of 40 characters.

     It is recommended that the version you specify is greater than all versions of your existing environment. However, you can also specify an existing version and append it with a dash (-) followed by a custom alphanumeric value (for example, **02.10.18-updated**). Ensure that there is no space before the dash (-) and the custom value that you specify does not contain a colon (:).

   - Select the appropriate connection and provider.

   - If Chef Server is set as the environment package type, select the Chef Server and chef environment. 

4. Click **IMPORT ALL**.

   The blueprint is imported as a new version of your existing environment.

5. Click the version list on the canvas.

   You can see the previous versions of the existing environment in this list.

6. _(Optional)_ <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-deploy', viewPage: 'deploy-and-manage-environments', viewSection: 'compare'})" style="text-decoration:none">Compare differences</a> between the version that you have imported and previous versions of the existing environment.

7. _(Optional)_ <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-deploy', viewPage: 'deploy-and-manage-environments', viewSection: 'deploy'})" style="text-decoration:none">Start a new deployment</a> of the environment version that you have imported.

   None of the existing deployments of the environment are impacted. To see the list of deployments across all versions of the existing environment, see <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-deploy', viewPage: 'deploy-and-manage-environments', viewSection: 'view-deploy'})" style="text-decoration:none">Viewing deployments</a>.

   If required, you can also redeploy an existing deployment with the new environment version. For more information, see <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-deploy', viewPage: 'deploy-and-manage-environments', viewSection: 'redeploy'})" style="text-decoration:none">Redeploying existing deployments</a>.  

## <a id="env-upgrade" name="env-upgrade"></a>How do I upgrade an existing environment?

When you create an environment and start a deployment, Deploy Accelerator creates the resources using the configured provider. After an environment is deployed in production, you can choose to continue to make updates in the same environment. However, this approach makes it difficult to keep a track of changes to an environment over time. Instead, it is recommended that you release the environment to freeze any updates to that environment. When you want to upgrade this existing environment (add or update resources), you can create a new environment version.<br>

**High-level steps to upgrade an existing environment**

1. <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-deploy', viewPage: 'deploy-and-manage-environments', viewSection: 'create-env'})" style="text-decoration:none">Create a new environment</a> and <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-deploy', viewPage: 'deploy-and-manage-environments', viewSection: 'resource'})" style="text-decoration:none">add resources</a> as required. 

   To provision any compute resources in the environment, also <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-deploy', viewPage: 'deploy-and-manage-environments', viewSection: 'packages'})" style="text-decoration:none">add appropriate packages</a> to those resources.

   _**Important:** Deploy Accelerator cannot deploy packages on compute resources that are already deployed. Therefore, you must add the appropriate packages to a resource before you start a deployment of the environment._

   _**Best practice:** If you need to frequently deploy new versions of a package on a resource, you can <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-deploy', viewPage: 'deploy-and-manage-environments', viewSection: 'create-layered-env'})" style="text-decoration:none">create a layered environment</a>. The parent environment can contain all your infrastructure resources, while the child environment can contain the **Virtual VM** resource to which you can add the appropriate package version. Each time you update the package version on the **Virtual VM** resource, you can destroy and redeploy the child environment--without having to destroy the parent environment that contains the infrastructure._

2. <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-deploy', viewPage: 'deploy-and-manage-environments', viewSection: 'deploy'})" style="text-decoration:none">Start a deployment</a> of the environment.

   Each environment can have multiple deployments, such as Staging and Production.  

3. _(Optional)_ After the production deployment of the environment completes successfully, <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-deploy', viewPage: 'deploy-and-manage-environments', viewSection: 'version-release'})" style="text-decoration:none">release the environment</a>.

   Releasing an environment ensures that no further updates can be made to the existing environment.

   If you <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-deploy', viewPage: 'deploy-and-manage-environments', viewSection: 'redeploy'})" style="text-decoration:none">redeploy existing deployments</a> of a released environment, already deployed resources are not impacted. This is because during a redeployment, only updates to deployed resources are considered.

4. To upgrade the existing environment that has been released, perform the following actions:

   - <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-deploy', viewPage: 'deploy-and-manage-environments', viewSection: 'env-version'})" style="text-decoration:none">Create a new environment version</a>.
   - In the new environment version, add or update resources as required.
   - Save the environment.
   - _(Optional)_ <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-deploy', viewPage: 'deploy-and-manage-environments', viewSection: 'compare'})" style="text-decoration:none">Compare differences</a> between the two environment versions.

5. To upgrade the existing (production) deployment based on the new environment version, perform the following actions:

   - From the deployments list on the canvas, select the existing deployment that you want to upgrade.

   - To view the plan for the existing deployment, click the **Plan** icon (![](/images/rean-deploy/icon_envplan.PNG)) and select **Plan Selected Deployment**.

   - In the Review and Plan: Environment Name window, select the new environment version that you have created and **PLAN**.

     The deployment plan shows the new or updated resources that will be deployed. The already deployed resources that were not updated in the new environment version are not impacted.

   - To redeploy the existing deployment, click the **Re-Deploy** icon (![](/images/rean-deploy/icon_envredeploy.PNG)).

   - On the **Deployment** tab, from the Environment Version list, select the new environment version that you have created.

   - Select the Confirmation check box and click **UPGRADE**.

     The production deployment gets associated with the new environment version. 

## <a id="collaborate" name="collaborate"></a>How do I collaborate with other users?

Deploy Accelerator allows you to collaborate with other users on environments and related entities. You can share environments that you have created with multiple groups.<br>

When you share an environment, you can also define share permissions for groups. Based on the assigned share permissions, users in these groups can view, edit, export, and delete the environment. You can also enable these users to start and destroy their own deployments of the shared environment.<br>

The provider, connection, and deployments associated with the shared environment are not automatically shared. You can choose to separately share the provider, connection, and deployments and assign the appropriate permissions to the same set of groups. Otherwise, users in the groups with the deploy permission can use their own providers to start new deployments of the shared environment.

**Examples**

The following examples highlight the different benefits of collaborating with other users:

- The networking team can share the network environment and its Production deployment with the database and application teams and assign only the View permission. These teams can view and use the network deployment as the parent deployment for their own deployments.
- The application team can comprise multiple members who need to start deployments of the application environment. For example, different QA team members might need to start QA deployments of the application. The owner can share the environment with these users and assign permissions to deploy and destroy their own deployments.

**High-level steps to collaborate with other users**

1. Request your Deploy administrator to <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-platform-common', viewPage: 'administer', viewSection: 'add-group'})" style="text-decoration:none">create a new group</a>, assign the appropriate policies (access level) to the group, and add users to the group.

2. _(Optional)_ If you plan to use the registered Chef Server in your environment, request the administrator to <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-deploy', viewPage: 'administer', viewSection: 'package-share'})" style="text-decoration:none">share the appropriate Chef Server packages and roles</a> with the new group.

3. <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-deploy', viewPage: 'deploy-and-manage-environments', viewSection: 'environments'})" style="text-decoration:none">Create a new environment</a> and select the appropriate provider and connection for the environment.

   While creating an environment, you can choose to share the environment with appropriate groups. However, you can also create the environment and later <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-deploy', viewPage: 'deploy-and-manage-environments', viewSection: 'collaboration'})" style="text-decoration:none">share that environment</a> with the appropriate groups.

   By default, only the current environment version is shared with the selected groups. While <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-deploy', viewPage: 'deploy-and-manage-environments', viewSection: 'env-version'})" style="text-decoration:none">creating a new version of this environment</a>, you can choose to apply the share permissions from the base environment.

4. _(Optional)_ Share the <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-deploy', viewPage: 'deploy-and-manage-environments', viewSection: 'share-provider'})" style="text-decoration:none">provider</a> and <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-deploy', viewPage: 'deploy-and-manage-environments', viewSection: 'share-connection'})" style="text-decoration:none">connections</a> used in the environment with the same group.

5. _(Optional)_ When you <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-deploy', viewPage: 'deploy-and-manage-environments', viewSection: 'deploy'})" style="text-decoration:none">start a new deployment</a> of the environment, <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-deploy', viewPage: 'deploy-and-manage-environments', viewSection: 'deploy-share'})" style="text-decoration:none">share this deployment</a> with the appropriate group.

   When you share the environment, its deployments are not automatically shared with the group. You have to separately share each deployment with the appropriate groups and assign share permissions.

_**Note:** If multiple users in a group are working simultaneously on a shared environment or another shared entity, Deploy Accelerator shows an error message in case of any conflicts. For example, say **User A** has added a resource named **vpc** to a shared environment and **User B** also tries to add a resource named **vpc**, an error message is shown to **User B**. This error message is shown even if **User A** has not saved the environment after adding the **vpc** resource._

## <a id="access-entities" name="access-entities"></a>How do I access entities of a user who has left the organization?

If a user who leaves an organization has shared environments and other entities with a group, all members of that group can continue to access these shared entities. However, if the user has not shared any environments, deployments, providers, and connections, no other user can automatically access these entities. In this case, the Deploy administrator can disable the user and share all the user's entities with one or more groups.

For detailed step-by-step instructions, see <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-platform-common', viewPage: 'administer', viewSection: 'disable-user'})" style="text-decoration:none">Disable an existing user</a>.

**Example**

**User A**, **User B**, and **User C** are members of the **Application Blueprints** group in Deploy Accelerator. The three users share all their environments and deployments with this group, making it possible for them to access each other's entities. 

**User C** leaves the organization without sharing his most recent environments and deployments with the **Application Blueprints** group. Now no one (including **User A** and **User B**) can access these environments and deployments.

**User A** and **User B** have to spend time recreating **User C's** environments. Also, they cannot destroy any resources that **User C** has deployed. To resolve these issues, the Deploy administrator can disable **User C** and share all the user's entities with the **Application Blueprint** group. Now, **User A** and **User B** can access and work with **User C's** environments, deployments, providers, and connections.

## <a id="template-file" name="template-file"></a>How do I create a template file?

Deploy Accelerator enables you to render a template file from a template string by using the **Template** data source. Ideally, this template string should be loaded from an external file (**Local file** resource). However, you can also use an inline template string in the **Template** data source.<br>

**To create a template file by using the Template resource, perform the following actions:**

1. Create or open the environment in which you want to generate a template file. 

2. _(Optional)_ To load the template string from an external file, perform the following actions:

   - From the **Resources** tab in the left panel, drag the Local file resource to the canvas.

   - In the Resource Name window, enter a name for the resource and click **CREATE**.

   - In the **name** attribute, enter the name of the template file you want to create (for example, **init.tpl**).

   - In the **content** attribute, click **Set text**, enter the template string in the Set String value for window, and click **SET VALUE**.

     To escape interpolation, use double dollar signs ($$).

3. From the **Resources** tab in the left panel, drag the **Template** data source to the canvas.

4. In the **vars** attribute, click **Set Json**, enter the variables in the Set Json value for window, and click **SET VALUE**.

   **Example:**

   ```json
   {
     "keystore_password": "password"
   }
   ```

5. In the **template** attribute, click **Set text**, and perform one of the following actions:

   - If you have already added the template string in the **Local file** resource, specify the file path, as shown in the example below.

     ```bash
     "${file("${path.module}/init.tpl")}"
     ```

   - Add an inline template string, as shown in the example in the image below. 

     Consider the following points when using dollar signs ($) in the inline template string:

     - To indicate a variable defined in the **vars** attribute of the **Template** data source, you must use double dollar signs ($$).

       In the example, double dollar signs are used to refer to the **keystore_password** variable. When you start a deployment, **$${keystore_password}** will be rendered as **${keystore_password}** in the template file.

     - To escape interpolation, the template file needs to use double dollar signs. However, if you are using an inline template string to generate the template file, you must use four dollar signs ($$$$).

       In the example, **$$$${my_pass}** will be rendered as **$${my_pass}** in the template file. 

     ![](/images/rean-deploy/TemplateInlineString.PNG)

6. Save the environment. 

## <a id="generate-keypair" name="generate-keypair"></a>How do I dynamically generate a key pair for an EC2 instance?

The following procedure describes an example of how you can use the **TLS Private Key Generator** and **Key Pair** resources to dynamically generate a key pair and associate it with an AWS EC2 instance.

1. On the canvas, click the **Create Environment** icon (![](/images/rean-deploy/icon_envcreate.PNG)).

2. In the Create Environment window, enter the name as **TLS_PrivateKey**, add a description for this environment, specify the version as 01.00.00, select the appropriate environment package type, connection, and provider, and click **CREATE**.

3. To add the **TLS Private Key Generator** resource to the environment, perform the following actions: 

   - From the **Resources** tab in the left panel, drag the **TLS Private Key Generator** resource to the canvas.

   - In the Resource Name window, enter the name as **AppTLSPrivateKeyGen** and click **CREATE**.

     ![](/images/rean-deploy/scenario_ssh_02.PNG)

4. To add the **Key Pair** resource to the environment, perform the following actions:

   - From the **Resources** tab in the left panel, drag the **Key Pair** resource to the canvas.

   - In the Resource Name window, enter the name as **AppKeypair** and click **CREATE**.

     ![](/images/rean-deploy/scenario_ssh_04.PNG)

   - Select the **AppKeypair** resource and on the **Resource** tab in the right panel that opens, enter the following attribute values:

     - **key_name:** AppKeypair

     - **public_key:** ${AppTLSPrivateKeyGen.public_key_openssh}

       In the **public_key** attribute, you must use the interpolation syntax to reference the **public_key_openssh** attribute value of the **TLS Private Key Generator** resource that you created in step 3.

5. To add the **Instance** resource to the environment, perform the following actions:

   - From the **Resources** tab in the left panel, drag the **Instance** resource to the canvas.

   - In the Resource Name window, enter the name as **AppServer** and click **CREATE**.

     ![](/images/rean-deploy/scenario_ssh_06.PNG)

   - Select the **AppServer** resource and on the **Resource** tab in the right panel that opens, enter the following value for the **key_name** attribute:

     ${AppKeypair.key_name}

     In the **key_name** attribute, you must use the interpolation syntax to reference the **key_name** attribute value of the **Key Pair** resource that you created in step 4.

   - In the **Connection** attribute, select **Use Custom Connection** and then click **Set Json** for the **Custom Connection** attribute.

   - In the Set Json value for: customConnection window, enter the content shown below and click **SET VALUE**.

     ```
     { 
        "private_key": "${AppTLSPrivateKeyGen.private_key_pem}",
        "user": "ubuntu",
        "type": "ssh"
     }
     ```

     In the interpolation syntax for the **private_key** parameter, you must use the interpolation syntax to reference the **private_key_pem** attribute value of the **TLS Private Key Generator** resource that you created in step 3.

   - In the **ami** and **instance_type** attributes, specify the appropriate values.

6. Click the **Save** icon (![](/images/rean-deploy/icon_envsave.PNG)).

7. _(Optional)_ To use this dynamically generated key pair in another environment, perform the following actions: 

   - From the **Resources** tab in the left panel, drag the **Output** resource to the canvas.

   - Select the **output** resource and on the **Resource** tab in the right panel that opens, click **Set Json** for the **output** attribute.

   - In the Set Json value for: output window, enter the content as shown below and click **SET VALUE**.

     ```
     { 
         "ssh_private_key": { 
         "value": "${AppTLSPrivateKeyGen.private_key_pem}"  
          },
         "key_name": {
         "value": "${AppKeypair.key_name}"
         }
     }
     
     ```

   - To save the environment and define the output, click the **Save** icon (![](/images/rean-deploy/icon_envsave.PNG)).

8. To start a new deployment, perform the following actions:

   - Click the **Deploy** icon (![](/images/rean-deploy/icon_envdeploy.PNG)).
   - On the **Deployment** tab, enter the deployment name and description.
   - Click **START NEW DEPLOYMENT**.

9. _(Optional)_ Open the other environment in which you want to use the dynamically generated key pair and perform the following actions: 

   - From the **Resources** tab in the left panel, drag the **Depends On** resource to the canvas.

   - In the Resource Name window, enter the name as **depends-on** and click **CREATE**.

   - Click the **depends-on** resource.

   - In the right panel that opens, on the **Resource** tab, enter **TLS_PrivateKey** in the **Depends_On** attribute.

   - From the **Resources** tab in the left panel, drag the **Instance** resource to the canvas.

   - In the Resource Name window, enter the name as **instance-dynamic-key** and click **CREATE**.

   - Select the **instance-dynamic-key** resource and on the **RESOURCE** tab in the right panel that opens, enter **${depends-on.key_name}** in the **key_name** attribute.

     In this interpolation syntax, **key_name** is the variable that you have defined in the **output** resource of the **TLS_PrivateKey** environment in step 7.

   - In the **Connection** attribute, select **Use Custom Connection** and then click **Set Json** for the **Custom Connection** attribute.

   - In the Set Json value for: customConnection window, enter the content shown below, and click **SET VALUE**.

     ```
      { 
           "private_key": "${depends-on.ssh_private_key}",
           "user": "ubuntu",
           "type": "ssh"
      }
     
     ```

     In the **private_key** parameter, use the interpolation syntax to reference the **ssh_private_key** variable that you have defined in the **output** resource of the **TLS_PrivateKey** environment in step 7.

   - Click the **Save** icon (![](/images/rean-deploy/icon_envsave.PNG)).

   - Click the **Deploy** icon (![](/images/rean-deploy/icon_envdeploy.PNG)) to open the Review and Deploy: *EnvironmentName* window.

   - On the **Deployment** tab, enter the deployment name and description, select the parent deployment name, and then click **START NEW DEPLOYMENT**.
