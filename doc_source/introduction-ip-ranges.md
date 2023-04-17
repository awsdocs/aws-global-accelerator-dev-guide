# Location and IP address ranges of Global Accelerator Edge servers<a name="introduction-ip-ranges"></a>

For a list of Global Accelerator Edge server locations, see *Global Edge Network* on the [AWS Global Accelerator features](https://aws.amazon.com/global-accelerator/features/) page\.

AWS publishes its current IP address ranges in JSON format\. To view the current ranges, download [ ip\-ranges\.json](https://ip-ranges.amazonaws.com/ip-ranges.json)\. For more information, see [AWS IP address ranges](https://docs.aws.amazon.com/general/latest/gr/aws-ip-ranges.html) in the *Amazon Web Services General Reference*\.

Before you work with the `ip-ranges.json` file, first review the following information:
+ To find the IP address ranges that are associated with AWS Global Accelerator Edge servers, search `ip-ranges.json` for the following string:

  `"service": "GLOBALACCELERATOR"`
+ Global Accelerator entries that include `"region": "GLOBAL"` refer to the static IP addresses that are allocated to accelerators\. If you want to filter for traffic through your accelerator that comes from points of presence \(POPs\) in one area, filter for entries that include a specific geographical area, such as `us-*` or `eu-*`\. So, for example, if you filter for `us-*`, you will see only traffic coming through POPs in the United States \(U\.S\.\)\.
+ You might see client IP addresses in AWS WAF, instead of Global Accelerator IP addresses\. Client IP addresses appear in AWS WAF when you configure Global Accelerator for client IP address preservation and you enable AWS WAF to block connections from your Application Load Balancers that don't come from Global Accelerator\.