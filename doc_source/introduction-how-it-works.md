# How AWS Global Accelerator works<a name="introduction-how-it-works"></a>

The static IP addresses provided by AWS Global Accelerator serve as single fixed entry points for your clients\. When you set up your accelerator with Global Accelerator, you associate the static IP addresses to regional endpoints in one or more AWS Regions\. For standard accelerators, the endpoints are Network Load Balancers, Application Load Balancers, Amazon EC2 instances, or Elastic IP addresses\. For custom routing accelerators, endpoints are virtual private cloud \(VPC\) subnets with one or more EC2 instances\. The static IP addresses accept incoming traffic onto the AWS global network from the edge location that is closest to your users\.

**Note**  
If you bring your own IP address range to AWS \(BYOIP\) to use with Global Accelerator, you can instead assign static IP addresses from your own pool to use with your accelerator\. For more information, see [Bring your own IP addresses \(BYOIP\) in AWS Global Accelerator](using-byoip.md)\.

From the edge location, traffic for your application is routed based on the type of accelerator that you configure\. 
+ For standard accelerators, traffic is routed to the optimal AWS endpoint based on several factors, including the user’s location, the health of the endpoint, and the endpoint weights that you configure\. 
+ For custom routing accelerators, each client is routed to a specific Amazon EC2 instance and port in a VPC subnet, based on the external static IP address and listener port that you provide\.

Traffic travels over the well\-monitored, congestion\-free, redundant AWS global network to the endpoint\. By maximizing the time that traffic is on the AWS network, Global Accelerator ensures that traffic is always routed over the optimum network path\.

With some endpoint types \([in some AWS Regions](preserve-client-ip-address.regions.md)\), you have the option to preserve and access the client IP address\. Two types of endpoints can preserve the source IP address of the client in incoming packets: Application Load Balancers and Amazon EC2 instances\. Global Accelerator does not support client IP address preservation for Network Load Balancer and Elastic IP address endpoints\. Endpoints on custom routing accelerators always have the client IP address preserved\.

Global Accelerator terminates TCP connections from clients at AWS edge locations and, almost concurrently, establishes a new TCP connection with your endpoints\. This gives clients faster response times \(lower latency\) and increased throughput\.

In standard accelerators, Global Accelerator continuously monitors the health of all endpoints, and instantly begins directing traffic to another available endpoint when it determines that an active endpoint is unhealthy\. This allows you to create a high\-availability architecture for your applications on AWS\. Health checks aren't used with custom routing accelerators and there is no failover, because you specify the destination to route traffic to\.

When you add an accelerator, security groups and AWS WAF rules that you have already configured continue to work as they did before you added the accelerator\.

If you want fine\-grained control over your global traffic, you can configure weights for your endpoints in a standard accelerator\. You can also increase \(dial up\) or decrease \(dial down\) the percentage of traffic to a particular endpoint group, for example, for performance testing or stack upgrades\. 

Be aware of the following when you use Global Accelerator:
+ **IP address advertising:** AWS Direct Connect does not advertise IP address prefixes for AWS Global Accelerator over a public virtual interface\. We recommend that you do not advertise IP addresses that you use to communicate with Global Accelerator over your AWS Direct Connect public virtual interface\. If you advertise IP addresses that you use to communicate with Global Accelerator over your AWS Direct Connect public virtual interface, it will result in an asymmetric traffic flow: your traffic toward Global Accelerator goes to Global Accelerator over the internet, but return traffic coming to your on\-premises network comes over your AWS Direct Connect public virtual interface\.
+ **IP fragmentation:** IP packets that are too large to fit into a standard Ethernet frame \(1500\+ bytes\) when transmitted across the internet or other large networks are fragmented by intermediate routers and sent individually\. The TCP protocol does not require IP fragmentation because clients and endpoints automatically negotiate a smaller Maximum Segment Size \(MSS\)\. However, the UDP protocol requires IP fragmentation\. When packets are fragmented, Global Accelerator forwards UDP fragments to the configured endpoint, which reassembles the original IP packet\. Global Accelerator drops TCP fragments at the edge, because they are not supported by the AWS network\.
+ **Cross\-account resources:** When you add a resource as an endpoint in Global Accelerator, the resource cannot belong to another AWS account\.

