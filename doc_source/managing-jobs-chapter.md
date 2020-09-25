# Managing ETL jobs with AWS Glue Studio<a name="managing-jobs-chapter"></a>

You can use the simple graphical interface in AWS Glue Studio to manage your ETL jobs\.Using the navigation menu, choose **Jobs** to view the **Manage jobs** page\. On this page, you can see all the jobs that you have created either with AWS Glue Studio or the AWS Glue console\. You can view, manage, and run your jobs on this page\. 

**Topics**
+ [Start a job run](#start-jobs)
+ [Stop job runs](#stop-jobs)
+ [View your jobs](#view-jobs)
+ [View information for recent job runs](#view-job-run-details)
+ [View the job script](#view-job-script)
+ [Modify the job properties](#edit-jobs-properties)
+ [Save the job](#save-job)
+ [Clone a job](#clone-jobs)

## Start a job run<a name="start-jobs"></a>

In AWS Glue Studio, you run your jobs on demand\. A job can run multiple times, and each time you run the job, AWS Glue collects information about the job activities and performance\. This information is referred to as a *job run* and is identified by a job run ID\.

You can initiate a job run in  the following ways in AWS Glue Studio:
+ On the **Manage Jobs** page, choose the job you want to start, and then choose the **Run job** button\.
+ If you're viewing a job in the visual graph editor and the job has been saved, you can choose the **Run** button to start a job run\.

For more information about job runs, see [Working with Jobs on the AWS Glue Console](https://docs.aws.amazon.com/glue/latest/dg/console-jobs.html) in the *AWS Glue Developer Guide*\.

## Stop job runs<a name="stop-jobs"></a>

You can stop a job before it has completed its job run\. You might choose this option if you know that the job isn't configured correctly, or if the job is taking too long to complete\.

On the **Monitoring** page, in the **Job runs breakdown** list, choose the job that you want to stop, choose **Actions**, and then choose **Stop run**\. 

## View your jobs<a name="view-jobs"></a>

You can view all your jobs on the **Manage jobs** page\. You can access this page by choosing **Jobs** in the navigation pane\.

On the **Manage jobs** page, you can see all the jobs that were created in your account\. The **Your jobs** list shows the job name, its type, the status of the last run of that job, and the dates on which the job was created and last modified\. You can choose the name of a job to see detailed information for that job\.

You can also use the Monitoring dashboard to view all your jobs\. You can access the dashboard by choosing **Monitoring** in the navigation pane\. For more information about using the dashboard, see [Monitoring ETL jobs in AWS Glue Studio](monitoring-chapter.md)\.

### Customize the job display<a name="view-jobs-customize"></a>

You can customize how the jobs are displayed in the **Your jobs** section of the **Manage jobs** page\. Also, you can enter text in the search text field to display only jobs with a name that contains that text\.

If you click on the settings icon ![\[\]](http://docs.aws.amazon.com/glue/latest/ug/images/manage-console-icon-settings.png) in the **Your jobs** section, you can customize how AWS Glue Studio displays the information in the table\. You can choose to wrap the lines of text in the display, change the number of jobs displayed on the page, and specify which columns to display\.

## View information for recent job runs<a name="view-job-run-details"></a>

A job can run multiple times as new data is added at the source location\. Each time a job runs, the job run is assigned a unique ID, and information about that job run is collected\. You can view this information by using any of the following methods:
+ If you created a job using the visual graph editor and then chose the **Run** button on that page, you can choose either the link in the notification message for **View runs** or the **Run details** tab to view the job run information\.
+ In the navigation pane, choose **Jobs**, and then choose the name of the job you want to review in the **Your jobs** list\. This opens the job in the visual job editor\. Choose the **Run details** tab to view the job run information\.
+ In the navigation pane, choose **Monitoring**\. Scroll down to the **Job runs breakdown** list\. Choose the job and then choose **View run details**\.

The information displayed on the job run detail page includes:
+ Job run ID
+ Number of attempts to run this job
+ Status of the job run
+ Start and end time for the job run
+ The runtime for the job run
+ A link to the job log files
+ A link to the job error log files
+ The error returned for failed jobs

For more information about the job logs, see [Viewing the job run logs](monitoring-chapter.md#monitoring-job-run-logs)\.

## View the job script<a name="view-job-script"></a>

After you provide information for all the nodes in the graph, AWS Glue Studio generates a script that is used by the job to read the data from the source, transform the data, and write the data in the target location\. If you save the job, you can view this script at any time\.

1. Choose **Jobs** in the navigation pane\.

1. On the **Manage Jobs** page, in the **Your Jobs** list, choose the name of the job you want to review\.

1. On the visual graph editing page, choose the **Script** tab at the top of the graph editing pane to view the job script\. 

   You can only view the generated script–you can't edit it\.

## Modify the job properties<a name="edit-jobs-properties"></a>

The nodes in the graph define the actions performed by the job, but there are several properties that you can configure for the job as well\. These properties determine the environment that the job runs in, the resources it uses, the threshold settings, the security settings, and more\.

1. Choose **Jobs** in the navigation pane\.

1. On the **Manage Jobs** page, in the **Your Jobs** list, choose the name of the job you want to review\.

1. On the visual graph editing page, choose the **Job details** tab at the top of the job graph editing pane\. 

1. Modify the job properties, as needed\. 

   For more information about the job properties, see [Defining Job Properties](https://docs.aws.amazon.com/glue/latest/dg/add-job.html#create-job) in the *AWS Glue Developer Guide*\. 

1. Expand the **Advanced properties** section if you need to specify these additional job properties:
   + **Delay notification threshold \(minutes\)**–Specify a delay threshold for the job\. If the job runs for a longer time than that specified by the threshold, then AWS Glue sends a delay notification for the job to Amazon CloudWatch\.
   + **Security configuration** and **Server\-side encryption**–Use these fields to choose the encryption options for the job\.
   + **Python library path**, **Dependent jars path**, or **Referenced files path**–Use these fields to specify the location of additional files used by the job when executing the script\.
   + **Job Parameters**–You can add a set of key\-value pairs that are passed as named parameters to the job script\. In Python calls to AWS Glue APIs, it's best to pass parameters explicitly by name\. For more information about using parameters in a job script, see [Passing and Accessing Python Parameters in AWS Glue](https://docs.aws.amazon.com/glue/latest/dg/aws-glue-programming-python-calling.html#aws-glue-programming-python-calling-parameters) in the *AWS Glue Developer Guide*\. 
   + **Tags**–You can add tags to the job to help you organize and identify them\.

1. After you have modified the job properties, save the job\.

## Save the job<a name="save-job"></a>

A red **Job has not been saved** callout is displayed to the left of the **Save** button until you save the job\. 

![\[A red oval with the label "Job has not been saved" to the left of the Save button.\]](http://docs.aws.amazon.com/glue/latest/ug/images/edit-graph-callout-not-saved_GA.png)

You must provide all the required information before you can choose the **Save** button to save your job\. After you save the job, the callout changes to display the time that the job was last saved\.

If you exit AWS Glue Studio before saving your job, the next time you sign in to AWS Glue Studio, a notification appears\. The notification indicates that there is an unsaved job, and asks if you want to restore it\. You can either restore the job and continue to edit it, or create a new job\.

### Troubleshooting errors when saving a job<a name="save-job-troubleshooting"></a>

If you choose the **Save** button, but your job is missing some information, then a red callout appears on the tab where the information is missing\.

![\[A screenshot showing the tabs for the visual graph editor pane with a callout labeled 1 on the Visual tab.\]](http://docs.aws.amazon.com/glue/latest/ug/images/screenshot-save-job-error-in-graph-GA.png)
+ If a node in the graph isn't configured correctly, the **Visual** tab shows a red callout, and the node with the error displays a warning symbol ![\[A red triangle with an exclamation point in the center\]](http://docs.aws.amazon.com/glue/latest/ug/images/edit-graph-warning_icon.png)\.

  1. Choose the node\. In the node details panel, a red callout appears on the tab where the missing or incorrect information is located\.   
![\[A screenshot showing the tabs for the node details panel with a callout labeled 1 on the Transform tab.\]](http://docs.aws.amazon.com/glue/latest/ug/images/screenshot-node-detail-error-callout.png)

  1. Choose the tab in the node details panel that shows a red callout, and then locate the problem fields, which are highlighted\. An error message below the fields provides additional information about the problem\.
+ If the problem is a missing node in the graph, the **Visual** tab shows a red callout and the area to the right of the graph, where the node details panel is displayed, shows a message indicating the problem\.
+ If there is a problem with the job properties, the **Job details** tab shows a red callout\. Choose the **Job details** tab and locate the problem fields, which are highlighted\. An error message below the fields provides additional information about the problem\.

## Clone a job<a name="clone-jobs"></a>

You can use the Clone action to copy an existing job into a new job\.

1. On the **Manage jobs** page, in the **Your jobs** list, choose the job that you want to duplicate\.

1. From the **Actions** menu, choose **Clone job**\. 

1. Enter a name for the new job\. You can then save or edit the job\.