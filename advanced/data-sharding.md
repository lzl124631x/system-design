# Data Sharding

Assume we want to store the users' photos in our database and shard the data.

## Partitioning based on UserID

We want to keep all data of a user on the same shard. Assume we use 200 shards, we can find the `shardID` by `userID % 200` . Each shard can have its own auto-increment sequence for `photoID`, and we prepend `shardID` to each `photoID` so that each photo has a unique global `photoID`.

### **Issues of this approach**

1. How would we handle hot users? Several people follow such hot users, and any photo they upload is seen by a lot of other people.
2. Some users will have a lot of photos compared to others, thus making a non-uniform distribution of storage.
3. What if we cannot store all pictures of a user on one shard? If we distribute photos of a user onto multiple shards, will it cause higher latencies?
4. Storing all pictures of a user on one shard can cause issues like unavailability of all of the user’s data if that shard is down or higher latency if it is serving high load etc.

## Partitioning based on PhotoID

We can generate globally unique `photoID`s first then find the `shardID` using `photoID % 200`.

### How to generate photoIDs?

ONe solution could be that we dedicate a separate database instance to generate auto-incrementing IDs. This is a Key Generation Service \(KGS\).

### Single point of failure

The KGS is a single point of failure.

One solution is that we define two databases with one generating even numbered IDs and the other generating odd numbered. And we put a load balancer in front of both of these databases to round robin between them and to deal with downtime.

## Plan for future growth of the system

We can use the above partition methods to do logical partition. At early stage of the system, we can store multiple logical partition on the same server. Later as some of the logical partitions grow big, we can migrate them to a separate server.

This can be done using config files or a separate database that map our logical partitions to database servers.



