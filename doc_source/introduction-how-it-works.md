# How AWS Global Accelerator Works<a name="introduction-how-it-works"></a>

AWS Global Accelerator provides you with a set of static IP addresses that are anycast from the AWS edge network\. If you bring your own IP address range to AWS \(BYOIP\), you can instead assign static IP addresses from your own pool to use with your accelerator\. For more information, see [Bring Your Own IP Addresses \(BYOIP\) in AWS Global Accelerator](using-byoip.md)\.

The static IP addresses serve as single fixed entry points for your clients\. When you set up your accelerator with Global Accelerator, you associate your static IP addresses to regional endpoints—Network Load Balancers, Application Load Balancers, EC2 instances, or Elastic IP addresses—in one or more AWS Regions\. The static IP addresses accept incoming traffic onto the AWS global network from the edge location that is closest to your users\.

**Note**  
The idle timeout for the network connection depends on the type of connection:  
The timeout is 300 seconds for TCP connections to endpoints *with* client IP address preservation enabled \(Application Load Balancers and EC2 instances\)\.
The timeout is 90 seconds for TCP connections to endpoints *without* client IP address preservation \(Network Load Balancers and Elastic IP addresses\)\.
The timeout is 30 seconds for UDP connections\.

From the edge location, traffic for your application is routed to the optimal AWS endpoint based on several factors, including the user’s location, the health of the endpoint, and the endpoint weights that you configure\. Traffic travels over the well\-monitored, congestion\-free, redundant AWS global network to the endpoint\. By maximizing the time that traffic is on the AWS network, Global Accelerator ensures that traffic is always routed over the optimum network path\. 

Global Accelerator continuously monitors the health of all endpoints, and instantly begins directing traffic to another available endpoint when it determines that an active endpoint is unhealthy\. This allows you to create a high\-availability architecture for your applications on AWS\.

When you add an accelerator, security groups and AWS WAF rules that you have already configured continue to work as they did before you added the accelerator\.

If you want fine\-grained control over your global traffic, you can configure weights for your endpoints\. You can also increase \(dial up\) or decrease \(dial down\) the percentage of traffic to a particular endpoint group, for example, for performance testing or stack upgrades\. 

Global Accelerator supports both TCP and UDP protocols\.

**Note**  
AWS Direct Connect does not advertise IP address prefixes for AWS Global Accelerator over a public virtual interface\. We recommend that you do not advertise IP addresses that you use to communicate with Global Accelerator over your AWS Direct Connect public virtual interface\. If you advertise IP addresses that you use to communicate with Global Accelerator over your AWS Direct Connect public virtual interface, it will result in an asymmetric traffic flow: your traffic toward Global Accelerator goes to Global Accelerator over the internet, but return traffic coming to your on\-premises network comes over your AWS Direct Connect public virtual interface\.

