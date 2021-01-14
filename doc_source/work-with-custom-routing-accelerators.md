# Work with custom routing accelerators in AWS Global Accelerator<a name="work-with-custom-routing-accelerators"></a>

This chapter includes procedures and recommendations for creating custom routing accelerators in AWS Global Accelerator\. A custom routing accelerator lets you use application logic to directly map one or more users to a specific Amazon EC2 instance among many destinations, while gaining the performance improvements of routing your traffic through Global Accelerator\. This is useful when you have an application that requires a group of users to interact with each other on the same session running on a specific EC2 instance and port, such as gaming applications or Voice over IP \(VoIP\) sessions\. 

Endpoints for custom routing accelerators must be virtual private cloud \(VPC\) subnets, and a custom routing accelerator can only route traffic to Amazon EC2 instances in those subnets\. When you create a custom routing accelerator, you can include thousands of Amazon EC2 instances running in a single or multiple VPC subnets\. To learn more, see [How custom routing accelerators work in AWS Global Accelerator](about-custom-routing-how-it-works.md)\.

If instead you want Global Accelerator to automatically choose the closest healthy endpoint to your clients, create a standard accelerator\. For more information, see [Work with standard accelerators in AWS Global Accelerator](work-with-standard-accelerators.md)\.

To set up custom routing accelerator, you do the following:

1. Review the guidelines and requirements for creating a custom routing accelerator\. See [Guidelines and restrictions for custom routing accelerators](about-custom-routing-guidelines.md)\.

1. Create a VPC subnet\. You can add EC2 instances to the subnet at any time after adding the subnet to Global Accelerator\.

1. Create an accelerator, and select the option for a custom routing accelerator\.

1. Add a listener and specify a range of ports for Global Accelerator to listen on\. Make sure that you include a large range with enough ports for Global Accelerator to map to all the destinations that you expect to have\. These ports are distinct from destination ports, which you specify in the next step\. For more information about listener port requirements, see [Guidelines and restrictions for custom routing accelerators](about-custom-routing-guidelines.md)\.

1. Add one or more endpoint groups for AWS Regions in which you have VPC subnets\. You specify the following for each endpoint group:
   + An endpoint port range, which represents the ports on your destination EC2 instances that will be able to receive traffic\.
   + The protocol for each destination port range: UDP, TCP, or both UDP and TCP\.

1. For the endpoint subnet, select a subnet ID\. You can add multiple subnets in each endpoint group and subnets can be different sizes \(up to /17\)\.

The following sections step through working with custom routing accelerators, listeners, endpoint groups, and endpoints\.

**Topics**
+ [How custom routing accelerators work in AWS Global Accelerator](about-custom-routing-how-it-works.md)
+ [Guidelines and restrictions for custom routing accelerators](about-custom-routing-guidelines.md)
+ [Custom routing accelerators in AWS Global Accelerator](about-custom-routing-accelerators.md)
+ [Listeners for custom routing accelerators in AWS Global Accelerator](about-custom-routing-listeners.md)
+ [Endpoint groups for custom routing accelerators in AWS Global Accelerator](about-custom-routing-endpoint-groups.md)
+ [VPC subnet endpoints for custom routing accelerators in AWS Global Accelerator](about-custom-routing-endpoints.md)