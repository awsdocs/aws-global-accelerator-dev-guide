# Accelerators in AWS Global Accelerator<a name="about-accelerators"></a>

An *accelerator* in AWS Global Accelerator directs traffic to optimal endpoints over the AWS global network to improve the availability and performance of your internet applications that have a global audience\. Each accelerator includes one or more listeners\. A listener processes inbound connections from clients to Global Accelerator, based on the protocol and port that you configure\. 

You create an accelerator by providing a name for it\.  When you create your accelerator, Global Accelerator provisions static IP addresses for you\. The static IP addresses are anycast from the AWS edge network to your endpoints such as Elastic IP addresses, Network Load Balancers, or Application Load Balancers\. You then associate those static IP addresses with your accelerator\. After you create your accelerator, you can edit it to change the name, or you can delete it when you no longer need it\.

This section explains how to work with an accelerator on the Global Accelerator console\. If you want to use API operations with Global Accelerator, see the [ AWS Global Accelerator API Reference](https://docs.aws.amazon.com/global-accelerator/latest/api/Welcome.html)\.

**Topics**
+ [Static IP Addresses in AWS Global Accelerator](about-static-ip-addresses.md)
+ [Creating, Editing, or Deleting an Accelerator](about-accelerators.creating-editing.md)
+ [Viewing Your Accelerators](about-accelerators.viewing.md)