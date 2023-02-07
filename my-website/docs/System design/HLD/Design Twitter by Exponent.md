## Requirements:
1. Creating a tweet
2. Viewing (or generating the timeline)
3. Follow people and interact with tweets
4. edit tweets? media in tweets? search?

## Non-func requires:
1. optimize for reads
2. optimize for influencers
3. high availability
4. low latency (generation of timeline)

## MVP:

### APIs
- POST create tweet
- GET getTweets
- POST follow user
- POST like tweet 

### Design
- users --> load bals --> API servers --> Users&Tweets
-                         Timeline Gen Service
-                         

### How would you load distribute?
- round robin, geo location, consistent hashing

### How does the Timeline Gen work?
- Looks at user and pulls in tweets (cache)
- Influencer service because they have special needs
- Push or pull method? hybrid based off activity

### Followups
- Very popular small subset of tweets that are active, cache