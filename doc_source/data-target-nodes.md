# Configuring data target nodes<a name="data-target-nodes"></a>

The data target is where the job writes the transformed data\. 

## Overview of data target options<a name="edit-jobs-target-overview"></a>

Your data target \(also called a data sink\) can be:
+ Amazon S3 – The job writes the data in a file in the specified Amazon S3 location in the format you specify\.

  If you configure partition columns for the data target, then the job writes the dataset to Amazon S3 into directories based on the partition key\.
+ AWS Glue Data Catalog – The job uses the information associated with the table in the Data Catalog to write the output data to a target location\. 

  You can create the table manually or with the crawler\. You can also use AWS CloudFormation templates to create tables in the Data Catalog\. 

  If the job requires a connection to access your target location, the name of the connection is associated with the table in the Data Catalog\. 

  For more information about creating tables in the Data Catalog, see [Defining Tables in the AWS Glue Data Catalog](https://docs.aws.amazon.com/glue/latest/dg/tables-described.html) in the *AWS Glue Developer Guide*\.

## Editing the data target node<a name="edit-jobs-target"></a>

The data target is where the job writes the transformed data\. 

Perform the following steps to configure a data target node:

1. Choose a data target node in the graph\. When you choose a node, the node details panel appears on the right\-side of the page\.

1. Make sure the **Node properties** tab is selected in the node details panel, then enter the following information:
   + **Name**: Enter a name to associate with the node in the job graph\.
   + **Node  type**: Choose the destination type for the data\.
     + If you choose **S3** for the target, then the job writes the dataset to one or more files in the Amazon S3 location you specify\.
     + If you choose **AWS Glue Data Catalog** for the target, then the job writes to a location described by the table selected from the Data Catalog\.
   + **Node parents**: The parent node is the node in the graph that provides the output data you want to write to the target location\. For a pre\-populated graph, the target node should already have the parent node selected\. If there is no parent node displayed, then choose a parent node from the list\. 

     A target node has a single parent node\.

1. Choose the **Data target properties** tab in the node details panel and enter the target output properties\.

   1. If you chose **S3** for the target type, then enter the following information\.
      + **Format**: Choose a format from the list\. The available format types for the data results are:
        + **JSON**: JavaScript Object Notation\. 
        + **CVS**: Comma\-separated values\. 
        + **Avro**: Apache Avro JSON binary\. 
        + **Parquet**: Apache **Parquet** columnar storage\. 
        + **Glue Parquet**: A custom Parquet writer type that is optimized for `DynamicFrames` as the data format\. Instead of requiring a precomputed schema for the data, Glue Parquet computes and modifies the schema dynamically\.
        + **ORC**: Apache Optimized Row Columnar \(ORC\) format\. 

        To learn more about these format options, see [Format Options for ETL Inputs and Outputs in AWS Glue](https://docs.aws.amazon.com/glue/latest/dg/aws-glue-programming-etl-format.html) in the *AWS Glue Developer Guide*\.
      + **Compression Type**: You can choose to optionally compress the data using either the `gzip` or `bzip2` format\. The default is no compression, or **None**\.
      + **S3 Target Location**: The Amazon S3 bucket and location for the data output\. You can choose the **Browse S3** button to see the Amazon S3 buckets that you have access to and choose one as the target destination\. 
      + **Partition**: Choose which columns to use as partitioning keys in the output\. To add more partition keys, choose **Add a partition key**\.

   1. If you chose **AWS Glue Data Catalog** for the target type, then enter the following information:
      + **Database**: Choose the database that contains the table you want to use as the target from the list\. This database must already exist in the Data Catalog\.
      + **Table**: Choose the table that defines the schema of your output data from the list\. This table must already exist in the Data Catalog\.

        A table in the Data Catalog consists of the names of columns, data type definitions, partition information, and other metadata about the target dataset\. Your job writes to a location described by this table in the Data Catalog\.

        For more information about creating tables in the Data Catalog, see [Defining Tables in the AWS Glue Data Catalog](https://docs.aws.amazon.com/glue/latest/dg/tables-described.html) in the *AWS Glue Developer Guide*\.