# Listeners for custom routing accelerators in AWS Global Accelerator<a name="about-custom-routing-listeners"></a>

For a in AWS Global Accelerator, you configure a listener that specifies a range of listener ports with associated protocols that Global Accelerator maps to specific destination Amazon EC2 instances in your VPC subnet endpoints\. When you add a VPC subnet endpoint, Global Accelerator creates a static port mapping between the port ranges that you define for your listener and the destination IP addresses and ports in the subnet\. Then you can use the port mapping to specify your accelerator static IP addresses together with a listener port and protocol to direct user traffic to specific destination Amazon EC2 instance IP addresses and ports in your VPC subnet\. 

You define a listener when you create your , and you can add more listeners at any time\. Each listener can have one or more endpoint groups, one for each AWS Region in which you have VPC subnet endpoints\. A listener in a supports both TCP and UDP protocols\. You specify the protocol or protocols for each destination port range that you define: UDP, TCP, or both UDP and TCP\.

For more information, see [How work in AWS Global Accelerator](about-custom-routing-how-it-works.md)\.

## Adding, editing, or removing a custom routing listener<a name="about-custom-routing-listeners.creating-custom-routing-listeners"></a>

This section explains how to work with custom routing listeners on the AWS Global Accelerator console\. To learn about using API operations with AWS Global Accelerator, see the [AWS Global Accelerator API Reference](https://docs.aws.amazon.com/global-accelerator/latest/api/Welcome.html)\.

## To add a listener for a

The range that you specify when you create a listener defines how many listener port and destination IP address combinations that you can use with your \. For maximum flexibility, we recommend that you specify a large port range\. Each listener port range that you specify must include a minimum of 16 ports\.
**Note**  
After you create a listener, you can edit it to add additional port ranges and associated protocols, but you can't decrease existing port ranges\.

1. Open the Global Accelerator console at [ https://us\-west\-2\.console\.aws\.amazon\.com/ec2/v2/home?region=us\-west\-2\#Global Accelerator:](https://us-west-2.console.aws.amazon.com/ec2/v2/home?region=us-west-2#GlobalAccelerator:)\. 

1. On the **Accelerators** page, choose a \.

1. Choose **Add listener**\.

1. On the **Add listener** page, enter the listener port range that you want to associate with the accelerator\. 

   Listeners support ports 1\-65535\. For maximum flexibility with a , we recommend that you specify a large port range\.

1. Choose **Add listener**\.

## To edit a listener for a

When you edit a listener for a , be aware that you can add additional port ranges and associated protocols, increase existing port ranges, or change protocols, but you can't decrease existing port ranges\.

1. Open the Global Accelerator console at [ https://us\-west\-2\.console\.aws\.amazon\.com/ec2/v2/home?region=us\-west\-2\#Global Accelerator:](https://us-west-2.console.aws.amazon.com/ec2/v2/home?region=us-west-2#GlobalAccelerator:)\. 

1. On the **Accelerators** page, choose an accelerator\.

1. Choose a listener, and then choose **Edit listener**\.

1. On the **Edit listener** page, make the changes that you want to existing port ranges or protocols, or add new port ranges\.

   Be aware that you cannot decrease the range of an existing port range\.

1. Choose **Save**\.

## To remove a listener

1. Open the Global Accelerator console at [ https://us\-west\-2\.console\.aws\.amazon\.com/ec2/v2/home?region=us\-west\-2\#Global Accelerator:](https://us-west-2.console.aws.amazon.com/ec2/v2/home?region=us-west-2#GlobalAccelerator:)\. 

1. On the **Accelerators** page, choose an accelerator\.

1. Choose a listener, and then choose **Remove**\.

1. In the confirmation dialog box, choose **Remove**\.