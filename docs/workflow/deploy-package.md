---
title: Deploy solution packages
---

# Deploy solution packages 

Hitachi Cloud Accelerator Platform - Workflow Accelerator allows you to create and maintain a catalog of solution packages and easily deploy these solution packages across various cloud providers. This topic describes how to deploy the solution packages that you have registered. It also describes how to redeploy or destroy registered solution packages that you have already deployed.

## <a id="Content" name="Content"></a>Contents
* <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-workflow', viewPage: 'deploy-solution-packages', viewSection: 'prereqs'})" style="text-decoration:none">Prerequisites</a>
* <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-workflow', viewPage: 'deploy-solution-packages', viewSection: 'deploy-obj'})" style="text-decoration:none">Understanding the Solution Package Deployment Input Object structure</a>
* <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-workflow', viewPage: 'deploy-solution-packages', viewSection: 'deploy-sp'})" style="text-decoration:none">Deploying a solution package</a>
* <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-workflow', viewPage: 'deploy-solution-packages', viewSection: 'deploystatus-sp'})" style="text-decoration:none">Viewing the deployment status of a solution package</a>
* <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-workflow', viewPage: 'deploy-solution-packages', viewSection: 'redploy-sp'})" style="text-decoration:none">Redeploying an existing deployment</a>
* <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-workflow', viewPage: 'deploy-solution-packages', viewSection: 'destroy-sp'})" style="text-decoration:none">Destroying a deployment</a> 
* <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-workflow', viewPage: 'deploy-solution-packages', viewSection: 'logs'})" style="text-decoration:none">Viewing deployment logs</a>
* <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-workflow', viewPage: 'deploy-solution-packages', viewSection: 'actions-sp'})" style="text-decoration:none">Performing additional actions on deployments</a>

## <a id="prereqs" name="prereqs"></a>Prerequisites

Before deploying a solution package, you must perform the following actions:

1. Ensure that you have completed all <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-workflow', viewPage: 'prerequisites', viewSection: 'prereq'})" style="text-decoration:none">prerequisites for Workflow Accelerator</a>.

2. Ensure that you have <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-workflow', viewPage: 'create-and-register-solution-packages', viewSection: 'reg'})" style="text-decoration:none">registered your solution package</a>.

   Note the ID of the registered solution package. You will require this ID to deploy the solution package.

3. Get IDs of the Deploy Accelerator providers that you have used in your solution package. The provider IDs are available on the List Providers page in Deploy Accelerator. 

4. Prepare the Solution Package Deployment Input Object. For more information, see <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-workflow', viewPage: 'deploy-solution-packages', viewSection: 'deploy-obj'})" style="text-decoration:none">Understanding the Solution Package Deployment Input Object structure</a>.

## <a id="deploy-obj" name="deploy-obj"></a>Understanding the Solution Package Deployment Input Object structure

The Solution Package Deployment Input Object structure includes the following data objects:

- <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-workflow', viewPage: 'deploy-solution-packages', viewSection: 'sp-id'})" style="text-decoration:none">solutionPackageID</a>
- <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-workflow', viewPage: 'deploy-solution-packages', viewSection: 'name'})" style="text-decoration:none">name</a>
- <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-workflow', viewPage: 'deploy-solution-packages', viewSection: 'desc'})" style="text-decoration:none">description</a>
- <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-workflow', viewPage: 'deploy-solution-packages', viewSection: 'input'})" style="text-decoration:none">inputParameters</a>
- <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-workflow', viewPage: 'deploy-solution-packages', viewSection: 'prov'})" style="text-decoration:none">providers</a>
- <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-workflow', viewPage: 'deploy-solution-packages', viewSection: 'tags'})" style="text-decoration:none">tags</a>

Based on your requirements, you must create the deployment input object for each solution package that you want to deploy.<br>

The following is an example of the Solution Package Deployment Input Object.

```json
{
    "solutionPackageId": "AW3URleQQYIgadxCC8hgJ",
    "name" : "Staging_Env_Deploy", 
    "description" : "solution package developer demo",
    "inputParameters" : {
        "name": "demo",
        "env" : "sample-demo",
        "customer": "hitachi",
        "instance_type": "t2.small",
        "cidr": "10.10.10.20/32",
        "whitelisted_ip":["71.124.103.45/32", "76.212.44.133/16", "210.19.95.45/32"],
        "tagsTest": {
            "project":"Platform",
            "buildUrl": "true",
            "environment": "QA",
            "product": "Platform"
        }
    },
    "providers" : {
        "aws-provider" : 5
    },
    "tags": {
        "Environment": "Sample"
    }
}
```

