# Creating or updating a standard accelerator<a name="about-accelerators.creating-editing"></a>

This section explains how to create or update standard accelerators on the console\. To work with Global Accelerator programmatically, see the [AWS Global Accelerator API Reference](https://docs.aws.amazon.com/global-accelerator/latest/api/Welcome.html)\.

**Important**  
Make sure that you’re in the US West \(Oregon\) Region\. You must be in this Region to create or update accelerators\.

# To create a standard accelerator

1. Open the Global Accelerator console at [ https://us\-west\-2\.console\.aws\.amazon\.com/ec2/v2/home?region=us\-west\-2\#Global Accelerator:](https://us-west-2.console.aws.amazon.com/ec2/v2/home?region=us-west-2#GlobalAccelerator:)\. 

1. Choose **Create accelerator**\.

1. Provide a name for your accelerator\.

1. For **Accelerator type**, select **Standard**\.

1. Optionally, if you brought your own IP address ranges to AWS \(BYOIP\), you can specify a static IP address for your accelerator, one from each address pool\. Make this choice for each of the two static IP addresses for your accelerator\.
   + For each static IP address, choose the IP address pool to use\.
**Note**  
You must choose a different IP address pool for each static IP address\. This restriction is because Global Accelerator assigns each address range to a different network zone, for high availability\.
   + If you chose your own IP address pool, also choose a specific IP address from the pool\. If you choose the default Amazon IP address pool, Global Accelerator assigns a specific IP address to your accelerator\.

1. Optionally, add one or more tags to help you identify your accelerator resources\.

1. Choose **Next** to add listeners, endpoint groups, and endpoints\.

# To edit a standard accelerator

1. Open the Global Accelerator console at [ https://us\-west\-2\.console\.aws\.amazon\.com/ec2/v2/home?region=us\-west\-2\#Global Accelerator:](https://us-west-2.console.aws.amazon.com/ec2/v2/home?region=us-west-2#GlobalAccelerator:)\. 

1. In the list of accelerators, choose one, and then choose **Edit**\.

1. On the **Edit accelerator** page, make any changes that you like\. For example, you can disable the accelerator so that it no longer accepts or routes traffic, or so that you can delete it\. Or, if the accelerator is disabled, you can enable it\.

1. Choose **Save changes**\.