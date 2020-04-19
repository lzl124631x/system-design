# Facebook News Feed

## Fanout method

**Fanout write = Megafeed**

![](https://lh4.googleusercontent.com/Jq6cAjuUnWJHbLWP3rPcr2N5SdQ54pktub2x7v1iReLl0lC9Cu6vBqbmSniGZkeAXCAeOqkkuuRD29K8mBzmxOXDryggxcWbDywGFRjRgD6UYmf38DuAWzXGrbX-iBvrgsNFwWxV)

Pro:

* just one thing to read
* we can do pre-rank.

**Fanout read = Multifeed**

![](../.gitbook/assets/image%20%2811%29.png)

Facebook chose Fanout read \(Multifeed\).

* Write amplification makes the storage needs expensive in Megafeed
  * Write amplification: suppose you have 300 followers, you sending a new post will result in 300 writes to the system. This changes the problem from a tractable dataset that can be saved in memory to a big disk storage problem.
* Developing with read-time aggregation is flexible
  * The developer can simply aggregate the data, apply their algorithms, and see the output right away. It would take longer with fanout write.
* Memory and network easier to engineer around
  * News feed launches in 2005 with fanout write. At that time memory and network weren't that good. The fanout read approach started 2007. Now the hardware is more powerful to support fanout read. 
* Never have huge fan-out write to do, only bounded \(&lt;10k\) fan-out read
  * Justin Bieber problem: with fanout write, when JB sends a new post, we need to write to a million different places. And because facebook's friend relationship is bidirectional, JB's news feed pool will be write a million times if each of his friends sends a new post. But nobody would read one million posts.

![](../.gitbook/assets/image%20%2813%29.png)

## Leaf Nodes

* In-memory \(mostly\) databases
* Do ~40 requests per feed query
  * 10 billion querys per day to the aggregator. So ~400 billion requests per day, about 4.6 million QPS.
* About 50% of the total LOC.

### Leaf node indexes

* Must store a number of users on each leaf
* Once we find a user, we want to scan his/her activity in time order
* Want to have an easy way of adding new activity without locking
* Most natural data structure is a hashtable to a linked list \(map from userId to posts\)

![](../.gitbook/assets/image%20%284%29.png)

![](../.gitbook/assets/image%20%286%29.png)

![](../.gitbook/assets/image%20%2824%29.png)

## Reference

1. Facebook News Feed: Social Data at Scale \(NOV 26, 2012\)
   1. Video: [https://www.infoq.com/presentations/Facebook-News-Feed/](https://www.infoq.com/presentations/Facebook-News-Feed/)
   2. Slide: [https://secure.trifork.com/dl/qcon-newyork-2012/slides/facebook%20news-feed%20qcon%202012.pdf](https://secure.trifork.com/dl/qcon-newyork-2012/slides/facebook%20news-feed%20qcon%202012.pdf)
   3. Talked about how feed data is stored.
2. Scale at Facebook
   1. Video: [https://www.infoq.com/presentations/Scale-at-Facebook/](https://www.infoq.com/presentations/Scale-at-Facebook/)
3. Scalling Memcache at Facebook
   1. [https://www.usenix.org/sites/default/files/conference/protected-files/nishtala\_nsdi13\_slides.pdf](https://www.usenix.org/sites/default/files/conference/protected-files/nishtala_nsdi13_slides.pdf)

