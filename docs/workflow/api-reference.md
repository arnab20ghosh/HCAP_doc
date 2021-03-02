---
title: Using Workflow Accelerator REST APIs
---

# <a id="api" name="api"></a>Workflow Accelerator API Reference

Hitachi Cloud Accelerator Platform - Workflow Accelerator provides a set of REST APIs (Application Programming Interface) for the **Solution Package** and **Workflow Engine** services. The API Reference is organized by components and provides information about the method, syntax, parameters, and response code for each API.

## Contents

- <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-workflow', viewPage: 'api', viewSection: 'sp-api'})" style="text-decoration:none">Accessing the Solution Package API documentation</a>
- <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-workflow', viewPage: 'api', viewSection: 'we-api'})" style="text-decoration:none">Accessing the Workflow Engine API documentation</a>
- <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-workflow', viewPage: 'api', viewSection: 'curl'})" style="text-decoration:none">Using cURL to make API requests</a>

## <a id="sp-api" name="sp-api"></a>Accessing the Solution Package API documentation

The Solution Package API documentation lists the APIs that you can use to register, update, and delete solution packages. It also includes APIs to get a list of registered solution packages or search for a solution package based on specific criteria such as name, version, and ID.<br>

To view the Solution Package API documentation for the version of Workflow Accelerator that you have deployed, go to **https://*YOUR_PLATFORM_BASE_URL*/api-documentation/solutionpackagedoc/swagger-ui.html**.<br>

To view the Solution Package API documentation for the latest version of Workflow Accelerator, see the [Workflow Accelerator API Reference website](https://rean-platform.reancloud.com/api-documentation/solutionpackagedoc/swagger-ui.html).<br>

_**Note:** The API documentation describes APIs for all supported schema versions of the solution package. Use the APIs for the schema version that you have used to create your solution package._<br>

The following image shows the Solution Package APIs for schema version 2.*x*.

![](/images/rean-workflow/sp-api.PNG)

## <a id="we-api" name="we-api"></a>Accessing the Workflow Engine API documentation

The Workflow Engine API documentation lists the APIs that you can use to deploy, redeploy, and destroy solution packages. It also includes APIs to get the deployment status of a solution package and get a list of deployed solution packages.<br>

To view the Workflow Engine API documentation for the version of Workflow Accelerator that you have deployed, go to **https://*YOUR_PLATFORM_BASE_URL*/api-documentation/workflowenginedoc/swagger-ui.html**.<br>

To view the Workflow Engine API documentation for the latest version of Workflow Accelerator, see the [Workflow Accelerator API Reference website](https://rean-platform.reancloud.com/api-documentation/workflowenginedoc/swagger-ui.html).<br>

![](/images/rean-workflow/we-api.PNG)

## <a id="curl" name="curl"></a>Using cURL to make API requests

The Workflow Accelerator solution packages can be deployed in many different ways. For example, you can build a UI to trigger the solution package deployment and internally call Workflow Accelerator REST APIs.
Alternatively, you can use cURL commands or a REST API client (such as Postman) to directly run the API commands. This documentation provides examples of cURL commands for making API requests to Workflow Accelerator.<br>

For information about using these APIs to perform different actions in Workflow Accelerator, see <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-workflow', viewPage: 'create-and-register-solution-packages', viewSection: 'Content'})" style="text-decoration:none">Create and register solution package</a> and <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-workflow', viewPage: 'deploy-solution-packages', viewSection: 'Content'})" style="text-decoration:none">Deploy solution packages</a>.

### Set environment variables

Before you run the API commands, set the following environment variables for Hitachi Cloud Accelerator Platform:

- HCAP_URL
- USERNAME
- PASSWORD

_**Important:** Ensure that the user account whose authentication details you specify, is a member of the <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-workflow', viewPage: 'prerequisites', viewSection: 'hcap-instance'})" style="text-decoration:none">required groups</a>. Also, if your solution packages use pre-created providers in Deploy Accelerator, ensure that the user account can access the providers._

**Example**

```
export USERNAME=admin
export PASSWORD=admin123
export HCAP_URL= https://hcap.hitachivantara.com
```

### cURL command syntax and options

You can use the following cURL command syntax to make API requests to Workflow Accelerator.

```
curl -X <Method> <URL> \
 -H 'authorization: $USERNAME:$PASSWORD' \
 -H 'content-type: application/json' \
 -d '{
      <Body>  
 }' 
```

The cURL command includes the following sections:

- **Method**: This section contains the method used to call the API and the URL of the API.

  ```
  -X POST URL \
  ```

- **Header**: The values to be passed in the header of the command. The value for the **authorization** key must be your Cloud Accelerator Platform username and password, separated by a colon (:). The value for the **content-type** key must be **application/json**.

  ```
  -H 'authorization: $USERNAME:$PASSWORD' \
  -H 'content-type: application/json' \
  ```

- **Body**: The parameters to be passed in the body section of the URL. These values can be taken from the values defined in the solution package.

  ```
  -d '{
  	<data to be sent>
  }'
  ```

**Example**

```
curl -X PUT $HCAP_URL/api/hcapworkflowengine/solution-deploy/redeploy \
 -H 'authorization: $USERNAME:$PASSWORD' \
 -H 'content-type: application/json' \
 -d '{
 	solutionPackageId": "AXcdSDadssaUqCsd",
    "name": "DemoDeployment",
    "description": "This is a demo deployment",
    "inputParameters": {"vpc_cidr": "10.0.0.0/16", "zone": "us-east-1"},
    "providers":{
    	"DemoProvider": 8
    }
 }'
```

