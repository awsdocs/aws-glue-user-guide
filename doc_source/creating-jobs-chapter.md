# Creating ETL jobs with AWS Glue Studio<a name="creating-jobs-chapter"></a>

You can use the simple visual interface in AWS Glue Studio to create your ETL jobs\. You use the **Jobs** page to create new jobs\. 

On the **Jobs** page, you can see all the jobs that you have created either with AWS Glue Studio or AWS Glue\. You can view, manage, and run your jobs on this page\. 

**Topics**
+ [Start the job creation process](#create-jobs-start)
+ [Create jobs that use a connector](#create-jobs-connector)
+ [Next steps for creating a job in AWS Glue Studio](#create-jobs-next)

## Start the job creation process<a name="create-jobs-start"></a>

You use the visual editor to create and customize your jobs\. When you create a new job, you have the option of starting with an empty canvas, a job with a data source, transform, and data target node, or writing an ETL script\.

**To create a job in AWS Glue Studio**

1. Sign in to the AWS Management Console and open the AWS Glue Studio console at [https://console\.aws\.amazon\.com/gluestudio/](https://console.aws.amazon.com/gluestudio/)\.

1. You can either choose **Create and manage jobs** from the AWS Glue Studio landing page, or you can choose **Jobs** from the navigation pane\.

   The **Jobs** page appears\.

1. In the **Create job** section, choose a configuration option for your job\.
   + To create a job starting with an empty canvas, choose **Blank graph**\.
   + To create a job starting with source node, or with a source, transform and target node, choose **Source and target added to the graph**\.

     You then choose the data source type\. You can also choose the data target type, or you can choose the **Choose later** option to start with only a data source node in the graph\.
   + For those familiar with programming and writing ETL scripts, you can choose **Code editor** to create a new job\. You then have the option of writing code in a code editor window, or uploading an existing script from a local file\. If you choose to use the code editor, then you can't use the visual job editor\.

1. Choose **Create** to open the visual job editor\.  
![\[\]](http://docs.aws.amazon.com/glue/latest/ug/images/create-job-data-sources-screenshot2.png)

## Create jobs that use a connector<a name="create-jobs-connector"></a>

After you have added a connector to AWS Glue Studio and created a connection for that connector, you can create a job that uses the connection for the data source\.

For detailed instructions, see [Authoring jobs with custom connectors](connectors-chapter.md#job-authoring-custom-connectors)\.

## Next steps for creating a job in AWS Glue Studio<a name="create-jobs-next"></a>

You use the visual job editor to configure nodes for your job\. Each node represents an action, such as reading data from the source location or applying a transform to the data\. Each node you add to your job has properties that provide information about either the data location or the transform\.

The next steps for creating and managing your jobs are:
+ [Editing ETL jobs in AWS Glue Studio](edit-nodes-chapter.md)
+ [Adding connectors to AWS Glue Studio](connectors-chapter.md#creating-connectors)
+ [View the job script](managing-jobs-chapter.md#view-job-script)
+ [Modify the job properties](managing-jobs-chapter.md#edit-jobs-properties)
+ [Save the job](managing-jobs-chapter.md#save-job)
+ [Start a job run](managing-jobs-chapter.md#start-jobs)
+ [View information for recent job runs](managing-jobs-chapter.md#view-job-run-details)
+ [Accessing the job monitoring dashboard](monitoring-chapter.md#monitoring-accessing-dashboard)