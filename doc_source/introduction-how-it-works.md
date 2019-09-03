# How AWS Global Accelerator Works<a name="introduction-how-it-works"></a>

AWS Global Accelerator provides you with a set of two static IP addresses that are anycast from the AWS edge network\. The IP addresses serve as single fixed entry points for your clients\. When you set up your accelerator with Global Accelerator, you associate your static IP addresses to regional endpoints—such as Elastic IP addresses, Network Load Balancers, and Application Load Balancers—in one or more AWS Regions\. The static IP addresses accept incoming traffic onto the AWS global network from the edge location that is closest to your users\. \(Note that the idle timeout for connections is 65 seconds\.\)

From the edge location, traffic for your application is routed to the optimal AWS endpoint based on several factors, including the user’s location, the health of the endpoint, and the endpoint weights that you configure\. Traffic travels over the well\-monitored, congestion\-free, redundant AWS global network to the endpoint\. By maximizing the time that traffic is on the AWS network, Global Accelerator ensures that traffic is always routed over the optimum network path\. 

Global Accelerator continuously monitors the health of all endpoints, and instantly begins directing traffic to another available endpoint when it determines that an active endpoint is unhealthy\. This allows you to create a high\-availability architecture for your applications on AWS\.

Global Accelerator static IP addresses serve as a single, fixed entry point for clients that connect to your applications\. This gives you the flexibility to move traffic between Availability Zones or Regions when you’re doing performance testing, stack upgrades, or failover, without having to update your applications or DNS entries\. 

When you add an accelerator, security groups and AWS WAF rules that you already have configured continue to work as they did before you added the accelerator\.

If you want fine\-grained control over your global traffic, you can configure weights for your endpoints\. You can also increase \(dial up\) or decrease \(dial down\) the percentage of traffic to a specific endpoint group, for example, for performance testing or stack upgrades\. 

Global Accelerator supports both TCP and UDP protocols\.

**Note**  
AWS Direct Connect does not advertise IP address prefixes for AWS Global Accelerator over a public virtual interface\. We recommend that you do not advertise IP addresses that you use to communicate with Global Accelerator over your AWS Direct Connect public virtual interface\. If you advertise IP addresses that you use to communicate with Global Accelerator over your AWS Direct Connect public virtual interface, it will result in an asymmetric traffic flow: your traffic towards Global Accelerator goes to Global Accelerator over the internet but return traffic coming to your on\-premises network comes over your AWS Direct Connect public virtual interface\.

**Topics**
+ [Customizing Traffic Flow by using Traffic Dials and Endpoint Weights](#introduction-traffic-dials-weights)
+ [Health Checks for AWS Global Accelerator](#about-endpoint-groups-automatic-health-checks)
+ [Viewing Client IP Addresses in AWS Global Accelerator](introduction-how-it-works-client-ip.md)

## Customizing Traffic Flow by using Traffic Dials and Endpoint Weights<a name="introduction-traffic-dials-weights"></a>

There are two ways that you can customize how AWS Global Accelerator sends traffic to your endpoints:
+ Change the traffic dial to cap the traffic for one or more endpoint groups
+ Specify weights to change the proportion of traffic to the endpoints in a group

**How Traffic Dials Work**  
For each endpoint group in an accelerator, you can set a traffic dial to control the percentage of traffic that is sent to the endpoint group\. The percentage is applied only to traffic that is already directed to the endpoint group, not to all listener traffic\.   
The traffic dial limits the portion of traffic that an endpoint group accepts, expressed as a percentage of traffic directed to that endpoint group\. For example, if you set the traffic dial for an endpoint group in US\-East\-1 to 50 \(that is, 50%\) and the accelerator directs 100 user requests to that endpoint group, only 50 requests are accepted by the group\. The accelerator directs the remaining 50 requests to endpoint groups in other Regions\.  
For more information, see [Adjusting Traffic Flow With Traffic Dials](about-endpoint-groups-traffic-dial.md)\. 

**How Weights Work**  
For each endpoint, you can specify weights, which are numbers that change the proportion of traffic that the accelerator routes to each endpoint\. This can be useful, for example, to do performance testing within a Region\.  
A weight is a value that determines the proportion of traffic that the accelerator directs to an endpoint\. By default, the weight for an endpoint is 128—that is, half of the maximum value for a weight, 255\.  
The accelerator calculates the sum of the weights for the endpoints in an endpoint group, and then directs traffic to the endpoints based on the ratio of each endpoint's weight to the total\. For an example of how weights work, see [Endpoint Weights](about-endpoints-endpoint-weights.md)\.

Traffic dials and weights affect how the accelerator serves traffic in different ways: 
+ You configure traffic dials for *endpoint groups*\. The traffic dial lets you cut off a percentage of traffic—or all traffic—to the group, by "dialing down" traffic that the accelerator has already directed to it based on other factors, such as proximity\.
+ You use weights, on the other hand, to set values for *individual endpoints* within an endpoint group\. Weights provide a way to divide up traffic within the endpoint group—for example, if you want to do performance testing for specific endpoints in a Region\.

Although traffic dials typically limit the traffic that an endpoint group accepts, there are certain situations when traffic is still routed to an endpoint group even when you've set the traffic dial to zero\. For example, say you have two endpoint groups and you've set the traffic dial to 100% for the first one and to 0% for the second one\. If all of the endpoints in the first endpoint group become unhealthy, Global Accelerator routes traffic to the next best endpoint group based on geo\-proximity\. In this case, traffic is routed to the second endpoint group, regardless of its traffic dial setting\.

## Health Checks for AWS Global Accelerator<a name="about-endpoint-groups-automatic-health-checks"></a>

AWS Global Accelerator automatically checks the health of the endpoints that are associated with your static IP addresses, and then directs user traffic only to healthy endpoints\.

If you've configured custom health check settings—in Global Accelerator or by configuring settings directly for Network Load Balancer or Application Load Balancer load balancers—Global Accelerator uses those settings as follows:
+ For Network Load Balancer and Application Load Balancer endpoints, Global Accelerator follows the health check settings that you've configured for the load balancers on the Elastic Load Balancing console\.
+ For Elastic IP address endpoints, you can configure custom health check settings in Global Accelerator\. By default, Global Accelerator uses the listener port and protocol for health checks\. For UDP listeners with Elastic IP address endpoints, Global Accelerator uses the listener port and the TCP protocol for health checks, so you must have a TCP server on your endpoint\. 

When you add an endpoint, it must pass a health check to be considered healthy before traffic is directed to it\. If Global Accelerator doesn’t have any healthy endpoints to route traffic to, it routes requests to all endpoints\. 

Global Accelerator includes default health checks that are run automatically, but you can configure the timing for the checks and other options\. For more information, see [Health Check Options](about-endpoint-groups-health-check-options.md)\.