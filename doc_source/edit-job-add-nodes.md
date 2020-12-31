# Adding nodes to the job graph<a name="edit-job-add-nodes"></a>

You can add additional data sources, transforms, and data targets to your job to support more complex ETL actions\.

1. Go to the visual graph editor for a new or saved job and choose the **Visual** tab\.

1. Choose the **Add node** icon \(![\[\]](http://docs.aws.amazon.com/glue/latest/ug/images/edit-toolbar-icon-add-orig.png)\) in the floating toolbar\.

1. Edit the node, as described in the following sections:
   + For a source node, see [Editing the data source node](edit-jobs-source.md)\.
   + For a transform node, see [Editing the data transform node](edit-jobs-transforms.md)\.
   + For a data target node, see [Editing the data target node](data-target-nodes.md#edit-jobs-target)\.

1. If you're inserting a node in between two nodes in the graph, then choose the node that will be the child for the new node, and change the parent node of that child node to point to the newly added node\.