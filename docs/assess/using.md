---
title: Run assessment policies
---

# Run assessment policies
Hitachi Cloud Accelerator Platform - Assess ( Assess Accelerator) is a tool that automates the assessment of your cloud environment against the relevant security and compliance standards.<br>

This topic describes how you can use Assess Accelerator to run assessment jobs and view or download assessment reports.

## <a id="Content" name="Content"></a>Contents

**Get started**

- <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-assess', viewPage: 'run-assessment-policies', viewSection: 'overview'})" style="text-decoration:none">Overview of assessment policies</a>
- <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-assess', viewPage: 'run-assessment-policies', viewSection: 'access'})" style="text-decoration:none">Accessing Assess Accelerator</a>

**Run assessment jobs**

- <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-assess', viewPage: 'run-assessment-policies', viewSection: 'providers'})" style="text-decoration:none">Prerequisites for AWS Assessments</a>
- <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-assess', viewPage: 'run-assessment-policies', viewSection: 'providers'})" style="text-decoration:none">Prerequisites for Azure Assessments</a>
- <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-assess', viewPage: 'run-assessment-policies', viewSection: 'policy-run'})" style="text-decoration:none">Creating AWS assessment jobs</a>
- <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-assess', viewPage: 'run-assessment-policies', viewSection: 'azure-run'})" style="text-decoration:none">Creating Azure assessment jobs</a>

**View and download reports**

- <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-assess', viewPage: 'run-assessment-policies', viewSection: 'policy-results'})" style="text-decoration:none">Viewing assessment reports</a>
- <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-assess', viewPage: 'run-assessment-policies', viewSection: 'results-download'})" style="text-decoration:none">Downloading assessment reports</a>
- <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-assess', viewPage: 'run-assessment-policies', viewSection: 'compare-view'})" style="text-decoration:none">Viewing and downloading comparison reports</a>

## <a id="overview" name="overview"></a>Overview of assessment policies

Assess Accelerator contains out-of-the-box policies that help you to assess if your cloud infrastructure meets the best-practice standards based on different checks. Assessment reports that are generated provide the status for each assessment check and possible solutions for resolving issues.<br>

Assess Accelerator supports multiple tools that can be used for assessments of your environment. For each assessment tool, Assess Accelerator provides a specific set of checks. These checks are categorized under the assessment policies. For more information, see <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-assess', viewPage: 'assess-checks', viewSection: 'Content'})" style="text-decoration:none">Assessment Checks Reference</a>.<br>

The following table describes the out-of-the-box policies that are available to assess your cloud infrastructure.

| Policy name              | Description                                                  |
| ------------------------ | ------------------------------------------------------------ |
| Cost Optimization Policy | This policy enables you to assess how optimally you are managing the cost of your cloud infrastructure. It basically assesses cost optimization for your Amazon Web Services (AWS) environment by checking for unused Amazon Machine Images (AMIs), Snapshots, route tables, Elastic Load Balancers (ELBs), security groups, network interfaces, and much more. |
| Operations Policy        | This policy enables you to assess the operational efficiency of your AWS environment based on best practices. It evaluates your environment based on criteria such as creation of your own VPC, data encryption, creation of the required tags for instances, and use of appropriate IAM user names. |
| Security Policy          | This policy enables you to assess the security of your AWS  and Azure environment based on industry standards and best practices. It consists of security assessment for network compliance, monitoring compliance, logging compliance, and IAM compliance.<br>This policy is based on the best-practice security guidelines developed by the Center for Internet Security (CIS) for Amazon Web Services and Microsoft Azure environments. |

## <a id="access" name="access"></a>Accessing Assess Accelerator

Assess Accelerator is deployed as part of Hitachi Cloud Accelerator Platform.

1. Sign in to <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-platform-common', viewPage: 'createAndAccessAccount', viewSection: 'logon'})" style="text-decoration:none">Hitachi Cloud Accelerator Platform</a>.


   For information on creating a Hitachi Cloud Accelerator Platform account, see <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-platform-common', viewPage: 'createAndAccessAccount', viewSection: 'create'})" style="text-decoration:none">Create & access account</a>.

