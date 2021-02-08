# AWS Global Accelerator components<a name="introduction-components"></a>

AWS Global Accelerator includes the following components:

**Static IP addresses**  
Global Accelerator provides you with a set of two static IP addresses that are anycast from the AWS edge network\. If you bring your own IP address range to AWS \(BYOIP\) to use with Global Accelerator, you can instead assign IP addresses from your own pool to use with your accelerator\. For more information, see [Bring your own IP addresses \(BYOIP\) in AWS Global Accelerator](using-byoip.md)\.  
The IP addresses serve as single fixed entry points for your clients\. If you already have Elastic Load Balancing load balancers, Amazon EC2 instances, or Elastic IP address resources set up for your applications, you can easily add those to a standard accelerator in Global Accelerator\. This allows Global Accelerator to use static IP addresses to access the resources\.  
The static IP addresses remain assigned to your accelerator for as long as it exists, even if you disable the accelerator and it no longer accepts or routes traffic\. However, when you *delete* an accelerator, you lose the static IP addresses that are assigned to it, so you can no longer route traffic by using them\. You can use IAM policies like tag\-based permissions with Global Accelerator to limit the users who have permissions to delete an accelerator\. For more information, see [ Tag\-based policies](auth-and-access-control.md#access-control-manage-access-tag-policies)\.

**Accelerator**  
An accelerator directs traffic to endpoints over the AWS global network to improve the performance of your internet applications\. Each accelerator includes one or more listeners\.  
There are two types of accelerators:  
+ A *standard* accelerator directs traffic to the optimal AWS endpoint based on several factors, including the user’s location, the health of the endpoint, and the endpoint weights that you configure\. This improves the availability and performance of your applications\. Endpoints can be Network Load Balancers, Application Load Balancers, Amazon EC2 instances, or Elastic IP addresses\.
+ A *custom routing* accelerator lets you deterministically route multiple users to a specific EC2 destination behind your accelerator, as is required for some use cases\. You do this by directing users to a unique IP address and port on your accelerator, which Global Accelerator has mapped to the destination\.
For more information, see [ Types of accelerators](introduction-accelerator-types.md)\.

**DNS name**  
Global Accelerator assigns each accelerator a default Domain Name System \(DNS\) name, similar to `a1234567890abcdef.awsglobalaccelerator.com`, that points to the static IP addresses that Global Accelerator assigns to you or that you choose from your own IP address range\. Depending on the use case, you can use your accelerator's static IP addresses or DNS name to route traffic to your accelerator, or set up DNS records to route traffic using your own custom domain name\.

**Network zone**  
A network zone services the static IP addresses for your accelerator from a unique IP subnet\. Similar to an AWS Availability Zone, a network zone is an isolated unit with its own set of physical infrastructure\.  When you configure an accelerator, by default, Global Accelerator allocates two IPv4 addresses for it\. If one IP address from a network zone becomes unavailable due to IP address blocking by certain client networks, or network disruptions, then client applications can retry on the healthy static IP address from the other isolated network zone\.

**Listener**  
A listener processes inbound connections from clients to Global Accelerator, based on the port \(or port range\) and protocol \(or protocols\) that you configure\. A listener can be configured for TCP, UDP, or both TCP and UDP protocols\. Each listener has one or more endpoint groups associated with it, and traffic is forwarded to endpoints in one of the groups\. You associate endpoint groups with listeners by specifying the Regions that you want to distribute traffic to\. With a standard accelerator, traffic is distributed to optimal endpoints within the endpoint groups associated with a listener\.

**Endpoint group**  
Each endpoint group is associated with a specific AWS Region\. Endpoint groups include one or more endpoints in the Region\. With a standard accelerator, you can increase or reduce the percentage of traffic that would be otherwise directed to an endpoint group by adjusting a setting called a *traffic dial*\. The traffic dial lets you easily do performance testing or blue/green deployment testing, for example, for new releases across different AWS Regions\. 

**Endpoint**  
An endpoint is the resource that Global Accelerator directs traffic to\.  
Endpoints for standard accelerators can be Network Load Balancers, Application Load Balancers, EC2 instances, or Elastic IP addresses\. An Application Load Balancer endpoint can be an internet\-facing or internal\. Traffic for standard accelerators is routed to endpoints based on the health of the endpoint along with configuration options that you choose, such as endpoint weights\. For each endpoint, you can configure weights, which are numbers that you can use to specify the proportion of traffic to route to each one\. This can be useful, for example, to do performance testing within a Region\.  
Endpoints for custom routing accelerators are virtual private cloud \(VPC\) subnets with one or many Amazon EC2 instances that are the destinations for traffic\.