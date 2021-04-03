# Might have some latency
# Locked to AZ
# Have a Provisioned quantity (1TB will cost 1TB cost even if use less than that)
# At the creation of instance, you can only select GP2 and IO1.
# You can ls (using command lsblk) the volumes on your SSHed instance but can only enter the root volume.
# We can't access EBS immediately. you will have to mount it first. (Follow AWS guide)
# Can be a