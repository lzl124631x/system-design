# Design a decentralized web crawler

## Question

[https://leetcode.com/discuss/interview-question/system-design/124657/facebook-system-design-a-web-crawler-that-will-crawl-wikipedia](https://leetcode.com/discuss/interview-question/system-design/124657/facebook-system-design-a-web-crawler-that-will-crawl-wikipedia)

We can't use a centralized data store.

We need to deploy the same crawler software on each node and each node will do the job of crawling and storing data. We have 10,000 nodes and each node can communicate with all other nodes. We have to minimize communication and make sure each node does equal amount of work.

## Solution

After a node crawls a page, it will get a list of URLs to crawl next.

The brute force solution would be that this node communicates with all other nodes to see what are the links that haven't been crawled.

A better solution would be that a node use **Consistent Hashing** to determine which node should handle that URL and send the URL to that node. In this way, each node becomes a task assigner, and the communication between nodes are minimized. When a new node is added to the system, some links \(old or new\) will get migrated to the new node. When a node becomes offline, the links assigned to this node will get shared across other nodes.

