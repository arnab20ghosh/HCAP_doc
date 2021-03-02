---
title: Overview of Assess Accelerator
---

# <a id="overview" name="overview"></a>Overview of Assess Accelerator

Hitachi Cloud Accelerator Platform - Assess ( Assess Accelerator) is a tool that automates the assessment of your cloud environment against relevant security and compliance standards. It contains out-of-the-box policies that help you to assess if your cloud infrastructure meets the best-practice standards and requirements for security, operations, and cost-optimization.<br>

Assess Accelerator supports the following assessment tools:
- **HCAP Assess:** This is an inbuilt tool, which can be used for security, operations, and cost optimization assessments of AWS cloud infrastructure.
- **Prowler:** This is an open-source third-party tool, which can be used for security assessments of AWS cloud infrastructure.
- **Azure CIS Blueprint**: This tool is an Azure service which uses an Azure blueprint to execute CIS checks on Azure cloud accounts. This tool is used for running security assessments of Azure cloud infrastructure. 

For each assessment tool, Assess Accelerator provides a <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-assess', viewPage: 'assess-checks', viewSection: 'Content'})" style="text-decoration:none">set of checks</a> against which the cloud accounts are evaluated. These checks are categorized under the out-of-the-box policies in Assess Accelerator. You can create an assessment template for each tool and add all or some of the supported checks in the template. Based on your requirements, you can create multiple assessment templates with different sets of checks.<br>

Assess Accelerator enables you to create an assessment job for one or more providers (or accounts) by selecting the appropriate assessment template and policies. The assessment report that Assess Accelerator generates for each provider, enables you to take action and fix any security and compliance issues in your environment. You can also generate a report that compares the assessment results across multiple jobs or providers.<br>

For more information, see <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-assess', viewPage: 'run-assessment-policies', viewSection: 'Content'})" style="text-decoration:none">Run assessment policies</a> and <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-assess', viewPage: 'assess-templates', viewSection: 'Content'})" style="text-decoration:none">Create and manage assessment templates</a>.<br>

The following image shows the Home page of Assess Accelerator:

![](/images/rean-assess/assess_home.PNG)


