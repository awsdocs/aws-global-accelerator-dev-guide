# How to get started with AWS Global Accelerator<a name="introduction-get-started"></a>

You can get started with setting up AWS Global Accelerator by using the API or by using the AWS Global Accelerator console\. Because Global Accelerator is a global service, it’s not tied to a specific AWS Region\. Note that Global Accelerator is a global service that supports endpoints in multiple AWS Regions but you must specify the US West \(Oregon\) Region to create or update accelerators\.\)

To get started using Global Accelerator, you follow these general steps: 

1. **Choose the type of accelerator that you want to create: **A standard accelerator or a \.

1. **Configure the initial setup for Global Accelerator:** Provide a name for your accelerator\. Then configure one or more listeners to process inbound connections from clients, based on the protocol and port \(or port range\) that you specify\.

1. **Configure regional endpoint groups for your accelerator:** You can select one or more regional endpoint groups to add to your listener\. The listener routes requests to the endpoints that you've added to an endpoint group\. 

   For a standard accelerator, Global Accelerator monitors the health of endpoints within the group by using the health check settings that are defined for each of your endpoints\. For each endpoint group in a standard accelerator, you can configure a *traffic dial* percentage to control the percentage of traffic that an endpoint group will accept\. The percentage is applied only to traffic that is already directed to the endpoint group, not all listener traffic\. By default, the traffic dial is set to 100% for all regional endpoint groups\.

   For a , traffic is deterministically routed to a specific destination in a VPC subnet, based on the listener port that the traffic is received on\.

1. **Add endpoints to endpoint groups:** The endpoints that you add depend on the type of accelerator\.
   + For a standard accelerator, you can add one or more regional resources, such as load balancers or EC2 instances endpoints, to each endpoint group\. Next, you can decide how much traffic you want to route to each endpoint by setting endpoint weights\. 
   + For a , you add one or more virtual private cloud \(VPC\) subnets with up to thousands of Amazon EC2 instance destinations\.

For detailed steps about how to create a standard accelerator or a using the AWS Global Accelerator console, see [Getting started with AWS Global Accelerator](getting-started.md)\. To work with API operations, see [Common actions that you can use with AWS Global Accelerator](global-accelerator-actions.md) and the [AWS Global Accelerator API Reference](https://docs.aws.amazon.com/global-accelerator/latest/api/Welcome.html)\.