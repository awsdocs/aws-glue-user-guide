# Tutorial: Using the open\-source Elasticsearch Spark Connector<a name="tutorial-elastisearch-connector"></a>

Elasticsearch is a popular open\-source search and analytics engine for use cases such as log analytics, real\-time application monitoring, and clickstream analysis\. You can use Elasticsearch as a data store for your extract, transform, and load \(ETL\) jobs by configuring the Elasticsearch Spark Connector in AWS Glue Studio\. This connector is available for free from [AWS Marketplace](https://aws.amazon.com/marketplace/pp/B08PPT2V5J)\. 

In this tutorial, we will show how to connect to your Amazon Elasticsearch Service nodes with a minimal number of steps\. 

**Topics**
+ [Prerequisites](#tutorial-prerequisites)
+ [Step 1: \(Optional\) Create an AWS secret for your Elasticsearch cluster information](tutorial-step1.md)
+ [Step 2: Subscribe to the connector](tutorial-step2.md)
+ [Step 3: Activate the connector in AWS Glue Studio and create a connection](tutorial-step3.md)
+ [Step 4: Configure an IAM role for your ETL job](tutorial-step4.md)
+ [Step 5: Create a job that uses the Elasticsearch connection](tutorial-step5.md)
+ [Step 6: Run the job](tutorial-step6.md)

## Prerequisites<a name="tutorial-prerequisites"></a>

To use this tutorial, you must have the following:
+ Access to AWS Glue Studio
+ Access to an Elasticsearch cluster in the AWS Cloud
+ Configured access to the Amazon VPC that contains your data store, as described in [Configuring a VPC for your ETL job](setting-up.md#getting-started-vpc-config)\.
+ Configured permissions according to [Job\-related permissions](setting-up.md#getting-started-min-privs-job)
+ \(Optional\) Access to AWS Secrets Manager\.