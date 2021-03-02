---
title: Overview of Workflow Accelerator
---

# <a id="overview" name="overview"></a>Overview of Workflow Accelerator

Hitachi Cloud Accelerator Platform - Workflow Accelerator allows you to create and maintain a catalog of solution packages and easily deploy these solution packages. It is an orchestration tool that can stitch together multiple workflow layers to deliver an end-to-end solution. You can use Workflow Accelerator to develop your solutions once and then deploy them multiple times by passing the appropriate set of inputs.<br>

Before you start creating solution packages, you must understand the following building blocks of Workflow Accelerator:

- <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-workflow', viewPage: 'overview', viewSection: 'sp'})" style="text-decoration:none">Solution package</a>
- <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-workflow', viewPage: 'overview', viewSection: 'workflow-actions'})" style="text-decoration:none">Workflow actions</a>
- <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-workflow', viewPage: 'overview', viewSection: 'dep-tools'})" style="text-decoration:none">Deployment tools</a>
- <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-workflow', viewPage: 'overview', viewSection: 'auth'})" style="text-decoration:none">Authentication mechanisms</a>

As the next step, you can view the <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-workflow', viewPage: 'prerequisites', viewSection: 'content'})" style="text-decoration:none">prerequisites</a> for using Workflow Accelerator and <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-workflow', viewPage: 'understand-solution-package-schema', viewSection: 'sp-schema'})" style="text-decoration:none">understand the solution package schema</a> before you <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-workflow', viewPage: 'create-and-register-solution-packages', viewSection: 'Content'})" style="text-decoration:none">create and register</a> and <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-workflow', viewPage: 'deploy-solution-packages', viewSection: 'Content'})" style="text-decoration:none">deploy</a> solution packages. 

## <a id="sp" name="sp"></a>Solution package

Basically, a solution package in Workflow Accelerator is a JSON file that contains information required for installing an end-to-end solution across various cloud platforms. It uses a <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-workflow', viewPage: 'understand-solution-package-schema', viewSection: 'sp-schema'})" style="text-decoration:none">predefined schema</a> to define the different workflow layers of a solution, the deployment sequence of these layers, input and output parameters, deployment parameters, authentication details for deploying each layer, and other required information.

For example, a solution package for an application can contain layers for networking infrastructure, a Kubernetes cluster, and the application itself. It can define that the networking infrastructure layer must be deployed first, followed by the Kubernetes cluster layer, and then finally the application layer. It can also use the output of the networking layer to deploy the Kubernetes cluster, and the output of the Kubernetes cluster layer to deploy the application layer. 

To <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-workflow', viewPage: 'create-and-register-solution-packages', viewSection: 'register-sp'})" style="text-decoration:none">register</a> and <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-workflow', viewPage: 'deploy-solution-packages', viewSection: 'deploy-sp'})" style="text-decoration:none">deploy</a> the solution packages that you have created, you have to use <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-workflow', viewPage: 'api', viewSection: 'api'})" style="text-decoration:none">REST APIs</a>. Workflow Accelerator currently does not have a user interface.

## <a id="workflow-actions" name="workflow-actions"></a>Workflow actions

Each workflow layer in a solution package specifies the type of action to be performed. Currently, Workflow Accelerator supports the following actions:

- Create providers in Deploy Accelerator
- Deploy environments through Deploy Accelerator
- Register Foundry solution packages
- Deploy Foundry solution packages
- Register Helm repositories with the Helm service in Workflow Accelerator
- Deploy Helm charts to a Kubernetes cluster from a Helm repository
- Deploy other solution packages


## <a id="dep-tools" name="dep-tools"></a>Deployment tools

The Workflow Accelerator uses the appropriate deployment tool based on the type of action to be performed by a workflow layer. For the latest supported workflow actions, it uses the deployment tools listed in the following table.

| Deployment tool                   | Description                                                  |
| --------------------------------- | ------------------------------------------------------------ |
| Deploy Accelerator                | Deployment automation tool that enables you to deploy environments, which are a collection of resources that you need to deploy application stacks across various cloud platforms. |
| Workflow Accelerator Helm service | Inbuilt service available with the Workflow Accelerator that enables you to register Helm repositories and deploy Helm charts. |
| Hitachi Foundry                   | Framework for the rapid development, curation, and management of service-oriented software solutions. Enables you to deploy Foundry solution packages. |

## <a id="auth" name="auth"></a>Authentication mechanism

Workflow Accelerator leverages providers in Deploy Accelerator to access the authentication details that are required to deploy environments. For example, Workflow Accelerator references the appropriate AWS provider in Deploy Accelerator to get authentication details for accessing the AWS account in which infrastructure needs to be deployed.<br>

To deploy Helm charts and Foundry solution packages, the authentication details for Helm repository and OCI Harbor repository have to be provided while deploying solution packages.