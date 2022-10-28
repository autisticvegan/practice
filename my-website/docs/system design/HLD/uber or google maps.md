Uber / Google Maps

Functional Requirements:
- Show nearby cars and keep their location up to date
- Once matched, driver and rider should be able to see each
- Optimal route calculation in low latency with both time and distance numbers
(geo-spatial index)
Capacity Estimates
- Push location changes every 3 seconds
- 1 mil active daily riders, 500k active daily drivers
- 20 bytes of data to store per rider / driver in geospatial index
- Sharding (brooklyn)
API Design
- Search (latLng, radius)
- Match (userID, nearbyDriverIDs)
- GetRoute(startLatLng, endLatLng)
Database Schema
- Users(id, email, pw_hash)
- Drivers(id, email, pw_hash, in_ride)
- Rides/Trips(user_id, driver_id, route, time)
- Geospatial index - keeping users and drivers in, which helps with visualization
Architectural Design
- Similar to Yelp

- User should be able to see other drivers in vicinity - quad tree or geohash - normally
partitioned by bounding boxes, so we need something more dynamic - consistent
hashing, coordination service like zookeeper, or gossip protocol (ringpop)
- Need to shard and insure it is up to date, as compared to Yelp, but durability is not as
important, so in memory (redis)
- Push lat long to the right node, and if they leave delete it, locations are being
propagated, redis pushes them notifications through longpoll, websocket, or service
event. Once we know a redis node to pull from, we can sort by stars.
- Uber uses H3 (hexagons)
- Every edge is a road, nodes are nodes. Djikstras algorithm, A*, but these don’t really
work with changing and complex graphs. Contraction Hierarchies (prioritize highways,
prune less important edges and nodes), then precompute distances. Heuristic is how
many shortcut edges need to be added. Segment graph, 15x speedup
- Stream processing with GPS signals in kafka (durability and replayability is important),
use hidden markov model (viterbi algorithm) to predict most likely route since gps signals
are noisy / lossy. Sensor fusion
- Websockets, flink stream processors, saves trips in cassandra db, pk: user_id, sk:
timestamp, Neo4j Graph DB as route cache (uses nodes instead of indices), scales
logarithmically rather than linearly
