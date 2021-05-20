# Timeline creation with sharded data

To create the timeline for any given user, one of the most important requirements is to fetch latest photos from all people the user follows. For this, we need to have a mechanism to sort photos on their time of creation. This can be done efficiently if we can make photo creation time part of the PhotoID. Since we will have a primary index on PhotoID, it will be quite quick to find latest PhotoIDs.

We can use epoch time for this. Let’s say our PhotoID will have two parts; the first part will be representing epoch seconds and the second part will be an auto-incrementing sequence. So to make a new PhotoID, we can take the current epoch time and append an auto incrementing ID from our key generating DB. We can figure out shard number from this PhotoID \( PhotoID % 200\) and store the photo there.

## What could be the size of our PhotoID?

Let’s say our epoch time starts today, how many bits we would need to store the number of seconds for next 50 years?

`86400 sec/day * 365 (days a year) * 50 (years) => 1.6 billion seconds`

We would need 31 bits to store this number. Since on the average, we are expecting 23 new photos per second; we can allocate 9 bits to store auto incremented sequence. So every second we can store \(2^9 =&gt; 512\) new photos. We can reset our auto incrementing sequence every second.

