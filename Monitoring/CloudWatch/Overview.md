CloudWatch gives us (metric, alarm, logs & event based reaction) - (Monitoring) features to us.
Let's talk about each feature.
# Metrics
A variable to monitor e.g CPUUtilization, Network usage, bandwidth
## Metric have
- Dimension - The attribute of a metric (instanceid, env)
- TimeStamp - You know it.
## Characteristic
- Metrics belong to namespace
- Up to 10 dimensions per metric
- Dashboard to visualize metrics in UI
## EC2 Detailed Monitoring
By default EC2 have metrics happening every `5 minutes` but it can be reduce to lower value at the expense of some money.
> Note: Custom metric will need to be added from within the instance to access memory usage loggin. Its not pushed bydefault
### Benefit
- Can be used to scale ASG prior than `5 minute` monitoring
## Custom Metric
- Ability to define you own metric for your resource
> Note: To change metric resultion (frequency) you will have to use `StorageResolution` API parameter(API used is PutMetricData)

# Alarm
Sending Alarms based on metrics. We can send notification to any service, trigger lambda function & SNS notification.
## Terminologies
### Alarm States
- OK - Nothing is happening
- INSUFFICIENT_DATA - When u dunn have enough datapoints in metric to trigger alarms.
- ALARM - When Alarm threshold has passed.
### Other
- Period - Time in seconds to evaluate the metrics.For High Resolution(`Min=10s` & `Max=30s`)

# Logs
## Characteristic
- Filter logs based on some expressions.
- Log Groups: Group Logs on folder basis
- Log Streams: They are stream of logs within your Log Group.
- Logs can be expired
> Note: To send logs to CloudWatch, IAM permission must be there & shoukd be valid.
- Encryption: Using KMS at rest.
## CloudWatch Agent (Old)
A Agent can be used to send logs from your EC2 instance to Cloudwatch to alter the default behaviour(by default it Cloudwatch don't catch logs from EC2)
### CloudWatch Agent Characteristic
> Note: Make Sure IAM permissions are valid
- Can be setup on-premises too.
## CloudWatch Unified Agent (New)
This agent can collect extra metrics from your EC2 instance part from the logs. 
### CloudWatch Unified Agent Characteristic
- Easy setup using `SSM Parameter Store`(Please search for it on internet. I don't know this myself yet. Just don't want you to slip out on information).
### CloudWatch Unified Agent Collects (At granual level too)
- CPU
- Disk Space
- NetStat
- RAM
- Processes
- Swap Space
- .... etc
## Metric Filter
Can search for specific keywords in logs.
It can be used to trigger alarms
> Note: Filter publish data for events that happens only after we create the alarm.

# Event
Send event to SQS, SNS, trigger lambda function on a particular event in your service
You can have a cronjob as well to trigger event.
It gives u a small JSON doc informing you about the change.
