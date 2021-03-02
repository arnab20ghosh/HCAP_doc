---
title: Deploy Accelerator info byte 6
---

# <a id="info-06" name="info-06"></a>Deploy Accelerator info byte 6: Packages

Packages in Hitachi Cloud Accelerator Platform - Deploy (Deploy Accelerator) can leverage different infrastructure automation tools to configure compute instances in an environment. Deploy Accelerator includes out-of-the-box support for Chef Solo, Chef Server, and Puppet. You can add and manage your own custom Chef Solo or Puppet packages. You can also leverage an existing setup of Chef Servers to configure compute instances in an environment.<br>

Deploy Accelerator also provides a few utility packages for specific use cases. For example, the **file** package enables you to upload a file on a compute instance and the **execute-script** package enables you to run a command on a compute instance.

## Why use packages

The following are a couple of advantages of using packages:

- You can **automate the configuration of compute instances** in your environment. For example, at the end of a deployment, you can get a compute instance that has Tomcat and NGINX installed on it.

- You can **create a package for your own custom application** and deploy it on a compute instance in the environment.

## Related topics

- <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-deploy', viewPage: 'deploy-and-manage-environments', viewSection: 'user-package'})" style="text-decoration:none">Adding user-defined packages</a>
- <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-deploy', viewPage: 'deploy-and-manage-environments', viewSection: 'create-package-version'})" style="text-decoration:none">Creating new package versions</a>
- <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-deploy', viewPage: 'administer', viewSection: 'chef-server'})" style="text-decoration:none">Registering Chef servers in Deploy Accelerator</a>



------

<a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-deploy-infobytes', viewPage: 'info05', viewSection: ''})" style="text-decoration:none"><< Previous info byte</a> | <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-deploy-infobytes', viewPage: 'info', viewSection: ''})" style="text-decoration:none">Deploy Accelerator info bytes</a> | <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-deploy-infobytes', viewPage: 'info07', viewSection: ''})" style="text-decoration:none">Next info byte >></a>

