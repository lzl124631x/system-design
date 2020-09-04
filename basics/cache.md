# Cache

Increase the performance of **read** operations.

Application server cache: local cache. Example: map, leveldb. High performance but hard to scale. Violates stateless server principle.

CDN: static content cache, media/binarries

Independent cache system:

* **Redis**: complex data structure. Built-in high availability
* **Memcache**: simple key-value, high concurrency

## Cache writing policy

write-through: write to cache and db.

write-around: discard cache result, write db

write-back: only write cache, don't write to DB. not consistent.

If the cache content is easy to calculate, use write-through, otherwise, write-around.

Cache eviction policies: LRU, LFU, FIFO.

