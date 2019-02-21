# Creating, Editing, or Deleting an Accelerator<a name="about-accelerators.creating-editing"></a>

This section explains how to work with accelerators on the console\. To work with Global Accelerator programmatically, see the [AWS Global Accelerator API Reference](https://docs.aws.amazon.com/global-accelerator/latest/api/Welcome.html)\.

# To create an accelerator

1. Open the Global Accelerator console at [ https://us\-west\-2\.console\.aws\.amazon\.com/ec2/v2/home?region=us\-west\-2\#Global Accelerator:](https://us-west-2.console.aws.amazon.com/ec2/v2/home?region=us-west-2#GlobalAccelerator:)\. 

1. Choose **Create accelerator**\.

1. Provide a name for your accelerator\.

1. Choose **Next** to add listeners, endpoint groups, and endpoints\.

# To edit an accelerator

1. Open the Global Accelerator console at [ https://us\-west\-2\.console\.aws\.amazon\.com/ec2/v2/home?region=us\-west\-2\#Global Accelerator:](https://us-west-2.console.aws.amazon.com/ec2/v2/home?region=us-west-2#GlobalAccelerator:)\. 

1. In the list of accelerators, choose one, and then choose **Edit**\.

1. On the **Edit accelerator** page, make any changes that you like\. For example, you can disable the accelerator so that you can delete it\.

1. Choose **Save**\.

If you created an accelerator as a test or if you're no longer using an accelerator, you can delete it\. On the console, disable the accelerator, and then you can delete it\. You don't have to remove listeners and endpoint groups from the accelerator\.

To delete an accelerator by using an API operation instead of the console, you must first remove all listeners and endpoint groups that are associated with the accelerator, and then disable it\. For more information, see the [ `DeleteAccelerator`](https://docs.aws.amazon.com/global-accelerator/latest/api/API_DeleteAccelerator.html) operation in the *AWS Global Accelerator API Reference*\.

# To disable an accelerator

1. Open the Global Accelerator console at [ https://us\-west\-2\.console\.aws\.amazon\.com/ec2/v2/home?region=us\-west\-2\#Global Accelerator:](https://us-west-2.console.aws.amazon.com/ec2/v2/home?region=us-west-2#GlobalAccelerator:)\. 

1. In the list, choose an accelerator that you want to disable\.

1. Choose **Edit**\.

1. Choose **Disable accelerator**, and then choose **Save**\.

# To delete an accelerator

1. Open the Global Accelerator console at [ https://us\-west\-2\.console\.aws\.amazon\.com/ec2/v2/home?region=us\-west\-2\#Global Accelerator:](https://us-west-2.console.aws.amazon.com/ec2/v2/home?region=us-west-2#GlobalAccelerator:)\. 

1. In the list, choose an accelerator that you want to delete\.

1. Choose **Delete**\.
**Note**  
If you haven't disabled the accelerator, **Delete** is unavailable\.

1. In the confirmation dialog box, choose **Delete**\.