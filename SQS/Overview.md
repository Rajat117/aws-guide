# Prerequisite Knowledge
We primarily have 2 types of application communication
1. Synchronous - An application talks to another application directly.
E.g. App1 ---DM--> App2
2. Asynchronous - We have a middleware in b/w (usually a queue) through which 2 services communicate indirectly.
E.G App1 --PostIn--> Queue <---RetreiveFrom-- App2

# Intro
It is a managed queue service.

# Terminologies
- Producer - The one which produces messages into the Queue (Can be many).
- Consumer - The one which consumes message from the Queue (Can be many).
- Maximum Receives - The number of times a message can be received by the consumer. Min = 1. Max = 1000.

# Characteristic
- No limit on throughput
- No limit on message
- Default Message Retention Period = 4 days. Max = 14 days. Min = 1 min
- Low latency. Around < 10ms for both publish & consume.
- Max Message size = 256KB

# Types
1. Standard
2. FIFO

# Security
## Encryption
- Client-side encryption
- KMS keys at-rest encryption
- In-flight encryption using HTTPS.
## Access Control
- IAM policies
## SQL Access Policy
- Similar to S3 bucket policies.
- Useful for cross-account access to SQS queues.
- Useful for allowing other services to write to an SQS queue.

# Use Case 
To decouple b/w applications.

# Message Visibility Timeout
A duration in which message polled by one consumer becomes invisible to other consumers.
## Message Visibility Timeout Characteristic
- Can be increased by the consumer
- Min time = 0s. Max time = 12 hrs.

# Dead Letter Queue
When the message is not consumed by a queue for a certain number of time and it crosses [Maximum Receives](#Terminologies) it can be sent to DLQ.
DLQ is useful for debugging purposes.

# Delay Queues
Queues we set a delay on the message for it to be available for consumer.
## Delay Queue Characteristic
- Default is 0 Seconds.
- Default can be set the queue level. Max = 15 min.
- Can be overriden at the send time using `DelaySecond` paramter

# Long Polling
Consumer can wait certain extra seconds when polling for new messages if there are none there or we wanna receive a lot more messages by increasing the polling duration.
## Long Polling Characteristic
- Min = 1 sec;
- Max = 20 sec;
- Can be enabled at queue level.
- Can be overriden at API call level using `WaitTimeSeconds` parameter.

# SQS Extended Client
To send large message we can use SQS Extended Client (a Java library). 
In this we utilize S3 bucket to make our data available to consumer.
## How does this work?
- We upload our large data to S3.
- We send the pointer(a metadata) to that data through SQL queue to our consumer waiting at the other end.

# Must Know APIs
- `CreateQueue`
- `DeleteQueue`
- `PurgeQueue`
- `SendMessage`
- `ReceiveMessage`
- `DeleteMessage`
- `ReceiveMessageWaitTimeSeconds`
- `ChangeMessageVisibility`
- Batch APIs for `SendMessage`, `DeleteMessage`, `ChangeMessageVisibility`
