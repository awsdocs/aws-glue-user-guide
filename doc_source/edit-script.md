# Editing or uploading a job script<a name="edit-script"></a>

Use the AWS Glue Studio visual editor to edit the job script or upload your own script\.

You can use the visual editor to edit job nodes only if the jobs were created with AWS Glue Studio\. If the job was created using the AWS Glue console, through API commands, or with the command line interface \(CLI\), you can use the code editor in AWS Glue Studio to edit the job script, parameters, and schedule\. You can also edit the script for a job created in AWS Glue Studio by converting the job to script\-only mode\.

**To edit the job script or upload your own script**

1. If creating a new job, on the **Jobs** page, choose the **Code editor** option\. In the **Developer mode options** section that appears, you can choose to either start with a blank script \(**Write code in an editor**\), or you can upload a local file to use as the job script\.

   You can choose only Python or Scala scripts to upload\. Scala scripts must have the file extension `.scala`\. Python scripts must be recognized as files of type Python\. 

1. Go to the visual job editor for the new or saved job, and then choose the **Script** tab\.

1. If you didn't create a new job using the **Code editor** option, and you have never edited the script for an existing job, the **Script** tab displays the heading **Script \(Locked\)**\. This means the script editor is in read\-only mode\. Choose **Edit script** to unlock the script for editing\.

   To make the script editable, AWS Glue Studio converts your job from a visual job to a script\-only job\. If you unlock the script for editing, you can't use the visual editor for this job afterwards\.

   In the confirmation window, choose **Confirm** to continue or **Cancel** to keep the job available for visual editing\.

   If you choose **Confirm**, the Visual tab no longer appears in the editor\. You can use AWS Glue Studio to modify the script using the code editor, modify the job details or schedule, or view job runs\.
**Note**  
Until you save the job, the change is not permanent\. If you close the job before saving it and reopen it in the visual editor, you will still be able to edit the individual nodes in the visual editor\.

1. Edit the script as needed\. 

   When you are done editing the script, choose **Save** to save the job and permanently convert the job from visual to script\-only\.

1. \(Optional\) You can download the script from the AWS Glue Studio console by choosing the **Download** button on the **Script** tab\. When you choose this button, a new browser window opens, displaying the script from its location in Amazon S3\. The **Script filename** and **Script path** parameters in the **Job details** tab of the job determine the name and location of the script file in Amazon S3\.   
![\[\]](http://docs.aws.amazon.com/glue/latest/ug/images/job-details-script-location-params-screenshot.png)

   When you save the job, AWS Glue save the job script at the location specified by these fields\. If you modify the script file at this location within Amazon S3, AWS Glue Studio will load the modified script the next time you edit the job\.