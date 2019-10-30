# What Is AWS Global Accelerator?<a name="what-is-global-accelerator"></a>

AWS Global Accelerator is a network layer service that you use to create *accelerators* that direct traffic to optimal endpoints over the AWS global network\. This improves the availability and performance of your internet applications that are used by a global audience\. 

Global Accelerator provides you with static IP addresses that you associate with your accelerator\. These IP addresses are anycast from the AWS edge network\. They distribute incoming application traffic across multiple endpoints in one or more AWS Regions, which increases the availability of your applications\. Endpoints can be Network Load Balancers, Application Load Balancers, EC2 instances, and Elastic IP addresses\.

**Important**  
The IP addresses are assigned to your accelerator for as long as it exists, even if you disable the accelerator and it no longer accepts or routes traffic\. However, when you *delete* an accelerator, you lose the static IP addresses that are assigned to the accelerator, so you can no longer route traffic by using them\. As a best practice, ensure that you have permissions in place to avoid inadvertently deleting accelerators\. You can use IAM policies with Global Accelerator to limit the users who have permissions to delete an accelerator\. For more information, see [Authentication and Access Control for AWS Global Accelerator](auth-and-access-control.md)\.

Global Accelerator uses the AWS global network to route traffic to the optimal regional endpoint based on health, client location, and policies that you configure\. The service reacts instantly to changes in health or configuration to ensure that internet traffic from clients is always directed to healthy endpoints\.

For a list of the AWS Regions where Global Accelerator and other services are currently supported, see the [AWS Region Table](https://aws.amazon.com/about-aws/global-infrastructure/regional-product-services/)\.

**Topics**
+ [AWS Global Accelerator Components](introduction-components.md)
+ [How AWS Global Accelerator Works](introduction-how-it-works.md)
+ [IP Address Ranges of Global Accelerator Edge Servers](introduction-ip-ranges.md)
+ [AWS Global Accelerator Use Cases](introduction-benefits-of-migrating.md)
+ [How to Get Started with AWS Global Accelerator](introduction-get-started.md)
+ [Pricing for AWS Global Accelerator](introduction-pricing.md)