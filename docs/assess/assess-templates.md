---
title: Create and manage assessment templates
---

# Create and manage assessment templates

Hitachi Cloud Accelerator Platform - Assess ( Assess Accelerator) is a tool that automates the assessment of your cloud environment against the relevant security and compliance standards.<br>

This topic describes how to create and manage assessment templates, which are required to <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-assess', viewPage: 'run-assessment-policies', viewSection: 'Content'})" style="text-decoration:none">run assessment jobs</a>.

### Contents

- <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-assess', viewPage: 'assess-templates', viewSection: 'assessment-template'})" style="text-decoration:none">Assessment templates</a>
- <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-assess', viewPage: 'assess-templates', viewSection: 'connectes'})" style="text-decoration:none">Connecting to the Access Accelerator backend pod</a>
- <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-assess', viewPage: 'assess-templates', viewSection: 'upload-template'})" style="text-decoration:none">Creating and uploading assessment templates</a>
- <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-assess', viewPage: 'assess-templates', viewSection: 'view-template'})" style="text-decoration:none">Viewing uploaded assessment templates</a>
- <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-assess', viewPage: 'assess-templates', viewSection: 'update-template'})" style="text-decoration:none">Updating assessment templates</a>
- <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-assess', viewPage: 'assess-templates', viewSection: 'delete-template'})" style="text-decoration:none">Deleting assessment templates</a>

## <a id="assessment-template" name="assessment-template"></a>Assessment templates

Assess Accelerator supports multiple tools that can be used for assessments of your cloud infrastructure. For each assessment tool, Assess Accelerator provides a <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-assess', viewPage: 'assess-checks', viewSection: 'Content'})" style="text-decoration:none">set of checks</a> against which the cloud accounts are evaluated. An assessment template is a JSON template that defines the configurations of an assessment tool. It contains the list of checks to use and to ignore. Based on your requirements, you can create multiple assessment templates with different sets of checks.<br>

The following sections help you to understand the structure and format of the assessment templates.

- <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-assess', viewPage: 'assess-templates', viewSection: 'objects'})" style="text-decoration:none">Objects in an assessment template</a>
- <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-assess', viewPage: 'assess-templates', viewSection: 'format'})" style="text-decoration:none">Format of an assessment template</a>
- <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-assess', viewPage: 'assess-templates', viewSection: 'sample-hcap'})" style="text-decoration:none">Assessment template for HCAP Assess</a>
- <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-assess', viewPage: 'assess-templates', viewSection: 'sample-prowler'})" style="text-decoration:none">Assessment template for Prowler</a>

### <a id="objects" name="objects"></a>Objects in an assessment template

| Parameter                     | Type   | Description                                                  |
| ----------------------------- | ------ | ------------------------------------------------------------ |
| name                          | String | Unique name of the assessment template. This name will appear in the list of assessment templates on the Assess Accelerator UI. This name is also used in the Read\|Update\|Delete operations of assessment templates in Elasticsearch.<br><br>_**Note:** Template JSONs are pushed to Elasticsearch using the APIs. Make sure the templates have unique names._ |
| description                   | String | Short description of the assessment template. This description appears in the UI by placing the mouse pointer on the **Information** icon. |
| cloud_provider_type           | String | Cloud provider type specific to the assessment template and the configurations defined in it. |
| assessment_framework_provider | List   | The assessment tool that we want to associate with the assessment template. Enter one of the following values:<br>- For Prowler tool: "**assessment.provider.prowler.2.2.0**"<br>- For HCAP Assess tool:  "**assessment.provider.hcap.assess**"<br />- For Azure CIS Blueprint tool: "**assessment.provider.azure_blueprint.1.1**" |
| data_collection_configuration | List   | Each object in this list describes assessment tool-specific customization configurations required to be done in the Data Collection phase of Assess DataPipeline.<br><br>These configurations (if specified) will override the default configurations defined by the **"assessment_framework_provider"** parameter. |
| customization                 | Object | Tool specific customizations to specify either set of Rules to skip or set of Rules to execute.<br>- <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-assess', viewPage: 'assess-checks', viewSection: 'prowler'})" style="text-decoration:none">Prowler checks</a><br>- <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-assess', viewPage: 'assess-checks', viewSection: 'checks'})" style="text-decoration:none">HCAP Assess checks</a><br /> The Azure CIS Blueprint tool does not currently support customization. |
| rules_to_include              | List   | Tool specific list of IDs of the checks that are to be included in the assessment. |
| rules_to_exclude              | List   | Tool specific list of IDs of the checks that are to be excluded from the assessment. |

