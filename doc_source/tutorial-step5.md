# Step 5: Create a job that uses the Elasticsearch connection<a name="tutorial-step5"></a>

After creating a role for your ETL job, you can create a job in AWS Glue Studio that uses the connection and connector for Open Spark ElasticSearch\.

If your job runs within a Amazon Virtual Private Cloud \(Amazon VPC\), make sure the VPC is configured correctly\. For more information, see [Configuring a VPC for your ETL job](setting-up.md#getting-started-vpc-config)\.

**To create a job that uses the Elasticsearch Spark Connector**

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
![\[\]](http://docs.aws.amazon.com/glue/latest/ug/images/data-source-ES-properties-connection-screenshot.png)

      For an explanation of these connection options, refer to: [https://www.elastic.co/guide/en/elasticsearch/hadoop/current/configuration.html](https://www.elastic.co/guide/en/elasticsearch/hadoop/current/configuration.html)\.

1. Add a target node to the graph as described in [Adding nodes to the job diagram](edit-job-add-nodes.md) and [Editing the data target node](data-target-nodes.md#edit-jobs-target)\. 

   Your data target can be Amazon S3, or it can use information from an AWS Glue Data Catalog or a connector to write data in a different location\. For example, you can use a Data Catalog table to write to a database in Amazon RDS, or you can use a connector as your data target to write to data stores that are not natively supported in AWS Glue\.  
![\[\]](http://docs.aws.amazon.com/glue/latest/ug/images/data-target-options-screenshot.png)

   If you choose a connector for your data target, you must choose a connection created for that connector\. Also, if required by the connector provider, you must add options to provide additional information to the connector\. If you use a connection that contains information for an AWS secret, then you don’t need to provide the user name and password authentication in the connection options\.  
![\[\]](http://docs.aws.amazon.com/glue/latest/ug/images/data-target-connection-options-screenshot.png)

1. Optionally, add additional data sources and one or more transform nodes as described in [Editing the data transform node](edit-jobs-transforms.md)\.

1. Configure the job properties as described in [Modify the job properties](managing-jobs-chapter.md#edit-jobs-properties), starting with step 3, and save the job\.

## Next step<a name="tutorial-step5.1"></a>

 [Step 6: Run the job](tutorial-step6.md) 