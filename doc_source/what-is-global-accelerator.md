# What Is AWS Global Accelerator?<a name="what-is-global-accelerator"></a>

AWS Global Accelerator is a network layer service that you use to create *accelerators* that direct traffic to optimal endpoints over the AWS global network\. This improves the availability and performance of your internet applications that are used by a global audience\. 

Global Accelerator provides you with a set of two static IP addresses that you associate with your accelerator\. These IP addresses are anycast from the AWS edge network\. They distribute incoming application traffic across multiple endpoints in one or more AWS Regions, which increases the availability of your applications\. Endpoints can be Elastic IP addresses, Network Load Balancers, and Application Load Balancers\.

**Note**  
For a list of the AWS Regions where Global Accelerator and other services are currently supported, see the [AWS Region Table](https://aws.amazon.com/about-aws/global-infrastructure/regional-product-services/)\.

Global Accelerator uses the AWS global network to route traffic to the optimal regional endpoint based on health, client location, and policies that you configure\. The service reacts instantly to changes in health or configuration to ensure that internet traffic from clients is always directed to healthy endpoints\.

**Topics**
+ [AWS Global Accelerator Components](introduction-components.md)
+ [How AWS Global Accelerator Works](introduction-how-it-works.md)
+ [IP Address Ranges of Global Accelerator Edge Servers](introduction-ip-ranges.md)
+ [AWS Global Accelerator Use Cases](introduction-benefits-of-migrating.md)
+ [How to Get Started with AWS Global Accelerator](introduction-get-started.md)
+ [Pricing for AWS Global Accelerator](introduction-pricing.md)