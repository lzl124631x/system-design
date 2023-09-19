# Twitter News Feed (Timeline)

* Home timeline: fan-out write
* Search: fan-out read

## Home Timeline



![](<../.gitbook/assets/image (46).png>)

Each write is fanned out 3 times for redundancy purpose.

We query the Social Graph Service to fan out the write to all the followers.

![](<../.gitbook/assets/image (8).png>)

![](<../.gitbook/assets/image (14).png>)

Every write is consist of:

1. tweet ID: the sent tweet
2. user ID: the sender's ID
3. bits: miscellaneous product related bits.

![](<../.gitbook/assets/image (39).png>)

max limit: 800 tweets in your timeline

If you are not a active user (logged in in the last 30 days), we don't fan out write into your timeline.

![](<../.gitbook/assets/image (23).png>)

If your cache is empty, we will reconstruct your timeline.



## Search

![](<../.gitbook/assets/image (44).png>)

Earlybird is a modified version of Lucene.

Twitter mainly rank the contents based on:

1. Re-tweet
2. Like
3. Reply

![](<../.gitbook/assets/image (22).png>)

The home timeline requires O(n) write and O(1) read

The search timeline requires O(1) write and O(n) read

![](<../.gitbook/assets/image (27).png>)

## Improve fanout write

Race condition:

1. Lady gaga sends out tweet
2. I retweet or reply
3. My fanout write is done before Lady gaga's is done.

400 million tweets a day, 4600 tweets a second

Merge home timeline and search timeline.

![](<../.gitbook/assets/image (52).png>)

![](<../.gitbook/assets/image (17).png>)

Don't fanout write for users with large number of followers. Only do fan out for users with small number of followers.

![](<../.gitbook/assets/image (6).png>)

![](<../.gitbook/assets/image (26).png>)

![](<../.gitbook/assets/image (16).png>)



## Stats

![](<../.gitbook/assets/image (12) (1).png>)

![](<../.gitbook/assets/image (21).png>)

![](<../.gitbook/assets/image (37).png>)

## Reference

1. Timelines at Scale (APR 03, 2013): [https://www.infoq.com/presentations/Twitter-Timeline-Scalability/](https://www.infoq.com/presentations/Twitter-Timeline-Scalability/)
