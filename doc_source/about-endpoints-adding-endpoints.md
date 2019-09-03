# Adding, Editing, or Removing an Endpoint<a name="about-endpoints-adding-endpoints"></a>

You add endpoints to endpoint groups so that traffic can be directed to your resources\. You can edit an endpoint to change the weight for the endpoint\. Or you can remove an endpoint from your accelerator by removing it from an endpoint group\. Removing an endpoint doesn't affect the endpoint itself, but Global Accelerator can no longer direct traffic to that resource\.

This section explains how to work with endpoints on the AWS Global Accelerator console\. If you want to use API operations with AWS Global Accelerator, see the [ AWS Global Accelerator API Reference](https://docs.aws.amazon.com/global-accelerator/latest/api/Welcome.html)\.

# To add an endpoint

1. Open the Global Accelerator console at [ https://us\-west\-2\.console\.aws\.amazon\.com/ec2/v2/home?region=us\-west\-2\#Global Accelerator:](https://us-west-2.console.aws.amazon.com/ec2/v2/home?region=us-west-2#GlobalAccelerator:)\. 

1. In the **Global Accelerator resources** section, choose an accelerator\.

1. In the **Listeners** section, for **Listener ID**, choose the ID of a listener\.

1. In the **Endpoint groups** section, for **Endpoint group ID**, choose the ID of the endpoint group that you want to add an endpoint to\.

1. In the **Endpoints** section, choose **Add endpoint**\.

1. On the **Add endpoints** page, choose an endpoint from the dropdown list\.

1. Optionally, for **Weight**, enter a number from 0 to 255 to set a weight for routing traffic to this endpoint\. When you add weights to endpoints, you configure Global Accelerator to route traffic based on proportions that you specify\. By default, all endpoints have a weight of 128\. For more information, see [Endpoint Weights](about-endpoints-endpoint-weights.md)\.

1. Optionally, enable client IP address preservation for an Application Load Balancer endpoint\. Under **Preserve client IP address**, select **Preserve address**\. For more information, see [ Viewing Client IP Addresses in AWS Global Accelerator](introduction-how-it-works-client-ip.md)\.

1. Choose **Add endpoint**\.

# To edit an endpoint

You can edit an endpoint configuration to change the weight\. For more information, see [Endpoint Weights](about-endpoints-endpoint-weights.md)\.

1. Open the Global Accelerator console at [ https://us\-west\-2\.console\.aws\.amazon\.com/ec2/v2/home?region=us\-west\-2\#Global Accelerator:](https://us-west-2.console.aws.amazon.com/ec2/v2/home?region=us-west-2#GlobalAccelerator:)\. 

1. In the **Listeners** section, for **Listener ID**, choose the ID of a listener\.

1. In the **Endpoint groups** section, for **Endpoint group ID**, choose the ID of the endpoint group\.

1. Choose **Edit endpoint**\.

1. On the **Edit endpoint** page, change the weight for the endpoint resource\.

1. Choose **Save**\.

# To remove an endpoint

1. Open the Global Accelerator console at [ https://us\-west\-2\.console\.aws\.amazon\.com/ec2/v2/home?region=us\-west\-2\#Global Accelerator:](https://us-west-2.console.aws.amazon.com/ec2/v2/home?region=us-west-2#GlobalAccelerator:)\. 

1. In the **Listeners** section, for **Listener ID**, choose the ID of a listener\.

1. In the **Endpoint groups** section, for **Endpoint group ID**, choose the ID of the endpoint group\.

1. Choose **Remove endpoint**\.

1. In the confirmation dialog box, choose **Remove**\.