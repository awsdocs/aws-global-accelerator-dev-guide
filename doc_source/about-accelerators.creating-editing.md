# Creating or updating a standard accelerator<a name="about-accelerators.creating-editing"></a>

This section explains how to create or update standard accelerators on the console\. To work with Global Accelerator programmatically, see the [AWS Global Accelerator API Reference](https://docs.aws.amazon.com/global-accelerator/latest/api/Welcome.html)\.

# To create a standard accelerator

1. Open the Global Accelerator console at [ https://console\.aws\.amazon\.com/globalaccelerator/home](https://console.aws.amazon.com/globalaccelerator/home)\. 

1. Choose **Create accelerator**\.

1. Provide a name for your accelerator\.

1. For **Accelerator type**, select **Standard**\.

1. For **Address type**, select **IPv4** or **Dual\-stack**\.

1. Optionally, if you brought your own IP address ranges to AWS \(BYOIP\), you can specify a static IP address for your accelerator, one from each address pool\. Make this choice for each of the two static IP addresses for your accelerator\.
   + For each static IP address, choose the IP address pool to use\.
**Note**  
You must choose a different IP address pool for each static IP address\. This restriction is because Global Accelerator assigns each address range to a different network zone, for high availability\.
   + If you chose your own IP address pool, also choose a specific IP address from the pool\. If you choose the default Amazon IP address pool, Global Accelerator assigns a specific IP address to your accelerator\.

1. Optionally, add one or more tags to help you identify your accelerator resources\.

1. Choose **Next** to add listeners, endpoint groups, and endpoints\.

# To edit a standard accelerator

1. Open the Global Accelerator console at [ https://console\.aws\.amazon\.com/globalaccelerator/home](https://console.aws.amazon.com/globalaccelerator/home)\. 

1. In the list of accelerators, choose one, and then choose **Edit**\.

1. On the **Edit accelerator** page, make changes, such as the following:
   + Change the name of the accelerator\.
   + Disable the accelerator so that it no longer accepts or routes traffic, or so that you can delete it\. 
   + Enable the accelerator, if it is disabled\.
   + Update the IP address type\. If it's set to IPv4, change it to dual\-stack\. Or if it's dual\-stack, change it to IPv4\.
   + Update tags\.

1. Choose **Save changes**\.

If you disable an accelerator, be aware of the following:
+ Static IP addresses remain assigned to your accelerator even if you disable the accelerator and it no longer accepts or routes traffic\. Your accelerator retains the same static IP addresses for as long as the accelerator exists\.
+ If you delete the accelerator, however, you lose the static IP addresses that are assigned to it\. At that time, you can no longer route traffic by using the addresses\.

If you make changes to the IP address type, be aware of the following:
+ Only an accelerator that has dual\-stack endpoints can be changed to an IP address type of dual\-stack\.
+ If you change the IP address type for an accelerator from dual\-stack to IPv4, Global Accelerator saves the IPv6 IP addresses that are assigned to the accelerator\. This means that if you change the IP address type for the accelerator back to dual\-stack, the original IPv6 static IP addresses are restored for the accelerator\. 

If you want to change other functionality for your accelerator, such as adding or removing endpoints, updating traffic dials, or adjusting endpoint weights, see the specific sections that cover those topics, such as the following:
+ [Adding, editing, or removing a standard listener](about-listeners.creating-listeners.md)
+ [ Adding, editing, or removing a standard endpoint group](about-endpoint-groups.create-endpoint-group.md)
+ [Adding, editing, or removing a standard endpoint](about-endpoints-adding-endpoints.md)