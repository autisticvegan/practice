Traditional queues vs LBMBs

Message Queue (JMS / AMQP based)

    Examples: RabbitMQ, Amazon SQS
    Messages are not durable, typically
    Messages are inserted and removed into the queue with low latency
    No ordering guarantee!
    Messages are ACK'ed by consumers before they are removed from the queue.
    Can parallelize at the message level.

Bottom line: Suited for processing messages that are bulky and some delay is acceptable, i.e. offloading computationally expensive work asynchronously. You generally don't care about the ordering of the messages as long as it gets done. Also good if you want routing on a message-by-message basis.


Log-based Message Broker (a.k.a. event stream)

    Examples: Apache Kafka, Amazon Kinesis
    Writes append-only logs to disk. Durable. Offers event replay mechanisms and fault tolerance.
    High throughput of data and distributed. The append-only logs are partitioned by any number of machine nodes you throw at it.
    Ordered. (only at the partition level though - messages across multiple partitions for a single topic have no ordering)

Bottom line: Suited for messages that are quick to process, need some ordering guarantee (with caveats above) and have very high data throughput requirements. Event replay mechanisms and fault tolerance are also nice. Can be slower than traditional message queues due to potential disk reads and routing is not as granular as message queues (no event-based routing, but by partition/topic).