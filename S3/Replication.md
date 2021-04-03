CRR(Cross Region Replication) & SRR(Server Region Replication)

# Rules
- Must enable versioning in source and destination
- Must give proper IAM permission to both the buckets.

# Characteristic
- Buckets can be im different accounts
- Copying happens asynchronously but it happens quickly

# CRR Use Case
- To have lower latency in some other region
- Replication in other accounts

# SRR Use Case
- To aggregate logs from multiple buckets to single bucket.

# Points to Remember
- Replication will happen only after we enable it (Existing objects won't get copied there)
- Any DELETE operation won't get replicated in S3(Irrespective of deleting an object with or withour marker).
- There is no chaining of replication(I myself don't know what this means)

