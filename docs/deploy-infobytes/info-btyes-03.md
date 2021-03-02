---
title: Deploy Accelerator info byte 3
---

# <a id="info-03" name="info-03"></a>Deploy Accelerator info byte 3: Multiple deployments of an environment

After you have designed the infrastructure for a solution in Hitachi Cloud Accelerator Platform - Deploy (Deploy Accelerator), you have to create the resources in the selected cloud platform. For that, you have to start a deployment of the environment.<br>

Ideally, you will want to test the environment before you deploy it in production. Deploy Accelerator enables you to start and maintain multiple deployments of the same environment. For example, you can start a QA deployment, and if it is successful, you can start a new production deployment.<br>

Deploy Accelerator also enables you to configure different resource values for each deployment of the same environment. For example, you can define different VPC IDs for the QA and production deployments.

## Why start multiple deployments of an environment

The following are a few advantages of having multiple deployments of the same environment:

- You can **maintain different deployments for QA** (testing the IT infrastructure), **staging, and production**.
- You can **maintain multiple production deployments of the same environment**.
  For example, say two departments have to deploy applications in different networks. In this case, you can create a network environment based on industry-standard IT infrastructure architecture. You can then have two production deployments with different resource values (such as VPC IDs, security groups, and subnets) for the two departments.
- You can **implement the Blue-Green deployment technique** by having two simultaneous production deployments.

## Related topic

<a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-deploy', viewPage: 'deploy-and-manage-environments', viewSection: 'endtoend-overview'})" style="text-decoration:none">End-to-end process for multiple deployments of an environment</a>



------

<a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-deploy-infobytes', viewPage: 'info02', viewSection: ''})" style="text-decoration:none"><< Previous info byte</a> | <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-deploy-infobytes', viewPage: 'info', viewSection: ''})" style="text-decoration:none">Deploy Accelerator info bytes</a> | <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-deploy-infobytes', viewPage: 'info04', viewSection: ''})" style="text-decoration:none">Next info byte >></a>