---
title: Overview of Test Accelerator
---

# <a id="overview" name="overview"></a>Overview of Test Accelerator

Testing an application to identify major problems and fixing them is an important part of the Product Release Cycle. The speed of testing is one of the critical pillars of DevOps. Hitachi Cloud Accelerator Platform - Test (Test Accelerator) is a cloud-based, DevOps-centric, test automation solution that dynamically creates infrastructure to perform rapid in-parallel cross-browser, functional, and scale (load) testing.<br>

You can integrate your existing automation code with Test Accelerator and run automated (cross browser) tests on your web applications. Test Accelerator also enables you to do a URL check or perform manual testing of your web application on different combinations of browsers. In addition, the infrastructure test covers the testing of your IT infrastructure, such as servers, network switches, and routers.<br>

For each test job, you can view when the job was last run and the total number of browsers in different states (Configuring, Running, Success, and Failed). You can view an HTML report of a test run for a specific browser and a summary report of the test runs for all browsers. On the Home page of Test Accelerator, you can also view the total number of test cases passed and releasable builds.<br>

Test Accelerator runs on Kubernetes and launches Kubernetes pods to run different types of tests. For browser-based tests, pods are launched based on the number of browsers in the test job. For infrastructure and API tests, a pod is launched for each infrastructure or API test job.

For information about using Test Accelerator, see the <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-test', viewPage: 'run-tests', viewSection: 'Content'})" style="text-decoration:none">Run tests</a> topic. For information about configuring Test Accelerator, see the <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-test', viewPage: 'administer', viewSection: 'Content'})" style="text-decoration:none">Administer Test Acelerator</a> topic.

The following image shows the Home page of Test Accelerator:

![](/images/rean-test/rt_dashboard.PNG)
