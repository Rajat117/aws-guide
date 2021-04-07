Evolved version of CloudWatch Event.<br>
The CloudWatch event uses default Bus created by AWS for your account. Through which we can connect to services existing only in AWS.
The EventBridge allows you to have multiple buses to connect to other partners or (SaaS).

# Characteristic
- Multiple buses
- Cross account bus access
- Custom bus allowed

# Schema Registry
EventBridge analyze the events in your bus and generate a default schema out of it.
## Benefit
- You application code will know in advance how to access it.
## Characteristic
- Can be versioned