---
title: Deploy Accelerator info byte 2
---

# <a id="info-02" name="info-02"></a>Deploy Accelerator info byte 2: Layered environments

Hitachi Cloud Accelerator Platform - Deploy (Deploy Accelerator) enables you to create two types of environments:

- **Standalone environments**, which include all the required resources and do not depend on any other environment.
- **Layered environments**, which are a collection of multiple environments in which some environments (child environments) are dependent on other environments (parent environments). In a layered environment, resources in child environments can reference resource values from parent environments.

You can create layered environments for complex IT infrastructures. For example, instead of adding network, database, and application resources in the same environment, you can create separate environments for each set of resources and then create a dependency between the environments. An Instance resource in the application environment can reference the subnet and security group values from the network environment

## Why use layered environments

The following are a few advantages of using layered environments to create the IT infrastructure:

- You can **easily update, deploy, and destroy a set of resources** in the parent or child environments without affecting resources in the other environments. You have to redeploy the other environments only if any resource values that they reference have been updated.
- You can **create a common network environment as the parent environment**. And then create child environments for each application that you want to deploy in this network. Resources in each child application environment can reference resource values from the parent network environment.
- You can **configure different ownership for each environment within a layered environment**. For example, the network team can own the network environment while different application teams can only view this environment and use it as a parent for their own application environments.

## Related topics

- <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-deploy', viewPage: 'deploy-and-manage-environments', viewSection: 'layered-env'})" style="text-decoration:none">Overview of layered environments</a>
- <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-deploy', viewPage: 'deploy-and-manage-environments', viewSection: 'scenario-layered'})" style="text-decoration:none">Creating a layered environment</a>



------

<a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-deploy-infobytes', viewPage: 'info01', viewSection: ''})" style="text-decoration:none"><< Previous info byte</a> | <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-deploy-infobytes', viewPage: 'info', viewSection: ''})" style="text-decoration:none">Deploy Accelerator info bytes</a> | <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-deploy-infobytes', viewPage: 'info03', viewSection: ''})" style="text-decoration:none">Next info byte >></a>