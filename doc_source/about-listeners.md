# Listeners in AWS Global Accelerator<a name="about-listeners"></a>

With AWS Global Accelerator, you add listeners that process inbound connections from clients based on the ports and protocols that you specify\. You define a listener when you create your accelerator, and you can add more listeners at any time\. You associate each listener with one or more endpoint groups, and you associate each endpoint group with one AWS Region\.

**Topics**
+ [Adding, Editing, or Removing a Listener](#about-listeners.creating-listeners)
+ [Client Affinity](#about-listeners-client-affinity)

## Adding, Editing, or Removing a Listener<a name="about-listeners.creating-listeners"></a>

This section explains how to work with listeners on the AWS Global Accelerator console\. To complete these tasks by using an API operation instead of the console, see [https://docs.aws.amazon.com/global-accelerator/latest/api/API_CreateListener.html](https://docs.aws.amazon.com/global-accelerator/latest/api/API_CreateListener.html), [https://docs.aws.amazon.com/global-accelerator/latest/api/API_UpdateListener.html](https://docs.aws.amazon.com/global-accelerator/latest/api/API_UpdateListener.html), and [https://docs.aws.amazon.com/global-accelerator/latest/api/API_DeleteListener.html](https://docs.aws.amazon.com/global-accelerator/latest/api/API_DeleteListener.html) in the *AWS Global Accelerator API Reference*\.

## To add a listener

1. Open the Global Accelerator console at [ https://us\-west\-2\.console\.aws\.amazon\.com/ec2/v2/home?region=us\-west\-2\#Global Accelerator:](https://us-west-2.console.aws.amazon.com/ec2/v2/home?region=us-west-2#GlobalAccelerator:)\. 

1. Choose **Add listener**\.

1. On the **Add listener** page, enter the ports or port ranges that you want to associate with the listener\. Listeners support ports 1\-65535\.

1. Choose the protocol for the ports that you entered\.

1. Optionally, choose to enable client affinity\. Client affinity for a listener means that Global Accelerator ensures that connections from a specific source \(client\) IP address are always routed to the same endpoint\. To enable this behavior, in the dropdown list, choose **Source IP**\.

   The default is **None**, which means that client affinity is not enabled and Global Accelerator distributes traffic equally between the endpoints in the endpoint groups for the listener\.

   For more information, see [Client Affinity](#about-listeners-client-affinity)\.

1. Choose **Add listener**\.

## To edit a listener

1. Open the Global Accelerator console at [ https://us\-west\-2\.console\.aws\.amazon\.com/ec2/v2/home?region=us\-west\-2\#Global Accelerator:](https://us-west-2.console.aws.amazon.com/ec2/v2/home?region=us-west-2#GlobalAccelerator:)\. 

1. Choose **Edit listener**\.

1. On the **Edit listener** page, change the ports, port ranges, or protocols that you want to associate with the listener\.

1. Optionally, choose to enable client affinity\. Client affinity for a listener means that Global Accelerator ensures that connections from a specific source \(client\) IP address are always routed to the same endpoint\. To enable this behavior, in the dropdown list, choose **Source IP**\.

   The default is **None**, which means that client affinity is not enabled and Global Accelerator distributes traffic equally between the endpoints in the endpoint groups for the listener\.

   For more information, see [Client Affinity](#about-listeners-client-affinity)\.

1. Choose **Save**\.

## To remove a listener

1. Open the Global Accelerator console at [ https://us\-west\-2\.console\.aws\.amazon\.com/ec2/v2/home?region=us\-west\-2\#Global Accelerator:](https://us-west-2.console.aws.amazon.com/ec2/v2/home?region=us-west-2#GlobalAccelerator:)\. 

1. Choose **Remove listener**\.

1. In the confirmation dialog box, choose **Remove**\.

## Client Affinity<a name="about-listeners-client-affinity"></a>

If you have stateful applications, you can choose to have Global Accelerator direct all requests from a user at a specific source \(client\) IP address to the same endpoint resource, to maintain client affinity\.

By default, client affinity for a listener is set to **None** and Global Accelerator distributes traffic equally between the endpoints in the endpoint groups for the listener\.

Global Accelerator uses a consistent\-flow hashing algorithm to choose the optimal endpoint for a user's connection\. If you configure client affinity for your Global Accelerator resource to be **None**, Global Accelerator uses the 5\-tuple properties—source IP, source port, destination IP, destination port, and protocol—to select the hash value\. Next, it chooses the endpoint that provides the best performance\. If a given client uses different ports to connect to Global Accelerator and you've specified this setting, Global Accelerator can't ensure that connections from the client are always routed to the same endpoint\. 

If you want to maintain client affinity by routing a specific user—identified by their source IP address—to the same endpoint each time they connect, set client affinity to **Source IP**\. When you specify this option, Global Accelerator uses the 2\-tuple properties—source IP and destination IP—to select the hash value and route the user to the same endpoint whenever they connect\.