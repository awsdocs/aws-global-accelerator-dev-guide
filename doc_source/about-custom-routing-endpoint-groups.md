# Endpoint groups for custom routing accelerators in AWS Global Accelerator<a name="about-custom-routing-endpoint-groups"></a>

With a custom routing accelerator in AWS Global Accelerator, an endpoint group defines the ports and protocols that destination Amazon EC2 instances in your virtual private cloud \(VPC\) subnets accept traffic on\.

You create an endpoint group for your custom routing accelerator for each AWS Region in which your VPC subnets and EC2 instances are located\. Each endpoint group in a custom routing accelerator can have multiple VPC subnet endpoints\. Similarly, you can add each VPC to multiple endpoint groups, but the endpoint groups must be associated with different listeners\.

For each endpoint group, you specify a set of one or more port ranges that include the ports that you want to direct traffic to on the EC2 instances in the Region\. For each endpoint group port range, you specify the protocol to use: UDP, TCP, or both UDP and TCP\. This provides maximum flexibility for you, without having to duplicate sets of port ranges for each protocol\. For example, you might have a game server with gaming traffic running over UDP on ports 8080\-8090 while you also have a server listening for chat messages over TCP on port 80\.

To learn more, see [How custom routing accelerators work in AWS Global Accelerator](about-custom-routing-how-it-works.md)\.

## Adding, editing, or removing an endpoint group for a custom routing accelerator<a name="about-custom-routing-endpoint-groups.create-endpoint-group"></a>

You work with an endpoint group for your custom routing accelerator on the AWS Global Accelerator console or by using an API operation\. You can add or remove VPC subnet endpoints from an endpoint group at any time\.

This section explains how to work with endpoint groups for your custom routing accelerator on the AWS Global Accelerator console\. To learn about using API operations with Global Accelerator, see the[ AWS Global Accelerator API Reference](https://docs.aws.amazon.com/global-accelerator/latest/api/Welcome.html)\.

## To add an endpoint group for a custom routing accelerator

1. Open the Global Accelerator console at [ https://us\-west\-2\.console\.aws\.amazon\.com/ec2/v2/home?region=us\-west\-2\#Global Accelerator:](https://us-west-2.console.aws.amazon.com/ec2/v2/home?region=us-west-2#GlobalAccelerator:)\. 

1. On the **Accelerators** page, choose a custom routing accelerator\.

1. In the **Listeners** section, for **Listener ID**, choose the ID of the listener that you want to add an endpoint group to\.

1. Choose **Add endpoint group**\.

1. In the section for a listener, specify a Region for the endpoint group\.

1. For **Ports and protocols sets**, enter port ranges and protocols for your Amazon EC2 instances\.
   + Enter a **From port** and a **To port** to specify a range of ports\.
   + For each port range, specify the protocol or protocols for that range\.

   The port range doesn't have to be a subset of your listener port range, but there must be enough total ports in the listener port range to support the total number of ports that you specify for the endpoint groups in your custom routing accelerator\.

1. Choose **Save**\.

1. Optionally, choose **Add endpoint group** to add additional endpoint groups for this listener\. You can also choose another listener and add endpoint groups\.

1. Choose **Add endpoint group**\.

## To edit an endpoint group for a custom routing accelerator

1. Open the Global Accelerator console at [ https://us\-west\-2\.console\.aws\.amazon\.com/ec2/v2/home?region=us\-west\-2\#Global Accelerator:](https://us-west-2.console.aws.amazon.com/ec2/v2/home?region=us-west-2#GlobalAccelerator:)\. 

1. On the **Accelerators** page, choose a custom routing accelerator\.

1. In the **Listeners** section, for **Listener ID**, choose the ID of the listener that the endpoint group is associated with\.

1. Choose **Edit endpoint group**\.

1. On the **Edit endpoint group** page, change the Region, the range of ports, or the protocol for a range of ports\.

1. Choose **Save**\.

## To remove a custom routing accelerator

1. Open the Global Accelerator console at [ https://us\-west\-2\.console\.aws\.amazon\.com/ec2/v2/home?region=us\-west\-2\#Global Accelerator:](https://us-west-2.console.aws.amazon.com/ec2/v2/home?region=us-west-2#GlobalAccelerator:)\. 

1. On the **Accelerators** page, choose an accelerator\.

1. In the **Listeners** section, choose a listener, and then choose **Remove**\.

1. In the **Endpoint groups** section, choose an endpoint group, and then choose **Remove**\.

1. On the confirmation dialog box, choose **Remove**\.