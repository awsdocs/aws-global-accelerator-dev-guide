# Avoiding connection collisions that result in TCP connection time delays<a name="about-endpoints.avoid-connection-collisions"></a>

Intermittent connectivity issues can be caused by connection collisions in AWS Global Accelerator\. These can occur when users \(with the same source IP and source port\) access resources in Global Accelerator in certain scenarios\. The collisions can result in TCP connection time delays for traffic that goes through your accelerators\.

You can avoid these delays by configuring your accelerators with *port overrides*, a feature in Global Accelerator that enables you to route incoming traffic to a different destination ports on your accelerator endpoints\. Follow the guidance in this section to learn about how to use port overrides to prevent the connection collisions and avoid potential TCP connection time delays\.

## Scenarios that can cause connection collisions<a name="about-endpoints.avoid-connection-collisions.scenarios"></a>

There are three scenarios in Global Accelerator that can lead to connection collisions, and thus to TCP connection time delays:
+ You configure the same resource as an endpoint with multiple accelerators\.
+ You configure resources as endpoints behind Global Accelerator, and you also send traffic directly over the internet from your end users to the same resources\.
+ You configure Network Load Balancer endpoints for cross\-zone traffic\.

For Network Load Balancer endpoints, we recommend that you disable cross\-zone traffic for the load balancers to avoid connection collisions\. For more information, see [ TCP Connection Delays](https://docs.aws.amazon.com/elasticloadbalancing/latest/network/load-balancer-troubleshooting.html#tcp-delays) in the *User Guide for Network Load Balancers*\.

For the other scenarios, we recommend that you use the port override feature with the endpoint group to prevent collisions\. Using port overrides, you can map Global Accelerator listener ports to different destination port numbers on an endpoint resource\. Listener ports default to using the same port numbers on endpoint resources\. By using port overrides, accelerators can route traffic from the same users \(with the source IP and source port\) to the same endpoint, but use different destination port numbers, which avoids collisions\.

The next section provides specific examples for each of the scenarios of how you can configure port overrides to avoid connection collisions\. For more information about configuring port overrides, see [Overriding listener ports](about-endpoint-groups-port-override.md)\.

## How to prevent connection collisions by using port overrides<a name="about-endpoints.avoid-connection-collisions.how-to-prevent"></a>

By default, an accelerator routes user traffic to endpoints in AWS Regions using the same protocol and the same destination port ranges that you specify when you create a listener\. However, you can optionally choose to override the port number mapping for the listener port\. That is, you can map a listener port number to route traffic to a different destination port number on an endpoint\.

For example, if you define a listener that accepts TCP traffic on ports 80 and 443, by default, the accelerator routes traffic to those same ports, 80 and 443, on endpoints\. However, using the port override feature, the accelerator can route traffic coming in on those ports to different ports on endpoints, such as 8080 and 8443\.

By creating different port mappings for listeners in two \(or more\) accelerators that have the same resources configured behind them, you can use separate destination port numbers for each accelerator and avoid collisions\.

For example, say you have Accelerator\-A and Accelerator\-B, and each one has a listener configured for TCP and port 443\. You can set up a port override for the listener for Accelerator\-A to map port 443 to 8443, and the listener for Accelerator\-B to map port 443 to 9443\. Now you configure an Application Load Balancer endpoint, ALB\-1234, for example, to listen on both ports 8443 and 9443\. Then traffic coming in on port 443 \(to the listeners for both accelerators\) from the same user IP address will arrive at ALB\-1234, without connection collisions or TCP connection time delays\. 

You can see the traffic paths for this example illustrated in the following:

`Accelerator-A [listener: tcp,443] → Endpoint-Group [port-override: 443→8443] → ALB-1234 (listener: HTTPS,8443)`

`Accelerator-B [listener: tcp,443] → Endpoint-Group [port-override: 443→9443] → ALB-1234 (listener: HTTPS,9443) `

You can use a port override in a similar way to prevent connection collisions for resources that are accessed by both direct user traffic and through an accelerator by overriding the default mapping for the accelerator's listener port number\. To prevent collisions in this scenario, do the following:

1. Determine the port that you want the resource to listen on for your direct traffic\. 

1. Configure the listener for your accelerator to override the default port, and configure the listener on your resource to listen on that port for accelerator traffic\.

For example, you could set up a port override for the listener for your accelerator to map port 443 to port 8443\. Now, you could configure an Application Load Balancer endpoint, for example, to listen for your accelerator traffic on port 8443 and for direct traffic on port 443\. With this configuration, you avoid connection collisions on the Application Load Balancer for traffic coming from the same user IP address\.