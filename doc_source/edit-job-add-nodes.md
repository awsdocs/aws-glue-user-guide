# Adding nodes to the job diagram<a name="edit-job-add-nodes"></a>

You can add additional data sources, transforms, and data targets to your job to support more complex ETL actions\.

**To add nodes to a job diagram**

1. Go to the visual editor for a new or saved job and choose the **Visual** tab\.

1. Use the toolbar buttons to add a node of a specific type: **Source**, **Transform**, or **Target**\.  
![\[\]](http://docs.aws.amazon.com/glue/latest/ug/images/edit-toolbar-new.png)

1. Edit the node, as described in the following sections:
   + For a source node, see [Editing the data source node](edit-jobs-source.md)\.
   + For a transform node, see [Editing the data transform node](edit-jobs-transforms.md)\.
   + For a data target node, see [Editing the data target node](data-target-nodes.md#edit-jobs-target)\.

1. If you're inserting a node in between two nodes in the job diagram, then perform the following actions:

   1. Choose the node that will be the parent for the new node\.

   1. Choose one of the toolbar buttons to add a new node to the job diagram\. The new node is added as a child of the currently selected node\.

   1. Choose the node that will be the child of the newly added node and change its parent node to point to the newly added node\.

If you added a node by mistake, you can use the **Undo** button on the toolbar to reverse the action\.