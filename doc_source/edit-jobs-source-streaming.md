# Using a streaming data source<a name="edit-jobs-source-streaming"></a>

You can create streaming extract, transform, and load \(ETL\) jobs that run continuously and consume data from streaming sources in Amazon Kinesis Data Streams, Apache Kafka, and Amazon Managed Streaming for Apache Kafka \(Amazon MSK\)\.

**To configure properties for a streaming data source**

1. Go to the visual graph editor for a new or saved job\.

1. Choose a data source node in the graph for Kafka or Kinesis Data Streams\.

1. Choose the **Data source properties** tab, and then enter the following information:
   + **Database**: \(Optional\) Choose the database in the AWS Glue Data Catalog that contains the table associated with your streaming data source\. You can use the search field to search for a database by its name\. If you choose the option **Detect schema**, you don't need to populate this field\.
   + **Table**: \(Optional\) Choose the table associated with the source data from the list\. This table must already exist in the AWS Glue Data Catalog\. You can use the search field to search for a table by its name\. If you choose the option **Detect schema**, you don't need to populate this field\.
   + **Detect schema**: Choose this option to have AWS Glue Studio detect the schema from the streaming data, rather than storing the schema information in a Data Catalog table\.
   + **Window size**: By default, your ETL job processes and writes out data in 100\-second windows\. This allows data to be processed efficiently and permits aggregations to be performed on data that arrives later than expected\. You can modify this window size to increase timeliness or aggregation accuracy\. 

     AWS Glue streaming jobs use checkpoints rather than job bookmarks to track the data that has been read\. 
   + **Advanced connection options**: Expand this section to add key\-value pairs to specify additional connection options\. For information about what options you can specify here, see ["connectionType": "kafka"](https://docs.aws.amazon.com/glue/latest/dg/aws-glue-programming-etl-connect.html#aws-glue-programming-etl-connect-kafka) or ["connectionType": "kinesis"](https://docs.aws.amazon.com/glue/latest/dg/aws-glue-programming-etl-connect.html#aws-glue-programming-etl-connect-kinesis)in the *AWS Glue Developer Guide*\.

**Note**  
Data previews are not currently supported for streaming data sources\.