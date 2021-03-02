---
title: Prerequisites for using Workflow Accelerator
---

# <a id="prereq" name="prereq"></a>Prerequisites for using Workflow Accelerator

<a id="content" name="content"></a>Before you start using Hitachi Cloud Accelerator Platform - Workflow Accelerator to <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-workflow', viewPage: 'create-and-register-solution-packages', viewSection: 'create-sp'})" style="text-decoration:none">create</a> and <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-workflow', viewPage: 'deploy-solution-packages', viewSection: 'deploy-sp'})" style="text-decoration:none">deploy</a> solution packages, you must perform the following prerequisite actions:

- <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-workflow', viewPage: 'prerequisites', viewSection: 'hcap-instance'})" style="text-decoration:none">Creating an account in Hitachi Cloud Accelerator Platform</a>
- <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-workflow', viewPage: 'prerequisites', viewSection: 'cloud-account'})" style="text-decoration:none">Creating a cloud provider</a>
- <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-workflow', viewPage: 'prerequisites', viewSection: 'deploy-learn'})" style="text-decoration:none">Learning about Deploy Accelerator</a>

After completing the prerequisites the next steps are to <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-workflow', viewPage: 'understand-solution-package-schema', viewSection: 'sp-schema'})" style="text-decoration:none">understand the solution package schema</a> and then <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-workflow', viewPage: 'create-and-register-solution-packages', viewSection: 'Content'})" style="text-decoration:none">create and register</a> and <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-workflow', viewPage: 'deploy-solution-packages', viewSection: 'Content'})" style="text-decoration:none">deploy</a> solution packages.

## Creating an account in Hitachi Cloud Accelerator Platform

To perform actions in Workflow Accelerator, you require a user account in Hitachi Cloud Accelerator Platform. For more information about creating your account, see <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-platform-common', viewPage: 'createAndAccessAccount', viewSection: 'create'})" style="text-decoration:none">Creating a Cloud Accelerator Platform account.</a><br>

Contact your Cloud Accelerator Platform administrator to ensure that your user account is a member of the following groups:

- SOLUTION_PACKAGE_USER
- SOLUTION_PACKAGE_DEPLOYMENT_USER
- CLOUD_ARCHITECT
- HELM_USER

For information about the access level granted by these groups, see <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-platform-common', viewPage: 'administer', viewSection: 'default-groups'})" style="text-decoration:none">Default groups</a>.

## Creating a cloud account 

To deploy resources in the cloud using solution packages, create an account for the appropriate cloud service provider (for example, Amazon Web Services). Workflow Accelerator supports all <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-deploy', viewPage: 'deploy-and-manage-environments', viewSection: 'providerlist'})" style="text-decoration:none">cloud providers that Deploy Accelerator supports</a>.

Ensure that your cloud account has the access to deploy the required resources.

## Learning about Deploy Accelerator

Workflow Accelerator works closely with Hitachi Cloud Accelerator Platform - Deploy (Deploy Accelerator). Therefore, it is recommended that you have a good knowledge of Deploy Accelerator, especially how to <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-deploy', viewPage: 'deploy-and-manage-environments', viewSection: 'environments'})" style="text-decoration:none">create environments</a>, <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-deploy', viewPage: 'deploy-and-manage-environments', viewSection: 'provider'})" style="text-decoration:none">configure providers</a>, <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-deploy', viewPage: 'deploy-and-manage-environments', viewSection: 'bp-tips'})" style="text-decoration:none">export environments as blueprints</a>, and <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-deploy', viewPage: 'deploy-and-manage-environments', viewSection: 'deploy'})" style="text-decoration:none">start new deployments</a>.

For more information, see <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-deploy', viewPage: 'overview', viewSection: 'overview'})" style="text-decoration:none">Overview of Deploy Accelerator</a>.

