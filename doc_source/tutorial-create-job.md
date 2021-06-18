# Tutorial: Getting started with AWS Glue Studio<a name="tutorial-create-job"></a>

You can use AWS Glue Studio to create jobs that extract structured or semi\-structured data from a data source, perform a transformation of that data, and save the result set in a data target\.

**Topics**
+ [Prerequisites](#tutorial-create-job-prereq)
+ [Step 1: Start the job creation process](#tutorial-create-job-step1)
+ [Step 2: Edit the data source node in the job diagram](#tutorial-create-job-step2)
+ [Step 3: Edit the transform node of the job](#tutorial-create-job-step3)
+ [Step 4: Edit the data target node of the job](#tutorial-create-job-step4)
+ [Step 5: View the job script](#tutorial-create-job-view-script)
+ [Step 6: Specify the job details and save the job](#tutorial-create-job-details)
+ [Step 7: Run the job](#tutorial-create-job-run-job)
+ [Next steps](#tutorial-next-steps)

## Prerequisites<a name="tutorial-create-job-prereq"></a>

This tutorial has the following prerequisites:
+ You have an AWS account\.
+ You have access to AWS Glue Studio\.
+ Your account has all the necessary permissions for creating and running a job for an Amazon S3 data source and data target\. 
+ You have created an AWS Identity and Access Management role for the job to use\. You can also choose an IAM role for the job that includes permissions for all your data sources, data targets, temporary directory, scripts, and any libraries used by the job\.
+ The following components exist in AWS:
  + The `Flights Data Crawler` crawler
  + The `flights-db` database
  + The `flightscsv` table
  + The IAM role `AWSGlueServiceRole-CrawlerTutorial`

  To create these components, you can complete the service tutorial **Add a crawler**, which populates the AWS Glue Data Catalog with the necessary objects\. This tutorial also creates an IAM role with the necessary permissions\. You can find the tutorial on the AWS Glue service page at [https://console\.aws\.amazon\.com/glue/](https://console.aws.amazon.com/glue/)\. The tutorial is located in the left\-side navigation, under **Tutorials**\. Alternatively, you can use the documentation version of this tutorial, [Tutorial: Adding an AWS Glue crawler](tutorial-add-crawler.md)\.

## Step 1: Start the job creation process<a name="tutorial-create-job-step1"></a>

In this task, you choose to start the job creation by using a template\. 

**To create a job, starting with a template**

1. Sign in to the AWS Management Console and open the AWS Glue Studio console at [https://console\.aws\.amazon\.com/gluestudio/](https://console.aws.amazon.com/gluestudio/)\.

1. On the AWS Glue Studio landing page, choose **View jobs** under the heading **Create and manage jobs**\.

1. On the **Jobs** page, under the heading **Create job**, choose the **Source and target added to the graph** option\. Then, choose **S3** for the **Source** and **S3** for the **Target**\.

1. Choose the **Create** button to start the job creation process\.

The job editing page opens with a simple three\-node job diagram displayed\.

## Step 2: Edit the data source node in the job diagram<a name="tutorial-create-job-step2"></a>

Choose the **Data source \- S3 bucket** node in the job diagram to edit the data source properties\.

**To edit the data source node**

1. On the **Node properties** tab in the node details pane, for **Name**, enter a name that is unique for this job\. 

   The value you enter is used as the label for the data source node in the job diagram\. If you use unique names for the nodes in your job, then it's easier to identify each node in the job diagram, and also to select parent nodes\. For this tutorial, enter the name **S3 Flight Data**\.

1. Choose the **Data source properties \- S3** tab in the node details panel\.

1. Choose the **Data Catalog table** option for the S3 source type\.

1. For **Database**, choose the **flights\-db** database from the list of available databases in your AWS Glue Data Catalog\.

1. For **Table**, enter **flight** in the search field, and then choose the **flightscsv** table from your AWS Glue Data Catalog\.

1. \(Optional\) Choose the **Output schema** tab in the node details panel to view the data schema\.

1. \(Optional\) After configuring the node properties and data source properties, you can preview the dataset from your data source by choosing the **Data preview** tab in the node details panel\. The first time you choose this tab for any node in your job, you are prompted to provide an IAM role to access the data\. There is a cost associated with using this feature, and billing starts as soon as you provide an IAM role\.

   By default, the first 5 columns are selected for viewing in the **Data preview** tab\. To view other columns, choose **Previewing 5 of 65 fields**\. For example, you can deselect the first 5 columns and select `fl_date`, `airline_id`, `fl_num`, `tail_num`, and `origin_airport_id`\. Scroll to the end of the column list and choose **Confirm** to save your choices\.

After you have provided the required information for the data source node, a green check mark appears on the node in the job diagram\.

## Step 3: Edit the transform node of the job<a name="tutorial-create-job-step3"></a>

The transform node is where you specify how you want to modify the data from its original format\. An *ApplyMapping* transform enables you to rename data property keys, change the data types, and drop columns from the dataset\.

When you edit the **Transform \- ApplyMapping** node, the original schema for your data is shown in the **Source key** column in the node details panel\. This is the data property key name \(column name\) that is obtained from the source data and stored in the table in the AWS Glue Data Catalog\.

The **Target key** column shows the key name that will appear in the data target\. You can use this field to change the data property key name in the output\. The **Data type** column shows the data type of the key and allows you to change it to different data type for the target\. The **Drop** column contains a check box\. This box allows you to choose a field to drop it from the target schema\.

**To edit the transform node**

1. Choose the **Transform \- ApplyMapping** node in the job diagram to edit the data transformation properties\.

1. In the node details panel, on the **Node properties** tab, review the information\. 

   You can change the name of this node if you want\.

1. Choose the **Transform** tab in the node details panel\.

1. Choose to drop the keys `quarter` and `day_of_week` by selecting the check box in the **Drop** column for each key\. 

1. For the key that shows `day_of_month` in the **Source key** column, change the **Target key** value to `day`\. 

   Change the data type for the `month` and `day` keys to **tinyint**\. The `tinyint` data type stores integers using 1 byte of storage, with a range of values from 0 to 255\. When changing the data type, you must verify that the data type is supported by your target\.

1. \(Optional\) Choose the **Output schema** tab in the node details panel to view the modified schema\.

1. \(Optional\) After configuring the node properties and transform properties, you can preview the modified dataset by choosing the **Data preview** tab in the node details panel\. The first time you choose this tab for any node in your job, you are prompted to provide an IAM role to access the data\. There is a cost associated with using this feature, and billing starts as soon as you provide an IAM role\.

    By default, the first 5 columns are selected for the data preview, but the columns are no longer the same as the columns viewed on the data source node because we dropped two of the columns and renamed a third column\.

Notice that the **Transform \- Apply Mapping** node in the job diagram now has a green check mark, indicating that the node has been edited and has all the required information\. 

## Step 4: Edit the data target node of the job<a name="tutorial-create-job-step4"></a>

A data target node determines where the transformed output is sent\. The location can be an Amazon S3 bucket, a Data Catalog table, or a connector and connection\. If you choose a Data Catalog table, the data is written to the location associated with that table\. For example, if you use a crawler to create a table in the Data Catalog for a JDBC target, the data is written to that JDBC table\.

**To edit the data target node**

1. Choose the **Data target \- S3 bucket** node in the job diagram to edit the data target properties\.

1. In the node details panel on the right, choose the **Node properties** tab\. For **Name**, enter a unique name for the node, such as **Revised Flight Data**\.

1. Choose the **Data target properties \- S3** tab\. 

1. For **Format**, choose **JSON**\. 

   For **Compression Type**, keep the default value of **None**\.

   For the **S3 Target Location**, choose the **Browse S3** button to see the Amazon S3 buckets that you have access to, and choose one as the target destination\.

   For the **Data Catalog update options**, keep the default setting of **Do not update the Data Catalog**\.

   For more information about the available options, see [Overview of data target options](data-target-nodes.md#edit-jobs-target-overview)\.

## Step 5: View the job script<a name="tutorial-create-job-view-script"></a>

After you configure all the nodes in the job, AWS Glue Studio generates a script that is used by the job to read, transform, and write the data in the target location\. 

To view the script, choose the **Script** tab at the top of the job editing pane\. Don’t click the **Edit script** button, because this will take you out of visual editor mode\.

If you clicked the **Edit script** button and confirmed your choice, you can reload the page \(without saving the job first\), to reset the **Script** tab\.

## Step 6: Specify the job details and save the job<a name="tutorial-create-job-details"></a>

Before you can save and run your extract, transform, and load \(ETL\) job, you must first enter additional information about the job itself\.

**To specify the job details and save the job**

1. Choose the **Job details** tab\. 

1. Enter a name for the job–for example **FlightDataETL**\. Provide a UTF\-8 string with a maximum length of 255 characters\. 

   You can optionally enter a description of the job\.

1. For the **IAM role**, choose `AWSGlueServiceRole-CrawlerTutorial` from the list of available roles\. You might have to add access to the target Amazon S3 bucket to this role\.

   If you have many roles to choose from, you can start entering part of the role name in the **IAM role** search field, and the roles with the matching text string will be displayed\. For example, you can enter **tutorial** in the search field to find all roles with `tutorial` \(case\-insensitive\) in the name\. 

   The AWS Identity and Access Management \(IAM\) role is used to authorize access to resources that are used to run the job\. You can only choose roles that already exist in your account\. The role you choose must have permission to access your Amazon S3 sources, targets, temporary directory, scripts, and any libraries used by the job, as well as access to AWS Glue service resources\.

   For the steps to create a role, see [Create an IAM Role for AWS Glue](https://docs.aws.amazon.com/glue/latest/dg/create-an-iam-role.html) in the *AWS Glue Developer Guide*\.

1. For the remaining fields, use the default values\.

1. Choose **Save** in the top\-right corner of the page\.

   You should see a notification at the top of the page that the job was successfully saved\.

If you don't see a notification that your job was successfully saved, then there is most likely information missing that prevents the job from being saved\.
+ Review the job in the visual editor, and choose any node that doesn't have a green check mark\. 
+ If any of the tabs above the visual editor pane have a callout, choose that tab and look for any fields that are highlighted in red\.

## Step 7: Run the job<a name="tutorial-create-job-run-job"></a>

Now that the job has been saved, you can run the job\. Choose the **Run** button at the top of the page\. You should then see a notification that the job was successfully started\. 

You can choose either the link in the notification for **Run Details**, or choose the **Runs** tab to view the run status of the job\. 

On the **Runs** tab, there is a card for each recent run of the job with information about that job run\.

For more information about the job run information, see [View information for recent job runs](managing-jobs-chapter.md#view-job-run-details)\.

## Next steps<a name="tutorial-next-steps"></a>

After you start the job run, you might want to try some of the following tasks: 
+ View the job monitoring dashboard – [Accessing the job monitoring dashboard](monitoring-chapter.md#monitoring-accessing-dashboard)\.
+ Try a different transform on the data – [Overview of mappings and transforms](edit-jobs-transforms.md#transforms_overview)\.
+ View the jobs that exist in your account – [View your jobs](managing-jobs-chapter.md#view-jobs)\.
+ Run the job using a time\-based schedule – [Schedule job runs](managing-jobs-chapter.md#schedule-jobs)\.