### <a id="sp-id" name="sp-id"></a>solutionPackageID

ID of the registered solution package. This ID is generated after registering the Solution Package.  This is a mandatory parameter.

### <a id="name" name="name"></a>name

The name of the solution package deployment. The name has to be unique per solution package. This is a mandatory parameter.

### <a id="desc" name="desc"></a>description

Description of the solution package deployment.

### <a id="input" name="input"></a>inputParameters

Contains input parameters with its respective values required for the deployment. The name of the input parameter must be same as defined in the **inputParameters** object in the solution package JSON.<br>

The parameter in the object is defined in the following format:

```json
"inputParameters" : {
    "Name" : "Value"
}
```

Here, **Name** is the name of the parameter and **Value** is the value of the parameter. Consider the following points while defining the value of the parameter.

- If a parameter has predefined values, you must enter a value from the **possibleValues** defined in the **inputParameters** object in the Solution Package. 
- If a parameter has a default value set in the Solution Package and it is not defined in deployment, the default value will be used.
- If a parameter does not have any value defined in the Solution Package, it is mandatory to define a value for the parameter during deployment. 

### <a id="prov" name="prov"></a>providers

List of providers to be used for deployment. The parameter in the object is defined in the following format:

```json
"providers" : {
    "Provider_name": <providerID>
}
```

**Example**

```json
"providers" : {
    "aws-provider": 3
}
```

The name of the provider must be same as defined in the **providers** section in the solution package JSON. The **Provider_name** parameter is the name of the provider in the Solution Package. Make sure that the **Provider_name** is same as defined in the Solution Package.<br>

