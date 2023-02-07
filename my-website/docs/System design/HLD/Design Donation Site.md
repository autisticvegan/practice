

- Take in users info



- authentication
- input validation (cc, etc)
- synchronous or asynchronous? asynchronous is better (think queues)
- temporal
- what if payment provider is down?
- how are IDs generated?
- dedupe requests? session id? hash the payload?
- do receipts get sent immediately or are they batched up?
- do we have access to spanner? or clock systems?
- hot shards? (can add more)
- what kind of alarms / dashboards? - cpu, memory, 5xx rate, 4xx rate, outages, service-to-service, queuing lengths, business metrics like throughput?
- fall back mechanisms?
- basically design gofundme