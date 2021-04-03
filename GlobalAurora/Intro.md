It is to replace Aurora Cross Region Read Replica approach with much simpler and in efficient way.

We have 1 DB is primary region.
and can have 5 seondary region (16 replicas per region) with replication less than 1 second which helps in reducing latency alot.

We can promote another region as primary region in less than 1 min(RTO - Recovery Time Objective)