The **providerID** value is the registered ID of the provider in Deploy Accelerator. Make sure that all the providerIDs defined in the Solution Package is entered in this object. For more information on registering providers in Deploy Accelerator using API, see [Deploy Accelerator API documentation](https://rean-platform.reancloud.com/api-documentation/reandeploydoc/api-docs/index.html#/Provider/getProviderByName). 

You can override the default provider value at the time of Solution Package deployment by declaring a provider name and its provider ID.

### <a id="tags" name="tags"></a>tags

Additional tags for the solution. The tags must be in the following format:

```json
{
    "tagname1": "tag1 value",
    "tagname2": "tag2 value"
}
```

These tags can be used for creating a tag and searching a solution deployment with the tag name for a specific tag value. For example, you can create a tag called **Environment** that can have three values -- **Testing**, **Staging**, and **Production**. This will allow you to use the **Environment** parameter to search for a solution deployment that is in **Production**. 

**Example**

```json
{
    "Environment": "Testing"
}
```

## <a id="deploy-sp" name="deploy-sp"></a>Deploying a solution package

To deploy a solution package, use the following cURL command. For information about the cURL command syntax and options, see <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-workflow', viewPage: 'api', viewSection: 'curl'})" style="text-decoration:none">Using cURL to make API requests</a>.  

```
curl -X POST $HCAP_URL/api/hcapworkflowengine/solution-deploy \
 -H 'authorization: $USERNAME:$PASSWORD' \
 -H 'content-type: application/json' \
 -d '{
        "solutionPackageId": "SolutionPackageID",
        "name": "DeploymentName",
        "description": "Deployment description",
        "inputParameters": {
            "ParameterName": "value",
            "ParameterName": "Value"
        },
        "providers":{
            "ProviderName": ProviderID,
            "ProviderName": ProviderID
        }
	}'
```

**Body JSON Example**

```json
{
    "solutionPackageId": "AXcdSDadssaUqCsd",
    "name": "DemoDeployment",
    "description": "Deployment description",
    "inputParameters": {"vpc_cidr": "10.0.0.0/16", "zone": "us-east-1"},
    "providers":{
        "DemoProvider": 8
    }
}
```

In the **response** section, confirm that the status of the solution package is **DEPLOY_INITIATED**. This status indicates that Workflow Accelerator has initiated the deployment of the workflow layers in the order in which they are listed in the solution package. For more information, see <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-workflow', viewPage: 'deploy-solution-packages', viewSection: 'deploystatus-sp'})" style="text-decoration:none">Viewing the deployment status of a solution package</a>.<br>

_**Note:** Make a note of the deployment ID as you will need it to view the deployment status of the solution package. You will also need this ID if you want to redeploy or destroy the deployed solution package._

## <a id="redeploy-sp" name="redeploy-sp"></a>Redeploying an existing deployment

To redeploy a solution package, use the following cURL command. For information about the cURL command syntax and options, see <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-workflow', viewPage: 'api', viewSection: 'curl'})" style="text-decoration:none">Using cURL to make API requests</a>. 

```
curl -X PUT $HCAP_URL/api/hcapworkflowengine/solution-deploy/redeploy \
 -H 'authorization: $USERNAME:$PASSWORD' \
 -H 'content-type: application/json' \
 -d '{
 	"solutionPackageId": "SolutionPackageID",
	"name": "DeploymentName",
	"description": "Deployment description",
	"inputParameters": {"ParameterName": "value", "ParameterName": "Value"},
	"providers":{
		"ProviderName": ProviderID,
		"ProviderName": ProviderID
	}
 }'
```

Workflow Accelerator once again deploys the workflow layers in the order that is specified in the solution package.

## <a id="destroy-sp" name="destroy-sp"></a>Destroying a deployment

To destroy a solution package, use the following cURL command. For information about the cURL command syntax and options, see <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-workflow', viewPage: 'api', viewSection: 'curl'})" style="text-decoration:none">Using cURL to make API requests</a>. 

```
curl -X DELETE $HCAP_URL/api/hcapworkflowengine/solution-deploy/<SOLUTION_PACKAGE_DEPLOYMENT_ID> \
 -H 'authorization: $USERNAME:$PASSWORD' \
 -H 'content-type: application/json'
```

The order in which Workflow Accelerator destroys workflow layers in the solution package is the reverse of the deployment order. For example, the workflow layer that was deployed last is destroyed first.

## <a id="deploystatus-sp" name="deploystatus-sp"></a>Viewing the deployment status of a solution package

To view the deployment status of a solution package, use the following cURL command. For information about the cURL command syntax and options, see <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-workflow', viewPage: 'api', viewSection: 'curl'})" style="text-decoration:none">Using cURL to make API requests</a>. 

```
curl -X GET $HCAP_URL/api/hcapworkflowengine/solution-deploy/<SOLUTION_PACKAGE_DEPLOYMENT_ID> \
 -H 'authorization: $USERNAME:$PASSWORD' \
 -H 'content-type: application/json'
```

In the **response** section, check the **status** attribute to view the deployment status of the solution package. The following table lists the status that is shown based on different scenarios. 

| Scenario                                                     | Status            |
| ------------------------------------------------------------ | ----------------- |
| Deployment of a solution package has been initiated.         | DEPLOY_INITIATED  |
| Deployment of a solution package is in progress.             | DEPLOYING         |
| The solution package has been successfully deployed.<br><br>_**Note:** Make a note of the deployment ID as you will need it later if you want to redeploy or destroy this deployment of the solution package._ | DEPLOYED          |
| Deployment of any workflow layer in a solution package fails. | FAILED            |
| Redeployment of an existing deployment of a solution package is in progress. | DEPLOYING         |
| The Destroy action for an existing deployment of a solution package has been initiated | DESTROY_INITIATED |
| An existing deployment of a solution package is being destroyed. | DESTROYING        |
| An existing deployment of a solution package is successfully destroyed. | DESTROYED         |

_**Note:** To view the deployment status for a specific workflow layer in the solution package, check the **workflowStatus** attribute in the **response** section._

## <a id="logs" name="logs"></a>Viewing deployment logs

In the **response** section, check the **recentError** attribute to view any error messages related to the deployment of the solution package. You can also check the **oldError** attribute for viewing previous error messages.<br>

To view more detailed deployment logs of a failed environment in a solution package, you can <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-platform-common', viewPage: 'createAndAccessAccount', viewSection: 'logon'})" style="text-decoration:none">sign in to Cloud Accelerator Platform</a> and open the Deploy Accelerator environment whose deployment has failed. Ensure that the failed deployment is selected in the deployment list on the canvas and click the **Logs** icon. After you have fixed the issues with the environment, you can <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-workflow', viewPage: 'deploy-solution-packages', viewSection: 'redploy-sp'})" style="text-decoration:none">redeploy the existing deployment of the solution package</a>.

## <a id="actions-sp" name="actions-sp"></a>Performing additional actions on deployments

The Workflow Engine REST APIs also allow you to perform a few additional actions on the deployments of solution packages. For example, you can get a list of all your deployed solution packages, get the solution package deployments by solution package ID, or get the solution package deployments by solution package ID and deployment name.<br>

For information about accessing the Workflow Engine API documentation, see <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-workflow', viewPage: 'api', viewSection: 'we-api'})" style="text-decoration:none">Workflow Accelerator API Reference</a>.