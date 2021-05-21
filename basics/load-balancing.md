# Load Balancing

![](../.gitbook/assets/image%20%2849%29.png)

* Client to gateway: DNS parse domain to different ip addresses. \(If we have multiple data centers, DNS will find the geographically closest data center\)
* Gateway to web server: reverse proxy
* web server to application server: connection pool
* database load balancing: partition / sharding

How to distribute traffic:

* random, round-robin
* min connection count
* min latency
* based on ip.

## What if load balancer crashed?

TODO

