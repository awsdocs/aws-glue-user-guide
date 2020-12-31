# Editing the data source node<a name="edit-jobs-source"></a>

To specify the data source properties, you first choose a data source node in the graph\. Then, on the right\-side in the node details panel, you configure the node properties\.

1. Go to the visual graph editor for a new or saved job\.

1. Choose a data source node in the graph\.

1. Choose the **Node properties** tab in the node details panel, and then enter the following information:
   + **Name**: \(Optional\) Enter a name to associate with the node in the job graph\. This name should be unique among all the nodes for this job\.
   + **Node type**: The node type determines the action performed by the node\. In the list of options for **Node type**, choose one of the values listed under the heading **Data source**\.

     If you select a connector for the **Node type**, then follow the instructions at [Authoring jobs with custom connectors](connectors-chapter.md#job-authoring-custom-connectors) to complete the configuration of the data source properties\.

     For other types of data sources, a table for the source type that you choose must exist in the AWS Glue Data Catalog\. AWS Glue Studio does not create the table\.

1. Choose the **Data Source Properties** tab, and then enter the following information:
   + **Database**: Choose the database in the Data Catalog that contains the source table you want to use for this job\. You can use the search field to search for a database by its name\.
   + **Table**: Choose the table associated with the source data from the list\. This table must already exist in the AWS Glue Data Catalog\. You can use the search field to search for a table by its name\.
   + **Partition predicate**: Enter a Boolean expression based on Spark SQL that includes only the partitioning columns\. For example: `"(year=='2020' and month=='04')"`

1. After choosing the database and table, you can view the data schema by choosing the **Output schema** tab in the node details panel\. The information presented on this tab is read\-only and cannot be edited at this stage of job editing\.