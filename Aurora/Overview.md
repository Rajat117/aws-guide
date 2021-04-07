# Intro 
It is a technology owned by AWS.<br>
Not open source. Aurora is compatible with MySQL and Postgres compatible

# Cluster Design
## Basic 101
We have 1 `Master Data`
We have 1 `Client Application`
Between Master and Client App we have a `Writer Endpoint` that helps write into DB (First Master DB).
## Basic 102
We can have auto-scaling `Read Replicas` (Limit = 15)
We have 1 `Client Application` (Same client)
They are load balanced and managed by the `Reader Endpoint` that helps read data from DB (Read Replicas)
> Note : Load Balancing happens at connection level not statement level.
## Basic 103
We have shared storage volume that is auto-expanding(auto-scaling).

## Features
- We can have
  -  1 writer & multiple reader endpoint
  -  1 writer & multiple reader endpoint working in parallel.
  -  Multiple writes - To leverage multiple writes.
  -  Serverless - Let AWS manage most of the things on its own.

> Note: In case of failover of master instane, `Writer Endpoint` starts refering to one of the read replica, thereby making it a master.(So aurora manages failover for us)

# Characteristic
- It has lot of optimizations
- It claims to have `5 * performance` over MySQL and `3 * performance` improvement over Postgres in RDS.
- From 10GB - 64TB. Grows automatically.
- Backup. Min = 1 day. Max = 35 days.
- BackTrack - Go back in time to check a bad commit. 
- Upto 15 replicas (Replication process is faster as well)
- Failover handling is much faster.
- Costs 20% more than normal RDS.
- One master takes the write (Aurora Instance)
  - Since storage is striped across 100s of volumne. There is a central server that takes that write & write it to any of the striped volumne.
  - E.g <br>
    | AZ1 | AZ2 | AZ3 |
    | :---: | :---:| :---: |
    | Master & RR1 | RRn | RR15 |
    | v1, v2, v3, v4| v4...vn | vn+1.... vm|
- Cross Region (not AZ) replication

# Availability
- 6 copies of data
    - 4 out of 6 needed for write
    - 3 out of 6 needed for reads.
    - self healing (handles bad data cases) with peer to peer replication
    - Storage is striped across 100s of volumes

# Security
- Same as [RDS](#RDS-Security-encryption-operation)
- Automated backups, snapshots & replicas are also encrypted.
- You are responsible for protecting the instance with security group.
- You can't SSH into Aurora.
