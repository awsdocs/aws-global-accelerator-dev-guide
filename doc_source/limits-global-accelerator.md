# Quotas for AWS Global Accelerator<a name="limits-global-accelerator"></a>

Your AWS account has the following quotas, also known as limits, related to AWS Global Accelerator\.


****  

| Entity | Quota | 
| --- | --- | 
| Accelerators per AWS account  | 20 | 
| Listeners per accelerator  | 10 | 
| Port ranges per listener | 10 | 
| Port overrides per endpoint group | 10 | 
| Endpoints per endpoint group – more than one endpoint type: The maximum number of endpoints in an endpoint group containing more than one endpoint type\. | 10 | 
| Endpoints per endpoint group – Network Load Balancers: The maximum number of Network Load Balancers in an endpoint group containing only Network Load Balancer endpoints\. | 10 | 
| Endpoints per endpoint group – Application Load Balancers: The maximum number of Application Load Balancers in an endpoint group containing only Application Load Balancer endpoints\. | 10 | 
| Endpoints per endpoint group – Elastic IP addresses: The maximum number of Elastic IP addresses in an endpoint group containing only Elastic IP address endpoints\. | 10 | 
| Endpoints per endpoint group – EC2 instances: The maximum number of EC2 instances in an endpoint group containing only EC2 instance endpoints\. | 10 | 
| Endpoints per endpoint group – VPC subnets: The maximum number of VPC subnets in an endpoint group containing only subnet endpoints\.  | 10 | 
| Tags per accelerator  | 50 | 

In addition, there are quotas for Network Load Balancers, Application Load Balancers, Amazon EC2 instances, or Elastic IP addresses that are used as endpoints for an accelerator\. For more information, see the following:
+ [Elastic IP address quota](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/elastic-ip-addresses-eip.html#using-instance-addressing-limit) in the *Amazon EC2 User Guide*\.
+ [Amazon EC2 service quotas](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ec2-resource-limits.html) in the *Amazon EC2 User Guide*\.
+ [Quotas for your Network Load Balancers](https://docs.aws.amazon.com/elasticloadbalancing/latest/network/load-balancer-limits.html) in the *User Guide for Network Load Balancers*\.
+ [Quotas for your Application Load Balancers](https://docs.aws.amazon.com/elasticloadbalancing/latest/application/load-balancer-limits.html) in the *User Guide for Application Load Balancers*\.