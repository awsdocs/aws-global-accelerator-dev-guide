# Standard accelerators in AWS Global Accelerator<a name="about-accelerators"></a>

A *standard accelerator* in AWS Global Accelerator directs traffic to optimal endpoints over the AWS global network to improve the availability and performance of your internet applications that have a global audience\. Each accelerator includes one or more listeners\. A listener processes inbound connections from clients to Global Accelerator, based on the protocol \(or protocols\) and port \(or port range\) that you configure\. 

When you create an accelerator, by default, Global Accelerator provides you with a set of two static IP addresses\. If you bring your own IP address range to AWS \(BYOIP\), you can instead assign static IP addresses from your own pool to use with your accelerator\. For more information, see [Bring your own IP addresses \(BYOIP\) in AWS Global Accelerator](using-byoip.md)\.

**Important**  
The IP addresses are assigned to your accelerator for as long as it exists, even if you disable the accelerator and it no longer accepts or routes traffic\. However, when you *delete* an accelerator, you lose the Global Accelerator static IP addresses that are assigned to the accelerator, so you can no longer route traffic by using them\. As a best practice, ensure that you have permissions in place to avoid inadvertently deleting accelerators\. You can use IAM policies with Global Accelerator, for example, tag\-based permissions, to limit the users who have permissions to delete an accelerator\. For more information, see [ Tag\-based policies](auth-and-access-control.md#access-control-manage-access-tag-policies)\.

This section explains how to create, edit, or delete a standard accelerator on the Global Accelerator console\. If you want to use API operations with Global Accelerator, see the [ AWS Global Accelerator API Reference](https://docs.aws.amazon.com/global-accelerator/latest/api/Welcome.html)\.

**Topics**
+ [Creating or updating a standard accelerator](#about-accelerators.creating-editing)
+ [Deleting an accelerator](#about-accelerators.deleting)
+ [Viewing your accelerators](about-accelerators.viewing.md)
+ [Add an accelerator when you create a load balancer](about-accelerators.alb-accelerator.md)
+ [Using global static IP addresses instead of regional static IP addresses](about-accelerators.eip-accelerator.md)
+ [Bring your own IP addresses \(BYOIP\) in AWS Global Accelerator](using-byoip.md)

## Creating or updating a standard accelerator<a name="about-accelerators.creating-editing"></a>

This section explains how to create or update standard accelerators on the console\. To work with Global Accelerator programmatically, see the [AWS Global Accelerator API Reference](https://docs.aws.amazon.com/global-accelerator/latest/api/Welcome.html)\.

**Important**  
Make sure that you’re in the US West \(Oregon\) Region\. You must be in this Region to create or update accelerators\.

## To create a standard accelerator

1. Open the Global Accelerator console at [ https://us\-west\-2\.console\.aws\.amazon\.com/ec2/v2/home?region=us\-west\-2\#Global Accelerator:](https://us-west-2.console.aws.amazon.com/ec2/v2/home?region=us-west-2#GlobalAccelerator:)\. 

1. Choose **Create accelerator**\.

1. Provide a name for your accelerator\.

1. Optionally, if you have brought your own IP address range to AWS \(BYOIP\), you can specify static IP addresses for your accelerator from that address pool\. Make this choice for each of the two static IP addresses for your accelerator\.
   + For each static IP address, choose the IP address pool to use\.
   + If you chose your own IP address pool, also choose a specific IP address from the pool\. If you chose the default Amazon IP address pool, Global Accelerator assigns a specific IP address to your accelerator\.

1. Optionally, add one or more tags to help you identify your accelerator resources\.

1. Choose **Next** to add listeners, endpoint groups, and endpoints\.

## To edit a standard accelerator

1. Open the Global Accelerator console at [ https://us\-west\-2\.console\.aws\.amazon\.com/ec2/v2/home?region=us\-west\-2\#Global Accelerator:](https://us-west-2.console.aws.amazon.com/ec2/v2/home?region=us-west-2#GlobalAccelerator:)\. 

1. In the list of accelerators, choose one, and then choose **Edit**\.

1. On the **Edit accelerator** page, make any changes that you like\. For example, you can disable the accelerator so that it no longer accepts or routes traffic, or so that you can delete it\. Or, if the accelerator is disabled, you can enable it\.

1. Choose **Save changes**\.

## Deleting an accelerator<a name="about-accelerators.deleting"></a>

If you created an accelerator as a test or if you're no longer using an accelerator, you can delete it\. On the console, disable the accelerator, and then you can delete it\. You don't have to remove listeners and endpoint groups from the accelerator\.

**Important**  
Global Accelerator is a global service that can front application endpoints in multiple AWS Regions but you must be in the US West \(Oregon\) Region to delete accelerators by using the AWS Management Console or AWS CLI\.

To delete an accelerator by using an API operation instead of the console, you must first remove all listeners and endpoint groups that are associated with the accelerator, and then disable it\. For more information, see the [DeleteAccelerator](https://docs.aws.amazon.com/global-accelerator/latest/api/API_DeleteAccelerator.html) operation in the *AWS Global Accelerator API Reference*\.

## To disable an accelerator

1. Open the Global Accelerator console at [ https://us\-west\-2\.console\.aws\.amazon\.com/ec2/v2/home?region=us\-west\-2\#Global Accelerator:](https://us-west-2.console.aws.amazon.com/ec2/v2/home?region=us-west-2#GlobalAccelerator:)\. 

1. In the list, choose an accelerator that you want to disable\.

1. Choose **Edit**\.

1. Choose **Disable accelerator**, and then choose **Save**\.

## To delete an accelerator

1. Open the Global Accelerator console at [ https://us\-west\-2\.console\.aws\.amazon\.com/ec2/v2/home?region=us\-west\-2\#Global Accelerator:](https://us-west-2.console.aws.amazon.com/ec2/v2/home?region=us-west-2#GlobalAccelerator:)\. 

1. In the list, choose an accelerator that you want to delete\.

1. Choose **Delete**\.
**Note**  
If you haven't disabled the accelerator, **Delete** is unavailable\.

1. In the confirmation dialog box, choose **Delete**\.
**Important**  
When you delete an accelerator, you lose the static IP addresses that are assigned to the accelerator, so you can no longer route traffic by using them\.