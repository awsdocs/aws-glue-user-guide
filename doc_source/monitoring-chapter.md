# Monitoring ETL jobs in AWS Glue Studio<a name="monitoring-chapter"></a>

Monitoring is an important part of maintaining the reliability, availability, and performance of ETL jobs used in AWS Glue and AWS Glue Studio\. You should collect monitoring data from all of the parts of your AWS solution so that you can more easily debug a multipoint failure if one occurs\. 

**Topics**
+ [Accessing the job monitoring dashboard](#monitoring-accessing-dashboard)
+ [Overview of the job monitoring dashboard](#monitoring-dashboard-overview)
+ [Job runs breakdown](#monitoring-job-breakdown)
+ [Viewing the job run logs](#monitoring-job-run-logs)
+ [Viewing the details of a job run](#monitoring-job-run-details)
+ [Viewing Amazon CloudWatch metrics for a job run](#monitoring-job-run-metrics)

## Accessing the job monitoring dashboard<a name="monitoring-accessing-dashboard"></a>

You access the job monitoring dashboard by choosing the **Monitoring** link in the AWS Glue Studio navigation pane\.

## Overview of the job monitoring dashboard<a name="monitoring-dashboard-overview"></a>

The job monitoring dashboard provides an overall summary of the job runs, with totals for the jobs with a status of **Running**, **Canceled**, **Success**, or **Failed**\. Additional tiles provide the overall job success rate, the estimated DPU usage for jobs, a breakdown of the job status counts by job type, worker type, and by day\. 

The graphs in the tiles are interactive\. You can choose any block in a graph to run a filter that displays only those jobs in the **Job runs breakdown** table at the bottom of the page\.

You can change the date range for the information displayed on this page by using the date range selector\. When you change the date range, the information tiles adjust to show the values for the specified number of days before the current date\. You can also use a specific date range if you choose **Custom** from the date range selector\. 

## Job runs breakdown<a name="monitoring-job-breakdown"></a>

The **Job runs breakdown** resource list shows the jobs for the specified date range and filters\.

You can filter the jobs on additional criteria, such as status, worker type, job type, and the job name\. In the filter box at the top of the table, you can enter the text to use as a filter\. The table results are updated with rows that contain matching text as you enter the text\.

You can view a subset of the jobs by choosing elements from the graphs on the job monitoring dashboard\. For example, if you choose the number of running jobs in the **Job runs summary** tile, then the **Job runs breakdown** list displays only the jobs that currently have a status of `Running`\. If you choose one of the bars in the **Worker type breakdown** bar chart, then only job runs with the matching worker type and status are shown in the **Job runs breakdown** list\.

The **Job runs breakdown** resource list displays the details for the job runs\. You can sort the rows in the table by choosing a column heading\. 

You can choose any job run in the list and view additional information\. Choose a job run, and then do one of the following:
+ Choose the **Actions** menu and the **View logs** option to view the job run logs for that job\. 
+ Choose the **Actions** menu and the **View job** option to view the job in the visual graph editor\.
+ Choose the **Actions** menu and the **Stop run** option to stop the current run of the job\.
+ Choose **View run details** to view the job run details page\.

## Viewing the job run logs<a name="monitoring-job-run-logs"></a>

You can view the job logs in a variety of ways:
+ On the **Monitoring** page, in the **Job Run Breakdown** table, choose a job\. Then, on the **Actions** menu, choose **View logs** \.
+ In the visual job editor, on the **Run details** tab for a job, choose the hyperlinks to view the logs:
  + **Logs** – Links to the logs written to `stdout` for this job run\. When you choose this link, it takes you to Amazon CloudWatch Logs, where you can see all the details about the tables that were created in the AWS Glue Data Catalog and any errors that were encountered\.
  + **Error Logs** – Links to the logs written to `stderr` for this job run\. When you choose this link, it takes you to CloudWatch Logs, where you can view details about any errors that were encountered during the job run\.
+ If you run a job on\-demand and the job fails, choose the link in the banner to view the logs for that job run\.

## Viewing the details of a job run<a name="monitoring-job-run-details"></a>

You can choose a job in the **Job Run Breakdown** table and then choose **View run details** to see detailed information for that run of the job\. 

The information displayed on the job run detail page includes:
+ Job name, run status, start time, end time, and last modified date
+ AWS Glue version used by the job run
+ Number of recent attempts to run this job
+ Start and end time for the job run
+ The amount of time it took for the job to start
+ The amount of time for job execution
+ The name of the trigger associated with the job
+ The date when the job was last modified
+ The security configuration for the job 
+ The job run timeout threshold value
+ The capacity allocated for the job run and the maximum request capacity
+ The number of workers and the worker type
+ A link to the job log files
+ A link to the job error log files
+ The error returned for failed jobs

## Viewing Amazon CloudWatch metrics for a job run<a name="monitoring-job-run-metrics"></a>

On the job run details page, below the **Run details** section, you can view the job metrics\. AWS Glue Studio sends job metrics to Amazon CloudWatch for every job run\. 

AWS Glue reports metrics to Amazon CloudWatch every 30 seconds\. The AWS Glue metrics represent delta values from the previously reported values\. Where appropriate, metrics dashboards aggregate \(sum\) the 30\-second values to obtain a value for the entire last minute\. However, the Apache Spark metrics that AWS Glue passes on to Amazon CloudWatch are generally absolute values that represent the current state at the time they are reported\. 

**Note**  
You must configure your account to access Amazon CloudWatch, as described in [Amazon CloudWatch permissions](setting-up.md#getting-started-min-privs-cloudwatch)\.

The metrics provide information about your job run, such as:
+ **ETL Data Movement** – The number of bytes read from or written to Amazon S3\.
+ **Memory Profile: Heap used** – The number of memory bytes used by the Java virtual machine \(JVM\) heap\.
+ **Memory Profile: heap usage** – The fraction of memory \(scale: 0–1\) used by the JVM heap\.
+ **CPU Load** – The fraction of CPU system load used \(scale: 0–1\)\.