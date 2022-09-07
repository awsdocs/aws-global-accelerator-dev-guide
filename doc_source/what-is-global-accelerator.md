# What is AWS Global Accelerator?<a name="what-is-global-accelerator"></a>

AWS Global Accelerator is a service in which you create *accelerators* to improve the performance of your applications for local and global users\. Depending on the type of accelerator you choose, you can gain additional benefits: 
+ With a standard accelerator, you can improve availability of your internet applications that are used by a global audience\. With a standard accelerator, Global Accelerator directs traffic over the AWS global network to endpoints in the nearest Region to the client\. 
+ With a custom routing accelerator, you can map one or more users to a specific destination among many destinations\.

Global Accelerator is a global service that supports endpoints in multiple AWS Regions\. To determine if Global Accelerator or other services are currently supported in a specific AWS Region, see the [AWS Regional Services List](http://aws.amazon.com/about-aws/global-infrastructure/regional-product-services/)\.

By default, Global Accelerator provides you with static IP addresses that you associate with your accelerator\. The static IP addresses are anycast from the AWS edge network\. For IPv4, Global Accelerator provides two static IPv4 addresses\. For dual\-stack, Global Accelerator provides a total of four addresses: two static IPv4 addresses and two static IPv6 addresses\. For IPv4, instead of using the addresses that Global Accelerator provides, you can configure these entry points to be IPv4 addresses from your own IP address ranges that you bring to Global Accelerator \(BYOIP\)\. 

**Important**  
The static IP addresses remain assigned to your accelerator for as long as it exists, even if you disable the accelerator and it no longer accepts or routes traffic\. However, when you *delete* an accelerator, you lose the static IP addresses that are assigned to it, so you can no longer route traffic by using them\. You can use IAM policies, like tag\-based permissions with Global Accelerator, to limit the users who have permissions to delete an accelerator\. For more information, see [ Tag\-based policies](auth-and-access-control.md#access-control-manage-access-tag-policies)\.

For standard accelerators, Global Accelerator uses the AWS global network to route traffic to the optimal regional endpoint based on health, client location, and policies that you configure, which increases the availability of your applications\. Endpoints for standard accelerators can be Network Load Balancers, Application Load Balancers, Amazon EC2 instances, or Elastic IP addresses that are located in one AWS Region or multiple Regions\. The service reacts instantly to changes in health or configuration to ensure that internet traffic from clients is always directed to healthy endpoints\.

Custom routing accelerators only support virtual private cloud \(VPC\) subnet endpoint types and route traffic to private IP addresses in that subnet\.

**Topics**
+ [AWS Global Accelerator components](introduction-components.md)
+ [How AWS Global Accelerator works](introduction-how-it-works.md)
+ [Types of accelerators](introduction-accelerator-types.md)
+ [Location and IP address ranges of Global Accelerator edge servers](introduction-ip-ranges.md)
+ [AWS Global Accelerator use cases](introduction-benefits-of-migrating.md)
+ [AWS Global Accelerator Speed Comparison Tool](introduction-speed-comparison-tool.md)
+ [How to get started with AWS Global Accelerator](introduction-get-started.md)
+ [Tagging in AWS Global Accelerator](tagging-in-global-accelerator.md)
+ [Pricing for AWS Global Accelerator](introduction-pricing.md)