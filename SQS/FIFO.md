FIFO : First In First Out

# Characteristic
- Limited throuput: 300msg/s without batching, 3000 msg/s with batching
- Feature of de-duplication i.e only and exactly 1 send capability.

# DeDuplication
A feature that refuse to send the same message.
## Types of DeDuplication 
- Content-based deduplication: will do SHA-256 hash of the body.
- Message DeDuplication ID based deduplication: Add a unique id to the message

# Message Grouping
Group the queues based on the message group Id.
Each Group's queue will arrive in the same order as it was published.
E.g
```
Producer -> Sends -> 1,2,3,4,5 messages -> groupId = User1 | Consumer -> will reveive -> 1,2,3,4,5 in order -> for groupId = User1
```
I know the example sucks. Will update it when I will be in good mood.
