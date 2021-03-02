---
title: Create and register solution packages
---

# <a id="reg" name="reg"></a>Create and register solution packages 

Hitachi Cloud Accelerator Platform - Workflow Accelerator allows you to create and maintain a catalog of solution packages and easily deploy these solution packages. This topic describes how to create and register solution packages.

## <a id="Content" name="Content"></a>Contents
* <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-workflow', viewPage: 'create-and-register-solution-packages', viewSection: 'prereqs'})" style="text-decoration:none">Prerequisites</a>
* <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-workflow', viewPage: 'create-and-register-solution-packages', viewSection: 'create-sp'})" style="text-decoration:none">Creating a solution package</a>
* <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-workflow', viewPage: 'create-and-register-solution-packages', viewSection: 'register-sp'})" style="text-decoration:none">Registering a solution package</a>
* <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-workflow', viewPage: 'create-and-register-solution-packages', viewSection: 'add-actions-sp'})" style="text-decoration:none">Performing additional actions on a solution package</a>

## <a id="prereqs" name="prereqs"></a>Prerequisites

Before creating a solution package, you must perform the following actions:

1. Ensure that you have completed all <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-workflow', viewPage: 'prerequisites', viewSection: 'content'})" style="text-decoration:none">prerequisites for Workflow Accelerator</a>.

2. Plan the end-to-end solution for which you want to create the solution package. 

   For example, identify the cloud service providers for the solution, determine the number of required workflow layers, and outline the dependency between the layers.

3. For each workflow layer in the solution package, ensure that you have the details that need to be specified for the action. For more information, see <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-workflow', viewPage: 'understand-solution-package-schema', viewSection: 'actions'})" style="text-decoration:none">Workflow actions</a>.

4. Make a note of the user inputs required to deploy each workflow layer in the solution package.

5. Create the required providers in Deploy Accelerator and make a note of the provider details. For more information, see <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-deploy', viewPage: 'deploy-and-manage-environments', viewSection: 'provider'})" style="text-decoration:none">Configuring providers</a>.

   For example, to deploy infrastructure in AWS, create an AWS provider. Similarly, to deploy a Helm chart in a Kubernetes cluster, create a Helm provider.

   _**Note:** Workflow Accelerator supports all providers and authentication methods that are available in Deploy Accelerator._

## <a id="create-sp" name="create-sp"></a>Creating a solution package

1. Ensure that you have completed all the <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-deploy', viewPage: 'deploy-and-manage-environments', viewSection: 'prereqs'})" style="text-decoration:none">prerequisites</a> for creating a solution package.

2. Open a text editor and create a new file.

3. Save the file in the JSON format (**.json**).

4. In the JSON file, enter the schema structure of the solution package, as shown in the example below.

   ```json
   {
       "schemaVersion":"X.X",
       "scheduler":{},
       "metadata":{},
       "input":{},
       "blueprints":[],
       "providers":[],
       "outputs":{},
       "workflow":[]
   }
   ```

5. Enter the appropriate data within each data object of the schema structure.

   For information about the data objects, see the latest <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-workflow', viewPage: 'understand-solution-package-schema', viewSection: 'sp-schema'})" style="text-decoration:none">solution package schema</a>.

6. Save your updates to the file.

After you have created your solution package, you must <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-deploy', viewPage: 'deploy-and-manage-environments', viewSection: 'register-sp'})" style="text-decoration:none">register the solution package</a>. You can deploy only registered solution packages.

## <a id="register-sp" name="register-sp"></a>Registering a solution package

To register a solution package, use the following cURL command. For information about the cURL command syntax and options, see <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-workflow', viewPage: 'api', viewSection: 'curl'})" style="text-decoration:none">Using cURL to make API requests</a>. 

```
curl -X POST ${HCAP_URL}/api/solution_package/v2 \
 -H 'authorization: $USERNAME:$PASSWORD' \
 -H 'content-type: application/json' \
 -d '{
 	<Solution Package JSON>
 }'
```

**Body JSON Example**