**Topics**
+ [Idle timeout in AWS Global Accelerator](#about-idle-timeout)
+ [Static IP addresses in AWS Global Accelerator](#about-static-ip-addresses)
+ [Traffic flow management with traffic dials and endpoint weights](#introduction-traffic-dials-weights)
+ [Health checks for AWS Global Accelerator](#about-endpoint-groups-automatic-health-checks)

## Idle timeout in AWS Global Accelerator<a name="about-idle-timeout"></a>

AWS Global Accelerator sets an idle timeout period that applies to its connections\. If no data has been sent or received by the time that the idle timeout period elapses, Global Accelerator closes the connection\. To ensure that the connection stays alive, the client or the endpoint must send at least 1 byte of data before the idle timeout period elapses\.

The Global Accelerator idle timeout for a network connection depends on the type of connection:
+ The timeout is 340 seconds for TCP connections\.
+ The timeout is 30 seconds for UDP connections\.

Global Accelerator continues to direct traffic to an endpoint until the idle timeout is met, even if the endpoint is marked as unhealthy\. Global Accelerator selects a new endpoint, if needed, only when a new connection starts or after an idle timeout\.

## Static IP addresses in AWS Global Accelerator<a name="about-static-ip-addresses"></a>

You use the static IP addresses that Global Accelerator assigns to your accelerator—or that you specify from your own IP address pool, for standard accelerators—to route internet traffic to the AWS global network close to where your users are, regardless of their location\. For standard accelerators, you associate the addresses with Network Load Balancers, Application Load Balancers, Amazon EC2 instances, or Elastic IP addresses that run in a single AWS Region or multiple Regions\. For custom routing accelerators, you direct traffic to EC2 destinations in VPC subnets in one or more Regions\. Routing traffic through the AWS global network improves availability and performance because traffic doesn't have to take multiple hops over the public internet\. Using static IP addresses also lets you distribute incoming application traffic across multiple endpoint resources in multiple AWS Regions\. 

In addition, using static IP addresses makes it easier to add your application to more Regions or to migrate applications between Regions\. Using fixed IP addresses means that users have a consistent way to connect to your application as you make changes\. 

If you like, you can associate your own custom domain name with the static IP addresses for your accelerator\. For more information, see [Route custom domain traffic to your accelerator](dns-addressing-custom-domains.mapping-your-custom-domain.md)\.

Global Accelerator provides the static IP addresses for you from the Amazon pool of IP addresses, unless you bring your own IP address range to AWS, and then specify the static IP addresses from that pool\. \(For more information, see [Bring your own IP addresses \(BYOIP\) in AWS Global Accelerator](using-byoip.md)\.\) To create an accelerator on the console, the first step is to prompt Global Accelerator to provision the static IP addresses by entering a name for your accelerator or choose your own static IP addresses\. To see the steps for creating an accelerator, see [Getting started with AWS Global Accelerator](getting-started.md)\.

The static IP addresses remain assigned to your accelerator for as long as it exists, even if you disable the accelerator and it no longer accepts or routes traffic\. However, when you *delete* an accelerator, you lose the static IP addresses that are assigned to it, so you can no longer route traffic by using them\. You can use IAM policies like tag\-based permissions with Global Accelerator to limit the users who have permissions to delete an accelerator\. For more information, see [ Tag\-based policies](auth-and-access-control.md#access-control-manage-access-tag-policies)\.

## Traffic flow management with traffic dials and endpoint weights<a name="introduction-traffic-dials-weights"></a>

There are two ways that you can customize how AWS Global Accelerator sends traffic to your endpoints with a standard accelerator:
+ Change the traffic dial to limit the traffic for one or more endpoint groups
+ Specify weights to change the proportion of traffic to the endpoints in a group

**How traffic dials work**  
For each endpoint group in a standard accelerator, you can set a traffic dial to control the percentage of traffic that is sent to the endpoint group\. The percentage is applied only to traffic that is already directed to the endpoint group, not to all listener traffic\.   
The traffic dial limits the portion of traffic that an endpoint group accepts, expressed as a percentage of traffic directed to that endpoint group\. For example, if you set the traffic dial for an endpoint group in `us-east-1` to 50 \(that is, 50%\) and the accelerator directs 100 user requests to that endpoint group, only 50 requests are accepted by the group\. The accelerator directs the remaining 50 requests to endpoint groups in other Regions\.  
For more information, see [Adjusting traffic flow with traffic dials](about-endpoint-groups-traffic-dial.md)\. 

**How weights work**  
For each endpoint in a standard accelerator, you can specify weights, which are numbers that change the proportion of traffic that the accelerator routes to each endpoint\. This can be useful, for example, to do performance testing within a Region\.  
A weight is a value that determines the proportion of traffic that the accelerator directs to an endpoint\. By default, the weight for an endpoint is 128—that is, half of the maximum value for a weight, 255\.  
The accelerator calculates the sum of the weights for the endpoints in an endpoint group, and then directs traffic to the endpoints based on the ratio of each endpoint's weight to the total\. For an example of how weights work, see [ Endpoint weights](about-endpoints-endpoint-weights.md)\.

Traffic dials and weights affect how the standard accelerator serves traffic in different ways: 
+ You configure traffic dials for *endpoint groups*\. The traffic dial lets you cut off a percentage of traffic—or all traffic—to the group, by "dialing down" traffic that the accelerator has already directed to it based on other factors, such as proximity\.
+ You use weights, on the other hand, to set values for *individual endpoints* within an endpoint group\. Weights provide a way to divide up traffic within the endpoint group\. For example, you can use weights to do performance testing for specific endpoints in a Region\.

**Note**  
For more information about how traffic dials and weights affect failover, see [Failover for unhealthy endpoints](about-endpoints-endpoint-weights.md#about-endpoints-endpoint-weights.unhealthy-endpoints)\.

## Health checks for AWS Global Accelerator<a name="about-endpoint-groups-automatic-health-checks"></a>

For standard accelerators, AWS Global Accelerator automatically checks the health of the endpoints that are associated with your static IP addresses, and then directs user traffic only to healthy endpoints\.

Global Accelerator includes default health checks that are run automatically, but you can configure the timing for the checks and other options\. If you've configured custom health check settings, Global Accelerator uses those settings in specific ways, depending on your configuration\. You configure those settings in Global Accelerator for Amazon EC2 instance or Elastic IP address endpoints or by configuring settings on the Elastic Load Balancing console for Network Load Balancers or Application Load Balancers\. For more information, see [Changing health check options](about-endpoint-groups-health-check-options.md)\.

When you add an endpoint to a standard accelerator, it must pass a health check to be considered healthy before traffic is directed to it\. If Global Accelerator doesn’t have any healthy endpoints to route traffic to in a standard accelerator, it routes requests to all endpoints\. 