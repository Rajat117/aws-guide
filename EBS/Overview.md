# Intro
EBS - (Elastic Block Store) Volume is a network drive we can attach to our instances and it persist your data.

> Need - We might loose data in root volumne if instance is terminated
> Locked to specific AZ (Snapshot can make it possible to use EBS in another AZ)

# Rules
- Might have some latency (Its a network storage.Not a physical storage)
- Locked to AZ
- Have a Provisioned quantity (1TB will cost 1TB cost even if use less than that)
- At the creation of instance, you can only select GP2 and IO1.
- You can ls (using command lsblk) the volumes on your SSHed instance but can only enter the root volume.
- We can't access EBS immediately. you will have to mount it first. (Follow AWS guide)
- Can be attached to 1 instance at a time.
  
> Note: We can delete/preserve root volume or even EBS volume by checking/unchecking `Delete on Termination` checkbox in console.

# TYPES
- GP2/GP3 - General Purpose SSD.Cost Effective. 
- IO1/IO2 - Highest Performance SSD. Low Latency. High Throughput
- ST1 - Low cost HDD. Frequently Accessed application. Throughput Intesive workload
- SC1 - Lowest cost HDD. Less Frequently Accessed App.
## Characterized in
- Sizes
- Throughput
- IOPS (I/O Operations per seconds)

> Note: Only GP2/GP3 or IO1/IO2 can be used as root volumes. (The volume where your OS boots)
> Note: EBS are updated frequently.

# Types Deep Dive
## GP Use Case
- Can allocate - 1GiB - 16TiB
- GP2
  - 3IOPS/GiB
  - IOPS - 100 to 16000
  - Burst To - 3000
  - Size of vol & IOPS are linked. [E.g u get `3IOPS/GB` & at `5334 GB u are at the limit(Max IOPS)`]
- GP3
  - IOPS - 3000 IOPS to 16000 IOPS
  - Throughput - 125 MiB/s to 1000 MiB/s
## IO1 Use Case
- 100IOPS/Gib
- Minimum IOPS - 100
- Max IOPS - 64000 (For Nitro) or 32000 (For Others) [Can increase independently from storage size].
- Can Allocate - 4GiB - 16TiB
- Size of volumnes and IOPS are independent.
- Multi-Attach Capability
## ST1 Use Case
- Can Allocate - 500GiB - 16TiB 
- Throughput - 500 MiB/s
## SC1 Use Case
- Can Allocate - 150Gib - 16TiB
- Throughput - 250 MiB/s

# Instance Store 
It is a physical storage attached to your EC2 machine. It is a ephermal storage so u lose data as soon as the instance is stopped.

