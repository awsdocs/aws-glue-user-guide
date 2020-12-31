# Editing the data transform node<a name="edit-jobs-transforms"></a>

AWS Glue Studio provides a set of built\-in transforms that you can use to process your data\. Your data passes from one node in the graph to another in a data structure called a `DynamicFrame`, which is an extension to an Apache Spark SQL `DataFrame`\.

In the pre\-populated graph for a job, between the data source and data target nodes is the **Transform \- ApplyMapping** node\. You can configure this transform node to modify your data, or you can use additional transforms\. 

**Topics**
+ [Overview of mappings and transforms](#transforms_overview)
+ [Using ApplyMapping to remap data property keys](#transforms-configure-appplymapping)
+ [Using SelectFields to remove most data property keys](#transforms-configure-select-fields)
+ [Using DropFields to keep most data property keys](#transforms-configure-drop-fields)
+ [Renaming a field in the dataset](#transforms-configure-rename-field)
+ [Using Spigot to sample your dataset](#transforms-configure-spigot)
+ [Joining datasets](#transforms-configure-join)
+ [Using SplitFields to split a dataset into two](#transforms-configure-split-fields)
+ [Overview of *SelectFromCollection* transform](#transforms-selectfromcollection-overview)
+ [Using SelectFromCollection to choose which dataset to keep](#transforms-configure-select-collection)
+ [Filtering keys within a dataset](#transforms-filter)
+ [Creating a custom transformation](#transforms-custom)

## Overview of mappings and transforms<a name="transforms_overview"></a>

The following built\-in transforms are available with AWS Glue Studio:
+ **ApplyMapping**: Map data property keys in the data source to data property keys in the data target\. You can rename keys, modify the data types for keys, and choose which keys to drop from the dataset\.
+ **SelectFields**: Choose the data property keys that you want to keep\.
+ **DropFields**: Choose the data property keys that you want to drop\.
+ **RenameField**: Rename a single data property key\.
+ **Spigot**: Write samples of the data to an Amazon S3 bucket\.
+ **Join**: Join two datasets into one dataset using a comparison phrase on the specified data property keys\. You can use inner, outer, left, right, left excluding, and right excluding joins\.
+ **SplitFields**: Split data property keys into two `DynamicFrames`\. Output is a collection of `DynamicFrames`: one with selected data property keys, and one with the remaining data property keys\. 
+ **SelectFromCollection**: Choose one `DynamicFrame` from a collection of `DynamicFrames`\. The output is the selected `DynamicFrame`\.
+ **Filter**: Split a dataset into two, based on a filter condition\.
+ **Custom transform**: Enter code into a text entry field to use custom transforms\. The output is a collection of `DynamicFrames`\. 

## Using ApplyMapping to remap data property keys<a name="transforms-configure-appplymapping"></a>

An *ApplyMapping* transform remaps the source data property keys into the desired configured for the target data\. In an ApplyMapping transform node, you can:
+ Change the name of multiple data property keys\.
+ Change the data type of the data property keys, if the new data type is supported and there is a transformation path between the two data types\.
+ Choose a subset of data property keys by indicating which data property keys you want to drop\.

You can add additional *ApplyMapping* nodes to the graph as needed–for example, to modify additional data sources or following a *Join* transform\. 

1. Add a transform to the graph, if needed, by choosing the **Add node** icon \(![\[\]](http://docs.aws.amazon.com/glue/latest/ug/images/edit-toolbar-icon-add-orig.png)\) in the floating toolbar\.

1. With the transform node selected, choose the transform **ApplyMapping** for the **Node type** on the **Node properties ** tab in the node details panel\.

1. On the **Node properties** tab, enter a name for the node in the graph\. If a node parent isn't already selected, then choose a node from the **Node parents** list to use as the input source for the transform\.

1. Choose the **Transform** tab in the node details panel\.

1. Modify the input schema:
   + To rename a data property key, enter the new name of the key in the **Target key** field\.
   + To change the data type for a data property key, choose the new data type for the key from the **Data type** list\.
   + To remove a data property key from the target schema, choose the **Drop** check box for that key\.

1. Choose the **Output Schema** tab to see what the schema looks like after the transform is applied\.

## Using SelectFields to remove most data property keys<a name="transforms-configure-select-fields"></a>

You can create a subset of data property keys from the dataset using the *SelectFields* transform\. You indicate which data property keys you want to keep and the rest are removed from the dataset\.

1. Add a transform to the graph, if needed, by choosing the **Add node** icon \(![\[\]](http://docs.aws.amazon.com/glue/latest/ug/images/edit-toolbar-icon-add-orig.png)\) in the floating toolbar\.

1. With the transform node selected, choose the transform **SelectFields** for the **Node type** on the **Node properties ** tab in the node details panel\.

1. On the **Node properties** tab, enter a name for the node in the graph\. If a node parent is not already selected, then choose a node from the **Node parents** list to use as the input source for the transform\.

1. Choose the **Transform** tab in the node details panel\.

1. Under the heading **SelectFields**, choose the data property keys in the dataset that you want to keep\. Any data property keys not selected are dropped from the dataset\.

   You can also choose the check box next to the column heading **Field** to automatically choose all the data property keys in the dataset\. Then you can deselect individual data property keys to remove them from the dataset\.

1. Choose the **Output Schema** tab to see what the schema looks like after the transform is applied\.

## Using DropFields to keep most data property keys<a name="transforms-configure-drop-fields"></a>

You can create a subset of data property keys from the dataset using the *DropFields* transform\. You indicate which data property keys you want to remove from the dataset and the rest of the keys are retained\.

1. Add a transform to the graph, if needed, by choosing the **Add node** icon \(![\[\]](http://docs.aws.amazon.com/glue/latest/ug/images/edit-toolbar-icon-add-orig.png)\) in the floating toolbar\.

1. With the transform node selected, choose the transform **DropFields** for the **Node type** on the **Node properties ** tab in the node details panel\.

1. On the **Node properties** tab, enter a name for the node in the graph\. If a node parent is not already selected, then choose a node from the **Node parents** list to use as the input source for the transform\.

1. Choose the **Transform** tab in the node details panel\.

1. Under the heading **DropFields**, choose the data property keys to drop from the data source\.

   You can also choose the check box next to the column heading **Field** to automatically choose all the data property keys in the dataset\. Then you can deselect individual data property keys so they are retained in the dataset\.

1. Choose the **Output Schema** tab to see what the schema looks like after the transform is applied\.

## Renaming a field in the dataset<a name="transforms-configure-rename-field"></a>

You can use the *RenameField* transform to change the name for an individual property key in the dataset\. 

**Tip**  
To rename multiple data property keys in the dataset, use the *ApplyMapping* transform instead\.

1. Add a transform to the graph, if needed, by choosing the **Add node** icon \(![\[\]](http://docs.aws.amazon.com/glue/latest/ug/images/edit-toolbar-icon-add-orig.png)\) in the floating toolbar\.

1. With the transform node selected, choose the transform **RenameField** for the **Node type** on the **Node properties ** tab in the node details panel\.

1. On the **Node properties** tab, enter a name for the node in the graph\. If a node parent is not already selected, then choose a node from the **Node parents** list to use as the input source for the transform\.

1. Choose the **Rename field configuration** tab\.

1. Under the heading **RenameField configuration**, choose a property key from the source data in the **Source path** field and then enter a new name in the **Target path** field\. 

1. Choose the **Output Schema** tab to see what the schema looks like after the transform is applied\.

## Using Spigot to sample your dataset<a name="transforms-configure-spigot"></a>

To test the transformations performed by your job, you might want to get a sample of the data to check that the transformation works as intended\. The *Spigot* transform writes a subset of records from the dataset to a JSON file in an Amazon S3 bucket\. The data sampling method can be either a specific number of records from the beginning of the file or a probability factor used to pick records\.

1. Add a transform to the graph, if needed, by choosing the **Add node** icon \(![\[\]](http://docs.aws.amazon.com/glue/latest/ug/images/edit-toolbar-icon-add-orig.png)\) in the floating toolbar\.

1. With the transform node selected, choose the transform **Spigot** for the **Node type** on the **Node properties ** tab in the node details panel\.

1. On the **Node properties** tab, enter a name for the node in the graph\. If a node parent is not already selected, then choose a node from the **Node parents** list to use as the input source for the transform\.

1. Choose the **Spigot configuration** tab in the node details panel\.

1. Enter an Amazon S3 path or choose **Browse S3** to find the location in Amazon S3\. This is the location where the job writes the JSON file that contains the data sample\.

1. Enter information for the sampling method\. You can specify a number of records to write starting from the beginning of the dataset and a probability \(entered as a decimal value with a maximum value of 1\) of picking any given record\. 

   For example, to write the first 50 records from the dataset, you would set the number of records from the beginning of the file to 50 and the probability to 1 \(100%\)\.

## Joining datasets<a name="transforms-configure-join"></a>

The *Join* transform allows you to combine two datasets into one\. You specify the key names in the schema of each dataset to compare\. The output `DynamicFrame` contains rows where keys meet the join condition\. The rows in each dataset that meet the join condition are combined into a single row in the output `DynamicFrame` that contains all the columns found in either dataset\.

1. If there is only one data source available, you must add a new data source node to the graph\. See [Adding nodes to the job graph](edit-job-add-nodes.md) for details\.

1. Choose one of the source nodes for the join, and then add a new node to the graph by choosing the **Add node** icon \(![\[\]](http://docs.aws.amazon.com/glue/latest/ug/images/edit-toolbar-icon-add-orig.png)\) in the floating toolbar\.

1. With the transform node selected, choose the transform **Join** for the **Node type** on the **Node properties ** tab\. You can optionally give the node a new name\.

1. In the **Node properties** tab, under the heading **Node parents**, add a parent node so that there are two datasets providing inputs for the join\. The parent can be a data source node or a transform node\. 
**Note**  
A join can have only two parent nodes\.

1. Choose the **Transform** tab\.

   If you see a message indicating that there are conflicting key names, you can either:
   + Choose **Resolve** to automatically add an *ApplyMapping* transform node to your graph\. The *ApplyMapping* node adds a prefix to any keys in the dataset that have the same name as a key in the other dataset\. For example, if you use the default value of **right**, then any keys in the right dataset that have the same name as a key in the left dataset will be renamed to `(right)keyname`\.
   + Manually add a transform node earlier in the graph to remove or rename the conflicting keys\.

1. Choose the type of join in the **Join type** list\. 
   + **Inner join**: All rows from each dataset that satisfy the join condition\. Rows that do not satisfy the join condition are not returned\.
   + **Left join**: All rows from the left dataset and only the rows from the right dataset that satisfy the join condition\. 
   + **Right join**: All rows from the right dataset and only the rows from the left dataset that satisfy the join condition
   + **Outer join**: All rows from both datasets\.
   + **Left excluding join**: All rows in the left dataset that do not satisfy the join condition\. 
   + **Right excluding join**: All rows in the right dataset that do not satisfy the join condition\. 

1. On the **Transform** tab, under the heading **Join conditions**, choose **Add condition**\. Choose a property key from each dataset to compare\. Property keys on the left side of the comparison operator are referred to as the left dataset and property keys on the right are referred to as the right dataset\. 

   For more complex join conditions, you can add additional matching keys by choosing **Add condition** more than once\. If you accidentally add a condition, you can use the delete icon \(![\[\]](http://docs.aws.amazon.com/glue/latest/ug/images/delete-icon-black.png)\) to remove it\.

1. Choose the **Output Schema** tab to see what the schema looks like after the transform is applied\.

For an example of the join output schema, consider a join between two datasets with the following property keys:

```
Left: {id, dept, hire_date, salary, employment_status}
Right: {id, first_name, last_name, hire_date, title}
```

The join is configured to match on the `id` and `hire_date` keys using the `=` comparison operator\. 

Because both datasets contain `id` and `hire_date` keys, you used the **Resolve** option to automatically add the prefix **right** to the keys in the right dataset\. 

The keys in the output schema would be:

```
{id, dept, hire_date, salary, employment_status, 
(right)id, first_name, last_name, (right)hire_date, title}
```

## Using SplitFields to split a dataset into two<a name="transforms-configure-split-fields"></a>

The *SplitFields* transform allows you to choose some of the data property keys in the input dataset and put them into one dataset and the unselected keys into a separate dataset\. The output from this transform is a collection of `DynamicFrames`\.

**Note**  
You must use a *SelectFromCollection* transform to convert the collection of `DynamicFrames` into a single `DynamicFrame` before you can send the output to a target location\.

1. Add a transform to the graph, if needed, by choosing the **Add node** icon \(![\[\]](http://docs.aws.amazon.com/glue/latest/ug/images/edit-toolbar-icon-add-orig.png)\) in the floating toolbar\.

1. With the new transform node selected, choose the transform **SplitFields** for the **Node type** in the **Node properties** tab of the details panel\.

1. On the **Node properties** tab, enter a name for the node in the graph\. If a node parent is not already selected, then choose a node from the **Node parents** list to use as the input source for the transform\.

1. Choose the **Transform** tab\.

1. Under the heading **Split fields**, choose which property keys you want to put into the first dataset\. The keys that you do not choose are placed in the second dataset\.

1. You can choose the **Output Schema** tab to see what each schema will look like after the transform is applied\.

## Overview of *SelectFromCollection* transform<a name="transforms-selectfromcollection-overview"></a>

Certain transforms have multiple datasets as their output instead of a single dataset, for example, *SplitFields*\. The *SelectFromCollection* transform selects one dataset \(`DynamicFrame`\) from a collection of datasets \(an array of `DynamicFrames`\)\. The output for the transform is the selected `DynamicFrame`\. 

You must use this transform after you use a transform that creates a collection of `DynamicFrames`, such as:
+ Custom code transforms
+ *SplitFields*

If you don't add a *SelectFromCollection* transform node to your job graph after any of the above transforms, you will get an error for your job\. 

The parent node for this transform must be a node that returns a collection of `DynamicFrames`\. If you choose a parent for this transform node that returns a single `DynamicFrame`, such as a *Join* transform, your job returns an error\. 

Similarly, if you use a *SelectFromCollection* node in your job graph as the parent for a transform that expects a single `DynamicFrame` as input, your job returns an error\.

![\[The screenshot shows the Node parents field on the Node properties tab of the node details panel. The selected node parent is SplitFields and the error message displayed reads "Parent node SplitFields outputs a collection, but node DropFields does not accept a collection."\]](http://docs.aws.amazon.com/glue/latest/ug/images/screenshot-edit-splitfields-wrong-parent.png)

## Using SelectFromCollection to choose which dataset to keep<a name="transforms-configure-select-collection"></a>

Use the *SelectFromCollection* transform to convert a collection of `DynamicFrames` into a single `DynamicFrame`\.

1. Add a transform to the graph, if needed, by choosing the **Add node** icon \(![\[\]](http://docs.aws.amazon.com/glue/latest/ug/images/edit-toolbar-icon-add-orig.png)\) in the floating toolbar\.

1. With the new transform node selected, choose the transform **SelectFromCollection** for the node type in the **Node properties** tab of the details panel\.

1. On the **Node properties** tab, enter a name for the node in the graph\. If a node parent is not already selected, then choose a node from the **Node parents** list to use as the input source for the transform\.

1. Choose the **Transform** tab\.

1. Under the heading **Frame**, choose the array index number that corresponds to the `DynamicFrame` you want to select from the collection of `DynamicFrames`\.

   For example, if the parent node for this transform is a *SplitFields* transform, on the **Output schema** tab of that node you can see the schema for each `DynamicFrame`\. If you want to keep the `DynamicFrame` associated with the schema for **Output 2**, you would select **1** for the value of **Frame**, which is the second value in the list\.

   Frames that you do not choose aren't included in the output\.

1. You can choose the **Output Schema** tab to see what the schema will look like after the transform is applied\.

## Filtering keys within a dataset<a name="transforms-filter"></a>

Use the *Filter* transform to create a new dataset by filtering records from the input dataset based on a regular expression\. Rows that don't satisfy the filter condition are removed from the output\.
+ For string data types, you can filter rows where the key value matches a specified string\.
+ For numeric data types, you can filter rows by comparing the key value to a specified value using the comparison operators `<`, `>`, `=`, `!=`, `<=`, and `>=`\.

If you specify multiple filter conditions, the results are combined using an `AND` operator by default, but you can choose `OR` instead\.

1. Add a transform to the graph, if needed, by choosing the **Add node** icon \(![\[\]](http://docs.aws.amazon.com/glue/latest/ug/images/edit-toolbar-icon-add-orig.png)\) in the floating toolbar\.

1. With the new transform node selected, choose the transform **Filter** for the node type in the **Node properties** tab of the details panel\.

1. On the **Node properties** tab, enter a name for the node in the graph\. If a node parent isn't already selected, then choose a node from the **Node parents** list to use as the input source for the transform\.

1. Choose the **Transform** tab\.

1. Add a filter condition:
   + If there are currently no filters, you can choose the **Add new filter** button that is displayed in the **Filter** section\.
   + To the far right of the heading **Filter**, you can choose the Add icon \(![\[\]](http://docs.aws.amazon.com/glue/latest/ug/images/filter-add-icon.png)\) to add a new filter condition\.

   In the first field \(on the left\), choose a property key name from the dataset\. In the middle field, choose the comparison operator\. In the last field \(on the right\), enter the comparison value\. Here are some examples of filter conditions:
   + `year >= 2018`
   + `State matches 'CA*'`

   When you filter on string values, make sure that the comparison value uses a regular expression format that matches the script language selected in the job properties \(Python or Scala\)\.

1. Add additional filter conditions, as needed\. 

1. If you want to use OR to combine the filter expressions, then choose the AND option \(![\[\]](http://docs.aws.amazon.com/glue/latest/ug/images/filter-AND-option.png) to change it to `OR`\. 

## Creating a custom transformation<a name="transforms-custom"></a>

If you need to perform more complicated transformations on your data, or want to add data property keys to the dataset, you can add a **Custom code** transform to your job graph\. The Custom code node allows you to enter a script that performs the transformation\. 

When using custom code, you must use a schema editor to indicate the changes made to the output through the custom code\. When editing the schema, you can perform the following actions:
+ Add or remove data property keys
+ Change the data type of data property keys
+ Change the name of data property keys
+ Restructure a nested property key

You must use a *SelectFromCollection* transform to choose a single `DynamicFrame` from the result of your Custom transform node before you can send the output to a target location\. 

Use the following tasks to add a custom transform node to your graph\.

### Adding a custom code transform node to the graph<a name="transforms-custom-addnode"></a>

1. Add a transform to the graph, if needed, by choosing the **Add node** icon \(![\[\]](http://docs.aws.amazon.com/glue/latest/ug/images/edit-toolbar-icon-add-orig.png)\) in the floating toolbar\.

1. With the transform node selected, choose the transform **Custom transform** for the **Node type** on the **Node properties ** tab\.

1. On the **Node properties** tab, enter a name for the node in the graph\. If a node parent is not already selected, or if you want multiple inputs for the custom transform, then choose a node from the **Node parents** list to use as the input source for the transform\.

### Entering code for the custom transform node<a name="transforms-custom-addcode"></a>

You can type or copy code into an input field\. The job uses this code to perform the data transformation\. You can provide a code snippet in either Python or Scala\. The code should take one or more `DynamicFrames` as input and returns a collection of `DynamicFrames`\. 

1. With the custom transform node selected in the graph, choose the **Transform** tab\. 

1. In the text entry field under the heading **Code block**, paste or enter the code for the transformation\. The code that you use must match the language specified for the job on the **Job details** tab\.

   When referring to the input nodes in your code, AWS Glue Studio names the `DynamicFrames` returned by the graph nodes sequentially based on the order of creation, for example:
   + Data source nodes: `DataSource0`, `DataSource1`, `DataSource2`, and so on\.
   + Transform nodes: `Transform0`, `Transform1`, `Transform2`, and so on\.

The following examples show the format of the code to enter in the code box:

------
#### [ Python ]

The following example takes the first `DynamicFrame` received, converts it to a `DataFrame` to apply the native filter method \(keeping only records that have over 1000 votes\), then converts it back to a `DynamicFrame` before returning it\.

```
def FilterHighVoteCounts (glueContext, dfc) -> DynamicFrameCollection:
    df = dfc.select(list(dfc.keys())[0]).toDF()
    df_filtered = df.filter(df["vote_count"] > 1000)
    dyf_filtered = DynamicFrame.fromDF(df_filtered, glueContext, "filter_votes")
    
    return(DynamicFrameCollection({"CustomTransform0": dyf_filtered}, glueContext))
```

------
#### [ Scala ]

The following example takes the first `DynamicFrame` received, converts it to a `DataFrame` to apply the native filter method \(keeping only records that have over 1000 votes\), then converts it back to a `DynamicFrame` before returning it\.

```
object FilterHighVoteCounts {
  def execute(glueContext : GlueContext, input : Seq[DynamicFrame]) : Seq[DynamicFrame] = {
    val frame = input(0).toDF()
    val filtered = DynamicFrame(frame.filter(frame("vote_count") > 1000), glueContext)
    Seq(filtered)
  }
}
```

------

### Editing the schema in a custom transform node<a name="transforms-custom-editschema"></a>

When you use a custom transform node, AWS Glue Studio cannot automatically infer the output schemas created by the transform\. You use **Edit schema** to describe the schema changes implemented by the custom transform code\.

A custom code node can have any number of parent nodes, each providing a `DynamicFrame` as input for your custom code\. A custom code node returns a collection of `DynamicFrames`\. Each `DynamicFrame` that is used as input has an associated schema\. You must add a schema that describes each `DynamicFrame` returned by the custom code node\. 

1. With the custom transform node selected in the job graph, in the node details panel, choose the **Output schema** tab\. 

1. Choose **Edit** to make changes to the schema\. 

   If you have nested data property keys, such as an array or object, you can use the tree\-view icon to the left of the top\-level key name to either expand or collapse the list of child data property keys\.

1. Modify the schema using the following actions in the **Output schema** section of the page:
   + To rename a property key, place the cursor in the **Key** text box for the property key, then enter the new name\.
   + To change the data type for a property key, use the list to choose the new data type for the property key\.
   + To add a new top\-level property key to the schema, choose the ![\[\]](http://docs.aws.amazon.com/glue/latest/ug/images/edit-schema-actions-button.png) button, and then choose **Add root key**\. 
   + To add a child property key to the schema, choose the Add icon ![\[\]](http://docs.aws.amazon.com/glue/latest/ug/images/filter-add-icon.png)associated with the parent key\. Enter a name for the child key and choose the data type\.
   + To remove a property key from the schema, choose the delete icon \(![\[\]](http://docs.aws.amazon.com/glue/latest/ug/images/delete-icon-black.png)\) to the far right of the key name\. 

1. If your custom transform code uses multiple `DynamicFrames`, choose the ![\[\]](http://docs.aws.amazon.com/glue/latest/ug/images/edit-schema-actions-button.png) button, and then choose either **Add output schema** or **Duplicate**\. Then add new root keys to the schema or edit the duplicated keys\.

When you are done, choose **Apply** to modify the output schema\.

### Configure the custom transform output<a name="transforms-custom-output"></a>

A custom code transform returns a collection of `DynamicFrames`, even if there is only one `DynamicFrame` in the result set\. A *SelectFromCollection* transform is added to the job graph automatically, with the custom node transform as its parent\. Update this additional transform to indicate which dataset you want to use\. See [Using SelectFromCollection to choose which dataset to keep](#transforms-configure-select-collection) for more information\.

Add additional *SelectFromCollection* transforms to the job graph if you want to use an additional `DynamicFrame` produced by the custom code\.