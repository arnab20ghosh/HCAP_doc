---
title: Administer Test Accelerator
---

# Administer Test Accelerator

Hitachi Cloud Accelerator Platform - Test (Test Accelerator) is a cloud-based, DevOps-centric, test automation solution that dynamically creates infrastructure to perform rapid in-parallel cross-browser, functional, scale, and infrastructure testing. 

## <a id="properties" name="properties"></a>Configuring Test Accelerator

You can view and edit the Test Accelerator Configurations for multiple categories, such as Mail and SMTP, Artifactory Details. These parameters are set while deploying Test Accelerator.

1. On the Home page of Test Accelerator, click the **More options** icon (![](/images/rean-platform-common/icon_more.PNG)) in the top-right corner.

2. Click **Configuration**. The configurations appear under the **Properties** tab.

   ![](/images/rean-test/rt_configproperty.PNG)

3. Click the appropriate category, and edit one or more properties based on your requirements.

   The following table describes the categories of properties that you can configure:

   | Category              | Description                                                  |
   | --------------------- | ------------------------------------------------------------ |
   | Miscellaneous         | This section contains the Help Documentation URL.            |
   | Artifactory Details   | This section contains properties used for configuring the Artifactory URL and authentication details and the location of the ZIP files that contain the sample automation codes. |
   | Mail and SMTP         | This section contains properties used for configuring the Test Accelerator for sending emails to its users, related to test jobs. |
   | Kubernetes Properties | This section contains properties used for configuring pods in the Kubernetes cluster for Test Accelerator. If the parameters in Kubernetes properties are left blank, then the default values from Kubernetes cluster are used. |

4. To save modified values, click **SUBMIT**.

5. To restore all values to system default, click **RESTORE DEFAULT VALUES**.

   