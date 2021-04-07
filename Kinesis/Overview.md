A  managed alternative to Apache Kafka. Allows to work on real-time big data such as application log, metrics, IoT.

# Characteristics
- Great for real-time big data.
- Data is automatically replicated to 3 AZ
- Great for streaming processing framework like Sprak, NiFi.

# What do we have in store of Kinesis

## Kinesis Streams:
Low Latency streaming at scale.
### Characteristic
- It divides streams into shards/parts.
- Each shard can store data for up to 7 days. (Default = 1 day).
- To increase throuput and scalability, we can increase the number of shards.
- Data cannot be delete in streams.It gets deleted only after its expiration interval.
- We can replay data by going back in time. It don't get deleted till its expiration interval.
- Multiple app can consume the same streams.

### Shards Characteristic
- Write Per Shard = 1 MB/s or 1000 msgs/s
- Read Per Shard = 2 MB/s
- We are billed on the per shard basis.(So be cautious ther).
- Availability to batch messages.
- Reshard: Increase Number of shards.
- Merging - Decrease Number of shards.
- Records are ordered per shard.


## Kinesis Analytic
Allows to perform analytics on streams using SQL
## Kinesis Firehouse: 
Allows to store stream into other AWS services like S3, Redshit, ElasticSearch.

