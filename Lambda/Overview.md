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
Its a synchronous invocations of setting up a event that can poll the streams of data from
- Kinesis Data Streams
- DynamoDB Streams
- SQS or SQS FIFO Queue

# Event Source Mapper Scaling
1. Kinesis Data Strams & DymanoDB Streams
2. SQS Standard
3. SQS FIO


# Streams & Lambda
# Queues & Lambda
# SQS & Lambda

> Note: `--innvoation type Event` - async

# Lamdda & IAM Execution
## Some Sample roles
- `AWSLambdaBasicExecutionRole` - Upload logs to CloudWatch.
- `AWSLambdakinesis Execution Role` - Read from Kinesis
- `AWSLambdaDynamo DBExecution Role` - Read from DynamoDB Streams
- `AWSLambdaSQSQueue`- Execution Role Read from SOS
- `AWSLambdaVPCAccessExecution Role` - Deploy Lambda function in VPC
- `AWSXRayDaemonWriteAccess` - Upload trace data to X-Ray.
## Best Practice
- `One Lambda Execution Role` per `Function`

# Lambda Resource Based Policy
Use resource based policy to allow other services to access your Lambda resources.
### Conditions for IAM principal to access Lambda
    - if the IAM policy attached to the principal authorizes it<br />
    OR<br/>
    - if the resource based policy authorizes.

# Environment Variables
## Characteristic
- Can be encrypted using KMS
- Lambda has its own system env variable.

# Logging & Monitoring
## CLoudWatch
AWS Lambda with the help of `AWSLambdaBasicExecutionRole` role, store logs in CloudWatch.
CloudWatch also stores the metric for your lambda function such as 
- Invocation, Duration, Concurrent Execution
- Error Count, throttling, success count
- Async Delivery Failures
- How lagging you are in your streaming of kinesis & dynamoDB
## XRay
For this you will have to<br>
- Enable X-Ray in Lambda (Check X-Ray Tracing option in console)
- Use X-Ray SDK in your code.
- Apply X-Ray Daemon Write IAM Role to your Lambda
- Environment Variable if needed
    - _X_AMZN_TRACE_ID: contains the tracing header
    - AWS_XRAY_CONTEXT_MISSING: by default, LOG_ERROR
    - AWS_XRAY_DAEMON_ADDRESS: the X-Ray Daemon IP_ADDRESS:PORT

# VPC
AWS lambda function by default is not launched in your VPC(Its launched in AWS owned VPC). Therefore your Lambda function can not access resources in your own VPC.
> Note: Deploying a lambda function in your public subnet does not expose it to the public internet.
## How to deploy your Lambda in your own VPC.
- Create & assign your own VPC & SG(Security Groups).
- Lamdba with the help of `AWSLambdaVPCAccessExecutionRole` will create an ENI for you in your each subnet.
## How to expose your Lambda publicly
- By the use of NAT gateway in public subnet
     - NAT gateway in turn will talk to Internet GateWay (IGW).
     - Like this:<br/>
    <pre>
        (Private Subnet) -> (Public Subnet) -> IGW -> WWW <br>
           (Lambda fn)   ->     (NAT)       -> IGW -> WWW
    </pre>

# Performance
## Configuration
- RAM
    - `Min = 128MB` | `Max = 3008MB` (INcreases in the 64MB increment).
    - vCPU - `directlyProportionTo` - RAM
    - 1798MB RAM === 1vCPU
    - After 1798MB RAM you get another vCPU.
    - > Note: For computation heavy function increase RAM
- Timeout
    - `Default = 3sec` | `Min = 1 sec` | `Max = 15mins`  
## Execution Context
A temporary runtime env that initializes any external dependancies of your lambda function.
### Characteristic
- It is maintained for some time in case another Lambda function might have to use it.(Avoid reinitialization).
- It has the `/tmp` directory.
    - Can be used for file write & available for read as well in the Lambda function
    - Max size = `512 MB`;
    - Persistent till the execution time of your function.(Even when the execution context is frozen)
> Note: Inialize entites like db connection outide the functio handler.(It will initialze the entity once. Not every time the function runs - It's nothing new. It is basically the programming pattern.)
## Concurrency
### Chacteristic
- `Max = 1000 concurrent execution`.(To have more. Raise a support ticket).
- Concurrency can be reserved at the function level.
- On passing concurrency limit. Throttle will
    - Return 429 - Throttle Error (For Sync Invoke)
    - Retry automatically & then go to DLQ (For Async Invoke).
### Issues
- Hai ek issue. Samajh nhi aa rha kese samjhau.
### Cold Start
- The  huge time, the first invocation of lambda function can take if it has many dependencies.
- To solve this
    - Concurrency is allocated even before the function is invoked.
    - AWS has already upgraded lamda function to reduce cold start

# Lambda with CloudFormation
## Characteristic
- You can paste your lambda function code in your cloudformation template only if it don't have any external dependencies.
- To refer Lambda function with dependencies(included or not), you can refer it using S3 parameters for Lambda function in template.(You upload file in S3 & refer it in template).

# Lambda Layers
They allow us
## Run Custom Runtime
Languages that don't have support for Lambda
E.g. 
- `C++`
- `Rust`
## Externalize Dependancies
- We can create layers of dependencies that don't change much each tim we update our lambda fn.
- Any other fn can also refer these layers.

# Lambda Versions & Alias
## Versions
As the name indicates we can have version of our lambda function code. Each deployed version is immutable except `$LATEST version`(Can't be changed).
## Aliases
Alias can help you point to different versions.Alias are mutable.
E.g `Dev` Alias can point to `$LATEST` version & `Prod` alias can point to `V1`
- Advantage of Blue/Green Deployment.(I might have mentioned it somewhere else(Probably Stages in Beanstalk) in the doc. Please search for it. I will add a link to that piece of code if I remember this)

# Lambda with CodeDeploy

# Lamda Limits
Per Region
## Execution
- Env Variables can be of upto 4KB
- `/tmp` - has 512MB & can be used for disk space
## Deployment
- Lambda fn
    - Compressed Zip = 50MB
    - Uncompressed Zip = 250MB
    - > Note: Can use the `/tmp` directory to load big files at startup
- Env Variables can be of upto 4KB

> Note: Don't use recursive calls in Lamda function.(It will be dangerous & costly to you)