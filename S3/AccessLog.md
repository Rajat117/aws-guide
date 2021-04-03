We can store the access log for s3 bucket in another s3 bucket.

# Caution | Warning | Beware
- Don't store logs of your s3 bucket is the same bucket. It will create an infinite loop

If you did not get the above message. Here' a small scenario to help you
```
You store something in S3

A log is written for it

For this also a log is written

and so on
```
