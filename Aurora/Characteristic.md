- It has lot of optimizations
- It claims to have 5* performance improvement over MySQL and 3* over Postgres in RDS.
- From 10GB - 64TB. Grows automatically
- Upto 15 replicas (Replication process is fasrer as well)
- Failover handling is much faster.
- Costs 20% more than normal RDS.
- One master takes the write
- Cross Region (not AZ) replication

# Availability
6 copies of data
    - 4 out of 6 needed for write
    - 3 out of 6 needed for reads.
    - self healing (handles bad data cases) with peer to peer replication
    - Storage is striped across 100s of volumes



 