### <a id="format" name="format"></a>Format of an assessment template

```json
{
   "name": "<assessment_template_unique_name>",
   "description": "Assessment template description",
   "cloud_provider_type": "AWS",
   "assessment_framework_provider": [],
   "data_collection_configuration":[
      {
         "image_name": "<Image_Name>",
         "image_tag": "<Image_Tag>",
         "customisation":{
            "rules_to_include":[
               "<check_ID1>",
               "<check_ID2>"
            ],
            "rules_to_exclude":[
               "<check_ID1>",
               "<check_ID2>"
            ]
         }
      }
   ],
}
```

***Notes***

- *If both **rules_to_include** and **rules_to_exclude** lists are empty, all the checks will be executed.*
- *If some checks are specified in the **rules_to_include** list and the **rules_to_exclude** list is empty, only the checks that are specified in **rules_to_include** list will get executed.*
- *If some checks are specified in the **rules_to_exclude** list and the **rules_to_include** list is empty, all the checks will be executed except the ones that are specified in **rules_to_exclude** list.*
- *If some checks are specified in both **rules_to_include** and **rules_to_exclude** lists, the checks specified in **rules_to_include** list will be ignored. In this case, all the checks will be executed except the ones that are specified in **rules_to_exclude** list.*
- *The **rule_IDs** must be same as mentioned in <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-assess', viewPage: 'assess-checks', viewSection: 'prowler'})" style="text-decoration:none">Prowler checks</a> and <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-assess', viewPage: 'assess-checks', viewSection: 'checks'})" style="text-decoration:none">HCAP Assess checks</a>.*

### <a id="sample-hcap" name="sample-hcap"></a>Assessment template for HCAP Assess

The HCAP Assess tool includes checks for the Security, Operations, and Cost Optimization policies in Assess Accelerator. When users select an HCAP Assess template for an assessment job, Assess Accelerator uses the HCAP Assess tool to run the checks for all the selected policies in the job. The checks that are run are based on the configurations in the selected assessment template.<br>

For example, say a user selects the following sample assessment template and all policies (Security, Operations, and Cost Optimization) in an assessment job. In this case, Assess Accelerator will use the HCAP Assess tool to run all checks in the Operations and Cost Optimization policies but will run only the CIS1.1, CIS1.3A, and CIS1.5 checks in the Security policy.

**Sample assessment template for HCAP Assess** 

```json
{
   "name": "template.hcap.assess",
   "description": "Assessment template is HCAP specific with customisations configured.",
   "cloud_provider_type": "AWS",
   "assessment_framework_provider": ["assessment.provider.hcap.assess"],
   "data_collection_configuration":[
      {
         "assessment_tool": "",
         "image_name": "",
         "image_tag": "",
         "customisation":{
            "rules_to_include":["CIS1.1","CIS1.3A","CIS1.5"],
            "rules_to_exclude":[]
         }
      }
   ],
}
```

### <a id="sample-prowler" name="sample-prowler"></a>Assessment template for Prowler

The Prowler tool includes checks for only the Security policy in Assess Accelerator. When users select a Prowler template for an assessment job, Assess Accelerator uses the Prowler tool to run the CIS checks in the Security policy. It uses the HCAP Assess tool to run the CAP checks in the Security policy and all checks in the Operations and Cost Optimization policies. The checks that are run are based on the configurations in the selected assessment template.<br>

For example, say a user selects the following sample assessment template and all policies (Security, Operations, and Cost Optimization) in an assessment job. In this case, Assess Accelerator will use the Prowler tool to run the check11, check12, and check13 checks in the Security policy and the HCAP Assess tool to run all checks in the Operations and Cost Optimization policies.

**Sample assessment template for Prowler**

```json
{
   "name": "Prowler template",
   "description": "This Assessment Template is Prowler specific enforcing only check11, check12, check13 checks to execute.",
   "cloud_provider_type": "AWS",
   "assessment_framework_provider": ["assessment.provider.prowler.2.2.0"],
   "data_collection_configuration":[
      {
         "assessment_tool": "",
         "image_name": "toniblyx/prowler",
         "image_tag": "2.2.0",
         "customisation":{
            "rules_to_include":[
               "check11",
               "check12",
               "check13"
            ],
            "rules_to_exclude":[]
         }
      }
   ],
}
```

