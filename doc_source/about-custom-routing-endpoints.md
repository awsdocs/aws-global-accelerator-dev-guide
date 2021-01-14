# VPC subnet endpoints for in AWS Global Accelerator<a name="about-custom-routing-endpoints"></a>

Endpoints for define the virtual private cloud \(VPC\) subnets that can receive traffic through a \. Each subnet can contain one or many Amazon EC2 instance destinations\. When you add a VPC subnet endpoint, Global Accelerator generates new port mappings that you can use to route traffic to the destination EC2 instance IP addresses in the subnet\. Then you can use the Global Accelerator API to get a static list of all the port mappings for the subnet\. For more information, see [ListCustomRoutingPortMappings](https://docs.aws.amazon.com/global-accelerator/latest/api/API_ListCustomRoutingPortMappings.html)\.

You can only direct traffic to EC2 instances in the subnets, not other resources like load balancers \(in contrast to standard accelerators\)\. The EC2 instance types that are supported are listed in [Endpoints for standard accelerators in AWS Global Accelerator](about-endpoints.md)\.

By default, traffic directed through a can't arrive at any destinations in your subnet\. To enable destination instances to receive traffic, you must specifically allow all traffic to the subnet or, alternatively, enable traffic to specific instance IP addresses and ports in the subnet\. To enable traffic to specific destinations, you must use the Global Accelerator API\. For more information, see [AllowCustomRoutingTraffic](https://docs.aws.amazon.com/global-accelerator/latest/api/API_AllowCustomRoutingTraffic.html) and [DenyCustomRoutingTraffic](https://docs.aws.amazon.com/global-accelerator/latest/api/API_DenyCustomRoutingTraffic.html)\.

**Important**  
Updating a subnet or specific destination to allow or deny traffic takes time to propagate across the internet\. To determine if a change has propagated, you can call the `DescribeCustomRoutingAccelerator` API action to check the accelerator status\. For more information, see [ DescribeCustomRoutingAccelerator](https://docs.aws.amazon.com/global-accelerator/latest/api/API_DescribeCustomRoutingAccelerator.html)

To learn more, see [How work in AWS Global Accelerator](about-custom-routing-how-it-works.md)\.

Because VPC subnets preserve the client IP address, be aware of the information in the following section when you add subnets as endpoints for : [ Adding endpoints with client IP address preservation](about-endpoints.sipp-caveats.md)\. 

## Adding, editing, or removing a VPC subnet endpoint<a name="about-custom-routing-endpoints-adding-endpoints"></a>

You add virtual private cloud \(VPC\) subnet endpoints to endpoint groups in your so that you can direct user traffic to destination Amazon EC2 instances in the subnet\. 

When you add and remove EC2 instances from the subnet, or enable or disable traffic to EC2 destinations, you change whether those destinations can receive traffic\. However the Global Accelerator port list mapping doesn't change\.

You can remove the VPC subnet from your accelerator by removing it from an endpoint group\. Removing a subnet doesn't affect the subnet itself, but Global Accelerator can no longer direct traffic to the subnet or to the Amazon EC2 instances in it\. In addition, Global Accelerator will reclaim the port mappings for the VPC subnet to potentially use them for new subnets that you add\.

The steps in this section explain how to add or remove VPC subnet endpoints on the AWS Global Accelerator console\. To learn about using API operations with AWS Global Accelerator, see the [AWS Global Accelerator API Reference](https://docs.aws.amazon.com/global-accelerator/latest/api/Welcome.html)\.

## To add a VPC subnet endpoint

1. Open the Global Accelerator console at [ https://us\-west\-2\.console\.aws\.amazon\.com/ec2/v2/home?region=us\-west\-2\#Global Accelerator:](https://us-west-2.console.aws.amazon.com/ec2/v2/home?region=us-west-2#GlobalAccelerator:)\. 

1. On the **Accelerators** page, choose a \.

1. In the **Listeners** section, for **Listener ID**, choose the ID of a listener\.

1. In the **Endpoint groups** section, for **Endpoint group ID**, choose the ID of the endpoint group \(AWS Region\) that you want to add the VPC subnet endpoint to\.

1. In the **Endpoints** section, choose **Add endpoint**\.

1. On the **Add endpoints** page, for **Endpoint**, choose a VPC subnet\.

   If you don't have any VPCs, there aren't any items in the list\. To continue, add at least one VPC, then come back to the steps here, and choose a VPC from the list\.

1. Choose **Add endpoint**\.

## To edit a VPC subnet endpoint

You can edit an endpoint to enable or disable traffic to all destinations in the VPC subnet\. 

To enable or disable traffic to specific destinations in the subnet, you must use the Global Accelerator API\. For more information, see [AllowCustomRoutingTraffic](https://docs.aws.amazon.com/global-accelerator/latest/api/API_AllowCustomRoutingTraffic.html) and [DenyCustomRoutingTraffic](https://docs.aws.amazon.com/global-accelerator/latest/api/API_DenyCustomRoutingTraffic.html)\.

1. Open the Global Accelerator console at [ https://us\-west\-2\.console\.aws\.amazon\.com/ec2/v2/home?region=us\-west\-2\#Global Accelerator:](https://us-west-2.console.aws.amazon.com/ec2/v2/home?region=us-west-2#GlobalAccelerator:)\. 

1. On the **Accelerators** page, choose a \.

1. In the **Listeners** section, for **Listener ID**, choose the ID of a listener\.

1. In the **Endpoint groups** section, for **Endpoint group ID**, choose the ID of the endpoint group \(AWS Region\) of the VPC subnet endpoint that you want to edit\.

1. Choose **Edit endpoint**\.

1. On the **Edit endpoint** page, make updates, and then choose **Save**\.

## To remove an endpoint

1. Open the Global Accelerator console at [ https://us\-west\-2\.console\.aws\.amazon\.com/ec2/v2/home?region=us\-west\-2\#Global Accelerator:](https://us-west-2.console.aws.amazon.com/ec2/v2/home?region=us-west-2#GlobalAccelerator:)\. 

1. On the **Accelerators** page, choose a \.

1. In the **Listeners** section, for **Listener ID**, choose the ID of a listener\.

1. In the **Endpoint groups** section, for **Endpoint group ID**, choose the ID of the endpoint group \(AWS Region\) of the VPC subnet endpoint that you want to remove\.

1. Choose **Remove endpoint**\.

1. In the confirmation dialog box, choose **Remove**\.