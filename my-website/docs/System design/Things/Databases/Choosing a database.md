# Choosing  Database
1. Is it write heavy or read heavy?
2. Do we want to scale horizontally or vertically?
3. Which of the CAP theorem do we care about?
4. What does the company already use? What are developers familar with (query language)?
5. Is our data small enough to store in memory? What kind of replication do we need? Do we need a graph?

### Indexes:
- LSM Trees + SSTables (writes) (compaction, can use bloomfilters when reading)
- B-Trees (reads)

### Replication:
- Single Leader replication (ensures not conflicts)
- multi leader replication
- leaderless replication (for this and multi, more throughouput, but write conflicts)

### SQL
- Note about normalized / relational data and updates
- Use when correctness is more important than speed (along with relations)

### MongoDB
- Not really useful in sys design, but good if you want SQL guarantees with more flexibility

### Cassandra
- Wide column data store, flexible schemas, ease of partitioning
- Good for high write volume, consistency is not important, all writes and reads go to same shard
- useful for chat applications

### Riak
- Similar to Cassandra but uses CRDTS (conflict free replicated data types)

### HBase
- Use when need fast column reads, i.e. youtube thumbnails, sensor readings (images are stored in column)

### Memcached and Redis
- Not databases, but good for caches (i.e. geospatial index)

### Neo4j
- useful for friends on social media

### TimescaleDB / Apache Druid
- sensor data, use LSM trees for fast ingestion, but split into small indexes
- Does not use typical tombstone method

### VoltDB
- SQL but completely in memory, expensive and only allows for small datasets

### Spanner
- SQL uses GPS clocks in data center to avoid locking by using timestamps to determine order of writes
- very expensive

### Dynamodb
- DynamoDB is optimized for high read loads, and may not perform well for high write loads. If your application requires a large number of writes per second, you may want to consider a database optimized for write-intensive workloads, such as Cassandra.

### CAP🧢
`Consistency
    Every read receives the most recent write or an error.
Availability
    Every request receives a (non-error) response, without the guarantee that it contains the most recent write.
Partition tolerance
    The system continues to operate despite an arbitrary number of messages being dropped (or delayed) by the network between nodes.
    `


