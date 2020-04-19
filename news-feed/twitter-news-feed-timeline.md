# Twitter News Feed \(Timeline\)

## Home Timeline



![](../.gitbook/assets/image%20%2814%29.png)

Each write is fanned out 3 times for redundancy purpose.

We query the Social Graph Service to fan out the write to all the followers.

![](../.gitbook/assets/image%20%2821%29.png)

![](../.gitbook/assets/image%20%285%29.png)

Every write is consist of:

1. tweet ID: the sent tweet
2. user ID: the sender's ID
3. bits: miscellaneous product related bits.

![](../.gitbook/assets/image%20%2817%29.png)

max limit: 800 tweets in your timeline

If you are not a active user \(logged in in the last 30 days\), we don't fan out write into your timeline.

![](../.gitbook/assets/image%20%2810%29.png)

If your cache is empty, we will reconstruct your timeline.



## Search

![](../.gitbook/assets/image%20%289%29.png)

Earlybird is a modified version of Lucene.

Twitter mainly rank the contents based on:

1. Re-tweet
2. Like
3. Reply

![](../.gitbook/assets/image%20%2815%29.png)

The home timeline requires O\(n\) write and O\(1\) read

The search timeline requires O\(1\) write and O\(n\) read

![](../.gitbook/assets/image%20%2827%29.png)

## Improve fanout write

Race condition:

1. Lady gaga sends out tweet
2. I retweet or reply
3. My fanout write is done before Lady gaga's is done.

400 million tweets a day, 4600 tweets a second

Merge home timeline and search timeline.

![](../.gitbook/assets/image%20%283%29.png)

![](../.gitbook/assets/image%20%282%29.png)

Don't fanout write for users with large number of followers. Only do fan out for users with small number of followers.

![](../.gitbook/assets/image%20%2818%29.png)

![](../.gitbook/assets/image%20%2835%29.png)

![](../.gitbook/assets/image%20%2828%29.png)



## Stats

![](../.gitbook/assets/image%20%2812%29.png)

![](../.gitbook/assets/image%20%2832%29.png)

![](../.gitbook/assets/image%20%2830%29.png)

## Reference

1. Timelines at Scale \(APR 03, 2013\): [https://www.infoq.com/presentations/Twitter-Timeline-Scalability/](https://www.infoq.com/presentations/Twitter-Timeline-Scalability/)

