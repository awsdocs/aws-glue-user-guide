# Editing the data source node<a name="edit-jobs-source"></a>

To specify the data source properties, you first choose a data source node in the job diagram\. Then, on the right side in the node details panel, you configure the node properties\.

**To modify the properties of a data source node**

1. Go to the visual editor for a new or saved job\.

1. Choose a data source node in the job diagram\.

1. Choose the **Node properties** tab in the node details panel, and then enter the following information:
   + **Name**: \(Optional\) Enter a name to associate with the node in the job diagram\. This name should be unique among all the nodes for this job\.
   + **Node type**: The node type determines the action that is performed by the node\. In the list of options for **Node type**, choose one of the values listed under the heading **Data source**\.

1. Configure the **Data source properties** information\. For more information, see the following sections:
   + [Using Data Catalog tables for the data source](edit-jobs-source-catalog-tables.md)
   + [Using a connector for the data source](edit-jobs-source-connectors.md)
   + [Using files in Amazon S3 for the data source](edit-jobs-source-s3-files.md)
   + [Using a streaming data source](edit-jobs-source-streaming.md)

1. \(Optional\) After configuring the node properties and data source properties, you can view the schema for your data source by choosing the **Output schema** tab in the node details panel\. The first time you choose this tab for any node in your job, you are prompted to provide an IAM role to access the data\. If you have not specified an IAM role on the **Job details** tab, you are prompted to enter an IAM role here\.

1. \(Optional\) After configuring the node properties and data source properties, you can preview the dataset from your data source by choosing the **Data preview** tab in the node details panel\. The first time you choose this tab for any node in your job, you are prompted to provide an IAM role to access the data\. There is a cost associated with using this feature, and billing starts as soon as you provide an IAM role\.