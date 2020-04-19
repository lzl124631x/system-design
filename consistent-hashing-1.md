# Consistent Hashing

## The problem of naive hashing function

A naive hashing function is `key % n` where `n` is the number of servers.

It has two major drawbacks:

1. NOT horizontally scalable. When you add new servers, all existing mapping are broken. It could introduce painful maintenance work and downtime to the system.
2. May NOT be load balanced. If the data is not uniformly distributed, this might cause some servers to be hot and saturated while others idle and almost empty.

## Consistent Hashing

Distributed Hash Table \(DHT\)

It allows distributing data in such a way that minimize reorganization when nodes are added or removed, hence making the system easier to scale up or down.

The key idea is that it's a distribution scheme that DOES NOT depend directly on the number of servers.

In Consistent Hashing, when the hash table is resized, only `k / n` keys need to be remapped, where `k` is the total number of keys and `n` is the total number of servers.

* When a new node is added, it takes shares from a few hosts without touching other's shares
* When a node is removed, its shares are shared by other hosts.

## How it works?

### Basic Setup

Suppose our hash function output range is `[0, INT_MAX]`. We regard the range as a "ring" -- the "Hash Ring".

As shown below, the hashes of the keys scatter on the Hash Ring.

![](.gitbook/assets/image.png)

And we also hash our servers onto the ring. Suppose we have three servers, A, B and C.

![](.gitbook/assets/image%20%281%29.png)

For each key, we find its correponding server by looking closewise. So "Alice" and "Bob" are mapped to server B, and "Casey" is mapped to server A. Server C is idle.

![](.gitbook/assets/image%20%282%29.png)

## Reference

1. [https://www.toptal.com/big-data/consistent-hashing](https://www.toptal.com/big-data/consistent-hashing)





