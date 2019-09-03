# Endpoints in AWS Global Accelerator<a name="about-endpoints"></a>

Endpoints in AWS Global Accelerator can be Elastic IP addresses, Network Load Balancers, or Application Load Balancers\. \(An Application Load Balancer endpoint can be an internet\-facing Application Load Balancer or an internal Application Load Balancer\.\) A static IP address serves as a single point of contact for clients, and Global Accelerator then distributes incoming traffic across healthy endpoints\. Global Accelerator directs traffic to endpoints by using the port that you specify for the listener that the endpoint group for the endpoint belongs to\. Each endpoint group can have multiple endpoints\.

**Note**  
You can add each endpoint to multiple endpoint groups, but the endpoint groups must be associated with different listeners\.

You can add or remove endpoints from endpoint groups based on usage\.

If demand on your application increases, you can add more endpoints to one or more endpoint groups to handle the increased traffic\. Global Accelerator starts routing requests to an endpoint as soon as you add it and the endpoint passes the initial health checks\.

You can remove endpoints from your endpoint groups, for example, if you need to service your endpoints\. Removing an endpoint takes it out of the endpoint group, but does not affect the endpoint otherwise\. Global Accelerator stops directing traffic to an endpoint as soon as you remove it from an endpoint group\. The endpoint goes into a state where it waits for all current requests to be completed so there's no interruption for client traffic that is in progress\. You can add the endpoint back to the endpoint group when you’re ready for it to resume receiving requests\.

Global Accelerator continually monitors the health of all endpoints that are included in an endpoint group\. It routes traffic only to the active endpoints that are healthy\. If Global Accelerator doesn’t have any healthy endpoints to route traffic to, it routes traffic to all endpoints\.

**Topics**
+ [Adding, Editing, or Removing an Endpoint](about-endpoints-adding-endpoints.md)
+ [Endpoint Weights](about-endpoints-endpoint-weights.md)
+ [Transitioning Your ALB Endpoints to Use Client IP Address Preservation](about-endpoints.transition-to-IP-preservation.md)