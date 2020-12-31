# Step 5: Create a job that uses the Elasticsearch connection<a name="tutorial-step5"></a>

After creating a role for your ETL job, you can create a job in AWS Glue Studio that uses the connection and connector for Open Spark ElasticSearch\.

If your job runs within a Amazon Virtual Private Cloud \(Amazon VPC\), make sure the VPC is configured correctly\. See [Configuring an Amazon VPC for your ETL job](setting-up.md#getting-started-vpc-config) for more information\.

1. In AWS Glue Studio, choose **Connectors**\.

1. In the **Your connections** list, select the connection you just created and choose **Create job**\.

1. In the visual job editor, choose the Data source node\. On the right, on the **Data source properties \- Connector** tab, configure additional information for the connector\. 

   1. Choose **Add schema** and enter the schema of the data set in the data source\. Connections do not use tables stored in the Data Catalog, which means that AWS Glue Studio doesn't know the schema of the data\. You must manually provide this schema information\. For instructions on how to use the schema editor, see [Editing the schema in a custom transform node](edit-jobs-transforms.md#transforms-custom-editschema)\.

   1. Expand **Connection options**\.

   1. Choose **Add new option** and enter the information needed for the connector that was not entered in the AWS secret: 
      + **es\.nodes** : **https://*<ElasticSearch endpoint>***
      + **es\.port** : **443**
      + **path** : **test**
      + **es\.nodes\.wan\.only\.** : **true**

      For an explanation of these connection options, refer to: [https://www.elastic.co/guide/en/elasticsearch/hadoop/current/configuration.html](https://www.elastic.co/guide/en/elasticsearch/hadoop/current/configuration.html)\.

1. Add a target node to the graph as described in [Adding nodes to the job graph](edit-job-add-nodes.md) and [Editing the data target node](data-target-nodes.md#edit-jobs-target)\.

1. Optionally, add one or more transform nodes as described in [Editing the data transform node](edit-jobs-transforms.md)\.

1. Configure the job properties as described in [Modify the job properties](managing-jobs-chapter.md#edit-jobs-properties), starting with step 3, and save the job\.