# Custom routing accelerators in AWS Global Accelerator<a name="about-custom-routing-accelerators"></a>

A *custom routing accelerator* in AWS Global Accelerator lets you use custom application logic to direct one or more users to a specific destination among many destinations, while using the AWS global network to improve the availability and performance of your application\. 

A custom routing accelerator routes traffic only to ports on Amazon EC2 instances that are running in virtual private cloud \(VPC\) subnets\. With a custom routing accelerator, Global Accelerator does not route traffic based on the geoproximity or health of the endpoint\. To learn more, see [How custom routing accelerators work in AWS Global Accelerator](about-custom-routing-how-it-works.md)\.

When you create an accelerator, by default, Global Accelerator provides you with a set of two static IP addresses\. If you bring your own IP address range to AWS \(BYOIP\), you can instead assign static IP addresses from your own pool to use with your accelerator\. For more information, see [Bring your own IP addresses \(BYOIP\) in AWS Global Accelerator](using-byoip.md)\.

**Important**  
The IP addresses are assigned to your accelerator for as long as it exists, even if you disable the accelerator and it no longer accepts or routes traffic\. However, when you *delete* an accelerator, you lose the Global Accelerator static IP addresses that are assigned to the accelerator, so you can no longer route traffic by using them\. As a best practice, ensure that you have permissions in place to avoid inadvertently deleting accelerators\. You can use IAM policies such as tag\-based permissions with Global Accelerator to limit the users who have permissions to delete an accelerator\. For more information, see [ Tag\-based policies](auth-and-access-control.md#access-control-manage-access-tag-policies)\.

This section explains how to create, edit, or delete a custom routing accelerator on the Global Accelerator console\. To learn about using API operations with Global Accelerator, see the [AWS Global Accelerator API Reference](https://docs.aws.amazon.com/global-accelerator/latest/api/Welcome.html)\.

**Topics**
+ [Creating or updating a custom routing accelerator](#about-custom-routing-accelerators.creating-editing)
+ [Viewing your custom routing accelerators](#about-custom-routing-accelerators.viewing)
+ [Deleting a custom routing accelerator](#about-custom-routing-accelerators.deleting)

## Creating or updating a custom routing accelerator<a name="about-custom-routing-accelerators.creating-editing"></a>

## To create a custom routing accelerator

1. Open the Global Accelerator console at [ https://console\.aws\.amazon\.com/globalaccelerator/home](https://console.aws.amazon.com/globalaccelerator/home)\. 

1. Choose **Create accelerator**\.

1. Provide a name for your accelerator\.

1. For **Accelerator type**, select **Custom routing**\.

1. Optionally, if you have brought your own IP address range to AWS \(BYOIP\), you can specify static IP addresses for your accelerator from that address pool\. Make this choice for each of the two static IP addresses for your accelerator\.
   + For each static IP address, choose the IP address pool to use\.
   + If you chose your own IP address pool, also choose a specific IP address from the pool\. If you chose the default Amazon IP address pool, Global Accelerator assigns a specific IP address to your accelerator\.

1. Optionally, add one or more tags to help you identify your accelerator resources\.

1. Choose **Next** to go to the next pages in the wizard to add listeners, endpoint groups, and VPC subnet endpoints\.

## To edit a custom routing accelerator

1. Open the Global Accelerator console at [ https://console\.aws\.amazon\.com/globalaccelerator/home](https://console.aws.amazon.com/globalaccelerator/home)\. 

1. In the list of custom routing accelerators, choose one, and then choose **Edit**\.

1. On the **Edit accelerator** page, make any changes that you like\. For example, you can disable the accelerator so that you can delete it\.

1. Choose **Save**\.

## Viewing your custom routing accelerators<a name="about-custom-routing-accelerators.viewing"></a>

You can view information about your custom routing accelerators on the console\. To see descriptions of your custom routing accelerators programmatically, see [ListCustomRoutingAccelerator](https://docs.aws.amazon.com/global-accelerator/latest/api/API_ListCustomRoutingAccelerator.html) and [DescribeCustomRoutingAccelerator](https://docs.aws.amazon.com/global-accelerator/latest/api/API_DescribeCustomRoutingAccelerator.html) in the AWS Global Accelerator API Reference\.

## To view information your custom routing accelerators

1. Open the Global Accelerator console at [ https://console\.aws\.amazon\.com/globalaccelerator/home](https://console.aws.amazon.com/globalaccelerator/home)\. 

1. To see details about an accelerator, choose an accelerator, and then choose **View**\.

## Deleting a custom routing accelerator<a name="about-custom-routing-accelerators.deleting"></a>

If you created a custom routing accelerator as a test, or if you're no longer using an accelerator, you can delete it\. On the console, disable the accelerator, and then you can delete it\. You don't have to remove listeners and endpoint groups from the accelerator\.

To delete a custom routing accelerator by using an API operation instead of the console, you must first remove all listeners and endpoint groups that are associated with the accelerator, and then disable it\. For more information, see the [DeleteAccelerator](https://docs.aws.amazon.com/global-accelerator/latest/api/API_DeleteAccelerator.html) operation in the *AWS Global Accelerator API Reference*\.

## To disable a custom routing accelerator

1. Open the Global Accelerator console at [ https://console\.aws\.amazon\.com/globalaccelerator/home](https://console.aws.amazon.com/globalaccelerator/home)\. 

1. In the list, choose an accelerator that you want to disable\.

1. Choose **Edit**\.

1. Choose **Disable accelerator**, and then choose **Save**\.

## To delete a custom routing accelerator

1. Open the Global Accelerator console at [ https://console\.aws\.amazon\.com/globalaccelerator/home](https://console.aws.amazon.com/globalaccelerator/home)\. 

1. In the list, choose an accelerator that you want to delete\.

1. Choose **Delete**\.
**Note**  
If you haven't disabled the accelerator, **Delete** is unavailable\. To disable the accelerator, see the previous procedure\.

1. In the confirmation dialog box, choose **Delete**\.
**Important**  
When you delete an accelerator, you lose the static IP addresses that are assigned to the accelerator, so you can no longer route traffic by using them\.