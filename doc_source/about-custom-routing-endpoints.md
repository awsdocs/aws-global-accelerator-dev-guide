# VPC subnet endpoints for custom routing accelerators in AWS Global Accelerator<a name="about-custom-routing-endpoints"></a>

Endpoints for custom routing accelerators are virtual private cloud \(VPC\) subnets that can receive traffic through an accelerator\. Each subnet can contain one or many Amazon EC2 instance destinations\. When you add a subnet endpoint, Global Accelerator generates new port mapping\. Then you can use the Global Accelerator API to get a static list of all the port mappings for the subnet, which you can use to route traffic to destination EC2 instance IP addresses in the subnet\. For more information, see [ListCustomRoutingPortMappings](https://docs.aws.amazon.com/global-accelerator/latest/api/API_ListCustomRoutingPortMappings.html)\.

You can only direct traffic to EC2 instances in the subnets, not other resources like load balancers \(in contrast to standard accelerators\)\. The EC2 instance types that are supported are listed in [Endpoints for standard accelerators in AWS Global Accelerator](about-endpoints.md)\.

To learn more, see [How custom routing accelerators work in AWS Global Accelerator](about-custom-routing-how-it-works.md)\.

Be aware of the following when you add VPC subnets for your custom routing accelerator:
+ By default, traffic directed through a custom routing accelerator can't arrive at any destinations in your subnet\. To enable destination instances to receive traffic, you must choose to allow all traffic to the subnet or, alternatively, enable traffic to specific instance IP addresses and ports \(destination sockets\) in the subnet\. 
**Important**  
Updating a subnet or specific destination to allow or deny traffic takes time to propagate across the internet\. To determine if a change has propagated, you can call the `DescribeCustomRoutingAccelerator` API action to check the accelerator status\. For more information, see [ DescribeCustomRoutingAccelerator](https://docs.aws.amazon.com/global-accelerator/latest/api/API_DescribeCustomRoutingAccelerator.html)\.
+ Because VPC subnets preserve the client IP address, you should review the relevant security and configuration information when you add subnets as endpoints for custom routing accelerators\. For more information, see [ Adding endpoints with client IP address preservation](about-endpoints.sipp-caveats.md)\. 

## Adding, editing, or removing a VPC subnet endpoint<a name="about-custom-routing-endpoints-adding-endpoints"></a>

You add virtual private cloud \(VPC\) subnet endpoints to endpoint groups in your custom routing accelerators so that you can direct user traffic to destination Amazon EC2 instances in the subnet\. 

When you add and remove EC2 instances from the subnet, or enable or disable traffic to EC2 destinations, you change whether those destinations can receive traffic\. However the Global Accelerator port mapping doesn't change\.

To allow traffic to some destinations in the subnet, but not all, enter IP addresses for each EC2 instance that you want to allow, along with the ports on the instance that you want to receive traffic\. The IP addresses that you specify must be for EC2 instances in the subnet\. You can specify a port or range of ports, from the ports that are mapped for the subnet\.

You can remove the VPC subnet from your accelerator by removing it from an endpoint group\. Removing a subnet doesn't affect the subnet itself, but Global Accelerator can no longer direct traffic to the subnet or to the Amazon EC2 instances in it\. In addition, Global Accelerator will reclaim the port mapping for the VPC subnet to potentially use them for new subnets that you add\.

The steps in this section explain how to add, edit, or remove VPC subnet endpoints on the AWS Global Accelerator console\. To learn about using API operations with AWS Global Accelerator, see the [AWS Global Accelerator API Reference](https://docs.aws.amazon.com/global-accelerator/latest/api/Welcome.html)\.

## To add a VPC subnet endpoint

1. Open the Global Accelerator console at [ https://us\-west\-2\.console\.aws\.amazon\.com/ec2/v2/home?region=us\-west\-2\#Global Accelerator:](https://us-west-2.console.aws.amazon.com/ec2/v2/home?region=us-west-2#GlobalAccelerator:)\. 

1. On the **Accelerators** page, choose a custom routing accelerator\.

1. In the **Listeners** section, for **Listener ID**, choose the ID of a listener\.

1. In the **Endpoint groups** section, for **Endpoint group ID**, choose the ID of the endpoint group \(AWS Region\) that you want to add the VPC subnet endpoint to\.

1. In the **Endpoints** section, choose **Add endpoint**\.

1. On the **Add endpoints** page, for **Endpoint**, choose a VPC subnet\.

   If you don't have any VPCs, there aren't any items in the list\. To continue, add at least one VPC, then come back to the steps here, and choose a VPC from the list\.

1. For VPC subnet endpoint that you add, you can choose to allow or deny traffic to all destinations in the subnet, or you can allow traffic to only specific EC2 instances and ports\. The default is to deny traffic to all destinations in the subnet\.

1. Choose **Add endpoint**\.

## To allow or deny traffic to specific destinations

You can edit the VPC subnet port mapping for an endpoint to allow or deny traffic to specific EC2 instances and ports \(destination sockets\) in a subnet\. 

1. Open the Global Accelerator console at [ https://us\-west\-2\.console\.aws\.amazon\.com/ec2/v2/home?region=us\-west\-2\#Global Accelerator:](https://us-west-2.console.aws.amazon.com/ec2/v2/home?region=us-west-2#GlobalAccelerator:)\. 

1. On the **Accelerators** page, choose a custom routing accelerator\.

1. In the **Listeners** section, for **Listener ID**, choose the ID of a listener\.

1. In the **Endpoint groups** section, for **Endpoint group ID**, choose the ID of the endpoint group \(AWS Region\) of the VPC subnet endpoint that you want to edit\.

1. Choose an endpoint subnet, and then choose **View details**\.

1. On the **Endpoint** page, under **Port mappings**, choose an IP address, and then choose **Edit**\.

1. Enter the ports that you want to enable traffic for, and then choose **Allow these destinations**\.

## To allow or deny ALL traffic to a subnet

You can update an endpoint to allow or deny traffic to all destinations in the VPC subnet\. 

1. Open the Global Accelerator console at [ https://us\-west\-2\.console\.aws\.amazon\.com/ec2/v2/home?region=us\-west\-2\#Global Accelerator:](https://us-west-2.console.aws.amazon.com/ec2/v2/home?region=us-west-2#GlobalAccelerator:)\. 

1. On the **Accelerators** page, choose a custom routing accelerator\.

1. In the **Listeners** section, for **Listener ID**, choose the ID of a listener\.

1. In the **Endpoint groups** section, for **Endpoint group ID**, choose the ID of the endpoint group \(AWS Region\) of the VPC subnet endpoint that you want to update\.

1. Choose **Allow/Deny all traffic**\. 

1. Choose an option, to allow all traffic or deny all traffic, and then choose **Save**\.

## To remove an endpoint

1. Open the Global Accelerator console at [ https://us\-west\-2\.console\.aws\.amazon\.com/ec2/v2/home?region=us\-west\-2\#Global Accelerator:](https://us-west-2.console.aws.amazon.com/ec2/v2/home?region=us-west-2#GlobalAccelerator:)\. 

1. On the **Accelerators** page, choose a custom routing accelerator\.

1. In the **Listeners** section, for **Listener ID**, choose the ID of a listener\.

1. In the **Endpoint groups** section, for **Endpoint group ID**, choose the ID of the endpoint group \(AWS Region\) of the VPC subnet endpoint that you want to remove\.

1. Choose **Remove endpoint**\.

1. In the confirmation dialog box, choose **Remove**\.