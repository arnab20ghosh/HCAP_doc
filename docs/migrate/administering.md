---
title: Administer Migrate Accelerator
---

# Administer Migrate Accelerator

Hitachi Cloud Accelerator Platform - Migrate (Migrate Accelerator) helps you to migrate applications that are running in your existing data centers to the cloud. This topic describes how to configure Migrate Accelerator.

## <a id="configuration" name="configuration"></a>Configuring Migrate Accelerator

To update the Migrate Accelerator configuration properties, you must have administrative access to the instance on which Hitachi Cloud Accelerator Platform is deployed.

1. Connect to the EC2 instance on which Cloud Accelerator Platform is deployed.
2. Locate the **${PLATFORM_HOME}/rean-migrate** folder.
3. If the **application.properties** file is not available in this folder, create the file.
4. If the <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-migrate', viewPage: 'administer', viewSection: 'properties'})" style="text-decoration:none">configuration properties</a> that you want to update are not available in the **application.properties** file, add those properties.
5. Set the value of the appropriate properties in the **application.properties** file.
6. Save the **application.properties** file.
7. Restart the **rean-migrate** service.

### <a id="properties" name="properties"></a>Migrate Accelerator configuration properties

The following table lists the Migrate Accelerator configuration properties that you can update based on your requirements.

| Property                                                     | Description                                                  |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| com.reancloud.migration.server.linux.agent_folder            | Applies to Linux servers that Migrate Accelerator has to migrate to the cloud.<br><br>It defines the full path of the folder in which Migrate Accelerator must automatically install the CloudEndure migration agent. This folder must be accessible on all Linux servers. |
| com.reancloud.migration.server.windows.agent_folder          | Applies to Windows servers that Migrate Accelerator has to migrate to the cloud.<br><br>It defines the full path of the folder in which Migrate Accelerator must automatically install the CloudEndure migration agent. This folder must be accessible on all Windows servers. |
| com.reancloud.platform.migrate.winrm.port                    | Applies to Windows servers that Migrate Accelerator has to migrate to the cloud.<br><br>It defines the WinRM port through which Migrate Accelerator can initiate installation of the CloudEndure migration agent over an unencrypted communication channel.<br><br>**Default Value:** 5985 |
| com.reancloud.platform.migrate.winrm.https.port              | Applies to Windows servers that Migrate Accelerator has to migrate to the cloud.<br><br>It defines the WinRM port through which Migrate Accelerator can initiate installation of the CloudEndure migration agent over a secure communication channel.<br><br>**Default Value:** 5986 |
| com.reancloud.platform.migrate.migration_status_thread_pool_size | Maximum size of the pool of worker threads that Migrate Accelerator must dedicate to the migration management actions. For example, initiating CloudEndure agent installation and retrieving status of migration from CloudEndure.<br><br>**Default Value:** 10 |
| com.reancloud.migrate.server.thread.delay                    | Number of milliseconds that Migrate Accelerator must wait before invoking recurring migration management actions. For example, initiating agent installation and retrieving status of migration from CloudEndure.<br><br>**Default Value:** 15,000 |


