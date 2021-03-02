# Solution package schema version 1.2

Solution package in Workflow Accelerator is a JSON file that allows you to define all the information that is required for installing end-to-end application across various cloud platforms. To register and deploy the solution packages that you create, you have to use REST APIs.

This page describes the version 1.2 of the solution package schema. To view the most recent schema, see Understand the solution package schema.

## Solution package example

 Each solution package contains multiple JSON blocks for different data object types.

 The following is an example of the solution package for installing Magento E-Commerce application:

```json
{
	"schemaVersion": "1.2",
	"metadata": {
		"name": "magento",
		"version": "00.00.01",
		"description": "This solution package is for installing Magento commerce application.",
		"icon": "http://https://magento.com/log.png",
		"applicationVersion": "01.00.00",
		"ownerName": "MFI",
		"ownerEmail": "customer.mfi@reancloud.com",
		"duration": {
			"minDeploymentTime": "1d 3h 20m",
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
	},
	"blueprints": [
		{
			"name": "VPC",
			"version": "0.1.1"
		},
		{
			"name": "Magento",
			"version": "1.0.1"
		}
	],
	"workflow": [
		"NwLayer:01.00.00",
		"Magento:01.00.00"
	],  
	"customData": {
		"name": "SAP Hana",
		"version": "2.0.0"
	},
	"providers": [
		{
			"name": "aws-provider",
			"type": "aws"
		},
        {
            "name": "artifactory_repo",
            "type": "artifactory",
            "default_provider_name": "default_artifactory"
		}
	],
	"input": {
		"inputParameters": [
			{
				"name": "vpc_cidr",
				"type": "String",
				"description": "VPC CIDR"
			},
			{
				"name": "env",
				"type": "String",
				"description": "Environment"
			},
			{
				"name": "customer",
				"type": "String",
				"description": "Customer Name"
			},
			{
				"name": "instance_size",
				"type": "String",
				"description": "instance_size",
				"possibleValues": [
					"t2.large",
					"t2.xlarge"
				]
			},
			{
				"name": "db_name",
				"type": "String",
				"description": "db_name"
			},
			{
				"name": "db_password",
				"type": "String",
				"description": "db_password"
			},
			{
				"name": "admin_email",
				"type": "String",
				"description": "Email id for the admin"
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
		],
		"inputMapping": {
			"NwLayer": {
				"provider": "aws-provider",
				"deployInput": [
					{
						"key": "vpc_cidr",
						"value": "${#input.vpc_cidr}"
					},
					{
						"key": "env",
						"value": "${#input.env}"
					},
					{
						"key": "customer",
						"value": "${#input.customer}",
						"type": "String"
					},
					{
						"key": "whitelisted_ip",
						"value": "${#input.whitelisted_ip}",
						"type": "List"
					},
					{
						"key": "tagsTest",
						"value": "${#input.tagsTest}",
						"type": "Map"
					}
				]
			},
			"MagentoApp": {
				"provider": "aws-provider",
				"deployInput": [
					{
						"key": "env",
						"value": "${#input.env}"
					},
					{
						"key": "customer",
						"value": "${#input.customer}"
					},
					{
						"key": "instance_size",
						"value": "${#input.instance_size}"
					},
					{
						"key": "db_name",
						"value": "${#input.db_name}"
					},
					{
						"key": "db_password",
						"value": "${#input.db_password}"
					},
					{
						"key": "admin_email",
						"value": "${#input.admin_email}"
					}
					{
						"key": "VPC_ID",
						"value": "${#output['NwLayer']['vpc_id']}" 
					}
					{
						"key": "Customer_full_ID",
						"value": "${#output['NwLayer']'customer_name']}-${#output['NwLayer']['env']}"
					}
				]
			}
		}
	}
}
```

## Data objects in the solution package schema

The solution package schema contains the following data objects:

- schemaVersion
- metadata
- blueprints
- providers
- workflow
- customData
- input

  - inputParameters
  - inputMapping

### schemaVersion

The version of the solution package schema. The entry for this parameter must **1.0** by default. You can search a solution package using the schema version attribute. This is a mandatory parameter.

### metadata

This data object contains the metadata about the Solution package and the application to be installed using Current Solution package. The information in the metadata section is used for displaying, accessing and searching the solution package by using parameters like name, version , language, cloud region, etc.

The object must be in the following format:

