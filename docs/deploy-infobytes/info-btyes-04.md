---
title: Deploy Accelerator info byte 4
---

# <a id="info-04" name="info-04"></a> Deploy Accelerator info byte 4: Environment versions and releases

Each environment in Hitachi Cloud Accelerator Platform - Deploy (Deploy Accelerator) can have multiple versions. When an environment version is ready for production, you can release that version. Once released, an environment version cannot be updated. To add or update resources in the environment, you have to create a new environment version. Deploy Accelerator also enables you to redeploy existing deployments with new environment versions.<br>

Environment versions and releases in Deploy Accelerator ensure that you do not have to maintain multiple environments for the same application (or workload). Each time you need to upgrade an application you can just create a new environment version.

## Why create environment versions and releases

The following are a couple of advantages of environment versions and releases:

- You can create environment versions to ensure that a record is maintained of the changes that are made to an environment.
  The Compare feature enables you to easily identify the differences between two environment versions.
- You can release an environment version to ensure that no changes can be made to the deployed production resources.

## Related topics

- <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-deploy', viewPage: 'deploy-and-manage-environments', viewSection: 'env-version'})" style="text-decoration:none">Creating new environment versions</a>
- <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-deploy', viewPage: 'deploy-and-manage-environments', viewSection: 'version-release'})" style="text-decoration:none">Releasing environment versions</a>
- <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-deploy', viewPage: 'deploy-and-manage-environments', viewSection: 'compare'})" style="text-decoration:none">Comparing differences between environments</a>



------

<a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-deploy-infobytes', viewPage: 'info03', viewSection: ''})" style="text-decoration:none"><< Previous info byte</a> | <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-deploy-infobytes', viewPage: 'info', viewSection: ''})" style="text-decoration:none">Deploy Accelerator info bytes</a> | <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-deploy-infobytes', viewPage: 'info05', viewSection: ''})" style="text-decoration:none">Next info byte >></a>