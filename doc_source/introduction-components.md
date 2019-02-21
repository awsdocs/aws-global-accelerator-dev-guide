# AWS Global Accelerator Components<a name="introduction-components"></a>

Global Accelerator includes components that work together to help you improve the availability and performance of your applications:

**Static IP address**  
AWS Global Accelerator provides you with a set of static IP addresses that are anycast from the AWS edge network\. The IP addresses serve as single fixed entry points for your clients\. If you already have Elastic Load Balancing load balancers or Elastic IP address resources set up for your applications, you can easily add those to Global Accelerator\. This allows Global Acceleratorstatic IP addresses to access the resources\.

**Accelerator**  
An accelerator directs traffic to optimal endpoints over the AWS global network to improve the availability and performance of your internet applications\. Each accelerator includes one or more listeners\.

**Network zone**  
A network zone services the static IP addresses for your accelerator from a unique IP subnet\. Similar to an AWS Availability Zone, a network zone is an isolated unit with its own set of physical infrastructure\.  When you configure an accelerator, Global Accelerator allocates two IPv4 addresses for it\. If one IP address from a network zone becomes unavailable due to IP address blocking by certain client networks, or due to network disruptions, client applications can retry on the healthy static IP address from the other isolated network zone\.

**Listener**  
A listener processes inbound connections from clients to Global Accelerator, based on the protocol and port that you configure\. Each listener has one or more endpoint groups associated with it, and traffic is forwarded to endpoints in one of the groups\. You associate endpoint groups with listeners by specifying the Regions that you want to distribute traffic to\. Traffic is distributed to optimal endpoints within the endpoint groups associated with a listener\.

**Endpoint group**  
Each endpoint group is associated with a specific AWS Region\. Endpoint groups include one or more endpoints in the Region\. You can increase or reduce the percentage of traffic that would be otherwise directed to an endpoint group by adjusting a setting called a *traffic dial*\. The traffic dial lets you easily do performance testing or blue/green deployment testing for new releases across different AWS Regions, for example\. 

**Endpoint**  
An endpoint is an Elastic IP address, Network Load Balancer, or Application Load Balancer\. Traffic is routed to endpoints based on several factors, including the geo\-proximity to the user, the health of the endpoint, and the configuration options that you choose, such as endpoint weights\. For each endpoint, you can configure weights, which are numbers that you can use to specify the proportion of traffic to route to each one\. This can be useful, for example, to do performance testing within a Region\.