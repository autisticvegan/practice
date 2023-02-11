# Design Doordash

## Func Requirements
- Place order
- Matched with nearby dasher
- See location of driver and see location of user

## Capacity Estimates
- Just in US, 400 million people, 10 million active users, 1 order per day per user
- 10 million users, 500 bytes per user = 5 GB
- Payment is outsourced to Stripe
- 500k dashers

## API Endpoints
- create_account(user_info)
- place_order(restaurant, customer_address)

## Notes
- use websockets for updating location
- can use cassandra for speed, but since that's not necessary we canuse MySQL / Postgres with single leader replication (ACID)
- Geosharded database with redis
- longpolling could be worse than websockets, but maybe server side events are better
- 

### Onboarding a restauraunt
- Lat long -> geohash
- index each rest in the proper geoshard (use BTree to locate subpartitions)
#### How does geohash work?
- Uber does it hexagonally
- Redis uses sorted set and we can binary search that
- How to deal with edges? Look at surrounding bounding boxes
- compare to Rtree which can overlap
- Haversine distance, shortest path, graph databases, rely on google maps

### Driver Update Service
- driver table where they are being geosharded to correct instance
- update every 5 seconds
- use consistent hashing for even distribution, also use coordination service, gossip protocol between redis clusters
- write replicas not read replicas on the consistent hashing ring
