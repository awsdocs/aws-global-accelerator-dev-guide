# Endpoints in AWS Global Accelerator<a name="about-endpoints"></a>

Endpoints in AWS Global Accelerator can be Network Load Balancers, Application Load Balancers, EC2 instances, or Elastic IP addresses\. A static IP address serves as a single point of contact for clients, and Global Accelerator then distributes incoming traffic across healthy endpoints\. Global Accelerator directs traffic to endpoints by using the port \(or port range\) that you specify for the listener that the endpoint group for the endpoint belongs to\. 

Each endpoint group can have multiple endpoints\. You can add each endpoint to multiple endpoint groups, but the endpoint groups must be associated with different listeners\.

Global Accelerator continually monitors the health of all endpoints that are included in an endpoint group\. It routes traffic only to the active endpoints that are healthy\. If Global Accelerator doesn’t have any healthy endpoints to route traffic to, it routes traffic to all endpoints\.

Be aware of the following for specific types of Global Accelerator endpoints:

**Application Load Balancer endpoints**  
+ An Application Load Balancer endpoint can be internet\-facing or internal\.

**EC2 instance endpoints**  
+ An EC2 instance endpoint can't be one of the following types: C1, CC1, CC2, CG1, CG2, CR1, CS1, G1, G2, HI1, HS1, M1, M2, M3, or T1\.
+ EC2 instances are supported as endpoints in only some AWS Regions\. For a list of supported Regions, see [ Supported Regions for Client IP Address Preservation](preserve-client-ip-address.regions.md)\.
+ We recommend that you remove an EC2 instance from Global Accelerator endpoint groups before you terminate the instance\. If you terminate an EC2 instance before you remove it from an endpoint group in Global Accelerator, and then you create another instance in the same VPC with the same private IP address, and health checks pass, Global Accelerator will route traffic to the new endpoint\. 

A feature that you can use with some endpoint types—in some Regions— is *client IP address preservation*\. With this feature, you preserve the source IP address of the original client for packets that arrive at the endpoint\. You can use this feature with Application Load Balancer and EC2 instance endpoints\. For more information, see [Preserve Client IP Addresses in AWS Global Accelerator](preserve-client-ip-address.md)\.

If you intend to use the client IP address preservation feature, be aware of the following when you add endpoints to Global Accelerator:

**Elastic network interfaces**  
To support client IP address preservation, Global Accelerator creates elastic network interfaces in your AWS account—one for each subnet where an endpoint is present\. For more information about how Global Accelerator works with elastic network interfaces, see [Best Practices for Client IP Address Preservation](best-practices-aga.md)\.

