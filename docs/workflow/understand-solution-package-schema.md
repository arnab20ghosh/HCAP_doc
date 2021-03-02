---
title: Understand the solution package schema
---

# <a id="sp-schema" name="sp-schema"></a>Understand the solution package schema

Solution package in Workflow Accelerator is a JSON file that allows you to define all the information that is required for installing end-to-end solutions across various cloud platforms. To register and deploy the solution packages that you create, you have to use REST APIs.<br>

This page describes the most recent major version (for example: 2.x) of the solution package schema. To view the schema for older versions, see <a href="downloads/rean-workflow/solution-package-schema-v1.html" target="_blank">Solution Package schema 1.0</a>.

## Contents

- <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-workflow', viewPage: 'understand-solution-package-schema', viewSection: 'sample'})" style="text-decoration:none">Sample solution package</a>
- <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-workflow', viewPage: 'understand-solution-package-schema', viewSection: 'data-object'})" style="text-decoration:none">Data objects in solution package schema</a>
- <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-workflow', viewPage: 'understand-solution-package-schema', viewSection: 'actions'})" style="text-decoration:none">Supported workflow actions</a>

## <a id="sample" name="sample"></a>Sample solution package

The following is an example of a solution package for installing an application. For information about the different JSON blocks in the solution package, see <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-workflow', viewPage: 'understand-solution-package-schema', viewSection: 'data-object'})" style="text-decoration:none">Data objects in solution package schema</a>.

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
        "provider": "aws_provider",
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
      {
        "name": "Demo-BP",
		"version": "0.1.1"
	}
  ],
 "providers": [
   	 {
        "name": "aws_provider",
        "type": "aws"
    },
    {
        "name": "artifactory_repo",
        "type": "artifactory",
        "default_provider_name": "default_artifactory"
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

## <a id="data-object" name="data-object"></a>Data objects in solution package schema

 The solution package schema contains multiple JSON blocks for the following data objects:

- <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-workflow', viewPage: 'understand-solution-package-schema', viewSection: 'schemaversion'})" style="text-decoration:none">schemaVersion</a>
- <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-workflow', viewPage: 'understand-solution-package-schema', viewSection: 'metadata'})" style="text-decoration:none">metadata</a>
- <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-workflow', viewPage: 'understand-solution-package-schema', viewSection: 'sp-schema'})" style="text-decoration:none">schedule</a>
- <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-workflow', viewPage: 'understand-solution-package-schema', viewSection: 'blueprints'})" style="text-decoration:none">blueprints</a>
- <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-workflow', viewPage: 'understand-solution-package-schema', viewSection: 'workflow'})" style="text-decoration:none">workflow</a>
- <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-workflow', viewPage: 'understand-solution-package-schema', viewSection: 'sp-schema'})" style="text-decoration:none">customData</a>
- <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-workflow', viewPage: 'understand-solution-package-schema', viewSection: 'providers'})" style="text-decoration:none">providers</a>
- <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-workflow', viewPage: 'understand-solution-package-schema', viewSection: 'input'})" style="text-decoration:none">input</a>
- <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-workflow', viewPage: 'understand-solution-package-schema', viewSection: 'output'})" style="text-decoration:none">output</a>

### <a id="schemaversion" name="schemaversion"></a>schemaVersion

The version of the solution package schema. You can search a solution package using the **schemaVersion** attribute. This is a mandatory parameter.

It is recommended that you use the latest schema version to create a new solution package. For example, the entry for this parameter can be **2.0**. However, older schema versions continue to be supported. If you are updating an existing solution package, specify the schema version that was used to create that solution package.

***Note*:** *All solution packages created with schema version 2.x must be registered or edited using the REST API version v2, as shown below:*
***https://{HCAP-base-URL}/api/reansolutionpackage/solution_package/v2***

### <a id="metadata" name="metadata"></a>metadata

This data object contains the metadata about the solution package and the application to be installed using the solution package. The information in the metadata section is used to display, access, and search the solution package by using parameters such as name, version, language, and cloud region.

The object must be in the following format:

```json
"metadata": {
    "name": "magento",
	"version": "00.00.01",
	"description": "This solution package is for installing Magento commerce application.",
	"icon": "http://https://magento.com/log.png",
	"applicationVersion": "01.00.00",
	"ownerName": "MFI",
	"ownerEmail": "customer.mfi@hitachivantara.com",
	"duration": {
        "minDeploymentTime": "1d 1h 20m",
		"maxDeploymentTime": "1d 2h 30m"
	},
	"language": [
        "en_US"
	],
	"licenseName": "license-321",
	"cloudRegion": [
        "us-east-1"
	],
	"vertical": [],
	"tags": {
        "domain": "commerce",
		"has_free_trials": false
	}
}
```

Following are the attributes of the **metadata** object:

- name (mandatory parameter)
- version (mandatory parameter)
- description
- icon
- applicationVersion
- ownerName
- ownerEmail
- duration
- language
- licenseName
- cloudRegion (mandatory parameter)
- vertical
- tags

#### name (mandatory parameter)

The name of the solution package. The solution name and version must be unique per user 

#### version (mandatory parameter)

The version of the solution package. You can create multiple versions for a single solution name. 

#### description

Description of the solution. You can add a detailed information about the application in this parameter.

#### icon

URL to the location of the Application icon image.

#### applicationVersion

The version of the application which is getting deployed as a part of this solution package 

#### ownerName

The name of the owner of the solution package. This is a mandatory parameter.

#### ownerEmail

The email ID of the owner of the solution package. This is a mandatory parameter.

#### duration

A user entry to define the minimum and maximum deployment time required by the solution package. The object must be in the following format:

```json
"duration": {
	"minDeploymentTime": "1d 1h 20m",
	"maxDeploymentTime": "1d 2h 30m"
}
```

The correct format for entry of time 1d 3h 20m for 1 day, 3 hours and 20 minutes. This format does not support time entry in seconds. 

#### language

List of languages supported by the application to be deployed using solution package.  The list must be the language code in ISO standard. For example:

```json
"language": [
    "en_US"
]
```

For more information on the language codes, in the ISO website, see [Codes for the Representation of Names of Languages]( http://www.loc.gov/standards/iso639-2/php/code_list.php ).

#### licenseName

The license required for using the solution package. Before entering the license name here, make sure that the license is created for the solution package. For more information on the creation of the license key, see the license-controller API documentation in Solution Package. 

The license-control API documentation is available at following URL: 
**https://{HCAP-base-URL}/api-documentation/solutionpackagedoc/swagger-ui.html#/license-controller**

#### cloudRegion (mandatory parameter)

List of cloud regions where the solution package is to be deployed. For example:

```json
"cloudRegion": [
	"us-east-1"
]
```

#### vertical

Vertical of the organization to which the application belongs.

#### tags

Additional properties for the solution. The tags must be in the following format:

```json
"tags":{
    "tagname1": "tag1 value",
    "tagname2": "tag value"
}
```

These tags can be used for creating a tag and searching a solution with the tag name for a specific tag value. For example,  you can tag a solution package as { "domain" : "commerce" }, which can be used for searching all the applications in the Finance domain. 

```json
"tags": {
    "domain": "commerce",
    "has_free_trials": false
}
```

### <a id="schedule" name="schedule"></a>schedule

This data object allows you to set a schedule for deploying a solution package multiple times. When a solution package with a **schedule** parameter is deployed successfully, the subsequent deployments are scheduled and triggered based on the specified schedule.<br>

The **schedule** object is optional.

The object must be in the following format:

```
schedule": {        
"cron": "0 */2 * ? * *"    
}
```

Consider the following points about the deployment of solution packages with the schedule parameter:

- If a solution deployment is destroyed, the scheduling is stopped.
- If a solution deployment is in a running state, the scheduled deployment is skipped.
- The next scheduled deployment starts even if the previous deployment job fails.
- The scheduling of next deployment is automatically triggered after the Workflow Accelerator services are up from a downtime. For example, if a job is schedules at 10:00, 12:00, and 14:00, and the Workflow Accelerator services face a downtime from 11:00 to 13:00, then the next deployment scheduled at 14:00 is automatically triggered.

_**Note:** If required, you can update a solution package to add, update, or remove the **schedule** object and then redeploy the solution package deployment._

### <a id="blueprints" name="blueprints"></a>blueprints

This object contains the list of blueprints that will get automatically imported from the artifactory before starting the deployment of the solution package. In the artifactory, these blueprints must be stored in the repository that is configured in Deploy Accelerator.

Environments in the blueprint are imported into Deploy Accelerator with the naming convention `<solution_package_name>_<environment_name>`.

_**Note**: Blueprints will get imported only once, the solution package will reuse the previously imported blueprints if they are already present in Deploy Accelerator. The blueprints must be present in the artifactory with the provided name and version, otherwise complete deployment of the solution package will fail._

 The object must be in the following format: 

```json
"blueprints": [
    {
        "name": "VPC",
		"version": "0.1.1"
	},
	{
		"name": "Magento",
		"version": "1.0.1"
	}
]
```

Following are the attributes of the **blueprints** object:

- name
- version

#### name

Name of the blueprint. The entry must be exactly same as the name of the blueprint in the artifactory.

#### version

Version of the blueprint for the specified name.

_**Note:** You can also choose to manually import blueprints into Deploy Accelerator. In this case, you must specify an empty section for the **blueprints** object, as shown below._

`"blueprints": []`

### <a id="workflow" name="workflow"></a>workflow

This data object contains the list of actions that will get executed. The actions are executed in the same order in which they are listed. 

The **workflow** object is defined using the following format. 

```json
"workflow": [
    {
        "action": "<WorkflowActionName>",
        "name": "sampleName",
        "condition": "${#input['Is_solution_package_deployment']}",
        "data": {
            <data attributes based on the workflow action>
        }
    },
    {
        "action": "<WorkflowActionName>",
        "name": "sampleName",
        "condition": "${#input['Is_solution_package_deployment']}",
        "data": {
            <data attributes based on the workflow action>
        }
    }  
]
```

The following example uses the **deploySolutionPackage** action.

```json
"workflow": [
   {
       "action": "deploySolutionPackage",
       "name": "sc_dependency1",
       "condition": "${#input['Is_solution_package_deployment']}",
       "data": {
           "solution_package_name": "SolutionPackage_A1",
           "solution_package_version": "00.00.100"
      }
   }
]
```

Following are the attributes of the **workflow** object:

- action
- name
- condition
- data

#### action

The action that must be executed by the workflow layer. For the list of supported workflow actions, along with the data attributes, input mapping parameters, and output for each action, see <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-workflow', viewPage: 'understand-solution-package-schema', viewSection: 'actions'})" style="text-decoration:none">Supported workflow actions</a>. 

#### name

Name of the workflow layer. All other objects in the solution package must use this layer name to reference the details that are defined in the **data** attribute. 

#### condition

Condition based on which the layer is either executed or skipped. It allows you to control whether or not an optional layer of the solution package will be executed.

This attribute is a Spring expression that can be resolved to Boolean based on the value of the condition:

- If the value is **true** or resolves to **true**, the layer will be executed.
- If the value is **false** or resolves to **false**, the layer will be skipped.

The Spring expression for the condition can use input parameters, combination of multiple conditions, or output of a previous layer.

**Example:**

```json
"condition": "${#input[‘Is_subnet_deployment’]}"

"condition": "${#output['network-layer']['vpc_cidr'] == '10.0.0.0/16'}"
```

_**Note:** The **condition** attribute is optional. If you do not use the **condition** attribute, the layer will be executed._

#### data

Details that are required to execute the defined action. The data parameters that you can declare are based on the action that has been defined for the workflow layer. For more information, see <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-workflow', viewPage: 'understand-solution-package-schema', viewSection: 'actions'})" style="text-decoration:none">Supported workflow actions</a>.

### <a id="customdata" name="customdata"></a>customData

This object allows you to define custom attributes for the solution package. These custom attributes can be used as a search parameter for the solution package. 

The object must be in the following format:

```json
"customData": {
	"name": "SAP Hana",
	"version": "2.0.0"
}
```

### <a id="providers" name="providers"></a>providers

This data object lists all providers that are required to deploy the workflow layers in the solution package. 

The object must be in the following format:

```json
"providers": [
   	 {
        "name": "aws_provider",
        "type": "aws"
    },
    {
        "name": "artifactory_repo",
        "type": "artifactory",
        "default_provider_name": "default_artifactory"
    }
]
```

Following are the attributes of the **providers** object:

- name
- type
- default_provider_name

#### name 

Name of the provider. The entry must be exactly same as the provider declared in the blueprint.

#### type

Cloud service provider. For example, AWS, Google Cloud, and Microsoft Azure.

Depending on the target cloud provider and account in the blueprint, you can define the providers list in the following ways:

- **Case 1**: All the blueprints for the solution are to be deployed on the same Cloud service Provider account.

  ```json
  "providers": [
      {
          "name": "aws_account1",
          "type": "aws"
      }
  ]
  ```

- **Case 2**: Blueprints in the solution package are to be deployed on two different accounts of the same cloud service provider.

  ```json
  "providers": [
      {
          "name": "aws_account1",
          "type": "aws"
      },
      {
          "name": "aws_account2",
          "type": "aws"
      }
  ]
  ```

- **Case 3**: Blueprints in the solution package targeting multiple cloud providers.

  ```json
  "providers": [
      {
          "name": "aws_account1",
          "type": "aws"
      },
      {
          "name": "k8s_provider",
          "type": "helm"
      }
  ]
  ```

#### default_provider_name

The default_provider_name parameter allows you to define a default provider for your solution package. The value of this parameter must be same as the name of the provider created in Deploy Accelerator. If required, you can override the default provider value at the time of deployment.

You can define multiple default providers in solution package.

This is an optional parameter. 

```json
"providers": [
    {
        "name": "artifactory_repo",
        "type": "artifactory",
        "default_provider_name": "default_artifactory"
    }
]
```

### <a id="input" name="input"></a>input

The **input** object contains 2 sub objects **inputParameters** and **inputMapping**. 

The object must be in the following format:

```json
"input": {
	"inputParameters": {
		/*Parameter definition*/
	},
	"inputMapping": {
		/*"Workflow layer name"*/
		{
		 /*Parameter Mapping*/
		}
	}
}
```

#### inputParameters

The **inputParameters** object contains the declaration of unique parameters that are required for deploying the workflow layer.  This section consists of all unique sets of inputs that the solution owner wants the user to enter while deploying the solution package. For example, instance_size, which can be used in the one of the blueprint to set the EC2 instance size.

The object must be in the following format:

```json
"inputParameters": [
    {
        "name": "vpc_cidr",
		"type": "String",
		"description": "VPC CIDR"
    },
    {
        "name": "whitelisted_ip",
		"type": "List",
		"description": "List of IP's to whitelist"
    },
	{
        "name": "tagsTest",
		"type": "Map",
		"description": "Resource tags"
    }
]
```

Following are the attributes of the **inputParameters** object:

- **name:** Name of the parameter. The name must be a single string without any space.
- **type:** The data type of the input parameter. The supported types are List, String, Boolean, Map, and Integer.
- **description:** Description of the parameter. You can add a detailed information about the application in this parameter. It is a free text area.
- **defaultValue:** The default value of the parameter, if no value is entered while deployment.
- **possibleValues:** The list of possible values from which the user must select a value. 

**Example**

```json
{
    "name": "instance_size",
    "type": "String",
    "description": "instance_size",
    "possibleValues": [
        "t2.large",
        "t2.xlarge"
    ]
}
```

#### inputMapping

The **inputMapping** object contains the declaration of parameters that are used to deploy a workflow layer. The parameters that you can declare are based on the action that has been defined for the workflow layer. For more information, see <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-workflow', viewPage: 'understand-solution-package-schema', viewSection: 'actions'})" style="text-decoration:none">Supported workflow actions</a>.

You can declare parameters for multiple workflow layers in a single **inputMapping** object.

The object must be in the following format:

```json
"inputMapping": {
    "workflowLayerName": {
        <Input Mapping parameters for the workflow layer>
    },
     "workflowLayerName": {
        <Input Mapping parameters for the workflow layer>
    }
}
```

### <a id="output" name="output"></a>output

This data object is used to declare the output parameters of a solution package. You can define multiple parameters in the **output** object. You can view the result of the parameters defined in the **output** object after the solution package is deployed. 

The output parameters can also be used as input parameters in another solution package. 

The object must be in the following format:

```json
{
   "outputs": [
    {
      "name": "output1",
      "value": "${#input.cidr}",
      "description": "Output example with default type and directly from inputs of the solution package"
    },
    {
      "name": "output2",
      "value": "${#output['vpc']['customer']}",
      "description": "Output  example from the output of a workflow layer",
      "type": "String"
    }
  ]
}
```

Following are the attributes of the **output** object:

- name
- value
- description
- type

#### name

The name of the output parameter.

#### value

The value for the **output** parameter. There are multiple ways to define values for output parameters.

- **Case 1**: Use the value of an input parameter that is defined in the solution package.

  ```json
  {
  	"name": "vpc_cidr",
  	"value": "${#input['vpc_cidr']}",
  	"type": "String"
  }
  ```

- **Case 2**: Use the value of an output parameter of any workflow layer defined in the solution package.

  ```json
  {
  	"name": "vpc_id",
  	"value": "${#output['network-layer']['vpc_id']}",
  	"type": "String"
  }
  ```

  In this case, **network-layer** is name of the workflow layer from where the output parameter will be received.

- **Case 3**: Use the combined value of multiple input parameters or output parameters of any workflow layer defined in the solution package.

  ```json
  {
  	"name": "resource-name-prefix",
  	"value": "${#output['network-layer']['customer_name']}-${#output['network-layer']['env']}",
  	"type": "String"
  }
  ```

#### description

The description of the output parameter. This is a free text section.

#### type

The type of the **output** parameter. The supported types are List, String, Boolean, Map, and Integer. The default value of the parameter is **String**, if no value is specified while creating the solution package.

## <a id="actions" name="actions"></a>Supported workflow actions

The <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-workflow', viewPage: 'understand-solution-package-schema', viewSection: 'workflow'})" style="text-decoration:none">workflow</a> data object contains the list of actions that a solution package must execute. For each workflow action, you must specify the appropriate data, input mapping, and output parameters.

The Solution Package schema supports the following workflow actions:

- <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-workflow', viewPage: 'understand-solution-package-schema', viewSection: 'deploy-env'})" style="text-decoration:none">deployEnv</a>
- <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-workflow', viewPage: 'understand-solution-package-schema', viewSection: 'create-provider'})" style="text-decoration:none">createProvider</a>
- <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-workflow', viewPage: 'understand-solution-package-schema', viewSection: 'create-helm'})" style="text-decoration:none">createHelmRepo</a>
- <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-workflow', viewPage: 'understand-solution-package-schema', viewSection: 'deploy-helm'})" style="text-decoration:none">deployHelmChart</a>
- <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-workflow', viewPage: 'understand-solution-package-schema', viewSection: 'create-foundry'})" style="text-decoration:none">createFoundrySolutionPackage</a>
- <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-workflow', viewPage: 'understand-solution-package-schema', viewSection: 'deploy-foundry'})" style="text-decoration:none">deployFoundrySolutionPackage</a>
- <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-workflow', viewPage: 'understand-solution-package-schema', viewSection: 'deploy-sp'})" style="text-decoration:none">deploySolutionPackage</a>

### Summary of workflow action details

This section provides a quick overview of the data parameters, input mapping parameters, and output of each workflow action that the Solution Package schema supports. For more information, see the detailed section on each workflow action.

| Workflow action                                              | Data parameters                                   | Input Mapping parameters                                     | Output of the workflow action                                |
| ------------------------------------------------------------ | ------------------------------------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-workflow', viewPage: 'understand-solution-package-schema', viewSection: 'deploy-env'})" style="text-decoration:none">deployEnv</a><br>Deploys the environment that is defined in the **data** parameters. | envName<br>envVersion                             | provider<br>deployInput                                      | All outputs from the environment's deployment                |
| <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-workflow', viewPage: 'understand-solution-package-schema', viewSection: 'create-provider'})" style="text-decoration:none">createProvider</a><br>Creates a provider in Deploy Accelerator. | provider_name<br>provider_type                    | provider_json_string<br>provider_json                        | provider_id<br>provider_name<br>provider_type<br>globalProvider |
| <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-workflow', viewPage: 'understand-solution-package-schema', viewSection: 'create-helm'})" style="text-decoration:none">createHelmRepo</a><br>Registers a new Helm repository. You can use this action when helm charts to be installed by the **deployHelmChart** action are not present in the default repository. | repo_name                                         | repo_url<br>username<br>password<br>is_oci_registry<br>caFile<br>inSecureSkipTlsVerify | repo_name<br>repo_url                                        |
| <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-workflow', viewPage: 'understand-solution-package-schema', viewSection: 'deploy-helm'})" style="text-decoration:none">deployHelmChart</a><br>Deploys Helm charts to the Kubernetes cluster from the Helm repository that is defined in the **Input Mapping** parameters. | chart_name<br>chart_version                       | providerId<br>repoName<br>namespace<br>values                | helmStatus<br>helmDeploymentName<br>helmInstallLogs          |
| <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-workflow', viewPage: 'understand-solution-package-schema', viewSection: 'create-foundry'})" style="text-decoration:none">createFoundrySolutionPackage</a><br>Registers the Foundry solution package that is defined in the **data** parameters. The Foundry solution package must be located in the configured Artifactory of Hitachi Cloud Accelerator Platform.<br><br>This action initially pushes the Foundry solution package to the Harbor registry that is configured for the Foundry Control Plane. Next, it registers the Foundry solution package, which then starts showing up in the list of available Foundry solution packages in the Foundry Control Plane. | solution_package_name<br>solution_package_version | provider<br>oci_url<br>oci_username<br>oci_password          | None                                                         |
| <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-workflow', viewPage: 'understand-solution-package-schema', viewSection: 'deploy-foundry'})" style="text-decoration:none">deployFoundrySolutionPackage</a><br>Deploys the Foundry solution package that is defined in the **data** parameters. Only Foundry solution packages that are available in the Foundry Control Plane can be deployed. | solution_package_name<br>solution_package_version | auth<br>solution_config                                      | chartName<br>chartVersion<br>chartDescription<br>applicationVersion<br>modelVersion<br>solutionName<br>updateDate<br>solutionResources<br>status |
| <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-workflow', viewPage: 'understand-solution-package-schema', viewSection: 'deploy-sp'})" style="text-decoration:none">deploySolutionPackage</a><br>Deploys the solution package that is defined in the data parameters. This solution package can be a prerequisite for the current solution package. | solution_package_name<br>solution_package_version | providers<br>deploySolutionPackageInput                      | All outputs from the solution package's deployment           |

### <a id="deploy-env" name="deploy-env"></a>deployEnv action

The **deployEnv** workflow action deploys the environment that is defined in the **data** attribute.

**Example**

```json
{
    "action" : "deployEnv",
    "name" : "app",
    "condition" : "${#input.isApp}",
    "data" : {
        "envName" : "app_demo",
        "envVersion" : "01.00.00"
    }
}
    
```

#### Data parameters

Following are the data parameters for the **deployEnv** workflow action:

- envName
- envVersion  

You can define only one environment name and version per action. The environment name and version must be the same as used in the blueprint that is imported either automatically or manually. Make sure that the environment is present in Deploy Accelerator before starting the deployment.

_**Note:** The naming convention used for environments in a blueprint that are imported from the artifactory is **solutionPackageName_environmentName**. However, while specifying these environments in the **workflow** object, make sure that you enter only the **environmentName**. Before starting the deployment, the **solutionPackageName** is automatically prefixed to the environment name._

#### Input Mapping parameters

For the **deployenv** workflow action, you can declare the input mapping that will be used for the workflow layer with a specific provider.

- **provider** -- The provider to be used by the workflow layer for deployment. 

- **region** -- The region in which the environment is to be deployed. This is an optional parameter.

- **connection** -- The connection ID that can be used to connect to the instances in the deployed environment. This is an optional parameter.

- **chefEnvironment** -- The environment that is available on the selected Chef Server. This is an optional parameter.

- **deployInput** -- The values to be used while deploying the workflow layer using the solution package. 

  - **key** -- The exact name as defined in the **Input Variables** resource of the Deploy Accelerator environment for which you are configuring this input mapping. 

  - **value** -- The value for the **inputParameter** key. There are three types of input mapping values, as described below.

    **Case 1**: Mapping values for input parameters used in the solution package.

    ```json
    {
    	"key": "vpc_cidr",
    	"value": "${#input['vpc_cidr']}",
    	"type": "STRING"
    }
    ```

    **Case 2**: Mapping output parameter of another workflow layer with the input parameter. When a solution package has two blueprints that are not connected using the **Depends On** feature of Deploy Accelerator, the **output** parameter of the parent blueprint must be used in the child blueprint.

    ```json
    {
    	"key": "vpc_id",
    	"value": "${#output['network-layer']['vpc_id']}",
    	"type": "STRING"
    }
    ```

    In this case **network-layer** is name of the workflow layer from where the output parameter will be received. 

    **Case 3**: Mapping input parameter with multiple input parameters or workflow layer output.

    ```json
    {
    	"key": "resource-name-prefix",
    	"value": "${#output['network-layer']['customer_name']}-${#output['network-layer']['env']}",
    	"type": "STRING"
    }
    ```

  - **type** -- The type of the **inputParameter** key. The supported types are List, String, Boolean, Map, and Integer. The default value of the parameter is **String**, if no value is entered while creating the Solution Package.

    _**Note:** The value of the **inputParameter** key is resolved based on the type of the inputParameter. If you specify an incorrect type, complete deployment of the solution package will fail._

**Example**

```json
{
  "provider": "AWS_1",
  "region" : "${#input['region']}",
  "connection" : {
    "default" : "${#input['default']}",
    "some_resource" : "${#input['some_resource']}"
  },
  "chefEnvironment" : "${#input['chef_environment']}",
  "deployInput": []  
}
```

#### Output parameters

The output parameters for the **deployEnv** workflow action include all of the environment's deployment outputs.

### <a id="create-provider" name="create-provider"></a>createProvider

The **createProvider** workflow action creates a provider in Deploy Accelerator. Workflow Accelerator supports all providers and authentication methods that are available in Deploy Accelerator. For more information, see <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-deploy', viewPage: 'deploy-and-manage-environments', viewSection: 'provider'})" style="text-decoration:none">Configuring providers</a>. 

**Example**

```json
{
    "action": "createProvider",
    "name": "aws_provider_creation_helm",
    "condition": "${#input['provider_creation_helm']}",
    "data": {
        "provider_name": "helm_provider",
        "provider_type": "helm3"
    }
}
```

#### Data parameters

Following are the data parameters for the **createProvider** action:

- provider_name
- provider_type

#### Input Mapping parameters

For the **createProvider** action, you can define the inputs for providers with dynamic configuration. The parameters in the **createProvider** object must be same as the parameters used in Deploy Accelerator. You can define parameters for the provider in this section, or you can define the provider in the Solution package deployment object. You must use one of the following definition type.

- **provider_json_string**: Used to pass the provider JSON at the time of deployment, and must be defined in the Solution Package Deployment Object.

  ```json
  "inputMapping":{
      "aws_provider_creation": {
          "provider_json_string": {"#input['provider-json']"}   
      } 
  } 
  ```

- **provider_json:** The parameters for defining a provider. The parameters are same as the parameters in the provider definition JSON in the Deploy Accelerator. You might need to modify the parameters as per the provider type. The provider parameters defined in this section are fixed.

  - **access_key**: Access key to the AWS account.
  - **secret_key**: Secret key to the AWS account.
  - **region**: Region of the AWS account.

  ```json
  "inputMapping": {
      "aws_provider_creation": {
          "provider_json": {
              "access_key": "${#input.access_key}",
              "secret_key": "${#input.secret_key}",
              "region": "${#input.region}"        
          }
      } 
  }
  ```

#### Output parameters

Following are the output parameters for the **createProvider** workflow action:

- provider_id
- provider_name
- provider_type
- globalProvider

### <a id="create-helm" name="create-helm"></a>createHelmRepo action

The **createHelmRepo** action registers a new Helm repository. You can use this action when the helm charts to be installed by the **deployHelmChart** action are not available in the **default** repository in artifactory.

**Example**

```json
{
    "action": "createHelmRepo",
    "name": "repoSP",
    "condition": "${#input['repoSP']}",
    "data": {
        "repo_name": "repo"
    }
}
```

#### Data parameters

The data parameter for the **createHelmRepo** workflow action is **repo_name**.

A repository named **default** is already created in the Helm service. Therefore, ensure that you do not specify **default** as the repository name.

#### Input Mapping parameters

For the **createHelmRepo** workflow action, you can define the parameters to register the Helm repository with the URL provided in the parameters.

- **repo_url** -- URL for deployment of the Helm repository. 
- **username** -- Username for accessing the Helm repository.
- **password** -- Password for accessing the Helm repository.
- **is_oci_registry** -- Enable or disable support for OCI registry. Enter **false** for using Artifactory, and enter **true** for using Harbor.
- **caFile**: The CA bundle to verify the certificates of the HTTPS enabled servers.
- **inSecureSkipTlsVerify**: Enable or disable the TLS certificate check for the Helm repository.

 **Example**

```json
"inputMapping": {
    "helmRepo": {
        "repo_url":"$(#input.repo_url)",
        "username":"$(#input.username)",
        "password":"$(#input.password)",
        "is_oci_registry": false,
        "caFile": "$(#input.caFile)",
        "inSecureSkipTlsVerify": false
    }
}
```

#### Output parameters

Following are the output parameters for the **createHelmRepo** workflow action:

- repo_name
- repo_url

### <a id="deploy-helm" name="deploy-helm"></a>deployHelmChart

The **deployHelmChart** workflow deploys Helm charts to the Kubernetes cluster from the Helm repository deployed in the earlier action. If no repository is declared in the **createHelmRepo** action, it refers to the the default repository in artifactory.

**Example**

```json
{
    "action": "deployHelmChart",
    "name": "deploy_helm",
    "condition": "${#input['deploy_helm']}",
    "data": {
        "chart_name": "repo/platform-helm-sampleapp",
        "chart_version": "0.1.2"
    }
}
```

#### Data parameters

Following are the data parameters for the deployHelmChart workflow action:

- chart_name
- chart_version

The chart_name must be in the format **repo_name/chart_name**. If you have not declared any **repo_name**, use **default/chart_name**.

#### Input Mapping parameters

For the **deployHelmChart** workflow action, you can deploy a Helm chart in the recently deployed Helm repository.

- **namespace** - The namespace in which the Helm Chart is deployed. If not defined, it is deployed in the default namespace.
- **repository** - Registered repository name with the service from where it will deploy the helm charts. (mandatory)
- **provider** - The provider for deploying Helm charts. It should be registered with Deploy Accelerator. (mandatory)
- **values** - JSON for overriding the default values of the Helm Chart from Solution Package.
- **values_string** - JSON for overriding the values from the Solution Package deployment object. The name must match the value defined in the solution package.

**Example**

```json
"deploy_helm": {
    "provider": "${#providers['provider_creation_helm']['provider_id']}",
    "repository": "${#output['helm_repo_creation']['repo_name']}",
    "namespace": "${#input['namespace']}",
    "values": {
        "docker": {
            "image": "reanplatform-sampleapp:0.0.1",
            "registry": {
                "username": "${#input.username}",
                "password": "${#input.password}",
                "server": "${#input.server}"
            }
        }
    }
}
```

#### Output parameters

Following are the output parameters for the **deployHelmChart** workflow action:

- helmStatus
- helmDeploymentName
- helmInstallLogs

### <a id="create-foundry" name="create-foundry"></a>createFoundrySolutionPackage action

The **createFoundrySolutionPackage** workflow action registers the Foundry solution package that is defined in the **data** attribute. This action consists of the following steps:

- The Foundry solution package, which is located in the configured Artifactory of Hitachi Cloud Accelerator Platform, is pushed to the Harbor registry that is configured for the Foundry Control Plane. 
- The Foundry solution package is registered and starts showing up in the list of available Foundry solution packages in the Foundry Control Plane.

**Example**

```json
{
    "action": "createFoundrySolutionPackage",
    "name": "foundry_package",
    "condition": "${#input['foundry_package']}",
    "data": {
        "solution_package_name": "hello-world-changed",
        "solution_package_version": "0.2.0"
    }
}
```

#### Data parameters

Following are the data parameters for the **createFoundrySolutionPackage** workflow action:

- solution_package_name
- solution_package_version

You can define only one Foundry solution package and version per action. The Foundry solution package name and version must be the same as the file name and version that is stored in the configured artifactory of Cloud Accelerator Platform. Before starting the deployment, make sure that the solution package is present in the configured repository of the artifactory.

If the Foundry solution package is already registered in the Foundry Control Plane, this action checks if there is any change in the Foundry solution package that is present in the configured repository of the Artifactory. If a change is identified, the registered Foundry solution package is updated.

_**Note:** If you destroy a deployment of the Workflow Accelerator solution package, the Foundry solution package that has already been registered does not get deregistered. It continues to be available in the Foundry Control Plane._

#### Input Mapping parameters

For the **createFoundrySolutionPackage** workflow action, you can declare the credentials for accessing the Harbor registry in which the Foundry solution package will be pushed, along with the provider for the Kubernetes cluster in which the Foundry Control Plane is installed. This Kubernetes provider must exist in Deploy Accelerator.

- **provider** -- The Kubernetes provider ID (in Deploy Accelerator) to be used by the workflow layer to connect to the cluster in which Foundry Control Plane is installed. You can get this provider ID either from the output of the previous layer or from the input parameters.
- **oci_url** -- URL for accessing the Harbor registry that is configured for the Foundry Control Plane.
- **oci_username** -- User name to sign-in to the Harbor registry.
- **oci_password** -- Password to sign-in to the Harbor registry.

For the OCI parameters, you can map values for input parameters used in the solution package.

**Example**

```json
"inputMapping": {
    "foundry-package": {
        "provider": "${#input['providerID']}",
        "oci_url": "${#input['harborHost']}",
        "oci_username": "${#input['harborUsername']}",
        "oci_password": "${#input['harborPassword']}"
    }
}
```

#### Output parameters

The **createFoundrySolutionPackage** workflow action has no output parameters.

### <a id="deploy-foundry" name="deploy-foundry"></a>deployFoundrySolutionPackage

The **deployFoundrySolutionPackage** workflow action deploys the Foundry solution package that is defined in the **data** attribute. Only Foundry solution packages that are available in the Foundry Control Plane can be deployed.

**Example**

```json
{
    "action": "deployFoundrySolutionPackage",
    "name": "foundry_package_deploy",
    "condition": "${#input['foundry_package']}",
    "data": {
        "solution_package_name": "hello-world-changed",
        "solution_package_version": "0.2.0"
    }
}
```

#### Data parameters

Following are the data parameters for the **deployFoundrySolutionPackage** workflow action:

- solution_package_name
- solution_package_version 

You can define only one Foundry solution package and version per action. The Foundry solution package name and version must be the same as the name and version that is registered in the Foundry control plane.

#### Input Mapping parameters

For the **deployFoundrySolutionPackage** workflow action, you can declare the credentials for accessing the Foundry Control Plane, along with optional configuration information about the Foundry Control Plane. 

- **auth** -- The authentication details required to connect to the Foundry Control Plane and deploy the Foundry solution package.

  - **client_id** -- Client ID to connect to the Foundry Control Plane.
  - **client_secret** -- Client Secret to connect to the Foundry Control Plane.
  - **username** -- Username to connect to the Foundry Control Plane.
  - **password** -- Password to connect to the Foundry Control Plane.
  - **foundry_host** -- Host on which the Foundry Control Plane is installed. 
  - **namespace** -- Kubernetes namespace in which the Foundry Control Plane is installed.

- **solution_config** -- Information about the Foundry solution package deployment.

  - **modelVersion** -- Version of the Foundry Control Plane.

  - **values** OR **values_string** -- You can either provide a fixed list of values or specify that the values will be taken from a JSON string that the user will provide as input while deploying the solution package.

    **Format for values** 

    ```json
    "values": {
        "image": {
            "gatekeeperInitPullPolicy": "IfNotPresent",
            "pullPolicy": "IfNotPresent",
            "repository": "harbor.prod.platfom/foundry/foundry-hello-world",
            "tag": "2.0.0.345"
        }
    }
    ```

    **Format for values_string**

    ```json
    "values_string": "${#input['values_from_input_param']}"
    
    ```

**Example:**

```json
"inputMapping": {
    "foundry-package-deploy": {
        "auth": {
            "client_id": "${#input['clientId]}",
            "client_secret": "${#input['clientSecret]}",
            "username": "${#input['username]}",
            "password": "${#input['password]}",
            "foundry_host": "${#input['foundryHost]}",
            "namespace": "${#input['namespace]}"
        },
        "solution_config": {
            "modelVersion": "${#input['modelversion']}",
            "values_string": "${#input['values']}"
        }
    }
}
```

#### Output parameters

Following are the output parameters for the **deployFoundrySolutionPackage** workflow action:

- chartName
- chartVersion
- chartDescription
- applicationVersion
- modelVersion
- solutionName
- updateDate
- solutionResources
- status

### <a id="deploy-sp" name="deploy-sp"></a>deploySolutionPackage

The **deploySolutionPackage** workflow action deploys the Workflow Accelerator solution package that is a prerequisite for the current solution package.

Example

```json
{
    "action": "deploySolutionPackage",
    "name": "sc_dependency1",
    "condition": "${#input['Is_solution_package_deployment']}",
    "data": {
        "solution_package_name": "SolutionPackage_A1",
        "solution_package_version": "00.00.100"
    }
}
```

#### Data parameters

Following are data parameters for the **deploySolutionPackage** workflow action:

- solution_package_name
- solution_package_version

You can define only one Workflow Accelerator solution package and version per action. The solution package name and version must be the same as defined in its solution package JSON.

#### Input Mapping parameters

For the **deploySolutionPackage** workflow action, you can declare the providers and the input parameters required for deploying all the layers from the solution package declared in the action.

- **Layer name object** (dynamic parameter): The name of the workflow layer to be deployed by the solution package defined in action.
- **providers**: List of the providers required for deploying all the layers from referenced solution package.
- **deploySolutionPackageInput**: List of all the input parameters required for deploying all the layers from referenced solution package.

**Example**

```json
"inputMapping" : {
    "sc_dependency1": {
        "providers" : {
            "aws-provider": "${#providers['aws-provider']}"
        },
        "deploySolutionPackageInput" : [
            {
                "name" : "vpc_cidr",
                "value" : "${#input.vpc_cidr}",
                "type" : "String"
            },
            {
                "name" : "env",
                "value" : "${#input.env},
                "type" : "String"
            },
            {
                "name" : "customer",
                "value" : "${#input.customer}",
                "type: "String"
            }
        ]
    }
}
```

#### Output parameters

The output parameters for the **deploySolutionPackage** workflow action include all of the solution package's deployment outputs.