# Preserve Client IP Addresses in AWS Global Accelerator<a name="preserve-client-ip-address"></a>

Your options for preserving and accessing the client IP address for AWS Global Accelerator depend on the endpoints that you've set up with your accelerator\. There are two types of endpoints that can preserve the source IP address of the client in incoming packets: Application Load Balancers and EC2 instances\.
+ When you use an internet\-facing Application Load Balancer as an endpoint with Global Accelerator, you can choose to preserve the source IP address of the original client for packets that arrive at the load balancer by enabling client IP address preservation\.
+ When you use an internal Application Load Balancer or an EC2 instance with Global Accelerator, the endpoint always has client IP address preservation enabled\. 

Global Accelerator does not support client IP address preservation for Network Load Balancer and Elastic IP address endpoints\.

When you plan for adding client IP address preservation, be aware of the following:
+ Before you add and begin to route traffic to endpoints that preserve the client IP address, make sure that all your required security configurations, for example, security groups, are updated to whitelist the user client IP address\. 
+ Client IP address preservation is supported only in specific AWS Regions\. For more information, see [ Supported Regions for Client IP Address Preservation](preserve-client-ip-address.regions.md)\.

**Topics**
+ [How To Enable Client IP Address Preservation](preserve-client-ip-address.how-to-enable-preservation.md)
+ [Benefits of Client IP Address Preservation](preserve-client-ip-address.benefits-of-preservation.md)
+ [How the Client IP Address is Preserved in AWS Global Accelerator](preserve-client-ip-address.headers.md)
+ [Best Practices for Client IP Address Preservation](best-practices-aga.md)
+ [Supported Regions for Client IP Address Preservation](preserve-client-ip-address.regions.md)