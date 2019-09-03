# Transitioning Your ALB Endpoints to Use Client IP Address Preservation<a name="about-endpoints.transition-to-IP-preservation"></a>

Follow the guidance in this topic to transition one or more of the Application Load Balancer endpoints in your accelerator to endpoints that preserve the user’s client IP address\. For more information about client IP address preservation, see [ Viewing Client IP Addresses in AWS Global Accelerator](introduction-how-it-works-client-ip.md)\.

We recommend that you transition to using client IP address preservation slowly\. First, add new Application Load Balancer endpoints that you enable to preserve the client IP address\. Then slowly move traffic from existing endpoints to the new endpoints that have client IP address preservation, by configuring weights on the endpoints\. 

**Important**  
Before you begin to route traffic to Application Load Balancer endpoints that preserve the client IP address, make sure that all of the configurations in which you’ve whitelisted Global Accelerator client IP addresses are updated to whitelist the user client IP address instead\.

Client IP address preservation is available only for Application Load Balancer endpoints and only in specific AWS Regions\. For more information, see [ Supported Regions for Client IP Address Preservation](introduction-how-it-works-client-ip.md#introduction-how-it-works-client-ip.regions)\.

This section explains how to work with endpoint groups on the AWS Global Accelerator console\. If you want to use API operations with Global Accelerator, see the[ AWS Global Accelerator API Reference](https://docs.aws.amazon.com/global-accelerator/latest/api/Welcome.html)\.

After you move a small amount of traffic to the new Application Load Balancer for which you've enabled client IP address preservation, test to make sure that your configuration is working as you expect it to\. Then gradually increase the proportion of traffic to the Application Load Balancer that has client IP address preservation enabled by adjusting the weights on your Application Load Balancer endpoints\.

To transition to endpoints that preserve client IP addresses, start by following the steps here to add a new Application Load Balancer endpoint and enable client IP address preservation\. These steps must be completed in the Global Accelerator console\.

# To add an Application Load Balancer with client IP address preservation enabled

1. Open the Global Accelerator console at [ https://us\-west\-2\.console\.aws\.amazon\.com/ec2/v2/home?region=us\-west\-2\#Global Accelerator:](https://us-west-2.console.aws.amazon.com/ec2/v2/home?region=us-west-2#GlobalAccelerator:)\. 

1. In the **Accelerators** section, choose an accelerator, and then choose **View details**\.

1. In the **Listeners** section, choose a listener, and then choose **View details**\.

1. In the **Endpoint group** section, choose an endpoint group, and then choose **View details**\. 

1. In the **Endpoints** section, choose **Add endpoint**\.

1. On the **Add endpoints** page, in the **Endpoints** drop down list, choose an Application Load Balancer endpoint\.

1. In the **Weight** field, choose a low number compared to the weights that are set for your other Application Load Balancers\. For example, if the weight for a corresponding ALB is 255, you could enter a weight of 5 for the new ALB, to start with\. For more information, see [Endpoint Weights](about-endpoints-endpoint-weights.md)\.

1. Under **Preserve client IP address**, select **Preserve address**\.

1. Choose **Save changes**\.

Next, follow the steps here to edit the corresponding existing ALB endpoint \(that you're replacing with the new Application Load Balancer\) to reduce the weight for the Application Load Balancer so that less user traffic goes to that endpoint\.

# To reduce traffic for the existing Application Load Balancer endpoint

1. On the **Endpoint group** page, choose the Application Load Balancer endpoint that doesn't have client IP address preservation enabled\.

1. Choose **Edit**\.

1. On the **Edit endpoint** page, in the **Weight** field, enter a lower number than the current number\. For example, if the current weight is 255, you could enter a weight of 220\.

1. Choose **Save changes**\.

After you’ve tested with a small portion of the original traffic, by setting the weight for the new ALB to a low number, you can slowly transition all of the traffic by continuing to adjust the weights for the original and new endpoints\.

For example, say you start with an existing ALB with a weight set to 200 and add a new ALB endpoint \(with client IP address preservation enabled\) with a weight set to 5\. Gradually shift traffic from the original ALB to the new ALB by increasing the weight for the new ALB and decreasing the weight for the original ALB\. For example: original ALB weight 190/new ALB weight 10, original ALB weight 180/new ALB weight 20, original ALB weight 170/new ALB weight 30, and so on\.

 When you have decreased the weight to 0 for the original endpoint, all traffic goes to the new Application Load Balancer endpoint which preserves the user’s client IP address information\.

If you have additional Application Load Balancer endpoints that you want to transition to use client IP address preservation, repeat the steps in this section to migrate them\.

If you need to revert your configuration for an Application Load Balancer, so that traffic to the endpoint doesn't preserve the client IP address, you can do that at any time: increase the weight for the endpoint that does *not* have client IP address preservation to the original value, and decrease the weight for the endpoint *with* client IP address preservation to 0\.