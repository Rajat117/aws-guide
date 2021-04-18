Serverless NoSQL DB managed by AWS.
# Characteristic
- Replication across 3 AZ
- Scale to massive workloads automatically
- Fast & Consistent
# Basic

# Types

## DynamoDB - Writing Data
- `Putltem` - Write data to Dynamo DB (create data or full replace)
Consumes WCU
- `Updateltem` – Update data in DynamoDB (partial update of attributes)
Possibility to use Atomic Counters and increase them
- `Conditional Writes`- Accept a write / update only if conditions are respected, otherwise reject
    - Helps with concurrent access to items
    - No performance impact

## DynamoDB – Deleting Data
- `Deleteltem`
    - Delete an individual row
    - Ability to perform a conditional delete
- `Delete Table`
    - Delete a whole table and all its items
    - Much quicker deletion than calling Deleteltem on all items

## DynamoDB – Batching Writes
- `Batch Writeltem`
    - Up to 25 Putltem and / or Deleteltem in one call
    - Up to 16 MB of data written
    - Up to 400 KB of data per item
- Batching allows you to save in latency by reducing the number of API
calls done against DynamoDB
- Operations are done in parallel for better efficiency
- It's possible for part of a batch to fail
, in which case we have the try the failed items (using exponential back-off algorithm)

## Dynamo DB – Reading Data
- `Getltem`
    - Read based on Primary key
    - Primary Key = HASH or HASH-RANGE
    - Eventually consistent read by default
    -  Option to use strongly consistent reads (more RCU - might take longer)
    - ProjectionExpression can be specified to include only certain attributes
- `Batch Getltem`
    - Up to 100 items
    - Up to 16 MB of data
    - Items are retrieved in parallel to minimize latency

## DynamoDB – Query
- Query returns items based on:
    - PartitionKey value (must be = operator)
- SortKey value (=;<,<=,>, >=, Between, Begin) - optional
- FilterExpression to further filter (client side filtering)
- Returns:
    - Up to 1 MB of data
    - Or number of items specified in Limit
- Able to do pagination on the results
- Can query table, a local secondary index, or a global secondary index

## Dynamo DB - Scan
- Scan the entire table and then filter out data (inefficient)
- Returns up to 1 MB of data – use pagination to keep on reading
- Consumes a lot of RCU
- Limit impact using Limit or reduce the size of the result and pause
- For faster performance, use parallel scans:
- Multiple instances scan multiple partitions at the same time
    - Increases the throughput and RCU consumed
    - Limit the impact of parallel scans just like you would for Scans
    - Can use a Projection Expression + FilterExpression (no change to RCU)

# DynamoDB LSI (Local Secondary Index)
Alternate range key for the table
# DynamoDB GSI (Global Secondary Index)
It is used to speed up queries on non-key attributes
Create a new index table
> Note: GSI Idexes can cause throttling(Even if enough WCU are present on the main table). LSI don't do that(They uses WCU & RCU of the main table)

# DynamoDB Concurrency Model
The feature of condition update/delete(like update only if this field is null) makes dynamoDB concurrent database. (Same operation can happen in parallel this way).Dynamo DB is an optimistic locking database. Based on 

# DAX (DynamoDB Accelerator)
It is a great feature that you can leverage to have microsecond latency for your read requests. 
## How it does that
- When we perform a write query in DynamoDB it caches the write in DAX.
- Now on the Read request we retrieve it from the DAX instead of going all the way to DynamoDB.
## Benefits
- Solves Hot Key problem
## Characteristic
- TTL = 5min
- Nodes = Max - 10|Recommended(in Prod) - 3
- Multi AZ
- Encryption option

# DynamoDB Streams
It is a log of changes or operation performed on your table.
## Characteristic
- Retention Period = 24hr
- We can create a duplicate table from these logs (in any other AZ if you want)
- Streams are made of shards(Automatically provisioned by AWS)
## Choose the type of data you want in streams
- KEYS_ONLY
- NEW_IMAGE
- OLD_IMAGE
- NEW_AND_OLD_IMAGES

# DynamoDB TTL
We can delete rows based on TTL we set
## Characteristic
- No extra cost(no use of WCU or RCU).
- TTL is enabled per row (a TTL column gets added with timestamp)
- Deletes expired items withing 48hrs.(Even from GSI/LSI)
- Only option to recover data would be streams.(only if they are not expired as well :joy:)

# DynamoDB CLI
