# Step 4: Configure an IAM role for your ETL job<a name="tutorial-step4"></a>

When you create the AWS Glue ETL job, you specify an AWS Identity and Access Management \(IAM\) role for the job to use\. The role must grant access to all resources used by the job, including Amazon S3 \(for any sources, targets, scripts, driver files, and temporary directories\), and also AWS Glue Data Catalog objects\.

The assumed IAM role for the AWS Glue ETL job must also have access to the secret that was created in the previous section\. By default, the AWS managed role `AWSGlueServiceRole` does not have access to the secret\. To set up access control for your secrets, see [Authentication and Access Control for AWS Secrets Manager](https://docs.aws.amazon.com/secretsmanager/latest/userguide/auth-and-access.html) and [Limiting Access to Specific Secrets](https://docs.aws.amazon.com/secretsmanager/latest/userguide/auth-and-access_identity-based-policies.html#permissions_grant-limited-resources)\.

**To configure an IAM role for your ETL job**

1. Configure the permissions described in [Job\-related permissions](setting-up.md#getting-started-min-privs-job)\.

1. Configure the additional permissions needed when using connectors with AWS Glue Studio, as described in [Additional permissions when using connectors](setting-up.md#getting-started-min-privs-connectors)\.

## Next step<a name="tutorial-step4.1"></a>

 [Step 5: Create a job that uses the Elasticsearch connection](tutorial-step5.md) 