# Facebook News Feed

## Fanout method

**Fanout write = Megafeed**

![](https://lh4.googleusercontent.com/Jq6cAjuUnWJHbLWP3rPcr2N5SdQ54pktub2x7v1iReLl0lC9Cu6vBqbmSniGZkeAXCAeOqkkuuRD29K8mBzmxOXDryggxcWbDywGFRjRgD6UYmf38DuAWzXGrbX-iBvrgsNFwWxV)

Pro:

* just one thing to read
* we can do pre-rank.

**Fanout read = Multifeed**

![](../.gitbook/assets/image%20%284%29.png)

Facebook chose Fanout read \(Multifeed\).

* Write amplification makes the storage needs expensive in Megafeed
  * Write amplification: suppose you have 300 followers, you sending a new post will result in 300 writes to the system. This changes the problem from a tractable dataset that can be saved in memory to a big disk storage problem.
* Developing with read-time aggregation is flexible
  * The developer can simply aggregate the data, apply their algorithms, and see the output right away. It would take longer with fanout write.
* Memory and network easier to engineer around
  * News feed launches in 2005 with fanout write. At that time memory and network weren't that good. The fanout read approach started 2007. Now the hardware is more powerful to support fanout read. 
* Never have huge fan-out write to do, only bounded \(&lt;10k\) fan-out read
  * Justin Bieber problem: with fanout write, when JB sends a new post, we need to write to a million different places. And because facebook's friend relationship is bidirectional, JB's news feed pool will be write a million times if each of his friends sends a new post. But nobody would read one million posts.



## Reference

1. [https://www.infoq.com/presentations/Facebook-News-Feed/](https://www.infoq.com/presentations/Facebook-News-Feed/)

