# Using tag\-based policies with AWS Global Accelerator<a name="security_iam-tag-policies"></a>

When you design IAM policies, you might set granular permissions by granting access to specific resources\. However, as the number of resources that you manage grows, this task becomes more difficult\. Tagging a resource, and then using tags in policy statement conditions can make this task easier\. You can grant access in bulk to any resource that has a certain tag\. You can repeatedly apply this tag to relevant resources, when you create the resource or by updating the resource later\.

Using tags in conditions is one way to control access to resources and requests\. Tags can be attached to a resource or passed in the request to services that support tagging\. In Global Accelerator, only accelerators can include tags\. For more information about tagging in Global Accelerator, see [Tagging in AWS Global Accelerator](tagging-in-global-accelerator.md)\.

When you create an IAM policy, you can use tag condition keys to control:
+ Which users can perform actions on an accelerator, based on tags that it already has\.
+ What tags can be passed in an action's request\.
+ Whether specific tag keys can be used in a request\.

For example, the AWS `GlobalAcceleratorFullAccess` managed user policy gives users unlimited permission to perform any Global Accelerator action on any resource\. The following policy limits this power and denies unauthorized users permission to perform any Global Accelerator action on any *production* accelerators\. A customer's administrator must attach this IAM policy to unauthorized IAM users, in addition to the managed user policy\.

```
{ 
   "Version":"2012-10-17",
   "Statement":[ 
      { 
         "Effect":"Deny",
         "Action":"*",
         "Resource":"*",
         "Condition":{ 
            "ForAnyValue:StringEquals":{ 
               "aws:RequestTag/stage":"prod"
            }
         }
      },
      { 
         "Effect":"Deny",
         "Action":"*",
         "Resource":"*",
         "Condition":{ 
            "ForAnyValue:StringEquals":{ 
               "aws:ResourceTag/stage":"prod"
            }
         }
      }
   ]
}
```

For the complete syntax and semantics of tag condition keys, see [ Control access using IAM tags](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_iam-tags.html) in the *IAM User Guide*\.