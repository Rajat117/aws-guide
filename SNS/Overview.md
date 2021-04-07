SNS - Simple Notification Service
It is based on the principle of Pub/Sub(Publish/Subscribe)
The source of Publish can be one and receivers can be multiple with the subscription.

# Terminologies
- Publisher - Something which pushes message to SNS.
- Topic - Topic can be a entity for separating same type of notification in a single line. Max - 100000. 
E.g `Transaction` - For all transaction related notification, `Deposit` - For deposit related notification.
- Subscriber - Any entity that has subscribed to recieve the notifications c. Max = 10000000.
    Can be
    - SQS
    - HTTP/HTTPS
    - Lambda
    - Emails/Emails-JSON
    - SMS message
    - Mobile notification

> Note: SNS is already  and can be integrated with lots of AWS services

# Types of Publish
## Topic Publish
- Create Topic
- Create Subscription.
- Publish to the topic
## Direct Publish
- Can publish directly to
    - Endpoint
- Use Case: Google GCM, Apple APNS, Amazon ADM.

# Security
Same as SQS.
