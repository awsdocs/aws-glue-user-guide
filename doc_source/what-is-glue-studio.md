# What is AWS Glue Studio?<a name="what-is-glue-studio"></a>

AWS Glue Studio is a new graphical interface that makes it easy to create, run, and monitor extract, transform, and load \(ETL\) jobs in AWS Glue\. You can visually compose data transformation workflows and seamlessly run them on AWS Glue’s Apache Spark\-based serverless ETL engine\. You can inspect the schema and data results in each step of the job\.

![\[\]](http://docs.aws.amazon.com/glue/latest/ug/images/screenshot-legislator-job-in-editor3.png)

AWS Glue Studio is designed not only for tabular data, but also for semi\-structured data, which is difficult to render in spreadsheet\-like data preparation interfaces\. Examples of semi\-structured data include application logs, mobile events, Internet of Things \(IoT\) event streams, and social feeds\. 

When creating a job in AWS Glue Studio, you can choose from a variety of data sources that are stored in AWS services\. You can quickly prepare that data for analysis in data warehouses and data lakes\. AWS Glue Studio also offers tools to monitor ETL workflows and validate that they are operating as intended\. You can preview the dataset for each node\. This helps you to debug your ETL jobs by displaying a sample of the data at each step of the job\.

AWS Glue Studio provides a visual interface that makes it easy to:
+ Pull data from an Amazon S3, Amazon Kinesis, or JDBC source\.
+ Configure a transformation that joins, samples, or transforms the data\.
+ Specify a target location for the transformed data\.
+ View the schema or a sample of the dataset at each point in the job\.
+ Run, monitor, and manage the jobs created in AWS Glue Studio\.

## Features of AWS Glue Studio<a name="glue-studio-feature-overview"></a>

AWS Glue Studio helps you to create and manage jobs that gather, transform, and clean data\. Advanced users can use AWS Glue Studio to troubleshoot and edit job scripts\.

### Visual job editor<a name="features-visual-editor"></a>

You can perform the following actions when creating and editing jobs in AWS Glue Studio:
+ Add additional nodes to the job to implement:
  + Multiple data sources\.
  + Multiple data targets\.
  + Data sources and targets that use connectors for external data stores that were not previously supported
+ View a sample of the data at each node in the job diagram\.
+ Change the parent nodes for an existing node\.
+ Add transforms that:
  + Join data sources\.
  + Select specific fields from the data\.
  + Drop fields\.
  + Rename fields\.
  + Change the data type of fields\.
  + Write select fields from the data into a JSON file in an Amazon S3 bucket \(spigot\)\.
  + Filter out data from a dataset\.
  + Split a dataset into two datasets\.
  + Find missing values in a dataset and provide the missing value in a separate column\.
  + Use SQL to query and transform the data\.
  + Use custom code\.

### Job performance dashboard<a name="features-job-monitoring"></a>

AWS Glue Studio provides a comprehensive run dashboard for your ETL jobs\. The dashboard displays information about job runs from a specific time frame\. The information displayed on the dashboard includes:
+ Jobs overview summary – A high\-level overview showing total jobs, current runs, completed runs, and failed jobs\.
+ Status summaries – Provides high level job metrics based on job properties, such as worker type and job type\.
+ Job runs time line – A bar graph summary of successful, failed, and total runs for the currently selected time frame\.
+ Job run breakdown – A detailed list of job runs from the selected time frame\.

### Support for dataset partitioning<a name="features-partitioning"></a>

You can use AWS Glue Studio to efficiently process partitioned datasets\. You can load, filter, transform, and save your partitioned data by using SQL expressions or user\-defined functions–to avoid listing and reading unnecessary data from Amazon S3\.

## When should I use AWS Glue Studio?<a name="when-to-use-glue"></a>

**Use AWS Glue Studio for a simple visual interface to create ETL workflows for data cleaning and transformation, and run them on AWS Glue\.**

AWS Glue Studio makes it easy for ETL developers to create repeatable processes to move and transform large\-scale, semi\-structured datasets, and load them into data lakes and data warehouses\. It provides a boxes\-and\-arrows style visual interface for developing and managing AWS Glue ETL workflows that you can optionally customize with code\. AWS Glue Studio combines the ease of use of traditional ETL tools, and the power and flexibility of AWS Glue’s big data processing engine\.

AWS Glue Studio provides multiple ways to customize your ETL scripts,including adding nodes that represent code snippets in the visual editor\. 

**Use AWS Glue Studio for easier job management\.** AWS Glue Studio provides you with job and job run management interfaces that make it clear how jobs relate to each other, and give an overall picture of your job runs\. The job management page makes it easy to do bulk operations on jobs \(previously difficult to do in the AWS Glue console\)\. All job runs are available in a single interface where you can search and filter\. This gives you a constantly updated view of your ETL operations and the resources you use\. You can use the real\-time dashboard in AWS Glue Studio to monitor your job runs and validate that they are operating as intended\. 

## Accessing AWS Glue Studio<a name="acessing-glue-studio"></a>

To access AWS Glue Studio, sign in to AWS as a user that has the required permissions, as described in [Set up IAM permissions for AWS Glue Studio](setting-up.md#getting-started-iam-permissions)\. Then you can sign in to the AWS Management Console and open the AWS Glue console at [https://console\.aws\.amazon\.com/glue/](https://console.aws.amazon.com/glue/)\. Click the **AWS Glue Studio** link in the navigation pane\.

## Pricing for AWS Glue Studio<a name="pricing-for-glue-studio"></a>

When using AWS Glue Studio, you are charged for data previews\. After you specify an IAM role for the job, the visual editor starts an Apache Spark session for sampling your source data and executing transformations\. This session runs for 30 minutes and then turns off automatically\. AWS charges you for 2 DPUs at the development endpoint rate \(DEVED\-DPU\-Hour\), typically resulting in a charge of $0\.44 for each 30 minute session\. The rate might vary for each region\. At the end of the 30 minute session, you can choose **Retry** on the **Data preview** tab for any node or reload the visual editor page to start a new 30 minute session at the same rates\. 

You also pay for the underlying AWS services that your jobs use or interact with–for example, AWS Glue, your data sources, and your data targets\. For pricing information, see [AWS Glue Pricing](https://aws.amazon.com/glue/pricing)\.