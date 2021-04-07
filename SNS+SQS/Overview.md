By combining both SNS & SQS we can leverage the feature of both the service.

# SNS + SQS: Fan Out Pattern
This pattern allows us to have SQS as a subscriber to the SNS topic.

# Benefits
- Fully decoupled, no data loss
- Can add more SQS subscribers later.
- Leverage SQS data persistence, delayed processing & retries.


> Note: SQS queue access policy should allow write from SNS.
> Note: SNS cannot send messages to SQS FIFO queue(Limitation)