**Topics**
+ [Static IP Addresses in AWS Global Accelerator](#about-static-ip-addresses)
+ [Traffic Flow Management with Traffic Dials and Endpoint Weights](#introduction-traffic-dials-weights)
+ [Health Checks for AWS Global Accelerator](#about-endpoint-groups-automatic-health-checks)

## Static IP Addresses in AWS Global Accelerator<a name="about-static-ip-addresses"></a>

You use the static IP addresses that Global Accelerator assigns to your accelerator—or that you specify from your own IP address pool—to route internet traffic to the AWS global network close to where your users are, regardless of their location\. You associate the addresses with Network Load Balancers, Application Load Balancers, EC2 instances, or Elastic IP addresses that run in a single AWS Region or multiple Regions\. Routing traffic through the AWS global network improves availability and performance because traffic doesn't have to take multiple hops over the public internet\. Using static IP addresses also lets you distribute incoming application traffic across multiple endpoint resources in multiple AWS Regions\. 

In addition, using static IP addresses makes it easier to add your application to more Regions or to migrate applications between Regions\. Using fixed IP addresses means that users have a consistent way to connect to your application as you make changes\. 

If you like, you can associate your own custom domain name with the static IP addresses for your accelerator\. For more information, see [Route Custom Domain Traffic to Your Accelerator](about-accelerators.mapping-your-custom-domain.md)\.

Global Accelerator provides the static IP addresses for you from the Amazon pool of IP addresses, unless you bring your own IP address range to AWS and specify the static IP addresses from that pool\. For more information, see [Bring Your Own IP Addresses \(BYOIP\) in AWS Global Accelerator](using-byoip.md)\. To create an accelerator on the console, the first step is to prompt Global Accelerator to provision the static IP addresses by entering a name for your accelerator or choose your own static IP addresses\. To see the steps for creating an accelerator, see [ Creating or Updating an Accelerator](about-accelerators.md#about-accelerators.creating-editing)\.

## Traffic Flow Management with Traffic Dials and Endpoint Weights<a name="introduction-traffic-dials-weights"></a>

There are two ways that you can customize how AWS Global Accelerator sends traffic to your endpoints:
+ Change the traffic dial to limit the traffic for one or more endpoint groups
+ Specify weights to change the proportion of traffic to the endpoints in a group

**How Traffic Dials Work**  
For each endpoint group in an accelerator, you can set a traffic dial to control the percentage of traffic that is sent to the endpoint group\. The percentage is applied only to traffic that is already directed to the endpoint group, not to all listener traffic\.   
The traffic dial limits the portion of traffic that an endpoint group accepts, expressed as a percentage of traffic directed to that endpoint group\. For example, if you set the traffic dial for an endpoint group in `us-east-1` to 50 \(that is, 50%\) and the accelerator directs 100 user requests to that endpoint group, only 50 requests are accepted by the group\. The accelerator directs the remaining 50 requests to endpoint groups in other Regions\.  
For more information, see [Adjusting Traffic Flow With Traffic Dials](about-endpoint-groups-traffic-dial.md)\. 

**How Weights Work**  
For each endpoint, you can specify weights, which are numbers that change the proportion of traffic that the accelerator routes to each endpoint\. This can be useful, for example, to do performance testing within a Region\.  
A weight is a value that determines the proportion of traffic that the accelerator directs to an endpoint\. By default, the weight for an endpoint is 128—that is, half of the maximum value for a weight, 255\.  
The accelerator calculates the sum of the weights for the endpoints in an endpoint group, and then directs traffic to the endpoints based on the ratio of each endpoint's weight to the total\. For an example of how weights work, see [Endpoint Weights](about-endpoints-endpoint-weights.md)\.

Traffic dials and weights affect how the accelerator serves traffic in different ways: 
+ You configure traffic dials for *endpoint groups*\. The traffic dial lets you cut off a percentage of traffic—or all traffic—to the group, by "dialing down" traffic that the accelerator has already directed to it based on other factors, such as proximity\.
+ You use weights, on the other hand, to set values for *individual endpoints* within an endpoint group\. Weights provide a way to divide up traffic within the endpoint group\. For example, you can use weights to do performance testing for specific endpoints in a Region\.

## Health Checks for AWS Global Accelerator<a name="about-endpoint-groups-automatic-health-checks"></a>

AWS Global Accelerator automatically checks the health of the endpoints that are associated with your static IP addresses, and then directs user traffic only to healthy endpoints\.

Global Accelerator includes default health checks that are run automatically, but you can configure the timing for the checks and other options\. If you've configured custom health check settings, Global Accelerator uses those settings in specific ways, depending on your configuration\. You configure those settings in Global Accelerator for EC2 instance or Elastic IP address endpoints or by configuring settings on the Elastic Load Balancing console for Network Load Balancers or Application Load Balancers\. For more information, see [Health Check Options](about-endpoint-groups-health-check-options.md)\.

When you add an endpoint, it must pass a health check to be considered healthy before traffic is directed to it\. If Global Accelerator doesn’t have any healthy endpoints to route traffic to, it routes requests to all endpoints\. 