2. Click the **Module selector** icon (![](/images/rean-platform-common/icon_accelerator.PNG)) in the top-left corner.

   The Assess Accelerator home page appears.

_**Note:** You can access Assess Accelerator and perform various actions only if your Hitachi Cloud Accelerator Platform administrator has granted you the appropriate permissions._

## <a id="providers" name="providers"></a>Prerequisites for AWS Assessments

The prerequisites for AWS assessment includes creating a provider. Following are the prerequisites you need to complete before running assessments for AWS:

- <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-assess', viewPage: 'run-assessment-policies', viewSection: 'user'})" style="text-decoration:none">Creating IAM user and role with required permission</a>
- <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-assess', viewPage: 'run-assessment-policies', viewSection: 'configure-provider'})" style="text-decoration:none">Configuring a provider</a>

### <a id="user" name="user"></a>Creating IAM user and role with required permission

#### Creating AWS user

Before configuring a provider, you must create an Identity and Access Management (IAM) user or role with permissions to run the different assessment checks on your AWS infrastructure.

1. Download the following custom inline policies:

   - <a href="downloads/rean-assess/rean-assess-aws-iam-policy-1.json" download="rean-assess-aws-iam-policy.json">rean-assess-aws-iam-policy-1.json</a>
   - <a href="downloads/rean-assess/rean-assess-aws-iam-policy-2.json" download="rean-assess-aws-iam-policy.json">rean-assess-aws-iam-policy-2.json</a>
   - <a href="downloads/rean-assess/rean-assess-aws-iam-policy-3.json" download="rean-assess-aws-iam-policy.json">rean-assess-aws-iam-policy-3.json</a>

