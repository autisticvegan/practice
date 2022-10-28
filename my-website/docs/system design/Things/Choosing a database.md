

Indexes:
- LSM Trees + SSTables (writes) (compaction, can use bloomfilters when reading)
- B-Trees (reads)

Replication:
- Single Leader replication (ensures not conflicts)
- multi leader replication
- leaderless replication (for this and multi, more throughouput, but write conflicts)

SQL
- Note about normalized / relational data and updates
- Use when correctness is more important than speed (along with relations)

MongoDB
- Not really useful in sys design, but good if you want SQL guarantees with more flexibility

Cassandra
- Wide column data store, flexible schemas, ease of partitioning
- Good for high write volume, consistency is not important, all writes and reads go to same shard
- useful for chat applications

Riak
- Similar to Cassandra but uses CRDTS (conflict free replicated data types)

HBase
- Use when need fast column reads, i.e. youtube thumbnails, sensor readings (images are stored in column)

Memcached and Redis
- Not databases, but good for caches (i.e. geospatial index)

Neo4j
- useful for friends on social media

TimescaleDB / Apache Druid
- sensor data, use LSM trees for fast ingestion, but split into small indexes
- Does not use typical tombstone method

VoltDB
- SQL but completely in memory, expensive and only allows for small datasets

Spanner
- SQL uses GPS clocks in data center to avoid locking by using timestamps to determine order of writes
- very expensive




