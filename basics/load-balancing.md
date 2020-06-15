# Load Balancing

![](../.gitbook/assets/image%20%2845%29.png)

* Client to gateway: DNS parse domain to different ip addresses.
* Gateway to webserver: reverse proxy
* webserver to application server: connection pool
* database load balancing: partition / sharding

How to distribute traffic:

* random, round-robin
* min connection count
* min latency
* based on ip.

