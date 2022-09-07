# Standard accelerators in AWS Global Accelerator<a name="about-accelerators"></a>

A *standard accelerator* in AWS Global Accelerator directs traffic to optimal endpoints over the AWS global network to improve the availability and performance of your internet applications that have a global audience\. Each accelerator includes one or more listeners\. A listener processes inbound connections from clients to Global Accelerator, based on the protocol \(or protocols\) and port \(or port range\) that you configure\. 

## Global static IP addresses for your accelerator<a name="about-accelerators.static-ip-addresses"></a>

By default, Global Accelerator provides you with static IP addresses that are associated with your accelerator\. The static IP addresses are anycast from the AWS edge network\. 

For IPv4, Global Accelerator provides two static IPv4 addresses\. For dual\-stack, Global Accelerator provides a total of four addresses: two static IPv4 addresses and two static IPv6 addresses\. If you bring your own IP address range to AWS \(BYOIP\) to use with Global Accelerator \(IPv4 only\), you can instead assign IPv4 addresses from your own pool to use with your accelerator\. For more information, see [Bring your own IP addresses \(BYOIP\) in AWS Global Accelerator](using-byoip.md)\.

For accelerators with dual\-stack, Global Accelerator allocates the IPv6 addresses from the same two /64 CIDR prefixes\. This can help simplify steps for allow\-listing and setting ACL controls\.

You can add IPv4\-only endpoints to standard accelerators that are configured for IPv4 IP address types, but accelerators that you configure as dual\-stack require that you add only endpoints that also support dual\-stack\. Also be aware that only Application Load Balancers can be added as dual\-stack endpoints\.

**Important**  
The IP addresses are assigned to your accelerator for as long as it exists, even if you disable the accelerator and it no longer accepts or routes traffic\. However, when you *delete* an accelerator, you lose the Global Accelerator static IP addresses that are assigned to the accelerator, so you can no longer route traffic by using them\. As a best practice, ensure that you have permissions in place to avoid inadvertently deleting accelerators\. You can use IAM policies with Global Accelerator, for example, tag\-based permissions, to limit the users who have permissions to delete an accelerator\. For more information, see [ Tag\-based policies](auth-and-access-control.md#access-control-manage-access-tag-policies)\.

This section explains how to create, edit, or delete a standard accelerator on the Global Accelerator console\. If you want to use API operations with Global Accelerator, see the [AWS Global Accelerator API Reference](https://docs.aws.amazon.com/global-accelerator/latest/api/Welcome.html)\.

**Topics**
+ [Global static IP addresses for your accelerator](#about-accelerators.static-ip-addresses)
+ [Creating or updating a standard accelerator](about-accelerators.creating-editing.md)
+ [Deleting an accelerator](about-accelerators.deleting.md)
+ [Viewing your accelerators](about-accelerators.viewing.md)
+ [Add an accelerator when you create a load balancer](about-accelerators.alb-accelerator.md)
+ [Using global static IP addresses instead of regional static IP addresses](about-accelerators.eip-accelerator.md)