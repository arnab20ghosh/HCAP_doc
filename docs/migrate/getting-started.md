---
title: Overview of Migrate Accelerator
---

# <a id="overview" name="overview"></a>Overview of Migrate Accelerator

Hitachi Cloud Accelerator Platform - Migrate (Migrate Accelerator) helps you to easily migrate applications that are running in your existing data centers to the cloud as servers or containers in a easy and automated way. You can use these migrated server images in <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-deploy', viewPage: 'overview'})" style="text-decoration:none">Hitachi Cloud Accelerator Platform - Deploy (Deploy Accelerator)</a> and build and deploy the infrastructure.<br>

Migrate Accelerator brings in data from Discovery tools and creates logical application groups of the discovered servers. However, you can change the default grouping of servers based on your requirements. Migrate Accelerator also enables you to generate a build plan for each application group of the discovered servers. In the build plan, Migrate Accelerator automatically populates server details, such as host name and operating system. You can download and use this build plan to capture other details that are required to plan the migration of your application infrastructure to the cloud.<br>

After you have finalized the servers in an application group, you can create a migration job in Migrate Accelerator, which uses a migration tool to start the server replication process. You can test that the servers have been successfully replicated and the migrated application is working correctly and then perform the cutover and create the final server images. However, before the cutover, you must carefully plan the downtime for the application that is being migrated.<br>

For information about using Migrate Accelerator, see the <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-migrate', viewPage: 'discover-and-migrate-resources', viewSection: 'Content'})" style="text-decoration:none">Discover and migrate resources</a> topic.