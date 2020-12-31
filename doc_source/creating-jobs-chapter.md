# Creating ETL jobs with AWS Glue Studio<a name="creating-jobs-chapter"></a>

You can use the simple graphical interface in AWS Glue Studio to create your ETL jobs\. You use the **Manage jobs** page to create new jobs\. 

On the **Manage jobs** page, you can see all the jobs that you have created either with AWS Glue Studio or the AWS Glue console\. You can view, manage, and run your jobs on this page\. 

**Topics**
+ [Start the job creation process](#create-jobs-start)
+ [Create jobs that use a connector](#create-jobs-connector)
+ [Next steps for creating a job in AWS Glue Studio](#create-jobs-guiedit)

## Start the job creation process<a name="create-jobs-start"></a>

You use the visual graph editor to create and customize your jobs\. When you create a new job, you have the option of starting with an empty canvas, a job graph with only a source node, or a job graph with a data source, transform, and data target node\.

1. Access the **Manage jobs** page\. You can either choose **Create and manage jobs** from the AWS Glue Studio landing page, or you can choose **Jobs** from the navigation pane\.

1. In the **Create job** section, choose a configuration option for your job\.
   + To create a job starting with an empty canvas, choose **Blank graph**\.
   + To create a job starting with source node, or with a source, transform and target node, choose **Source and target added to the graph**\.

     You then choose the data source type\. You can also choose the data target type, or you can choose the **Choose later** option to start with only a data source node in the graph\.

     The data target can be either Amazon S3 or the AWS Glue Data Catalog\. 

     For more information about creating tables in the Data Catalog, see [Defining Tables in the AWS Glue Data Catalog](https://docs.aws.amazon.com/glue/latest/dg/tables-described.html) in the *AWS Glue Developer Guide*\.

1. Choose **Create** to open the visual job editor\.

## Create jobs that use a connector<a name="create-jobs-connector"></a>

After you have added a connector to AWS Glue Studio and created a connection for that connector, you can create a job that uses the connection for the data source\.

For detailed instructions, see [Authoring jobs with custom connectors](connectors-chapter.md#job-authoring-custom-connectors)\.

## Next steps for creating a job in AWS Glue Studio<a name="create-jobs-guiedit"></a>

You use the visual job editor to configure nodes in the graph for your job\. Each node represents an action, such as reading data from the source location or applying a transform to the data\. Each node you add to your job graph has properties that provide information about either the data location or the transform\.

The next steps for creating and managing your jobs are:
+ [Editing ETL jobs in AWS Glue Studio](edit-nodes-chapter.md)
+ [View the job script](managing-jobs-chapter.md#view-job-script)
+ [Modify the job properties](managing-jobs-chapter.md#edit-jobs-properties)
+ [Save the job](managing-jobs-chapter.md#save-job)
+ [Start a job run](managing-jobs-chapter.md#start-jobs)
+ [View information for recent job runs](managing-jobs-chapter.md#view-job-run-details)
+ [Accessing the job monitoring dashboard](monitoring-chapter.md#monitoring-accessing-dashboard)