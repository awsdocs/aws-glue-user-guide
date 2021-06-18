# Monitoring ETL jobs in AWS Glue Studio<a name="monitoring-chapter"></a>

Monitoring is an important part of maintaining the reliability, availability, and performance of ETL jobs used in AWS Glue and AWS Glue Studio\. You should collect monitoring data from all of the parts of your AWS solution so that you can more easily debug a multipoint failure if one occurs\. 

**Topics**
+ [Accessing the job monitoring dashboard](#monitoring-accessing-dashboard)
+ [Overview of the job monitoring dashboard](#monitoring-dashboard-overview)
+ [Job runs view](#monitoring-job-breakdown)
+ [Viewing the job run logs](#monitoring-job-run-logs)
+ [Viewing the details of a job run](#monitoring-job-run-details)
+ [Viewing Amazon CloudWatch metrics for a job run](#monitoring-job-run-metrics)

## Accessing the job monitoring dashboard<a name="monitoring-accessing-dashboard"></a>

You access the job monitoring dashboard by choosing the **Monitoring** link in the AWS Glue Studio navigation pane\.

## Overview of the job monitoring dashboard<a name="monitoring-dashboard-overview"></a>

The job monitoring dashboard provides an overall summary of the job runs, with totals for the jobs with a status of **Running**, **Canceled**, **Success**, or **Failed**\. Additional tiles provide the overall job run success rate, the estimated DPU usage for jobs, a breakdown of the job status counts by job type, worker type, and by day\. 

The graphs in the tiles are interactive\. You can choose any block in a graph to run a filter that displays only those jobs in the **Job runs** table at the bottom of the page\.

You can change the date range for the information displayed on this page by using the **Date range** selector\. When you change the date range, the information tiles adjust to show the values for the specified number of days before the current date\. You can also use a specific date range if you choose **Custom** from the date range selector\. 

## Job runs view<a name="monitoring-job-breakdown"></a>

The **Job runs** resource list shows the jobs for the specified date range and filters\.

You can filter the jobs on additional criteria, such as status, worker type, job type, and the job name\. In the filter box at the top of the table, you can enter the text to use as a filter\. The table results are updated with rows that contain matching text as you enter the text\.

You can view a subset of the jobs by choosing elements from the graphs on the job monitoring dashboard\. For example, if you choose the number of running jobs in the **Job runs summary** tile, then the **Job runs** list displays only the jobs that currently have a status of `Running`\. If you choose one of the bars in the **Worker type breakdown** bar chart, then only job runs with the matching worker type and status are shown in the **Job runs** list\.

The **Job runs** resource list displays the details for the job runs\. You can sort the rows in the table by choosing a column heading\. The table contains the following information:


| Property | Description | 
| --- | --- | 
| Job name | The name of the job | 
| Type |  The type of job environment: [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/glue/latest/ug/monitoring-chapter.html)  | 
| Start time |  The date and time at which this job run was started\.  | 
| End time |  The date and time that this job run completed\.  | 
| Run status |  The current state of the job run\. Values can be: [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/glue/latest/ug/monitoring-chapter.html)  | 
| Run time | The amount of time that the job run consumed resources\. | 
| Capacity |  The number of AWS Glue data processing units \(DPUs\) that were allocated for this job run\. For more information about capacity planning, see [Monitoring for DPU Capacity Planning](https://docs.aws.amazon.com/glue/latest/dg/monitor-debug-capacity.html) in the *AWS Glue Developer Guide*\.  | 
| Worker type |  The type of predefined worker that was allocated when the job ran\. Values can be `Standard`, `G.1X`, or `G.2X`\.   | 
| DPU hours |  The estimated number of DPUs used for the job run\. A DPU is a relative measure of processing power\. DPUs are used to determine the cost of running your job\. For more information, see the [AWS Glue pricing](https://aws.amazon.com/glue/pricing/) page\.  | 

You can choose any job run in the list and view additional information\. Choose a job run, and then do one of the following:
+ Choose the **Actions** menu and the **View job** option to view the job in the visual editor\.
+ Choose the **Actions** menu and the **Stop run** option to stop the current run of the job\.
+ Choose the **View CloudWatch logs** button to view the job run logs for that job\. 
+ Choose **View run details** to view the job run details page\.

## Viewing the job run logs<a name="monitoring-job-run-logs"></a>

You can view the job logs in a variety of ways:
+ On the **Monitoring** page, in the **Job runs** table, choose a job run, and then choose **View CloudWatch logs**\.
+ In the visual job editor, on the **Runs** tab for a job, choose the hyperlinks to view the logs:
  + **Logs** – Links to the Apache Spark job logs written when continuous logging is enabled for a job run\. When you choose this link, it takes you to the Amazon CloudWatch logs in the `/aws-glue/jobs/logs-v2` log group\. By default, the logs exclude non\-useful Apache Hadoop YARN heartbeat and Apache Spark driver or executor log messages\. For more information about continuous logging, see [Continuous Logging for AWS Glue Jobs](https://docs.aws.amazon.com/glue/latest/dg/monitor-continuous-logging.html) in the *AWS Glue Developer Guide*\.
  + **Error logs** – Links to the logs written to `stderr` for this job run\. When you choose this link, it takes you to the Amazon CloudWatch logs in the `/aws-glue/jobs/error` log group\. You can use these logs to view details about any errors that were encountered during the job run\.
  + **Output logs** – Links to the logs written to `stdout` for this job run\. When you choose this link, it takes you to the Amazon CloudWatch logs in the `/aws-glue/jobs/output` log group\. You can use these logs to see all the details about the tables that were created in the AWS Glue Data Catalog and any errors that were encountered\.

## Viewing the details of a job run<a name="monitoring-job-run-details"></a>

You can choose a job in the **Job runs** list on the **Monitoring** page, and then choose **View run details** to see detailed information for that run of the job\. 

The information displayed on the job run detail page includes:


| Property | Description | 
| --- | --- | 
| Job name | The name of the job | 
| Run Status |  The current state of the job run\. Values can be: [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/glue/latest/ug/monitoring-chapter.html)  | 
| Glue version | The AWS Glue version used by the job run | 
| Recent attempt | The number of automatic retry attempts for this job run | 
| Start time |  The date and time at which this job run was started  | 
| End time |  The date and time that this job run completed  | 
| Start\-up time |  The amount of time spent preparing to run the job  | 
| Execution time |  The amount of time spent running the job script  | 
| Trigger name |  The name of the trigger associated with the job  | 
| Last modified on |  The date when the job was last modified  | 
| Security configuration |  The security configuration for the job, which includes Amazon S3 encryption, CloudWatch encryption, and job bookmarks encryption settings  | 
| Timeout | The job run timeout threshold value | 
| Allocated capacity |  The number of AWS Glue data processing units \(DPUs\) that were allocated for this job run\. For more information about capacity planning, see [Monitoring for DPU Capacity Planning](https://docs.aws.amazon.com/glue/latest/dg/monitor-debug-capacity.html) in the *AWS Glue Developer Guide*\.  | 
| Max capacity |  The maximum capacity available to the job run\.  | 
| Number of workers | The number of workers used for the job run  | 
| Worker type |  The type of predefined workers allocated for the job run\. Values can be `Standard`, `G.1X`, or `G.2X`\.  | 
| Logs | A link to the job logs for continuous logging \(/aws\-glue/jobs/logs\-v2\)  | 
| Output Logs | A link to the job output log files \(/aws\-glue/jobs/output\) | 
| Error logs | A link to the job error log files \(/aws\-glue/jobs/error\) | 

## Viewing Amazon CloudWatch metrics for a job run<a name="monitoring-job-run-metrics"></a>

On the details page for a job run, below the **Run details** section, you can view the job metrics\. AWS Glue Studio sends job metrics to Amazon CloudWatch for every job run\. 

AWS Glue reports metrics to Amazon CloudWatch every 30 seconds\. The AWS Glue metrics represent delta values from the previously reported values\. Where appropriate, metrics dashboards aggregate \(sum\) the 30\-second values to obtain a value for the entire last minute\. However, the Apache Spark metrics that AWS Glue passes on to Amazon CloudWatch are generally absolute values that represent the current state at the time they are reported\. 

**Note**  
You must configure your account to access Amazon CloudWatch, as described in [Amazon CloudWatch permissions](setting-up.md#getting-started-min-privs-cloudwatch)\.

The metrics provide information about your job run, such as:
+ **ETL Data Movement** – The number of bytes read from or written to Amazon S3\.
+ **Memory Profile: Heap used** – The number of memory bytes used by the Java virtual machine \(JVM\) heap\.
+ **Memory Profile: heap usage** – The fraction of memory \(scale: 0–1\), shown as a percentage, used by the JVM heap\.
+ **CPU Load** – The fraction of CPU system load used \(scale: 0–1\), shown as a percentage\.