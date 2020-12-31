# Using connectors and connections with AWS Glue Studio<a name="connectors-chapter"></a>

AWS Glue provides built\-in support for the most commonly used data stores \(such as Amazon Redshift, Amazon Aurora, Microsoft SQL Server, MySQL, MongoDB, and PostgreSQL\) using JDBC connections\. AWS Glue also allows you to use custom JDBC drivers in your extract, transform, and load \(ETL\) jobs\. For data stores that are not natively supported, such as SaaS applications, you can use connectors\. 

A *connector* is an optional code package that assists with accessing data stores in AWS Glue Studio\. You can subscribe to several connectors offered in AWS Marketplace\.

When creating ETL jobs, you can use a natively supported data source, a connector from AWS Marketplace, or your own custom connectors\. If you use a connector, you must first create a connection for the connector\. A *connection* contains the properties that are required to connect to a particular data store\. You use the connection with your data sources and data targets in the ETL job\. Connectors and connections work together to facilitate access to the data stores\.

**Topics**
+ [Overview of using connectors and connections](#using-connectors-overview)
+ [Adding connectors to AWS Glue Studio](#creating-connectors)
+ [Creating connections for connectors](#creating-connections)
+ [Authoring jobs with custom connectors](#job-authoring-custom-connectors)
+ [Managing connectors and connections](#managing-connectors)
+ [Developing custom connectors](#developing-custom-connectors)

## Overview of using connectors and connections<a name="using-connectors-overview"></a>

A *connection* contains the properties that are required to connect to a particular data store\. When you create a connection, it is stored in the AWS Glue Data Catalog\. You choose a connector, and then create a connection based on that connector\. 

You can subscribe to connectors for non\-natively supported data stores in AWS Marketplace, and then use those connectors when you're creating connections\. Developers can also create their own connectors, and you can use them when creating connections\.

The following steps describe the overall process of using connectors in AWS Glue Studio:

1. Subscribe to a connector in AWS Marketplace, or develop your own connector and upload it to AWS Glue Studio\. For more information, see [Adding connectors to AWS Glue Studio](#creating-connectors)\.

1. Create a connection\. You choose which connector to use and provide additional information for the connection, such as login credentials, URI strings, and virtual private cloud \(VPC\) information\. For more information, see [Creating connections for connectors](#creating-connections)\.

1. Create an IAM role for your job\. The job assumes the permissions of the IAM role that you specify when you create it\. This IAM role must have the necessary permissions to authenticate with, extract data from, and write data to your data stores\. For more information, see [Job\-related permissions](setting-up.md#getting-started-min-privs-job) and [Additional permissions when using connectors](setting-up.md#getting-started-min-privs-connectors)\.

1. Create an ETL job and configure the data source properties for your ETL job\. Provide the connection options and authentication information as instructed by the custom connector provider\. For more information, see [Authoring jobs with custom connectors](#job-authoring-custom-connectors)\.

1. Customize your ETL job by adding transforms or additional data stores, as described in [Editing ETL jobs in AWS Glue Studio](edit-nodes-chapter.md)\.

1. Customize the job run environment by configuring job properties, as described in [Modify the job properties](managing-jobs-chapter.md#edit-jobs-properties)\.

1. Run the job\.

## Adding connectors to AWS Glue Studio<a name="creating-connectors"></a>

A connector is a piece of code that facilitates communication between your target data source and AWS Glue\. You can either subscribe to a connector offered in AWS Marketplace, or you can create your own custom connector\. 

**Topics**
+ [Subscribing to AWS Marketplace connectors](#subscribe-marketplace-connectors)
+ [Creating custom connectors](#creating-custom-connectors)

### Subscribing to AWS Marketplace connectors<a name="subscribe-marketplace-connectors"></a>

AWS Glue Studio makes it easy to add connectors from AWS Marketplace\.

1. In the AWS Glue Studio console, choose **Connectors** in the console navigation pane\.

1. On the **Connectors** page, choose **Go to AWS Marketplace**\.

1. In AWS Marketplace, on the **Featured products**, choose the connector you want to use\. You can choose one of the featured connectors, or use search\. You can search on the name or type of connector, and you can use options to refine the search results\.

   If you want to use one of the featured connectors, choose **View product**\. If you used search to locate a connector, then choose the name of the connector\.

1. On the product page for the connector, use the tabs to view information about the connector\. If you decide to purchase this connector, choose **Continue to Subscribe**\.

1. Provide the payment information, and then choose **Continue to Configure**\. 

1. On the **Configure this software** page, choose the method of deployment and the version of the connector to use\. Then choose **Continue to Launch**\.

1. On the **Launch this software** page, you can review the **Usage Instructions** provided by the connector provider\. When you're ready to continue, choose **Activate connection in AWS Glue Studio**\.

   After a small amount of time, the console displays the **Create marketplace connection** page in AWS Glue Studio\.

1. Create a connection that uses this connector, as described in [Creating connections for connectors](#creating-connections)\. 

   Alternatively, you can choose **Activate connector only** to skip creating a connection at this time\. You must create a connection at a later date before you can use the connector\.

### Creating custom connectors<a name="creating-custom-connectors"></a>

You can also build your own connector and then upload the connector code to AWS Glue Studio\. 

Custom connectors are integrated into AWS Glue Studio through the AWS Glue Spark runtime API\. The AWS Glue Spark runtime allows you to plug in any connector that is compliant with the Spark, Athena, or JDBC interface\. It allows you to pass in any connection option that is available with the custom connector\. 

You can encapsulate all your connection properties with [AWS Glue Connections](https://docs.aws.amazon.com/glue/latest/dg/connection-using.html) and supply the connection name to your ETL job\. Integration with Data Catalog connections allows you to use the same connection properties across multiple calls in a single Spark application or across different applications\.

You can specify additional options for the connection\. The job script that AWS Glue Studio generates contains a `Datasource` entry that uses the connection to plug in your connector with the specified connection options\. For example:

```
Datasource = glueContext.create_dynamic_frame.from_options(connection_type = 
"custom.jdbc", connection_options = {"dbTable":"Account","connectionName":"my-custom-jdbc-
connection"}, transformation_ctx = "DataSource0")
```

1. Create the code for your custom connector\. For more information, see [Developing custom connectors](#developing-custom-connectors)\.

1. Add support for AWS Glue features to your connector\. Here are some examples of these features and how they are used within the job script generated by AWS Glue Studio:
   + **Data type mapping** – Your connector can typecast the columns while reading them from the underlying data store\. For example, a `dataTypeMapping` of `{"INTEGER":"STRING"}` converts all columns of type `Integer` to columns of type `String` when parsing the records and constructing the `DynamicFrame`\. This helps users to cast columns to types of their choice\.

     ```
     DataSource0 = glueContext.create_dynamic_frame.from_options(connection_type 
     = "custom.jdbc", connection_options = {"dataTypeMapping":{"INTEGER":"STRING"}", 
     connectionName":"test-connection-jdbc"}, transformation_ctx = "DataSource0")
     ```
   + **Partitioning for parallel reads** – AWS Glue allows parallel data reads from the data store by partitioning the data on a column\. You must specify the partition column, the lower partition bound, the upper partition bound, and the number of partitions\. This feature enables you to make use of data parallelism and multiple Spark executors allocated for the Spark application\.

     ```
     DataSource0 = glueContext.create_dynamic_frame.from_options(connection_type 
     = "custom.jdbc", connection_options = {"upperBound":"200","numPartitions":"4",
     "partitionColumn":"id","lowerBound":"0","connectionName":"test-connection-jdbc"},
     transformation_ctx = "DataSource0")
     ```
   + **Use AWS Secrets Manager for storing credentials** –The Data Catalog connection can also contain a `secretId` for a secret stored in AWS Secrets Manager\. The AWS secret can securely store authentication and credentials information and provide it to your ETL job at runtime\. Alternatively, you can specify the `secretId` from the Spark script as follows:

     ```
     DataSource = glueContext.create_dynamic_frame.from_options(connection_type 
     = "custom.jdbc", connection_options = {"connectionName":"test-connection-jdbc",
      "secretId"-> "my-secret-id"}, transformation_ctx = "DataSource0")
     ```
   + **Filtering the source data with row predicates and column projections** – The AWS Glue Spark runtime also allows users to push down SQL queries to filter data at the source with row predicates and column projections\. This allows your ETL job to load filtered data faster from data stores that support push\-downs\. An example SQL query pushed down to a JDBC data source is: `SELECT id, name, department FROM department WHERE id < 200.`

     ```
     DataSource = glueContext.create_dynamic_frame.from_options(connection_type = 
     "custom.jdbc", connection_options = {"query":"SELECT id, name, department FROM department 
     WHERE id < 200","connectionName":"test-connection-jdbc"}, transformation_ctx = 
     "DataSource0")
     ```
   + **Job bookmarks** – AWS Glue supports incremental loading of data from JDBC sources\. AWS Glue keeps track of the last processed record from the data store, and processes new data records in the subsequent ETL job runs\. Job bookmarks use the primary key as the default column for the bookmark key, provided that this column increases or decreases sequentially\. For more information about job bookmarks, see [Job Bookmarks](https://docs.aws.amazon.com/glue/latest/dg/monitor-continuations.html) in the *AWS Glue Developer Guide\.*

     ```
     DataSource0 = glueContext.create_dynamic_frame.from_options(connection_type = 
     "custom.jdbc", connection_options = {"jobBookmarkKeys":["empno"], "jobBookmarksKeysSortOrder"
     :"asc", "connectionName":"test-connection-jdbc"}, transformation_ctx = "DataSource0")
     ```

1. Package the custom connector as a JAR file and upload the file to Amazon S3\.

1. Test your custom connector\. For more information, see the instructions on GitHub at [https://github.com/aws-samples/aws-glue-samples/blob/master/ETLConnector/integrationtest/README.md](https://github.com/aws-samples/aws-glue-samples/blob/master/ETLConnector/integrationtest/README.md)\.

1. In the AWS Glue Studio console, choose **Connectors** in the console navigation pane\.

1. On the **Connectors** page, choose **Create custom connector**\.

1. On the **Create custom connector** page, enter the following information:
   + The path to the location of the custom code JAR file in Amazon S3\.
   + A name for the connector that will be used by AWS Glue Studio\.
   + Your connector type, which can be one of **JDBC**, **Spark**, or **Athena**\.
   + The name of the entry point within your custom code that AWS Glue Studio calls to use the connector\. 
     + For JDBC connectors, this field should be the class name of your JDBC driver\.
     + For Spark connectors, this field should be the fully qualified data source class name, or its alias, that you use when loading the Spark data source with the `format` operator\.
   + \(JDBC only\) The base URL used by the JDBC connection for the data store\.
   + \(Optional\) A description of the custom connector\.

1. Choose **Create connector**\. 

1. From the **Connectors** page, create a connection that uses this connector, as described in [Creating connections for connectors](#creating-connections)\.

## Creating connections for connectors<a name="creating-connections"></a>

An AWS Glue connection is a Data Catalog object that stores connection information for a particular data store\. Connections store login credentials, URI strings, virtual private cloud \(VPC\) information, and more\. Creating connections in the Data Catalog saves the effort of having to specify all connection details every time you create a job\.

1. In the AWS Glue Studio console, choose **Connectors** in the console navigation pane\.

1. Choose the connector you want to create a connection for, and then choose **Create connection**\.

1. On the **Create connection** page, enter a name for your connection, and optionally a description\.

1. Enter the connection details\. Depending on the type of connector you selected, you're prompted to enter additional information:
   + Enter the requested authentication information, such as a user name and password, or choose an AWS secret\.
   + For connectors that use JDBC, enter the information required to create the JDBC URL for the data store\.
   + If you use a virtual private cloud \(VPC\), then enter the network information for your VPC\.

1. Choose **Create connection**\.

   You are returned to the **Connectors** page, and the informational banner indicates the connection that was created\. You can now use the connection in your AWS Glue Studio jobs, as described in [Create jobs that use a connector](creating-jobs-chapter.md#create-jobs-connector)\.

## Authoring jobs with custom connectors<a name="job-authoring-custom-connectors"></a>

After you create a job that uses a connector for the data source, the visual job editor displays a job graph with a data source node configured for the connector\. You must configure the data source properties for that node\.

1. Sign in to the AWS Management Console and open the AWS Glue Studio console at [https://console\.aws\.amazon\.com/gluestudio/](https://console.aws.amazon.com/gluestudio/)\.

1. On the **Connectors** page, in the **Your connections** resource list, choose the connection you want to use in your job, and then choose **Create job**\. 

   Alternatively, on the AWS Glue Studio **Jobs** page, under **Create job**, choose **Source and target added to the graph**\. In the **Source** drop\-down list, choose the custom connector that you want to use in your job\. Optionally, you can choose a data target location\.  
![\[\]](http://docs.aws.amazon.com/glue/latest/ug/images/create-job-data-sources-screenshot.png)

1. Choose **Create** to open the visual job editor\.

1. Choose the connector data source node in the job graph\. Then, on the right\-side, in the node details panel, choose the **Source properties** tab, if it's not already selected\.  
![\[\]](http://docs.aws.amazon.com/glue/latest/ug/images/data-source-properties-connector-screenshot.png)

1. In the **Source Properties** tab, choose the connection that you want to use for this job\. 

   Enter the additional information required for each connection type:

------
#### [ JDBC ]
   + **Data source input type**: Choose to provide either a table name or a SQL query as the data source\. Depending on your choice, you then need to provide the following additional information:
     + **Table name**: The name of the table in the data source\. If the data source does not use the term *table*, then supply the name of an appropriate data structure, as indicated by the custom connector usage information \(which is available in AWS Marketplace\)\.
     + **Filter predicate**: A condition clause to use when reading the data source, similar to a `WHERE` clause, which is used to retrieve a subset of the data\.
     + **Query code**: Enter a SQL query to use to retrieve a specific dataset from the data source\. An example of a basic SQL query is:

       ```
       SELECT column_list FROM table_name WHERE where_clause
       ```
   + **Schema**: Because AWS Glue Studio is using information stored in the connection to access the data source instead of retrieving metadata information from a Data Catalog table, you must provide the schema metadata for the data source\. Choose **Add schema** to open the schema editor\. 

     For instructions on how to use the schema editor, see [Editing the schema in a custom transform node](edit-jobs-transforms.md#transforms-custom-editschema)\.
   + **Partition column**: \(Optional\) You can choose to partition the data reads by providing values for **Partition column**, **Lower bound**, **Upper bound**, and **Number of partitions**\. 

     The `lowerBound` and `upperBound` values are used to decide the partition stride, not for filtering the rows in table\. All rows in the table are partitioned and returned\. 
**Note**  
Column partitioning adds an extra partitioning condition to the query used to read the data\. When using a query instead of a table name, you should validate that the query works with the specified partitioning condition\. For example:  
If your query format is `"SELECT col1 FROM table1"`, then test the query by appending a `WHERE` clause at the end of the query that uses the partition column\.
If your query format is `"SELECT col1 FROM table1 WHERE col2=val"`, then test the query by extending the `WHERE` clause with `AND` and an expression that uses the partition column\.
   + **Data type casting**: If the data source uses data types that are not available in JDBC, use this section to specify how a data type from the data source should be converted into JDBC data types\. You can specify up to 50 different data type conversions\. All columns in the data source that use the same data type are converted in the same way\. 

     For example, if you have three columns in the data source that use the `Float` data type, and you indicate that the `Float` data type should be converted to the JDBC `String` data type, then all three columns that use the `Float` data type are converted to `String` data types\.

------
#### [ Spark ]
   + **Schema**: Because AWS Glue Studio is using information stored in the connection to access the data source instead of retrieving metadata information from a Data Catalog table, you must provide the schema metadata for the data source\. Choose **Add schema** to open the schema editor\. 

     For instructions on how to use the schema editor, see [Editing the schema in a custom transform node](edit-jobs-transforms.md#transforms-custom-editschema)\.
   + **Connection options**: Enter additional key\-value pairs as needed to provide additional connection information or options\. For example, you might enter a database name, table name, a user name, and password\.

     For example, for Elasticsearch, you enter the following key\-value pairs, as described in [Tutorial: Using the open\-source Elasticsearch Spark Connector](tutorial-elastisearch-connector.md):
     + `es.net.http.auth.user` : `username`
     + `es.net.http.auth.pass` : `password` 
     + `es.nodes` : `https://<Elasticsearch endpoint>`
     + `es.port` : `443`
     + `path`: `<Elasticsearch resource>`
     + `es.nodes.wan.only` : `true`

   For an example of the minimum connection options to use, see the sample test script [MinimalSparkConnectorTest\.scala](https://github.com/aws-samples/aws-glue-samples/blob/master/GlueCustomConnectors/development/Spark/MinimalSparkConnectorTest.scala) on GitHub, which shows the connection options you would normally provide in a connection\.

   which shows the connection options you would normally provide in a connection\.

------
#### [ Athena ]
   + **Table name**: The name of the table in the data source\. If using a connector for reading from Athena\-Cloudwatch logs, you would enter the table name `all_log_streams`\.
   + **Athena schema name**: Choose the schema in your Athena data source that corresponds to the database that contains the table\. If using a connector for reading from Athena\-Cloudwatch logs, you would enter a schema name similar to `/aws/glue/name`\.
   + **Schema**: Because AWS Glue Studio is using information stored in the connection to access the data source instead of retrieving metadata information from a Data Catalog table, you must provide the schema metadata for the data source\. Choose **Add schema** to open the schema editor\. 

     For instructions on how to use the schema editor, see [Editing the schema in a custom transform node](edit-jobs-transforms.md#transforms-custom-editschema)\.
   + **Additional connection options**: Enter additional key\-value pairs as needed to provide additional connection information or options\. 

   For an example, see the `README.md` file at [https://github\.com/aws\-samples/aws\-glue\-samples/blob/master/GlueCustomConnectors/development/Athena](https://github.com/aws-samples/aws-glue-samples/blob/master/GlueCustomConnectors/development/Athena)\. In the steps in this document, the sample code shows the minimal required connection options, which are `tableName`, `schemaName`, and `className`\. The code sample specifies these option as part of the `optionsMap` variable, but you can specify them for your connection and then use the connection\. 

------

1. After providing the required information, you can view the resulting data schema for your data source by choosing the **Output schema** tab in the node details panel\. The schema displayed on this tab is used by any child nodes that you add to the job graph\.

1. Continue creating your ETL job by adding transforms, additional data stores, and data targets, as described in [Editing ETL jobs in AWS Glue Studio](edit-nodes-chapter.md)\.

1. Customize the job run environment by configuring job properties as described in [Modify the job properties](managing-jobs-chapter.md#edit-jobs-properties)\.

1. Save and run the job\.

## Managing connectors and connections<a name="managing-connectors"></a>

You use the **Connectors** page in AWS Glue Studio to manage your connectors and connections\.

**Topics**
+ [Viewing connector and connection details](#connector-details)
+ [Editing connectors and connections](#editing-connectors)
+ [Cancel a subscription for a connector](#cancel-subscription)

### Viewing connector and connection details<a name="connector-details"></a>

You can view summary and detailed information for your connectors and connections\.

You can view summary information about your connectors and connections in the **Your connectors** and **Your connections** resource tables on the **Connectors** page\. To view detailed information, perform the following steps\.

1. In the AWS Glue Studio console, choose **Connectors** in the console navigation pane\.

1. Choose the connector or connection that you want to view detailed information for\.

1. Choose **Actions**, and then choose **View details** to open the detail page for that connector or connection\.

1. On the detail page, you can choose to **Edit** the connector or connection\.
   + For connectors, you can choose **Create connection** to create a new connection that uses the connector\.
   + For connections, you can choose **Create job** to create a job that uses the connection\.

### Editing connectors and connections<a name="editing-connectors"></a>

You use the **Connectors** page to change the information stored in your connectors and connections\.

1. In the AWS Glue Studio console, choose **Connectors** in the console navigation pane\.

1. Choose the connector or connection that you want to change\.

1. Choose **Actions**, and then choose **Edit**\.

   You can also choose **View details** and on the connector or connection detail page, you can choose **Edit**\.

1. On the **Edit connector** or **Edit connection** page, update the information, and then choose **Save**\.

### Cancel a subscription for a connector<a name="cancel-subscription"></a>

You can cancel your subscription in AWS Marketplace if you no longer need to use a connector\.

**Note**  
If you cancel your subscription to a connector, this does not remove the connector or connection from your account\. Any jobs that use the connector and related connections will no longer be able to use the connector and will fail\.   
Before you unsubscribe or re\-subscribe to a connector from AWS Marketplace, you should delete existing connections and connectors associated with that AWS Marketplace product\.

1. Sign in to the AWS Marketplace console at [https://console\.aws\.amazon\.com/marketplace](https://console.aws.amazon.com/marketplace)\.

1. Choose **Manage subscriptions**\.

1. On the **Manage subscriptions** page, choose **Manage** next to the connector subscription that you want to cancel\.

1. Choose **Actions** and then choose **Cancel subscription**\.

1. Select the check box to acknowledge that running instances are charged to your account, and then choose **Yes, cancel subscription**\.

## Developing custom connectors<a name="developing-custom-connectors"></a>

You can write the code that reads data from your data store and formats the data for use with AWS Glue Studio jobs\. You can create connectors for Spark, Athena, and JDBC data stores\. Sample code posted on GitHub provides an overview of the basic interfaces you need to implement\.

**Topics**
+ [Developing Spark connectors](#code-spark-connector)
+ [Developing Athena connectors](#code-athena-connector)
+ [Developing JDBC connectors](#code-jdbc-connector)
+ [Developing Glue Connectors for AWS Marketplace](#code-marketplace-connector)

### Developing Spark connectors<a name="code-spark-connector"></a>

You can create a Spark connector with Spark DataSource API V2 \(Spark 2\.4\) to read data\.

1. Configure a local development environment for creating your connector code\. You can use any IDE or even just a command line editor to write your connector\. 

   For example, you can configure a local Scala environment with a local AWS Glue ETL maven library, as described in [Developing Locally with Scala](https://docs.aws.amazon.com/glue/latest/dg/aws-glue-programming-etl-libraries.html#develop-local-scala) in the *AWS Glue Developer Guide*\.

1. Follow the steps in the AWS Glue GitHub sample library for developing Spark connectors, which is located at [https://github\.com/aws\-samples/aws\-glue\-samples/blob/master/GlueCustomConnectors/development/Spark/README\.md](https://github.com/aws-samples/aws-glue-samples/blob/master/GlueCustomConnectors/development/Spark/README.md)\.

### Developing Athena connectors<a name="code-athena-connector"></a>

You can create an Athena connector to be used by AWS Glue and AWS Glue Studio to query a custom data source\.

1. Configure a local development environment for creating your connector code\. You can use any IDE or even just a command line editor to write your connector\. 

   For example, you can use the instructions in the `README.md` file at [https://github\.com/aws\-samples/aws\-glue\-samples/blob/master/GlueCustomConnectors/development/GlueSparkRuntime/README\.md](https://github.com/aws-samples/aws-glue-samples/blob/master/GlueCustomConnectors/development/GlueSparkRuntime/README.md)\.

1. Follow the steps in the AWS Glue GitHub sample library for developing Athena connectors, which is located at [https://github\.com/aws\-samples/aws\-glue\-samples/blob/master/GlueCustomConnectors/development/Athena](https://github.com/aws-samples/aws-glue-samples/blob/master/GlueCustomConnectors/development/Athena)\.

### Developing JDBC connectors<a name="code-jdbc-connector"></a>

You can create a connector that uses JDBC to access your data stores\.

1. Configure a local development environment for creating your connector code\. You can use any IDE or even just a command line editor to write your connector\. 

1. Install the AWS Glue Spark runtime libraries in your local development environment\. Refer to the instructions in the AWS Glue GitHub sample library at [ https://github\.com/aws\-samples/aws\-glue\-samples/blob/master/GlueCustomConnectors/development/GlueSparkRuntime/README\.md](https://github.com/aws-samples/aws-glue-samples/blob/master/GlueCustomConnectors/development/GlueSparkRuntime/README.md)\.

1. Create an entry point that AWS Glue Studio uses to run the connector code\. When you add your connector using the AWS Glue Studio console, this is used as the value for **Class name**\.

1. Write the code that is responsible for retrieving the data from the data source\. This can include instructions on handling partitioned data or partitioning the read operations\.

   Use the `GlueContext` API to read data with the connector\. Users can add more input options in the AWS Glue Studio console to configure the connection to the data source, if necessary\. For a code example that shows how to read from and write to a JDBC database with a custom JDBC connector, see [Custom and AWS Marketplace connectionType values](https://docs.aws.amazon.com/glue/latest/dg/aws-glue-programming-etl-connect.html#aws-glue-programming-etl-connect-market)\.

### Developing Glue Connectors for AWS Marketplace<a name="code-marketplace-connector"></a>

As an AWS partner, you can create custom connectors and upload them to AWS Marketplace to sell to AWS Glue customers\.

The process for developing the connector code is the same as for custom connectors, but the process of uploading and verifying the connector code is more detailed\. Refer to the instructions on Github in the following location: [https://github\.com/aws\-samples/aws\-glue\-samples/blob/master/GlueCustomConnectors/marketplace/publishGuide\.pdf](https://github.com/aws-samples/aws-glue-samples/blob/master/GlueCustomConnectors/marketplace/publishGuide.pdf)