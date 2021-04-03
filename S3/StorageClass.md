# S3 Standard
General Purpose
## Characteristic
- High durability(99.9999999%)
- High availability(99.99%)
- Sustain 2 concrurent facility failures.
## Use Cases
- For CRM or normal applications

# S3 Standard-Infrequent Access
Suitable for data is less frequenctly accessed, but requires rapid access when needed.
## Characteristic
- High availability(99.9%)
- Same as [this](#S3-Standard)
- But low cost
- Minimum Storage Duration(MSD) = 30 Days
## Use Cases
- Data recovery warehouse or backup option

3. S3 One Zone-Infrequent Access
Same as IA but data is stored in only one AZ
## Characteristic
- Same Durability
- High availability(99.5%)
- Failure in AZ leads to loss of data
- 99.5% availability
- Low latency and high througput
- Suuports SSL for data at transit and encrption at rest
- Low cost compared to IA
- Minimum Storage Duration(MSD) = 30 Days
## Use Cases
- Storing secondary backup copies

4. S3 Intelligent Tiering
## Characteristic
- High availability(99.99%)
- Small low latency and high throuput performance of S3 standard.
- Intelligent enough to move object b/w [S3 Standard](#S3-Standard) and [S3 IA](#S3-Standard-Infrequent-Access) tiers based on their access pattern
- Monitoting and auto tiering fee.
- Minimum Storage Duration(MSD) = 30 Days
## Use Cases
Your call

# Glacier
## Characteristic
- High availability(99.99%)
- Low cost object meant for backup
- Storage for longer term
- Cost = Storage/Month + Retrieval Cost
- Term Change
    - Object --is called-> Archive(Each archive can be up to 40 TB)
    - Bucket --is called-> Vault
- Minimum Storage Duration(MSD) = 90 Days
## Retrievel Options
- Expedited (1-5 min) 
- Standard (3 -5 hrs)
- Bulk (5-12 hrs)
Fee is depedant on time(lesser the time u want to take, the more u have to pay)
## Use Cases
You know

# Glacier Deep Archive
## Characteristic
- Same as [Glacier](#-Glacier)
- Difference is the Retrieval Options and Storage durations
- Minimum Storage Duration(MSD) = 180 Days
## Retrievel Options
- Standard (12 hrs)
- Bulk (48 hrs)
## Use Cases
You know this too

# S3 Reduced Redundancy Storage (deprecated)