**Endpoints in private subnets**  
You can target an Application Load Balancer or an EC2 instance in a private subnet using AWS Global Accelerator but you must have an [internet gateway](https://docs.aws.amazon.com/vpc/latest/userguide/VPC_Internet_Gateway.html) attached to the VPC that contains the endpoints\. For more information, see [Secure VPC Connections in AWS Global Accelerator](secure-vpc-connections.md)\.

**Whitelist the client IP address**  
Before you add and begin to route traffic to endpoints that preserve the client IP address, make sure that all your required security configurations, for example, security groups, are updated to whitelist the user client IP address\. Network access control lists \(ACLs\) only apply to egress \(outbound\) traffic\. If you need to filter ingress \(inbound\) traffic, you must use security groups\. 

**Topics**
+ [Adding, Editing, or Removing an Endpoint](#about-endpoints-adding-endpoints)
+ [Endpoint Weights](about-endpoints-endpoint-weights.md)
+ [Transitioning Endpoints to Use Client IP Address Preservation](about-endpoints.transition-to-IP-preservation.md)

## Adding, Editing, or Removing an Endpoint<a name="about-endpoints-adding-endpoints"></a>

You add endpoints to endpoint groups so that traffic can be directed to your resources\. You can edit an endpoint to change the weight for the endpoint\. Or you can remove an endpoint from your accelerator by removing it from an endpoint group\. Removing an endpoint doesn't affect the endpoint itself, but Global Accelerator can no longer direct traffic to that resource\.

You can add or remove endpoints from endpoint groups based on usage\. For example, if demand on your application increases, you can add more endpoints to one or more endpoint groups to handle the increased traffic\. Global Accelerator starts routing requests to an endpoint as soon as you add it and the endpoint passes the initial health checks\. You can manage traffic to endpoints by adjusting the weights on an endpoint, to send proportionally more or less traffic to the endpoint\.

You can remove endpoints from your endpoint groups, for example, if you need to service your endpoints\. Removing an endpoint takes it out of the endpoint group, but does not affect the endpoint otherwise\. Global Accelerator stops directing traffic to an endpoint as soon as you remove it from an endpoint group\. The endpoint goes into a state where it waits for all current requests to be completed so there's no interruption for client traffic that is in progress\. You can add the endpoint back to the endpoint group when you’re ready for it to resume receiving requests\.

This section explains how to work with endpoints on the AWS Global Accelerator console\. If you want to use API operations with AWS Global Accelerator, see the [ AWS Global Accelerator API Reference](https://docs.aws.amazon.com/global-accelerator/latest/api/Welcome.html)\.

## To add an endpoint

1. Open the Global Accelerator console at [ https://us\-west\-2\.console\.aws\.amazon\.com/ec2/v2/home?region=us\-west\-2\#Global Accelerator:](https://us-west-2.console.aws.amazon.com/ec2/v2/home?region=us-west-2#GlobalAccelerator:)\. 

1. On the **accelerators** page, choose an accelerator\.

1. In the **Listeners** section, for **Listener ID**, choose the ID of a listener\.

1. In the **Endpoint groups** section, for **Endpoint group ID**, choose the ID of the endpoint group that you want to add an endpoint to\.

1. In the **Endpoints** section, choose **Add endpoint**\.

1. On the **Add endpoints** page, choose an endpoint from the dropdown list\.

1. Optionally, for **Weight**, enter a number from 0 to 255 to set a weight for routing traffic to this endpoint\. When you add weights to endpoints, you configure Global Accelerator to route traffic based on proportions that you specify\. By default, all endpoints have a weight of 128\. For more information, see [Endpoint Weights](about-endpoints-endpoint-weights.md)\.

1. Optionally, enable client IP address preservation for an internet\-facing Application Load Balancer endpoint\. Under **Preserve client IP address**, select **Preserve address**\. 

   This option is always selected for internal Application Load Balancer and EC2 instance endpoints, and never selected for Network Load Balancer and Elastic IP address endpoints\. For more information, see [Preserve Client IP Addresses in AWS Global Accelerator](preserve-client-ip-address.md)\.
**Note**  
Before you add and begin to route traffic to endpoints that preserve the client IP address, make sure that all your required security configurations, for example, security groups, are updated to whitelist the user client IP address\.

1. Choose **Add endpoint**\.

## To edit an endpoint

You can edit an endpoint configuration to change the weight\. For more information, see [Endpoint Weights](about-endpoints-endpoint-weights.md)\.

1. Open the Global Accelerator console at [ https://us\-west\-2\.console\.aws\.amazon\.com/ec2/v2/home?region=us\-west\-2\#Global Accelerator:](https://us-west-2.console.aws.amazon.com/ec2/v2/home?region=us-west-2#GlobalAccelerator:)\. 

1. On the **accelerators** page, choose an accelerator\.

1. In the **Listeners** section, for **Listener ID**, choose the ID of a listener\.

1. In the **Endpoint groups** section, for **Endpoint group ID**, choose the ID of the endpoint group\.

1. Choose **Edit endpoint**\.

1. On the **Edit endpoint** page, make updates, and then choose **Save**\.

## To remove an endpoint

1. Open the Global Accelerator console at [ https://us\-west\-2\.console\.aws\.amazon\.com/ec2/v2/home?region=us\-west\-2\#Global Accelerator:](https://us-west-2.console.aws.amazon.com/ec2/v2/home?region=us-west-2#GlobalAccelerator:)\. 

1. On the **accelerators** page, choose an accelerator\.

1. In the **Listeners** section, for **Listener ID**, choose the ID of a listener\.

1. In the **Endpoint groups** section, for **Endpoint group ID**, choose the ID of the endpoint group\.

1. Choose **Remove endpoint**\.

1. In the confirmation dialog box, choose **Remove**\.