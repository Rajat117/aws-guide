# Basic 101
We have 1 `Master Data`
We have 1 `Client Application`
B/W Master and Client App we have a `Writer Endpoint` that helps write into DB.

# Basic 102
We can have auto-scaling `Read Replicas` (Limit = 15)
We have 1 `Client Application` (Same client)
They are load balanced and managed by the `Reader Endpoint` that helps read data from DB

# Basic 103
We have shared storage volume that is auto-expanding(auto-scaling).
