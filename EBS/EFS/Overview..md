EFS - Elastic File system - Network-File-System.
Flexible with AZ

# Characteristic
- Can share data.
- UseCase - CMS, Data Sharing.
- Uses NSFv4.1 protocol.
- Expensive
- Compatible with only Linux based AMI
- 1000s of concurrent NFS(Net) clients
- 10 GB+ /s throughput
- AWS claims it can grow to Petabyte-scale

# StorageClasses
EFS has a lifecycle manage feature which allows u to move file after N days to their storage classes
## Standard
- For Frequent access
## InFrequent Access (EFS-IA)
- Have a cost to retrive file and lower price to store.
  
Instance Store - Ephemeral storage