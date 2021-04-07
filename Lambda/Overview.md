Lambda is a serverless utility managed by AWS. In Lambda we can write a script or function or code to run on demand on a particular server which we dunn manage and is invisible to us(That's why serverless).

# Characteristic
- Virtual functions means no servers to manage
- They generally have short execution.
- They run on-demand and that's why billed only for that amount of time.
- Scale automatically.
- Can be 
    1. Synchronous
    2. Asynchronous
# Advantages
- Low Price.
- Available for many programming languages.
- Can be monitored using CloudWatch.
- Easy to get more resources per functions (Up to 3 GB/function)
- Increase in RAM -> Increases CPU & Network.

# Lamdba@Edge
It's basically used alongside  CDN (say CloudFront).If we want to trigger a lambda function on each edge location or want to perform request filtering before or after reaching your application.

# Scenarios where it can be used:
- Can use it to change CloudFront request & response. You can perform
    - Viewer request - (As soon as CloudFront receives a request from a viewer).
    - Origin request - (Before sending request to application/origin)
    - Origin response - (After receiving response from the server)
    - Viewer Resoponse - (Before CloudFront fwds the response to the viewer).

# Use Case
- Website Security & Privacy.
- Authorization & Authentication.
- Dynamic Web Application at Edge.
- SEO
- User Tracking & Analytics.

# Event Source Mapping 
Its a technique of setting up a event that can poll the streams of data from
- Kinesis Data Streams
- DynamoDB Streams
- SQS or SQS FIFO Queue
