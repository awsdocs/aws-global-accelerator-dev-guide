# Work with standard accelerators in AWS Global Accelerator<a name="work-with-standard-accelerators"></a>

This chapter includes procedures and recommendations for creating standard accelerators in AWS Global Accelerator\. With a standard accelerator, Global Accelerator chooses the closest healthy endpoint for your traffic\.

If instead you want to use custom application logic to direct one or more users to a specific endpoint among many endpoints, create a custom routing accelerator\. For more information, see [Work with in AWS Global Accelerator](work-with-custom-routing-accelerators.md)\.

To set up a standard accelerator, do the following:

1. Create an accelerator, and choose the standard accelerator option\.

1. Add a listener with a specific set of ports or port range, and choose the protocol to accept: TCP, UDP, or both\.

1. Add one or more endpoint groups, one for each AWS Region in which you have endpoint resources\.

1. Add one or more endpoints to endpoint groups\. This isn't required, but traffic won't be routed if you don't have any endpoints\. Endpoints can be Network Load Balancers, Application Load Balancers, Amazon EC2 instances, or Elastic IP addresses\.

The following sections step through working with standard accelerators, listeners, endpoint groups, and endpoints\.

**Topics**
+ [Standard accelerators in AWS Global Accelerator](about-accelerators.md)
+ [Listeners for standard accelerators in AWS Global Accelerator](about-listeners.md)
+ [Endpoint groups for standard accelerators in AWS Global Accelerator](about-endpoint-groups.md)
+ [Endpoints for standard accelerators in AWS Global Accelerator](about-endpoints.md)