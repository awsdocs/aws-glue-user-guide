# Setting up for AWS Glue Studio<a name="setting-up"></a>

Complete the tasks in this section when you're using AWS Glue Studio for the first time:

**Topics**
+ [Sign up for AWS](#setting-up-aws-sign-up)
+ [Create an IAM administrator user](#setting-up-create-iam-user)
+ [Signing in as an IAM user](#getting-started-signin-iam-user)
+ [IAM permissions needed for the AWS Glue Studio user](#getting-started-min-privs)
+ [Job\-related permissions](#getting-started-min-privs-job)
+ [Set up IAM permissions for AWS Glue Studio](#getting-started-iam-permissions)
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

1. \(Optional\) Add metadata to the user by attaching tags as key\-value pairs\. For more information about using tags in IAM, see [Tagging IAM Entities](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_tags.html) in the *IAM User Guide*\.

1. Choose **Next: Review** to see the list of group memberships to be added to the new user\. When you are ready to proceed, choose **Create user**\.

You can use this same process to create more groups and users and to give your users access to your AWS account resources\. To learn about using policies that restrict user permissions to specific AWS resources, see [Access Management](https://docs.aws.amazon.com/IAM/latest/UserGuide/access.html) and [Example Policies](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies_examples.html)\.

## Signing in as an IAM user<a name="getting-started-signin-iam-user"></a>

 Sign in to the [IAM console](https://console.aws.amazon.com/iam) by choosing **IAM user** and entering your AWS account ID or account alias\. On the next page, enter your IAM user name and your password\.

**Note**  
For your convenience, the AWS sign\-in page uses a browser cookie to remember your IAM user name and account information\. If you previously signed in as a different user, choose the sign\-in link beneath the button to return to the main sign\-in page\. From there, you can enter your AWS account ID or account alias to be redirected to the IAM user sign\-in page for your account\.

## IAM permissions needed for the AWS Glue Studio user<a name="getting-started-min-privs"></a>

To use AWS Glue Studio, the user must have access to various AWS resources\. The user must be able to view and select Amazon S3 buckets, IAM policies and roles, and AWS Glue Data Catalog objects\.

### AWS Glue service permissions<a name="getting-started-min-privs-glue"></a>

AWS Glue Studio uses the actions and resources of the AWS Glue service\. Your user needs permissions on these actions and resources to effectively use AWS Glue Studio\. You can grant the AWS Glue Studio user the `AWSGlueConsoleFullAccess` managed policy, or create a custom policy with a smaller set of permissions\.

### Amazon CloudWatch permissions<a name="getting-started-min-privs-cloudwatch"></a>

You can monitor your AWS Glue Studio jobs using Amazon CloudWatch, which collects and processes raw data from AWS Glue into readable, near\-real\-time metrics\. By default, AWS Glue metrics data is sent to CloudWatch automatically\. For more information, see [What Is Amazon CloudWatch?](https://docs.aws.amazon.com/AmazonCloudWatch/latest/DeveloperGuide/WhatIsCloudWatch.html) in the *Amazon CloudWatch User Guide*, and [AWS Glue Metrics](https://docs.aws.amazon.com/glue/latest/dg/monitoring-awsglue-with-cloudwatch-metrics.html#awsglue-metrics) in the *AWS Glue Developer Guide*\. 

To access CloudWatch dashboards from AWS Glue Studio, perform the following steps:

1. Sign in to the [IAM console](https://console.aws.amazon.com/iam/) as an administrator user\.

1. In the navigation pane, choose **Roles**\.

1. Choose **Create role**\.

1. Choose **Another AWS account**\.

1. For **Account ID**, enter the AWS Glue Studio user account, and then choose **Next: Permissions**\.

1. Choose **Next: Tags**\.

1. Choose **Next: Review**\.

1. Enter **CloudWatchDashboard** for Role name, and then choose **Create role**\.
**Important**  
You must use this exact string\.

1. When returned to the **Roles** page, choose the **CloudWatchDashboard** link in the message at the top of the page\. 

   You can also enter the role name in the Search field and then choose the role name\.

1. On the **Permissions** tab, in the **Permissions** policy section, choose **Add inline policy**\.

1. Choose the **JSON** tab and then enter the following text into the editor:

   ```
   {
       "Version": "2012-10-17",
       "Statement": [
           {
               "Action": [
                   "cloudwatch:Describe*",
                   "cloudwatch:Get*",
                   "cloudwatch:List*",
                   "cloudwatch:Search*",
                   "ec2:DescribeTags",
                   "lambda:InvokeFunction",
                   "logs:Describe*",
                   "logs:Filter*",
                   "logs:Get*",
                   "logs:Start*",
                   "logs:Stop*"
               ],
               "Resource": [
                  "*"
               ],
               "Effect": "Allow",
               "Sid": "Stmt1394386573000"
           }
       ]
   }
   ```

1. Choose **Review policy**\.

1. For **Name**, enter **CloudwatchMetricAPIs**, and then choose **Create policy**\.

For more information for changing permissions for an IAM user using policies, see [Changing Permissions for an IAM User](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_users_change-permissions.html) in the *IAM User Guide*\. 

## Job\-related permissions<a name="getting-started-min-privs-job"></a>

When you create a job using AWS Glue Studio, the job assumes the permissions of the IAM role that you specify when you create it\. This IAM role must have permission to extract data from your data source, write data to your target, and access AWS Glue resources\. 

The name of the role that you create for the job must start with the string `AWSGlueServiceRole` for it to be used correctly by AWS Glue Studio\. For example, you might name your role `AWSGlueServiceRole-FlightDataJob`\.

### Data source and data target permissions<a name="getting-started-min-privs-data"></a>

An AWS Glue Studio job must have access to Amazon S3 for any sources, targets, scripts, and temporary directories that you use in your job\. You can create a policy to provide fine\-grained access to specific Amazon S3 resources\. 
+ Data sources require `s3:ListBucket` and `s3:GetObject` permissions\. 
+ Data targets require `s3:ListBucket`, `s3:PutObject`, and `s3:DeleteObject` permissions\.

If the job uses data sources or targets other than Amazon S3, then you must attach the necessary permissions to the IAM role used by the job to access these data sources and targets\. For more information, see [Setting Up Your Environment to Access Data Stores](https://docs.aws.amazon.com/glue/latest/dg/start-connecting.html) in the *AWS Glue Developer Guide*\.

### AWS Key Management Service permissions<a name="getting-started-min-privs-kms"></a>

If you plan to access Amazon S3 sources and targets that use server\-side encryption with AWS Key Management Service \(AWS KMS\), then attach a policy to the AWS Glue Studio role used by the job that enables the job to decrypt the data\. The job role needs the `kms:ReEncrypt`, `kms:GenerateDataKey`, and `kms:DescribeKey` permissions\. Additionally, the job role needs the `kms:Decrypt` permission to upload or download an Amazon S3 object that is encrypted with an AWS KMS customer master key \(CMK\)\.

There are additional charges for using AWS KMS CMKs\. For more information, see [AWS Key Management Service Concepts \- Customer Master Keys \(CMKs\)](https://docs.aws.amazon.com/https://docs.aws.amazon.com/kms/latest/developerguide/concepts.html#master_keys) and [AWS Key Management Service Pricing](https://aws.amazon.com/kms/pricing) in the *AWS Key Management Service Developer Guide*\.

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

## Populate the AWS Glue Data Catalog<a name="getting-started-populate-catalog"></a>

AWS Glue Studio uses datasets that are defined in the AWS Glue Data Catalog\. These datasets are used as sources and targets for ETL workflows in AWS Glue Studio\.

Before you create a job in AWS Glue Studio, databases and tables must already exist in the AWS Glue Data Catalog\. You can use AWS Glue or an AWS CloudFormation template file to add databases and tables to the AWS Glue Data Catalog\. 

For more information about populating the Data Catalog, see [AWS Glue Data Catalog](https://docs.aws.amazon.com/glue/latest/dg/components-overview.html#data-catalog-intro) in the *AWS Glue Developer Guide*\.