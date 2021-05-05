# Types Of environment
- Worker Environment
- Web Server Environment

# Deployment Modes
## All at once
In tnis deployment all the instances application is stopped at once & deployed with version 2 or latest code at once too.
### Characteristic
- fastest
- instance are not available to serve traffic for a bit so downtime
- No additional cost
- Good when there are quick deployments.
## Rolling Update
In this deployment it divides the no of instances into batches. Say for 4 instance, 2 batches(bucket -general term) are created each containing 2 instances.
It will first deploy 1st batch & then 2nd & so on..
### Characteristic
- No additional Cost
- you can set Bucket size(Batch size)
- Application runs at below cpacity for some time.
- At some points runs both the version(new & old)
- Duration: Can be long if we have many instances.
## Rolling with additional batches
Same as Rolling but now we will first be allocating extra batch apart from the existing instances.Say for 4 instances, we will first deploy second version to 2 extra instances & perform the rolling on existing instances.
### Characteristic
- Additional Cost (extra instances)
- Can set Bucket size.
- At some points runs both the version(new & old)
- Application don't run below capacity
- Duration: Can be long
- Good for production
## Immutable
Here in this deployment the updated code is deployed on a new temporary ASG. After successfully deploying version 2 on new ASG. It will move the instances on it to the permanent ASG & terminate the v1 on that ASG.
### Characteristic
- Zero Downtime
- High Cost
- Longest Deployment
- Quick rollback(can terminate new ASG)
- Great option for prod
## Blue/Green Deplpyment
I dunn have the mood today to write about it. If you still see this message. I forgot about it. :sweat_smile:

# LifeCycle Policy
Setup a policy which will delete your old bundles from BeanstalkUI
## LifeCycle Policy Characteristc
- Options
    - Time based
    - Space based (Basically Count based)
- The deleted bundle from UI can be retained or deleted from S3.

# Extension
