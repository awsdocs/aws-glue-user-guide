# Job editor features<a name="job-editor-features"></a>

The job editor provides the following features for creating and editing jobs\.
+ A visual diagram of your job, with a node for each job task: Data source nodes for reading the data; transform nodes for modifying the data; data target nodes for writing the data\.

  You can view and configure the properties of each node in the job diagram\. You can also view the schema and sample data for each node in the job diagram\. These features help you to verify that your job is modifying and transforming the data in the right way, without having to run the job\.
+ A Script viewing and editing tab, where you can modify the code generated for your job\.
+ A Job details tab, where you can configure a variety of settings to customize the environment in which your AWS Glue ETL job runs\.
+ A Runs tab, where you can view the current and previous runs of the job, view the status of the job run, and access the logs for the job run\.
+ A Schedules tab, where you can configure the start time for you job, or set up a recurring job runs\.

## Using schema previews in the visual job editor<a name="schema-previews"></a>

While creating or editing your job, you can use the **Output schema** tab to view the schema for your data\. 

Before you can see the schema, the job editor needs permissions to access the data source\. You can specify an IAM role on the Job details tab of the editor or on the **Output schema** tab for a node\. If the IAM role has all the necessary permissions to access the data source, you can then view the schema on the **Output schema** tab for a node\.

## Using data previews in the visual job editor<a name="data-previews"></a>

While creating or editing your job, you can use the **Data preview** tab to view a sample of your data\. 

Before you can see the data sample, the job editor needs permissions to access the data source\. The first time you choose the **Data preview** tab, you are prompted to choose an IAM role to use\. This can be the same role that you plan to use for your job, or it can be a different role\. The IAM role you choose must have the necessary permissions to create the data previews\.

After you choose an IAM role, it takes about 20 to 30 seconds before the data appears\. You are charged for data preview usage as soon as you choose the IAM role\. The following features help you when viewing the data\.
+ Choose the settings icon \(a gear symbol\) to configure your preferences for data previews\. You can change the sample size or you can choose to wrap the text from one line to the next\. These settings apply to all nodes in the job diagram\. 
+ Choose the **Previewing x of y fields** button to select which columns \(fields\) to preview\. When you preview you data using the default settings, the job editor shows the first 5 columns of your dataset\. You can change this to show all or none \(not recommended\)\. 
+ You can scroll through the data preview window both horizontally and vertically\. 
+ Use the split/whole screen button to expand the Data preview tab to the entire screen \(over\-laying the job graph\), to better view the data and data structures\.

Data previews help you create and test your job, without having to repeatedly run the job\.
+ You can test an IAM role to make sure you have access to your data sources or data targets\.
+ You can check that the transform is modifying the data in the intended way\. For example, if you use a Filter transform, you can make sure that the filter is selecting the right subset of data\.
+ If your dataset contains columns with values of multiple types, the data preview shows a list of tuples for these columns\. Each tuple contains the data type and its value, as shown in the following screenshot\.  
![\[The screenshot shows the Data preview tab for a node. The columns displayed are country, alpha-2 code, alpha-3 code, numeric code, and latitude. The first 5 countries listed are Afghanistan, Albania, Algeria, American Samoa, and Andorra. For the latitude column, the values shown are: {"long":33, "string":null}, {"long":41, "string":null},{"long":28, "string":null},{"long":null, "string":"-14.3333"}, {"long":null, "string":"42.5"}, and 2 more.\]](http://docs.aws.amazon.com/glue/latest/ug/images/data-previews-choice-type.png)

## Restrictions when using data previews<a name="data-preview-limits"></a>

When using data previews, you might encounter the following restrictions or limitations\. 
+ The first time you choose the Data preview tab you must choose IAM role\. This role must have the necessary permissions to access the data and other resources needed to create the data previews\.
+ After you provide an IAM role, it takes a while before the data is available for viewing\. For datasets with less than 1 GB of data, it can take up to one minute\. If you have a large dataset, you should use partitions to improve the loading time\. Loading data directly from Amazon S3 has the best performance\.
+ If you have a very large dataset, and it takes more than 30 minutes to query the data for the data preview, the request will time out\. You can reduce the dataset size to use data previews\.
+ By default, you see the first 5 columns in the Data preview tab\. If the columns have no data values, you will get a message that there is no data to display\. You can increase the number of rows sampled, or selected different columns to see data values\.
+ Data previews are currently not supported for streaming data sources, or for data sources that use custom connectors\.
+ Errors on one node effect the entire job\. If any one node has an error with data previews, the error will show up on all nodes until you correct it\.
+ If you change a data source for the job, then the child nodes of that data source might need to be updated to match the new schema\. For example, if you have an ApplyMapping node that modifies a column, and the column does not exist in the replacement data source, you will need to update the ApplyMapping transform node\.
+ If you view the Data preview tab for a SQL query transform node, and the SQL query uses an incorrect field name, the Data preview tab shows an error\. 