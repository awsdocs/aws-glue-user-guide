# Setting up for AWS Glue Studio<a name="setting-up"></a>

Complete the tasks in this section when you're using AWS Glue Studio for the first time:

**Topics**
+ [Sign up for AWS](#setting-up-aws-sign-up)
+ [Create an IAM administrator user](#setting-up-create-iam-user)
+ [Signing in as an IAM user](#getting-started-signin-iam-user)
+ [IAM permissions needed for the AWS Glue Studio user](#getting-started-min-privs)
+ [Job\-related permissions](#getting-started-min-privs-job)
+ [Set up IAM permissions for AWS Glue Studio](#getting-started-iam-permissions)
+ [Configuring an Amazon VPC for your ETL job](#getting-started-vpc-config)
+ [Populate the AWS Glue Data Catalog](#getting-started-populate-catalog)

## Sign up for AWS<a name="setting-up-aws-sign-up"></a>

If you do not have an AWS account, complete the following steps to create one\.

**To sign up for an AWS account**

1. Open [https://portal\.aws\.amazon\.com/billing/signup](https://portal.aws.amazon.com/billing/signup)\.

1. Follow the online instructions\.

   Part of the sign\-up procedure involves receiving a phone call and entering a verification code on the phone keypad\.

## Create an IAM administrator user<a name="setting-up-create-iam-user"></a>

If your account already includes an IAM user with full AWS administrative permissions, you can skip this section\.

**To create an administrator user for yourself and add the user to an administrators group \(console\)**

1. Sign in to the [IAM console](https://console.aws.amazon.com/iam/) as the account owner by choosing **Root user** and entering your AWS account email address\. On the next page, enter your password\.
**Note**  
We strongly recommend that you adhere to the best practice of using the **Administrator** IAM user below and securely lock away the root user credentials\. Sign in as the root user only to perform a few [account and service management tasks](https://docs.aws.amazon.com/general/latest/gr/aws_tasks-that-require-root.html)\.

1. In the navigation pane, choose **Users** and then choose **Add user**\.

1. For **User name**, enter **Administrator**\.

1. Select the check box next to **AWS Management Console access**\. Then select **Custom password**, and then enter your new password in the text box\.

1. \(Optional\) By default, AWS requires the new user to create a new password when first signing in\. You can clear the check box next to **User must create a new password at next sign\-in** to allow the new user to reset their password after they sign in\.

1. Choose **Next: Permissions**\.

1. Under **Set permissions**, choose **Add user to group**\.

1. Choose **Create group**\.

1. In the **Create group** dialog box, for **Group name** enter **Administrators**\.

1. Choose **Filter policies**, and then select **AWS managed \-job function** to filter the table contents\.

1. In the policy list, select the check box for **AdministratorAccess**\. Then choose **Create group**\.
**Note**  
You must activate IAM user and role access to Billing before you can use the `AdministratorAccess` permissions to access the AWS Billing and Cost Management console\. To do this, follow the instructions in [step 1 of the tutorial about delegating access to the billing console](https://docs.aws.amazon.com/IAM/latest/UserGuide/tutorial_billing.html)\.

1. Back in the list of groups, select the check box for your new group\. Choose **Refresh** if necessary to see the group in the list\.

1. Choose **Next: Tags**\.

1. \(Optional\) Add metadata to the user by attaching tags as key\-value pairs\. For more information about using tags in IAM, see [Tagging IAM entities](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_tags.html) in the *IAM User Guide*\.

1. Choose **Next: Review** to see the list of group memberships to be added to the new user\. When you are ready to proceed, choose **Create user**\.

You can use this same process to create more groups and users and to give your users access to your AWS account resources\. To learn about using policies that restrict user permissions to specific AWS resources, see [Access management](https://docs.aws.amazon.com/IAM/latest/UserGuide/access.html) and [Example policies](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies_examples.html)\.

## Signing in as an IAM user<a name="getting-started-signin-iam-user"></a>

 Sign in to the [IAM console](https://console.aws.amazon.com/iam) by choosing **IAM user** and entering your AWS account ID or account alias\. On the next page, enter your IAM user name and your password\.

**Note**  
For your convenience, the AWS sign\-in page uses a browser cookie to remember your IAM user name and account information\. If you previously signed in as a different user, choose the sign\-in link beneath the button to return to the main sign\-in page\. From there, you can enter your AWS account ID or account alias to be redirected to the IAM user sign\-in page for your account\.

## IAM permissions needed for the AWS Glue Studio user<a name="getting-started-min-privs"></a>

To use AWS Glue Studio, the user must have access to various AWS resources\. The user must be able to view and select Amazon S3 buckets, IAM policies and roles, and AWS Glue Data Catalog objects\.

### AWS Glue service permissions<a name="getting-started-min-privs-glue"></a>

AWS Glue Studio uses the actions and resources of the AWS Glue service\. Your user needs permissions on these actions and resources to effectively use AWS Glue Studio\. You can grant the AWS Glue Studio user the `AWSGlueConsoleFullAccess` managed policy, or create a custom policy with a smaller set of permissions\.

**Important**  
Per security best practices, it is recommended to restrict access by tightening policies to further restrict access to Amazon S3 bucket and Amazon CloudWatch log groups\. For an example Amazon S3 policy, see [Writing IAM Policies: How to Grant Access to an Amazon S3 Bucket](http://aws.amazon.com/blogs/security/writing-iam-policies-how-to-grant-access-to-an-amazon-s3-bucket/)\. 

### Amazon CloudWatch permissions<a name="getting-started-min-privs-cloudwatch"></a>

You can monitor your AWS Glue Studio jobs using Amazon CloudWatch, which collects and processes raw data from AWS Glue into readable, near\-real\-time metrics\. By default, AWS Glue metrics data is sent to CloudWatch automatically\. For more information, see [What Is Amazon CloudWatch?](https://docs.aws.amazon.com/AmazonCloudWatch/latest/DeveloperGuide/WhatIsCloudWatch.html) in the *Amazon CloudWatch User Guide*, and [AWS Glue Metrics](https://docs.aws.amazon.com/glue/latest/dg/monitoring-awsglue-with-cloudwatch-metrics.html#awsglue-metrics) in the *AWS Glue Developer Guide*\. 

To access CloudWatch dashboards, the user accessing AWS Glue Studio needs one of the following:
+ The `AdministratorAccess` policy
+ The `CloudWatchFullAccess` policy
+ A custom policy that includes one or more of these specific permissions:
  + `cloudwatch:GetDashboard` and `cloudwatch:ListDashboards` to view dashboards
  + `cloudwatch:PutDashboard` to create or modify dashboards
  + `cloudwatch:DeleteDashboards` to delete dashboards

For more information for changing permissions for an IAM user using policies, see [Changing Permissions for an IAM User](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_users_change-permissions.html) in the *IAM User Guide*\. 

## Job\-related permissions<a name="getting-started-min-privs-job"></a>

When you create a job using AWS Glue Studio, the job assumes the permissions of the IAM role that you specify when you create it\. This IAM role must have permission to extract data from your data source, write data to your target, and access AWS Glue resources\. 

The name of the role that you create for the job must start with the string `AWSGlueServiceRole` for it to be used correctly by AWS Glue Studio\. For example, you might name your role `AWSGlueServiceRole-FlightDataJob`\.

### Data source and data target permissions<a name="getting-started-min-privs-data"></a>

An AWS Glue Studio job must have access to Amazon S3 for any sources, targets, scripts, and temporary directories that you use in your job\. You can create a policy to provide fine\-grained access to specific Amazon S3 resources\. 
+ Data sources require `s3:ListBucket` and `s3:GetObject` permissions\. 
+ Data targets require `s3:ListBucket`, `s3:PutObject`, and `s3:DeleteObject` permissions\.

If the job uses data sources or targets other than Amazon S3, then you must attach the necessary permissions to the IAM role used by the job to access these data sources and targets\. For more information, see [Setting Up Your Environment to Access Data Stores](https://docs.aws.amazon.com/glue/latest/dg/start-connecting.html) in the *AWS Glue Developer Guide*\.

If you are using connectors and connections for your data store, you need additional permissions, as described in [Additional permissions when using connectors](#getting-started-min-privs-connectors)\.

### AWS Key Management Service permissions<a name="getting-started-min-privs-kms"></a>

If you plan to access Amazon S3 sources and targets that use server\-side encryption with AWS Key Management Service \(AWS KMS\), then attach a policy to the AWS Glue Studio role used by the job that enables the job to decrypt the data\. The job role needs the `kms:ReEncrypt`, `kms:GenerateDataKey`, and `kms:DescribeKey` permissions\. Additionally, the job role needs the `kms:Decrypt` permission to upload or download an Amazon S3 object that is encrypted with an AWS KMS customer master key \(CMK\)\.

There are additional charges for using AWS KMS CMKs\. For more information, see [AWS Key Management Service Concepts \- Customer Master Keys \(CMKs\)](https://docs.aws.amazon.com/kms/latest/developerguide/concepts.html#master_keys) and [AWS Key Management Service Pricing](https://aws.amazon.com/kms/pricing) in the *AWS Key Management Service Developer Guide*\.

### Additional permissions when using connectors<a name="getting-started-min-privs-connectors"></a>

If you are using an AWS Glue Custom Connector and connection to access a data store, the role used to run the AWS Glue ETL job needs additional permissions attached:
+ The AWS managed policy `AmazonEC2ContainerRegistryReadOnly` for accessing connectors purchased from AWS Marketplace
+ The `glue:GetJob` and `glue:GetJobs` permissions
+ AWS Secrets Manager permissions for accessing AWS secrets used with connections\. Refer to [IAM policy examples for secrets in AWS Secrets Manager](https://docs.aws.amazon.com/mediaconnect/latest/ug/iam-policy-examples-asm-secrets.html) for example IAM policies\.

If your AWS Glue ETL job runs within a Amazon VPC, then the VPC must be configured as described in [Configuring an Amazon VPC for your ETL job](#getting-started-vpc-config)\.

## Set up IAM permissions for AWS Glue Studio<a name="getting-started-iam-permissions"></a>

You can create the roles and assign policies to users and job roles by using the AWS administrator user\. 

1. Create an IAM policy for the AWS Glue service\.

   You can use the **AWSGlueConsoleFullAccess** AWS managed policy\. 

   To create your own policy, follow the steps documented in [Create an IAM Policy for the AWS Glue Service](https://docs.aws.amazon.com/glue/latest/dg/create-service-policy.html) in the *AWS Glue Developer Guide*\.

1. Create an IAM role for AWS Glue and attach the IAM policy to this role\.

   Follow the steps documented in [Create an IAM Role for AWS Glue](https://docs.aws.amazon.com/glue/latest/dg/create-an-iam-role.html) in the *AWS Glue Developer Guide*\.

1. Create a user for AWS Glue or AWS Glue Studio\.

   You can either use the administrator user for configuring AWS Glue resources, or you can create a separate user for accessing AWS Glue Studio\. 

   To create additional users for AWS Glue and AWS Glue Studio, follow the steps in [Creating Your First IAM Delegated User and Group](https://docs.aws.amazon.com/IAM/latest/UserGuide/getting-started_create-delegated-user.html) in the *IAM User Guide*\. 

## Configuring an Amazon VPC for your ETL job<a name="getting-started-vpc-config"></a>

Amazon Virtual Private Cloud \(Amazon VPC\) enables you to define a virtual network in your own logically isolated area within the AWS cloud, known as a *virtual private cloud \(VPC\)*\. You can launch your AWS resources, such as instances, into your VPC\. Your VPC closely resembles a traditional network that you might operate in your own data center, with the benefits of using AWS's scalable infrastructure\. You can configure your VPC; you can select its IP address range, create subnets, and configure route tables, network gateways, and security settings\. You can connect instances in your VPC to the internet\. You can connect your VPC to your own corporate data center, making the AWS cloud an extension of your data center\. To protect the resources in each subnet, you can use multiple layers of security, including security groups and network access control lists\. For more information, see the [Amazon VPC User Guide](https://docs.aws.amazon.com/vpc/latest/userguide/)\.

You can configure your AWS Glue ETL jobs to run within a VPC when using connectors\. You must configure your VPC for the following, as needed:
+ Public network access for data stores not in AWS\. All data stores that are accessed by the job must be available from the VPC subnet\. 
+ If your job needs to access both VPC resources and the public internet, the VPC needs to have a Network Address Translation \(NAT\) gateway inside the VPC\. 

  For more information, see [Setting Up Your Environment to Access Data Stores](https://docs.aws.amazon.com/glue/latest/dg/start-connecting.html) in the *AWS Glue Developer Guide*\.

## Populate the AWS Glue Data Catalog<a name="getting-started-populate-catalog"></a>

AWS Glue Studio uses datasets that are defined in the AWS Glue Data Catalog\. These datasets are used as sources and targets for ETL workflows in AWS Glue Studio\.

When reading from a data source, your ETL job needs to know the schema of the data being read\. The ETL job can get this information from a table in the AWS Glue Data Catalog\. You can use a crawler, the AWS Glue console or CLI, or an AWS CloudFormation template file to add databases and tables to the AWS Glue Data Catalog\. For more information about populating the Data Catalog, see [AWS Glue Data Catalog](https://docs.aws.amazon.com/glue/latest/dg/components-overview.html#data-catalog-intro) in the *AWS Glue Developer Guide*\.

When using connectors, you can use the schema builder to enter the schema information when configuring the data source node of your ETL job in AWS Glue Studio\. See [Authoring jobs with custom connectors](connectors-chapter.md#job-authoring-custom-connectors) for more information\.