2. In the AWS account where you want to run the assessment policies, perform the following actions:

   - Create IAM policies by using the custom inline policies that you have downloaded.

      For step-by-step instructions, see the [AWS Identity and Access Management User Guide](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies_create.html).

      _**Important:** To enable Assess Accelerator to upload assessment reports to an S3 bucket, you must add the **s3:PutObject** permission to one of the IAM policies. To enable Assess Accelerator to create a new S3 bucket, you must also add the **s3:CreateBucket** permission, as shown in the following example:_

      ```
      {
          "Version": "2012-10-17",
          "Statement": [
              {
                  "Sid": "VisualEditor0",
                  "Effect": "Allow",
                  "Action": [
                      "s3:PutObject", 
                      "s3:CreateBucket"
                  ],
                  "Resource": "<s3_bucket_ARN>/*"
              }
          ]
      }
      ```

   - If you plan to use the **Instance Profile with Assume Role** or **Static Credentials with Assume Role** method while <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-assess', viewPage: 'run-assessment-policies', viewSection: 'configure-provider'})" style="text-decoration:none">configuring a provider</a>, perform the following actions:

     - Create an IAM role that Assess Accelerator can assume to run the assessment policies.

       For step-by-step instructions, see the [AWS Identity and Access Management User Guide](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_create_for-user.html).

     - Attach the IAM policies that you have created to this role.

      While creating the AWS provider, you must specify this IAM role.

   - If you plan to use the **Static Credentials** method while <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-assess', viewPage: 'run-assessment-policies', viewSection: 'configure-provider'})" style="text-decoration:none">configuring a provider</a>, perform the following actions:

     - Create an IAM group and attach the IAM policies that you have created to this group.

       For step-by-step instructions, see the [AWS Identity and Access Management User Guide](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_groups_create.html). 

     - Create an IAM user and add the user to the IAM group that you have created.

       For step-by-step instructions, see the [AWS Identity and Access Management User Guide](http://docs.aws.amazon.com/IAM/latest/UserGuide/id_users_create.html). 


     While creating the AWS provider, you must provide credentials of this IAM user. 

***Important****: Make sure that the IAM user/role does not have administrator access. As per AWS CIS Foundations Benchmark the use of administrator access is highly discouraged. This is applicable for both Instance Profile and Static Credentials.*

#### <a id="providerk8s" name="providerk8s"></a>Creating Kubernetes user

Following are the steps to create a provider for instance profile when Assess is running on EKS. Before configuring a provider, you must create an Identity and Access Management (IAM) user or role with permissions.

1. Download the following custom inline policies:

   - <a href="downloads/rean-assess/rean-assess-aws-iam-policy-1.json" download="rean-assess-aws-iam-policy.json">rean-assess-aws-iam-policy-1.json</a>
   - <a href="downloads/rean-assess/rean-assess-aws-iam-policy-2.json" download="rean-assess-aws-iam-policy.json">rean-assess-aws-iam-policy-2.json</a>
   - <a href="downloads/rean-assess/rean-assess-aws-iam-policy-3.json" download="rean-assess-aws-iam-policy.json">rean-assess-aws-iam-policy-3.json</a>

2. Create an IAM role specific to Assess pod. In the AWS account where you want to run the assessment policies, perform the following actions:

   - Create an IAM Role (or use an existing role with the required name) for the Assess pod specific IAM Role**.** For the IAM role, you can enter the name as ***hcap-assess-iam-role***, or use a custom name specified in the **customer.yml** file before deploying Assess. The custom name must have the value "**assess_pods_iam_role_name**".
     Once the Assess is deployed, make sure to use only this Role for various Instance profile use-cases. For different use-cases, you can change the policies attached to this Role as per requirement.

   - After creating a new Role, select **Type of trusted entity** as **AWS Service - ec2**.

   - Add EKS worker node's IAM Role in the Trust relationships for the above role:

     - Under the Role, go to "**Trust relationships**" tab and click on "**Edit trust relationships**". Replace the policy JSON with the following JSON.

       ```
       {
         "Version": "2012-10-17",
         "Statement": [
           {
             "Effect": "Allow",
             "Principal": {
               "Service": "ec2.amazonaws.com"
             },
             "Action": "sts:AssumeRole"
           },
           {
             "Sid": "",
             "Effect": "Allow",
             "Principal": {
               "AWS": "<EKS_Worker_ec2_Node_IAM_Role_ARN>"
             },
             "Action": "sts:AssumeRole"
           }
         ]
       }
       ```

       For <EKS_Worker_ec2_Node_IAM_Role_ARN>, use the Role ARN of the IAM Role attached to the EKS Worker node ec2 instance, where Assess is running.

     - Save changes by clicking on "**Update Trust Policy**".

3. Attach the IAM policies to the above created role.

4. To create a provider with an instance profile without name use the following JSON:

   ```
   {
     "region": "<AWS_Region>"
   }
   ```

5. To create a provider with an instance profile without name with assume role use the following JSON:

   ```
   {
       "Version": "2012-10-17",
       "Statement": [
           {
               "Sid": "VisualEditor0",
               "Effect": "Allow",
               "Action": [
                   "sts:DecodeAuthorizationMessage",
                   "sts:GetCallerIdentity"
               ],
               "Resource": "*"
           },
           {
               "Sid": "VisualEditor1",
               "Effect": "Allow",
               "Action": "sts:*",
               "Resource": "<Assume_Role_ARN>"
           }
       ]
   }
   ```

### <a id="configure-provider" name="configure-provider"></a>Configuring a provider

Assess Accelerator uses the AWS providers that are available in Deploy Accelerator. 

1. Open Deploy Accelerator, on the home page, click the **More options** (![](/images/rean-platform-common/icon_more.PNG)) icon in the top-right corner and then click **Providers**.

2. On the Provider page, click **New**.

3. Enter the provider name and select the **AWS** provider type.

4. In the **Provider Details** section, use one of the following methods to specify authentication details of the AWS account in which Assess Accelerator must run the assessment policies.

   - **Instance Profile with Assume Role**

     This method provides a more secure way for cross-account access. Consider a scenario in which Hitachi Cloud Accelerator Platform is deployed in an AWS account that is different from the accounts in which Assess Accelerator must run the assessment policies. Instead of storing the access credentials for all those accounts in Assess Accelerator, you can attach a role to the instance in which Hitachi Cloud Accelerator Platform is deployed. Assess Accelerator can then assume a role in the other accounts and run the assessment policies. For more information about assuming roles, see the [AWS documentation](https://docs.aws.amazon.com/cli/latest/userguide/cli-roles.html).<br>

     To use the **Instance Profile with Assume Role** method, you must attach a role to the instance on which Hitachi Cloud Accelerator Platform is deployed. For the other accounts, you must specify a role that Assess Accelerator can assume to run the assessment policies. The role that you specify must have permissions to run the different assessment checks on the AWS infrastructure. It must also define the account in which Hitachi Cloud Accelerator Platform is deployed as a trusted entity.<br>

     In the **Provider Details** section, you must specify the details, as shown in the following example:

     ```
     {
         "region": "xx-xxxx-x",
         "assume_role": {
             "role_arn": "arn:aws:iam::xxxxxxxxxxx:role/assume_role",
             "session_name": "SESSION-NAME",
             "external_id": "assume_role"
         }
     }
     ```

   - **Instance Profile**

     This method provides a more secure way of accessing the account in which Assess Accelerator must run the assessment policies. However, Assess Accelerator can use this method only if a role is attached to the instance on which Hitachi Cloud Accelerator Platform is deployed. This role must have permissions to run the different assessment checks on the AWS infrastructure.<br>

     To use the Instance Profile method, you must specify only the region in which the assessment policies must be run, as shown in the following example:

     ```
     {
         "region": "xx-xxx-x"
     }
     ```

   - **Static Credentials with Assume Role**

     This method provides a more secure way for cross-account access. Consider a scenario in which Assess Accelerator needs to run the assessment policies across multiple AWS accounts. Instead of storing the access credentials for all these accounts in Assess Accelerator, you can specify long-term access credentials for only the parent account. Assess Accelerator can then use temporary credentials to access all other child accounts by assuming roles in those accounts. For more information about assuming roles, see the [AWS documentation](https://docs.aws.amazon.com/cli/latest/userguide/cli-roles.html).<br>

     To use the **Static Credentials with Assume Role** method, you must specify the credentials for only the parent account. For each child account, you must specify a role that Assess Accelerator can assume to run the assessment policies in that account. The role that you specify must have access to run the different assessment checks on the AWS infrastructure. It must also define the parent account as a trusted entity.<br>

     In the **Provider Details** section, you must specify the details, as shown in the following example:  

     ```
     {
         "access_key": "xxxxxxxxxx",
         "secret_key": "xxxxxxxxxx",
         "region": "xx-xxxx-x",
         "assume_role": {
             "role_arn": "arn:aws:iam::xxxxxxxxxxx:role/assume_role",
             "session_name": "SESSION-NAME",
             "external_id": "assume_role"
         }
     }
     ```

   - **Static Credentials**

     To use this method, you must specify the IAM user credentials for accessing the account in which Assess Accelerator must run the assessment policies, as shown in the following example:

     ```
     {
         "access_key": "ACCESS-KEY",
         "secret_key": "SECRET-KEY",
         "region": "xx-xxxx-x"
     }
     ```

     _**Note:** The IAM user whose credentials you specify must have permissions to run the different assessment checks on the AWS infrastructure. For more information, see <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-assess', viewPage: 'run-assessment-policies', viewSection: 'user'})" style="text-decoration:none">Before you begin</a>._

5. To verify whether the JSON syntax and the authentication details that you have specified are correct, click **VALIDATE**.

   To also save the provider after successfully validating the provider details, click **VALIDATE & SAVE**.

   _**Note:** The **VALIDATE** and **VALIDATE & SAVE** buttons are enabled only if you have specified a valid JSON syntax in the provider details._

6. Click **Save**.

   A new provider appears in the **Provider List** section.

   _**Note:** The **SAVE** button is enabled only if you have specified a valid JSON syntax in the provider details._

## <a id="azure" name="azure"></a>Prerequisites for Azure assessments

The Azure assessment in Assess Accelerator is executed by the Microsoft Azure blueprint service. The blueprint used for Azure assessment is a sample of the CIS Microsoft Azure Foundations Benchmark blueprint. For more details see, [Microsoft Azure Documentation](https://docs.microsoft.com/en-us/azure/governance/blueprints/samples/cis-azure-1-1-0#deploy). 

The prerequisite steps must be performed in the Azure account on which the assessment is to be run. The prerequisite involves the following steps:

- Deploy the Azure Blueprints CIS Microsoft Azure Foundations Benchmark blueprint sample
- Copy CIS Benchmark policy ID

### <a id="create-blueprint" name="create-blueprint"></a>Deploy the Azure Blueprints CIS Microsoft Azure Foundations Benchmark blueprint sample

The deployment steps include the following three steps:

- Create a new blueprint from the sample
- Mark your copy of the sample as **Published**
- Assign your copy of the blueprint to an existing subscription

For more information on how to deploy the sample blueprint, see [Microsoft Azure Documentation](https://docs.microsoft.com/en-us/azure/governance/blueprints/samples/cis-azure-1-1-0#deploy).

### <a id="cis" name="cis"></a>Copy CIS Benchmark policy ID

After a successful assignment of the blueprint, you must copy the policy ID for using while running the assessment job. 

To get the policy ID, perform the following actions:

1. In the Azure account, go to **Policy Service**. 

2. Select **CIS Microsoft Azure Foundations Benchmark 1.1.0** policy

3. From the Assignment ID parameter, click Copy to clipboard.

   ![](/images/rean-assess/azure_id.png)

4. Save the last section of the assignment ID. For example, if complete policy assignment id is ***/subscriptions/<subscription_id>/providers/Microsoft.Authorization/policyAssignments/qwertyuiop1234567*** then policy assignment ID to be saved is ***qwertyuiop1234567***.

## <a id="policy-run" name="policy-run"></a>Creating AWS assessment jobs

1. On the Home page of Assess Accelerator, select **Assess Now**.

2. For **Select your Cloud type**, select **AWS**.

	![](/images/rean-assess/assess_policyselect.PNG)

3. Enter a name for the assessment job.

   _**Tip:** You might run different types of assessment policies for one or more providers multiple times. Therefore, it is recommended that you specify a unique job name that helps you to identify the selected policies and any other details. For example, Operations-May2017-Week1._

4. In the **Select Providers** list, perform one of the following actions:

   - To run the assessment policies for one or more providers, select the check boxes next to those providers.
   - To run the assessment policies for all providers, select **All**.

   _**Note:** The assessment policies are run on all resources that are owned by the account that is specified in the provider. However, the account credentials that are specified must have the required access to run these policies on the resources. Otherwise, no data or incomplete data is displayed in the summary and detailed reports._

5. In the **Select Assessment Template** list, select a template for assessment. 

   You can create multiple templates with different checks for each template. For more information, see <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-assess', viewPage: 'assess-templates', viewSection: 'Content'})" style="text-decoration:none">Creating and managing assessment templates</a>.

6. Select the assessment policies that you want to run for the selected providers. 
   For information about the available policies, see <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-assess', viewPage: 'run-assessment-policies', viewSection: 'overview'})" style="text-decoration:none">Overview of assessment policies</a>.

7. _(Optional)_ To upload the assessment report for each provider to an AWS S3 bucket, perform the following actions:

   - Select the **Upload report to S3** check box.

   - Enter the S3 bucket name.

      For each selected provider, Assess Accelerator appends this S3 bucket name with the account ID (*BucketName-AccountID*).

      If the *BucketName-AccountID* bucket already exists for a provider, Assess Accelerator uploads the assessment reports to this existing bucket. Otherwise, Assess Accelerator creates a new S3 bucket and then uploads the assessment report to this bucket.

      _**Important:** To enable Assess Accelerator to upload assessment reports to an S3 bucket, you must add the **s3:PutObject** permission to the IAM policies that are used in each selected provider. To enable Assess Accelerator to create a new S3 bucket, you must also add the **s3:CreateBucket** permission, as shown in the following example:_

   	```json
   {
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "VisualEditor0",
            "Effect": "Allow",
            "Action": [
                "s3:PutObject", 
                "s3:CreateBucket"
            ],
            "Resource": "<s3_bucket_ARN>/*"
        }
    ]
   }
   	```

8. *(Optional)* To receive email notifications for assessments, perform the following actions:

   - Select **Enable Notification**.

   - In the **Customer Name** field, enter your company name and enter your email address that was used for creating the login credentials. You will receive an assessment start email and an email with a detailed report after assessment completion. 

     You can also enter multiple email addresses separated by a comma. The email addresses apart from the logged in user will only receive an assessment start email.

9. Click **START ASSESSMENT**. 

   The **Assessment Started** message appears.  

   ***Notes:*** 

   - *If the user has administrator access inherited from the IAM user in AWS, a validation message appears asking if you want to proceed with the assessment. You can choose to continue or cancel the assessment and check t he policies assigned to the IAM user.* 
   - *If the user is missing some required permissions, a validation message appears with a list of missing permissions. You can choose to continue or cancel the assessment and check the permissions assigned to the IAM user.*

10. To start another assessment, click **ASSESS MORE**.

11. To view the progress of the assessment, click **VIEW PROGRESS**.

12. Under the **My Assessment** tab, click **Refresh** (![](/images/rean-assess/icon_joblistrefresh.PNG)) to view the recently started assessment.
    If an assessment job contains multiple providers, Assess Accelerator creates a separate job for each provider in the format *JobName_ProviderName*. Following are the columns:

    - **Provider**: provider name

    - **Job Name**: job name for the provider. 

    - **Group**: assessment job name that you have specified.

      The status icons indicate whether the job is in progress (![](/images/rean-assess/icon_inprogress.PNG)), has failed (![](/images/rean-assess/icon_failed.PNG)), or has completed successfully (![](/images/rean-assess/icon_passed.PNG)). Place mouse-pointer over the status icons to see the job start date and time.

## <a id="azure-run" name="azure-run"></a>Creating Azure assessment jobs

1. On the Home page of Assess Accelerator, select **Assess Now**.

2. For **Select your Cloud type**, select **Azure**.

   ![](/images/rean-assess/assess_azure.png)

3. Enter a name for the assessment job.

   _**Tip:** You might run different types of assessment policies for one or more providers multiple times. Therefore, it is recommended that you specify a unique job name that helps you to identify the selected policies and any other details. For example, Operations-May2017-Week1._

4. In the **Select Providers** list, select a provider for running the assessment on that account. For Azure assessment job, you can currently select only one provider.

   _**Note:** The assessment policies are run on all resources that are owned by the account that is specified in the provider. However, the account credentials that are specified must have the required access to run these policies on the resources. Otherwise, no data or incomplete data is displayed in the summary and detailed reports._ 

5. In the **Select Assessment Template** list, select a template for assessment. 

   You can create multiple templates with different checks for each template. For more information, see <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-assess', viewPage: 'assess-templates', viewSection: 'Content'})" style="text-decoration:none">Creating and managing assessment templates</a>.

6. In the **Azure CIS Policy Assignment ID** field, enter the assignment ID acquired by performing the prerequisite steps. For more information, see <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-assess', viewPage: 'run-assessment-policies', viewSection: 'providers'})" style="text-decoration:none">Prerequisites for Azure assessments</a>. 

7. Select **Security Policy**. 

   For information about the available policies, see <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-assess', viewPage: 'run-assessment-policies', viewSection: 'overview'})" style="text-decoration:none">Overview of assessment policies</a>.

8. *(Optional)* To receive email notifications for assessments, perform the following actions:

   - Select **Enable Notification**.

   - In the **Customer Name** field, enter your company name and enter your email address that was used for creating the login credentials. You will receive an assessment start email and an email with a detailed report after assessment completion. 

     You can also enter multiple email addresses separated by a comma. The email addresses apart from the logged in user will only receive an assessment start email.

9. Click **START ASSESSMENT**. The **Assessment Started** message appears.  

10. To start another assessment, click **ASSESS MORE**.

11. To view the progress of the assessment, click **VIEW PROGRESS**.

12. Under the **My Assessment** tab, click **Refresh** (![](/images/rean-assess/icon_joblistrefresh.PNG)) to view the recently started assessment.
    If an assessment job contains multiple providers, Assess Accelerator creates a separate job for each provider in the format *JobName_ProviderName*. Following are the columns: 

    - **Provider**: provider name

    - **Job Name**: job name for the provider

    - **Group**: assessment job name that you have specified.

      The status icons indicate whether the job is in progress (![](/images/rean-assess/icon_inprogress.PNG)), has failed (![](/images/rean-assess/icon_failed.PNG)), or has completed successfully (![](/images/rean-assess/icon_passed.PNG)). Place mouse-pointer over the status icons to see the job start date and time.

## <a id="policy-results" name="policy-results"></a>Viewing assessment reports

1. On the Home page, select **My Assessment**.

2. From the list of assessment jobs, select the job for which you want to view a report.

   In the right panel, you can see a sunburst chart that provides a graphical summary of the policies that were run for the selected job, along with their status. 

   ![](/images/rean-assess/assess_chart.PNG)

   The sunburst chart consists of the following layers:

   - The center layer provides a summary of the assessment job. You can see the total number of checks that were run and the number of checks that failed.

   - The second layer represents the policies that were run for the selected job.

     For example, security policy, cost optimization policy, and operations policy.

   - The third layer represents different categories of assessment checks within each policy.

     For example, Security Assessment for Monitoring Compliance is a category of assessment check within the security policy.

   - The outermost layer represents each check that is included in a policy.

     For example, "Ensure no S3 buckets are public" is a specific check within the security policy.

3. To drill down into a specific set of data, click on a layer in the sunburst chart.

   When you click on the chart, the right panel further expands to display a report.

   ![](/images/rean-assess/assess_policydetails.PNG)

   The information displayed in the report is filtered based on the policy, assessment category, or assessment check that you click in the chart:

   - If you click on a policy in the second layer of the chart, you can view the different categories of assessment checks for that policy.

      ![](/images/rean-assess/assessmentcategories.PNG)

   - If you click on a specific category of assessment checks in the third layer of the chart, you can view the different assessment checks that are included in that category.

      ![](/images/rean-assess/assessmentchecks.PNG)

   - If you click on an assessment check in the outermost layer of the chart, you can view details about that check.

      ![](/images/rean-assess/assessmentcheckdetails.PNG)

      For each assessment check, you can view the status (failed or passed), severity level (CRITICAL, MAJOR, or WARNING), and possible solutions for resolving the identified issues.

   _**Note:** If the provider that you have selected does not have the permissions required to run a specific policy, no data is displayed for that policy._

4. _(Optional)_ To navigate to the previous layer, click on the center layer in the chart.

5. _(Optional)_ To rerun a failed job from the list of assessment jobs, click the **ReRun** link next to that job.

   _**Note:** If AWS credentials are not configured correctly, you cannot re-run the failed job from the list of assessment jobs._


## <a id="results-download" name="results-download"></a>Downloading assessment reports

1. On the Home page, select **My Assessment**.

2. From the list of assessment jobs, click the job for which you want to download a report. 

3. In the right panel, click **Download Report**.

4. In the Download Report window,  perform the following actions:

   ![](/images/rean-assess/assess_reportdownload.PNG)

   - In **Customer Name**, enter your company name.

   - In **Summary**, type a summary of the report.

     The text that you specify in this box is displayed in the **Executive Summary** section of the report.  

   - In the **Template** list, select the type of report as **Custom_Assess_Template**.

   - Click **Download**.

     Assess Accelerator generates the assessment report in the .docx format. The assessment report contains detailed tables that list the multiple assessment criteria, their status and severity level, and possible solutions.

     The report contains the following columns:

     - **Check ID:** The check ID for the assessment check. For more information, see <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-assess', viewPage: 'assess-checks', viewSection: 'Content'})" style="text-decoration:none">Assessment Checks Reference</a>.
     - **Assessment Check:** The check being performed on the resources.
     - **Status:** The result of the check after it is run. The status could either be **Passed** or **Failed**.
     - **Severity:** The severity of the result of the check. The severity could **Critical**, **Low**, or **Medium**.
     - **Output:** The output of the check after it is run. 
     - **Possible Solutions:** The recommendations after running the checks.



## <a id="compare-view" name="compare-view"></a>Viewing and downloading comparison reports

Assess Accelerator enables you to view and download a report that compares the assessment results across multiple jobs or providers. This report is especially useful in the following scenarios:

- If you have created an assessment job with multiple providers, you can generate a comparison report to view the assessment summary across all the providers.
- If you have created multiple jobs for the same provider over time, you can generate a comparison report to view the assessment summary across all the jobs for that provider.

**To view and download a comparison report, perform the following actions:**

1. On the Home page, select **Compare**. 

2. Click **Select Jobs**.

3. In the **Select your Cloud type** list, select **AWS** or **Azure**.

4. In the **Select job** list, perform one of the following actions:

   ![](/images/rean-assess/assesscompare_selectjobs.PNG)

   - To compare the assessment results across multiple jobs, select the check boxes next to those assessment jobs.
   - To compare the assessment results across all jobs, click **Select all jobs**.

   The selected jobs are displayed in the Summary table. To remove a job from the Summary table, click **Delete**(![](/images/rean-assess/compare_removejobs.PNG)).

   ![](/images/rean-assess/assesscompare_joblist.PNG)

   _**Note:** You can view the comparison report in the Assess Accelerator UI for a maximum of 6 jobs. If you select more than 6 jobs, you have to download the comparison report._

5. _(Only if you have selected a maximum of 6 jobs)_ To view and download the comparison report, perform the following actions:

   - In the Add Assessment jobs to compare window, click **OK**.

      On the **Compare** tab, you can view the comparison report for the selected jobs.

      ![](/images/rean-assess/assess_compare_report.PNG)

      If you move your mouse over a column header, you can see the provider name and the date and time when the assessment job was started.

   - To download the comparison report to your local computer, click **Export** and then select the **Comparison Report** option.

      The comparison report contains the following sheets:

      - **Dashboard:** This sheet provides an overall status of all the jobs or providers in charts and the graph format. It also displays the assessment status based on account, policy and checkset, and assessment checks (for example, Cost Optimization Assessment, Performance Assessment, and other Security Assessment) across all jobs or providers.
      - **Summary View:** This sheet lists all the assessment checks that were run and displays the total number of jobs (or providers) for which each check passed, failed, or was not applicable. It also displays the pass, fail, and not applicable percentage across all jobs or providers.
      - **Policy Raw Data:** This sheet provides all the assessment data that is gathered across all selected jobs or providers. You can use this data to generate your own reports and charts.   

   - _(Optional)_ To download a **TAR** file that contains the assessment summary report (*.docx* format) for each selected job, select the **Document Report** option.

      In the Download Report window, enter your company name and report summary, select the report type, and then click **DOWNLOAD**.


5. _(Only if you have selected more than 6 jobs)_ In the Add Assessment jobs to compare window, perform one of the following actions based on your requirements:

   - To download the comparison report to your local computer, click **Export Comparison Report**.

   - To download a **TAR** file that contains the assessment summary report (docx format) for each selected job, click **Export Document Report**.

      In the Download Report window, enter your company name and report summary, select the report type, and then click **DOWNLOAD**.
