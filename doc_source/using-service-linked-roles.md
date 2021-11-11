# Service\-linked role for Global Accelerator<a name="using-service-linked-roles"></a>

AWS Global Accelerator uses an AWS Identity and Access Management \(IAM\)[ service\-linked role](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_terms-and-concepts.html#iam-term-service-linked-role)\. A service\-linked role is a unique type of IAM role that is linked directly to a service\. Service\-linked roles are predefined by the service and include all of the permissions that the service requires to call other AWS services on your behalf\.

Global Accelerator uses the following IAM service\-linked role:
+ **AWSServiceRoleForGlobalAccelerator**–Global Accelerator uses this role to allow Global Accelerator to create and manage resources required for client IP address preservation\.

Global Accelerator automatically creates a role named AWSServiceRoleForGlobalAccelerator when the role is first required to support a Global Accelerator API operation\. The AWSServiceRoleForGlobalAccelerator role allows Global Accelerator create and manage resources necessary for client IP address preservation\. This role is required for using accelerators in Global Accelerator\. The ARN for the AWSServiceRoleForGlobalAccelerator role looks like this:

`arn:aws:iam::123456789012:role/aws-service-role/globalaccelerator.amazonaws.com/AWSServiceRoleForGlobalAccelerator`

A service\-linked role makes setting up and using Global Accelerator easier because you don’t have to manually add the necessary permissions\. Global Accelerator defines the permissions of its service\-linked role, and only Global Accelerator can assume the roles\. The defined permissions include the trust policy and the permissions policy\. The permissions policy cannot be attached to any other IAM entity\.

You must remove any associated Global Accelerator resources before you can delete a service\-linked role\. This helps protect your Global Accelerator resources by making sure that you don't remove a service\-linked role that is still required to access active resources\.

For information about other services that support service\-linked roles, see [AWS services that work with IAM](https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_aws-services-that-work-with-iam.html) and look for the services that have **Yes **in the **Service\-linked role** column\.

## Service\-linked role permissions for Global Accelerator<a name="slr-permissions"></a>

Global Accelerator uses a service\-linked role named **AWSServiceRoleForGlobalAccelerator**\. The following sections describe the permissions for the role\.

### Service\-linked role permissions<a name="slr-permissions-aga"></a>

This service\-linked role allows Global Accelerator to manage EC2 Elastic Network Interfaces and security groups, and to help diagnose errors\.

The AWSServiceRoleForGlobalAccelerator service\-linked role trusts the following service to assume the role:
+ `globalaccelerator.amazonaws.com`

The role permissions policy allows Global Accelerator to complete the following actions on the specified resources, as shown in the policy:

```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "ec2:CreateNetworkInterface",
                "ec2:DescribeNetworkInterfaces",
                "ec2:DescribeInstances",
                "ec2:DescribeInternetGateways",
                "ec2:DescribeSubnets",
                "ec2:DescribeRegions",
                "ec2:ModifyNetworkInterfaceAttribute",
                "ec2:DeleteNetworkInterface"
            ],
            "Resource": "*"
        },
        {
            "Effect": "Allow",
            "Action": [
                "ec2:DeleteSecurityGroup",
                "ec2:AssignIpv6Addresses",
                "ec2:UnassignIpv6Addresses"
            ],
            "Resource": "*",
            "Condition": {
                "StringEquals": {
                    "ec2:ResourceTag/AWSServiceName": "GlobalAccelerator"
                }
            }
        },
        {
            "Effect": "Allow",
            "Action": [
                "ec2:CreateSecurityGroup",
                "ec2:DescribeSecurityGroups"
            ],
            "Resource": "*"
        },
        {
            "Effect": "Allow",
            "Action": "elasticloadbalancing:DescribeLoadBalancers",
            "Resource": "*"
        },
        {
            "Effect": "Allow",
            "Action": "ec2:CreateTags",
            "Resource": [
                "arn:aws:ec2:*:*:security-group/*",
                "arn:aws:ec2:*:*:network-interface/*"
            ]
        }
    ]
}
```

You must configure permissions to allow an IAM entity \(such as a user, group, or role\) to delete the Global Accelerator service\-linked role\. For more information, see [Service\-Linked Role Permissions](https://docs.aws.amazon.com/IAM/latest/UserGuide/using-service-linked-roles.html#service-linked-role-permissions) in the *IAM User Guide*\.

## Creating the service\-linked role for Global Accelerator<a name="create-slr"></a>

You don't manually create the service\-linked role for Global Accelerator\. The service creates the role for you automatically the first time that you create an accelerator\. If you remove your Global Accelerator resources and delete the service\-linked role, the service creates the role again automatically when you create a new accelerator\.

## Editing the Global Accelerator service\-linked role<a name="edit-slr"></a>

Global Accelerator does not allow you to edit the AWSServiceRoleForGlobalAccelerator service\-linked role\. After the service has created a service\-linked role, you cannot change the name of the role because various entities might reference the role\. However, you can edit the description of a role by using IAM\. For more information, see [Editing a Service\-Linked Role](https://docs.aws.amazon.com/IAM/latest/UserGuide/using-service-linked-roles.html#edit-service-linked-role) in the *IAM User Guide*\.

## Deleting the Global Accelerator service\-linked role<a name="delete-slr"></a>

If you no longer need to use Global Accelerator, we recommend that you delete the service\-linked role\. That way you don’t have unused entities that are not actively monitored or maintained\. However, you must clean up the Global Accelerator resources in your account before you can manually delete the roles\.

After you have disabled and deleted your accelerators, then you can delete the service\-linked role\. For more information about deleting accelerators, see [ Creating or updating a standard accelerator](about-accelerators.creating-editing.md)\.

**Note**  
If you have disabled and deleted your accelerators but Global Accelerator hasn't finished updating, service\-linked role deletion might fail\. If that happens, wait for a few minutes, and then try the service\-linked role deletion steps again\.

**To manually delete the AWSServiceRoleForGlobalAccelerator service\-linked role**

1. Sign in to the AWS Management Console and open the IAM console at [https://console\.aws\.amazon\.com/iam/](https://console.aws.amazon.com/iam/)\.

1. In the navigation pane of the IAM console, choose **Roles**\. Then select the check box next to the role name that you want to delete, not the name or row itself\.

1. For **Role** actions at the top of the page, choose **Delete role**\.

1. In the confirmation dialog box, review the service last accessed data, which shows when each of the selected roles last accessed an AWS service\. This helps you to confirm whether the role is currently active\. If you want to proceed, choose **Yes, Delete** to submit the service\-linked role for deletion\.

1. Watch the IAM console notifications to monitor the progress of the service\-linked role deletion\. Because the IAM service\-linked role deletion is asynchronous, after you submit the role for deletion, the deletion task can succeed or fail\. For more information, see [Deleting a service\-linked role](https://docs.aws.amazon.com/IAM/latest/UserGuide/using-service-linked-roles.html#delete-service-linked-role) in the *IAM User Guide*\.

## Updates to the policy for the Global Accelerator service\-linked role \(an AWS managed policy\)<a name="security-iam-awsmanpol-updates"></a>

View details about updates to `AWSGlobalAcceleratorSLRPolicy`, the AWS managed policy for the Global Accelerator service\-linked role\. The following table lists updates since this service began tracking changes to the policy\. For automatic alerts about changes to this page, subscribe to the RSS feed on the AWS Global Accelerator [Document history](WhatsNew.md) page\.


| Change | Description | Date | 
| --- | --- | --- | 
|   [AWSGlobalAcceleratorSLRPolicy](https://console.aws.amazon.com/iam/home#policies/arn:aws:iam::aws:policy/aws-service-role/AWSGlobalAcceleratorSLRPolicy) – Updated policy  |  Global Accelerator added new permissions to support IPv6 addresses\. Global Accelerator uses `ec2:AssignIpv6Addresses` to update the GlobalAccelerator ENI on a customer subnet with an IPv6 address for sending and receiving IPv6 traffic, and uses `UnassignIpv6Addresses` to remove the IPv6 address when it's no longer needed\.  | November 15, 2021 | 
|   [AWSGlobalAcceleratorSLRPolicy](https://console.aws.amazon.com/iam/home#policies/arn:aws:iam::aws:policy/aws-service-role/AWSGlobalAcceleratorSLRPolicy) – Updated policy  |  Global Accelerator added a new permission to help Global Accelerator to diagnose errors\. Global Accelerator uses `ec2:DescribeRegions` to determine the AWS Region that a customer is in, which can help Global Accelerator to troubleshoot errors\.  | May 18, 2021 | 
|  Global Accelerator started tracking changes  |  Global Accelerator started tracking changes for its AWS managed policies\.  | May 18, 2021 | 

## Supported Regions for Global Accelerator service\-linked roles<a name="slr-regions"></a>

Global Accelerator supports using service\-linked roles in AWS Regions where Global Accelerator is supported\.

For a list of the AWS Regions where Global Accelerator and other services are currently supported, see the [AWS Region Table](https://aws.amazon.com/about-aws/global-infrastructure/regional-product-services/)\.