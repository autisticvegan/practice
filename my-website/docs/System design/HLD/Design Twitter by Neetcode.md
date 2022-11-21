Design Twitter by Neetcode

- Read heavy more than write-heavy
- GraphDB 
- Eventual consistency is okay
- Most popular tweets in cache
- To attack latency - sharding, cacheing, CDN is key, also pre-generate newsfeed
- Everytime a new tweet is made, process it and put it in the correct caches (sparkjob) - but not necessarily in all cases (i.e. kim kardashian doesn't need to update all followers feed caches)
- Think about going from batching to streaming (sparrow)
  
### Estimates
- 50 gb data written each day, each write is 1 mb
- 500 m users, 200 m DAU

### API
- CreateTweet(tweet, media) - server timestamps and decides on ID

### Stuff
- sharding - done based on userID, tweet ID doesn't make sense (can just look up one shard which has everything the user follows)

https://blog.twitter.com/engineering/en_us/topics/infrastructure/2022/twitter-sparrow-tackles-data-storage-challenges-of-scale

https://blog.twitter.com/engineering/en_us/topics/infrastructure/2022/stability-and-scalability-for-search

https://blog.twitter.com/engineering/en_us/topics/insights/2022/measuring-the-impact-of-twitter-network-latency-with-causalimpac


https://blog.twitter.com/engineering/en_us
