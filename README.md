# Introduction

I summarize what I learnt about System Design in this gitbook.

* Gitbook: [https://liuzhenglaichn.gitbook.io/systemdesign/](https://liuzhenglaichn.gitbook.io/systemdesign/)
* Github Repo: [https://github.com/lzl124631x/system-design](https://github.com/lzl124631x/system-design)

Reference:

* [https://github.com/donnemartin/system-design-primer](https://github.com/donnemartin/system-design-primer)

## Topics

**EVERYTHING IS A TRADE-OFF**

* Horizontal Scaling vs Vertical Scaling
* Cache
* Load Balancing
* Database replication
* Database partitioning

## Get Started

* [Scalability Lecture at Harvard](https://youtu.be/-W9F__D3oY4?t=5090) the best part I think is from 1:24:53
* [Scalability article](https://www.lecloud.net/tagged/scalability/chrono)
  * Load Balancer + Clones:
    * Purpose: More concurrent requests.
    * HowTo: Stateless Server. Centralized data store for session data \(external DB or external persistent cache\)
  * Database scaling:
    * Purpose: Resolve the query slowness caused by too many data.
    * HowTo: Sharding / Denormalization \(include no more joins in any database query\).
  * Cache:
    * Purpose: Improve read performance.
    * HowTo: in-memory cache like Memcached or Redis.
    * Patterns:
      1. Cached Database Queries. A hashed version of query is the cache key.  

         Issue: Expiration. When one piece of data changes, you need to delete all cached queries which may include that data.

      2. Cached Objects. 
  * Asynchronism:
    * Purpose: don't have to wait and occupy resource.
    * Paradigms:
      * Do expensive work beforehand. Example: dynamic content to static content.
      * Task/Message Queue

## Performance vs scalability

A service is scalable if it results in increased performance in a manner proportional to resources added. Generally, increasing performance means serving more units of work, but it can also be to handle larger units of work, such as when datasets grow.1

Another way to look at performance vs scalability:

* If you have a performance problem, your system is slow for a single user.
* If you have a scalability problem, your system is fast for a single user but slow under heavy load.

## Latency vs throughput

Latency is the time to perform some action or to produce some result.

Throughput is the number of such actions or results per unit of time.

Generally, you should aim for maximal throughput with acceptable latency.

## Availability vs consistency

### CAP theorem