```json
"metadata": {
	"name": "magento",
	"version": "00.00.01",
	"description": "This solution package is for installing Magento e-commerce application.",
	"icon": "http://https://magento.com/log.png",
	"applicationVersion": "01.00.00",
	"ownerName": "MFI",
	"ownerEmail": "customer.mfi@reancloud.com",
	"duration": {
		"minDeploymentTime": "1d 3h 20m",
		"maxDeploymentTime": "1d 2h 30m"
	},
	"language": [
		"en_US"
	],
	"licenseName": "License#321",
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

Following are the attributes of the metadata object:

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
	"minDeploymentTime": "1d 3h 20m",
	"maxDeploymentTime": "1d 2h 30m"
}
```

The correct format for entry of time 1d 3h 20m for 1 day, 3 hours and 20 minutes. This format does not support time entry in seconds. 

#### language

List of languages supported by the application to be deployed using solution package.  The list must be the language code in ISO standard. For example,

```json
"language": [
	"en_US"
]
```

For more information on the language codes, in the ISO website, see [Codes for the Representation of Names of Languages]( http://www.loc.gov/standards/iso639-2/php/code_list.php ).

#### licenseName

The license required for using the solution package. Before entering the license name here, make sure that the license is created for the solution package. For more information on the creation of the license key, see the license-controller API documentation in Solution Package. The license-control API documentation is available at following URL: 
**https://{HCAP-base-URL}/api-documentation/solutionpackagedoc/swagger-ui.html#/license-controller**

#### cloudRegion (mandatory parameter)

List of cloud region where the solution package is to be deployed. For example, 

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
{
	"tagname1": "tag1 value",
	"tagname2": "tag2 value"
}
```

These tags can be used for creating a tag and searching a solution with the tag name for a specific tag value. For example,  you can tag a solution package as { "domain" : "commerce" }, which can be used for searching all the applications in the Finance domain. 

```json
"tags": {
	"domain": "commerce",
	"has_free_trials": false
}
```

### blueprints

This object contains the list of blueprints that will get automatically imported from the artifactory before starting the deployment of the application. In the artifactory, these blueprints must be stored in the repository that is configured in Deploy Accelerator.

Environments in the blueprint are imported into Deploy Accelerator with the naming convention **<solution_package_name>_<environment_name>**.

> **Note**: Blueprint will get imported only once, the solution package will reuse the previously imported blueprint if it is already present in Deploy Accelerator. The blueprint must be present in the artifactory with the provided name and version, otherwise complete deployment of the solution package will fail. 

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

##### name

Name of the blueprint. The entry must be exactly same as the name of the blueprint in the artifactory.

##### version

Version of the blueprint for the specified name.

> **Note:** You can also choose to manually import blueprints into Deploy Accelerator. In this case, you must specify an empty section for the **blueprints** object, as shown below.
>
> ```json
> "blueprints": []
> ```

### workflow

The execution order of the Deploy Accelerator environments. The Environment Name and Version must be same as declared in the blueprints data object. Make sure that the environment is present in Deploy Accelerator before starting the deployment . The object must be in the following format:

```json
"workflow": [
	"environment_name_1:environment_1_version_number",
	"environment_name_2:environment_2_version_number"
]
```

> **Note:** The naming convention used for environments in a blueprint that are imported from the artifactory is **<solution_package_name>_<environment_name>**. However, while specifying these environments in the workflow object, make sure that you enter only the **<environment_name>**. Before starting the deployment, the **<solution_package_name>_** is automatically prefixed to the environment name. 

For example:

```json
"workflow": [
	"NwLayer:01.00.00",
	"Magento:01.00.00"
]
```

### customData

This object allows you to define custom attributes for the solution package. These custom attributes can be used as a search parameter for the solution package. The object must be in the following format:

```json
"customData": {
	"name": "SAP Hana",
	"version": "2.0.0"
}
```

### providers

The list of providers that the environments defined in the workflow will be using while deployment of the blueprint. The object must be in the following format:

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

Depending on the target cloud provider and account in the blueprint, you can define the providers list in the following ways:

**Case 1**: All the blueprints for the solution are to be deployed on the same Cloud service Provider account.

```json
[
	{
		"name" : "aws_account1",
		"type" : "aws"
	}
]
```

**Case 2**: Blueprints in the solution package are to be deployed on two different accounts of the same cloud service provider.

```json
[
	{
		"name" : "aws_account1",
		"type" : "aws"
	},
	{
		"name" : "aws_account2",
		"type" : "aws"
	}
]
```

**Case 3**: Blueprints in the solution package targeting multiple cloud providers.

```json
[
	{
		"name" : "aws_account1",
		"type" : "aws"
	},
	{
		"name" : "k8s_provider",
		"type" : "helm"
	}
]
```

>  **Note:** Make sure you have added all providers in the providers list that will be required for deploying the blueprints. 

##### name 

Name of the provider. The entry must be exactly same as the provider declared in the blueprint.

##### type

Cloud service provider. For example, AWS, Google Cloud, Microsoft Azure, etc.

##### default_provider_name

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

### input

The **input** data object contains 2 sub objects **inputParameters** and **inputMapping**. The object must be in the following format:

```json
"input": {
	"inputParmaters": {
		/*Parameter definition*/
	},
	"inputMapping": {
		/*"Environment name"*/
		{
		 /*Parameter Mapping*/
		}
	}
}
```

#### inputParameters

The **inputParameters** object contains the declaration of unique parameters that are required for deploying the environment.  This section consists of all unique sets of inputs that the solution owner wants the user to enter while deploying the solution package. For example, instance_size, which can be used in the one of the blueprint to set the ec2 instance size 

```json
"inputParameters": [
	{
		"name": "vpc_cidr",
		"type": "String",
		"description": "VPC CIDR"
	},
	{
		"name": "env",
		"type": "String",
		"description": "Environment"
	},
	{
		"name": "customer",
		"type": "String",
		"description": "Customer Name"
	},
	{
		"name": "instance_size",
		"type": "String",
		"description": "instance_size",
		"possibleValues": [
			"t2.large",
			"t2.xlarge"
		]
	},
	{
		"name": "db_name",
		"type": "String",
		"description": "db_name"
	},
	{
		"name": "db_password",
		"type": "String",
		"description": "db_password"
	},
	{
		"name": "admin_email",
		"type": "String",
		"description": "Email id for the admin"
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

##### name

Name of the parameter. The name must be a single string without any space. 

##### description

Description of the parameter. You can add a detailed information about the application in this parameter. It is a free text area.

##### type

The data type of the input parameter. Supported data types are: List, String, Boolean, Json, Integer
The default value for datatype is String.

##### defaultValue

The default value of the parameter, if no value is entered while deployment. 

##### possibleValues

The list of possible values from which the user must select a value. 

###### Example: inputParameter

```json
{
	"name": "instance_size",
	"type": "String",
	"description": "instance_size",
	"possibleValues":
	[
		"t2.large",
		"t2.xlarge"
	]
}
```

#### inputMapping

The inputMapping object contains the declaration of input parameter that will be used for a specific environment with a specific provider.  The mapping of input parameter is done for an environment. An environment can have multiple parameters under it. You can declare parameters for multiple environments in single inputMapping object.

```json
"inputMapping": {
	"NwLayer": {
		"provider": "aws-provider",
		"deployInput": [
			{
				"key": "vpc_cidr",
				"value": "${#input.vpc_cidr}"
			},
			{
				"key": "env",
				"value": "${#input.env}"
			},
			{
				"key": "customer",
				"value": "${#input.customer}",
				"type": "String"
			},
			{
				"key": "whitelisted_ip",
				"value": "${#input.whitelisted_ip}",
				"type": "List"
			},
			{
				"key": "tagsTest",
				"value": "${#input.tagsTest}",
				"type": "Map"
			}
		]
	}
}
```

##### environment name (dynamic parameter)

The environment name for which the following parameters are used for deployment. 

##### provider

The provider to be used by the environment for deployment. 

##### deployInput

The values for the parameters to be used while deploying the environment using the solution package. 

###### key

The exact name as defined in the inputParameter object. 

###### value

The value for the inputParameter key. There are three types of input mapping values:

- **Case 1**: Mapping values for input parameters used in the solution package.

  ```json
	{
		"key": "vpc_cidr",
		"value": "${#input['vpc_cidr']}",
		"type": "String"
	}
  ```

- **Case 2**: Mapping environment output parameter of earlier deployed environment with the input parameter. When solution package has two blueprints which are not connected using **Depends On** feature of Deploy Accelerator, the output parameter of the parent blueprint must be used in the child blueprint.

  ```json
	{
		"key": "vpc_id",
		"value": "${#output['NwLayer']['vpc_id']}",
		"type": "String"
	}
  ```

  In this case **NWLayer** is name of the environment from where the output parameter will be received. 

- **Case 3**: Mapping input parameter with multiple input parameters or environment output.

  ```json
	{
		"key": "resource-name-prefix",
		"value": "${#output['NwLayer']['customer_name']}-${#output['NwLayer']['env']}",
		"type": "String"
	}
  ```


###### type

The type of the inputParameter key. The supported types are are **List**, **String**, **Boolean**, **JSON**, and **Integer**. The value that you enter for this parameter is case sensitive. Therefore, enter the supported types as mentioned in this section. If you enter any other value (for example: **map**), registration of the solution package will fail.

The default value of the parameter is **String**, if no value is entered while creating the Solution Package.

> **Note:** The value of the inputParameter key is resolved based on the type of the inputParameter. If you specify an incorrect type, complete deployment of the solution package will fail.