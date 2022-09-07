# Endpoints for standard accelerators in AWS Global Accelerator<a name="about-endpoints"></a>

Endpoints for standard accelerators in AWS Global Accelerator can be Network Load Balancers, Application Load Balancers, Amazon EC2 instances, or Elastic IP addresses\. With standard accelerators, a static IP address serves as a single point of contact for clients, and Global Accelerator then distributes incoming traffic across healthy endpoints\. Global Accelerator directs traffic to endpoints by using the port \(or port range\) that you specify for the listener that the endpoint group for the endpoint belongs to\. 

Each endpoint group can have multiple endpoints\. You can add each endpoint to multiple endpoint groups, but the endpoint groups must be associated with different listeners\. A resource must be valid and active when you add it as an endpoint\.

**Important**  
Accelerators that you configure as dual\-stack require that you add only endpoints that also support dual\-stack\. Also be aware that only Application Load Balancers can be added as dual\-stack endpoints\.

Global Accelerator continually monitors the health of all endpoints that are included in a standard endpoint group\. It routes traffic only to the active endpoints that are healthy\. If Global Accelerator doesn’t have any healthy endpoints to route traffic to, it routes traffic to all endpoints\.

Be aware of the following for specific types of Global Accelerator standard endpoints:

**Application Load Balancer endpoints**  
+ An Application Load Balancer endpoint can be internet\-facing or internal\. 
+ Application Load Balancers can be added as dual\-stack endpoints\. 

**Network Load Balancer endpoints**  
+ A Network Load Balancer endpoint must be internet\-facing\. For Network Load Balancer endpoints, we recommend that you disable cross\-zone traffic for the load balancers to avoid connection collisions, which can result in increased TCP connection time\. For more information, see [ TCP Connection Delays](https://docs.aws.amazon.com/elasticloadbalancing/latest/network/load-balancer-troubleshooting.html#tcp-delays) in the *Network Load Balancers User Guide*\.
+ Network Load Balancers cannot be added as dual\-stack endpoints\. 

**Amazon EC2 instance endpoints**  
+ An EC2 instance endpoint can't be one of the following types: C1, CC1, CC2, CG1, CG2, CR1, CS1, G1, G2, HI1, HS1, M1, M2, M3, or T1\.
+ EC2 instances are supported as endpoints in only some AWS Regions\. For a list of supported Regions, see [Supported AWS Regions for client IP address preservation](preserve-client-ip-address.regions.md)\.
+ We recommend that you remove an EC2 instance from Global Accelerator endpoint groups before you terminate the instance\. If you terminate an EC2 instance before you remove it from an endpoint group in Global Accelerator, and then you create another instance in the same VPC with the same private IP address, and health checks pass, Global Accelerator will route traffic to the new endpoint\. 
+ EC2 instances cannot be added as dual\-stack endpoints\. 

For all endpoints, when you configure resources as endpoints behind Global Accelerator, we recommend that you don't also send traffic directly to the same endpoints over the internet\. Sending direct traffic can lead to connection collision issues\.

**Topics**
+ [Adding, editing, or removing a standard endpoint](about-endpoints-adding-endpoints.md)
+ [Endpoint weights](about-endpoints-endpoint-weights.md)
+ [Adding endpoints with client IP address preservation](about-endpoints.sipp-caveats.md)
+ [Transitioning endpoints to use client IP address preservation](about-endpoints.transition-to-IP-preservation.md)