```json
{
  "schemaVersion": "2.1",
  "metadata": {
    "name": "demo",
    "version": "00.00.01",
    "description": "demo",
    "icon": "https://google.com",
    "applicationVersion": "01.00.00",
    "language": [
      "english",
      "japanese"
    ],
    "ownerName": "demo-user",
    "ownerEmail": "demo.user@companyname.com",
    "cloudRegion": [
      "us-east-1",
      "us-west-1"
    ],
    "vertical": [],
    "tags": {
      "tag1": "value1",
      "tag2": "value2",
      "app" : "SampleApp"
    }
  },
  "input": {
    "inputParameters": [
      {
        "name": "cidr",
        "type": "String",
        "description": "AMI ID",
        "defaultValue": "10.0.0.0/16"
      },
      {
        "name": "isApp",
        "type": "String",
        "description": "AMI ID",
        "defaultValue": "true"
      },
      {
        "name": "isVpc",
        "type": "String",
        "description": "AMI ID",
        "defaultValue": "true"
      },
      {
        "name": "instance_type",
        "type": "String",
        "default": "t2.micro",
        "description": "instance type"
      },
      {
        "name": "customer_name",
        "type": "String",
        "description": "instance name"
      },
      {
        "name": "env",
        "type": "String",
        "description": "Environment like prod, qa, etc"
      },
      {
        "name": "list-value",
        "type": "List",
        "defaultValue": "'demo-one','demo-two'"
      },
      {
        "name": "json-value",
        "type": "Json"
      }
    ],
    "inputMapping": {
      "vpc": {
        "provider": "dns",
        "deployInput": [
          {
            "key": "vpc_cidr",
            "value": "${#input.cidr}"
          },
          {
            "key": "customer_name",
            "value": "${#input['customer_name']}"
          },
          {
            "key": "env",
            "value": "${#input['env']}"
          },
          {
            "key": "pqr",
            "value": "${#input['list-value']}",
            "type": "List"
          },
          {
            "key": "p",
            "value": "${#input['json-value']}",
            "type": "Map"
          }
        ]
      },
      "app": {
        "deployInput": [
          {
            "key": "instance_type",
            "value": "${#input['instance_type']}"
          },
          {
            "key": "customer_name",
            "value": "${#output['vpc']['customer']}"
          },
          {
            "key": "env1",
            "value": "{ '${#input['customer_name']}' : '${#input['customer_name']}' }",
            "type": "Map"
          },
          {
            "key": "vpc_id",
            "value": "${#output['vpc']['vpc_id']}"
          }
        ],
        "provider": "dns"
      }
    }
  },
  "blueprints": [
  ],
  "providers": [
    {
      "name": "dns",
      "type": "dns"
    }
  ],
  "outputs": [
    {
      "name": "output1",
      "value": "${#input.cidr}",
      "description": "Output sample example with default type and directly from inputs of SP"
    },
    {
      "name": "output2",
      "value": "${#output['vpc']['customer']}",
      "description": "Output sample example from output of layer",
      "type": "String"
    },
    {
      "name": "output3",
      "value": "${#output['app']['app_url']}",
      "description": "Output sample example from layer 2",
      "type": "String"
    },
    {
      "name": "output4",
      "value": "${#output['vpc']['prq-value']}",
      "description": "Output sample example with list type",
      "type": "List"
    },
    {
      "name": "output5",
      "value": "${#output['vpc']['json-value']}",
      "description": "Output sample example with map type",
      "type": "Map"
    }
  ],
  "workflow": [
    { 
      "action" : "deployEnv", 
      "name" : "vpc", 
      "condition" : "${#input.isVpc}",
      "data" : { 
        "envName" : "vpc-demo", 
        "envVersion" : "01.00.00" 
      } 
    },
    { 
      "action" : "deployEnv", 
      "name" : "app", 
      "condition" : "${#input.isApp}",
      "data" : { 
        "envName" : "app_demo", 
        "envVersion" : "01.00.00" 
      }
    }
  ]
}
```

## <a id="add-actions-sp" name="add-actions-sp"></a>Performing additional actions on solution package

The Solution Package REST APIs also allow you to perform a few additional actions on solution packages. For example, you can get a list of all your solution packages, search for a solution package, update a solution package, and delete a solution package.<br>

For information about accessing the Solution Package API documentation, see <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-workflow', viewPage: 'api', viewSection: 'sp-api'})" style="text-decoration:none">Workflow Accelerator API Reference</a>.