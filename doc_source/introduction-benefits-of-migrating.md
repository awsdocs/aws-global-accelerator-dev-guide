# Benefits of Using AWS Global Accelerator<a name="introduction-benefits-of-migrating"></a>

AWS Global Accelerator provides the following benefits:

**Instant regional failover**  
Global Accelerator automatically checks the health of the endpoints that are associated with your static IP addresses, and then directs user traffic only to healthy endpoints\. If the health status changes for an endpoint or you change the configuration, Global Accelerator reacts instantly to direct your users to the next healthy endpoint\.

**High availability**  
AWS Global Accelerator has a fault\-isolating design that increases the availability of your applications\. After you provision an accelerator, Global Accelerator allocates for you two IPv4 static addresses that are serviced by independent network zones\. Similar to AWS Availability Zones, these network zones are isolated units with their own set of physical infrastructures, and they service IP addresses from a unique IP subnet\. If one IP address from a network zone becomes unavailable due to IP address blocking by certain client networks, or due to network disruptions, then client applications can retry on the healthy static IP address from the other isolated network zone\.

**Avoidance of TTL delays**  
Some client devices and internet resolvers can cache IP addresses for longer durations than others\. So when you update an IP address to change the configuration, for example, because of a backend failure or a change in routing preferences, you can’t be sure how long it will take before your users have an updated IP address\. When you use Global Accelerator, you don't rely on IP address caches\. So when you make changes to your Global Accelerator configuration, propagation takes only seconds, eliminating potential downtime or delay for your users\.

**Better performance**  
Global Accelerator brings in traffic from the edge location that is closest to your users, by using anycast static IP addresses\. Then the traffic travels over the congestion\-free, redundant AWS global network, which provides an optimal path for applications that run in an AWS Region\. Global Accelerator chooses the best Region based on where your users are located\. All of these factors together create a more consistent experience for your users\. 

**Easy manageability for moving endpoints**  
The IP addresses that you provision in Global Accelerator are static and provide a single fixed entry point to your applications\. This lets your applications easily scale across Availability Zones, or even between Regions, for example, if you want to do blue/green deployment testing for application updates or failover simulations\. You can do all of that without having to update your DNS configurations or make changes to client\-facing applications\. In addition, because you can provide static IP addresses for corporate proxies to use, a company can whitelist your application’s static IP addresses in its firewalls\.

**Fine\-grained control**  
Global Accelerator gives you control so that you can choose exactly how you want to adjust incoming traffic\. You can configure a traffic dial for regional endpoint groups, so that you can increase or decrease traffic for a specific Region, for performance testing, or for application updates\. For each endpoint, you can set a weight that determines the proportion of traffic that Global Accelerator directs to it\. In addition, if you have stateful applications, you can choose to direct all requests from a user to the same backend target, regardless of the source port, to maintain client affinity\. These options give you ongoing fine\-grained control over how Global Accelerator directs your traffic\.