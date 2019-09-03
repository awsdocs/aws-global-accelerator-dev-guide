# Accelerators in AWS Global Accelerator<a name="about-accelerators"></a>

An *accelerator* in AWS Global Accelerator directs traffic to optimal endpoints over the AWS global network to improve the availability and performance of your internet applications that have a global audience\. Each accelerator includes one or more listeners\. A listener processes inbound connections from clients to Global Accelerator, based on the protocol and port that you configure\. 

When you provide a name for your accelerator and create it, Global Accelerator provisions two static IP addresses for you\. The static IP addresses are anycast from the AWS edge network to your endpoints such as Elastic IP addresses, Network Load Balancers, or Application Load Balancers\. You then associate those static IP addresses with your accelerator\. After you create your accelerator, you can edit it to change the name, or you can delete it when you no longer need it\.

This section explains how to work with an accelerator on the Global Accelerator console\. If you want to use API operations with Global Accelerator, see the [ AWS Global Accelerator API Reference](https://docs.aws.amazon.com/global-accelerator/latest/api/Welcome.html)\.

**Topics**
+ [Static IP Addresses in AWS Global Accelerator](#about-static-ip-addresses)
+ [Creating, Editing, or Deleting an Accelerator](#about-accelerators.creating-editing)
+ [Viewing Your Accelerators](#about-accelerators.viewing)

## Static IP Addresses in AWS Global Accelerator<a name="about-static-ip-addresses"></a>

Static IP addresses for Global Accelerator are advertised globally using anycast from edge locations\. You associate the addresses with Elastic Load Balancing resources or Elastic IP addresses that run in a single AWS Region or multiple Regions\. By using static IP addresses, you can onboard internet traffic to the AWS global network close to where your users are, regardless of their location\. Using the AWS global network improves availability and performance because traffic doesn't have to take multiple hops over the public internet\.

Using static IP addresses also makes it easier to add your application to more Regions or to migrate applications between AWS Regions\. Using fixed IP addresses means that users have a consistent way to connect to your application\.

AWS Global Accelerator provides static IP addresses for you\. The first step in creating your accelerator is to provision the static IP addresses by entering a name for your accelerator\.  After you provision the addresses to create your accelerator, you can edit or delete the accelerator\. To create an accelerator, see [ Creating, Editing, or Deleting an Accelerator](#about-accelerators.creating-editing)\.

## Creating, Editing, or Deleting an Accelerator<a name="about-accelerators.creating-editing"></a>

This section explains how to work with accelerators on the console\. To work with Global Accelerator programmatically, see the [AWS Global Accelerator API Reference](https://docs.aws.amazon.com/global-accelerator/latest/api/Welcome.html)\.

**Important**  
Make sure that you’re in the US\-West\-2 \(Oregon\) Region\. You must be in this Region to create or update accelerators\.

## To create an accelerator

1. Open the Global Accelerator console at [ https://us\-west\-2\.console\.aws\.amazon\.com/ec2/v2/home?region=us\-west\-2\#Global Accelerator:](https://us-west-2.console.aws.amazon.com/ec2/v2/home?region=us-west-2#GlobalAccelerator:)\. 

1. Choose **Create accelerator**\.

1. Provide a name for your accelerator\.

1. Choose **Next** to add listeners, endpoint groups, and endpoints\.

## To edit an accelerator

1. Open the Global Accelerator console at [ https://us\-west\-2\.console\.aws\.amazon\.com/ec2/v2/home?region=us\-west\-2\#Global Accelerator:](https://us-west-2.console.aws.amazon.com/ec2/v2/home?region=us-west-2#GlobalAccelerator:)\. 

1. In the list of accelerators, choose one, and then choose **Edit**\.

1. On the **Edit accelerator** page, make any changes that you like\. For example, you can disable the accelerator so that you can delete it\.

1. Choose **Save**\.

If you created an accelerator as a test or if you're no longer using an accelerator, you can delete it\. On the console, disable the accelerator, and then you can delete it\. You don't have to remove listeners and endpoint groups from the accelerator\.

To delete an accelerator by using an API operation instead of the console, you must first remove all listeners and endpoint groups that are associated with the accelerator, and then disable it\. For more information, see the [ `DeleteAccelerator`](https://docs.aws.amazon.com/global-accelerator/latest/api/API_DeleteAccelerator.html) operation in the *AWS Global Accelerator API Reference*\.

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

## Viewing Your Accelerators<a name="about-accelerators.viewing"></a>

You can view information about your accelerators on the console\. To see descriptions of your accelerators programmatically, see [ `ListAccelerators`](https://docs.aws.amazon.com/global-accelerator/latest/api/API_ListAccelerators.html) and [ `DescribeAccelerator`](https://docs.aws.amazon.com/global-accelerator/latest/api/API_DescribeAccelerator.html) in the *AWS Global Accelerator API Reference*\.

## To view information about your accelerator

1. Open the Global Accelerator console at [ https://us\-west\-2\.console\.aws\.amazon\.com/ec2/v2/home?region=us\-west\-2\#Global Accelerator:](https://us-west-2.console.aws.amazon.com/ec2/v2/home?region=us-west-2#GlobalAccelerator:)\. 

1. To see details about an accelerator, in the list, choose an accelerator, and then choose **View**\.