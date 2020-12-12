# Guidelines and restrictions for<a name="about-custom-routing-guidelines"></a>

When you create and work with in AWS Global Accelerator, keep the following guidelines and restrictions in mind\.

**Amazon EC2 instance destinations**  
The virtual public cloud \(VPC\) subnet endpoints in a can only include EC2 instances\. No other resources, such as load balancers, are supported for \.  
The types of EC2 instances that are supported with Global Accelerator are listed in [Endpoints for standard accelerators in AWS Global Accelerator](about-endpoints.md)\.

**Port mappings**  
When you add a VPC subnet, Global Accelerator creates a static port mapping of listener port ranges to the port ranges supported by the subnet\. The port mapping for a specific subnet never changes\.  
You can view the port mapping list for a programmatically\. For more information, see [https://docs.aws.amazon.com/global-accelerator/latest/api/API_ListCustomRoutingPortMappings.html](https://docs.aws.amazon.com/global-accelerator/latest/api/API_ListCustomRoutingPortMappings.html)\.

**VPC subnet size**  
VPC subnets that you add to a must be a minimum of /28 and a maximum of /17\.

**Listener port ranges**  
You must specify enough listener ports, by specifying listener port ranges, to accommodate the number of destinations included in the subnets that you plan to add to your \. The range that you specify when you create a listener determines how many listener port and destination IP address combinations that you can use with your \. For maximum flexibility and to reduce the possibility of getting an error that you don't have enough listener ports available, we recommend that you specify a large port range\.   
Global Accelerator allocates port ranges in blocks when you add a subnet to a \. We recommend that you allocate listener port ranges linearly and make the ranges large enough to support the number of destination ports that you intend to have\. That is, the number of ports you should allocate should be at least the subnet size times the number of destination ports and protocols \(destination configurations\) that you will have in the subnet\.   
The algorithm that Global Accelerator uses to allocate port mappings might require you to add more listener ports, beyond this total\.
After you create a listener, you can edit it to add additional port ranges and associated protocols, but you can't decrease existing port ranges\. For example, if you have a listener port range of 5,000–10,000, you can't change the port range to be 5900–10,000 and you can't change the port range to be 5,000–9,900\.  
Each listener port range must include a minimum of 16 ports\. Listeners support ports 1\-65535\.

**Destination port ranges **  
There are two places that you specify port ranges for a : the port ranges that you specify when you add a listener and the destination port ranges and protocols that you specify for an endpoint group\.  
+ **Listener port ranges: **The listener ports on the Global Accelerator static IP addresses that your clients connect to\. Global Accelerator maps each port to a unique destination IP address and port on a VPC subnet behind the accelerator\.
+ **Destination port ranges: **The sets of destination port ranges that you specify for an endpoint group \(also called the destination configurations\) are the EC2 instance ports that receive traffic\. To receive traffic on destination ports, the Security Groups associated with your EC2 instances must permit traffic on them\.

**Health checks and failover**  
Global Accelerator does not perform health checks for and does not failover to healthy endpoints\. Traffic for is routed deterministically, regardless of the health of a destination resource\. 

**All traffic is denied by default**  
By default, traffic directed through a is denied to all destinations in your subnet\. To enable destination instances to receive traffic, you must specifically allow all traffic to the subnet or, alternatively, enable traffic to specific instance IP addresses and ports in the subnet\. To enable traffic to specific destinations, you must use the Global Accelerator API\. For more information, see [AllowCustomRoutingTraffic](https://docs.aws.amazon.com/global-accelerator/latest/api/API_AllowCustomRoutingTraffic.html)\.  
Updating a subnet or specific destination to allow or deny traffic takes time to propagate across the internet\. To determine if a change has propagated, you can call the `DescribeCustomRoutingAccelerator` API action to check the accelerator status\. For more information, see [ DescribeCustomRoutingAccelerator](https://docs.aws.amazon.com/global-accelerator/latest/api/API_DescribeCustomRoutingAccelerator.html)\.

**BYOIP is not supported**  
Bring your own IP address \(BYOIP\) is not supported for \.

**AWS CloudFormation is not supported**  
AWS CloudFormation is not supported for \.