### <a id="sample-azure" name="sample-azure"></a>Assessment template for Azure CIS Blueprint

The Azure CIS Blueprint includes the checks for Security policy in Assess Accelerator. When you select Azure template for assessment, it runs all the checks in the Security policy for Azure. For the list of checks supported by Azure CIS blueprint, see <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-assess', viewPage: 'assess-checks', viewSection: 'azure'})" style="text-decoration:none">Azure CIS Blueprint checks</a>.

***Note***:*The features in the template like data_collection_configuration, data_curation_configuration, rules_to_exclude, and rules_to_include are currently not supported in this version.*

**Sample assessment template for Azure CIS Blueprint**

```json
{
   "name": "template.azure_blueprint.1.1",
   "description": "Assessment template description",
   "cloud_provider_type": "AZURE",
   "assessment_framework_provider": ["assessment.provider.azure_blueprint.1.1"],
   "data_collection_configuration":[
      {
         "assessment_tool": "azure_blueprint",
         "image_name": "",
         "image_tag": "",
         "customisation":{
            "rules_to_exclude":[],
            "rules_to_include":[]
         }
      }
   ],
   "data_curation_configuration":[
      {
         "assessment_tool": "azure_blueprint",
         "image_name": "",
         "image_tag": "",
         "customisation":{
            "rules_to_exclude":[],
            "rules_to_include":[]
         }
      }
   ]
}
```

## <a id="connectes" name="connectes"></a>Connecting to the Assess Accelerator backend pod

To manually add assessment templates, you have to upload a JSON file to the Elasticsearch pod in the Assess Accelerator kubernetes setup. To upload a JSON file, the first step is to connect to the Assess Accelerator backend pod (**reanassess-backend**). This step is also required if you want to later view, update, or delete the uploaded JSON file.

1. Make sure that you have set up kube-config and are able to connect to the cluster from your local machine.

2. To get the pod name of the Assess backend-service, use the following command:

   ```
   kubectl get pod -l app=reanassess-backend -o=Name
   ```

   **Output**: 

   ```
   pod/<assess_backend_pod_name>
   ```

   **Example Output Value:**

   ```
   pod/reanassess-backend-78bcfcf47-mdfgr
   ```

3. To connect to the Assess backend container, use the above pod name in the following command:

   ```
   kubectl exec --stdin --tty <assess_backend_pod_name> -- /bin/bash
   ```

## <a id="upload-template" name="upload-template"></a>Creating and uploading assessment templates

To manually add assessment templates, you have to upload a JSON file to the Elasticsearch pod in the Assess Accelerator kubernetes setup.

1. Create a JSON document using the pre-defined structure and format for the assessment template. For detailed information, see <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-assess', viewPage: 'assess-templates', viewSection: 'assessment-template'})" style="text-decoration:none">Assessment templates</a>.

   You must save the JSON document with the **.json** extension.

2. <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-assess', viewPage: 'assess-templates', viewSection: 'connectes'})" style="text-decoration:none">Connect to the Assess Accelerator backend kubernetes pod</a>.

3. Upload the assessment template JSON file that you have created to Elasticsearch by using the following command.

   ```
   curl -XPOST "<ES_Host>:9200/assessnow_custom/assessment_template?pretty" -d @<JSON_file_name>
   ```

   - `<ES_Host>` : Use the value **reanassess-es**.
   - `<JSON_file_name>` : Use the exact file name of the JSON file. 

   **Expected Output**

   ```
   {
     "_index" : "assessnow_custom",
     "_type" : "assessment_template",
     "_id" : "<some_autogenerated_id>",
     "_version" : 1,
     "result" : "created",
     "_shards" : {
       "total" : 3,
       "successful" : 1,
       "failed" : 0
     },
     "created" : true
   }
   ```

4. Make a note of the auto-generated ID of the template. 

   You will need the ID to view, update, or delete the assessment template. Alternatively, you can later search for the template, go through the output, and get the ID.

## <a id="view-template" name="view-template"></a>Viewing uploaded assessment templates

