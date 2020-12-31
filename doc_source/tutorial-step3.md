# Step 3: Activate the connector in AWS Glue Studio and create a connection<a name="tutorial-step3"></a>

After you choose **Continue to Launch**, you see the **Launch this software** page in AWS Marketplace\. After you use the link to activate the connector in AWS Glue Studio, you create a connection\. 

1. On the **Launch this software** page in the AWS Marketplace console, choose **Usage Instructions**, and then choose the link that appears in the window that appears\.

   Your browser is redirected to the AWS Glue Studio console **Create marketplace connection** page\.

1. Enter a name for the connection\. For example: **my\-es\-connection**\.

1. In the **Connection access** section, for **Connection credential type**, choose **User name and password**\. 

1. For the **AWS secret**, enter the name of your secret\. For example: **my\-es\-secret**\.

1. In the **Network options** section, enter the VPC information, if necessary\. 

1. Choose **Create connection and activate connector**\.

## Next step<a name="tutorial-step3.1"></a>

 [Step 4: Configure an IAM role for your ETL job](tutorial-step4.md) 