# Quotas for AWS Global Accelerator<a name="limits-global-accelerator"></a>

Your AWS account has specific quotas, also known as limits, related to AWS Global Accelerator\.

The Service Quotas console provides information about Global Accelerator quotas\. Along with viewing the default quotas, you can use the Service Quotas console to [ request quota increases](https://console.aws.amazon.com/servicequotas/home?region=us-east-1#!/services/globalaccelerator/quotas) for adjustable quotas\. Note that you must be in US East \(N\. Virginia\) when you request quota increases for Global Accelerator\.

**Topics**
+ [General quotas](#limits-global-accelerator-general)
+ [Quotas for endpoints per endpoint group](#limits-global-accelerator-endpoints)
+ [Related quotas](#limits-global-accelerator-additional)

## General quotas<a name="limits-global-accelerator-general"></a>

The following are overall quotas for Global Accelerator\.


****  

| Entity | Quota | 
| --- | --- | 
| Accelerators per AWS account  | 20 You can [ request a quota increase](https://console.aws.amazon.com/servicequotas/home?region=us-east-1#!/services/globalaccelerator/quotas)\. | 
| Listeners per accelerator  | 10 You can [ request a quota increase](https://console.aws.amazon.com/servicequotas/home?region=us-east-1#!/services/globalaccelerator/quotas)\. | 
| Port ranges per listener | 10 | 
| Port overrides per endpoint group | 10 You can [ request a quota increase](https://console.aws.amazon.com/servicequotas/home?region=us-east-1#!/services/globalaccelerator/quotas)\. | 

## Quotas for endpoints per endpoint group<a name="limits-global-accelerator-endpoints"></a>

The following are Global Accelerator quotas that apply to the number of endpoints in endpoint groups\.


****  

| Entity | Description | Quota | 
| --- | --- | --- | 
| Endpoint groups with more than one endpoint type  | Number of endpoints in an endpoint group containing more than one endpoint type\. | 10 | 
| Endpoint groups with just Application Load Balancers  | Number of Application Load Balancers in an endpoint group containing only Application Load Balancer endpoints\. | 10 | 
| Endpoint groups with just Network Load Balancers  | Number of Network Load Balancers in an endpoint group containing only Network Load Balancer endpoints\. | 10 | 
| Endpoint groups with just Amazon EC2 instances  | Number of EC2 instances in an endpoint group containing only EC2 instance endpoints\. | 10 You can [ request a quota increase](https://console.aws.amazon.com/servicequotas/home?region=us-east-1#!/services/globalaccelerator/quotas)\. | 
| Endpoint groups with just Elastic IP addresses  | Number of Elastic IP addresses in an endpoint group containing only Elastic IP address endpoints\. | 10 You can [ request a quota increase](https://console.aws.amazon.com/servicequotas/home?region=us-east-1#!/services/globalaccelerator/quotas)\. | 
| Endpoint groups with just Amazon Virtual Private Cloud subnets  | Number of Amazon VPC subnets in an endpoint group containing only subnet endpoints\. | 10 You can [ request a quota increase](https://console.aws.amazon.com/servicequotas/home?region=us-east-1#!/services/globalaccelerator/quotas)\. | 

## Related quotas<a name="limits-global-accelerator-additional"></a>

In addition to quotas in Global Accelerator, there are quotas that apply to the resources that you use as endpoints for an accelerator\. For more information, see the following:
+ [Elastic IP address quotas](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/elastic-ip-addresses-eip.html#using-instance-addressing-limit) in the *Amazon EC2 User Guide*\.
+ [Amazon EC2 service quotas](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ec2-resource-limits.html) in the *Amazon EC2 User Guide*\.
+ [Quotas for your Network Load Balancers](https://docs.aws.amazon.com/elasticloadbalancing/latest/network/load-balancer-limits.html) in the *User Guide for Network Load Balancers*\.
+ [Quotas for your Application Load Balancers](https://docs.aws.amazon.com/elasticloadbalancing/latest/application/load-balancer-limits.html) in the *User Guide for Application Load Balancers*\.
+ [Amazon VPC quotas](https://docs.aws.amazon.com/vpc/latest/userguide/amazon-vpc-limits.html) in the *Amazon VPC User Guide*\.