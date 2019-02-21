# Getting Started with AWS Global Accelerator<a name="getting-started"></a>

This tutorial provides the steps for getting started with AWS Global Accelerator using the console\. You can also use AWS Global Accelerator API operations to create and customize your accelerator\. At each step in this tutorial, there's a link to the corresponding API operation for completing the task programmatically\. For more information about working with AWS Global Accelerator API operations, see the [AWS Global Accelerator API Reference](https://docs.aws.amazon.com/global-accelerator/latest/api/Welcome.html)\.

**Tasks**
+ [ Before You Begin](#getting-started-before-you-begin)
+ [ Step 1: Create an Accelerator](#getting-started-accelerator)
+ [Step 2: Add Listeners](#getting-started-create-listeners)
+ [Step 3: Add Endpoint Groups](#getting-started-add-endpoint-groups)
+ [Step 4: Add Endpoints](#getting-started-add-endpoints)
+ [Step 5: Test Your Accelerator](#getting-started-create-and-test)
+ [Step 6: Delete Your Accelerator](#getting-started-delete-accelerator)

## Before You Begin<a name="getting-started-before-you-begin"></a>

Before you create an accelerator, create at least one resource that you can add as an endpoint to direct traffic to\. Do one of the following:
+ Launch at least one Amazon EC2 instance, and then create a Network Load Balancer or Application Load Balancer for it\. For more information, see [Getting Started with Amazon EC2](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/EC2_GetStarted.html) and [Create a Network Load Balancer](https://docs.aws.amazon.com/elasticloadbalancing/latest/network/create-network-load-balancer.html)\. 
+ Create an Elastic IP address, and then attach it to an Amazon EC2 instance or network interface\. For more information, see [Elastic IP Addresses](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/elastic-ip-addresses-eip.html)\.

## Step 1: Create an Accelerator<a name="getting-started-accelerator"></a>

To create your accelerator, you enter a name\. 

**Note**  
To complete this task by using an API operation instead of the console, see [https://docs.aws.amazon.com/global-accelerator/latest/api/API_CreateAccelerator.html](https://docs.aws.amazon.com/global-accelerator/latest/api/API_CreateAccelerator.html) in the *AWS Global Accelerator API Reference*\.

1. Open the Global Accelerator console at [ https://us\-west\-2\.console\.aws\.amazon\.com/ec2/v2/home?region=us\-west\-2\#Global Accelerator:](https://us-west-2.console.aws.amazon.com/ec2/v2/home?region=us-west-2#GlobalAccelerator:)\. 

1. Choose **Create accelerator**\.

1. Provide a name for your accelerator\.

1. Choose **Next**\.

## Step 2: Add Listeners<a name="getting-started-create-listeners"></a>

Create a listener to process inbound connections from your users to Global Accelerator\.

**Note**  
To complete this task by using an API operation instead of the console, see [https://docs.aws.amazon.com/global-accelerator/latest/api/API_CreateListener.html](https://docs.aws.amazon.com/global-accelerator/latest/api/API_CreateListener.html) in the *AWS Global Accelerator API Reference*\.

1. On the **Add listener** page, enter the ports or port ranges that you want to associate with the listener\. Listeners support ports 1\-65535\.

1. Choose the protocol for the ports that you entered\.

1. Optionally, choose to enable client affinity\. Client affinity for a listener means that Global Accelerator ensures that connections from a specific source \(client\) IP address are always routed to the same endpoint\. To enable this behavior, in the dropdown list, choose **Source IP**\.

   The default is **None**, which means that client affinity is not enabled and Global Accelerator distributes traffic equally between the endpoints in the endpoint groups for the listener\.

   For more information, see [Client Affinity](about-listeners-client-affinity.md)\.

1. Optionally, choose **Add listener** to add an additional listener\.

1. When you're finished adding listeners, choose **Next**\.

## Step 3: Add Endpoint Groups<a name="getting-started-add-endpoint-groups"></a>

Add one or more endpoint groups, each of which is associated with a specific AWS Region\.

**Note**  
To complete this task by using an API operation instead of the console, see [https://docs.aws.amazon.com/global-accelerator/latest/api/API_CreateEndpointGroup.html](https://docs.aws.amazon.com/global-accelerator/latest/api/API_CreateEndpointGroup.html) in the *AWS Global Accelerator API Reference*\.

1. On the **Add endpoint groups** page, in the section for a listener, choose a **Region** from the dropdown list\.

1. Optionally, for **Traffic dial**, enter a number from 0 to 100 to set a percentage of traffic for this endpoint group\. The percentage is applied only to the traffic already directed to this endpoint group, not all listener traffic\. By default, the traffic dial for an endpoint group is set to 100 \(that is, 100%\)\. 

1. Optionally, for custom health check values, choose **Configure health checks**\. When you configure health check settings, Global Accelerator uses the settings for health checks for Elastic IP address endpoints\. For Network Load Balancer and Application Load Balancer endpoints, Global Accelerator uses the health check settings that you've already configured for the load balancers themselves\. For more information, see [Health Check Options](about-endpoint-groups-health-check-options.md)\.

1. Optionally, choose **Add endpoint group** to add additional endpoint groups for this listener or other listeners\.

1. Choose **Next**\.

## Step 4: Add Endpoints<a name="getting-started-add-endpoints"></a>

Add one or more endpoints that are associated with specific endpoint groups\. This step isn't required, but no traffic is directed to endpoints in a Region unless the endpoints are included in an endpoint group\.

**Note**  
If you're creating your accelerator programmatically, you add endpoints as part of adding endpoint groups\. For more information, see [https://docs.aws.amazon.com/global-accelerator/latest/api/API_CreateEndpointGroup.html](https://docs.aws.amazon.com/global-accelerator/latest/api/API_CreateEndpointGroup.html) in the *AWS Global Accelerator API Reference*\.

1. On the **Create endpoints** page, in the section for an endpoint, choose an endpoint from the dropdown list\.

1. Optionally, for **Weight**, enter a number from 0 to 255 to set a weight for routing traffic to this endpoint\. When you add weights to endpoints, you configure Global Accelerator to route traffic based on proportions that you specify\. By default, all endpoints have a weight of 128\. For more information, see [Endpoint Weights](about-endpoints-endpoint-weights.md)\.

1. Optionally, choose **Add endpoint** to add more endpoints\.

1. Choose **Next**\.

After you choose **Next**, on the Global Accelerator dashboard you'll see a message that your accelerator is in progress\. When the process is finished, the accelerator status in the dashboard is **Active**\. 

## Step 5: Test Your Accelerator<a name="getting-started-create-and-test"></a>

Take steps to test your accelerator to make sure that traffic is being directed to your endpoints\.

## Step 6: Delete Your Accelerator<a name="getting-started-delete-accelerator"></a>

If you created an accelerator as a test or if you're no longer using an accelerator, you can delete it\. On the console, disable the accelerator, and then you can delete it\. You don't have to remove listeners and endpoint groups from the accelerator\.

To delete an accelerator by using an API operation instead of the console, you must first remove all listeners and endpoint groups that are associated with the accelerator as well as disable it\. For more information, see the [https://docs.aws.amazon.com/global-accelerator/latest/api/API_DeleteAccelerator.html](https://docs.aws.amazon.com/global-accelerator/latest/api/API_DeleteAccelerator.html) operation in the *AWS Global Accelerator API Reference*\.
+ Open the Global Accelerator console at [ https://us\-west\-2\.console\.aws\.amazon\.com/ec2/v2/home?region=us\-west\-2\#Global Accelerator:](https://us-west-2.console.aws.amazon.com/ec2/v2/home?region=us-west-2#GlobalAccelerator:)\. 
+ Choose the accelerator that you want to delete\.
+ Choose **Edit**\.
+ Choose **Disable accelerator**, and then choose **Save**\.
+ Choose the accelerator that you want to delete\.
+ Choose **Delete accelerator**\.
+ In the confirmation dialog box, choose **Delete**\.