To view an assessment template that you had previously uploaded to Elasticsearch, <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-assess', viewPage: 'assess-templates', viewSection: 'connectes'})" style="text-decoration:none">connect to the Assess Accelerator backend kubernetes pod</a> and use the following command.

```
curl -XGET "<ES_Host>:9200/assessnow_custom/assessment_template/_search?pretty" -d '{"query": {"match": {"name": "<assessment_template_unique_name>"}}}'
```

- `<ES_Host>` : Use the value **reanassess-es**.
- `<assessment_template_unique_name>` : Use the name of the assessment template that you want to view.

**Expected Output**

```json
{
  "took" : 2,
  "timed_out" : false,
  "_shards" : {
    "total" : 5,
    "successful" : 5,
    "failed" : 0
  },
  "hits" : {
    "total" : 1,
    "max_score" : 0.6931472,
    "hits" : [
      {
        "_index" : "assessnow_custom",
        "_type" : "assessment_template",
        "_id" : "<some_autogenerated_id>",
        "_score" : 0.6931472,
        "_source" : {
          "name" : "<assessment_template_unique_name>",
          "description" : "Description of the assessment template.",
          "cloud_provider_type" : "AWS",
          "assessment_framework_provider" : [
            "assessment.provider.hcap.assess.python"
          ],
          "data_collection_configuration" : [
            {
              "assessment_tool" : "hcap.assess",
              "image_name": "",
              "image_tag": "",
              "customisation" : {
                "rules_to_include" : [ ],
                "rules_to_exclude" : [ ]
              }
            }
          ],
          "data_curation_configuration" : [ ]
        }
      }
    ]
  }
}
```

***Notes***

- *The actual contents of the assessment template are within the **"_source"** field.*
- *The results of the search query can return multiple templates since it returns all the matches in the keyword.*
- *Note the **_id** of the template to delete or update it later.*

## <a id="update-template" name="update-template"></a>Updating assessment templates

1. <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-assess', viewPage: 'assess-templates', viewSection: 'connectes'})" style="text-decoration:none">Connect to the Assess Accelerator backend kubernetes pod</a>.

2. If you have not previously noted the ID of the assessment template you want to update, <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-assess', viewPage: 'assess-templates', viewSection: 'view-template'})" style="text-decoration:none">use the command to view the assessment template</a>.

3. To update the assessment template, use the following command.

   ```
   curl -XPOST "<ES_Host>:9200/assessnow_custom/assessment_template/<assessment_template_id>?pretty"-d @<updated_JSON_file_name>
   ```

   - `<ES_Host>` : Use the value **reanassess-es**.
   - `<assessment_template_id>` :  From the output of the view command, use the value of the **"_id"** field.
   - `<updated_JSON_file_name>` : Use the exact file name of the JSON file. 

   **Expected Output**

   ```json
   {
     "_index" : "assessnow_custom",
     "_type" : "assessment_template",
     "_id" : "default_assessment_template",
     "_version" : 2,
     "result" : "updated",
     "_shards" : {
       "total" : 3,
       "successful" : 1,
       "failed" : 0
     },
     "created" : false
   }
   ```

## <a id="delete-template" name="delete-template"></a>Deleting assessment  templates

1. <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-assess', viewPage: 'assess-templates', viewSection: 'connectes'})" style="text-decoration:none">Connect to the Assess Accelerator backend kubernetes pod</a>.

2. If you have not previously noted the ID of the assessment template you want to delete, <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-assess', viewPage: 'assess-templates', viewSection: 'view-template'})" style="text-decoration:none">use the command to view the assessment template</a>.

3. To delete the assessment template, use the following command.

   ```
   curl -XDELETE "<ES_Host>:9200/assessnow_custom/assessment_template/<assessment_template_id>"
   ```

   - `<ES_Host>` : Use the value **reanassess-es**.
   - `<assessment_template_id>` : From the output of the view command, use the value of the **"_id"** field. 

   **Expected Output**

   ```json
   {
     "took" : 21,
     "timed_out" : false,
     "total" : 1,
     "deleted" : 1,
     "batches" : 1,
     "version_conflicts" : 0,
     "noops" : 0,
     "retries" : {
       "bulk" : 0,
       "search" : 0
     },
     "throttled_millis" : 0,
     "requests_per_second" : -1.0,
     "throttled_until_millis" : 0,
     "failures" : [ ]
   }
   ```

