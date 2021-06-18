# Using files in Amazon S3 for the data source<a name="edit-jobs-source-s3-files"></a>

If you choose Amazon S3 as your data source, then you can choose either:
+ A Data Catalog database and table\.
+ A bucket, folder, or file in Amazon S3\.

If you use an Amazon S3 bucket as your data source, AWS Glue Studio detects the schema of the data at the specified location from one of the files, or by using the file you specify as a sample file\. Schema detection occurs when you use the **Infer schema** button\. If you change the Amazon S3 location or the sample file, then you must choose **Infer schema** again to perform the schema detection using the new information\.

**To configure a data source node that reads directly from files in Amazon S3**

1. Go to the visual editor for a new or saved job\.

1. Choose a data source node in the job diagram for an Amazon S3 source\.

1. Choose the **Data source properties** tab, and then enter the following information:
   + **S3 source type**: \(For Amazon S3 data sources only\) Choose the option **S3 location**\.
   + **S3 URL**: Enter the path to the Amazon S3 bucket, folder, or file that contains the data for your job\. You can choose **Browse S3** to select the path from the locations available to your account\. 
   + **Recursive**: Choose this option if you want AWS Glue Studio to read data from files in child folders at the S3 location\. 

     If the child folders contain partitioned data, AWS Glue Studio doesn't add any partition information that's specified in the folder names to the Data Catalog\. For example, consider the following folders in Amazon S3:

     ```
     S3://sales/year=2019/month=Jan/day=1
     S3://sales/year=2019/month=Jan/day=2
     ```

     If you choose **Recursive** and select the `sales` folder as your S3 location, then AWS Glue Studio reads the data in all the child folders, but doesn't create partitions for year, month or day\.
   + **Data format**: Choose the format that the data is stored in\. You can choose JSON, CSV, or Parquet\. The value you select tells the AWS Glue job how to read the data from the source file\.
**Note**  
If you don't select the correct format for your data, AWS Glue Studio might infer the schema correctly, but the job won't be able to correctly parse the data from the source file\.

     You can enter additional configuration options, depending on the format you choose\. 
     + **JSON** \(JavaScript Object Notation\)
       + **JsonPath**: Enter a JSON path that points to an object that is used to define a table schema\. JSON path expressions always refer to a JSON structure in the same way as XPath expression are used in combination with an XML document\. The "root member object" in the JSON path is always referred to as `$`, even if it's an object or array\. The JSON path can be written in dot notation or bracket notation\.

         For more information about the JSON path, see [JsonPath](https://github.com/json-path/JsonPath) on the GitHub website\.
       + **Records in source files can span multiple lines**: Choose this option if a single record can span multiple lines in the CSV file\.
     + **CSV** \(comma\-separated values\)
       + **Delimiter**: Enter a character to denote what separates each column entry in the row, for example, `;` or `,`\.
       + **Escape character**: Enter a character that is used as an escape character\. This character indicates that the character that immediately follows the escape character should be taken literally, and should not be interpreted as a delimiter\.
       + **Quote character**: Enter the character that is used to group separate strings into a single value\. For example, you would choose **Double quote \("\)** if you have values such as `"This is a single value"` in your CSV file\.
       + **Records in source files can span multiple lines**: Choose this option if a single record can span multiple lines in the CSV file\.
       + **First line of source file contains column headers**: Choose this option if the first row in the CSV file contains column headers instead of data\.
     + **Parquet** \(Apache Parquet columnar storage\)

       There are no additional settings to configure for data stored in Parquet format\.
   + **Partition predicate**: To partition the data that is read from the data source, enter a Boolean expression based on Spark SQL that includes only the partitioning columns\. For example: `"(year=='2020' and month=='04')"`
   + **Advanced options**: Expand this section if you want AWS Glue Studio to detect the schema of your data based on a specific file\. 
     + **Schema inference**: Choose the option **Choose a sample file from S3** if you want to use a specific file instead of letting AWS Glue Studio choose a file\.
     + **Auto\-sampled file**: Enter the path to the file in Amazon S3 to use for inferring the schema\.

     If you're editing a data source node and change the selected sample file, choose **Reload schema** to detect the schema by using the new sample file\.

1. Choose the **Infer schema** button to detect the schema from the sources files in Amazon S3\. If you change the Amazon S3 location or the sample file, you must choose **Infer schema** again to infer the schema using the new information\.