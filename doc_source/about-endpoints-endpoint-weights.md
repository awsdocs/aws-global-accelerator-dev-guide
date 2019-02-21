# Endpoint Weights<a name="about-endpoints-endpoint-weights"></a>

A weight is a value that determines the proportion of traffic that Global Accelerator directs to an endpoint\. Global Accelerator calculates the sum of the weights for the endpoints in an endpoint group, and then directs traffic to the endpoints based on the ratio of each endpoint's weight to the total\.

Weighted routing lets you choose how much traffic is routed to a resource in an endpoint group\. This can be useful in several ways, including load balancing and testing new versions of an application\.

To use weights, you assign each endpoint in an endpoint group a relative weight that corresponds with how much traffic that you want to send to it\. By default, the weight for an endpoint is 128—that is, half of the maximum value for a weight, 255\. Global Accelerator sends traffic to an endpoint based on the weight that you assign to it as a proportion of the total weight for all endpoints in the group:

![\[How relative weights work for endpoints\]](http://docs.aws.amazon.com/global-accelerator/latest/dg/)

For example, if you want to send a tiny portion of your traffic to one endpoint and the rest to another endpoint, you might specify weights of 1 and 255\. The endpoint with a weight of 1 gets 1/256 of the traffic \(1/1\+255\), and the other endpoint gets 255/256 \(255/1\+255\)\. You can gradually change the balance by changing the weights\. If you want Global Accelerator to stop sending traffic to an endpoint, you can change the weight for that resource to 0\.