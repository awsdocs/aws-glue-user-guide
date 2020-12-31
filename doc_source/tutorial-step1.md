# Step 1: \(Optional\) Create an AWS secret for your Elasticsearch cluster information<a name="tutorial-step1"></a>

To safely store and use your connection credential, save your credential in AWS Secrets Manager\. The secret you create will be used later in the tutorial by the connection\. The credential key\-value pairs will be fed into the Elasticsearch Spark Connector as normal connection options\.

**Note**  
Your AWS Glue ETL job and secret must be hosted in the same Region\. Cross\-Region secret retrieval is not supported currently\.

For more information about creating secrets, see [Creating and Managing Secrets with AWS Secrets Manager](https://docs.aws.amazon.com/secretsmanager/latest/userguide/managing-secrets.html) in the *AWS Secrets Manager User Guide*\.

1. Sign in to the [AWS Secrets Manager console](https://console.aws.amazon.com/secretsmanager/)\.

1. On either the service introduction page or the **Secrets** list page, choose **Store a new secret**\.

1. On the **Store a new secret** page, choose **Other type of secret**\. This option means that you must supply the structure and details of your secret\.

1. Add a **Key** and **Value** pair for the Elasticsearch cluster user name\. For example:

   `es.net.http.auth.user`: *username*

1. Choose **\+ Add row**, and enter another key\-value pair for the password\. For example:

   `es.net.http.auth.pass`: *password*

1. Choose **Next**\.

1. Enter a secret name\. For example: **my\-es\-secret**\. You can optionally include a description\.

   Record the secret name, which is used later in this tutorial, and then choose **Next**\.

1. Choose **Next** again, and then choose **Store** to create the secret\.

## Next step<a name="tutorial-step1.2"></a>

 [Step 2: Subscribe to the connector](tutorial-step2.md) 