# Types of accelerators<a name="introduction-accelerator-types"></a>

There are two types of accelerators that you can use with AWS Global Accelerator: *standard accelerators* and *custom routing accelerators*\. Both types of accelerators route traffic over the AWS global network to improve performance and stability, but they're each designed for different application needs\. 

**Standard accelerator**  
By using a standard accelerator, you can improve the availability and performance of your applications running on Application Load Balancers, Network Load Balancers, or Amazon EC2 instances\. With a standard accelerator, Global Accelerator routes client traffic across regional endpoints based on geo\-proximity and endpoint health\. It also allows customers to shift client traffic across endpoints based on controls such as traffic dials and endpoint weights\. This works for a wide variety of use cases, including blue/green deployment, A/B testing, and multi\-Region deployment\. To see more use cases, see [ AWS Global Accelerator use cases](introduction-benefits-of-migrating.md)\.  
To learn more, see [Work with standard accelerators in AWS Global Accelerator](work-with-standard-accelerators.md)\.

**Custom routing accelerator**  
Custom routing accelerators work well for scenarios where you want to use custom application logic to direct one or more users to a specific destination and port among many, while still gaining the performance benefits of Global Accelerator\. One example is VoIP applications that assign multiple callers to a specific media server to start voice, video, and messaging sessions\. Another example is online real\-time gaming applications where you want to assign multiple players to a single session on a game server based on factors such as geographic location, player skill, and game mode\.  
To learn more, see [Work with custom routing accelerators in AWS Global Accelerator](work-with-custom-routing-accelerators.md)\.

Based on your specific needs, you create one of these types of accelerators to accelerate your customer traffic\. 